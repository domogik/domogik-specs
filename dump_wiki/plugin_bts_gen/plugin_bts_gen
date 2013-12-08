{maketoc}

!But
Pallier à l'absence actuelle de l'implémentation des plugins dans Domogik (juin 2011).
Ce plugin est un exemple qui peut être instancié via copie des fichiers et paramétrage de chaque instance via l'IHM

!Fichiers
{CODE()}
# plugin
src/domogik/xpl/bin/bts_gen.py
src/share/domogik/plugins/bts_gen.xml
src/share/domogik/stats/bts/bts.basic-foo.xml  # j'ai mis 'foo' car il sera utilisé par tous et pas à dupliquer donc.
src/share/domogik/url2xpl/bts/on.xml

# widget
src/domogik/ui/djangomodo/core/templates/widgets/dmg_4x3_bts/main.js
src/domogik/ui/djangomodo/core/templates/widgets/dmg_4x3_bts/style.css
{CODE}

!Compatibilité avec Domogik
Ce plugin est développé dans la branche 0.1.0.beta2.bts. Les fichiers ne sont donc présents que dans cette branche.

!Principe de fonctionnement
Une instance de scénario a 2 statuts :
* actif (on) : plugin démarré et scénario actif
* inactif (off) : plugin démarré et scénario en attente d'un ordre d'activation

Au démarrage, une instance de scénario est inactive.

Pour activer une instance &quot;confort&quot; (par exemple), il faut envoyer le message xpl suivant :
{CODE()}
xpl-cmnd
{
...
}
bts.basic
{
scenario=confort
}
{CODE}
L'instance &quot;confort&quot; sera activée, toutes les autres seront désactivées.

Pour envoyer un tel message xpl en ligne de commande :
{CODE()}
cd src/domogik/xpl/bin/
./send.py xpl-cmnd bts.basic &quot;scenario=confort&quot;   
{CODE}

!Configuration d'une instance
!!startup-plugin
Démarrage auto du scénario (il sera tout de même inactif!) avec Domogik

!!input (entrée)
Nom de l'entrée du scénario. Il y 2 possibilités :
* ipx800:&lt;addresse device ipx800&gt;
* onewire:&lt;addresse device onewire de température&gt;

Exemples :
* ipx800:carte1-btn0
* ipx800:carte2-btn3
* onewire:C57B2E020000 
* ...

!!threshold (seuil)
Si (et seulement si) il s'agit d'une entrée onewire de température, il faudra préciser le seuil. Si la valeur de l'entrée est au dessus (&gt;=) du seuil on considérera qu'on est à un état &quot;haut&quot;. En dessous, à un état &quot;bas&quot;.

Exemple : 20

!!Sorties
!!!output-X
Addresse de la sortie n°X. Il a 2 possibilités : 
* ipx800:&lt;addresse device ipx800&gt;
* x10:&lt;addresse device x10&gt;

Exemples :
* ipx800:carte1-led6
* x10:A3
* ...

!!!level-X
Niveau logique que devra avoir la sortie pour l'état &quot;haut&quot; de l'entrée.
Le niveau opposé sera appliqué pour l'entrée à l'état &quot;bas&quot;

!Copier le template pour créer une instance &quot;confort&quot;
__Attention!__ : le nom d'une instance ne doit comporter que des lettres minuscules et faire au maximum 8 caractères!!!

!!Partie plugin
!!!Partie python
Copier le plugin : 
{CODE()}
$ cd src/domogik/xpl/bin
$ cp bts_gen.py confort.py
{CODE}

Editer le fichier confort.py et modifier la ligne suivante :
{CODE()}
INSTANCE_NAME=&quot;bts_gen&quot;                    
{CODE}
en :
{CODE()}
INSTANCE_NAME=&quot;confort&quot;                    
{CODE}

!!!Partie xml
Copier le plugin : 
{CODE()}
$ cd src/share/domogik/plugins/
$ cp bts_gen.xml confort.xml
{CODE}

