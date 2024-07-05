
![[Tabelle-EDF-RZ-Nachweis.png]]
$$u = \sum_{j=1}^{n} \frac{t_{Emax,j}}{\min(t_{Dmax,j}, t_{Pmin,j})} \leq Anzahl Prozessorkerne$$

$$u = \frac{5}{20}+\frac{15}{40}+\frac{10}{30} = \frac{23}{24} \approx 0,958 \leq 1$$
Da der hinreichende Schedulingtest erfolgreich war (da $u\leq 1$) muss kein notwendiger Scheduling test mehr durchgeführt werden