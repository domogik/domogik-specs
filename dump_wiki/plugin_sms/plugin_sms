{maketoc}

!Purpose
This plugin allows sending SMS by the telephone bias of your operator.  

Currently the plugin allows using the accounts with the operators:  SFR, Orange and Bouygues.  

If you have a subscription SMS limitless, that will not cost you anything of more.  

If you do not dispose limitless SMS, according to the operator have you the right to some free SMS.  The SMS outside of the free ones will be billed directly by the operator. 

!Package Installation required
{CODE()}
# sudo easy_install mechanize
{CODE}

!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug sms
{CODE}

You just have to reload administration page to see the plugin in the list.

!!Configuration
!!Start plugin
You can now start the plugin (start button).

!!!login
At the level of puts it login:  It is necessary to indicate your login that allows you to connect you on the site of the operator.  

!!!password
At the level of puts it password:  It is necessary to indicate your password that allows you to connect you on the site of the operator.  

!!!phone
At the level of puts it phone:  It is necessary to indicate your telephone number.  

The telephone number must correspond to the one of the account.  (Certain operators carry out this check to transmit the SMS).  

Of more it is necessary to respect the following format: 
* 00336XXXXXXXX 
* 00337XXXXXXXX 
* +336XXXXXXXX 
* +336XXXXXXXX
* 06XXXXXXXX 
* 07XXXXXXXX


!!!operator
At the level of puts it operator:  It is necessary to indicate name of the operateur.  This point is very important for it is according to this parameter that the plugin will tip on the good operator for the transmission of the sms.  

Here the possible values:  
* orange 
* sfr 
* bouygues

!Developper Notes
!!Create a device sms with a name test_sms by example
So create a widget server with the same name test_sms

in the last type url : IP:40405/command/communication/test_sms/send_sms/06XXXXXXXX/votre_message


!!How the online plugin to test of order? 
In a final one, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./sms.py -f
{CODE}

In a final other, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./send.py xpl-cmnd sendmsg.basic “to=XXX,body=YYYYY&quot;
{CODE}

where XXX is the number of the addressee and where YYYYY is the message that must be transmitted


!!!xPL schema
* [http://xplproject.org.uk/wiki/index.php?title=Schema_-_SENDMSG.BASIC|sendmsg.basic]


!!!!Message to send to plugin for send SMS to receiver
To ask a plugin to send a SMS, you should send this __xpl-cmnd__ message :
{CODE()}
SENDMSG.BASIC
{
to=&lt;receiver phone number&gt;
body=&lt;message&gt;g
}
{CODE}


