- poznámky
	- bacha na čísla verzí u Pythonu a balíčků
	- používat pole v numpy
- lineární regrese
	- dvě možnosti
		- explicitní
			- pozitiva: přesnost
			- negativa: outliers dělají problémy
		- SGD
			- pozitiva: méně paměti, regularizace
			- negativa: globální optimum nezaručeno
	- SGD + momentum
		- https://distill.pub/2017/momentum/
	- AdaGrad
	- AdaDelta
	- Adaptive Moment Estimation (ADAM)
- co máme
	- data $(x,y)\in\mathbb R^2$
	- model $f(x)=y,\;f:\mathbb R\to \mathbb R$
		- při lineární regresi konkrétně $y=ax+b$
	- parametry $\theta=(a,b)\in\mathbb R^2$
	- predikce $f_\theta(x)=y,\;f:\mathbb R^3\to \mathbb R$
	- loss $L(\theta,(x,y)),\;L:\mathbb R^4\to \mathbb R$
- $\text{softmax}(x)_i=\frac{e^{x_i}}{\sum_{k=0}^n e^{x_k}}$
- $f(x)_i=\frac{|x_i|}{\sum|x|}$
	- prohodilo by se pořadí (jelikož záporná čísla by se zobrazila mezi kladná čísla)
- $f_2(x)_i=\frac{x_i-\min(x)}{\sum|x-\min(x)|}$
	- u minima by to byla nula, což by nám znemožnilo např. u dvojprvkového vektoru vyjádřit nejistotu
- poissonovská regrese – viz slidy z roku 2022/2023
	- lze použít k řešení soutěžní úlohy
- time splines
	- něco jako one hot
	- úterý kóduju tak, že dám např. 0.8 úterý, 0.1 pondělí a 0.1 středě 
