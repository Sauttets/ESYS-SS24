
$$u = \sum_{j=1}^{n} \frac{t_{E\text{max},j}}{\min \left(t_{D\text{max},j}, t_{P\text{min},j} \right)} \leq n \left(2^{\frac{1}{n}} - 1\right) $$

![[Realzeitnachweis-Beispieltasks.png|600]]
$$ \begin{aligned} \text{TASK V: } & (20;5) \\ \text{TASK GUI: } & (40;15) \\ \text{TASK MONITORING: } & (30;10) \end{aligned} $$
Berechnung der Summenkomponenten: $$ \begin{aligned} \text{Für TASK V:} & \quad \frac{t_{E\max,1}}{t_{P\min,1}} = \frac{5}{20} = 0.25 \\
\text{Für TASK GUI:} & \quad \frac{t_{E\max,2}}{t_{P\min,2}} = \frac{15}{40} = 0.375 \\ 
\text{Für TASK MONITORING:} & \quad \frac{t_{E\max,3}}{t_{P\min,3}} = \frac{10}{30} = 0.333 \end{aligned} $$ $$ u = 0.25 + 0.375 + 0.333 = 0.958 $$ 
Überprüfung der rechten Seite der Ungleichung: $$ \begin{aligned} n (2^{\frac{1}{n}} - 1) &= 3 (2^{\frac{1}{3}} - 1) \approx 0.7797\end{aligned} $$ $$ 0.958 \leq 0.7797 \quad \text{(nicht erfüllt, da \( 0.958 > 0.7797 \))} $$

![[Auslastungsgrenze hinreichende bedingung.png|600]]
