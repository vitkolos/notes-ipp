# Úvod do strojového učení v Pythonu

- https://ufal.mff.cuni.cz/courses/npfl129
- https://github.com/ufal/npfl129/
- Piazza
	- primární způsob komunikace
	- čte ji víc lidí než e-mail, takže je větší šance, že nám někdo odpoví
	- nedávat tam zdrojový kód (do veřejných otázek)
- bodování
	- zápočet – alespoň 70 standardních bodů
	- standardní body nad 70 se přenáší ke zkoušce
	- bonusové body lze získat soutěžemi a dalšími aktivitami nad rámec, také se přenáší ke zkoušce
- definice strojového učení
	- pomocí zkušenosti (dat) se zlepšuje metrika na nějaké úloze
	- možné úlohy: klasifikace (přiřazení vstupu do diskrétní kategorie), regrese (přiřazení reálného čísla nebo vektoru reálných čísel), předvídání struktury, odstraňování šumu
	- metriky: accuracy (jak dobře se při klasifikaci trefujeme), …
	- zkušenost
		- supervised (učení s učitelem) – máme olablovaná data
		- unsupervised (učení bez učitele) – nemáme žádné labely, učíme se vidět vzory v datech
		- reinforcement learning (zpětnovazebné učení) – např. aby byl šachový program lepší než nejlepší hráči
- základní úlohy
	- mějme vstup $x\in\mathbb R^D$
	- regrese: pro $x$ hledáme reálnou proměnnou $t\in\mathbb R$
	- klasifikace: máme $K$ labelů, pro dané $x$ chceme najít ten správný
		- můžeme určit třídu
		- můžeme určit pravděpodobnostní distribuci tříd
	- obvykle máme trénovací sadu dvojic $(x,t)$
	- rozdělíme data na trénovací a testovací – aby bylo učení dost obecné
- notace
	- tenzor je nadkrychle čísel
	- všechny vektory jsou sloupcové
		- do matic je skládáme jako řádky
- vstupní data
	- trénovací množina $X\in\mathbb R^{N\times D}$
		- $N$ instancí, každé odpovídá $D$ reálných čísel
		- dimenze vstupu = feature
	- při učení s učitelem máme target $t$ pro každou instanci
		- v regresi … $t\in\mathbb R^N$
		- v klasifikaci … $t\in\set{0,1,\dots,K-1}$

## Lineární regrese

- lineární regrese
	- $y(x;w,b)=x^Tw+b$
		- $w$ … váhy
		- $b$ … bias (jindy se označuje jako intercept)
		- protože je otrava zacházet s biasem, někdy se k vektorům přidávají na konec jedničky, takže místo $b$ máme $1\cdot w_{d+1}$
	- chceme změřit, jak se nám regrese daří
		- použijeme mean squared error (MSE) nebo taky funguje součet druhých mocnin chyb (dělený dvěma)
	- co když matice $X^TX$ není regulární? můžeme přičíst náhodný šum (dost malý)
- overfitting, underfitting
	- overfitting … model funguje dobře na trénovacích datech, ale nefunguje na testovacích datech
	- kapacita modelu – slouží k ovlivňování underfittingu a overfittingu
		- representational capacity
		- effective capacity
		- čím větší kapacita modelu, tím větší pravděpodobnost overfittingu
	- dvě křivky – chyba na trénovacích a testovacích datech
		- mezera mezi nimi = generalization gap
	- cílem je najít minimum křivky chyby na trénovacích datech
		- "sweet spot"
	- jak se zbavit overfittingu
		- použít více dat
		- regularizace – jakýkoliv krok k větší generalizaci modelu
			- příkladem regularizace je snižování kapacity modelu
	- $L^2$-regularizace
		- upřednostňuje „jednodušší“ modely, tedy ty, které mají menší váhy
		- obvykle se aplikuje na opravdové váhy, ne na bias
		- důsledkem je omezení efektivní kapacity modelu
			- pro větší lambda nám kapacita přestane stačit – daty se v podstatě proloží přímka
			- lambda … regularization rate 
		- matice, kterou nakonec použijeme, je nutně regulární, takže jsme vyřešili problém s inverzní maticí
