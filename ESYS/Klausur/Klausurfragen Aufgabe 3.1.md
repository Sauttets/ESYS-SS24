#### Was ist der zweck des Cron-Daemon?
Der Zweck des Cron-Daemon ist es, zeitgesteuerte Aufgaben (Cron-Jobs) auf einem Unix-ähnlichen Betriebssystem auszuführen. Der Cron-Daemon ermöglicht es Benutzern und Administratoren, Aufgaben zu bestimmten Zeiten und Intervallen automatisch ausführen zu lassen. So können periodische Aufgaben, wie z.b. die Protokollierung Automatisiert werden.

#### Was ist logrotate und warum ist es wichtig für embedded Systeme?
logrotate ist ein Programm, das Logdateien rotiert, um Speicherplatz zu sparen und Überläufe zu verhindern. Es ist wichtig für embedded Systeme, da kontinuierliches Loggen zu Speicherknappheit und Systemausfällen führen kann. Es ist zu beachten, dass logs entsprechend nicht für längere Zeit gespeichert werden, was dazu führ das logs zeitnah ausgelesen oder in einen persistenten Speicherbereich kopiert werden müssen, um evtl. benötigte Informationen nicht zu verlieren.

#### In einem System sind im /etc/init.d verzeichnis folgende skripte hinterlegt: K99HelloWorld, K98StartupMessage, S99ByeWorld, S98ShowUptime. Wie ist die Reihenfolge in der die Skripte aufgerufen werden?

1. S98ShowUptime
2. S99ByeWorld
3. K98StartupMessage
4. K99HelloWorld.

#### Was ist das NTP und warum ist es überhaupt notwendig?
Da nicht jeder computer eine eingebaute Uhr haben kann, die immer weiter läuft auch wahrend sich ein Computer im Ausgeschalteten Zustand befindet, hat ein Computer beim einschalten unter Umständen keine moeglichkeit zu wissen, wie viel Uhr es momentan ist. Er könnte lediglich Zeit relativ zu seinem Einschalten anzeigen. Um jedoch die Zeit auch zwischen Geräten bis auf ein paar Millisekunden synchron zu halten, wird über das NTP über time server die aktuelle Uhrzeit abgefragt, und somit in regelmässigen abständen kontrolliert, ob die Zeit noch akkurat ist und falls notwendig nachjustiert.

#### Was ist ein Overlay und weshalb wurde eines in der Laboraufgabe 3.1 Konfiguriert? Sinn und Zweck des Overlays.
Ein Overlay ist ein Dateibaum, welches direkt über das zugrundeliegende Root-Filesystem gestülpt wird. Entwickler können darüber, temporäre Änderungen vornehmen, ohne die Basisinstallation zu verändern. Es können auch mehrere Overlays pro FS existieren, jedoch darf das FS nicht verändert werden, weil sonst keine älteren Overlays mehr funktionieren.

In der Aufgabe wurde dieses benutzt, um verschiedenste Skripte für Systemdienste wie ntpd (Timekeeping) oder lighttpd (Webserver) in das FS zu integrieren. Ein Overlay dafür zu verwenden, hat den Vorteil, dass Änderungen schneller getestet und umgesetzt werden können als auch gegebenenfalls mehrere Versionen erstellt werden können, ohne das zugrundeliegende FS zu zerstören.

#### Wie erstellen und konfigurieren Sie ein Post-build-Skript, das ein erzeugtes rootfs.cpio.gz in das Wurzelverzeichnis eines TFTP-Servers kopiert und sicherstellt, dass die richtigen Berechtigungen gesetzt sind?

Beispiel Post-build Skript:    
```sh 
#!/bin/sh  
TARGET_DIR=$1  
TFTP_ROOT=/srv/tftp  
cp ${TARGET_DIR}/[rootfs](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74418 "RootFS").cpio.gz ${TFTP_ROOT}/  
chmod 644 ${TFTP_ROOT}/[rootfs](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74418 "RootFS").cpio.gz  
# Überprüfen, ob der Kopiervorgang erfolgreich war  
if [ $? -eq 0 ]; then  
	echo "[rootfs](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74418 "RootFS").cpio.gz successfully copied to TFTP root."  
else  
	echo "Error copying [rootfs](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74418 "RootFS").cpio.gz to TFTP root."  
	exit 1  
fi 
```
Sicherstellen, dass das Skript ausführbar ist (chmod +x post-build.sh).

#### Welche Schritte sind erforderlich, um ein eigenes Paket in Buildroot zu erstellen und zu integrieren?
Ein eigenes Paket in Buildroot zu erstellen, erfordert das Anlegen eines Paketverzeichnisses und das Erstellen einer Config.in sowie einer .mk-Datei, die das Bauen des Pakets steue  
rt. Anschließen muss das Paket noch zur per source "package/<package_name>/Config.in" der "Root" Config hinzugefügt werden.  
Diese Dateien definieren, wie das Paket heruntergeladen, konfiguriert und ins Target-Filesystem installiert wird. Diese Flexibilität ermöglicht es Entwicklern, maßgeschneiderte Software effizient in ein Buildroot-basiertes System zu integrieren

#### Wie kann das Wissen über init-Skripte genutzt werden, um die Startreihenfolge von Diensten in einem Embedded Linux System zu steuern?
Die Startreihenfolge kann durch die Verwendung von rcS Skritpen über inittab durch die Benennung der Skripte im Verzeichniss /etc/init.d bestimmt werden.  
Dabei gibt die Nummer nach dem Festlegen ob das Skript beim Hoch- oder Herunterfahren aufgerufen werden soll die Reihenfolge an.  
S|K\<Nummer>\<Name>    
Diese Methode ermöglicht eine flexible und einfache Konfiguration der Dienstinitialisierung und gewährleistet, dass Abhängigkeiten korrekt behandelt werden.

#### Beschreiben Sie die Rollen von Pre-build-, Inter-build- und Post-build-Skripten in Buildroot.
- Pre-build-Skripte laufen nach Abschluss des Build-Prozesses, aber bevor das Dateisystem gepackt wird. 
- Inter-build-Skripte werden innerhalb der fakeroot-Umgebung ausgeführt, nachdem alle Pakete installiert sind. 
- Post-build-Skripte laufen, nachdem das Ziel-Dateisystem in ein Image gepackt wurde.

#### Wie konfiguriert man logrotate, um Logs täglich zu rotieren und 3 rotierte Logs mit einer Größenbeschränkung von 10k beizubehalten?
Siehe folgendes Beispielskript unter /etc/logrotate.d/messages.conf:  
```
/var/log/messages {  
    su root root  
    rotate 3  
    daily  
    size 10k  
    compress  
    delaycompress  
    create  
}
```
#### Vorteile und Nachteil von RootFS im RAM
**Vorteile:**
- Schneller Zugriff
- Schnelles booten da kein Filesystem check
- Flashspeicher nicht abgenutzt 
- Gleiche Konfiguration nach jedem reboot
**Nachteile:**
- Anderung am [RootFS](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74418 "RootFS") gehen nach reboot verloren
- Weniger RAM zu Verfugung
##### Wie kann man trotzdem persistent Daten speichern?
Ein extra Speichermedium formatieren, partitionieren und aufs [RootFS](https://moodle.htwg-konstanz.de/moodle/mod/resource/view.php?id=74418 "RootFS") mounten. Speichermedium kann Netzwerkdisk oder echte Disk sein.

Mounten mit `mount /dev/... /mount/point` oder ein Eintrag im `/etc/fstab`
