Ein ELF-Binary (Executable and Linkable Format) ist ein binäres Dateiformat, das hauptsächlich in Unix- und Unix-ähnlichen Betriebssystemen wie Linux, FreeBSD und Solaris verwendet wird.

Es wird sowohl für ausführbare Dateien als auch für Objektdateien, gemeinsam genutzte Bibliotheken und Core-Dumps verwendet. Hier sind einige Hauptmerkmale des ELF-Formats:

1. **Header**: Der ELF-Header befindet sich am Anfang der Datei und enthält grundlegende Informationen über die Datei, wie z. B. den Typ (z. B. ausführbare Datei, gemeinsam genutzte Bibliothek), die Architektur (z. B. 32-Bit oder 64-Bit) und den Eintragspunkt (wo die Ausführung beginnt).
    
2. **Program Header Table**: Diese Tabelle enthält Informationen, die der Betriebssystem-Lader verwendet, um die Datei in den Speicher zu laden. Jeder Eintrag beschreibt eine Segmentadresse im Speicher und deren Eigenschaften, wie z. B. die Ladeadresse, die Dateigröße und die Speichergröße.
    
3. **Section Header Table**: Diese Tabelle beschreibt die verschiedenen Abschnitte der Datei, wie z. B. den Textabschnitt (Maschinencode), den Datensatz (initialisierte Daten), den BSS-Abschnitt (nicht initialisierte Daten) und den Abschnitt mit Symboltabellen. Diese Informationen werden hauptsächlich vom Linker und Debugger verwendet.
    
4. **Abschnitte (Sections)**: ELF-Dateien bestehen aus mehreren Abschnitten, die verschiedene Arten von Daten enthalten, wie z. B. Maschinencode, Daten, Symboltabellen und Debugging-Informationen. Jeder Abschnitt hat eine bestimmte Adresse und Größe.
    
5. **Segmente**: Während Abschnitte eine logische Gruppierung von Daten darstellen, beschreiben Segmente, wie die Datei in den Speicher geladen werden soll. Segmente können mehrere Abschnitte umfassen.
    
6. **Dynamische Verknüpfung**: ELF-Dateien unterstützen dynamische Verknüpfung, bei der zur Laufzeit Bibliotheken geladen werden können. Dies ermöglicht es, kleinere ausführbare Dateien zu erstellen und gemeinsam genutzte Bibliotheken effizient zu nutzen.

ELF wurde als flexibles und erweiterbares Format entwickelt, das auf verschiedene Arten von Prozessorarchitekturen und Betriebssystemen angewendet werden kann. Es hat das ältere a.out-Format in den meisten Unix-ähnlichen Systemen abgelöst.