- volba hyperparametrů
	- učící algoritmus nenastavuje hyperparametry
	- validační/vývojová sada dat se používá k určení hyperparametrů
	- takže data dělíme mezi trénovací, vývojová a testovací (obvykle v poměru 60 %, 20 %, 20 %)
	- zatím jsme měli hyperparametry $M$ (stupeň polynomu) a $\lambda$ („úroveň regularizace“)
- gradient descent
	- někdy se hodí hledat nejlepší váhy iterativně
	- hledáme $\text{arg}_w\min E(w)$
	- můžeme použít gradient descent $w\leftarrow w-\alpha\nabla_wE(w)$
	- $\alpha$ … learning rate
	- přístupy
		- standard/batch gradient descent – použijeme všechna trénovací data
		- stochastic/online gradient descent (SGD) – po jednom vybíráme náhodné příklady z trénovacích dat
			- unbiased, but noisy
		- minibatch stochastic gradient descent
	- dá se dokázat, že SGD za určitých podmínek téměř jistě konvrguje
- feature types
	- polynomial features
	- categorical one-hot features
- features je potřeba normalizovat, abychom mohli pro všechny používat stejný learning rate
	- odečtením minima a vydělením rozdílem maxima a minima data dostaneme mezi nulu a jedničku
	- velký problém jsou outliers
		- dá se to řešit standardizací
		- data budou mezi -1 a 1
		- nebo se můžeme zbavit outlierů

## Binární klasifikace

- klasifikujeme data do dvou tříd
- nejjednodušší metrika je úspěšnost (accuracy)
	- poměr správně klasifikovaných dat
- budeme hledat nadrovinu, která nám oddělí jednu třídu od druhé
	- nadrovina … $x^Tw=0$
	- jedna třída … $x^Tw>0$
	- druhá třída … $x^Tw\lt 0$
- budeme uvažovat množinu tříd $\set{-1,+1}$, tedy target $t\in \set{-1,+1}$
- $t_ix_i^Tw\gt 0$
- perceptron
- poznámka: slajdy se s *výstražnou sumou* si nemusíme pamatovat
- problémy perceptronu
	- když není vstup lineárně separovatelný, algoritmus nikdy neskončí
	- algoritmus vrátí jedinou predikci, neumí vrátit pravděpodobnosti více predikcí
	- ale hlavně, algoritmus perceptronu najde nějaké řešení, ne nutně dobré řešení, protože když už to řešení najde, nemůže ho dále měnit/zlepšovat
- teorie informace
	- vlastnosti $I(X)$
		- $P(x)=1\implies I(X)=0$
		- $P(x,y)=P(x)P(y)\implies I(x,y)=I(x)+I(y)$
		- $\forall x:I(x)\geq 0$
	- $I(x)\equiv -\log P(x)=\log\frac1{P(x)}$
	- entropie $H(P)$
	- cross-entropy $H(P,Q)\geq H(P)$
		- jak jsem překvapený, když si myslím $Q$, ale ve skutečnosti se děje $P$
	- Gibbsova nerovnost
		- $H(P,Q)\geq H(P)$
		- $H(P,Q)=H(P)\iff P=Q$
	- KL divergence
	- normální rozdělení
		- centrální limitní věta
		- princip maximální entropie
- odhad maximální věrohodnosti
	- $L(w)=p_\text{model}(X;w)=\prod_{i=1}^Np_\text{model}(x_i;w)$
- binární logistická regrese
- multiclass logistic regression
	- místo váhového vektoru budeme mít matici vah
	- místo funkce sigmoid použijeme funkci softmax
	- $\text{softmax}(z)_i=\frac{\exp(z_i)}{\sum_j\exp(z_j)}$
	- vyžadujeme, aby data tvořila nějaké konvexní útvary
- multilayer perceptron
	- vstupní vrstva a výstupní vrstva „neuronů“
	- mezi nimi je skrytá vrstva
	- skrytá vrstva nám jakoby vyrábí features pro lineární model
	- tip: `numpy.logsumexp`
