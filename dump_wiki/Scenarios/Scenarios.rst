{maketoc}

Le développement des scénarios se fait dans la branche &quot;scenario&quot;.

Le but est de créer un module indépendant (non inclu dans RINOR). Dans sa première version, celui ci écoutera sur le xPL.
Cette écoute obligera à reparser les XML des plugins. Dès que 0MQ pourra être utilisé, celui ci le sera à la place de xPL.

Les scénarios se découpent en 4 parties :
* condition
* test
* parametre
* action

!Condition

Une condition est une modélisation en JSON d'une expression booléenne regroupant des tests, par exemple : 

{CODE(colors=&quot;python&quot;)}
{ &quot;AND&quot; : {
        &quot;OR&quot; : {
            &quot;one-uuid&quot; : { 
                &quot;param_name_1&quot; : { 
                    &quot;token1&quot; : &quot;value&quot;,
                    &quot;token2&quot; : &quot;othervalue&quot;
                },
                &quot;param_name_2&quot; : { 
                    &quot;token3&quot; : &quot;foo&quot;
                }
            },
            &quot;another-uuid&quot; : {
                &quot;param_name_1&quot; : {
                    &quot;token4&quot; : &quot;bar&quot;
                }
            }
        },
        &quot;yet-another-uuid&quot; : {
            &quot;param_name_1&quot; : {
                &quot;url&quot; : &quot;http://google.fr&quot;,
                &quot;interval&quot; : &quot;5&quot;
            }
        }
    }
}{CODE}

