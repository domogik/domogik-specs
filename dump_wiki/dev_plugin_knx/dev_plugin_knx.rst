__Notice : this plugin is still in specication__

.. toctree::




***************************
Installation du plugin KNX
***************************
Installation du BCUSDK
=======================
***********************
Installation du BCUSDK
***********************

Le BCUSDK contient des outils qui permettent la communication entre le PC et le bus via une interface

Pour ubuntu
Installer directement via launchpad
Ajouter dans le fichier /etc/apt/sources.list
.. code-block::
    
    deb http://ppa.launchpad.net/mkoegler/bcusdk/ubuntu YOUR_UBUNTU_VERSION_HERE main 
    deb-src http://ppa.launchpad.net/mkoegler/bcusdk/ubuntu YOUR_UBUNTU_VERSION_HERE main
    
    sudo apt-get update
    sudo apt-get install bcusdk
    


Sinon
.. code-block::
    
    Installer php5 via synaptic
    apt-get install gcc
    apt-get install g++ 
    apt-get install make 
    apt-get install libmysqlclient15-dev 
     
    
    wget http://sourceforge.net/projects/bcusdk/files/pthsem/pthsem_2.0.8.tar.gz
    wget http://sourceforge.net/projects/bcusdk/files/bcusdk/bcusdk_0.0.5.tar.gz
    tar -xzf pthsem_2.0.8.tar.gz 
    tar -xzf bcusdk_0.0.5.tar.gz
    
    cd pthsem-2.0.8/ 
    ./configure 
    make 
    make test 
    make install 
    export LD_LIBRARY_PATH=/usr/local/lib 
    
    cd ..
    cd bcusdk-0.0.5/ 
    ./configure --enable-onlyeibd --enable-eibnetiptunnel --enable-usb -- enable-eibnetipserver --enable-ft12 
    make 
    make install 
    


EIBD est prêt a fonctionner

Les paramètre eibd doivent être rentrer dans le fichier /etc/init.d/knxeibd au niveau de la ligne
.. code-block::
    
    EIBD_DAEMON_OPTS="--pid-file=$EIBD_PIDFILE paramètre
    


par exemple le paramètre peuvent être:
Interface IP: -i -d -D ipt:adressIP
Interface Serie:-i -d -D bcu1:/dev/ttyS0

Une fois paramètrer vous devez faire se lancer EIBD avant domogik, si vous avez défini le lancement automatique de domogik regarder dans /etc/rcX.d/ la valeur de l'ordre de lancement (voir update-rc.d) et définir correctement l'ordre

.. code-block::
    
    sudo update-rc.d knxeibd defaults 19
    


Paramètrage du plugin:
Pour palier a l'absence d'adresse multiple une solution a été adopté:
Un fichier de configuration est placé dans /var/log/domogik/knx.txt

La structure du fichier est la suivante:
datatype: adr_dmg: adr_cmd: adr_stat: end

exemple:
.. code-block::
    
    datatype:DT_Switch adr_dmg:lampe1 adr_cmd:1/1/5 adr_stat:1/1/0 end
    


L'adresse dmg n'a pas de structure propre, un nom un numéro convient a condition qu'il soit unique.

Les datatypes défini sont:
DT_Switch (0 ou 1)
DT_Scaling (Valeur 0-100% code 0-FFh) utilisé pour les variateurs
DT_Percent (valeur en % de 0-250)
DT_UpDown (pour les volets)
DT_Angle (de 0 à 360°)
DT_HCACMode (gestion de chauffage 4 ordres)

Une fois votre fichier de configuration complet vous pouvez démarrer le plugin (le fichier est charger au lancement du plugin) et ajouter vos device dans domogik en indiquant l'adresse adr_dmg

**********
Protocole
**********
Ressources
===========
* Explication des bases : http://www.openremote.org/display/knowledge/Technical+Overview+of+KNX#TechnicalOverviewofKNX-ETSEngineeringToolSoftware

Généralité
===========
* Un émetteur (interrupteur, capteur, etc...) n'émet qu'une seul adresse de groupe.
* Un actionneur peux avoir plusieurs groupes.
* Les adresses de groupes représentent un ordre ou une information. En fait, elle sert de lien entre le ou les émetteurs, et le ou les récepteurs.

