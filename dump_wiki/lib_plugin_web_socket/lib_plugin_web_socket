!Objectif de cette lib

Cette lib a pour objectif de créer une communication entre l'ui (domoweb) et le plugin pour les messages liés à la configuration du plugin grâce à une page spécial dans l'ui.

!Comment l'inclure dans le plugin
Vous pouvez vous référer à l'exemple wstemplate.py présent sur le dépôt.
!!Importer les lib
{CODE()}from wsuiserver import BroadcastServer
import time
import threading{CODE}
!!Initialiser votre web socket server
{CODE()}
self._wsPort = port
self._log = None
self.serverUI =  BroadcastServer(self._wsPort,  self.cb_ServerWS,  self._log) #
{CODE}
&quot;wsPort&quot; doit être propre à votre plugin, référez vous à la liste des ports déjà utilisés dans la documentation de domogik (network_port)
&quot;cb_ServerWS&quot; fait référence à la fonction de votre plugin qui traitera vos messages.
!!Fonction recevant les messages (cb_ServerWS)
{CODE()}def cb_ServerWS(self, message):
...
...{CODE}
&quot;message&quot; est de type dictionnaire
!!Répondre à un message
{CODE()}self.serverUI.sendAck(ackMsg){CODE}
&quot;ackMsg&quot; est de type dictionnaire
!!Arreter web socket server
{CODE()}self.serverUI.close(){CODE}