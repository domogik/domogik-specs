!Template for a member
!~~#F00:OBSOLETE implemented with xplfromdb spec~~

||__Created:__|20/08/2011
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=&gt;30, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}
__Target:__|0.3.0
__References:__|((Database_core_model|Database Model))||

The template system will be used to create the commands/states for a xpl member.

!! XML specification
{CODE()}
&lt;member_template version='(version number used for commands/states updates)' type='(plugin or external)'&gt;
    &lt;commands&gt;
        (List of Commands)
       &lt;command name='(Command label)' type='(Domogik Type)' reference='(Command string)' /&gt;
       ...
    &lt;/commands&gt;
    &lt;states&gt;
       (List of States)
       &lt;state name='(State label)' type='(Domogik Type)' reference='(Reference key)' /&gt;
       ...
    &lt;/states&gt;
&lt;/member_template&gt;
{CODE}

!!core_device record
In the core_device table a 'virtual' device will be created for each member.
This device will holds the commands and states for the member.
{FANCYTABLE(head=&gt;id~|~name~|~description~|~reference~|~type~|~version~|~member_id)}
1~|~plcbus member~|~~|~~|~member.plcbus~|~0.5~|~xpl-plcbus.myhost
2~|~onewire member~|~~|~~|~member.onewire~|~1.2~|~xpl-onewire.myhost
{FANCYTABLE}


!! Example for a Plugin member
{CODE(caption=&quot;plcbus.xml&quot;)}
&lt;member_template version='0.5' type='plugin'&gt;
    &lt;commands&gt;
        &lt;command name='Start' type='DT_Trigger' reference='start' /&gt;
        &lt;command name='Stop' type='DT_Trigger' reference='stop' /&gt;
    &lt;/commands&gt;
    &lt;states&gt;
        &lt;state name='Active' type='DT_State' reference='data' /&gt;
    &lt;/states&gt;
&lt;/member_template&gt;
{CODE}

!! Example for an external member
{CODE(caption=&quot;rfxcom.xml&quot;)}
&lt;member_template version='1.2' type='external'&gt;
    &lt;states&gt;
        &lt;state name='Active' type='DT_State' reference='data' /&gt;
    &lt;/states&gt;
&lt;/member_template&gt;
{CODE}