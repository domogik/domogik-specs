{maketoc}

!Creating a timer with XplTimer
Here is how to create a timer :
{CODE(colors='python')}
from domogik.xpl.common.xplconnector import XplLTimer 
import threading           

timer = XplLTimer(60, my_callback_function, self.myxpl)                        
timer.start()
{CODE}

When you want timer to stop, you can do this : 
{CODE(colors='python')}
timer.stop()
{CODE}

Note that the Xpltimer will automatically register itself to the instance so that the ''stop()'' method will be called automatically when the plugin is stopped.

