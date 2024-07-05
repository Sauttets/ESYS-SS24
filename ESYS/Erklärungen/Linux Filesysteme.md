
# Häufig verwendet/bekannt
### **ext (Extended File System)**
**Vorteile:**
- Erstes Dateisystem speziell für Linux entwickelt.
- Grundstein für spätere ext-Generationen.
**Nachteile:**
- Veraltet und ineffizient im Vergleich zu modernen Dateisystemen.
- Mangelnde Unterstützung für moderne Features wie Journalisierung.
**Einsatzgebiet:**
- Historisch interessant, aber heutzutage nicht mehr in praktischer Nutzung.
### **ext2 (Second Extended File System)**
**Vorteile:**
- Solide und bewährt.
- Keine Journalisierung, daher schnellere Schreiboperationen im Vergleich zu ext3/ext4.
**Nachteile:**
- Keine Journalisierung, was die Datenintegrität bei Abstürzen oder Stromausfällen gefährdet.
**Einsatzgebiet:**
- Embedded Systeme oder Umgebungen, in denen Journalisierung nicht notwendig ist und Schreibgeschwindigkeit priorisiert wird.
### **ext3 (Third Extended File System)**
**Vorteile:**
- Journalisierung, was die Datenintegrität erhöht.
- Rückwärtskompatibilität mit ext2.
**Nachteile:**
- Weniger performant als ext4.
- Begrenzte Skalierbarkeit für sehr große Dateisysteme.
**Einsatzgebiet:**
- Standarddateisystem für viele Linux-Distributionen in den 2000er Jahren.
### **ext4 (Fourth Extended File System)**
**Vorteile:**
- Verbesserte Performance und Skalierbarkeit.
- Unterstützung für sehr große Dateien und Dateisysteme.
- Verzögerte Allokation (Delayed Allocation), was die Fragmentierung reduziert.
**Nachteile:**
- Komplexer als ext2 und ext3, was zu potenziell mehr Fehlerquellen führen kann.
**Einsatzgebiet:**
- Weit verbreitet in modernen Linux-Distributionen für allgemeine Zwecke.
### **btrfs (B-Tree File System)**
**Vorteile:**
- Snapshots und Copy-on-Write (CoW).
- Integrierte RAID-Unterstützung und Datenintegritätsprüfung.
- Dynamisches Dateisystem- und Volumenmanagement.
**Nachteile:**
- Komplex und teilweise noch als experimentell betrachtet.
- Höherer Ressourcenverbrauch.
**Einsatzgebiet:**
- Datenzentren, Backup-Systeme, und Situationen, in denen Datenintegrität und Flexibilität entscheidend sind.
### **zfs (Zettabyte File System)**
**Vorteile:**
- Extrem hohe Skalierbarkeit.
- Integrierte RAID-Funktionalität und kontinuierliche Integritätsprüfung.
- Snapshots und Klonfunktionen.
**Nachteile:**
- Hoher Speicher- und Ressourcenverbrauch.
- Lizenzprobleme, die die Integration in den Linux-Kernel behindern.
**Einsatzgebiet:**
- Hochleistungsserver, Speicherlösungen und Unternehmensumgebungen, die hohe Zuverlässigkeit und Datenintegrität erfordern.
### **xfs**
**Vorteile:**
- Hohe Performance bei großen Dateien und parallelen Schreiboperationen.
- Effiziente Verwaltung großer Dateisysteme.
**Nachteile:**
- Komplexe Wiederherstellung bei Fehlern.
- Keine native Prüfsummenfunktionalität für Daten.
**Einsatzgebiet:**
- Hochleistungsanwendungen und Systeme, die große Dateien und hohe Schreib-/Leseoperationen erfordern.

