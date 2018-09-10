# CCU2GW - use ccu2 as lan gateway [![Github All Releases](https://img.shields.io/github/downloads/jp112sdl/CCU2GW/total.svg)](https://github.com/jp112sdl/CCU2GW/releases) 

#### auf CCU2:
```
# Dateisystem read/write mounten
mount -o remount,rw /

# Dateien herunterladen und Rechte anpassen
mv /firmware/fwmap /firmware/fwmap.orig
wget --no-check-certificate -q -O /usr/local/addons/hmlangw https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/hmlangw
wget --no-check-certificate -q -O /etc/init.d/S61hmlangw https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/src/S61hmlangw
wget --no-check-certificate -q -O /firmware/fwmap https://raw.githubusercontent.com/jp112sdl/CCU2GW/master/fwmap
chmod 755 /usr/local/addons/hmlangw
chmod 755 /etc/init.d/S61hmlangw

# Laufende Dienste stoppen
/etc/init.d/S70ReGaHss stop
/etc/init.d/S62HMServer stop
/etc/init.d/S61rfd stop
/etc/init.d/S60multimacd stop

# Funkmodul Firmware auf 1.4.1 updaten
eq3configcmd update-coprocessor -p /dev/mxs_auart_raw.0 -c -u -d /firmware

# Init-Skripte verschieben
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

# Neustart durchführen
reboot
```

- _manueller Aufruf mit Debug-Option_ <br/>
`/usr/local/addons/hmlangw -D -n CCU2GW0001 -s /dev/mxs_auart_raw.0 -r -1`



<hr/>

Rückgängig machen (CCU2 wieder als CCU2 nutzen):

```
# Dienst stoppen
/etc/init.d/S61hmlangw stop

# Init-Skripte verschieben und Dateien löschen
export UNUSEDDIR=/etc/init.d_unused/
mv ${UNUSEDDIR}S49hs485d /etc/init.d/
mv ${UNUSEDDIR}S50lighttpd /etc/init.d/
mv ${UNUSEDDIR}S55cuxd /etc/init.d/
mv ${UNUSEDDIR}S58LGWFirmwareUpdate /etc/init.d/
mv ${UNUSEDDIR}S59SetLGWKey /etc/init.d/
mv ${UNUSEDDIR}S60hs485d /etc/init.d/
mv ${UNUSEDDIR}S60multimacd /etc/init.d/
mv ${UNUSEDDIR}S61rfd /etc/init.d/
mv ${UNUSEDDIR}S62HMServer /etc/init.d/
mv ${UNUSEDDIR}S70ReGaHss /etc/init.d/
rmdir ${UNUSEDDIR}
rm /etc/init.d/S61hmlangw
rm /usr/local/addons/hmlangw
rm /usr/local/addons/serialnumber.txt
mv /firmware/fwmap.orig /firmware/fwmap

# Neustart durchführen
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