***********************
Installation du BCUSDK
***********************

Le BCUSDK contient des outils qui permettent la communication entre le PC et le bus via une interface

Pour ubuntu
Installer directement via launchpad
Ajouter 
.. code-block::
    
    deb http://ppa.launchpad.net/mkoegler/bcusdk/ubuntu YOUR_UBUNTU_VERSION_HERE main 
    deb-src http://ppa.launchpad.net/mkoegler/bcusdk/ubuntu YOUR_UBUNTU_VERSION_HERE 
    
    à votre source.list
    sudo apt-get update
    sudo apt-get install bcusdk
    


Sinon
.. code-block::
    
    Installer php5 via synaptic
    apt-get install gcc
    apt-get install g++ 
    apt-get install make 
    apt-get install libmysqlclient15-dev 
     
    
    wget http://sourceforge.net/projects/bcusdk/files/pthsem/pthsem_2.0.8.tar.gz
    wget http://sourceforge.net/projects/bcusdk/files/bcusdk/bcusdk_0.0.5.tar.gz
    tar -xzf pthsem_2.0.8.tar.gz 
    tar -xzf bcusdk_0.0.5.tar.gz
    
    cd pthsem-2.0.8/ 
    ./configure 
    make 
    make test 
    make install 
    export LD_LIBRARY_PATH=/usr/local/lib 
    
    cd ..
    cd bcusdk-0.0.5/ 
    ./configure --enable-onlyeibd --enable-eibnetiptunnel --enable-usb -- enable-eibnetipserver --enable-ft12 
    make 
    make install 
    


EIBD est prêt a fonctionner

Erreur: lors de mon install sur une Ubuntu server 11.04 j'ai eu l'erreur suivante en lançant eibd:
blablab error loading libraries: libpthsem.so.20 ....

J'ai vite trouver la réponse sur le net et voici la démarche a suivre

la commande ldd /usr/local/bin/eibd affiche les librairies utilisé par eibd et leur emplacement la ligne libpthsem.so.20 affiche not found

Vérifier que libpthsem.so.20 est bien présent dans /usr/local/lib
Éditer le fichier /etc/ld.so.conf et ajouter la ligne:
include /usr/local/lib

Enregistrer et quitter

en root lancer la commande ldconfig

relancer la commande ldd /usr/local/bin/eibd cette fois ci le chemin devrai être correct et eibd fonctionne.


Fonctions
==========
Les fonctions suivantes sont utilisable avec eibd:
groupsocketlisten: éoute le trafic bus en permance
groupwrite, groupswrite: écrit des données sur le bus
groupread: demande une valeur d'une adresse de groupe
groupresponse, groupsresponse: répond à une demande de valeur

les 's' dans les fonctions correspondent à des données courtes, l'absence de s indique une donnée longue.



Messages
=========
Les messages sont constitués de:

L'adresse de l'émetteur (séparé par des .)
L'adresse de groupe (séparé par de /)
Des données (ordre ou état)

* L'adresse de l'émetteur est l'adresse physique
* L'adresse de groupe indique à qui est destiné le message,(sauf en mode prog).

Par exemple, je veux allumer 5 ampoules avec un interrupteur, je les joins tous par la même adresse de groupe.
Mon interrupteur envoie donc 1 sur l'adresse de groupe A/B/C, tous les participants voient passer le télégramme, et les ampoules avec l'adresse de groupe A/B/C s'allument.

Les sorties d'état ainsi que les informations type températures sont diffusées de la même manière.
Dans l'exemple précédent, l'ampoule 1 peut par exemple envoyer son état en B/B/C à chaque modification ou sur demande.


exemple de message vue par groupsocketlisten d'EIBD ou 1/1/1 est un groupe qui commande une sortie A et ou le groupe 2/1/1 est le groupe d'état de cette sortie
.. code-block::
    
    Read from 1.2.1 to 2/1/1   # le module 1.2.1 demande l'état du groupe 2/1/1 qui est l'état de ma lampe
    
    Response from 1.1.2 to 2/1/1: 01 # le module 1.1.2 répond que le 2/1/1 est a 1
    
    Write from 1.2.1 to 1/1/1: 00 # 1.2.1 en déduit que l'action a faire est de mettre a 0 la lampe en commandant le groupe de commande 1/1/1
    
    Write from 1.1.2 to 2/1/1: 00 # le module répond donc en écrivant le groupe 2/1/1 est a 0
    




