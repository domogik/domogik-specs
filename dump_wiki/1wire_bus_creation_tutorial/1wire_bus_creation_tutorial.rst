****************************
1wire bus creation tutorial
****************************
^La traduction de cette page n'est pas terminée.^

Here is an example on how to create a 1wire bus.

I use a DS1420 interface. It is equipped with an RJ11 port. Unfortunately, I only have RJ45 cables, so I decided to continue with RJ45 connectors instead of RJ11 which are less and less commonly available.

Let's start creating an RJ11-RJ45 cable. I used an old phone RJ11 plug. The operation is pretty simple, just cut the cable at an extremity and place an RJ45 connector with the 4 cables using the 4 middle connectors. Then make sure to put the cables in the same order as on the other side with the RJ11 connector.

{img fileId="162" thumb="y" alt="" rel="box[g]"}

I have used a simple RJ45 cable extension connector.

{img fileId="163" thumb="y" alt="" rel="box[g]"}

Open the extension connector by using a screwdriver and we will solder our component inside. In my case it will be a temperature sensor of type DS1820B.

{img fileId="164" thumb="y" alt="" rel="box[g]"}

With my extension connection, unfortunately I was unable to solder on it, the tin wouldn't stick on it. So I replaced the contacts by copper ones.

{img fileId="165" thumb="y" alt="" rel="box[g]"}

After all soldering done, it remains to check if it works. The easiest way is to use OnewireViewer software,  `Maxim website download page <http://www.maxim-ic.com/products/ibutton/software/1wire/OneWireViewer.cfm>`_. If everything is fine, you'll see your interface and your sensor :  you'll be able to read the temperature from it.

{img fileId="166" thumb="y" alt="" rel="box[g]"}

The advantages of using such a mounting schema is the low cost of implementation and the easy way to serialize the components on the same bus.


