#HTWG
#semester5
#ESYS
#Realtime

**Reaktionszeit einer Task ist die Summe aus:**
- t<sub>E</sub>: Ausführungszeit der Task 
- D<sub>p</sub>: Summe der Verdrängungszeit (Preemption-Delay) aufgrund höher-priorer Tasks 
- t<sub>B</sub>: Summe der Blockierzeit aufgrund belegter Ressourcen durch nieder-priore Tasks 

**Realzeitbedingungen**
1. **u<sub>ges</sub> ≤ c**
   Die Auslastung u<sub>ges</sub> eines Rechensystems muss kleiner oder gleich der Anzahl Rechnerkerne c sein

2.  **t<sub>Dmax</sub>  ≥ t<sub>D</sub> ≥ t<sub>Dmin</sub>** 
   Die Reaktionszeit jeder Task muss größer oder gleich der minimal zulässigen Reaktionszeit, aber kleiner oder gleich der maximal zulässigen Reaktionszeit sein. 

**Variablen:**
- t<sub>Pmin</sub>: minimale Prozesszeit (minimale Periode)
- t<sub>Dmin</sub>: minimal zulässige Reaktionszeit (minimal Deadline)
- t<sub>Dmax</sub>: maximal zulässige Reaktionszeit (maximal Deadline) 
- t<sub>Emin</sub>: minimale Ausführungszeit der Tasks (minimal Execution time) 
- t<sub>Emax</sub>: maximale Ausführungszeit der (maximal Execution time) Tasks 
- t<sub>Ph</sub>: phase (zeit Offset wann der prozess starten soll nach dem das System gestartet ist oder anderen prozessen)

**Schreibweise temporaler Parameter**
- TASK:(t<sub>Ph</sub>; t<sub>Pmin</sub>; t<sub>Emax</sub>; t<sub>Dmax</sub>)
	- da tDmin oft trivial ist (time.sleep) wird dieser parameter meist nicht angegeben
- TASK:(t<sub>Pmin</sub>; t<sub>Emax</sub>; t<sub>Dmax</sub>)
	- wenn die Phase = 0 ist
- TASK:(t<sub>Pmin</sub>; t<sub>Emax</sub>)
	- Wenn maximale Deadline und minimale Periode gleich sind (t<sub>Pmin</sub> = t<sub>Dmax</sub>)
	
![[Realzeitnachweis-Beispieltasks.png|600]]
- V: (20;5)
- GUI: (40;15)
- MONITORING: (30;10)

#  Nachweis Priotitätsgesteuertes Scheduling
**Ziel:** Maximale Verdrängungszeit jeder Task bestimmen
### Hinreichender Schedulingtest
- wird ein Auslastungs-Grenzwert, abhängig vom jeweiligen Scheduling-Verfahren überschritten?
- Wird der Grenzwert nicht überschritten kann ein Realzeitsystem garantiert werden
**Berechnung**
- n = menge der tasks
$$u = \sum_{j=1}^{n} \frac{t_{E\text{max},j}}{\min \left(t_{D\text{max},j}, t_{P\text{min},j} \right)} \leq n \left(2^{\frac{1}{n}} - 1\right) $$
![[Auslastungsgrenze hinreichende bedingung.png|500]]

[[Beispielrechnung des Hinreichenden Realzeitnachweises (Priority Scheduling)]]

### Notwendiger Schedulingtest

Während die minimale Reaktionszeit t<sub>Rmin,i</sub> im günstigsten Fall identisch mit der minimalen Verarbeitungszeit t<sub>Emin,i</sub> ist, ist die Bestimmung der maximalen Reaktionszeit <sub>Rmax,i</sub> komplizierter: 
- Die Idee bei der Bestimmung der maximalen Reaktionszeit t<sub>Rmax,i</sub> ist, die Anforderungen an Rechenzeit der gleich- oder höherprioren Tasks aufzusummieren (diese bilden die Menge J) und der zur Verfügung stehenden Rechenzeit gegenüberzustellen. 
- Der Zeitpunkt, zu dem genauso viel Rechenzeit zur Verfügung gestellt worden ist, wie von den betrachteten Tasks benötigt wird, entspricht der maximalen Reaktionszeit <sub>Rmax,i</sub> der Task.

$$
t_{C,i}(t) = \sum_{j \in J} \left\lceil \frac{t}{t_{P\text{min},j}} \right\rceil * t_{E\text{max},j}
$$
t<sub>C</sub> = Rechenzeitanforderung
J = Menge der Tasks mit gleicher oder höherer Priorität

![[Grafische Darstellung notwendige bedingung.png]]

Da man die Funktion nicht durch umstellen lösen kann, wird ein iterativer Ansatz gewählt :
$$
t^{(l+1)} = \sum_{j \in M} \left\lceil \frac{t^{(l)}}{t_{P\text{min},j}} \right\rceil \cdot t_{E\text{max},j}
$$
[[Beispielrechnung des Notwendigen Realzeitnachweises (Priority Scheduling)]]

- Beginn der Iteration mit l = Anzahl der Tasks
- Iteration kann abgebrochen werden, sobald l = l+1

#  Nachweis EDF Scheduling

### Hinreichender Schedulingtest

$$u = \sum_{j=1}^{n} \frac{t_{Emax,j}}{\min(t_{Dmax,j}, t_{Pmin,j})} \leq Anzahl Prozessorkerne$$
- t<sub>Dmax,j</sub> ≥ t<sub>Pmin,j</sub> => erste Realzeitbedingung
	- Die notwendige und hinreichende Bedingung ist erfüllt
	- Es ist nicht mehr nötig einen notwendigen Schedulingtest durchzuführen
- t<sub>Dmax,j</sub> < t<sub>Pmin,j</sub> 
	- nur die hinreichende Bedingung ist gegeben
	- ein notwendiger Schedulingtest ist nötig

[[Beispielrechnung Hinreichender Schedulingtest (EDF)]]
### Notwendiger Schedulingtest

1. Bestimmung der Maximalen Berechnungszeit$$ x = 0 < I < kgV(t_{Dmax(1)},t_{Dmax(2)},...t_{Dmax(n)}) + max(t_{Dmin(1)},t_{Dmin(2)},...t_{Dmin(n)})$$
2. Bestimmen der einzelnen $I$ für jede Task $$ \begin{aligned} & \{k\cdot t_{Dmax}∣k∈Z,0<k\cdot t_{Dmax}<x\} \\ & = \{I_{1},I_{2},I_{3},I_{4},I_{5},...,I_{n} \} \end{aligned} $$
3. Für jedes $I$ $$t_{C,ges}(I) = \sum \left\lfloor \frac{I + t_{Pmin,i} - t_{Dmax,i} - t_{Ph,i}}{t_{Pmin,i}} \right\rfloor \cdot t_{Emax,i}$$
   Wenn:   $t_{C,ges}(I)< I$   für alle $I$ ist die notwendige Bedingung erfüllt

[[Beispielrechnung Notwendiger Schedulingtest (EDF)]]

**Grafische Darstellung Nachweis EDF Scheduling**	   
![[GrafischeDarstellungNotwendigerSchedulingTestEDF.png]]
