Ce plugin permet de réaliser des tests logiques ou de valeur sur des devices et de lancer une action en fonction du résultat.

!Dépendance:

Le plugin n'a aucune dépendance à proprement parler, en fonction de ce que vous voudrez réaliser, il vous faudra ou non installer d'autres plugins.

!!Attention, ce plugin étant en cours de développement et fortement lié a Domoweb, il vous faut aussi la version 'dev' de domoweb.

!Installation du plugin:

Ce plugin est inclus dans les sources, pour l'activer:

dmgenplug scene

!Ajouter une règle:

Pour ajouter une règle, assurez vous que le plugin est lancé, puis rendez vous dans l'onglet 'creator' de l'admin du plugin.

{img fileId=&quot;344&quot;}

Choisir un device à tester avec éventuellement une condition.

Pour ajouter un autre device à tester cliquer sur 'Add another device'.

Une fois tous les devices devant déclencher le test ajoutés, renseigner le champ condition en utilisant les termes device1, device2 etc. (limité a 100)

Des test pouvant être réalisés par exemple:
device1 or device2 --&gt; device1 et device2 doivent avoir un test configuré
device1 and device2 --&gt; device1 et device2 doivent avoir un test configuré
device1 != device2 --&gt; device1 et device2 peuvent avoir un test configuré ou non
(device1 and device2) or device3 --&gt; device1, device2 et device3 doivent avoir un test configurer
(device1 &gt; device2) and device3 --&gt; seul device3 doit avoir un test configuré
True  --&gt; dans ce cas dès qu'un message xpl-trig sera reçu pour l'un des device configurés, les actions &quot;true&quot; seront réalisées (idem si False mais avec les actions False)
....

Vous pouvez ensuite définir la ou les actions à réaliser, pour cela choisir sur quel état de la condition vous voulez réaliser l'action (True ou False) sélectionner le device à commander et sa valeur.

Cliquer sur &quot;Add another action&quot; pour ajouter une autre action (limité a 100 au total)

Option: vous pouvez choisir si la scène sera lancée automatiquement avec le plugin ou non. Cela permet de créer une scène qui devient active grâce a une autre scène.

!!Crée un tache avec des fonctions basées sur l'heure:

Grace au plugin cron vous avez la possiblité de définir des ordres à certaines heures ou sur certaines dates.
Pour l'utiliser dans le plugin Scene il vous faut un device a piloter, c'est pourquoi dans les devices de la technologie Scene vous trouverez un &quot;Fake device&quot; (un device fictif).

Si vous voulez qu'en cas de grosse chaleur l'été vos volets se ferment, définissez une tache cron entre 2 dates qui mettra a true votre Fake device entre ces 2 dates.

Ajouter ce fake device dans l'une des conditions d'une scene.

!!Exemple d'utilisation:
!!!-Arrosage automatique (plugin Scene et plugin Cron):
- Crée un fake device &quot;horraire arrosage&quot; type scene.fake device
- Dans le plugin Cron crée une tache qui comprend les jours ou vous voulez arroser et la plage horraire sur laquel vous autorisé l'arrosage.
- Dans le plugin Scene selectionner votre device &quot;horraire arrosage&quot; test '=' et valeur 'true'
- Ajouter eventuellement une autre condition, par exemple &quot;capteur1.humidity&quot; &lt; '20'
- Selectionner une commande &quot;True&quot;: &quot;arrosage&quot; à on et une commande &quot;False&quot; arrosage à &quot;off&quot;

!!!-Envoyer un sms si l'alarme se déclanche (plugin SMS et plugin Scene)
- Dans le plugin scene selection le device représentant l'état déclenché de votre alarme
- dans une commande True selectionner &quot;command line&quot; et entrer la ligne chemincomplet/./send.py xpl-cmnd sendmsg.basic &quot;to=yourphone,body=&quot;votre message&quot;



