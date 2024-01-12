# Zápočtový test

## Struktura testu

- funkce $f(x,y)=\_$
	- najděte definiční obor funkce $f$ a načrtněte jej
		- je tato množina otevřená nebo uzavřená?
	- vypočítejte $\nabla f(\_,\_)$
	- ukažte, že $f$ má v bodě $(\_,\_)$ totální diferenciál a určete ho
		- pomocí lineární aproximace určete přibližně hodnoty funkce $f(x,y)$ v okolí bodu $(\_,\_)$
	- napište rovnici tečné roviny a normály ke grafu $f$ v bodě $(\_,\_,\_)$
	- nabývá funkce $f$ globálních extrémů ve svém definičním oboru nebo lokálních extrémů uvnitř?
- rovnice o třech neznámých
	- ukažte, že touto rovnicí je definovaná implicitně funkce $z=f(x,y)\in C^2(U(\_,\_))$, pro kterou je $f(\_,\_)=\_$
	- určete $\frac{\partial f}{\partial x}(\_,\_)$ a $\frac{\partial f}{\partial y}(\_,\_)$
	- pomocí lineární aproximace určete přibližně hodnoty funkce $f(x,y)$ v okolí bodu $(\_,\_)$
	- určete $\frac{\partial^2 f}{\partial x\partial y}(\_,\_)$
- vysvětlete, proč funkce $f$ nabývá na množině $M$ svých globálních extrémů (přičemž $M$ je část roviny)
	- tyto globální extrémy najděte
- výpočet integrálu nebo teoretická otázka (metriky, kompaktnost, …)

## Poznámky

- nutné a postačující podmínky totálního diferenciálu (v bodě)
	- postačující: spojité parciální derivace
	- nutné: spojitost, lineární aproximovatelnost, tečná rovina, existence parciálních derivací
- $f$ je diferencovatelná $\equiv$ má totální diferenciál
- stacionární bod … $\nabla f=\vec o$
- totální diferenciál … $Df(x_0,y_0)(\vec h)=\nabla f(x_0,y_0)\cdot\vec h$
- lineární aproximace v zásadě odpovídá rovnici tečné roviny
	- vzorec lze odvodit pomocí $f'(x)=df/dx$, kde $df=f(x)-f(a)$ a $dx=x-a$
	- místo $f'(x)$ používáme gradient
	- směrový vektor normály ke grafu odpovídá normálovému vektoru tečné roviny
- hessián
	- determinant Hesseho matice (matice druhých parciálních derivací v daném bodě)
	- když je kladný, v daném bodě je extrém
	- když je záporný, v daném bodě není extrém
- Lagrangeovy multiplikátory
	- uvést, že používám větu o LM
	- máme množinu $M$, na které hledáme extrémy
	- $G(x,y)$ označíme funkci určující množinu $M$
		- musí platit $G(x,y)=0$
	- ověříme, že $\nabla G(x,y)\neq \vec o$ na množině $M$
	- ověříme spojitost parciálních derivací
	- k existující rovnici $G(x,y)=0$ přidáme dvě rovnice vzniklé z $\nabla f(x,y)=\lambda\cdot\nabla G(x,y)$
	- $x,y$, které najdeme, nám dají globální extrémy
- podmínka existence Riemannova integrálu
	- funkce musí být omezená na daném intervalu
- Fubiniova věta – lze prohodit pořadí integrace
- kompaktní množina – každá posloupnost má konvergentní podposloupnost
- hledání extrémů v neuzavřené množině – pomocí uzávěru
- hledání lokálních extrémů
	- v bodech nespojitosti
	- tam, kde neexistuje aspoň jedna derivace
	- tam, kde jsou všechny derivace rovny nule (ve stacionárním bodě)
- spojitá funkce na kompaktní množině má globální extrémy (podle věty)
- projít vzorce na derivace
- věta o implicitní funkci
	- ověříme, že po dosazení do levé strany rovnice opravdu vyjde nula
	- ověříme spojitost parciálních derivací
	- ověříme nenulovost parciální derivace podle $z$ v daném bodě
