.. toctree::



*******************************
Creating a timer with XplTimer
*******************************
Here is how to create a timer :
.. code-block::colors='python'
    
    from domogik.xpl.common.xplconnector import XplLTimer 
    import threading           
    
    timer = XplLTimer(60, my_callback_function, self.myxpl)                        
    timer.start()
    


When you want timer to stop, you can do this : 
.. code-block::colors='python'
    
    timer.stop()
    


Note that the Xpltimer will automatically register itself to the instance so that the ''stop()'' method will be called automatically when the plugin is stopped.