Editer le fichier confort.xml et modifier :
{CODE()}
  &lt;name&gt;bts_gen&lt;/name&gt;      
{CODE}
en :
{CODE()}
  &lt;name&gt;confort&lt;/name&gt;      
{CODE}

!!!Activer l'instance
Lancer : 
{CODE()}
$ dmgenplug -f confort
{CODE}

!!Partie widget
__Attention! :__ TOUJOURS FAIRE UNE SAUVEGARDE DU FICHIER AVANT MODIFICATION!
Editer le fichier __src/domogik/ui/djangomodo/core/templates/widgets/dmg_4x3_bts/main.js__ tel que décris ci-dessous :

!!!Dans : _init: function() {
Un bouton du widget correspond à un bloc comme ceci :
{CODE()}
            var button1 = $(&quot;&lt;button id='button1' class='button'&gt;A&lt;/button&gt;&quot;);  
            button1.click(function (e) {self.action1();e.stopPropagation();})   
                .keypress(function (e) {if (e.which == 13 || e.which == 32) {self.action1; e.stopPropagation();}});
            this.element.append(button1);
{CODE}

Pour ajouter un bouton, il faudra copier ce bloc en adaptant :
* button1 =&gt; buttonX  (PARTOUT!!!!)
* action1 =&gt; actionX

Pour modifier un libellé, il faut modifier la première ligne :
{CODE()}
var buttonX = $(&quot;&lt;button id='buttonX' class='button'&gt;Mon super libellé&lt;/button&gt;&quot;); 
{CODE}

!!!Plus loin
Si un bouton a été ajouté, ajouter un bloc comme celui-ci :
{CODE()}
        action1: function() {                                                   
            var self = this, o = this.options;                                  
            this.element.startProcessingState();                                
            rest.get(['command', o.devicetechnology, &quot;bts_gen&quot;, &quot;on&quot;],          
                function(data) {                                                
                    var status = (data.status).toLowerCase();                   
                    if (status == 'ok') {                                       
                        self.valid(o.featureconfirmation);                      
                    } else {                                                    
                        /* Error */                                             
                        self.cancel();                                          
                        $.notification('error', data.description);              
                    }                                                           
                }                                                               
            );                                                                  
        },                        
{CODE}
En adaptant :
* action1 =&gt; actionX
* le nom de l'instance :
{CODE()}
rest.get(['command', o.devicetechnology, &quot;bts_gen&quot;, &quot;on&quot;],          
{CODE}
devient pour &quot;confort&quot; :
{CODE()}
rest.get(['command', o.devicetechnology, &quot;confort&quot;, &quot;on&quot;],          
{CODE}

Si une instance est renommée, il faudra adapter le bon bloc de la même manière qu'indiqué juste au-dessus.

!Créer le device et placer le widget
Cette manipulation est à faire UNE SEULE FOIS. Toute modification du widget (ajout de boutons, etc) sera prise en compte en rafraîchissant la page.

!!Créer le device
Créer un device comme ceci : 
{IMG(attId=&quot;307&quot;)}{IMG}

!!Choisir le widget
Sélectionner ce widget et le placer :
{IMG(attId=&quot;306&quot;)}{IMG}

!Annexes
!!Récupérer la dernière version du template &quot;bts_gen&quot;
* se positionner dans le dossier des sources de domogik
* hg pull
* hg update 0.1.0.beta2.bts

!!Insertion des données en base
{CODE()}
$ cd src/tools/packages/                                 
$ ./insert_data.py ../../share/domogik/plugins/bts_gen.xml
Xml file OK                                                                     
Technology bts                                                                  
update...                                                                       
Device type bts.scenario                                                        
add...                                                                          
Device feature model bts.scenario.scenario                                      
M.P={}                                                                          
add...                              
{CODE}

!!Activer le plugin
{CODE()}
$ dmgenplug -f bts_gen
{CODE}