- regularizace pomocí dropoutu
	- při trénování zahazujeme některé neurony
	- tím nutíme model, aby byl robustnější
- věta o univerzální aproximaci
	- máme model, který může modelovat cokoliv
	- ale neznáme konkrétní $H$
	- a taky nevíme, jak se naučit cokoliv
- Lagrangeovy multiplikátory
	- hledáme extrém na oblasti vymezené omezující podmínkou (rovností)
	- v bodě extrému bude gradient kolmý na oblast
- F-skóre
	- harmonický průměr precision a recall
	- pokud nás víc zajímá recall, tak se používá parametr $\beta$
	- macro – průměr F skóre
	- micro – F skóre z globálního precision a recallu

## Reprezentace textu

- jak reprezentovat dokument
	- jako „bag of words“ – vektor slov, jedničky u slov, která v dokumentu jsou, jinak nuly
	- normalizovaný vektor frekvencí slov
	- můžeme slovům přiřadit váhu podle toho, jestli se v dokumentech obvykle vyskytují (např. určitý člen bude mít nízkou váhu)
		- v přirozených jazycích se slova řídí Zipfovým zákonem
			- zastoupení slov (obecně v textech) se přibližně řídí hyperbolou
		- proto se používá logaritmus, aby se to normalizovalo
	- mutual information
	- vstupní slovo můžeme reprezentovat jako one-hot vector
	- násobíme ho váhovou maticí – tomu říkáme word embedding
		- vektory pro příbuzná slova jsou blízko
		- CBOW
		- SkipGram
			- negative sampling
	- dimenzí u embeddingu je typicky pár set
	- když chceme klasifikovat větu, tak můžeme posčítat embeddingy jejich slov
	- někdy se hodí při embeddingu zohledňovat kontext slova – některá slova mají více významů

## Metoda nejbližších sousedů

- k-Nearest Neighbors
- trénovací data uložíme do vhodné datové struktury
- když nám přijdou data ke klasifikaci, tak se podíváme, co je jim z trénovacích dat nejpodobnější, a podle toho vrátíme výsledek
- neučíme se žádné parametry, ukládáme přímo trénovací data (tzv. lazy learning, líné učení, zajímavé věci se dějí až při inferenci, nikoliv při trénování)
- máme hyperparametry
	- $k$ … počet sousedů, které používáme k predikci
	- metrika … jak poznáme, co je nejbližší soused?
		- typicky se používají $L^p$ normy
		- kde $||x||_p=\sqrt[p]{\sum_i|x_i|^p}$
	- váhy
		- uniformní … všech $k$ nebližších sousedů má stejnou váhu
		- inverzní … váha je nepřímo úměrná vzdálenosti
		- softmax
- nemusí být jednoduché sousedy najít
	- používají se stromové datové struktury
- tak jako v domácím úkolu už se to spíš nepoužívá
- typičtější aplikace
	- doporučování videí
	- anonymní rozpoznávání obličejů např. v Google Fotkách

## Bayesovská pravděpodobnost

- v bayesovské interpretaci je pravděpodobnost kvantifikace nejistoty
- prior probability → posterior probability
	- na základě nových dat
- pozor: pokud je apriorní pravděpodobnost hodně malá, i klasifikátor s vysokými precision a recall může mít vysoké množství false positives
- MAP odhad
	- u normálního rozdělení vlastně minimalizujeme L2 regularizovaný NLL
- konjugované distribuce (conjugate distribution)
	- prior a posterior mají stejný „typ distribuce“
- credibility intervals máme „zadarmo“
- jak zvolit priors?
	- uninformative priors
	- snažíme se volit prior distributions tak, aby tam bylo co nejmíň předpokladů (využíváme princip maximální entropie)
	- chceme využívat konjugované distribuce, aby to šlo upočítat
	- asi se vybírají empiricky tak, aby to hezky vyšlo :D
- naivní bayesovský klasifikátor

## Korelace

- kovariance
	- střední hodnota je lineární vzhledem k součtu
	- čemu se rovná rozptyl součtu?
- korelace
- Pearsonův kolerační koeficient
	- „jsou data lineárně závislá?“
