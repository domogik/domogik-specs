!X10 plugin

This plugin documentation is now available on [http://docs.domogik.org/plugin/x10_heyu/dev/en/]


!!Developper Notes

!!!xPL schema
The [http://xplproject.org.uk/wiki/index.php?title=Schema_-_X10.BASIC|x10.basic] schema is used.

!!!/command
{CODE()}
/command/x10/&lt;address&gt;/on # switch on the lamp / appliance
/command/x10/&lt;address&gt;/off # switch off the lamp / appliance
{CODE}
''Only for lamps'' 
{CODE()}
/command/x10/&lt;address&gt;/dim/&lt;value&gt; # dim units by &lt;level&gt; (1-22) (decrease brightness)
/command/x10/&lt;address&gt;/bright/&lt;value&gt; # brighten units by &lt;level&gt; (1-22) (increase brightness)
{CODE}
Note that these values are relative.