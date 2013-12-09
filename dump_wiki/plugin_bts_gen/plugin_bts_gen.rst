.. toctree::



****
But
****
Pallier à l'absence actuelle de l'implémentation des plugins dans Domogik (juin 2011).
Ce plugin est un exemple qui peut être instancié via copie des fichiers et paramétrage de chaque instance via l'IHM

*********
Fichiers
*********
.. code-block::
    
    # plugin
    src/domogik/xpl/bin/bts_gen.py
    src/share/domogik/plugins/bts_gen.xml
    src/share/domogik/stats/bts/bts.basic-foo.xml  # j'ai mis 'foo' car il sera utilisé par tous et pas à dupliquer donc.
    src/share/domogik/url2xpl/bts/on.xml
    
    # widget
    src/domogik/ui/djangomodo/core/templates/widgets/dmg_4x3_bts/main.js
    src/domogik/ui/djangomodo/core/templates/widgets/dmg_4x3_bts/style.css
    


***************************
Compatibilité avec Domogik
***************************
Ce plugin est développé dans la branche 0.1.0.beta2.bts. Les fichiers ne sont donc présents que dans cette branche.

***************************
Principe de fonctionnement
***************************
Une instance de scénario a 2 statuts :
* actif (on) : plugin démarré et scénario actif
* inactif (off) : plugin démarré et scénario en attente d'un ordre d'activation

Au démarrage, une instance de scénario est inactive.

Pour activer une instance "confort" (par exemple), il faut envoyer le message xpl suivant :
.. code-block::
    
    xpl-cmnd
    {
    ...
    }
    bts.basic
    {
    scenario=confort
    }
    

L'instance "confort" sera activée, toutes les autres seront désactivées.

Pour envoyer un tel message xpl en ligne de commande :
.. code-block::
    
    cd src/domogik/xpl/bin/
    ./send.py xpl-cmnd bts.basic "scenario=confort"   
    


*****************************
Configuration d'une instance
*****************************
startup-plugin
===============
Démarrage auto du scénario (il sera tout de même inactif!) avec Domogik

input (entrée)
===============
Nom de l'entrée du scénario. Il y 2 possibilités :
* ipx800:<addresse device ipx800>
* onewire:<addresse device onewire de température>

Exemples :
* ipx800:carte1-btn0
* ipx800:carte2-btn3
* onewire:C57B2E020000 
* ...

threshold (seuil)
==================
Si (et seulement si) il s'agit d'une entrée onewire de température, il faudra préciser le seuil. Si la valeur de l'entrée est au dessus (>=) du seuil on considérera qu'on est à un état "haut". En dessous, à un état "bas".

Exemple : 20

Sorties
========
output-X
*********
Addresse de la sortie n°X. Il a 2 possibilités : 
* ipx800:<addresse device ipx800>
* x10:<addresse device x10>

Exemples :
* ipx800:carte1-led6
* x10:A3
* ...

level-X
********
Niveau logique que devra avoir la sortie pour l'état "haut" de l'entrée.
Le niveau opposé sera appliqué pour l'entrée à l'état "bas"

***************************************************************
Copier le template pour créer une instance "confort"
***************************************************************
__Attention!__ : le nom d'une instance ne doit comporter que des lettres minuscules et faire au maximum 8 caractères!!!

Partie plugin
==============
Partie python
**************
Copier le plugin : 
.. code-block::
    
    $ cd src/domogik/xpl/bin
    $ cp bts_gen.py confort.py
    


Editer le fichier confort.py et modifier la ligne suivante :
.. code-block::
    
    INSTANCE_NAME="bts_gen"                    
    

en :
.. code-block::
    
    INSTANCE_NAME="confort"                    
    


Partie xml
***********
Copier le plugin : 
.. code-block::
    
    $ cd src/share/domogik/plugins/
    $ cp bts_gen.xml confort.xml
    


Editer le fichier confort.xml et modifier :
.. code-block::
    
      <name>bts_gen</name>      
    

en :
.. code-block::
    
      <name>confort</name>      
    


Activer l'instance
*******************
Lancer : 
.. code-block::
    
    $ dmgenplug -f confort
    


Partie widget
==============
__Attention! :__ TOUJOURS FAIRE UNE SAUVEGARDE DU FICHIER AVANT MODIFICATION!
Editer le fichier __src/domogik/ui/djangomodo/core/templates/widgets/dmg_4x3_bts/main.js__ tel que décris ci-dessous :

Dans : _init: function() {
***************************
Un bouton du widget correspond à un bloc comme ceci :
.. code-block::
    
                var button1 = $("<button id='button1' class='button'>A</button>");  
                button1.click(function (e) {self.action1();e.stopPropagation();})   
                    .keypress(function (e) {if (e.which == 13 || e.which == 32) {self.action1; e.stopPropagation();}});
                this.element.append(button1);
    


Pour ajouter un bouton, il faudra copier ce bloc en adaptant :
* button1 => buttonX  (PARTOUT!!!!)
* action1 => actionX

Pour modifier un libellé, il faut modifier la première ligne :
.. code-block::
    
    var buttonX = $("<button id='buttonX' class='button'>Mon super libellé</button>"); 
    


Plus loin
**********
Si un bouton a été ajouté, ajouter un bloc comme celui-ci :
.. code-block::
    
            action1: function() {                                                   
                var self = this, o = this.options;                                  
                this.element.startProcessingState();                                
                rest.get(['command', o.devicetechnology, "bts_gen", "on"],          
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
    

En adaptant :
* action1 => actionX
* le nom de l'instance :
.. code-block::
    
    rest.get(['command', o.devicetechnology, "bts_gen", "on"],          
    

devient pour "confort" :
.. code-block::
    
    rest.get(['command', o.devicetechnology, "confort", "on"],          
    


Si une instance est renommée, il faudra adapter le bon bloc de la même manière qu'indiqué juste au-dessus.

************************************
Créer le device et placer le widget
************************************
Cette manipulation est à faire UNE SEULE FOIS. Toute modification du widget (ajout de boutons, etc) sera prise en compte en rafraîchissant la page.

Créer le device
================
Créer un device comme ceci : 
{IMG(attId="307")}{IMG}

Choisir le widget
==================
Sélectionner ce widget et le placer :
{IMG(attId="306")}{IMG}

********
Annexes
********
Récupérer la dernière version du template "bts_gen"
==============================================================
* se positionner dans le dossier des sources de domogik
* hg pull
* hg update 0.1.0.beta2.bts

Insertion des données en base
==============================
.. code-block::
    
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
    


Activer le plugin
==================
.. code-block::
    
    $ dmgenplug -f bts_gen
    