- Spearmanův koeficient pořadové korelace
	- „je zachováno pořadí?“
- Kendallův koeficient pořadové korelace $\tau$
	- „poměr souhlasných párů“
- „jak často se stane, že mezi 5 nejlepšími jsou ty, které chceme?“
	- precision pro fixních top 5
- mean reciprocal rank
- shoda anotátorů
	- Cohenovo $\kappa$
- výkon ML klasifikátoru
	- měl by být lepší než pár ifů – kdyby ne, děláme něco špatně
		- jako baseline se typicky nastavuje četnost největší třídy
	- asi nebude lepší než shoda anotátorů – kdyby byl, asi overfitujeme

## Ensembling

- $y_i(x)=t+\varepsilon_i(x)$
	- $y_i$ … prediction
	- $t$ … target
	- $\varepsilon_i(x)$ … chyba modelu
- $\mathbb E[(y_i(x)-t)^2]=\mathbb E[\varepsilon_i^2(x)]$
- bagging – bootstrap aggregation
	- modely trénuju na různých datech
	- u některých modelů zakážu nějaké features
- knowledge distillation / model compression
	- natrénujeme model „student“ pomocí učitelského modelu/modelů
	- snažíme se natrénovat model s co nejmenší cross-entropy vůči původnímu modelu
	- cíl – zmenšit model (abychom nemuseli používat celý ensemble nebo velký model)

## Decision trees

…

## SVD, PCA, K-Means

- dekompozice matice
- líbila by se nám taková, kde budou řádky a sloupečky ortogonální (statisticky nezávislé)
- vlastní čísla, vlastní vektory
- možné použití
	- ztrátová komprese obrázku
	- doporučovací systémy
- PCA
- power iteration
- k-means
	- citlivý na inicializaci
	- můžeme inicializovat víckrát a vybrat si ten s nejnižší chybou
- může se hodit clustery modelovat jako gaussiány
	- zvlášť pokud nemají stejnou velikost a jsou třeba elipsy
- k-means i outliery přiřadí do nějakého clusteru

## Testování statistických hypotéz

…

## Zkouška

- písemná
- když se nám nějaká otázka nebude zdát, na Piazze bude formulář, kam to můžeme napsat
- v lednu na přednášce/cvičení se podíváme na nejvíc problematické otázky

## Etika

- věda o tom, co je dobře/špatně
- hlavní teoretické rámce
	- deontologická etika – máme nějaká pravidla/principy, těch se držíme
	- konsekvencialistická etika / utilitarismus – dobré chování maximalizuje dobré následky (ale může být problém měřit, co jsou dobré následky)
	- etika ctností (virtue) – člověk je dobrý, pokud dělá dobře věci, ke kterým je určený; rozhodnutí je dobré (akce je dobrá), pokud by se takhle rozhodnul ctnostný člověk
	- kontraktová etika – ze společenské smlouvy (implicitní nebo explicitní) vyplývá, co je dobré
	- etika péče – rodíme se jako bezbranní, proto má vůči nám společnost nějakou odpovědnost a naopak my máme odpovědnost vůči společnosti; etika péče stojí na vztazích a odpovědnosti, která z nich vyplývá
- obvykle uvažujeme deontologickou a konsekvencialistickou etiku
- deontologická etika
	- zaměřuje se na povahu akcí spíš než na jejich důsledky
	- řídíme se definovanými pravidly a principy (např. Všeobecná deklarace lidských práv, Desatero přikázání, Kantův kategorický imperativ)
	- zásady v AI
		- vlídnost
		- neškodolibost
		- soukromí
		- nediskriminace
		- autonomie
		- informovaný souhlas
	- výhody: jasná pravidla, stabilita, respekt práv
	- nevýhody: rigidita, možný konflikt dvou pravidel, zanedbání důsledků
	- kritika: když jsi zlý, vždycky můžeš tvrdit, že vycházíš z dobrých principů, nehledě na důsledky
- utilitariánská etika
	- maximalizujeme celkové štěstí / well-being, minimalizujeme újmu
	- zaměřuje se na důsledky akcí
	- dobrá rozhodnutí = rozhodnutí, která maximalizují celkový dopad
	- výhody: flexibilita, kvantifikovatelnost
	- nevýhody: hrozí, že budeme ignorovat práva jednotlivců, je těžké definovat účelovou funkci
