Der Begriff `initrd` steht für "initial ramdisk", was eine vorübergehende Root-Dateisystem-Partition im RAM bezeichnet.

- **Zweck und Funktion:**
    - `initrd` ist eine temporäre RAM-Disk, die der Linux-Kernel beim Booten verwendet, bevor das eigentliche Root-Dateisystem auf der Festplatte verfügbar ist. Es dient dazu, notwendige Treiber und andere Software zu laden, die erforderlich sind, um das echte Root-Dateisystem zu mounten.
- **Verwendung:**
    - Beim Start eines Linux-Systems lädt der Bootloader den Kernel und das initrd in den Speicher. Der Kernel initialisiert das initrd als sein erstes Root-Dateisystem.
- **Komponenten von initrd:**
    - Ein initrd enthält typischerweise ein minimales Set an Binärdateien und Treibern, die notwendig sind, um grundlegende Hardware wie Festplatten, Netzwerkgeräte und Dateisysteme zu initialisieren. Es enthält auch das Skript /[[linuxrc]], das als erstes Programm vom Kernel ausgeführt wird, nachdem initrd geladen wurde.