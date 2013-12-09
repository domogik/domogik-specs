********************
xPL calendar schema
********************
__TODO : translate me in english!__

xPL ne semble pas encore posséder de schéma bien défini pour gérer la récupération d'évènements dans un calendrier.

Cette page propose donc d'en définir un.

CALENDAR.BASIC Message specification 
======================================

* Class = CALENDAR
* Type = BASIC

Le schéma CALENDAR.BASIC est utilisé pour transmettre les évènements à une date d'un calendrier.

XPL-STAT Structure
*******************

Ce schéma ne possède aucune structure de type 'stat', le type 'trigger' devrait être utilisé à la place.

XPL-CMND Structure 
********************

Ce schéma est utilisé pour réaliser les demandes de récupération d'évènements.

.. code-block::
    
    CALENDAR.REQUEST
    {
    command="REQUEST"
    date=<date dans le calendrier : 'TODAY', 'TOMORROW', YYYYMMDD>
    }
    


XPL-TRIG Structure 
********************

.. code-block::
    
    CALENDAR.BASIC
    {
    startdate=<date et heure de l'évènement>
    object=<objet de l'évènement>
    ((enddate=<date|heure de fin de l'évènement))
    ((priority=<priorité|de l'évènement : 'NORMAL', 'LOW', 'HIGH'>))
    ((location=<lieu|où se situe l'évènement>))
    ((description=<description|détaillé de l'évènement>))
    ((type=<type|de l'évènement : anniversaire, personnel, travail, etc>))
    }
    
