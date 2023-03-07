# Počítačové systémy

- …
- ABI (…)
- MIPS registry – jejich účely (jak by se měly používat) jsou popsány v MIPSovém ABI
	- je lepší používat přímo jména registrů v ABI – aby případné přečíslování registrů nedělalo problém
	- různé funkce registrů (…)
- základní instrukce
	- součet dvou registrů, uložení do (třetího) registru
		- na rozdíl od x86 umí MIPS uložit výsledek do třetího registru
	- přičtení 16bit. konstanty k registru, uložení do registru
	- podobně rozdíl, odečtení konstanty
	- logické operace – and, or, xor, nor (or + negace)
	- negace se dělá pomocí `nor $t1,$t2,$t2`
	- 