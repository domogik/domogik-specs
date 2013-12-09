prérequis: Tablette android rooté

Objectif:

Transformer une tablette low cost en ecran tactile murale.

Problème:
* L'écran se verrouille a la mise en veille et l'application passe en arriere plan
* La tablette plante après un long moment en veille ou en charge
* Démarrer automatiquement domodroid parce que madame elle sais pas

Solution:
 - Installer unlock qui permet de choisir si l'ecran se verrouille ou non
 - Installer SManager pour crée une tache programmer, pour celà crée un nouveau script 

.. code-block::
    
    #!/system/bin/sh
    su -c reboot
    

 puis dans menu de l'application -> Plus -> Advanced -> Ordonnanceur
 Et programmer le lancement du script a votre convenance (pour moi tous le jour a midi

 - Installer "startup manager" et ajouter domodroid a vos application.
