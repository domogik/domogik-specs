Feature linked to ((Scenarios))

!Developper Notes
!!Specifications
~~#990:
* how do we identify a scenario instance ? what is the id ? how do we create it ?
* when do we call start / stop features ?
~~
!!!/scenario/list-templates
List all xml template files
{CODE()}
{
    &quot;data&quot; : [
        {
            &quot;name&quot; : &quot;Scenario name&quot;,
            &quot;description&quot; : &quot;this is a scenario....&quot;,
            &quot;id&quot; : &quot;filename&quot; 
        } ,
        {
            &quot;name&quot; : &quot;Scenario name&quot;,
            &quot;description&quot; : &quot;this is a scenario....&quot;,
            &quot;id&quot; : &quot;filename&quot; 
        } 
    ]
}
{CODE}

!!!/scenario/detail-templates/&lt;template id&gt;
Get detail from a template
{CODE()}
{
    &quot;data&quot; : {
        &quot;id&quot; : &quot;string scenario id&quot;,
        &quot;name&quot; : &quot;scenario name&quot;,
        &quot;description&quot; : &quot;scenario description&quot;,
        &quot;parameters&quot; : [
            {
                &quot;id&quot; : &quot;param id&quot;,
                &quot;name&quot; : &quot;param name&quot;,
                &quot;description&quot; : &quot;param description&quot;,
                &quot;type&quot; : &quot;param type&quot; 
            },
            {
                &quot;id&quot; : &quot;param id&quot;,
                &quot;name&quot; : &quot;param name&quot;,
                &quot;description&quot; : &quot;param description&quot;,
                &quot;type&quot; : &quot;param type&quot;,
                &quot;available-values&quot; : ['a','b','e','f']
            } 
        ] 
    }
}
{CODE}

!!!/scenario/add/template-id/&lt;template id&gt;/instance-name/&lt;name given by user&gt;/param1/&lt;param 1 value&gt;/param2/&lt;...&gt;/...
Instantiate a scenario.
A scenario id will be created.

Returns only status message

{CODE()}
{
    &quot;instance-id&quot; : &quot;instance id&quot;
}
{CODE}

!!!/scenario/update/instance-id/&lt;instance id&gt;/instance-name/&lt;name given by user&gt;/param1/&lt;param 1 value&gt;/param2/&lt;...&gt;/...
Update a scenario instance
Returns only status message

!!!/scenario/del/&lt;instance id&gt;
Delete a scenario instance
Returns only status message

!!!/scenario/list-instances
List all scenario instancies
{CODE()}
{
    &quot;data&quot; : [
        {
            &quot;name&quot; : &quot;Scenario name&quot;,
            &quot;description&quot; : &quot;this is a scenario....&quot;,
            &quot;id&quot; : &quot;string_scenario_id&quot; ,
            &quot;instance-name&quot; : &quot;Name given by user&quot;,
            &quot;instance-id&quot; : &quot;instance id&quot;
            &quot;status&quot; : &quot;on/off&quot;
        } ,
        {
            &quot;name&quot; : &quot;Scenario name&quot;,
            &quot;description&quot; : &quot;this is a scenario....&quot;,
            &quot;id&quot; : &quot;string_scenario_id&quot; ,
            &quot;instance-name&quot; : &quot;Name given by user&quot;,
            &quot;instance-id&quot; : &quot;instance id&quot;
            &quot;status&quot; : &quot;on/off&quot;
        } 
    ]
}
{CODE}

!!!/scenario/detail-instances/&lt;instance id&gt;
Get detail from a template
{CODE()}
{
    &quot;data&quot; : {
        &quot;id&quot; : &quot;string scenario id&quot;,
        &quot;name&quot; : &quot;scenario name&quot;,
        &quot;description&quot; : &quot;scenario description&quot;,
        &quot;instance-name&quot; : &quot;Name given by user&quot;,
        &quot;instance-id&quot; : &quot;instance id&quot;
        &quot;status&quot; : &quot;on/off&quot;
        &quot;parameters&quot; : [
            {
                &quot;id&quot; : &quot;param id&quot;,
                &quot;name&quot; : &quot;param name&quot;,
                &quot;description&quot; : &quot;param description&quot;,
                &quot;type&quot; : &quot;param type&quot; ,
                &quot;value&quot; : &quot;param value&quot;
            },
            {
                &quot;id&quot; : &quot;param id&quot;,
                &quot;name&quot; : &quot;param name&quot;,
                &quot;description&quot; : &quot;param description&quot;,
                &quot;type&quot; : &quot;param type&quot; 
                &quot;value&quot; : &quot;param value&quot;
            } 
        ] 
    }
}
{CODE}

!!!/scenario/start/&lt;instance id&gt;
Start a scenario instance
Returns only status message

!!!/scenario/stop/&lt;instance id&gt;
Stop a scenario instance
Returns only status message