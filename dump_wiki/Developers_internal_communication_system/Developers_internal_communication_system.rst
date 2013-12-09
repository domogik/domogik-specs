!Système interne de communication

__But__ : refonte du système de communication interne en vue de rationnalisation du code existant / ajout de fonctionnalités supplémentaires.

!! Communication interne
Pour certaines actions internes à Domogik, la communication via xpl est limitée.
L'idée serait d'avoir un second réseau de communication, pour les échanges liés au fonctionnement de Domogik, et n'ayant pas d'intérèt pour les éléments domotiques.
Parmi les fonctionnalités qu'il serait interessant d'avoir:
* pouvoir passer plusieurs types de données, voir des objets
* Chiffrement des données
* Niveaux de priorité entre les messages, avec un niveau 'real time' pour les événements importants
* Gérer des échanges asynchrones de type commande/réponse. Cas pratique : installation d'un package, demande pour désactiver un plugin (pas stopper!), ...
* Gérer des échanges asynchrones de type commande/multiples réponses. Cas pratique : rest demande au manager d'installer un package. Le manager va renvoyer plusieurs réponses en fonction de l'avancement : 20%, 50%, 80%, fini. Ca permet d'avoir un meilleur rendu utilisateur.
* Gérer les absences de réponses à une commande (timeout).

Il serait utile de pouvoir integer les helpers dans ce réseau, de façon à pouvoir bénéficier de plus de fonctionnalités, et de pouvoir reproduire un comportement 'terminal'. 
''Note de Fritz : le cas des helpers est particulier... à voir si c'est vraiment judicieux!''

Ainsi que pour les plugins, d'avoir la possibilité de récupérer des données depuis la base.

!!Flux mixtes xpl/second canal
Dans certains cas il pourrait être judicieux de mixer xpl et le second canal de communication. 

Cas pratique : auto discovery (qui sera implémenté côté plugins dans XplPlugin). Lorsqu'un plugin détecte un device non connu pour sa techno, il envoie un xpl pour le signaler (avec techno/adresse/type/reference). Rest doit intercepter ce message xPL. Ensuite il serait judicieux que ce message soit transformé en message du second canal et soit diffusé. Ainsi les IHMs utilisées (quelles qu'elles soient) pourraient notifier ce nouveau device et proposer de le créer.

!!Limiter le second canal 
Le second canal devrait être limité aux échanges IHMs&lt;=&gt;rest&lt;=&gt;managers. Les plugins doivent utiliser uniquement xpl pour communiquer.

!! Evénements internes
Pour les UI, il serait grandement bénéficiable de pouvoir récupérer (sur tout écran et pas seulement depuis l'admin) toutes sortes d'événements relatifs au fonctionnement de Domogik:
* demarrage/arrêt de plugins
* modification de la base
* installations de packages
* executions de scenarios
* ...
Tout cela au sein d'un même flux d'évenements

!!Logs
Voir si ça pourrait permettre de remonter facilement les logs (à la demande) des différents hôtes vers rest ou les ihms.

!!Notes
Ne pas oublier de prendre en compte Domodroid :
* aspect déconnexion du réseau