Type de message
================
*s : short : moins de 6 bits
*l : long : jusqu'à 3 octets

short
******
Utiliser __groupswrite__.

en shell:
.. code-block::
    
    groupswrite ip:127.0.0.1 1/1/1 1
    

Écrit la valeur 1 dans un message de moins de 6bits sur le groupe 1/1/1
long
*****
Utiliser __groupwrite__.
.. code-block::
    
    groupwrite ip:127.0.0.1 1/1/1 1
    

Écrit la valeur 1 dans un message de plus de 6bits sur le groupe 1/1/1


Variation
==========
La variation est une commande "+" ou "-" suivie d'une commande d'arrêt. A ne pas utiliser depuis l'UI donc.
Privilégier les pourcentages.

Comment faire la différence entre un on/off, une montée descente, etc ?
========================================================================
Il n'y a pas de différence, la donnée est la même. Si une adresse de groupe contient un volet et un éclairage, l'envoi d'un 1 sur cette adresse provoquera l'allumage de la lumière et la descente du volet.
                 

Un on/off c'est 0 ou 1
Monter descente c'est 0 ou 1  
           
Varier la lumière + c'est 09 la lumière augmente jusqu'à ce qu'on envoie un 08
Varier la lumière - c'est 01 puis 00 ces 2 message sont en type s
mais on peux aussi envoyer la valeur en % mais ce n'est pas géré par la même adresse de groupe. Même si c'est la même sortie et c'est un message de type long.                                

Les groupes sont des commandes ou des informations.
Par exemple, sur un module de sortie, il est possible de déclencher un allumage ou un allumage-minuterie, en commandant 2 adresses de groupe différente. Par contre l'adresse de groupe qui indique l'état de la lampe sera la même dans les deux cas.

ex:
Pour l'allumage simple envoie 1 à l'adresse 1/2/3
Pour l'allumage-minuterie envoie 1 à l'adresse 1/2/4
L'état de la lampe sera toujours envoyé en 1/3/3


*******************************
Eibd et interactions avec Eibd
*******************************
Ressources
===========
* http://wiki.erazor-zone.de/wiki:projects:linux:eib

******
Tools
******
Wireshark
==========
* https://www.auto.tuwien.ac.at/a-lab/wireshark-plugin-for-knxnet/ip.html

commandes en shell d'EIBD:
groupsocketlisten: affiche tous les messages passant sur le bus jusqu'à interruption.

Les messages sont du type: 
"Write from X.Y.Z to X/Y/Z: Value"
or
"Read from X.Y.Z to X/Y/Z"

"Response from X.Y.Z to X/Y/Z: Value"

groupwrite: envoi un message sur le bus et acquitte avec un:"Send request" puis termine.

Nota: les messages envoyé via le localhost et lu par le localhost on l'adresse 0.0.0 si le message est envoyé par une autre machine via l'interface il prend l'adresse physique de l'interface.
Par exemple si 2 serveurs contrôlent le bus (1 de gestion et 1 de visualisation)

**********************
DPT les plus utilisés
**********************

    * 1.001: switching (on/off) (EIS1)
--    * 3.007: dimming (control of dimmer using up/down/stop) (EIS2)-- Ne pas utilisé dans domogik, en fonction du lag commande incertaine 
--    * 3.008: blinds (control of blinds using close/open/stop)-- Idem ci dessus
    * 5.xxx: 8bit unsigned integer (from 0 to 255) (EIS6)
    * 5.001: scaling (from 0 to 100%)
    * 5.003: angle (from 0 to 360°)
    * 6.xxx: 8bit signed integer (EIS14)
    * 7.xxx: 16bit unsigned integer (EIS10)
    * 8.xxx: 16bit signed integer
    * 9.xxx: 16 bit floating point number (EIS5)
    * 10.001: time (EIS3)
    * 11.001: date (EIS4)
    * 12.xxx: 32bit unsigned integer (EIS11)
    * 13.xxx: 32bit signed integer
    * 14.xxx: 32 bit IEEE 754 floating point number
    * 16.000: string (max 14 ASCII char) (EIS15)
    * 20.102: heating mode (comfort/standby/night/frost) 