ce qui représente une condition du type &quot;( A OR B ) AND C&quot;, ou, pour reprendre le nommage uuid/paramètre/token : 
{CODE()}
(one-uuid (param_name_1 (token1,token2) OR another-uuid(param_name_1(token4)) AND yet-another-uuid(param_name_1(url,interval)
{CODE}
Chaque &quot;clé&quot; d'une condition peut être : 
* Un opérateur booléen (AND, OR ou NOT), la valeur est alors une &quot;sous condition&quot; (ex. le &quot;OR&quot; ci dessus)
* un identifieur unique d'un test, la valeur est alors une liste de paramètres (ex. les &quot;*-uuid&quot; ci desssus).

!Test
Un test est un objet comparant 2 éléments entre eux. Chaque élément (opérateur de comparaison compris) est appelé &quot;paramètre&quot;.
Aucune intelligence (action de récupération d'un état/d'une donnéeà n'est présente dans les tests. Celle ci est déportée dans les paramètres.

Un test se contente de définir une liste de paramètres ainsi que leurs attributs et d'évaluer les valeurs retournées par les paramètres lorsque cela est nécessaire.

L'évaluation est faite par une méthode devant systématiquement être définie lors de l'ajout d'un nouveau test.
Une classe générique est fournie aux dévelopeurs de test de façon à n'avoir besoin d'écrire que la logique elle même.

Un test ressemble à : 
{CODE(colors=&quot;python&quot;,ln=&quot;1&quot;)}class TextInPageTest(AbstractTest):
    &quot;&quot;&quot; Simple test to check if a word is contained in an url
    &quot;&quot;&quot;

    def __init__(self, log, xpl = None, trigger = None):
        AbstractTest.__init__(self, log, xpl, trigger)
        self.add_parameter(&quot;url&quot;, &quot;url_value.UrlParameter&quot;)
        self.add_parameter(&quot;text&quot;, &quot;text.TextParameter&quot;)

    def evaluate(self):
        &quot;&quot;&quot; Evaluate if the text appears in the content of the page referenced by url
        &quot;&quot;&quot;
        p = self.get_raw_parameters()
        u = p[&quot;url&quot;]
        t = p[&quot;text&quot;]
        if u.evaluate() == None or t.evaluate() == None:
            return None
        else:
            return t.evaluate() in u.evaluate()
{CODE}

Ce test permet de vérifier si un texte est présent dans le contenu récupéré à une url donnée.
Il prend 2 paramètres définis ligne 7 et 8 : 

* un paramètre &quot;url&quot;
* un paramètre &quot;text&quot;

Dans la méthode ''evaluate'', chaque paramètre est évalué par un appel à sa propre méthode ''evaluate''. 
Ce que fait l'évaluation d'un paramètre dépend de chaque paramètre. 

Une valeur doit être renvoyée par cette méthode si le paramètre peut être évalué. 

'''None''' doit être renvoyé si le paramètre n'a pas pu être évalué.

Ici, si l'une des 2 évaluations renvoie '''None''', on retourne  '''None''' à notre tour.
Dans cet exemple, t.evaluate() est supposé retourner le texte à trouver, et u.evaluate() le contenu d'une page web.

Si les 2 valeurs sont retournées, on teste alors si le texte est présent dans le contenu de la page.

La méthode ''evaluate'' d'un test doit renvoyer un booléen si l'évaluation a pu être faite, et '''None''' sinon.

!Parametres

Les paramètres sont les éléments les plus &quot;primitifs&quot; d'un scénario. Ce sont les éléments de base représentant un &quot;objet&quot;.
Un paramètre possède un certain nombre d'attributs pouvant être configurés. 

Le nombre de paramètres sera probablement un ensemble fini assez restreint, on peut par exemple penser aux paramètres suivants :

* Chaine de caractère
* Url/page web
* opérateur de comparaison (&lt;,&gt;,=, etc ...)
* Etat d'un device domototique
* Etc ...

Un paramètre a un certain nombre d'attributs :

* un type : c'est une description &quot;en un mot&quot; de ce que fait le paramètre. Son but premier est de permettre aux UIs d'adapter la saisie (par exemple, un type &quot;text&quot; ou un type &quot;device&quot; pourra être présenté différemment). Il n'y a pas de contrainte explicite sur cet attribut, il est cependant bon de limiter le nombre de valeurs différentes entre les paramètres si cela n'est pas nécessaire.
* Une liste de valeurs (facultatif) : Cette liste sera fournie aux UIs pour leur permettre de restreindre le choix aux utilisateurs. 
* Une liste de filtres (facultatif) : Idem que précédemment, ceci a pour but de permettre aux UIs de fournir unemodélisation la plusprécise possible. Cette liste de filtre (sous forme de clé: valeur) devrait permettre aux UIs de restreindre certains choix (par exemple, forcer un housecode dans un sous ensemble).
* Une valeur par défaut (facultatif) : Idem que précédemment, l'UI devrait présélectionner cette valeur si elle existe
* Des '''entrées''' : Ces entrées définissent la liste des attributs du paramètre. L'UI devra récupérer cette liste et permettra à l'utilisateur de définir une valeur pour chaque attribut, afin de configurer le paramètre. Par exemple, pour un paramètre &quot;chaine de caractère&quot;, un seul attribut sera nécessaire : la chaîne. Pour un paramètre de type &quot;url&quot;, 2 attributs seront nécessaires : l'url et l'interval entre chaque récupération du contenu. Une entrée est spécifiée par :
** son nom
** son type (de même que le type des paramètres) est un mot permettant de préciser le type de l'attribut pour adapter la présentation de la saisie
** une description en quelques mots sur ce que devrait contenir l'attribut.

Un exemple de paramètre est :
{CODE(colors=&quot;python&quot;,ln=&quot;1&quot;)}class UrlParameter(AbstractParameter):
    &quot;&quot;&quot; This parameter looks periodically at some URL and return the content of the page
    &quot;&quot;&quot;

    def __init__(self, log, xpl, trigger = None):
        AbstractParameter.__init__(self, log, xpl, trigger)
        self.set_type(&quot;url&quot;)
        self.add_expected_entry(&quot;urlpath&quot;, &quot;string&quot;, &quot;Url the script will fetch&quot;)
        self.add_expected_entry(&quot;interval&quot;, &quot;integer&quot;, &quot;Interval between 2 fetch in second&quot;)
        self.set_default_value(&quot;interval&quot;, &quot;10&quot;)
        self._result = None
        self._event = Event()
        self._fetch_thread = Thread(target=self._fetch,name=&quot;UrlParameter.fetch&quot;)
        self._fetch_thread.start()

    def _fetch(self):
        &quot;&quot;&quot; This method will fetch the url peridodically and put the result in self._result
        It whould be called in some thread
        &quot;&quot;&quot;
        while not self._event.is_set():
            p =  self.get_parameters()
            if &quot;urlpath&quot; in p:
                try:
                    u = urlopen(p[&quot;urlpath&quot;])  
                except:
                    self._log.warn(&quot;urlopen : Exception occured : %s&quot; % sys.exc_info()[0])
                    self._result = None
                else:
                    self._result = &quot;\n&quot;.join(u.readlines())
                    self.call_trigger()
            if &quot;interval&quot; in p:
                self._event.wait(int(p[&quot;interval&quot;]))
            else:
                self._event.wait(10)

    def evaluate(self):
        &quot;&quot;&quot; return contents of url or none&quot;
        &quot;&quot;&quot;
        return self._result

    def destroy(self):
        &quot;&quot;&quot; Destroy fetch thread
        &quot;&quot;&quot;
        self._event.set()
        self._fetch_thread.join()
{CODE}

Ce paramètre étend d'une classe permettant de fournir les fonctionnalités de base.

Le constructeur effectue la configuration du paramètre, à savoir :
* défini un type &quot;url&quot; (pouvant permettre une vérification du format aupèrs des UI
* ajoute 2 attributs :
** urlpath, de type &quot;string&quot;, décrit comme &quot;Url that will be fetch&quot;
** interval, de type integer, décrit comme l'interval entre 2 fetch
* défini la valeur par défaut de l'interval à &quot;10&quot;.

De plus, quelques configurations propre à ce paramètre sont ajoutées (création d'un event, et démarrage d'un thread pour la méthode _fetch).

La méthode ''_fetch'' est une méthode propre à ce paramètre, qui contient la logique du paramètre. C'est une boucle qui récupère le contenu de l'url toutes les X secondes

La méthode ''evaluate'' surcharge celle de la classe parent, et se contente de retourner le contenu de la page web (initialisé à '''None''' dans le constructeur).

La méthode ''destroy'' surcharg celle de la classe parent, elle permet d'ajouter des actions à effectuer à l'arrêt du scénario (ici, arrêter le thread).


!Fonctionnement 

Le &quot;workflow&quot; d'un scénario est supposé être le suivant : 

# L'utilisateur demande la création d'une nouvelle condition par l'UI
# L'UI récupère la liste des tests et de leurs paramètres auprès du module de scénario (avec proxy via RINOR ou via la MQ éventuellement)
# Le module renvoie la liste des tests avec pour chacun les paramètres nécessaires
# L'UI permet à l'utilisateur, via un outil de modélisation, de créer une expression booléenne.
## Lorsque l'utilisateur veut créer un test, l'UI devra :
* Modéliser ce test pour l'utilisateur (avec les éventuelles restrictions/précisions définies pour les paramètres)
* Demander au module (avec proxy via RINOR ou via la MQ éventuellement, de façon asynchrone ou non) de créer une instance de ce test. Le module renverra alors un identifiant unique pour cette instance. Il n'est pas nécessaire que le module crée l'instance à ce moment là, mais seulement lors de la réalisation de la condition
# Lorsque l'utilisateur a modélisé sa condition, l'UI génère le JSON et l'envoie au module, qui se chargera alors de :
## Créer les tests et les associer aux uuids
## Créer la condition avec le JSON et la liste des tests

Il reste encore à préciser la façon dont les actions seront déclenchées. Vraissemblablement, un objet &quot;Action&quot; va être créé, utilisant lui aussi les paramètres.
Une liste d'actions (paramétrée) pourra alors être associée à une condition donnée pour définir un scénario complet.
Chaque action pourra, à travers le gestionnaire de scénario, récupérer les valeurs des paramètres entrés par l'utilisateur ou récupérées par le systeme.


!Exemples:
Si la luminosité intérieur est inférieure à la luminosité extérieure alors que les volets sont fermés et que l'utilisateur veut allumer la lumière alors on ouvre les volets de la pièce

Si la luminosité est supérieure a x% et que la température est supérieure à x°C alors on ferme les volets de la façade (1 ou plusieurs volets selon les technologies)

Si l'heure est comprise entre 22h et 3h et que le % d'humidité est inférieur a X% mettre l'arrosage en route

Si la fenêtre est ouverte mettre le chauffage hors-gel.

Mettre le chauffage hors-gel dans toute les pièces communicantes avec une pièce dont la fenêtre est ouverte.

Si la température intérieure est supérieure à 23°C et la température extérieure inférieure à 20°C alors mettre la VMC en marche forcée

Si l'alarme se déclenche, enregistrer avec les caméras IP, envoyer un E-mail et envoyer un SMS et appeler un N° prédéfini dans Asterisk

Si je mets l'alarme en route et qu'une fenêtre est ouverte, fermer le volet de la fenêtre

S'il manque un élément sur le mirro:r j'active la messagerie Asterisk de l'utilisateur concerné

Si un élément revient sur le mirro:r je fais des annonces via les Nabaz:tag (mail, appel en absence, nb de message)

Si un élément reviens sur le mirro:r et qu'un est déjà présent je l'annonce via les Nabaz:tag

S'il n'y a plus d'élément sur le mirro:r j'active l'alarme, je mets le chauffage en température réduite

Thermostat :
Si (jour de la semaine / : ex:dimanche) alors laisser température normale (cteN à atteindre) entre 9h et 22h
Si (jour de la semaine / : ex:lundi) alors laisser température normale (cteN à atteindre) entre 7h et 9h et..   sinon température basse(CteB à atteindre).
Test régulier température thermostat &gt; CteN ou CteB), vérifie heure et jour alors redemarrage ou arret chauffage,  
Trois valeurs définies pour chauffage :  CteN, CteB, CteHG (hors gel).
CteHG pour les absences prolongées ou vacances.
Quatre boutons-poussoir minimun : CteHG pendant x heures (ou jours), CteN, CteB, Prog1 (suit les si, si, si des exemples précédents) 
