# Programování v C\#

- zkouška bude podobná jako u principů
- principy Pythonu
	- přiřazení do proměnné vytvoří objekt na garbage-collectované haldě s daty, jejich délkou a overheadem (obsahuje ref. count a datový typ)
	- odkaz (reference) na tento objekt se uloží do lokální paměti na místo vyhrazené dané proměnné
	- při provádění operací pomocí přetížených operátorů se kontrolují datové typy proměnných (uvnitř objektů na haldě) a podle toho se provede vhodná operace
- v C/C++
	- ukládá se rovnou hodnota, nevytváří se žádný objekt ani reference – proměnné se vytvářejí rovnou na místě (v lokální paměti)
	- objekty se taky ukládají do lokální paměti
	- pointery se chovají dost podobně – obsahují adresu proměnné
	- halda
		- na haldě se objekty alokují pomocí klíčového slova `new`
		- alokátor si udržuje overhead
		- dealokace se provádí explicitně pomocí `delete`
	- rozdíl mezi třídou a strukturou je ten, že obsah struktury je defaultně public
	- ochranu přístupu (public/private) kontroluje překladač, jinak se nikam neukládá
- C#
	- .NET
		- běhové prostředí (runtime), mj. alokátor proměti
		- standardní knihovny
	- v dotnetu může (kromě C#) běžet víc jazyků – Visual Basic .NET, F#, …
	- jsou věci, které platí pro C#, a věci, které platí pro .NET

## Typy

- základní dělení všech typů
	- pointery – jsou ošklivé, nebudeme se o nich bavit
	- hodnotové typy – alokované na místě (s výjimkami)
		- enums
		- structures
			- simple types (Int32, Int64, Double, Boolean, Char, …)
			- nullables
			- user defined structures (struct)
	- referenční typy – alokované na spravované (managed) haldě
		- classes (e.g. strings)
		- interfaces
		- arrays
		- delegates
