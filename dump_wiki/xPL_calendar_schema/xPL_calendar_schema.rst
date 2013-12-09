!xPL calendar schema
__TODO : translate me in english!__

xPL ne semble pas encore posséder de schéma bien défini pour gérer la récupération d'évènements dans un calendrier.

Cette page propose donc d'en définir un.

!!CALENDAR.BASIC Message specification 

* Class = CALENDAR
* Type = BASIC

Le schéma CALENDAR.BASIC est utilisé pour transmettre les évènements à une date d'un calendrier.

!!!XPL-STAT Structure

Ce schéma ne possède aucune structure de type 'stat', le type 'trigger' devrait être utilisé à la place.

!!!XPL-CMND Structure 

Ce schéma est utilisé pour réaliser les demandes de récupération d'évènements.

{CODE()}
CALENDAR.REQUEST
{
command=&quot;REQUEST&quot;
date=&lt;date dans le calendrier : 'TODAY', 'TOMORROW', YYYYMMDD&gt;
}
{CODE}

!!!XPL-TRIG Structure 

{CODE()}
CALENDAR.BASIC
{
startdate=&lt;date et heure de l'évènement&gt;
object=&lt;objet de l'évènement&gt;
((enddate=&lt;date|heure de fin de l'évènement))
((priority=&lt;priorité|de l'évènement : 'NORMAL', 'LOW', 'HIGH'&gt;))
((location=&lt;lieu|où se situe l'évènement&gt;))
((description=&lt;description|détaillé de l'évènement&gt;))
((type=&lt;type|de l'évènement : anniversaire, personnel, travail, etc&gt;))
}
{CODE}