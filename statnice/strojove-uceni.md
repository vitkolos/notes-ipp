# Strojové učení

## Učení s učitelem

- klasifikace, regrese (základní typy úloh)
	- úloha klasifikace spočívá v přiřazení vhodné třídy (nebo sady tříd) konkrétní položce
		- typická je binární klasifikace
	- při regresi přiřazujeme položce $x$ vhodnou funkční hodnotu $y$
- standardní evaluační metriky
	- regrese
		- mean square error, $\mathrm{MSE}=\frac1N\sum_{i=1}^N (y_i-t_i)^2$
			- $y_i$ … predikce funkční hodnoty pro $x_i$
			- $t_i$ … reálná funkční hodnota pro $x_i$ (v trénovacích/testovacích datech)
	- klasifikace
		- negative log likelihood, $\mathrm{NLL}=-\sum_{i=1}^N p_i(t_i)$
			- $t_i$ … reálná třída $x_i$
			- $p_i$ … pravděpodobnostní rozdělení, které model vrací pro $x_i$ (pravděpodobnosti, že $x_i$ náleží jednotlivým třídám)
			- místo $p_i(t_i)$ lze také zapsat $p(t_i\mid x_i)$
		- accuracy (přesnost)
			- počet správně klasifikovaných ÷ celkový počet
			- $\frac{tp+tn}{tp+tn+fp+fn}$ (u binární klasifikace)
			- nevhodná metrika, pokud jsou třídy nevyvážené (např. testujeme vzácné onemocnění)
	- binární klasifikace (navíc)
		- základní dělení výsledků klasifikace
			- predikce je pozitivní, realita (target) rovněž → true positive (TP)
			- predikce je pozitivní, realita je negativní → false positive (FP)
			- predikce je negativní, realita je pozitivní → false negative (FN)
			- predikce je negativní, realita také → true negative (TN)
		- precision, $P=\frac{tp}{tp+fp}$
		- recall, $R=\frac{tp}{tp+fn}$
		- F-measure
			- vážený harmonický průměr precision a recallu
			- $F_\beta=\frac{(\beta^2+1)PR}{\beta^2P+R}=\frac{tp+\beta^2\cdot tp}{tp+fp+\beta^2(tp+fn)}$
			- $F_1=\frac{2PR}{P+R}=\frac{tp+tp}{tp+fp+tp+fn}$
			- je užitečné mít jednu hodnotu místo dvou ($P,R$)
- ohodnocení modelu (testovací data, křížová validace, maximální věrohodnost)
	- testovací data slouží k ověření toho, jak dobře náš model generalizuje
		- snažíme se zjistit, jak dobré výsledky model vrací pro data, která dosud neviděl
		- testovací data nesmím použít v procesu trénování modelu a ladění hyperparametrů
	- pokud je potřeba ladit hyperparametry, používá se train-dev-test split
		- parametry modelu trénujeme na trénovacích datech
		- hyperparametry určujeme pomocí vývojových dat (zjistíme, pro které hodnoty hyperparametrů má model nejlepší výkon)
			- vývojová data se někdy označují jako validační (validation set)
		- k finálnímu vyhodnocení modelu slouží testovací data
	- pokud mám dat málo a nelze z nich jednoduše vyčlenit testovací (nebo vývojová) data, používá se křížová validce (cross-validation)
		- trénovací data rozdělím na $n$ dílů
		- model natrénuju na datech z $n-1$ dílů
		- na zbylých datech model vyhodnotím
		- proces opakuju pro $n$ možných voleb
		- jako výsledné skóre modelu použiju průměr průběžných hodnocení
	- maximální věrohodnost (maximum likelihood)
		- máme-li fixní trénovací data, pak likelihood $L(w)$ (kde $w$ jsou váhy modelu) se rovná součinu pravděpodobností targetů trénovacích dat
		- odhadujeme váhy modelu tak, aby byl likelihood (věrohodnost) trénovacích dat co největší
		- přesněji
			- pro model s fixními vahami $w$ máme pravděpodobnostní distribuci $p_\text{model}(x;w)$, že model vygeneruje $x$
			- pro model s fixními vahami $w$ a konkrétní řádek $x$ máme pravděpodobnostní distribuci $p_\text{model}(t\mid x;w)$, jak model klasifikuje $x$
			- místo toho zafixujeme trénovací data a budeme měnit váhy → dostaneme $L(w)=p_\text{model}(X;w)=\prod_i p_\text{model}(x_i;w)$
			- $w_\text{MLE}=\text{arg max}_w\,p_\text{model}(X;w)$
				- MLE … maximum likelihood estimation
