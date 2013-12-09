*!Installation du plugin KNX

Installation du BCUSDK
=======================

Le BCUSDK contient des outils qui permettent la communication entre le PC et le bus via une interface, il existe des packages ubuntu par exemple: http://ppa.launchpad.net/mkoegler/bcusdk/

Pour installer a partir des sources:
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
    ./configure --enable-onlyeibd --enable-eibnetiptunnel --enable-usb --enable-eibnetipserver --enable-ft12 
    make 
    make install 
    


Sur ma Ubuntu Server 11.04 j'ai eux uun message d'erreur suivant lorsque j'ai tenté de lancer EIBD:

... error loading libraries: libpthsem.so.20 ....
Pour y remédier

cette ligne de commande montre les si les librairies sont tout présente:
.. code-block::
    
    ldd /usr/local/bin/eibd
    


The line libpthsem.so.20 affiche non trouver

Vérifier si elle est bien présente dans: /usr/local/lib
Editer le fichier /etc/ld.so.conf et ajouter la ligne:
include /usr/local/lib

Puis en tant que root executé:
.. code-block::
    
    ldconfig
    
    restart ldd /usr/local/bin/eibd and this time the path must be correct and eibd will work correctly.
    


EIBD est prêt a fonctionner

Demarrage automatique de EIBD
==============================
Pour démarré automatiquement EIBD avec votre distribution il faut crée un fichier dans /etc/init.d/

par exemple le fichier knxeibd situer dans src/domogik/examples/init/

Vous aurez a adapter la ligne

.. code-block::
    
    EIBD_DAEMON_OPTS="--pid-file=$EIBD_PIDFILE paramétre
    


Par exemple le paramètre peuvent être:
Interface IP: -i -d -D ipt:adressIP
Interface Serie:-i -d -D bcu1:/dev/ttyS0

Pour connaitre les paramètres nécessaire reporté vous a la documentation d'EIBD.

Maintenant que votre fichier est en place on ajoute le script a la liste des executions automatique avec la commande:

.. code-block::
    
    sudo update-rc.d knxeibd defaults XX
    


XX représente l'ordre dans lequel sont démarrer les scripts (plus le chiffre est proche de 0 plus il est lancer tôt.

Votre script doit être lancer avant celui de Domogik sinon le plugin ne pourra démarrer automatiquement.

*************************
Ajouter le KNX a domogik
*************************
Il suffit d'aller dans la partie administration

En mode DEV:
dans une console tapez la commande:
.. code-block::
    
    dmgenplug knx
    


***********************
Paramétrage du plugin:
***********************
Domogik ne sais pas gérer 2 adresses pour un même device, il faut donc passé par un alias.

Dans la zone Administration de domogik, dans le menu plugin KNX, il y a un onglet Special:

{img fileId=328}

En 1 c'est l'adresse qui sera renseigner dans le device Domogik (sont Alias)

En 2 l'adresse du groupe de commande sur le bus

En 3 Le datapoint type du groupe de commande

En 4 Le groupe de retour d'état si il existe

En 5 le datapoint type du groupe d'état.

En 6 si coché, le plugin interrogera la valeur au démarrage du plugin (attention cette fonction peu crée des actions inatendu)

En 7 Une description plus détailler vous permettant de vous retrouver dans votre fichier de configuration (cette ligne est ajouter avant la ligne de configuration

En 8 ce bouton enregistre votre nouvelle ligne de configuration dans le fichier

En 9 ce bouton permet de lire le fichier

Zone 10 affiche le contenu du fichier de configuration

En 11 ce bouton permet de supprimé la ligne indiqué dans la zone 12

Une fois le device renseigner et ajouter, le device sera reconnu par le plugin, pour pouvoir l'affiché dans domogik il faudrat l'ajouter dans la section device de domogik.

****************************************
Paramétrage du plugin (edition manuel):
****************************************
Pour palier a l'absence d'adresse multiple une solution a été adopté:
Un fichier de configuration doit être crée dans:

share/domogik/data/knx/knx.txt

Ce fichier contient des lignes types:
exemple:
.. code-block::
    
    datatype:1.001 adr_dmg:lampe1 adr_cmd:1/1/5 adr_stat:1/1/0 dpt_stat:1.001 check=True end
    


adr_dmg: Cette adresse n'a pas de structure propre, un nom un numéro convient a condition qu'il soit unique dans votre fichier, c'est cette adresse qui devra ensuite est reporté dans la configuration de "device" de domogik

adr_cmd: C'est l'adresse de group qui permet de piloté votre foncton
adr_stat: C'est l'adresse de group qui représente l'état de votre fonction si elle est différente de adr_cmd
datatype: C'est le type de donnée (commune a adr_stat et adr_cmd)
dpt_stat: Si le type de donnée est différent pour le stat (optionel)
check: Si True, le plugin demandera l'état du groups stat a son lancement.

DPT:
||| Réception | OK| Emission | OK | DataPoint Type | Description
| X | OK | X | OK | 1.001 | switching (on/off) (EIS1)
| X | OK | X | OK | 1.008 | blinds control up/down
| X |    | X |    | 3.007 | dimming (control of dimmer using up/down/stop) (EIS2)
| X |    | X | OK | 3.008 | blinds (control of blinds using close/open/stop)
| X | OK | X | OK | 5.xxx | 8bit unsigned integer (from 0 to 255) (EIS6)
| X | OK | X | OK | 5.001 | scaling (from 0 to 100%)
| X | OK | X | OK | 5.003 | angle (from 0 to 360°)
| X | OK | X | OK | 6.xxx | 8bit signed integer (EIS14)
| X | OK | X | OK | 7.xxx | 16bit unsigned integer (EIS10)
| X | OK | X | OK | 8.xxx | 16bit signed integer
| X | OK | X | OK | 9.xxx | 16 bit floating point number (EIS5)
| X | OK | X | OK |10.001 | time (EIS3)
| X | OK | X | OK |11.001 | date (EIS4)
| X | OK | X | OK |12.xxx | 32bit unsigned integer (EIS11)
| X | OK | X | OK |13.xxx | 32bit signed integer
| X | OK | X | OK |14.xxx | 32 bit IEEE 754 floating point number
| X | OK | X | OK |16.000 | string (max 14 ASCII char) (EIS15)
| X | OK | X | OK |20.102 | heating mode (comfort/standby/night/frost) |
| X | OK | X | OK |DT_HVACEib|Gestion HVACMode pour le Hager TB042||

Une fois votre fichier de configuration complet vous pouvez démarrer le plugin (le fichier est charger au lancement du plugin) et ajouter vos device dans domogik

