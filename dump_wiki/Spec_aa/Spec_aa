{maketoc}

! Communication link security
How to secure the link between the client, and the MQ? SSL?
Maybe we can differenciate local links (plugins, core, ...) and external links (UI, remote dmg servers)

! Authentication (Identify the client)

!!Cereal's idea

!!! req/rep
user (physical person) =&gt; rest:
- digest hash in http header
- inside rest do the authentication and authorization on the request
- create a hash (digest)
- send the zmq message to hadnle the request
zmq receiver:
- authenticathe the hash
- check authorizzation
- do action
- reply
!!! pub/sub
no solution yet, depends on the routing, if we use an mq router, this one can handle AA for pub/sub

!!!hash generation
~~#C00:Do not see the need for hash as it no more secure than user/pass~~
yes it is, as we generate the a new hash for every request we will not be vulnerable for
*reply attacks
*password sniffing (as the password is not sent over the line)
*(partly) men in the middle attacks

sender:
- generate hash
- store hash in authentication storage
- send message

receiver:
- check hash in authentication storage
- do action

hash keys:
- timestamp in minuts (so the hash is only valid for one minuts) (NOT sure about this ....)
- username
- hashed user password that is stored in the db
- random key (from domogik config)

!!! use cases
!!!! request coming in from over rest url
# rest authenticates the user
# rest check authorization
* if ok =&gt; do action
* if nok =&gt; sent http 404
# do the action

if the action is a zmq action, add an authenticator in the zmq message identifying this user (coming from the rest url)

on receive of the zmq message:
# check the authenticator to do authorzation and authentication
# do the action
# send response back

!!!! action coming from scenarios
# scenarios is another user
# so admin decides what actions a scenario user can take, the same flowchart applies as in a request coming from rest

{IMG(attId=&quot;440&quot;)}{IMG}

!Authorization (What the client can do)
!!Cereal's idea
authorization is based on user/groups and acls, a user can have multiple groups and a group can have multiple acls.

!!!What is an ACL
An acl or access control list is an identification to either an command, sensor or a whole device. Together with this linking a couple of fields are stored to keep track of the access control.

If nothing is defined, we don't have access, default = reject access

These fields depend on the object type:
*Object = Device: the possible ACLS are:
#view : view all commands/sensors of this device
#activate : activate all commands for this device 
*Object = Command: the possible ACLS are:
#view : view the status off the command
#activate : activate this command
*Object = Sensor: the possible ACLS are:
#view : view the sensor data for this sensor
#activate : NA

There is some linking between the device and commands/sensors, if the ACL is linked to a device this ACL will be used for all commands/sensors linked to this device, except if another ACl restricts access to a specific sensor/command.

!!!ACL examples
We have the following defined
Device A with command Ac1 Ac2 Ac3 and sensors As1 As2 As3
Device B with command Bc1 Bc2 and sensors Bs1
Device C with no commands and sensors Cs1 Cs2 Cs3

and we have the following ACLS
||Obeject Type   |Object|View|Activate
Device|A|1|1
Device|B|1|0
Command|Bc1|1|1
Sensor|Cs3|1|0||

This will result in the following access:
- full control of all commands and sensors of device A
- Full VIEW control of device B no activate control except for command BC1
- No access to device C, except for view on sensor C3

!! Ferllings idea
This system is based on the idea that right may vary based on four criteria:
The user, the locations of the user/feature, the terminal used and the state of the domotic system.
!!! Levels
Levels numbers describe the credential level for users.
2 fixed levels define the minimal and maximal values :
* Level 0 : (For admin users)
* Level 9 : (For guest/non logged users)

Any other Level numbers (between 1 and 8) can be created to organize users hierarchy.
example:
* Level 1 : Parents
* Level 2 : Children
* Level 3 : Friends and Occasional visitors

!!! Locations and Terminals
Features access can be different, based on the user location and feature location.
3 locations type have been identified:
* Local : The user and the requested feature are in the same room or defined zone.
* remote : The user is in a different room/zone from the requested feature.
* outside : The user is outside the house/building (insecure connection via Internet)

Specific terminal can also have specific limited level (specially for guest access).
For example, a embedded touchscreen, can only be allowed to access local features.

!!! States
Specific domotic states can also influence features access.
For example, If we do not want children to be able to access some feature, when there is no parent at home.

States can be set manually, using cron/calendar or using scenarios.
Some examples: Alarm on, Parent not at home, Holiday, Party at home, etc...

!!! Features access
To access a feature a user will need an equal or higher access level, than is the level set for this feature.
* For sensors, access will allow the user to view the sensor value.
* For commands, access will allow the user to launch the command.
Each sensor/command, will have a default set of requested level, for access:

{FANCYTABLE( head=&quot;Sensor/Command|Zone|Local|Remote|Outside&quot;, headaligns=&quot;left|center&quot;)}
Temperature|Bedroom|Level 9|Level 9|Level 8
Light switch|Bedroom|Level 9|Level 8|Level 0
{FANCYTABLE}
Explanation:
* The temperature value can be viewed on any local or remote location, without login, but outside access will require login with minimal Level 8 access.
* Light switch can be activated on the same room, with guest access (no login). From other remote locations Level 8 is required, and Level 0 (admin) from outside (internet) access.

As explained those default access can be changed based on terminal/state.
Example 1: I want my smartphone to have full access, without login needed, inside the house.

{FANCYTABLE( head=&quot;Sensor/Command|Zone|//Local|//Remote|//Outside&quot;, headaligns=&quot;left|center&quot;)}
||DEFAULT|T.SMARTPHONE|DEFAULT|T.SMARTPHONE|DEFAULT|T.SMARTPHONE
Light switch|Bedroom|Level 9|Level 9|Level 8|Level 9|Level 0|Level 0
{FANCYTABLE}

Example 2: I want prevent my son for watching the TV, when I am not at home.
{FANCYTABLE( head=&quot;Sensor/Command|Zone|//Local|//Remote|//Outside&quot;, headaligns=&quot;left|center&quot;)}
||DEFAULT|S.NOPARENT|DEFAULT|S.NOPARENT|DEFAULT|S.NOPARENT
TV|Livingroom|Level 9|None|Level 8|None|Level 0|Level 0
{FANCYTABLE}

!All (Fritz's idea)

Note : the points below doesn't describe exactily the authentication and authorisation process as I assume we could implement different modules for these features. So, I will use generic functions for these features and in these generic functions we will do what we want.
Note : basically, this work like this : an ecryption layed to protect the data. The first time a client connects to the server, it tries to authenticate : if it is a success, a token is given to the client. And then, the client will always add the token in its sub or req messages.

There are 3 topics : 

1. encrypt the data
2. authentication
3. authorisation

!!Encrypt data
This feature will allow to send clear id/password/hash in the json content of the MQ
This must be activated/deactivated with an option in domogik.cfg. This will allow to debug the MQ in dev mode, and eventually to deactivate ssl on small configurations like raspberry for better performances (but with a security hole)

To allow a real security we need to do a handshake.

On Domogik side, the ssl public and private keys can be managed during the installation and there will be no additionnal actions to do for the users.

For the UI, the main issue is how to do the keys exchange ? There will be a manual action to do... About domoweb, it can be a key file copy.
About Domodroid (and others), I actually don't know

!!Authentication (done with a req/rep) and authorisation (for all messages)
As the flow is encrypted, we can write login/password or any other needed item as clear data in the json. This could be a json dedicated part. Example :

{CODE()}
req : authentication
{
    &quot;security&quot; : { &quot;id&quot; : &quot;clientname&quot; },
	...
}
{CODE}

The client sends to the MQ server an auth request. On the server, a generic function &quot;checkAuthentication()&quot; is called with the security json part as parameter. Then, some code is called from this function to check the auth. So we could be able to change easily the auth management by using some auth modules. The function will return True (user granted) or False (user denied).

If the user is not granted, an error will be sent :


{CODE()}rep : authentication.failed
{
    &quot;security&quot; : { &quot;id&quot; : &quot;clientname&quot;, &quot;message&quot; : &quot;You are not granted&quot; },
	...

}{CODE}


If the user is granted, a token will be given to the client with an expirationd date :


{CODE()}
rep : authentication.success
{
    &quot;security&quot; : { &quot;id&quot; : &quot;clientname&quot;, &quot;token&quot; : &quot;some_uuid_token&quot;, &quot;timestamp&quot; : &quot;123456788899999&quot; },
	...

}
{CODE}

Then, the client will just have to include the token in all its MQ &quot;sub&quot; or &quot;pub&quot; or &quot;rep&quot; or &quot;req&quot; messages :

{CODE()}
req : somereq
{
    &quot;token&quot; : &quot;some_uuid_token&quot;,
	...
}
{CODE}

When a message is received on the server, first the token is checked :
1. the function &quot;checkToken(token)&quot; is called with the token as parameter. It returns true/false. 
* True : the token is valid, we can continue. 
* False, the token is not valid. In this case, if this is a sub/req message, an error response is returned. Else, nothing is done (as no response is waited by the client for a pub or a rep message).
2. the function &quot;checkAuthorisation(token, some_parameter_which_define_the_feature)&quot; is called to check if the user (identified by a token) is allowed to do the action (rep, req, sub, pub). It returns True, False
* True : the client is granted, we can continue.
* False : the client is not granted. In this case, if this is a sub/req message, an error response is returned. Else, nothing is done (as no response is waited by the client for a pub or a rep message).