### **ntfs (New Technology File System)**
**Vorteile:**
- Weit verbreitetes Dateisystem für Windows.
- Unterstützung für Dateikomprimierung, Verschlüsselung und große Dateien.
**Nachteile:**
- Weniger effizient auf nicht-Windows-Systemen.
- Komplexe Struktur kann zu höheren Overheads führen.
**Einsatzgebiet:**
- Primäres Dateisystem für Windows-basierte Computer und Server.
### **apfs (Apple File System)**
**Vorteile:**
- Optimiert für SSDs.
- Snapshots, Verschlüsselung und schnelle Dateikopien.
- Gute Leistung und Zuverlässigkeit.
**Nachteile:**
- Nur auf Apple-Geräten voll unterstützt.
- Mögliche Kompatibilitätsprobleme mit älteren MacOS-Versionen und Nicht-Apple-Systemen.
**Einsatzgebiet:**
- Standarddateisystem für macOS und iOS.
### **CramFS (Compressed ROM File System)**
**Vorteile:**
- Sehr geringe Größe durch Komprimierung.
- Read-only, ideal für Speicherplatzkritische Anwendungen.
**Nachteile:**
- Read-only, keine Möglichkeit zum Schreiben oder Ändern von Daten.
- Begrenzte Funktionalität und Flexibilität.
**Einsatzgebiet:**
- Embedded Systeme und Anwendungen, bei denen Speicherplatz knapp ist und nur lesender Zugriff benötigt wird.
### **SquashFS**
**Vorteile:**
- Komprimierung für geringe Dateigröße.
- Read-only, ideal für schreibgeschützte Umgebungen.
**Nachteile:**
- Read-only, keine Möglichkeit zum Schreiben oder Ändern von Daten.
- Höhere CPU-Auslastung aufgrund der Dekomprimierung.
**Einsatzgebiet:**
- Live-CDs, Embedded Systeme und schreibgeschützte Speicherlösungen.

# Neue/Nieschen Filesysteme
### ext3cow (Third Extended File System with Copy-On-Write)
**Vorteile:**
- Integriertes Copy-On-Write
- Unterstützt Snapshots

**Nachteile:**
- Weniger verbreitet und getestet als ext3

**Einsatzbereich:**
- Spezielle Anwendungen, die von Snapshots und COW profitieren

### Next3
**Vorteile:**
- Snapshots-Funktionalität
- Aufbauend auf ext3, daher stabil

**Nachteile:**
- Begrenzte Unterstützung und Verbreitung

**Einsatzbereich:**
- Anwendungen, die Snapshots benötigen, aber die Stabilität von ext3 bevorzugen


### ReiserFS
**Vorteile:**
- Gute Leistung bei kleinen Dateien
- Effiziente Speicherplatznutzung

**Nachteile:**
- Entwicklung wurde eingestellt, nicht mehr aktiv unterstützt

**Einsatzbereich:**
- Ältere Systeme, die von den spezifischen Vorteilen von ReiserFS profitieren


### bcachefs
**Vorteile:**
- Unterstützt Copy-On-Write (COW), Snapshots, Komprimierung und Verschlüsselung
- Hohe Leistung und Zuverlässigkeit

**Nachteile:**
- Noch relativ neu und möglicherweise nicht so ausgereift wie ältere Dateisysteme

**Einsatzbereich:**
- Für Systeme, die hohe Leistung und Zuverlässigkeit benötigen, wie Datenbanken und virtuelle Maschinen


### EcryptFS (Enterprise Cryptographic Filesystem)
**Vorteile:**
- Integrierte Verschlüsselung
- Transparent für Benutzeranwendungen

**Nachteile:**
- Kann die Leistung beeinträchtigen
- Verwaltung der Schlüssel kann komplex sein

**Einsatzbereich:**
- Ideal für Systeme, die sensible Daten schützen müssen, wie z.B. Laptops und mobile Geräte

### EncFS (Encrypted File System)
**Vorteile:**
- Benutzerfreundlich und einfach zu konfigurieren
- Arbeitet im Userland, keine speziellen Kernelmodule erforderlich

**Nachteile:**
- Kann langsamer sein als Kernel-basierte Dateisysteme
- Sicherheit ist nicht so robust wie bei EcryptFS

**Einsatzbereich:**
- Für Desktop-Benutzer, die einfache Verschlüsselung ohne Kernel-Modifikationen benötigen


### NILFS (New Implementation of a Log-structured File System)
**Vorteile:**
- Unterstützt kontinuierliche Snapshots
- Sehr gute Leistung bei sequentiellen Schreibvorgängen

**Nachteile:**
- Weniger bekannt und unterstützt

**Einsatzbereich:**
- Systeme, die kontinuierliche Snapshots benötigen, wie Backup-Server

### OrangeFS
**Vorteile:**
- Verteiltes Dateisystem für hohe Leistung und Skalierbarkeit

**Nachteile:**
- Komplexität der Verwaltung

**Einsatzbereich:**
- Hochleistungsrechner und Cluster-Umgebungen

### Reiser4
**Vorteile:**
- Verbesserte Leistung und Flexibilität
- Plugin-Unterstützung

**Nachteile:**
- Geringe Verbreitung und Unterstützung

**Einsatzbereich:**
- Spezialisierte Anwendungen, die von den erweiterten Funktionen profitieren

### Tux3
**Vorteile:**
- Versionierung und effiziente Speicherung

**Nachteile:**
- Noch in der Entwicklung und weniger stabil

**Einsatzbereich:**
- Experimentelle Systeme und Entwicklung