- přeučení a regularizace (generalizační chyba, včasné zastavení trénování, L2 a L1 regularizace)
	- underfitting – model je příliš slabý (příliš jednoduchý), plně jsme nevyužili jeho potenciál
	- overfitting (přeučení) – model špatně generalizuje, příliš se přizpůsobil trénovacím datům
	- generalizační chyba
		- zachycuje, jak dobře model generalizuje
		- typicky odpovídá výkonu modelu na testovacích datech (případně lze k jejímu určení použít křížovou validaci)
			- výkon = vhodná metrika (F-measure, accuracy, …)
	- generalizační chybu lze zachytit v grafu vedle trénovací chyby (výkonu modelu na trénovacích datech)
		- pokud se testovací (generalizační) křivka přibližovala k trénovací a v určitý moment se začala vzdalovat, došlo k přetrénování (overfitting) modelu
			- je potřeba zesílit regularizaci nebo včas zastavit trénování
		- pokud se testovací křivka ani nezačala přibližovat, je potřeba trénovat déle
	- regularizace
		- intuice
			- penalizujeme modely s většími váhami
			- preferujeme menší změny modelu
			- omezujeme efektivní kapacitu modelu
			- čím je model složitější, tím větší má váhy
		- ke ztrátové (loss) funkci přičteme normu vah vynásobenou parametrem $\lambda$
			- L1 regularizace … $\lambda(|w_1|+|w_2|+\dots+|w_n|)$
			- L2 regularizace … $\lambda(w_1^2+w_2^2+\dots+w_n^2)$
				- nebo také $\lambda\lVert w\rVert^2$, případně $\frac\lambda2\lVert w\rVert^2$, aby nám vyšla hezká derivace
- prokletí dimenzionality
	- s rostoucím počtem dimenzí (features) potřebujeme čím dál víc (exponenciálně) trénovacích dat, aby model rozumně generalizoval
	- chceme mít v trénovacích datech několik vzorků pro každou kombinaci features → s každou další dimenzí potřebujeme násobně víc vzorků

## Učení založené na příkladech

- algoritmus k-nejbližších sousedů
	- regrese: $t=\sum_i\frac{w_i}{\sum_j w_j}\cdot t_i$
		- vážený průměr
	- klasifikace
		- pro uniformní váhy můžeme hlasovat (nejčastější třída vyhrává, remízy rozhodujeme náhodně)
		- jinak uvažujeme one-hot kódování $t_i$ opět můžeme použít predikci $t=\sum_i\frac{w_i}{\sum_j w_j}\cdot t_i$ (zvolíme třídu s největší predikovanou pravděpodobností)
	- volba vah (weighting)
		- uniform: všech $k$ nejbližších sousedů má stejné váhy
		- inverse: váhy jsou nepřímo úměrné vzdálenosti
		- softmax: váhy jsou přímo úměrné softmaxu záporných vzdáleností
	- jak určit nejbližší sousedy / vzdálenosti?
		- $p$-norma: $\|x\|_p=\sqrt[p]{\sum_i|x_i|^p}$
		- obvykle se používá $p\in\set{1,2,3,\infty}$
		- vzdálenost $x$ a $y$ pak lze určit jako $\|x-y\|_p$

## Lineární regrese

- analytické řešení metodou nejmenších čtverců
	- sum of squares error: $\frac12\sum_{i}(x_i^Tw-t_i)^2$
		- lze ho zapsat jako $\frac12\lVert Xw-t\rVert^2$
	- snažíme se ho minimalizovat → hledáme hodnoty, kde je derivace chybové funkce podle každé z vah nulová
		- $\frac{\partial}{\partial w_j}\frac12\sum_{i}(x_i^Tw-t_i)^2=\sum_i x_{ij}(x_i^Tw-t_i)$
		- chceme, aby $\forall j:\sum_i x_{ij}(x_i^Tw-t_i)=0$
			- $X^T(Xw-t)=0$
			- $X^TXw=X^Tt$
	- je-li $X^TX$ invertibilní, pak lze určit explicitní řešení jako $w=(X^TX)^{-1}X^Tt$
- trénování pomocí stochastic gradient descent
	- gradient descent
		- snažíme se minimalizovat hodnotu chybové funkce $E(w)$ pro dané váhy $w$ volbou lepších vah
			- spočítáme $\nabla_wE(w)$ → tak zjistíme, jak váhy upravit
			- nastavíme $w\leftarrow w-\alpha\nabla_wE(w)$
				- $\alpha$ … learning rate (hyperparametr), „délka kroku“
			- tomu se říká gradient descent
		- standard gradient descent – používáme všechna trénovací data k výpočtu $\nabla_wE(w)$
		- stochastic (online) gradient descent – používáme jeden náhodný řádek
		- minibatch stochastic gradient descent – používáme $B$ náhodných nezávislých řádků
	- algoritmus pro trénink modelu lineární regrese (minibatch SGD)
		- náhodně inicializujeme $w$ (nebo nastavíme na nulu)
		- opakujeme, dokud to nezkonverguje nebo nám nedojde trpělivost
			- samplujeme minibatch řádků s indexy $\mathbb B$
				- buď uniformně náhodně, nebo budeme chtít postupně zpracovat všechna trénovací data (to se obvykle dělá, jednomu takovému průchodu se říká epocha), tedy je nasekáme na náhodné minibatche a procházíme postupně
			- $w\leftarrow w-\alpha\frac1{|\mathbb B|}\sum_{i\in \mathbb B}((x_i^Tw-t_i)x_i)-\alpha\lambda w$
				- jako $E$ se používá polovina MSE (s $L^2$ regularizací): $E(w)=\frac1{|\mathbb B|}\sum_{i\in\mathbb B}\frac12 (x_i^Tw-t_i)^2+\frac{\lambda}2 \lVert w\rVert^2$ (stačí to zderivovat)

