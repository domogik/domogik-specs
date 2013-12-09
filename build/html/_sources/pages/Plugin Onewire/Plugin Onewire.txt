**************
Plugin Onewire
**************
^La traduction de cette page n'est pas terminée.^
!Plugin onewire
{HTML}&lt;div class="to_dev_or_doc"&gt;
((plugin_onewire_dev|Aller à la page d'information de développement de ce plugin))
&lt;/div&gt;{HTML}
{maketoc}

!!Objectif
Ce plugin permet de communiquer avec des dispositifs 1-Wire.

Pour fonctionner, ce plugin a besoin de OWFS [http://www.owfs.org|OWFS].

Liste des dispositifs pris en charge :
||__Composant__|__Fiche technique__|__Version Domogik__
DS18B20        | http://pdfserv.maxim-ic.com/en/ds/DS18B20.pdf | 0.1.0
DS18S20        | http://pdfserv.maxim-ic.com/en/ds/DS18S20.pdf | 0.1.0
DS2401         | http://datasheets.maxim-ic.com/en/ds/DS2401.pdf | 0.1.0
DS2438         | http://datasheets.maxim-ic.com/en/ds/DS2438.pdf | dev release||

Dans les prochaines versions, d'autres composants seront inclus.

!!Caractéristiques connues
!!!Owfs 2.8p2 et owfs 2.8p3 ne fonctionnent pas très bien avec python.
Veuillez s'il vous plait, utiliser Owfs __2.7p38__ or __2.8p4__ (recommandé).
Owfs __2.8p4__ plante avec python2.7, utilisez une version plus récente ou les sources du dépôt

!Prerequis : installation OWFS
!!Ubuntu/Debian installation
Sur Ubuntu ou Debian, il existe des paquets OWFS (www.owfs.org) mais sont trop vieux. Donc, nous allons obtenir la dernière version des sources et les compiler.

!!!!Outils nécessaires pour compiler OWFS
Pour commencer, nous avons besoin d'un compilateur __C compiler__ pour installer OWFS. Nous utiliserons __gcc__. Pour vérifier si gcc est présent et sa version :
{CODE()}
$ gcc --version
{CODE}
Si gcc est présent c'est Ok, sinon : 
{CODE()}
# apt-get install gcc
{CODE}

Nous avons aussi besoin de make et ed :
{CODE()}
# apt-get install make ed
{CODE}

Ensuite, nous aurons besoin dans __Autoconf__ version 2.57 ou supérieure. Pour voir si elle est disponible:
{CODE()}
$ autoconf --version
{CODE}
Sinon installé-la : 
{CODE()}
# apt-get install autoconf
$ autoconf --version 
version 2.65 
{CODE}

Nous aurons aussi besoin des librairies de développement USB : 
{CODE()}
# apt-get install libusb-dev
{CODE}

Puis, installer swig :
{CODE()}
# apt-get install swig
{CODE}

!!!Owfs
Telecharger OWFS (adapter les lignes à votre version) et extraire le paquet :
{CODE()}
# cd /usr/src
#  wget http://downloads.sourceforge.net/project/owfs/owfs/2.8p4/owfs-2.8p4.tar.gz
# tar xvzf owfs-2.8p4.tar.gz
# cd owfs-2.8p4
{CODE}

Configurer OWFS avec python :
{CODE()}
# ./configure --enable-owpython
# make
As root / with sudo :
# make install
{CODE}

ou télécharger OWFS depuis le dépôt des sources :
{CODE()}
# sudo apt-get install cvs
# cd /usr/src
# cvs -z3 -d:pserver:anonymous@owfs.cvs.sourceforge.net:/cvsroot/owfs co owfs
# cd owfs
{CODE}

Et configurer OWFS avec python :
{CODE()}
# autoreconf -i
# ./configure --with-python 
# make
As root / with sudo :
# make install
{CODE}

OWFS est maintenant installé pour python

!!!!Test OWFS
Pour tester vous devez faire ceci :
{CODE()}
$ python
&gt;&gt;&gt; import ow
&gt;&gt;&gt; print ow.__version__                                                        
2.8p4-1.18                
{CODE}

!!Installation
Les plugins sont installés depuis la page d'administration. Voir ((Installing_the_packages|cette page)) pour plus de détails.

Assurez-vous de bien avoir installer OWFS avant d'installer le plugin.

!!Cablage et norme
Voir [http://owfs.org/index.php?page=wiring-standards]

!!Interfaces Onewire
!!!DS9490R
{img attId="258",stylebox="border",align="center"}

The device address to use for this interface will be __u__

Here is the description on this interface connection :

{img attId="283",stylebox="border",align="center"}

!!!!Permissions

Par défaut, vous devez être en root pour l'accès au réseau OneWire. Pour donner accès à tout le monde sur votre ordinateur et au périphérique OneWire, suivre ces instructions.

En premier lieu, obtenir les identifiants du fournisseur et du produit:
{CODE()}
$ lsusb  | grep DS1490
Bus 006 Device 013: ID 04fa:2490 Dallas Semiconductor DS1490F 2-in-1 Fob, 1-Wire adapter
{CODE}

Ici, l'ID du fournisseur est 04fa et l'identification du produit est 2490 (ils seront les mêmes pour tous les DS1490).

Créer une règle udev pour OneWire dans le fichier __/etc/udev/rules.d/onewire.rules__ :
{CODE()}
SUBSYSTEMS=="usb", ATTRS{idVendor}=="04fa", ATTRS{idProduct}=="2490", SYMLINK+="onewire", MODE="0666"
{CODE}
Si vous n'avez pas de DS9490, vous devez adapter l'ID du vendeur et l'ID du produit.

Il vous suffit de débrancher et rebrancher votre DS9490 disposer d'autorisations sur elle.

!!Configuration du plugin 
!!!Paramètres généraux
{FANCYTABLE(head=&gt;Key~|~Default value~|~Description)}
device~|~u~|~The 1wire device address. The available values are : __u__ (USB controller), __/dev/ttySO__ (serial port (adapter le nombre à votre situation)), __remote_system:3003__ (adresse du serveur OWFS(owserver))
cache~|~''checked''~|~Checked : utiliser le cache. Unchecked : ne pas utiliser le cache. La lecture des données du réseau 1 Wire est une opération lente, si vous lisez beaucoup de données, il pourrait être utile d'utiliser le cache. Pour plus d'information http://owfs.sourceforge.net/caching.html
{FANCYTABLE}


!!!Autres...
Il ya d'autres éléments de configuration qui dépendent des composants. Vous les trouverez dans les chapitres des composants de cette page.


!!DS18B20
!!!Comment le brancher
!!!!Mode parasite
{img attId="46",stylebox="border",align="center"}

!!!!Mode nominal 
{img attId="44",stylebox="border",align="center"}

!!Les éléments de configuration
!!!ds18b20-en
{FANCYTABLE(head=&gt;Key~|~Default value~|~Description)}
ds18b20-en~|~''unchecked''~|~activer (ou non) le support des composants DS18B20.
ds18b20-int~|~60~|~Intervalle entre chaque lecture de composant DS18B20. Si vous souhaitez contrôler la température de votre maison, 60 ou 120s est une bonne valeur. Si vous souhaitez contrôler un endroit où la température peut changer rapidement, vous pouvez mettre une petite valeur (5s par exemple) mais vous devrait mettre __cache__ False pour obtenir des valeurs instantanées.
ds18b20-res (1)~|~12~|~Résolution de la température lue sur le réseau OneWire. Les valeurs possibles sont: 9, 10, 11, 12.
{FANCYTABLE}


__(1)__Notez que la résolution a un impact sur ​​le temps de lecture de la température sur l'appareil. Sur ((Maxim site|http://www.maxim-ic.com/app-notes/index.mvp/id/4377)) vous trouverez ce tableau qui indique le temps pris pour chaque résolution:


{FANCYTABLE(head=&gt;Resolution~|~9 bits~|~10 bits~|~11 bits~|~12 bits)}
Conversion Time (ms) ~|~93.75 ~|~187.5 ~|~375 ~|~750
LSB (°C) ~|~0.5 ~|~0.25 ~|~0.125 ~|~0.0625
{FANCYTABLE}

!!!!Suivi des températures de la maison
Vous pouvez définir __ds18b20-int__ entre 60 secondes et 300 secondes (5 minutes) en fonction de la precison que vous voulez avoir. Moins de 60 secondes est inutile, plus de 300 secondes peut être pas suffisant pour gérer la température.

!!!Création d'un dispositif pour DS18B20
Dans l'administration, aller dans __Organization&gt; Devices__ . Créer un nouveau périphérique comme ceci:
{FANCYTABLE(head=&gt;Field~|~Suggested value~|~Description)}
Name~|~~|~Un nom ("Temperature", "Temp cuisine", ... à vous de voir)
Address~|~~|~L'Identifiant DS18b20 (vous pouvez l'obtenir avec cette commande dans le Helpers : __onewire ds18b20__ qui vous donnera toutes vos DS18B20 détecté)
Feature~|~__1Wire.Thermometer__~|~ 
Usage~|~__Temperature__~|~
Description~|~~|~une petite description (DS18b20, sonde_1 etc)
Reference~|~~|~"DS18B20" (Vous pouvez mettre ce que vous souhaitez)
{FANCYTABLE}


Exemple : 

{img attId="179",stylebox="border",align="center"}

((Setup_your_devices| Attribution des endroits,où vous pouvez maintenant voir la température)):)


!!DS18S20
!!!Difference with DS18B20
The DS18__B__20 component offers 4 resolutions for temperature : 9 ~ 12 bits. The DS18__S__20 offers only a 9bits resolution.

!!!How to plug 
!!!!Parasit mode
.. image:: ../../_static/images/69

!!!!Normal mode
.. image:: ../../_static/images/70

!!!Configuration items
{FANCYTABLE(head=&gt;Key~|~Default value~|~Description)}
ds18s20-en~|~''unchecked''~|~Enabling (or not) DS18S20 components support.
ds18s20-int~|~60~|~The interval between each DS18S20 component reading. If you want to monitor your house temperature, 60 or 120s is a good value. If you want to monitor something where temperature can change quickly, you can put a small value (5s for example) but you will have to set __cache__ to False to get instant values.
{FANCYTABLE}


!!!Configuration examples
See DS18S20 component for the examples.

!!!Creating a device for a DS18S20
See DS18S20 component for the indications.

!!DS2401
!!!How to plug 
!!!!Parasit mode
.. image:: ../../_static/images/63

!!!Configuration items
{FANCYTABLE(head=&gt;Key~|~Default value~|~Description)}
ds2401-en~|~''unchecked''~|~Enabling (or not) DS2401 components support.
ds2401-int~|~5~|~Interval between each DS2401 component reading. The interval to set depends on the usage you will have for DS2401 components.
{FANCYTABLE}

!!!!Opening sensor for a garage door
A garage door is something that takes time to close/open, especially when it has a motor. Opening or closing such a door can take up to 15 seconds, so there is no risk that someone opens and closes your door without being "seen" by the DS2401 component (with a 5 seconds value).

!!!Creating a device for a DS2401
In administration, go to __Organization &gt; Devices__ page. Create a new device like this :

{FANCYTABLE(head=&gt;Field~|~Suggested value~|~Description)}
Name~|~~|~A name
Address~|~~|~The DS2401 idid (you can get it with this helper command : __onewire ds2401__ which will give you all your DS2401 detected)
Feature~|~__1Wire.Serial Number__~|~ 
Usage~|~~|~The appropriate usage (shutter, window, door, ...)
Description~|~~|~a short description (Placement, usage, etc)
Reference~|~~|~the device reference (model, etc)
{FANCYTABLE}


Example : 

{img attId="180",stylebox="border",align="center"}

((Setup_your_devices|Attribute the feature to a place)) and you can now see the status of your DS2401 (present or not)

!!DS2438 in MS-T module (not in 0.1.0 : in dev release)
__Notice : as MS-T is only supported actually, only temperature feature is fully supported.__

{img attId="284",stylebox="border",align="center"}

!!!How to plug 
.. image:: ../../_static/images/290

!!!Configuration items
{FANCYTABLE(head=&gt;Key~|~Default value~|~Description)}
ds2438-en~|~''unchecked''~|~Enabling (or not) DS2401 components support.
ds2438-int~|~60~|~Interval between each DS2438 component reading. Interval to set depends on the usage you will have for DS2438 comopnents.
{FANCYTABLE}

!!!Creating a device for a DS2438Z - temperature
In administration, go to __Organization &gt; Devices__ page. Create a new device like this :

{FANCYTABLE(head=&gt;Field~|~Suggested value~|~Description)}
Name~|~~|~A name
Address~|~~|~The DS2428 id (you can get it with this helper command : __onewire ds2438__ which will give you all your DS18B20 detected)
Feature~|~__1Wire.Thermometer and humidity__~|~ 
Usage~|~__Temperature__~|~
Description~|~~|~a short description (Placement, usage, etc)
Reference~|~~|~the device reference (model, etc)
{FANCYTABLE}


Example : 

{img attId="376",stylebox="border",align="center"}

((Setup_your_devices|Attribute the feature to a place)) and you can now see your temperature.


!!Helpers
''To get an introduction to helpers, you can read the ((Plugins_helpers|Helper documentation)). To use a helper, the plugin must be stopped.''

__Warning :__ for some reasons, it is not a good idea to use both onewire helper and onewire plugin : you could obtain permission issues... These issues could even force you to reboot your computer or wait a long time before using back the plugin or the helper. So, you should only use the helper when the plugin is stopped and shouldn't start the plugin when using the helper. It is a sad thing and we will look how to correct these bug (which is linked to the ''ow'' library). If you have a solution about this, feel free to report it :)

__Notice about  parameter :__  parameter has the same possible values as defined in "configuration &gt; device". For the following examples we will use the "u" device which is Usb adaptor.

!!!onewire all 
__onewire all__ will list all onewire components found on your 1 wire network.

Example : 
{CODE()}
onewire all u
| Family | Component id | Type    |
-----------------------------------
| 28     | C57B2E020000 | DS18B20 |
| 01     | 4507B2130000 | DS2401  |
| 81     | 93702C000000 | DS1420  |
{CODE}

!!!onewire detail  
__onewire detail__ will display all attributes of  component.

Example : 
{CODE()}
onewire detail u C57B2E020000
C57B2E020000 attributes :
- address : 28C57B2E0200005D
- crc8 : 5D
- die : C2
- family : 28
- fasttemp : 25
- id : C57B2E020000
- locator : FFFFFFFFFFFFFFFF
- power : 0
- present : 1
- r_address : 5D0000022E7BC528
- r_id : 0000022E7BC5
- r_locator : FFFFFFFFFFFFFFFF
- temperature : 25.1875
- temperature10 : 25.25
- temperature11 : 25.25
- temperature12 : 25.1875
- temperature9 : 25
- temphigh : 75
- templow : 70
- trim : 56247
- trimblanket : 0
- trimvalid : 0
- type : DS18B20
{CODE}

!!!onewire ds18b20 
__onewire ds18b20__ will display important data about all DS18B20 components found.

Example : 
{CODE()}
onewire ds18b20 u
DS18B20 : id=C57B2E020000
- Temperature : 25.125
- Powered (1) / parasit (0) : 0	
{CODE}

!!!onewire ds18s20 
__onewire ds18s20__ will display important data about all DS18S20 components found.

Example : 
{CODE()}
onewire ds18s20 u
DS18S20 : id=F1F0DB010800
- Temperature : 28.75
- Powered (1) / parasit (0) : 0
{CODE}

!!!onewire ds2401 
__onewire ds2401__ will display important data about all DS2401 components found.

Example : 
{CODE()}
onewire ds2401 u
DS2401 : id=4507B2130000
- Present : 1
{CODE}

!!!onewire ds2438 
__onewire ds2438__ will display important data about all DS2438 components found.

Example : 
{CODE()}
onewire ds2438 u
DS2438 : id=F1F0DB010800
- Temperature : 28.75
- Humidity : 78
{CODE}