#HTWG
#semester5
#ESYS
#Linux 

Sammlung von Skripten zur: 
- Konfiguration
- Generierung  
- Zusammenbau einer Distribution

Enhält 700+ Skripte:
- Busybox 
- Netzwerk 
- Grafik (GUI) 
- Audio 
- Kernel 
- Bootloader 
- Eigene Software
- ...

Mit den folgenden befehlen kann buildroot konfiguriert werden:
- `make menuconfig` konfigurieren von Busybox selbs
- im Buildroot Verzeichnis: 
	- `make busybox-menuconfig` 
	- `make uclibc-menuconfig`
	- `make linux-menuconfig`

#### Buildroot Ordnerstruktur
``` c
buildroot/
├── arch //Konfigurationen der von Buildroot unterstützten Architekturen 
│   ├── arm
│   ├── x86
│   └── ...
├── board            // Default Boot-Konfiguration und Speicheranbindung  
│   ├── raspberrypi  //verschiedener Systemen (Soc's, Qemu, x86) 
│   ├── beaglebone
│   └── ...
├── boot
│   ├── u-boot // Hier sind die standardmäßig unterstützten Bootloader zu finden
│   ├── grub
│   ├── syslinux
│   └── ...
├── configs // Default/Minimale Konfiguration einiger SoC Boards 
│   ├── raspberrypi_defconfig
│   ├── beaglebone_defconfig
│   └── ...
├── docs // Dokumentation zu buildroot
│   ├── manual
│   ├── examples
│   ├── buildroot.html // Einstieg
│   └── ...
├── dl // Ablage der Archive, die gedownloadet wurden 
│   ├── package1.tar.gz 
│   ├── package2.zip 
│   └── ...
├── fs // Konfigurationsparameter des jeweiligen Dateisysteme
│   ├── cpio
│   ├── ext2
│   └── ...
├── linux // Kernel-Konfiguration/Patches/Versionen 
│   ├── 5.10
│   ├── 5.4
│   └── ...
├── package       // Enthält zu jedem Paket notwendige Patches, 
│   ├── busybox   // Kompilierparameter sowie target-fs-Pfade
│   ├── openssh
│   └── ...
├── support // Skripte, die von buildroot selbst verwendet werden
│   ├── scripts 
│   ├── hooks 
│   └── ...
├── system        // Enthält die Ordnerstruktur des Zielsystems, sowie die 
│   ├── init      // parametrisierten Eigenschaften (hostname)
│   ├── systemd
│   └── ...
├── toolchain     // Enthält Konfigurationen beziehungsweise Patches für die 
│   ├── external  // Entwicklungssoftware (Toolchain) selbst 
│   ├── glibc
│   └── ...
├── utils         // Beinhaltet nützliche Skripte, wie das vergleichen von
│   ├── kconfig   // Buildroot-Konfigurationen 
│   ├── legal-info
│   └── ...
├── output
│   ├── build // notwendige Werkzeuge für Generierung 
│   ├── host
│   │   ├── usr // enthält generierte Cross Development-Werkzeuge
│   │   └── ...
│   ├── images // Enthält die generierten Imagedateien 
│   │   ├── bzImage
│   │   ├── bootloader
│   │   ├── root-FS
│   │   └── ...
│   ├── staging
│   └── target // Hier befindet sich das komplettierte ROOT-FS des Targets 
├── Makefile
└── Config.in
```

**post-build-script**
- Wird aufgerufen nach der Generierung der Pakete aber bevor das Root-Filesystem zusammengebaut wird. 
- Mit Hilfe des Skripts können beispielsweise Dateien in das Root-Filesystem kopiert werden
