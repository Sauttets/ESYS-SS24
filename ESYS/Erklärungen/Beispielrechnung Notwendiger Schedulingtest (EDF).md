![[Tabelle-EDF-RZ-Nachweis.png]]

$$ $$
$$
\begin{align}
x&=0<I<kgV(t_{Dmax(1)},t_{Dmax(2)},...t_{Dmax(n)})+max(t_{Dmin(1)},t_{Dmin(2)},...t_{Dmin(n)})\\
\\
x  & = 0 < I < kgV(20ms ,30ms ,40ms)+max(0ms, 0ms, 0ms) = 120ms \\
\end{align}
$$

Mit x = 120 kann jetzt $I$ berechnet werden

$$
\begin{aligned} 
\{k\cdot t_{Dmax}∣k∈Z,0<k\cdot t_{Dmax}<x\} = \{I_{1},I_{2},I_{3},I_{4},I_{5},...,I_{n} \} 
\end{aligned} 
$$
$$
\begin{align}
I_{V}&=\{20,40,60,80,100\} \\
I_{M}&=\{30,60,90\} \\
I_{G}&=\{40,80\} \\
I &= \{20,30,40,60,80,90,100\}
\end{align}
$$


Nachdem wir alle relevanten I berechnet haben, kann nun der Notwendige Schedulingtest durchgeführt werden
$$t_{C,ges}(I) = \sum \left\lfloor \frac{I + t_{Pmin,i} - t_{Dmax,i} - t_{Ph,i}}{t_{Pmin,i}} \right\rfloor \cdot t_{Emax,i}$$
$$
\begin{align}
t_{C,ges}(I) &= 
\left\lfloor \frac{I + 20ms - 20 ms - 0ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{I + 30ms - 30ms - 0ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{I + 40ms - 40ms - 0ms}{40ms} \right\rfloor \cdot 15ms 
\\
t_{C,ges}(I) &= 
\left\lfloor \frac{I}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{I}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{I}{40ms} \right\rfloor \cdot 15ms 
\\\\
t_{C,ges}(20) &= 
\left\lfloor \frac{20ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{20ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{20ms}{40ms} \right\rfloor \cdot 15ms 
=5ms
\\
t_{C,ges}(30) &= 
\left\lfloor \frac{30ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{30ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{30ms}{40ms} \right\rfloor \cdot 15ms 
=15ms
\\
t_{C,ges}(40) &= 
\left\lfloor \frac{40ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{40ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{40ms}{40ms} \right\rfloor \cdot 15ms 
=35ms
\\
t_{C,ges}(60) &= 
\left\lfloor \frac{60ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{60ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{60ms}{40ms} \right\rfloor \cdot 15ms 
=50ms
\\
t_{C,ges}(80) &= 
\left\lfloor \frac{80ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{80ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{80ms}{40ms} \right\rfloor \cdot 15ms 
=70ms
\\
t_{C,ges}(90) &= 
\left\lfloor \frac{90ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{90ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{90ms}{40ms} \right\rfloor \cdot 15ms 
=80ms
\\
t_{C,ges}(100) &= 
\left\lfloor \frac{100ms}{20ms} \right\rfloor \cdot 5ms +
\left\lfloor \frac{100ms}{30ms} \right\rfloor \cdot 10ms +
\left\lfloor \frac{100ms}{40ms} \right\rfloor \cdot 15ms 
=85ms
\end{align}
$$

Da für alle $I$  gilt $t_{C,ges}(I)< I$  ist es ein Realzeitsystem

![[GrafischeDarstellungNotwendigerSchedulingTestEDF.png|600]]


# Beispiel mit Abhängigkeit
zur Erinnerung: 
TASK:(t<sub>Ph</sub>; t<sub>Pmin</sub>; t<sub>Emax</sub>; t<sub>Dmax</sub>)

**T1 (6,2,3)**
**T2 (2,6,3,4)**


$$
\begin{align}
x&=0<I<kgV(t_{Dmax(1)},t_{Dmax(2)},...t_{Dmax(n)})+max(t_{Dmin(1)},t_{Dmin(2)},...t_{Dmin(n)})\\
x  & = 0 < I < kgV(3ms ,4ms)+max(0ms, 0ms) = 12ms \\
\end{align}
$$

$$
\begin{align}
I_{T1}&=\{3ms,6ms,9ms\} \\
I_{T2}&=\{4ms,8ms\} \\
I &= \{3ms,4ms,6ms,8ms,9ms\}
\end{align}
$$

$$
\begin{align}
t_{C,ges}(I) &= 
\left\lfloor \frac{I + 6ms - 3ms - 0ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{I + 6ms - 4ms - 2 ms}{6ms} \right\rfloor \cdot 3ms
\\
t_{C,ges}(I) &= 
\left\lfloor \frac{I + 3ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{I}{6ms} \right\rfloor \cdot 3ms
\\
\\
t_{C,ges}(3ms) &= 
\left\lfloor \frac{3ms + 3ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{3ms}{6ms} \right\rfloor \cdot 3ms
=2ms
\\
t_{C,ges}(4ms) &= 
\left\lfloor \frac{4ms + 3ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{4ms}{6ms} \right\rfloor \cdot 3ms
=2ms
\\
t_{C,ges}(6ms) &= 
\left\lfloor \frac{6ms + 3ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{6ms}{6ms} \right\rfloor \cdot 3ms
=5ms
\\
t_{C,ges}(8ms) &= 
\left\lfloor \frac{8ms + 3ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{8ms}{6ms} \right\rfloor \cdot 3ms
= 5ms
\\
t_{C,ges}(9ms) &= 
\left\lfloor \frac{9ms + 3ms}{6ms} \right\rfloor \cdot 2ms +
\left\lfloor \frac{9ms}{6ms} \right\rfloor \cdot 3ms
= 7ms
\\
\end{align}
$$
Da für alle $I$  gilt $t_{C,ges}(I)< I$  ist es ein Realzeitsystem

![[Grafische-Darstellung-EDF-RZ-mitPhase.png|600]]
