#HTWG
#semester5
#ESYS
#Linux 

Emulator um beliebige Hardware zu emulien. => http://qemu.org
- systememulation: qemu-system-ARCHITEKTUR \[OPTIONEN]
- Prozessemulation: z.b. qemu-i386 PROGRAMMNAME

## RootFS
### Static
/sbin 
	Kommandos für die Systemverwaltung 
/sys 
	Virtuelles Dateisystem 
	Informationen über Geräte und Treiber 
/usr 
	Anwendungsprogramme 
	/usr/src: Linux Kernel Sourcen 
/lib
/dev
	gerätedateien für gerätetreiber
/etc
	Konfigurationsdateien
### Dynamic
/var 
	Logdateien, 
	Spooldateien temporäre Dateien (/var/tmp), 
	PID Dateien
/tmp 
	Temporäre Dateien, nach Reboot gelöscht 
	oft als tmpfs Dateisystem realisiert


