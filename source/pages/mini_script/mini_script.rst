****************
__Mini_Script__
****************


__Objectif__
=============


Lancer une action si une condition est réunie ou non réunie.

__Condition:__
===============


Ces conditions peuvent être:

* device A (=,>,<,!=) valeur X
* device A (=,>,<,!=) valeur X (and, or, !or) device B (=,>,<,!=) valeur Y
* device A (=,>,<,!=) device B

__Action:__
============


Envoyer un message xpl avec l'état True ou False de la scène et éventuellement une commande Rinor

__Description__
================

__IHM:__
*********


Sur 2 pages, une destinée la création, et une pour la gestion des scènes

''-Page Creator:''
  -- Création d'une scène (le plugin scène initialise une class Mscene et l'enregistre dans un fichier)

''-Page Manage:''
  -- Démarrer/arrêter une scène (interne à la class Mscene active ou stop les listener liée aux devices)
  -- Supprimer une scène (le plugin scène stop la Mscene et supprime la ligne du fichier)

__Plugin Scène__
*****************


* Ce plugin crée des objets de class Mscene à partir d'information contenues dans un message XPL
* Ce plugin crée des objets de class Mscene à partir d'information contenues dans un fichier

* Ce plugin gère la suppression des Mscene (stop la class Mscene et la supprime du fichier)

__Script Scène (Class Mscene)__
********************************


''Init:''
 - Enregistre toutes les variables données en argument dans des variables globales à la class MScene.
 - Lance un listener qui écoute les messages adresser à la scène uniquement afin de réceptionner les ordres start/stop
 - Appelle la fonction start

''Start:''
 - Interroge Rinor pour récupérer le latest de la key_stat des devices définis.
 - Lance des listeners qui écoute de façon précise le bus (schema, xpl-trig, device) pour les devices
 - Envoi un message notifiant que la scène est lancée.

''Stop:''
 - Détruit les listeners des devices
 - Envoi un message notifiant que la scène est stoppée.

--TODO--
''Delete''
 - Détruit le listerner de la scene
 - Appelle stop

''cmd_device:''
S'active lorsqu'un message xpl adressé à l'un des devices:
 - Sauvegarde la donnée dans une variable 
 - Lance la fonction de test de condition

''Test:''
 - Vérifie si les tests de la scène sont vrai ou faux:

 - Si vrai:
  -- Envoi un message xpl avec le nom de la scène et la valeur true (message xpl-trig si changement sinon xpl-stat)
  -- Exécute la commande via Rinor si défini (seulement si xpl-trig)

 - Si Faux:
  -- Envoi un message xpl avec le nom de la scène et la valeur false (message xpl-trig si changement sinon xpl-stat)
  -- Exécute la commande Rinor si défini (seulement si xpl-trig)

__Commentaire de dev.__
========================

 IHM
*****


Toutes les informations nécessaires sont dans /base/feature/list


Script (Mscene)
****************

La création d'un script nécessite:

En - les valeurs optionnels et + les valeurs obligatoires

* type_test: Test effectuer entre les 2 conditions (and, or, >, <, !=)

+ rest_server: adresse ip et port (transmiss ip:port) du service REST

+ Device 1 -> - {id_device,key_stat1,test1,value1}: id du premier device a tester, la clé d'entrée (temperature, data...), le test (>, <, !=), la valeur du test (on, off, numérique etc...)

* Device 2 -> - {id_device,key_stat2,test2,value2} idem mais pour un 2eme device

* Commande 1-> - {technologie1, adress_1, value_out1} technologie de la commande de sortie (knx, X10 ...) l'adresse du device, la valeur a commander

* Commande 2-> - {technologie2, adress_2, value_out2}

commande 1 est utilisée si la condition est remplie, sinon c'est la commande 2, l'envoie d'un ordre est optionnel, dans les 2 cas un message xpl sera émit avec l'état de la scène afin qu'elle puisse être réutilisée dans une autre scène.

Plugin
*******

Écoute les messages Xpl

Les messages réceptionnés sont:

-Création: on généré un objet Mscene avec les informations fournie
-Suppression: stop la scène et efface la ligne du fichier de config

 Ajout d'un usage spécifique aux scene:
****************************************


INSERT INTO `core_device_usage` (`id`, `name`, `description`, `default_options`) VALUES
('scene', 'Scene', 'Special for Scene plugin', '{ &amp;quot;actuator&amp;quot;: { &amp;quot;binary&amp;quot;: {&amp;quot;state0&amp;quot;:&amp;quot;False&amp;quot;, &amp;quot;state1&amp;quot;:&amp;quot;True&amp;quot;}, &amp;quot;range&amp;quot;: {&amp;quot;step&amp;quot;:10, &amp;quot;unit&amp;quot;:&amp;quot;%&amp;quot;}, &amp;quot;trigger&amp;quot;: {}, &amp;quot;number&amp;quot;: {} }, &amp;quot;sensor&amp;quot;: {&amp;quot;boolean&amp;quot;: {}, &amp;quot;number&amp;quot;: {}, &amp;quot;string&amp;quot;: {} } }');
