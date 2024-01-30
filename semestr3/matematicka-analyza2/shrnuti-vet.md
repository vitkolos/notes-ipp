# Shrnutí některých vět

- implicitní funkce
	- derivace podle $y$ je nenulová, ať je BÚNO kladná
	- v obdélníku jsou extrémy
	- nejdříve najdeme funkci
		- vezmeme funkci $\varphi_x$ jedné proměnné (pro pevné $x$)
		- ta má kladnou derivaci, takže roste, zároveň je prostá
		- přesně uprostřed okna je nulová
		- najdeme ostatní $y$, aby byla $\varphi_x$ nulová
		- tím dostaneme hledanou funkci
	- pak dokážeme její spojitost a vzorec pro derivaci
		- začneme s $0=F(x+h,f(x+h))-F(x,f(x))$
		- z $f(x+h)$ uděláme $f(x)+(f(x+h)-f(x))$
		- použijeme Lagrangeovu větu a chain rule
		- nakonec dostaneme $\frac{f(x+h)-f(x)}h=$ minus podíl parciálních derivací
		- z toho můžeme odvodit i spojitost, přičemž jako $\varepsilon$ použijeme $|h|\cdot\frac Ka$
- Fubiniho věta
	- 