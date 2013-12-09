!Create a new request to get all xpl messages
!!/xpl_msgs/request/new
Return :
{CODE()}
{
    &quot;status&quot; : &quot;OK&quot;,
    &quot;code&quot; : 0,
    &quot;description&quot; : &quot;None&quot;,
    &quot;ticket_id&quot; : 1,
    &quot;xpl_message&quot; : [
        {
            &quot;datetime&quot; : &quot;2011-05-23 20:23:33.486954&quot;,
            &quot;type&quot; : &quot;xpl-stat&quot;,
            &quot;source&quot; : &quot;xpl-onewire.shyrkadmg&quot;,
            &quot;destination&quot; : &quot;*&quot;,
            &quot;schema&quot; : &quot;sensor.basic&quot;,
            &quot;data&quot; : [
                   &quot;device&quot; : &quot;03EDB7010000&quot;,
                   &quot;current&quot; : &quot;22.5&quot;,
                   &quot;type&quot; : &quot;temp&quot;,
            ]
        },
		...
    ]
}
{CODE}

!Create a new request to get filtered xpl messages
Each filter can be used independently with each other.
!!/xpl_msgs/request/new/type/&lt;stat|trig|cmnd&gt;/source/&lt;source address&gt;/destination/&lt;destination address&gt;/schema/&lt;schema name&gt;
Return :
{CODE()}
Same as above, but only with messages that matches the filters.
{CODE}

!Get next results for an existing request
!!/xpl_msgs/request/get/&lt;ticket id&gt;

!Explicitly close an existing request
!!/xpl_msgs/request/free/&lt;ticket id&gt;
