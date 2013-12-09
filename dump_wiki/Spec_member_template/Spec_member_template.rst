**********************
Template for a member
**********************
**************************************************
~~#F00:OBSOLETE implemented with xplfromdb spec~~
**************************************************

||__Created:__|20/08/2011
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=>30, max=>100, label=>''draft'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|0.3.0
__References:__|((Database_core_model|Database Model))||

The template system will be used to create the commands/states for a xpl member.

 XML specification
===================
.. code-block::
    
    <member_template version='(version number used for commands/states updates)' type='(plugin or external)'>
        <commands>
            (List of Commands)
           <command name='(Command label)' type='(Domogik Type)' reference='(Command string)' />
           ...
        </commands>
        <states>
           (List of States)
           <state name='(State label)' type='(Domogik Type)' reference='(Reference key)' />
           ...
        </states>
    </member_template>
    


core_device record
===================
In the core_device table a 'virtual' device will be created for each member.
This device will holds the commands and states for the member.
{FANCYTABLE(head=>id~|~name~|~description~|~reference~|~type~|~version~|~member_id)}
1~|~plcbus member~|~~|~~|~member.plcbus~|~0.5~|~xpl-plcbus.myhost
2~|~onewire member~|~~|~~|~member.onewire~|~1.2~|~xpl-onewire.myhost
{FANCYTABLE}


 Example for a Plugin member
=============================
.. code-block::caption="plcbus.xml"
    
    <member_template version='0.5' type='plugin'>
        <commands>
            <command name='Start' type='DT_Trigger' reference='start' />
            <command name='Stop' type='DT_Trigger' reference='stop' />
        </commands>
        <states>
            <state name='Active' type='DT_State' reference='data' />
        </states>
    </member_template>
    


 Example for an external member
================================
.. code-block::caption="rfxcom.xml"
    
    <member_template version='1.2' type='external'>
        <states>
            <state name='Active' type='DT_State' reference='data' />
        </states>
    </member_template>
    
