# Algoritmy a datové struktury 2

## Hledání v řetězci

- značení
	- jehla $\iota$
		- $J=|\iota|$
	- seno $\sigma$
		- $S=|\sigma|$
	- abeceda $\Sigma$
		- předpokládáme konečnost a malou konstantní velikost
	- slova/řetězce $\alpha,\beta,\gamma,\dots$
	- znaky $a,b,c\dots$
	- délka řetězce $|\alpha|$
	- prázdný řetězec $\varepsilon$
		- $|\varepsilon|=0$
	- zřetězení $\alpha\beta$
	- i-tý znak $\alpha[i]$ (počítáme od nuly)
	- podřetězec $\alpha[i:j]$ (od i-tého znaku do (j-1). znaku včetně)
	- prefix $\alpha[:j]=\alpha[0:j]$
	- suffix $\alpha[i:]=\alpha[i:|\alpha|]$
	- $\alpha[:]=\alpha$
- pozorování
	- prázdný řetězec je prefixem i suffixem jakéhokoliv řetězce
	- každý řetězec je prefixem i suffixem sebe sama
	- každý podřetězec se dá zapsat jako prefix nějakého suffixu nebo suffix nějakého prefixu
- jak najít jehlu
	- můžeme hledat jehlu na každém indexu sena → $\Theta(J\cdot S)$
	- můžeme po nenalezení přeskočit dál → nefunguje, viz seno "clanekokokosu", jehla "kokos"
