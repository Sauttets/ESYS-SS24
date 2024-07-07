#HTWG
#semester5 
#ESYS 
#Linux 

## TLDR
### Kernel Sourcen
**Kernel Management**

- **Prozessmanagement**: Erstellen/Beenden von Prozessen, Single/Multi-Core-Scheduling.
- **Speichermanagement**: Adressumsetzung, Speicherschutz, Swap-Space, Extended Memory.
- **Device Drivers**: Standardisierter Zugriff auf Hardware, Peripherie via Treiber, Kernel-Komponenten mit Kernel Space Zugriff.

**Linux Kernel Besonderheiten**
- Keine Nutzung von LibC Funktionen.
- Kernel nutzt ähnliche Funktionen wie Standard C Lib (z.B. printk(), memset()).
- Keine Nutzung von floats/doubles, nur ganzzahlige Integer.

### Kernel Config
- Kernel-Build über Makefile mit >2000 Parametern.
- ARCH=\<Architektur> setzt Prozessorarchitektur.
- Alle Kernel-Configs in .config Datei.
- **make allnoconfig**: Minimale Config für Kompilierung (nicht bootfähig).
- **make mrproper**/**make distclean**: Entfernt durch make erzeugte Dateien inkl. .config.
- Module können mit **insmod**/**rmmod** geladen/entladen oder direkt in den Kernel kompiliert werden.

### Kernel Build
- ARCH= make -j \<n>: Parallelkompilierung mit n Kernen.

**Kernel Output**
- System.map: Symboltabelle.
- vmlinux: Komplettes ELF Binary.
- vmlinux.bin: Stripped Binary.
- Verschiedene Zielobjekte: head.o, misc.o, etc.
- piggy.gz/piggy.o: Komprimiertes Image.
- zImage/bzImage: Komprimiertes Kernel-Image für Bootloader.

### Kernel Boot
**Aufgabe von `head.o` in vmlinux**
- Prozessor-/Architekturprüfung, Page Tables aufsetzen, MMU initialisieren, einfaches Error Handling, Sprung zu **start_kernel()**.

**start_kernel() Funktion**
- Architektur Setup, Kernel Command Line verarbeiten, Subsysteme initialisieren, init Thread starten.

**RootFS**
- Betriebssysteme benötigen Filesystem: Konfigurationen, Applikationen etc.
- System besteht aus Kernel Image und RootFS Image.

### Kernel Bootparameter
- `root=`: Ort des RootFS.
- `ro/rw`: RootFS als read only/read write mounten.
- `console=`: Geräte als Konsole.
- `mem=`: Speicherzuweisung für Kernel.
- `initrd=`: Initial RAM Disk Image.
- `init=`/`rdinit=`: Alternatives Binary statt /sbin/init bzw. /init.
- `ip=`: Netzwerkkonfiguration.





## Kernel Sourcen
**Kernel Management**

**Prozessmanagement**
- Create/Destroy Prozesse
- Single core Scheduling
- Multi Core Scheduling

**Speichermanagement**
- Adressumsetzung
- Speicherschutz
- Swap-Space
- Extended Memory

**Device Drivers**
- Standardisierter zugriff auf Hardware
- Peripherie via spezifizierter Gerätetreiber
- Kernel-Komponenten haben Kernel Space zugriff

