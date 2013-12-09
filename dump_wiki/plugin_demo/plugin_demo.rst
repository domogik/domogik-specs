************
Plugin demo
************
.. toctree::



Specifications
===============
Irc discussion
***************
{code()}
16:44 < cereal_> fritz_sm1: do you have a description of what you want for the 
                 demo plugin?
16:44 < cereal_> what it should send?
17:35 < fritz_sm1> cereal_: no, I think we should define some features for a 
                   first round. And it other rounds we will had some other 
                   features.
17:36 < fritz_sm1> And somewhere (maybe plugin in plugin description), we could 
                   list what need to be created on UI as devices (address/type)
17:36 < fritz_sm1> for basically, for a first round, I think we should have at 
                   least some lighting features and some temperature features
17:36 < fritz_sm1> for 5/6 rooms
17:37 < fritz_sm1> after, for lights, it is quite simple : when a xpl-cmnd is 
                   received, we send back the appropriate xpl-trig
17:38 < fritz_sm1> for temperature, we should define a way to get temperatures 
                   that looks something real
17:38 < fritz_sm1> (maybe defining a table with one value per half an hour)
{CODE}