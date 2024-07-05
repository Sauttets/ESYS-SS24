#HTWG
#semester5
#ESYS
#Linux 


Je nach Konfiguration des RamFS wird per default gesucht
- nach `/init` bei initramfs Konfiguration, 
- nach `/linuxrc` bei initrd Konfiguration, 
- nach `/sbin/init` bei Standard Block-Geräten

init ist dafür verantwortlich, dass die für den Betrieb des Embedded System notwendigen Programme in einer geeigneten Reihenfolge gestartet werden

skripte die init verwendet werden typischerweise in `/etc/init.d` abgelegt

- **Initialisierungsprozess:**
    - `init` ist der erste Prozess, der vom Kernel gestartet wird, wenn ein Unix-ähnliches System hochfährt. Es hat daher immer die Prozess-ID (PID) 1.
- **Prozessverwaltung:**
    - Da es der erste Prozess ist, ist es verantwortlich für das Starten und Verwalten aller anderen Prozesse im System. Es bleibt während der gesamten Laufzeit des Systems aktiv.
- **Systemzustände:**
    - `init` verwaltet die verschiedenen Runlevels (oder Targets in neueren Systemen wie systemd). Diese Runlevels definieren die Betriebszustände des Systems, wie z.B. Single-User-Modus, Multi-User-Modus, grafischer Modus usw.

## Aufgaben von init

- **Starten von Systemdiensten:**
    - Es liest Konfigurationsdateien (wie `/etc/inittab` bei traditionellen SysV-init Systemen oder Unit-Dateien bei systemd) und startet verschiedene Systemdienste und Daemons basierend auf diesen Konfigurationen.
	    - welche Rechenprozesse sollen beim Booten gestartet werden
	    - welcher Rechenprozess im Fall einer Störung der Spannungsversorgung aktiv werden soll
	    - Wie das System auf Ereignisse, z.B. die Tastenkombination CTRL-ALT-DEL reagiert
	    - Konfiguration des Runtime Levels
		    - Runlevel 1 ist der - Single-User-Mode
		    - Runlevel 2 - Multi-User-Mode
	    
- **Überwachung und Neustart von Prozessen:**
    - `init` überwacht bestimmte kritische Prozesse und startet sie bei Bedarf neu, um die Systemstabilität zu gewährleisten.

- **Shutdown und Reboot:**
    - Es führt die notwendigen Schritte aus, um das System sicher herunterzufahren oder neu zu starten, wenn entsprechende Befehle gegeben werden (z.B. durch `shutdown` oder `reboot`).

## Initmodi
- `respawn`: Terminiert der Prozess, wird er wieder gestartet 
- `wait`: Prozess wird gestartet, init wartet auf das Prozessende 
- `boot`: Prozess wird während des Bootvorgangs gestartet (nicht in einem spezifischen Runlevel)
- `powerwait/powerfail`: init startet prozess und 'wartet'/'wartet nicht' auf das Ende des Prozesses 
- `powerfailnow`: Low Battery Event 
- `ctraltdel/kbrequest`: spezielle Events vom Keyboard