![[KernelManagement.png#left|300]]

**Linux Kernel Besonderheiten**
- Keine LibC funktionen nutzbar, da er Standalone sein muss
- Kann keinen User-Code nutzen
- Dem Kernel stehen ähnliche Funktionen wie in der Standard C lib zur verfügung
	- printk()
	- memset()
	- kmallock()
- Keine floats/doubles, da diese vom Kernel emuliert werden. Der Kernel nutzt nur ganzzahlige Integer

## Kernel Config

- Der kernel wird über eine Makefile mit >2000 parameter gebaut
	- über die Shell var `ARCH=\<Architektur>` lässt sich die benötigte Prozessorarchitektur einstellen
	- alle config parameter des Kernels werden in der .config file gespeichert
	- über `zcat /proc/config.gz` kann die config auch in einem laufenden System abgefragt werden 

	- `make allnoconfig` baut die minimal notwendige config, damit der Kernel kompiliert.
	- **⚠️ Dies erzeugt keinen Bootfähigen Kernel ⚠️**
	- `make mrproper` oder `make distclean` entfernt alle durch make erzeugten dateien AUCH die .config

	**Linux Module**
	- mit `insmod` und `rmmod` können module wie ein Treiber in den Kernel geladen und wieder entfernt werden
	- Alternativ können die Treiber auch direkt in den Kernel kompiliert werden (keine Infrastruktur zum laden/entladen von modulen nötig)
	
## Kernel Build 

- ARCH= make -j \<n>
- Über den Parameter -j kann eine Anzahl von Kernen angegeben werden um den Kernel ECHT parallel zu kompilieren
	![[KernelBuildProzess.png|400]]
	
**Kernel Output**
- System.map
	- Symboltabelle für die Zuordnung Objekt -> Adresse (Debugging)
- vmlinux
	- komplettes [[ELF Binary]] ("kernel proper")
	- unabhängig von der Zielarchitektur
- vmlinux.bin
	- Binary ohne Symbole, Kommentare, ... (Stripped)
- Target Objects
	- head.o 
	- misc.o 
	- Startup-Code 
	- Kernel EntpackCode
- piggy.gz / piggy.o 
	- ʼImageʼ komprimiert, bzw. als linkbares Objekt (.o)
- zImage/bzImage 
	- komprimiertes Kernel Image für Bootlader

## Kernel Boot
![[KernelInitialisierung.png|350]]

**Aufgabe von `head.o` in Kernel vmlinux**
- Checkt korrekte Prozessor/Architektur
- Aufsetzen der Page Tables für die Speicherverwaltung
- Initialisieren und Aktivierung der MMU
- Aufsetzen eines einfachen Error Handlings
- Sprung zur `start_kernel()` Funktion in `main.o` des Kernels
	
- die `start_kernel()` funktion hat die aufgabe:
	- Architektur Setup (setup_arch())
	- Verarbeitung der Kernel Command Line
	- Initialisierung der Subsysteme
	- init Thread starten 
		- Init vom Root-FS !
	- start_kernel() wird danach zum idle Thread

	**[[04-1-RootFS|RootFS]]**
	- Die meisten Betriebssysteme benötigen für den Betrieb ein Filesystem
	- Im filesystem werden Konfigurationen, Applikationen etc. abgelegt
	Das System besteht aus 2 images
	- Kernel Image
		- Notwendige Treiber
		- Kompiliert für die Prozessorarchitektur
		- Module
	- [[04-1-RootFS|RootFS]] Image
		- Systemprogramme
		- Konfigurationsspftware
		- Applications

## Kernel Bootparameter
Die setup() Funktionen der Treiber werden vom Kernel in einen  `.init.setup` Codespace verschoben, von wo diese aufgerufen werden. (`setup(”console= ” , console_setup)`)

- `root= ` gibt an wo sich das [[04-1-RootFS|RootFS]] befindet
- `ro/rw` mounted das [[04-1-RootFS|RootFS]] als read only oder read/write FS
- `console=` gibt an welche geräte als Console verwendet werden sollen
- `mem=` gibt an wie viel speicher der Kernel verwenden soll
- `initrd=` [[initrd|Initial RAM Disk Image]] (startet dort /[[linuxrc]])
- `init=` Angabe eines alternativen Binaries statt /sbin/[[04-3-Init]] (Block-Device Default)
- `rdinit=` Angabe eines alternativen Binaries statt /init ([[04-2-Initramfs]] Default)
- `ip=`  Angaben zur Art und Weise der Netzkarten Konfiguration (siehe nfsroot.txt )
