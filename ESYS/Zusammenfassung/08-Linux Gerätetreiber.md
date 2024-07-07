#HTWG
#semester5
#ESYS
#Linux 

Betriebssystemintern werden mehrere Arten von Geräten unterschieden:
- Character-Devices 
	- Geräte, die die Ein- und/oder Ausgaben zeichenweise durchführen (z.B. Keyboard)
	- Gelesene Zeichen können nicht erneut gelesen werden
- Block-Devices 
	- Geräte, die die Daten in Blöcken organisieren und übertragen (z.B. Festplatte)
	- Der „wahlfreie“ Zugriff" auf die Daten ist möglich (seeken)
	- Daten werden blockweise gelesen und geschrieben
- Network-Devices 
- USB-Devices

Interfaces für Geräte- und Dateizugriff" sind identisch
- `cat /etc/passwd`
- `cat /proc/cpuinfo`
- `cat /dev/console`

Jedes Gerät benötigt mindestens eine Gerätedatei in `/dev`


### Kernel Module 
##### Systemfunktionen
- `open()`/`close()`
	- "Öffnen“ des Gerätes:
		- ist die Datei vorhanden/ist der Treiber überhaupt geladen?
		- Stimmen die Zugriffsrechte?
		- Welcher Zugriff auf das Gerät wird verlangt?
		- Rückgabewert: Filedeskriptor
	- "Schließen" des geräts
		- Freigeben der bei `open()` allozierten Ressourcen
		- Nach dem `close()` Aufruf befindet sich das Gerät wieder in einem definierten Zustand.
- `read()`
	- `ssize_t read(int fd, char *buffer, size_t max_bytes_to_read);`
	- Lesen von Daten in den Speicher der Applikation
	- Returnwert:
		- Anzahl der gelesenen Bytes (Minimum 1 Byte)
		- ggf. Fehlercode
- `write()`
	- `ssize_t write(int fd, char *buffer, size_t MaxBytesToWrite);`
	- Schreiben von Daten 
	- Returnwert:
		- Anzahl der geschriebenen Bytes
		- ggf. Fehlercode
- `ioctl()`
	- `ioctl(int fd, unsigned long request, ...)`
	- Gerätespezifischer zugriff (Input/Output controll)
	- der request ist ein gerätespezifischer Befehlscode
- `select()`/`poll()` 
	- Zustand von Dateideskriptoren zu überwachen
-  `fcntl()`
	- Veränderung von Dateideskriptoren
- `seek()`

über `insmod` `rmmod` `lsmod` können Module (Treiber) geladen, entladen und gelisted werden

##### Funktion von Init_module()
- Modul bei Kernel-Subsysteme anmelden
	- IO-Subsystem (Treiber) 
	- PCI 
	- Sys-Filesystem 
	- proc-Filesystem
- Initialisierung von Ojekten
- Reservieren von Ressourcen

##### funktion von cleanup_module()
- Freigeben der allozierten Systemressourcen
- Abmelden des Moduls beim System


**Beispiel Kernel Modul (Treiber)**
```c
#include <linux/init.h>  
#include <linux/module.h>

static int __init hello_init(void) {  
    printk(KERN_INFO "Hello World!");    
    return 0;
    }

static void __exit hello_exit(void) {  
    printk(KERN_INFO "Unloaded");
    }

module_init(hello_init);  
module_exit(hello_exit);  

MODULE_LICENSE("GPL");  
MODULE_AUTHOR("Your Name");  
MODULE_DESCRIPTION("A simple example Linux module.");  
MODULE_VERSION("0.1");
```


### Lizenzen

 **GPL (GNU General Public License)**
- **Beschreibung:** Diese Lizenz erlaubt es, den Code zu verwenden, zu modifizieren und zu verbreiten, solange alle abgeleiteten Werke ebenfalls unter der GPL veröffentlicht werden. Dies stellt sicher, dass der Quellcode immer verfügbar bleibt.

**GPL v2 (GNU General Public License, Version 2)**
- **Beschreibung:** Dies ist die spezifische Version der GPL, die für den Linux-Kernel selbst verwendet wird. Sie bietet ähnliche Bedingungen wie die GPL, konzentriert sich jedoch auf diese spezielle Version.

**LGPL (GNU Lesser General Public License)**    
- **Beschreibung:** Ähnlich wie die GPL, aber weniger restriktiv. Sie erlaubt es, das Modul mit proprietärem Code zu verlinken, solange Änderungen am LGPL-Teil offen gelegt werden.

**Dual BSD/GPL**
- **Beschreibung:** Diese Lizenz erlaubt es, den Code entweder unter der BSD-Lizenz oder der GPL zu verwenden. Die BSD-Lizenz ist weniger restriktiv und erlaubt die Integration in proprietäre Software ohne die Offenlegung des Quellcodes.

**MIT**    
- **Beschreibung:** Eine sehr permissive Lizenz, die es erlaubt, den Code für fast jeden Zweck zu verwenden, zu modifizieren und zu verteilen, ohne viele Einschränkungen.

**Proprietäre Lizenz**    
- **Beschreibung:** Diese Lizenz erlaubt es, das Modul nur unter bestimmten, vom Autor festgelegten Bedingungen zu verwenden. Sie ist nicht offen und kann die Weitergabe oder Modifikation einschränken.


![[Kernel-Module-Log-Buffer.png|600]]

**Kernel Log Level**
![[Kernel-Loglevel.png|600]]


**Kernel Modul makefile**
```
ifneq ($(KERNELRELEASE),)
obj-m := module.o

else
KDIR := /lib/modules/$(shell uname -r)/build
PWD := $(shell pwd)

default:
    $(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules
endif
```

- `ifneq ($(KERNELRELEASE),)`  prüft, ob `KERNELRELEASE` gesetzt ist
- `obj-m := module.o`  gibt an, dass das Kernel-Modul `module.o` erstellt werden soll.
- `KDIR := /lib/modules/$(shell uname -r)/build` setzt `KDIR` auf das Verzeichnis, in dem die Kernel-Build-Dateien für die aktuell laufende Kernel-Version gespeichert sind.
- `PWD := $(shell pwd)` setzt `PWD` auf das aktuelle Verzeichnis.
- `$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules`  Dies ruft das Kernel-Build-System auf, um das Modul zu bauen. `-C $(KDIR)` wechselt in das Kernel-Build-Verzeichnis, `SUBDIRS=$(PWD)` gibt das Verzeichnis an, in dem das Modulquellcode liegt, und `modules` gibt an, dass alle Module in diesem Verzeichnis gebaut werden sollen.


### Treiberidentifizierung

- **Major-Nummern**: Werden bei der Registrierung des Treibers beim IO-Subsystem zugewiesen und in der Gerätedatei hinterlegt.
	- 8 Bit breite Nummer (255 geräte)

- **Minor-Nummern**: Ermöglichen die Unterscheidung zwischen verschiedenen logischen Einheiten oder Funktionen innerhalb eines Geräts.
	- 8 Bit breite Nummer (255 geräte)

- **Gerätenummern**: Werden bei der Treiberregistrierung reserviert und dienen der umfassenden Geräteadressierung im Kernel.
	- kombinierte major und minor number in eine 32-Bit-Gerätenummer (4 Mrd. Geräte)

![[Mapping-Major-Minor-Gerätenummer.png|600]]
