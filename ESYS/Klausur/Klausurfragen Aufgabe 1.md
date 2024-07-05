
#### Erläutern sie die Vor- und Nachteile von cross-Entwicklung im vergleich zur nativen Entwicklung auf dem Zielsystem
Cross-Entwicklung bietet den Vorteil einer leistungsfähigen und flexiblen Entwicklungsumgebung mit schnelleren Kompilierungszeiten und besseren Werkzeugen. Sie ist jedoch komplexer einzurichten und kann zu Kompatibilitäts- und Debugging-Herausforderungen führen.

Native Entwicklung bietet den Vorteil von Echtzeit-Feedback und genaueren Tests auf der Zielhardware, leidet jedoch unter den Einschränkungen der Ressourcen und der Geschwindigkeit der Zielhardware.

#### Was ist der Unterschied zwischen einem monolithischen Kernel und einem Mikrokernel?
Ein monolithischer Kernel führt alle grundlegenden Betriebssystemfunktionen wie Prozessmanagement, Speicherverwaltung und Gerätetreiber im Kernel-Modus aus, was eine hohe Leistung ermöglicht, aber potenziell weniger stabil und sicher ist. Ein Mikrokernel hingegen verschiebt viele dieser Funktionen in Benutzermodusprozesse, wodurch der Kernel selbst kleiner und potenziell stabiler und sicherer wird, aber möglicherweise auf Kosten der Leistung.

#### Warum nicht einfach ein fertiges Image aus dem Internet herunterladen?
Durch eigenes konfigurieren hat man bessere Kontrolle den kernel auf die benötigten Funktionen zu beschränken und so nicht das ganze unnötig gross werden zu lassen und hat einen besseren überblick über das system.

#### Wie kann ich dem Kernel mitteilen, dass ich gerne die Datei die Ich von meinem Freund bekommen habe als Konfigurationsdatei nehmen möchte?
Ich gebe dem Kernel die Datei in das /src directory mit und benenne sie um in .config.

#### Im Shell-Skript hw1.sh gibt es eine Funktion prepare_src(), die den Kernel-Quellcode vorbereitet. Erklären Sie, was diese Funktion genau macht und warum sie nützlich ist.
Die Funktion prepare_src() im Shell-Skript hw1.sh hat folgende Aufgaben:  
- Prüft, ob das Verzeichnis src_dir existiert. Wenn nicht, wird es erstellt.  
- Lädt den Kernel-Quellcode von der angegebenen URL herunter und entpackt ihn in das src_dir Verzeichnis.  
- Kopiert eine gespeicherte Konfigurationsdatei (dotconfig) in das src_dir Verzeichnis als .config.  

Diese Funktion ist nützlich, weil sie den gesamten Vorbereitungsprozess automatisiert und sicherstellt, dass der Quellcode korrekt heruntergeladen und die gewünschte Konfiguration angewendet wird, bevor der Build-Prozess startet.

#### Warum könnte es vorteilhaft sein, statisch gelinkte Binaries in einem Embedded-System zu verwenden?
- Unabhängige Binaries: Keine Notwendigkeit, dass spezifische Versionen von Bibliotheken auf dem Embedded System vorhanden sind.
- Einfachheit der Verteilung: Erleichtert die Verteilung und Installation der Software, da keine externen Abhängigkeiten berücksichtigt werden müssen.
- Geringerer Speicherbedarf zur Laufzeit: Keine Notwendigkeit für einen dynamischen Linker zur Laufzeit, was besonders in ressourcenbeschränkten Umgebungen vorteilhaft ist.

#### Welche Konfigurationen müssen Sie minimal vornehmen um einen bootfähigen Kernel zu generieren?
- Block Layer
- Festplattenzugriff (SCSI, SATA, Filesystem)
- Eingabe (Tastatur)
- Ausgabe (Console)
- Netzwerk (TCP/IP, Netzwerkkartentreiber)
- ELF

#### Sie haben die Aufgabe bekommen, herauszufinden, weshalb ihr Embedded Linux Gerät keine Verbindung mit dem lokalen Netzwerk aufbaut. Beschreiben Sie die Schritte, wie sie dies mit "make menuconfig" untersuchen würden.
1. Namen der Netzwerkkarte des [Embedded Linux](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74415 "Embedded Linux") Geräts herausfinden.
2. Mithilfe der Suchfunktion in "make menuconfig" den Treiber des Geräts finden. Alternativ händisch in [Device Drivers][network device support] suchen.
3. Falls der Treiber nicht ausgewählt wurde, mithilfe der Suchfunktion die gegebenenfalls vorhandenen Abhängigkeiten finden und mit dem Treiber auswählen.
4. Kernel neu kompilieren und installieren.

#### Was ist der Vorteil des Befehls 'make menuconfig' bei der Konfiguration eines Linux-Kernels?
- 'make menuconfig' bietet eine textbasierte, interaktive Menüoberfläche zur Anpassung der Kernel-Konfiguration.
- Dies ist vor allem vorteilhaft, weil man nicht alle 1000+ Optionen iterativ durchgehen muss.
- Zusätzlich bietet 'make menuconfig' eine Suchfunktion und weitere Informationen zu den Optionen/Paketen.

#### Wieso muss man GCC benutzen um den Linux Kernel zu kompilieren
Der [Linux Kernel](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74416 "Linux Kernel") benutzt GCC-Extensions wie: 

- Inline C Funktionen 
- Inline Assembler 
- branch prediction likely unlikely...

#### Was ist das bzImage was man nach dem kompilieren bekommt?
Komprimierte Kernel Image Datei die vom Bootloader zum booten benutzt wird.