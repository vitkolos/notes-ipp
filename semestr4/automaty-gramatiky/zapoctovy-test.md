# Zápočtový test

## Studijní materiály

- [řešení testů Vladana Majerecha](https://ktiml.mff.cuni.cz/~maj/2023NTIN071.html)
- [moodle kurz Marty Vomlelové](https://dl1.cuni.cz/course/view.php?id=5119)
- [skriptíčka Martina Mareše](https://mj.ucw.cz/vyuka/automaty/automaty.pdf)

## Praktické otázky

### Konečný automat

- základní KMP automat
- průnik a rozdíl automatů
- determinizace a redukce automatu

### Regulární výraz

- konstrukce automatu podle regulárního výrazu
- konstrukce regulárního výrazu podle popisu přijímaných slov
- konstrukce regulárního výrazu na základě konečného automatu

### Další praktické otázky

- zařazení jazyka slov tvaru $b|k^T$, kde $b$ je binární zápis čísla a $k$ je zápis téhož čísla v konkrétní číselné soustavě, do Chomského hierarchie
	- někdy je jazyk kontextový (monotónní), jindy i bezkontextový (v závislosti na vztahu číselných soustav)
	- čtyřková jde bezkontextově, jedničková a trojková jdou kontextově (monotónně)
- převod bezkontextové gramatiky do Chomského normální formy
	- Chomského normální forma – povolená jsou pouze pravidla ve tvaru $X\to YZ$ nebo $X\to a$, přičemž lze deklarovat $\lambda\in L$
		- kde $\lambda$ označuje prázdné slovo
	- moc dlouhá pravidla řešíme nadtrháváním
	- dlouhá pravidla s terminály řešíme přidáním odpovídajících neterminálů
	- pravidlo typu $T\to U$ musíme převést náhradou $U$ pravými stranami pravidel s $U$ na levé straně
	- pro pravidlo tvaru $U\to\lambda$ musíme pravidlo $T\to UV$ upravit na $T\to UV\mid V$
		- tady vzniklo problematické pravidlo $T\to V$, ale to řešíme způsobem uvedeným výše
- převod monotónní gramatiky do kontextového tvaru
	- např. $AB\to CD$ převedeme na $AB\to\bar AB\to\bar A\bar B\to C\bar B\to CD$
	- pokud by se mezi jednotlivé kroky přepisování vloudila nějaká pravidla operující se znaky z této dvojice, mohli bychom je přesunout před první krok nebo za poslední krok
- jazyk slov s mocninným počtem písmen
	- nejde bezkontextově, existuje monotónní gramatika

## Teoretické otázky

### Důkaz neregularity

- pumping lemma
	- nechť $L$ je regulární jazyk
	- $(\exists n\in\mathbb N)(\forall w\in L):|w|\geq n\implies w=\alpha\beta\gamma$
		- $|\beta|\gt 0$
		- $|\alpha\beta|\leq n$
		- $\forall t\geq 0:\alpha\beta^t\gamma\in L$
	- jelikož je $L$ regulární, existuje automat $A$ rozpoznávající $L$
		- za $n$ zvolíme počet stavů tohoto automatu
	- k důkazu neregularity $L_{01}=\set{0^k1^k\mid k\in\mathbb N}$ použijeme slovo $w=0^n1^n$, kde $n$ je konstanta z lemmatu
		- $|\alpha\beta|\leq n\implies 1\notin\alpha\beta$
		- slovo $\alpha\beta^t\gamma$ pro $t\neq 1$ má jiný počet nul než jedniček, tedy nepatří do jazyka, což je spor
- uzávěrové vlastnosti
	- mějme regulární jazyky $L,M$, pak $L\cup M$, $L\cap M$, $L-M$ a $\overline L$ jsou také regulární
		- kde $\overline L=\Sigma^*-L$ (doplněk)
	- důkaz neregularity jazyku slov se stejným počtem nul a jedniček
		- jazyk slov $0^*1^*$ je zjevně regulární
		- průnik těchto dvou jazyků je neregulární jazyk $L_{01}$
	- podobně umíme odvodit, že jazyk slov s různým počtem nul a jedniček není regulární a že jazyk slov tvaru $0^i1^j$, kde $i\neq j$ není regulární

### Důkaz nebezkontextovosti

- pumping lemma pro bezkontextové jazyky
	- nechť $L$ je bezkontextový jazyk
	- $(\exists n)(\forall w\in L):|w|\geq n\implies w=u_1u_2u_3u_4u_5$
		- $\forall k\geq 0:u_1u_2^ku_3u_4^ku_5\in L$
		- $|u_2u_3u_4|\leq n$
		- $|u_2u_4|>0$
- uzávěrové vlastnosti
	- bezkontextové jazyky jsou uzavřené na sjednocení, konkatenaci, iterace, pozitivní iterace, zrcadlový obraz

### Další teoretické otázky

- podtrhávací pumping lemma
	- dvě varianty – pro regulární i bezkontextové jazyky
	- obecně místo délek slov počítáme počty podtržených písmen (všechny „absolutní hodnoty“ ve lemmatech takto nahradíme)
	- pro CFL asi [Ogdenovo lemma](https://en.wikipedia.org/wiki/Ogden%27s_lemma)?
- normální formy gramatik
	- $\mathcal L_0$ … $\alpha\chi\beta\to\alpha\gamma\beta$
		- $\alpha,\beta\in (V_N\cup V_T)^*$
		- $\chi\in V_N$
		- $\gamma\in (V_N\cup V_T)^*$
	- $\mathcal L_1$ … $\alpha\chi\beta\to\alpha\gamma\beta$
		- $\alpha,\beta\in(V_N\cup V_T)^*$
		- $\chi\in V_N$
		- $\gamma\in (V_N\cup V_T)^+$
	- $\mathcal L_2$ … $X\to YZ\mid a$
		- $X,Y,Z\in V_N$
		- $a\in V_T$
	- $\mathcal L_3$ … $X\to aY\mid\lambda$
		- $X,Y\in V_N$
		- $a\in V_T$
- dvoucestný konečný automat vs. jednocestný konečný automat
	- stejně silné
- dvoucestný zásobníkový automat vs. jednocestný zásobníkový automat
	- existuje dvoucestný přijímající $0^n1^n2^n$, jednocestný nikoliv
- vztah mezi bezkontextovými gramatikami a jazyky přijímanými nedeterministickými zásobníkovými automaty prázdným zásobníkem
	- viz prezentace
