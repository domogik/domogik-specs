!Specifications
!!Different parts of plugin
!!!Legionella killing
One day by month, the temperature must be 65°C to kill legionalle (killed at 60°C).
We need : 
* one order to make temperature going to 65°C : see function __heat_to_65__.
* one way to know when doing this (day/hour)
** hour : a plugin parameter
** day : 2 parameters : 
*** number of the day in the period (1..7 for a week, 1..28 for a month)
*** period type : month or week
* a way to know that action append (people safety!)
** mail ?
** sms ?
** script (which would do the mail/sms/xpl message send/etc)?
** ==&gt; See how to do this

!!!Force water to 65°C
This will make the temperature going to 65°C : see function __heat_to_65__.
We need : 
* a xPL listener for heating order
* the function to do the action

!!!Consumption analysis
Each day of the week, the water consumption should be analysed to get water volume used in the day. This will be used for the day &quot;d+7&quot; to heat water.
In the first time, we may use last week data.
In a second time, we may use a formula which make a smart calculation with last weeks.

__Warning : to do this, we need to store and read data!!! How to do this ?__

When doing the calculation ?
* at midnight ?

What do we do if plugin is stopped for several days ?

!!!Water heating in function of analysis
Input ?
* a temperature for &quot;output temperature&quot; ?



!!Formulas
__Warning : formula in french for the moment__
{CODE()}
&quot;Quantité d'eau à 40°=-LN((T°sortie-T°entrée)/V40*100) x Volume du ballon&quot;
{CODE}

!!FAQ
!!!Why not using a scenarii to set when heating to kill legionella ?
Because this would need a manual configuration. This is a critical (people safety) feature.
