#HTWG
#semester5
#ESYS
#Linux

- Spezifische aufgaben ohne ausgeprägtes UI
	- Navi
	- Router
	- Waschmaschine
	- ...
- Diskless
- Kompakt

# Anforderungen
- Kurze Bootzeiten
- Ohne Vorwarnung stromlos geschaltet
- Dauerbetrieb (24 / 7 / 52)

- Exakte anpassung an Systemanforderungen
- keine überflüssigen Funktionen um overhead zu vermeiden
- auf die Gerätefunktion angepasste Hardwareplattformen
	- Cross-Compile-[[06-1-Toolchain|Toolchain]] 
	- Systemgeneratoren 
	- Simulator/Emulator
	
![[Ope-Deeply-Embedded.png#left|500]]

Deeply embedded Systeme laufen im vergleich zu Open Embedded Systemen ohne ein vollwertiges Betriebssystem

![[ES-Architektur.png|500]]

**Softwarekomponenten eines Embedded Linux Systems:** 
- Firmware (Bios) 
- [[05-Bios & Bootloader|Bootloader]] 
- [[02-Linux Kernel|Kernel]] 
- [[04-1-RootFS|Rootfilesystem]]

- Embedded Linux Kernel = Linux Kernel, speziell für die entspr. Hardware konfiguriert

**Hierachie von Embedded Architekturen**
![[HirarchieEmbedded.png|500]]

**Softwareverteilung ROM/Flash**
![[SoftwareverteilungRomFlash.png|400]]


**Linux Bibliotheken**
![[LunuxLibs.png|500]]


**Linux Toolchain**
![[LinuxToolchain.png|500]]


# Lizenzen

**GPL** 
- Modifikationen müssen öffentlich gemacht werden und bei Nachfrage abgegeben werden 
- Ohne Modifikationen ist kaum ein System aufzubauen. 
**BSD** 
- Autoren müssen genannt werden. 
- Modifikationen sind ohne weitere Einschränkungen möglich.

Der Linux kernel steht unter der GLP [[Lizenzen|Lizenz]] 
Code für Gerätetreiber ist in den meisten Fällen offenzulegen


# Vorteile Linux

- Skalierbarkeit erlaubt moderate Hardware-Ressourcen 
- Unterstützung aller gängigen Embedded Prozessoren 
- Aktive Entwicklergemeinde, => neueste Technologien 
- Firmen bieten kommerzielle Tools und Entwicklungsumgebungen an (+ Support) 
- Gleiche Tools auf Entwicklungs- und Zielrechner möglich 
- Grosse Softwareauswahl 
- Standard POSIX API's

# Nachteile Linux

- Mindestanforderungen an die Hardware: 32Bit, >4MB RAM 
- Somit nicht für Deeply Embedded Systems geeignet 
- Einschränkungen (noch) im Safety-Critical und Realtime Bereich.