## Logistická regrese

- binární klasifikace (sigmoid, metody trénování)
	- aktivační funkce sigmoid … $\sigma(x)=\frac1{1+e^{-x}}$
	- predikce $y(x;w)=\sigma(\bar y(x;w))=\sigma(x^Tw)$
		- správnou třídu získáme zaokrouhlením
		- přesná hodnota se rovná pravděpodobnosti, že je $x$ klasifikováno jako 1 (uvažujeme třídy 0 a 1)
		- $\bar y$ … „lineární složka“ logistické regrese
	- velikost vektoru vah $w$ odpovídá počtu features
		- nesmíme zapomenout také na bias, ten opět může být reprezentován jako další váha
	- při trénování se jako ztrátová funkce (loss) používá negative log likelihood (NLL)
		- pravděpodobnost targetu $t$ pro položku $x$ lze vyjádřit jako $p(t\mid x;w)=\sigma(x^Tw)^{t}(1-\sigma(x^Tw))^{1-{t}}$
	- algoritmus trénování pomocí minibatch SGD
		- klasifikujeme do tříd $\set{0,1}$, na vstupu máme dataset $X$ a learning rate $\alpha\in\mathbb R^+$
		- náhodně inicializujeme $w$ (nebo nastavíme na nulu)
		- opakujeme, dokud to nezkonverguje nebo nám nedojde trpělivost
			- samplujeme minibatch řádků s indexy $\mathbb B$
			- $w\leftarrow w-\alpha\frac1{|\mathbb B|}\sum_{i\in \mathbb B}(\sigma(x^Tw)-t)x-\alpha\lambda w$
				- jako $E$ se používá NLL (s $L^2$ regularizací)
				- výsledek se překvapivě podobá lineární regresi
					- gradient je také $(y(x)-t)x$
- klasifikace do více tříd (softmax, metody trénování)
	- klasifikujeme do jedné z $K$ tříd
	- parametry modelu: váhová matice $W$ (sloupce odpovídají třídám, řádky featurám), vektor biasů (jeden bias za každou třídu)
	- aktivační funkce … $\text{softmax}(z)_i=\frac{e^{z_i}}{\sum_je^{z_j}}$
		- softmax je invariantní k přičtení konstanty $\text{softmax}(z+c)_i=\text{softmax}(z)_i$
		- $\sigma(x)=\text{softmax}([x,0])_0=\frac{e^x}{e^x+e^0}=\frac1{1+e^{-x}}$
	- klasifikace: $p(C_i\mid x;W)=y(x;W)_i=\text{softmax}(\bar y(x;W))_i=\text{softmax}(x^TW)_i$
		- softmax zajišťuje normalizaci (aby se pravděpodobnosti sečetly na jedničku)
	- z linearity $\bar y$ lze dokázat, že oblasti tříd jsou konvexní – nemůže se stát, že by na úsečce mezi dvěma body v jedné třídě byl bod v jiné třídě
	- algoritmus trénování pomocí minibatch SGD
		- klasifikujeme do tříd $\set{0,\dots,K-1}$, na vstupu máme dataset $X$ a learning rate $\alpha\in\mathbb R^+$
		- náhodně inicializujeme $w$ (nebo nastavíme na nulu)
		- opakujeme, dokud to nezkonverguje nebo nám nedojde trpělivost
			- samplujeme minibatch řádků s indexy $\mathbb B$
			- $w\leftarrow w-\alpha\frac1{|\mathbb B|}\sum_{i\in \mathbb B}\left((\text{softmax}(x^TW)-1_t)x^T\right)^T-\alpha\lambda w$
				- jako $E$ se používá NLL (s $L^2$ regularizací)
				- srovnání gradientu logistické regrese
					- binary: $(y(x)-t)x$
					- multiclass: $((y(x)-1_t)x^T)^T$
				- přičemž $1_t$ je one-hot reprezentace targetu $t$ (tedy vektor s jedničkou na $t$-té pozici a nulami všude jinde)

## Rozhodovací stromy

- algoritmus učení a kritéria větvení
- prořezávání

## Metoda podpůrných vektorů

- klasifikátor pro lineárně separabilní třídy
- klasifikátor pro lineárně neseparabilní třídy
- jádrové funkce
- klasifikace do více tříd

## Kombinace více modelů

- bagging a boosting
- metoda náhodných lesů

## Statistické testy

- studentův t-test (jednovýběrový a dvouvýběrový)
- chí-kvadrát test (test dobré shody)

## Učení bez učitele

- shlukování (algoritmus k-means)
- hierarchické shlukování
- redukce dimenzionality (analýza hlavních komponent)
