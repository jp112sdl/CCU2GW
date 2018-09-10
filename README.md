# CCU2GW - use ccu2 as lan gateway [![Github All Releases](https://img.shields.io/github/downloads/jp112sdl/CCU2GW/total.svg)](https://github.com/jp112sdl/CCU2GW/releases) 

#### auf CCU2:
```
mount -o remount,rw /
wget --no-check-certificate -q -O /usr/local/addons/hmlangw https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/hmlangw
wget --no-check-certificate -q -O /etc/init.d/S61hmlangw https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/S61hmlangw
chmod 755 /usr/local/addons/hmlangw
chmod 755 /etc/init.d/S61hmlangw
mv /firmware/fwmap /firmware/fwmap.orig
wget --no-check-certificate -q -O /firmware/fwmap https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/fwmap
eq3configcmd update-coprocessor -p /dev/mxs_auart_raw.0 -c -u -d /firmware
```

- _Test (vorher alle Dienste beenden, die aufs Funkmodul zugreifen) mit_<br/>
`/usr/local/addons/hmlangw -D -n CCU2GW0001 -s /dev/mxs_auart_raw.0 -r -1`

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
reboot
```

<hr/>

### selbst kompilieren:
#### Debian (9)
- `apt-get update`
- `apt-get install libgcc-6-dev-armel-cross gcc-arm-linux-gnueabi g++-arm-linux-gnueabi libgcc1-armel-cross`

- `wget https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/hmlangw.cpp`
- `wget https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/hmframe.cpp`
- `wget https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/hmframe.h`
- `wget https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/Makefile`
- `wget https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/S61hmlangw`

- `make`
