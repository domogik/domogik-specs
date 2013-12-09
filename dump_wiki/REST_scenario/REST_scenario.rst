Feature linked to ((Scenarios))

*****************
Developper Notes
*****************
Specifications
===============
~~#990:
* how do we identify a scenario instance ? what is the id ? how do we create it ?
* when do we call start / stop features ?
~~
/scenario/list-templates
*************************
List all xml template files
.. code-block::
    
    {
        "data" : [
            {
                "name" : "Scenario name",
                "description" : "this is a scenario....",
                "id" : "filename" 
            } ,
            {
                "name" : "Scenario name",
                "description" : "this is a scenario....",
                "id" : "filename" 
            } 
        ]
    }
    


/scenario/detail-templates/<template id>
***********************************************
Get detail from a template
.. code-block::
    
    {
        "data" : {
            "id" : "string scenario id",
            "name" : "scenario name",
            "description" : "scenario description",
            "parameters" : [
                {
                    "id" : "param id",
                    "name" : "param name",
                    "description" : "param description",
                    "type" : "param type" 
                },
                {
                    "id" : "param id",
                    "name" : "param name",
                    "description" : "param description",
                    "type" : "param type",
                    "available-values" : ['a','b','e','f']
                } 
            ] 
        }
    }
    


/scenario/add/template-id/<template id>/instance-name/<name given by user>/param1/<param 1 value>/param2/<...>/...
*******************************************************************************************************************************************
Instantiate a scenario.
A scenario id will be created.

Returns only status message

.. code-block::
    
    {
        "instance-id" : "instance id"
    }
    


/scenario/update/instance-id/<instance id>/instance-name/<name given by user>/param1/<param 1 value>/param2/<...>/...
**********************************************************************************************************************************************
Update a scenario instance
Returns only status message

/scenario/del/<instance id>
**********************************
Delete a scenario instance
Returns only status message

/scenario/list-instances
*************************
List all scenario instancies
.. code-block::
    
    {
        "data" : [
            {
                "name" : "Scenario name",
                "description" : "this is a scenario....",
                "id" : "string_scenario_id" ,
                "instance-name" : "Name given by user",
                "instance-id" : "instance id"
                "status" : "on/off"
            } ,
            {
                "name" : "Scenario name",
                "description" : "this is a scenario....",
                "id" : "string_scenario_id" ,
                "instance-name" : "Name given by user",
                "instance-id" : "instance id"
                "status" : "on/off"
            } 
        ]
    }
    


/scenario/detail-instances/<instance id>
***********************************************
Get detail from a template
.. code-block::
    
    {
        "data" : {
            "id" : "string scenario id",
            "name" : "scenario name",
            "description" : "scenario description",
            "instance-name" : "Name given by user",
            "instance-id" : "instance id"
            "status" : "on/off"
            "parameters" : [
                {
                    "id" : "param id",
                    "name" : "param name",
                    "description" : "param description",
                    "type" : "param type" ,
                    "value" : "param value"
                },
                {
                    "id" : "param id",
                    "name" : "param name",
                    "description" : "param description",
                    "type" : "param type" 
                    "value" : "param value"
                } 
            ] 
        }
    }
    


/scenario/start/<instance id>
************************************
Start a scenario instance
Returns only status message

/scenario/stop/<instance id>
***********************************
Stop a scenario instance
Returns only status message