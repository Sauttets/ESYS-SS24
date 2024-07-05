#HTWG
#semester5
#ESYS
#Linux 

**Initramfs ist keine Ramdisk**:
- Eine Ramdisk emuliert eine Festplatte im RAM und benötigt einen entsprechenden Treiber.
- initramfs hingegen ist direkt in die VFS-Datenstrukturen integriert, was es effizienter macht.

Es wird nur so viel Hauptspeicher verwendet, wie Daten im Root-Filesystem liegen. Das bedeutet, dass der **Speicherbedarf dynamisch** ist und nur den tatsächlich benötigten Platz einnimmt.


**Einschränkungen von initramfs**
- keine Überwachung bezüglich der Root-FSGröße
- Falls das initramfs direkt ins Kernel-Immage gelinked wird (z.b. CPIO Archiv) muss die [[Lizenzen|GPL Lizenz]] eingehalten werden
![[Speicherbelegeung ohne-mit initramfs.png|500]]

Aufpassen beim umgang mit einem CPIO Archiv
- CPIO wertet Pfadangaben absolut aus. Daher mit `–no-absolute-filenames` aufrufen
``` sh
> $ mkdir /tmp/cpio 
> $ cd /tmp/cpio 
> $ zcat /usr/src/linux/usr/initramfs_data.cpio.gz | sudo cpio -i -d -H newc -no-absolute-filenames
```

**Bootablauf**
![[Bootablaufdiagramm.png]]


- Der Kernel-Parameter `rdinit=` erlaubt es, ein alternatives Programm anzugeben, das als Initialisierungsprogramm gestartet wird, anstatt des standardmäßigen `/init` im initramfs.
- Durch Setzen des `rdinit=`-Parameters kann angeben werden, dass der Kernel ein anderes Programm ausführen soll. Dies ist besonders nützlich für spezielle Anforderungen oder benutzerdefinierte Boot-Szenarien.
