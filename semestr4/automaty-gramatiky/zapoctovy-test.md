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
	- někdy je jazyk kontextový, jindy i bezkontextový (v závislosti na vztahu číselných soustav)
	- todo
- převod bezkontextové gramatiky do Chomského normální formy
	- Chomského normální forma – povolená jsou pouze pravidla ve tvaru $X\to YZ$ nebo $X\to a$, přičemž lze deklarovat $\lambda\in L$
	- moc dlouhá pravidla řešíme nadtrháváním, dlouhá pravidla s terminály řešíme přidáním neterminálů
	- pravidlo typu $S\to T$ musíme převést náhradou $T$ pravými stranami pravidel s $T$ na levé straně
- převod monotónní gramatiky do kontextového tvaru
	- např. $AB\to CD$ převedeme na $AB\to\bar AB\to\bar A\bar B\to C\overline B\to CD$
	- pokud by se mezi jednotlivé kroky přepisování vloudila nějaká pravidla operující se znaky z této dvojice, mohli bychom je přesunout před první krok nebo za poslední krok
- jazyk slov s mocninným počtem písmen
	- todo

## Teoretické otázky

### Důkaz neregularity

- pumping lemma
	- nechť $L$ je regulární jazyk
	- $(\exists n\in\mathbb N)(\forall w\in L):|w|\geq n\implies w=\alpha\beta\gamma$
		- $\beta\neq\lambda$
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
- uzávěrové vlastnosti

### Další teoretické otázky

- podtrhávací pumping lemma
- normální formy gramatik
- dvoucestný konečný automat vs. jednocestný konečný automat
- dvoucestný zásobníkový automat vs. jednocestný zásobníkový automat
- vztah mezi bezkontextovými gramatikami a jazyky přijímanými nedeterministickými zásobníkovými automaty prázdným zásobníkem
