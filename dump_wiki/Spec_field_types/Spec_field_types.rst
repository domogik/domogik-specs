!Types for generating UI fields
||__Created:__|8/07/2012
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=&gt;50, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}
__Target:__|?
__References:__|((Spec_device_template|Device template))||
{maketoc}

The following types are used to define a data value type and generate the appropriate field in the UI.

!! Type: boolean
Validation: Validates that the value is True (e.g. the check box is checked) if the field has required=true.
Errors: required

!! Type: string
Parameters:
*max_length:int (optional)
*min_length:int (optional)
*mask:str (optional) (9: Any digit character, A: Any letter character, *: Any letter or digit character)
*multilignes:bool (optional)
Validation: Validates max_length or min_length, if they are provided. Otherwise, all inputs are valid.
Errors: required, max_length, min_length

!! Type: choice
Parameters:
*choices : An iterable (e.g., a list or tuple) of 2-tuples to use as choices for this field.
Validation: Validates that the given value exists in the list of choices.
Errors: required, invalid_choice

!! Type: multiplechoice
Will return a list of values separated with ','
Parameters:
*choices : An iterable (e.g., a list or tuple) of 2-tuples to use as choices for this field.
Validation: Validates that the given values exists in the list of choices.
Errors: required, invalid_choice

!! Type: date
format is 'DD/MM/YYYY'
Parameters:
Validation: Validates that the given value respect the particular date format.
Errors: required, invalid

!! Type: time
format is 'HH:MM:SS'
Parameters:
Validation: Validates that the given value respect the particular time format.
Errors: required, invalid

!! Type: datetime
format is 'YYYY-MM-DD HH:MM:SS'
Parameters:
Validation: Validates that the given value respect the particular datetime format.
Errors: required, invalid

!! Type: float
Parameters:
*max_value:int (optional)
*min_value:int (optional)
These control the range of values permitted in the field.
Validation: Validates that the given value is an float.
Errors: required, invalid, max_value, min_value

!! Type: integer
Parameters:
*max_value:int (optional)
*min_value:int (optional)
These control the range of values permitted in the field.
Validation: Validates that the given value is an integer.
Errors: required, invalid, max_value, min_value

!! Type: email
Validation: Validates that the given value is a valid email address.
Parameters:
*max_length:int (optional)
*min_length:int (optional)
Errors: required, invalid

!! Type: ipv4
Validation: Validates that the given value is a valid IPv4 address.
Errors: required, invalid

!! Type: url
Parameters:
*max_length:int (optional)
*min_length:int (optional)
Validation: Validates that the given value is a valid URL.
Errors: required, invalid
