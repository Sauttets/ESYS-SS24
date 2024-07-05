#HTWG
#semester5
#ESYS
#Linux 

- Eine Toolchain ist eine Sammlung von Entwicklungswerkzeugen zur Programmierung von Applikationen und Betriebssystemen.
	- Make
	- Compiler Collection
	- Binutils (ein Set von Tools, um Binaries für eine CPU zu erzeugen)
	- Linker, Assembler
	- Debugger
	- Build System
- Eine Cross-Toolchain wird verwendet, wenn das Zielsystem (Target) eine andere Plattform als das Entwicklungssystem (Host) hat.

**Vorteile von Toolchains**
- Alle nötigen Tools vorhanden um alle Schritte der Entwicklung abzudecken
- gute Automatisierung durch Make
- erleichtert das kompilieren für mehrere unterschiedliche Architekturen
- Viele Toolchains beinhalten eine automatische Fehlererkennung

**Nachteile von Toolchains**
- Toolchains müssen genau an der Stelle im Dateisystem installiert werden, an welcher sie kompiliert wurden
- Toolchains enthalten oft veraltete Versionen
- Toolchains können übermäßig komplex sein


**Beispiel Skripte:**
- crosstool 
- crosstool-NG 
- ptxdist emdebian 
- [[06-2-Buildroot|buildroot]]
- openembedded 
Einige dieser Tools gehen weit über die Erstellung der Toolchain hinaus und erstellen komplette Distributionen incl. Paketmanager (z.B. openembedded)