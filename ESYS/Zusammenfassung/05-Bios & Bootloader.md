#HTWG
#semester5
#ESYS
#Linux 

# Bios 
- Firmware die auf dem ROM gespeichert ist
- BIOS (Basic Input Output) initialisiert die Hardware
	- CPU aktivieren
	- POST (Power on self test) starten
	- CPU Chaches aktivieren
	- Speicher initialisieren
	- Weitere Hardware initialisieren (I/O scan nach geräten)
- First Level Bootloader initialisieren

**Ablauf:**
- BIOS befinded sich im Persistenten ROM
- Hardware wird initialisiert
- Bootloader wird gestartet
- Bootloader wird in den RAM geladen
- BIOS gibt die kontrolle an den Bootloader ab

# Bootloader
- Initialisierung
	- Memory Controller 
	- Interrupt Controller 
	- Ein-/Ausgabe Bausteine (z.B. Ethernet Controller)
- Kopiert das OS image in den Hauptspeicher ([[02-Linux Kernel|Kernel]] images und [[04-1-RootFS|RootFS]])
	- ROM 
	- Flash 
	- Sekundärspeicher 
	- Netzwerk (z.B. tftp)
- Startet den Kernel mit den nötigen Parametern
- Übergibt die Kontrolle des systems an den Kernel (aufruf von `kmain()`

### Bootloader Stages

- 1st Stage: Minimale Funktionalität, Lädt nur den 2nd Stage Bootloader
- 2nd Stage: Volle Funktionalität (Kann selbst ein eigenes Betriebssystem sein)

### Bootloader auswäheln
- Unterstützung für die Plattform
- Codeumfang
- Funktionsumfang
	- tftp-boot, nfs-boot
	- sd-card-boot
	- Monitorfunktionalität
	- Skriptingfähigkeit

![[BootablaufLinixPC.png]]