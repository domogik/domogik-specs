.. toctree::



{IMG(attId="366")}{IMG}
*************
Présentation
*************
L'équipe de Domogik est fière de vous annoncer la première version de son application.
Cette version 0.1.0 avait plusieurs objectifs principaux qui furent tous atteints :
* Architecture modulaire et multi-hôtes.
* Prise en compte de plusieurs technologies en simultané grâce au protocole xPL.
* Possibilité de créer des IHMs à volonté. Le coeur de Domogik est totalement séparé de la partie graphique. Ainsi n'importe quelle IHM peut dialoguer avec Domogik en utilisant un point d'entrée unique.
* L'IHM livrée avec Domogik utilise les dernières technologies web.

Huit plugins sont fournis avec cette version :

* ((plugin_onewire|onewire)) : Support de la technologie 1-wire (DS18B20, DS18S20 and DS2401).
* ((plugin_plcbus|plcbus)) : support PlcBus.
* ((plugin_x10_heyu|x10_heyu)) : Support X10 (via heyu).
* ((plugin_ipx800|ipx800)) : support IPX 800 (cartes relai).
* ((plugin_teleinfo|teleinfo)) : les compteurs électriques récents d'EDF sont pris en charge. Vous pouvez ainsi mesurer votre consommation électrique.
* ((plugin_mirror|mirror)) : support du lecteur RFID Mir:ror.
* ((plugin_cidmodem|cidmodem)) : gestion du "caller id" avec un modem.
* ((plugin_wol_ping|wol_ping)) : démarrage à distance d'ordinateurs et ping.

{IMG(attId="367")}{IMG}

{IMG(attId="368")}{IMG}

{IMG(attId="369")}{IMG}

********************
Application Android
********************
Une application appelée `Domodroid <https://market.android.com/details?id=org.panel&amp;feature=search\_result>`_ est disponible sur l'Android Market et est pleinement opérationnelle avec Domogik 0.1.0.

**************
Compatibilité
**************
Partie serveur
===============
Domogik devrait fonctionner sur toutes les distributions GNU/Linux avec Python 2.6/2.7.
Il a été testé par l'équipe de développement sur les systèmes suivants :
* Ubuntu
* Debian
* Archlinux

Les architectures suivantes sont supportées :
* x86 32bits
* x86 64bits
* arm

Partie cliente
===============
Un des navigateurs suivants est nécessaire pour utiliser l'interface web de Domogik :
* Firefox >= 3.6
* Chrome >= 5
Il pourrait y avoir des problèmes avec d'autres navigateurs (si ils n'implémentent pas certaines fonctionnalités du HTML 5).

*****************
Demandes connues
*****************
''Ici sont listées des fonctionnalités non encore opérationnelles et qui seront ajoutées dans les prochaines versions.''
* Gestion des scénarios.
* Les navigateurs de smartphones ne sont pas supportés en intégralité en raison de l'utilisation de fonctionnalité avancées par l'IHM web de Domogik. Une adaptation sera effectuée dans une prochaine version.
* Traductions françaises : Domogik est pourtant un projet dont le cœur de l'équipe de développement est française, mais ayant une volonté d'en faire un projet international, nous avons choisi l'option d'utiliser une langue parlée par un nombre important de personnes.
* Domogik supporte le multi-hôtes mais l'installateur n'est pas encore prêt pour ce type d'installation.
* Certaines fonctionnalités du x10 et du Plcbus ne sont pas encore implémentées (par exemple ''ALL LIGHTS ON'').

*****************
Pour le futur...
*****************
Parlons maintenant un peu du futur de Domogik...

Plusieurs plugins sont en cours de développement pour les prochaines versions (envoi de SMS, Text To Speech, notifications Android et iPhone, Zibase, ...)

Concernant l'interface graphique principale : les personnes qui suivent le projet ont pu remarquer de nombreuses évolutions au niveau de l'organisation des éléments dans l'IHM. Nous avons testé plusieurs configurations et nous avons pensé trouver LA solution : les pages doivent être flexibles, modulaires et adaptées aux besoin de chacun! Mais ceci n'est pas inclus encore dans la version 0.1.0 qui vient de sortir. En effet cette solution est en cours de spécification et de développement. Donc ne râlez pas trop si la version actuelle ne vous convient pas totalement car la prochaine sera vraiment différente !

Concernant les périphériques mobiles (tablettes, smartphones, etc.), la version actuelle n'est pas totalement opérationnelle (sauf Android puisqu'il y a une application dédiée qui a été réalisée). Ainsi nous recherchons des personnes qui seraient intéressées pour développer une version mobile de notre IHM web. D'ailleurs les développeurs de Blackberry / iPhone sont les bienvenus même si ce n'est pas réellement urgent.

Parlons maintenant de la principale fonction manquant encore à Domogik : les scénarios. Nous avons commencé à travailler dessus. Cette fonctionnalité est considérée comme prioritaire et verra le jour dans les toutes prochaines versions.

Pour ce qui est des plugins, ils sont encore intégrés à Domogik pour le moment. Dans le futur Domogik ne contiendra plus de plugins par défaut, nous allons mettre en place un dépôt (avec un outil permettant facilement d'en ajouter et de les mettre à jour).

**************************
Comment signaler un bug ?
**************************
Vous venez de trouver un bug dans cette version et vous souhaitez nous le signaler ? C'est simple, il suffit de suivre [ReportABug|ces instructions].

**************************
Développement des plugins
**************************
Il est actuellement possible de développer vos propres plugins pour Domogik. Il y a plusieurs personnes qui travaillent sur de nouveaux plugins. N'hésitez pas à nous rejoindre, vous trouverez de l'aide sur le canal IRC (#domogik sur freenode) ainsi que `sur le forum <http://forum.domogik.org>`_.