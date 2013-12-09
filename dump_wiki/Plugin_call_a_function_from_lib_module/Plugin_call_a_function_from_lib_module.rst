*************************************************************************
How to call a function / method when something happens in the lib module
*************************************************************************

Typically an event is fired and catched by the ''lib'' module of your plugin. Then you'd like to send a xPL message.
How can you do that?

You have to use a ''callback'' function, here is how to do it:

In your ''bin'' module, you define a function that sends a xPL message:
.. code-block::colors='python'
    
    def send_xpl(self, param1, param2):
        msg = XplMessage(...)
        ...
    


In your ''bin'' module, somewhere you instantiate your ''lib'' class, and pass the ''callback'' method :
.. code-block::colors='python'
    
    myLib = MyLib(p1, p2, cb = self.send_xpl)
    


So in your ''lib'' module you will have something like:
.. code-block::colors='python'
    
    class MyLib:
        def __init__(self, p1, p2, cb):
            self.callback = cb
            ....
     
        def my_method_that_will_send_a_xpl_message():
            ...
            self.callback(param1, param2)
    
