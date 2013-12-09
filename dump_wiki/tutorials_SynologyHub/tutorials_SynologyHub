This tutorial explain how to build the C Hub, provided with Domogik, for Synology Arm, PowerPC platform.

All the following step can be executed from any Linux OS

!!Install the DSM Tool Chain

First you need to find you processor type:
http://forum.synology.com/wiki/index.php/What_kind_of_CPU_does_my_NAS_have

Then, you need to download the DSM tool chain:
http://sourceforge.net/projects/dsgpl/files
This package contain all compiling tools for your Synology platform.

Extract it to /usr/local/
{CODE()}# tar zxpf gcc343_glibc232_88f5281.tgz –C /usr/local/{CODE}

!!Download the xPL Hub sources
http://www.xpl4java.org/xPL4Linux/

{CODE()}
# cd /tmp
# wget http://www.xpl4java.org/xPL4Linux/downloads/xPLLib.tgz
# tar zxpf xPLLib.tgz
# cd xPLLib
{CODE}

!!Build the xPL Lib
Edit Makefile with your compilator parameters. For PowerPC it's:
{CODE()}
CCOPTS =  -mcpu=8548 -mhard-float -mfloat-gprs=double
LIBS = -lm -lc
LIBDIR = /usr/local/powerpc-linux-gnuspe/lib
INCDIR = /usr/local/powerpc-linux-gnuspe/include
..
LDOPTS	= -O
CC	=	/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc $(CCOPTS)
LIBCC	=	$(CC) -fPIC
LD	= 	/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-ld $(LDOPTS)
{CODE}

Use gcc for linking (Thanks Kuri for the tips)
{CODE()}
libxPL.so: $(LIB_OBJS)
	@echo &quot;Creating libxPL.so...&quot;
	$(LIBCC) -shared -o libxPL.so $(LIB_OBJS) -L$(LIBDIR) $(LIBS)
{CODE}

Run make
{CODE()}
$ make
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-io.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-utils.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-service.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-message.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-listeners.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-store.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-config.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -c xPL-hub.c
Creating libxPL.so...
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -mcpu=8548 -mhard-float -mfloat-gprs=double -fPIC -shared -o libxPL.so xPL-io.o xPL-utils.o xPL-service.o xPL-message.o xPL-listeners.o xPL-store.o xPL-config.o xPL-hub.o -L/usr/local/powerpc-linux-gnuspe/lib -lm -lc
Creating xPL.a...
ar: creating xPL.a
{CODE}

!!Build xPL Hub
The hub sources are in the examples sub folder
{CODE()}
cd examples
{CODE}
edit examples/Makefile with your compilator parameters. For PowerPC it's:
{CODE()}
LDOPTS	= -O -L/usr/local/powerpc-linux-gnuspe/lib
CC	=	/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc $(CCOPTS)
LD	= 	/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc $(LDOPTS)
{CODE}

run make
{CODE()}
$ make
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -g -DLINUX -pedantic -Wall -c xPL_Hub.c
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -O -L/usr/local/powerpc-linux-gnuspe/lib -o xPL_Hub xPL_Hub.o ../xPL.a -g -lm  
/usr/local/powerpc-linux-gnuspe/bin/powerpc-linux-gnuspe-gcc -O -L/usr/local/powerpc-linux-gnuspe/lib -static -o xPL_Hub_static xPL_Hub.o ../xPL.a -g -lm {CODE}

You should find, in the folder, two builds for the C-Hub:
xPL_Hub and xPL_Hub_static 

Reference:
((Synology DiskStation 3rd-Party Apps Integration Guide|http://download.synology.com/download/ds/userguide/Synology%20NAS%20Server%203rd-Party%20Apps%20Integration%20Guide.pdf))
