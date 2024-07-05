#HTWG
#semester5
#ESYS
#Linux 

Busybox fasst viele Standardprogramme, auch in Minimalausführung, in ein einzelnes Multicall Binary zusammen.

### Multicall Binary
- Betriebssystem übergibt den Programmnamen als Argument 0
- über Sym- oder Hardlinks kann auf die einzelnen programme zugegriffen werden
- je nach Link verhält sich Busybox unterschiedlich

![[MulticallBinary.png]]

- Über `make menuconfig` können die nötigen programme in Busybox konfiguriert werden.
- Busybox ins [[04-1-RootFS|RootFS]] kopieren: `rsync -a _install/ /mnt/rootfs/`

**Vorteile eines Multicall Binaries** 
- Nur ein binary benötigt, was die Größe des Binaries reduziert und so Ressourcen spart

**Nachteile eines Multicall Binaries**
- Da es als einzelnes binary erstellt wird, ist es nicht möglich ohne neu Kompilierung ein Programm zu entfernen oder hinzuzufügen
- Das debuggen einzelner Werkzeuge im Binary ist deutlich schwieriger