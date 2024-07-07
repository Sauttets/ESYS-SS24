#HTWG
#semester5
#ESYS
#Linux 

## Gerätearten
**Block Geräte**
- Floppy oder Festplatte (SCSI, IDE) 
- Compact Flash (als IDE Gerät ansprechbar) 
- RAM Disk 
- Loopback Geräte

**Memory Technology Devices (MTD)**
- Flash, ROM or RAM chips 
- MTD emulation on block devices

## Journaling
![[Journaling-Schematic.png|400]]

- Mit dem journaling Prinzip werden Änderungen zuerst **seriell** in ein Journal geschrieben
- Wenn eine der Bedingungen erfüllt ist, werden die im journal gespeicherten Änderungen in die Datei geschrieben
	- nach einem gewissen Zeitintervall
	- Wenn das Journal voll ist
	- bei Systemereignissen (Strg+S, schließen der Datei, ...)
- Durch Journaling kann die Datenkorruption jedoch nicht komplett vermieden werden, wenn das System beim Schreiben des Journals in die Datei abstürzt.

![[Journaling-Boot-Schematic.png|400]]

- Nach einem Absturz, wird macht das System einen FileSystem-Check und überprüft ob das Journal leer ist. 
- Wenn dies nicht der fall ist, wird das FS mithilfe des Journals in einen Korrekten zustand überführt

#### Vorteile von Journaling
- Dateisystem bleibt in einem korrekten Zustand, auch nach einem Systemcrash
- Im Falle eines Systemabsturzes kann das Dateisystem mithilfe des Journals schneller wiederhergestellt werden, da nur die im Journal verzeichneten Änderungen überprüft werden müssen.
- Reduzierte Dateisystem-Checks, da nur das Journal überprüft werden muss, da durch das Journaling im gesamten system immer ein korrekter Zustand des Filesystems gewährleistet ist.
#### Nachteile von Journaling
- Da der Umweg über das Journal mehr aufwand bedeutet, sind Journaling Systeme oft etwas inperformanter als Dateisysteme ohne Journaling
- Durch das Journaling wird etwas mehr Speicher benötigt.

#### Journaling optimierte Dateisysteme
- [[Linux Filesysteme#**ext4 (Fourth Extended File System)**|ext4]], [[Linux Filesysteme#**ext3 (Third Extended File System)**|ext3]] 
- [[Linux Filesysteme#**btrfs (B-Tree File System)**|btrfs]] (OpenSource),
- [[Linux Filesysteme#**zfs (Zettabyte File System)**|zfs]] (OpenSource), 
- JFS (IBM), 
- XFS (SGI),


## Flash typen

### NAND
#### Eingesetzt in
- USB-Sticks
- SD-Karten
- SSDs
- Mobile Geräte

#### Vorteile
- Höhere Speicherdichte (40% kleiner als NOR)
- Günstiger pro Gigabyte im Vergleich zu NOR-Flash
- Höhere Anzahl an Schreib- und Löschzyklen
- Besser geeignet für die Speicherung großer Datenmengen

#### Nachteile
- langsamer Zugriff
- Höhere Fehleranfälligkeit, insbesondere bei Datenintegrität
- Lesen und Schreiben ist nur blockweise möglich. 1 Block entspricht 16 kByte (32 Pages a 512 Byte)
- Bad Block Mangement notwendig


### NOR
#### Eingesetzt in
- Firmware und BIOS
- Systeme in denen eine hohe Zuverlässigkeit nötig ist

#### Vorteile
- Schnellere Lesezugriffe und direkte Adressierbarkeit
- Erhöhte Sicherheit, aufgrund der direkten Codeausführung (Execute in Place, XiP)
- Geringere Fehleranfälligkeit bei Datenintegrität
- Adressierung byte- oder wortweise

#### Nachteile
- Niedrigere Speicherdichte im Vergleich zu NAND-Flash
- Höherer Preis pro Gigabyte
- Langsamere Schreib- und Löschgeschwindigkeit
- Hohe leistungsaufnahme

#### Flash optimierte Dateisysteme
- Jffs2
- yaffs2

