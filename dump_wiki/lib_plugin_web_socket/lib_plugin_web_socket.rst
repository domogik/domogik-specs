**********************
Objectif de cette lib
**********************

Cette lib a pour objectif de créer une communication entre l'ui (domoweb) et le plugin pour les messages liés à la configuration du plugin grâce à une page spécial dans l'ui.

*********************************
Comment l'inclure dans le plugin
*********************************
Vous pouvez vous référer à l'exemple wstemplate.py présent sur le dépôt.
Importer les lib
=================
.. code-block::
    from wsuiserver import BroadcastServer
    import time
    import threading

Initialiser votre web socket server
====================================
.. code-block::
    
    self._wsPort = port
    self._log = None
    self.serverUI =  BroadcastServer(self._wsPort,  self.cb_ServerWS,  self._log) #
    

"wsPort" doit être propre à votre plugin, référez vous à la liste des ports déjà utilisés dans la documentation de domogik (network_port)
"cb_ServerWS" fait référence à la fonction de votre plugin qui traitera vos messages.
Fonction recevant les messages (cb_ServerWS)
=============================================
.. code-block::
    def cb_ServerWS(self, message):
    ...
    ...

"message" est de type dictionnaire
Répondre à un message
======================
.. code-block::
    self.serverUI.sendAck(ackMsg){CODE}
    "ackMsg" est de type dictionnaire
    Arreter web socket server
    ==========================
.. code-block::
    self.serverUI.close(){CODE}