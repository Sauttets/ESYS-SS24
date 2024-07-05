#HTWG
#semester5
#ESYS
#Linux

Ein RootFS (Root Filesystem) ist das Hauptdateisystem eines Betriebssystems, das alle grundlegenden Systemdateien und -verzeichnisse enthält, die zum Starten und Ausführen des Systems erforderlich sind. Es stellt die Wurzel des Verzeichnisbaums dar, von dem aus alle anderen Dateisysteme und Verzeichnisse eingebunden sind.

**Verzeichnisstruktur**
- /sbin
	- Kommandos für die Systemverwaltung
- /sys
	- Virtuelles Dateisystem 
	- Informationen über Geräte und Treiber
- /tmp
	- Temporäre Dateien, nach Reboot gelöscht 
	- Oft als tmpfs Dateisystem realisiert
- /usr
	- Anwendungsprogramme 
	- /usr/src: Linux Kernel Sourcen
- /var
	- Logdateien, Spooldateien 
	- Temporäre Dateien (/var/tmp), PID Dateien

### RootFS im RAM
- Linux bietet die Möglichkeit das RootFS komplett in den RAM zu laden und dort zu Mounten (Early-Userland)
- Ein Early Userland ist für ein Embedded system vollkommen ausreichend 

**Ablauf:**
1. Bios/UEFI
	- Führt eine Hardware initialisierung durch
	- Sucht nach Bootable device
	- Übergibt die kontrolle an den Bootloader
2. Bootloader
	- Lädt den Kernel in den Speicher und übergibt die Kontrolle an diesen
3. Kernel mit Root-FS im Early-Userland:
	- Initiiert das Early-Userland
	- Early Userland enthält alle Treiber und Configs um das system weiter zu konfigurieren und initialisieren
	- Early Userland wird im RAM gemounted
	- die /init datei im initramfs führt grundlegende Hardwareerkennung durch und Lädt Treiber
4. Userland
	- Bei Desktop/Server Systemen wird ein Userland gebooted, welches auf der Festplatte installiert ist
5. Starten von /sbin/init
	- started das endgültige RootFS über `exec()` 
	- initiiert alle nötigen Hintergrunddienste und Benutzerprozesse

**Vorteile Root-FS im RAM**
- Konsistentes Filesystem bei jedem Neustart 
- Booten ohne Filesystemcheck 
- Einfache Systemaktualisierung 
- Eventuell Auswahl des Rootfilesystems (Debug/Test) 
- Schneller Zugriff 
- Auf RAM sind unbegrenzte Schreibzyklen möglich

**Nachteile Root-FS im RAM**
- Änderungen am RootFS gehen nach einem Neustart des Systems verloren
- Für die Ramdisk werden 2-8 MB RAM benötigt

**Booten mit Ramdisk**
- Immage wird in die Ramdisk geladen und als EarlyUserland gemounted
- Teile des Hauptspeichers (RAM) werden als Ramdisk reserviert
- Ramdisks wird wie eine herkömmliche Disk gemounted

1.  Erzeugen einer Ramdisk `dd if=/dev/zero of=\ count=\` 
2. Datei `<NAME>` wird formatiert und lokal gemountet
3. Image `<NAME>` wird dann lokal ungemounted und steht als Root-FS Image zu Verfügung
4. `qemu-system -kernel -hda <NAME>`
5. Mit initrd Support packt der Kernel das komprimierte Root-FS Image aus
	- kopiert den Inhalt in eine RAM Disk.
	- Der Kernel mounted die RAM Disk als Root
	- Kernel Parameter initrd=
	- startet das Skript linuxrc auf dem Root Filesystem.

**Vergleich Root-FS Image vs. Dateisystem auf flash**
![[Vergleich-RootFS_Immage_im_RAM-FS_im_Flash.png]]

### Vorteile/Nachteile einer Ramdisk

**Vorteile**
- Zugriff ist schneller als auf den Flash
- Im flash sind die Schreibzugriffe limitiert
- Größe ist frei wählbar
- Daten in Ramdisk sind temporär
- vereinfachte Systemaktualisierung
**Nachteile**
- Ramdisk verbraucht Hauptspeicher
- Die daten sind doppelt vorhanden (im RAM und im Immage im flash)
- Änderungen am RootFS sind nach dem Neustart verloren
- Disk Treiber + Dateisystem Treiber nötig

**FS Treiber für den RAM**

- Ein FS-Treiber mapped das vorliegende FS auf das VFS (Virtual Filesystem), welches intern vom Kernel verwendet wird.

- Statt das Filesystem über einen Treiber zu "übersetzten" kann das Kernel-Build System die notwendigen Treiber, Gerätedateien und Bootprogramme in ein Archiv packen. 
- Dieses Archiv hat dann bereits die gleiche Struktur wie das VFS 
- Das Archiv wird zusätzlich zum Kernel-Image geladen oder direkt mit dem CPIO-Archiv gelinkt
- Die Kernel-Option für diesen Mechanismus ist **„initramfs“**.
