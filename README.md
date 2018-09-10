# CCU2GW - use ccu2 as lan gateway

#### CCU2
mount -o remount,rw /

#### Debian (9)
- apt-get update
- apt-get install libgcc-6-dev-armel-cross gcc-arm-linux-gnueabi g++-arm-linux-gnueabi libgcc1-armel-cross

- wget https://raw.githubusercontent.com/jens-maus/RaspberryMatic/master/buildroot-external/package/hmlangw/hmlangw.cpp
- wget https://raw.githubusercontent.com/jens-maus/RaspberryMatic/master/buildroot-external/package/hmlangw/hmframe.cpp
- wget https://raw.githubusercontent.com/jens-maus/RaspberryMatic/master/buildroot-external/package/hmlangw/hmframe.h
- wget https://raw.githubusercontent.com/jens-maus/RaspberryMatic/master/buildroot-external/package/hmlangw/Makefile
- wget https://raw.githubusercontent.com/jens-maus/RaspberryMatic/master/buildroot-external/package/hmlangw/S61hmlangw
- edit Makefile:

```
CC      = arm-linux-gnueabi-gcc

CFLAGS  = -Wall -O2 -pipe -march=armv5te -mtune=arm926ej-s -msoft-float -mfloat-abi=soft
```
 - make

 - scp hmlangw root@ccu2:/usr/local/addons/
 - scp S61hmlangw root@ccu2:/etc/init.d/


#### CCU2
Funkmodul FW Version anzeigen:
`eq3configcmd update-coprocessor -p /dev/mxs_auart_raw.0 -c -v -d /firmware`

-> /firmware/fwmap editieren; 1.4.1 muss aktiv sein
`eq3configcmd update-coprocessor -p /dev/mxs_auart_raw.0 -c -u -d /firmware`

_Test (vorher alle Dienste beenden, die aufs Funkmodul zugreifen) mit_
`/usr/local/addons/hmlangw -D -n CCU2LANGW1 -s /dev/mxs_auart_raw.0 -r -1`

```
export UNUSEDDIR=/etc/init.d_unused/
mkdir ${UNUSEDDIR}
mv /etc/init.d/S49hs485d ${UNUSEDDIR}
mv /etc/init.d/S50lighttpd ${UNUSEDDIR}
mv /etc/init.d/S55cuxd ${UNUSEDDIR}
mv /etc/init.d/S58LGWFirmwareUpdate ${UNUSEDDIR}
mv /etc/init.d/S59SetLGWKey ${UNUSEDDIR}
mv /etc/init.d/S60hs485d ${UNUSEDDIR}
mv /etc/init.d/S60multimacd ${UNUSEDDIR}
mv /etc/init.d/S61rfd ${UNUSEDDIR}
mv /etc/init.d/S62HMServer ${UNUSEDDIR}
mv /etc/init.d/S70ReGaHss ${UNUSEDDIR}

chmod 755 /etc/init.d/S61hmlangw
reboot
```
