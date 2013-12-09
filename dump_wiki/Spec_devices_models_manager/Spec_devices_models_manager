*************************************************
Device models management webapp (specifications)
*************************************************

Purpose
========

This web app is a REST service to receives informations about devices models from the users.
There will be a small UI to display the informations sent and change their status


Authentication
===============

The webapp will need a basic authentication for the user interface. As there are no critical data, there is no need to have something heavily secured.
Login/password will be enough. All accounts will have the same grants.

The new accounts can be created only on command line with a tool like this: *python add_user my_login my_password*
To update a password, same thing : *python update_user my_login new_password*
To delete a user : same thing : *python delete_user my_login*

Database model
===============

Table : users
**************

||Field|Type
user|string
password|password||



Table : data
*************

||Field|Type|Description
id|int|PK
package_id|string|data from the user. See chapter 'on domogik admin side'
device_type|string|data from the user. See chapter 'on domogik admin side'
device_model_or_reference|string|data from the user. See chapter 'on domogik admin side'
device_status|string|data from the user. See chapter 'on domogik admin side'
issue_description|string|data from the user. See chapter 'on domogik admin side'
user_email|string|data from the user. See chapter 'on domogik admin side'
created_on|datetime|when the row is inserted
status|enum|NEW : when inserted, PROCESSING, PROCESSED
issue_url|string|url of the issue (when in status PROCESSING/PROCESSED) : null when row is inserted||
~~#F00:last_value ?~~

How it will work (uses cases)
==============================

On Domogik admin side
**********************
There will be a button in the plugin devices view for each device. When clicking on the button the user will access to a form with these fields :

* package_id : <package id> (prefilled, not updatable)
* device_type : <device type> (prefilled, not updatable)
~~#F00:attention avec device_type dans le nouvau modèle: Il n'y a plus la notion de type. mais simplement un identifiant de template utilisé pour créer le device. cette donnée peut être nulle si le device a été créé manuellement, sans template. de plus ce champ devra être vidé si la structure du device à été modifiée~~
~~#F00:Il faudrait aussi voir si cereal à ajouté la version du template utilisé, pour les mise à jour~~

* device description (model, reference) : <device model or reference> (prefilled if possible, updatable by the user)
* device status (list of choices) : works fine / don't work / works a bit
~~#F00:pour quelle utilisation?~~

* (displayed if status != works fine) issue description : <informations from the user>
* user email : <the user email> (updatable, can be blank if the user don't want to give its email)

When the user validates the form, an url is called on the webapp with the data in a json format : 
{ 
  'package_id' : ...
  'device_type' : ...
  'device_model_or_reference' : ...
  'device_status' : ...
  'issue_description' : ...
  'user_email' : ...
}

~~#F00:Et les paramètres?~~

The url should return a HTTP 200 (or 204 ?) response. If so, a success notification will be displayed. If not, an error notification will be displayed.

The url is configured in /etc/domogik/domogik.cfg so we can change it from a version to another one (in case we need to change it a day)

On the webapp side
===================

There will be 2 "public" urls : 
* /add (POST) : this is the url called by the domogik admin
~~#F00:Je comprends pas à quoi ca sert~~

* / : the login box

Some other urls will be needed (but users won't need to know them) :
* /admin/* : all the pages of the admin

the /add url is called
***********************

Here is what should happen :
{code()}
check the content (correct values, ...)
check if there is no security issue (sql injection, ....)
store the data in database (add the current datetime, and the status 'NEW')
send an email to a mailing list to notify (can be disabled by config)
call a free url (to update a dashboard in the future)
{code}

the / url is accessed
**********************

A login box must be displayed. If the login/password is not good, display an error. If it is good, display the main niew

!!!!Main view
The main view will display a table will all non processed elements (status != PROCESSED). All elements with a KO status should be displayed first and be grouped by package id

If the 'issue description' of an element is too big, we should truncate the display and if the user click on it display in a light box (or something like this) the full 'issue description'

The following actions can be done on a 'WORKS' device status element :
* set status to 'PROCESSED'

The following actions can be done on a 'DON'T WORK / WORKS A LITTLE' device status element :
* set status from 'NEW' to 'PROCESSING'. When this is done, a form 'PROCESSING_ACTION' will be displayed.
* if the status was already to 'PROCESSING', click on the 'PROCESSING' button. a form 'PROCESSING_ACTION' will be opened
* set the status to 'PROCESSED'

!!!!Form 'PROCESSING_ACTION'
this form will have some fields :
* link to an issue on a tracker (free url). This field can be updated by the admin user
* link to send an email to the user. It should prefill the mail (if possible) with : the link to the issue on the tracked (previous field content), a title

All the debug about the issue must be handled in the issue on the tracker.

!!!!UI views

{IMG(attId="441",height="25%",width="25%")}{IMG}

Installation
=============
The installation must respect the following rules : 
* installer is in python
* all the installation options must be set as options for install.py

The installation must handle 
* create the database 
* (optionnal) import all tables from a sql file
* create an init.d file
* set the init.d to start on computer startup
* create the first admin account
* set email for notifications
* set if we send email or not
* set the free url for notification
* set if we want to call the url or not

Assuming the webapp sources are located in a folder named 'dmm', the install.py must be in this folder. The webapp will use the files from this folder to run/. The init script must be updated to use this folder.

We also need a 'debian_install_dependancies.sh' script to :
* install needed packages

All this is required because we want to be able to recreate the application from scratch on a new server in case we lost the main server. As some backups will be done, the option to import data is needed.