- někdy se vyplatí mezi frameworky přepínat – např. při hromadném neštěstí přejdeme z deontologické etiky na utilitarismus
- články o etice v ML se často zaměřují na negativní důsledky pro znevýhodněné lidi
- utilitarismus je problematický, když uvažujeme události s malou pravděpodobností a extrémní hodnotou užitku („je malá šance, že nás AI vyhubí, ale užitek by byl $-\infty$“)
- příklady, jak dělat etické systémy
	- deontologická etika
		- nepoužívat etnickou příslušnost jako feature
		- budovat důvěru
		- trvat na soukromí, férovosti a spravedlnosti
	- utilitariánství
		- na koho to bude mít dopad
		- jaká újma může nastat?
		- jak předejít újmě?
- problémy v různých fázích vývoje modelu strojového učení
	- definice problému
		- rozpoznávání Ujgurů od Číňanů – problém samotný není etický
		- automatické hodnocení esejí – studenti mají právo vědět, proč dostali špatné hodnocení
		- predikce recidivismu – porušuje právo na spravedlivý proces, je nedostatečně transparentní
	- shromažďování dat
		- reprezentační bias – data nejsou reprezentativní, chybí tam menšiny apod.
			- rozpoznávání obličejů
		- data z internetu nepopisují svět takový, jaký je
		- historický bias – nerovnosti z minulosti jsou v datasetech zachovány
		- problémy s autorským právem – u generativních modelů
		- problematické způsoby kolekce dat
			- crowdsourcing
				- lidé jsou najati, aby dělali práci, kterou má dělat model
				- špatně placená monotónní práce, může způsobovat psychologickou újmu (typicky v případě posuzování obrázků ze sociálních sítí)
				- gig economy – přivýdělek se stane hlavním úvazkem bez pracovněprávní ochrany
			- sběr uživatelských dat
				- trénovací data jsou sbírána od uživatelů, kteří nemají jinou možnost než data poskytovat, aby mohli službu používat
				- netransparentní transakce – uživatel získá službu, platí daty, není jasné, jakou hodnotu data mají
	- vývoj modelu
		- diskretizace výstupů zesiluje bias – pokud se rozhodujeme mezi dvěma možnostmi a jedna je pravděpodobnější, vždycky použijeme tu pravděpodobnější
		- větší modely snadno overfittujou, dají se z nich vytáhnout soukromé údaje, které byly obsaženy v trénovacích datech
		- destilace modelů také zesiluje biasy
		- modely se můžou naučit smazané features (etnická příslušnost, gender, …) z jiných features (jméno, škola, …)
	- vyhodnocení modelu
		- metriky neobsahují všechno, co bychom potřebovali (třeba gender bias)
		- v HR nás zajímá jenom accuracy – může se stát, že model systematicky znevýhodňuje nějaké uchazeče
		- používáme proxy metriky, abychom optimalizovali něco jiného
			- musíme metriky vhodně zvolit
			- čas sledování videa nemusí být dobrou metrikou pro jeho kvalitu – favorizuje videa s extrémními názory
	- použití modelu v praxi
		- nesoulad mezi trénovacími/testovacími daty a reálným prostředím
			- jazyk minorit je častěji klasifikován jako hate speech / NSFW
		- feedback loops (zpětnovazebné smyčky)
			- predikce ovlivňují chování uživatelů, to se pak používá jako zdroj trénovacích dat
			- způsobuje to echo chambers na sociálních sítích

## Co jsme se naučili

- základy statistiky
- základy teorie informace
	- preferujeme modely s větší entropií – nechceme do nich vnášet dodatečné předpoklady
- optimalizace – nulová derivace, Lagrangeovy multiplikátory, SGD, metody druhého řádu
- práce s daty – anotace, features, normalizace
- tréninik a evaluace – splitování dat, overfitting a regularizace, metriky
- geometrická intuice
- pravděpodobnostní intuice
- rozhodovací stromy