***********
Schéma xpl
***********

* xpl-cmnd : utilisé pour exécuter une commande sur le bus : Write,Read,Response
* xpl-trig : utilisé quand la boucle eibd "write" reçoit des "write" (Changement d'état) ou une confirmation de commande
* xpl-stat : utilisé quand eibd reçoit un message de type "Responce" (retour d'un état)

On remplace les / séparateurs de l'adresse de groupe par : afin d'éviter les problèmes avec rest.

xpl-cmnd
=========
.. code-block::
    
    xpl-cmnd
    {
    ...
    }
    knx.basic
    {
    command=<commande knx : Write,Read ou Response>
    group=<addrese du groupe à qui on envoie la commande>
    type=<s|l : short ou long ou none pour un read>
    data: <valeur si write none si read>
    }
    


Exemple : 
.. code-block::
    
    xpl-cmnd
    {
    hop=1
    source=xpl-knx.domogikserver
    target=*
    }
    knx.basic
    {
    command=Write
    group=1:1:1
    type=s
    data=1
    }
    


.. code-block::
    
    xpl-cmnd
    {
    hop=1
    source=xpl-knx.domogikserver
    target=*
    }
    knx.basic
    {
    command=Read
    group=1:1:1
    type=none
    data=none
    }
    



xpl-cmnd
=========
.. code-block::
    
    xpl-cmnd
    {
    ...
    }
    knx.basic
    {
    command=<Write, Write ack, Read, Read ack, Response, Response ack> ack est ajouté pour identifier un ack a d'un xpl-cmnd
    group=<addresse du groupe émettant la réponse>
    type=<s|l : short ou long>
    data=<valeur de la donnée
    }
    


Exemple : 
.. code-block::
    
    xpl-trig
    {
    hop=1
    source=xpl-knx.domogikserver
    target=*
    }
    knx.basic
    {
    command=Write
    group=1:1:1
    type=s
    data=00
    }
    


xpl-stat
=========
.. code-block::
    
    xpl-stat
    {
    ...
    }
    knx.basic
    {
    command=<Responce>
    group=<addresse du groupe émettant la réponse>
    type=<s|l : short ou long>
    data=<valeur de la donnée
    }
    


Exemple : 
.. code-block::
    
    xpl-stat
    {
    hop=1
    source=xpl-knx.domogikserver
    target=*
    }
    knx.basic
    {
    command=Response
    group=1:1:1
    type=s
    data=00
    }
    


((plugin_knx_exemple|Des exemples içi))

***************************
KNX dans DMG maintenant...
***************************
Le problème
============
Actuellement domogik n'intègre dans ça base qu'une seul adresse par device.
Hors en KNX on peu en avoir 2 voir plus.
Il faut donc modifier la base de donnée tel qu'elle existe et celà demande un gros travaille prévue pour la date du: "Un jour"
Il y a aussi le problème que l'interprétation des donnée du bus est laisser a l'appréciation des composants du bus (qui le savent lors de leur programmation) mais qui n'est pas communiqué (le datatype)

Le palliatif
=============
J'ai pensé a un palliatif, afin que l'existant de Domogik puisse faire fonctionner et visualisé correctement les états je vais crée un fichier text de configuration des composant KNX qui permettra d'avoir des adresse d'état et de command pour une même adresse dans domogik.

Ce fichier contiendra l'adresse du device domogik (quelconque) une adresse de commande, une adresse d'état, et le type de donnée.

Ce fichier sera consulter par le plugin afin de faire un lien entre les adresses reçu et les adresses de domogik.

par exemple le fichier serait constitué de ligne semblable a celle ci.
.. code-block::
    
    datatype:on/off\\\\Adr_dmg:193\\\\adr_cmd:1/1/1\\\\adr_stat:1/1/0
    
