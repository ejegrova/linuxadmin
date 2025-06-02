# Práce se soubory a adresáři

Teď, když umíš zkoumat soubory a adresáře, je můžeš začít vytvářet.


## Co už máme?

Nejdřív se vrať do adresáře `data-shell` a pomocí `ls -F` se koukni,
co v něm Nela už má:

```console
$ cd ~/Dokumenty/data-shell
$ pwd
/home/nela/Desktop/data-shell
$ ls -F
creatures/  data/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg  solar.pdf  writing/
```


## Vytvoření adresáře

Nela se rozhodla začít psát text své práce.

Vytvoř nový adresář zvaný `clanek`.
Použij k tomu příkaz `mkdir` (který nic nevypisuje):

```console
$ mkdir clanek
```

Příkaz `mkdir` (z angl. *make directory*, vytvoř adresář) vytvoří adresář
daného jména – nebo přesněji řečeno, na dané cestě.
Protože je `clanek` relativní cesta (ač dosud neexistovala),
nový adresář se vytvoří v aktuálním adresáři:

```console
$ ls -F
creatures/  data/ clanek/  molecules/  north-pacific-gyre/  notes.txt  pizza.cfg  solar.pdf  writing/
```

A zatím v něm nic není:

```console
$ ls -F clanek
```

Kdyby ses pokusila vytvořit několik vnořených adresářů najednou,
nebude to fungovat:

```console
$ mkdir clanek/kapitola-1/sekce-1/podsekce-1
mkdir: adresář „clanek/kapitola-1/sekce-1/podsekce-1“ nelze vytvořit: Adresář nebo soubor neexistuje
```

Chybová hláška tu je trošku zavádějící: `mkdir` si ve skutečnosti stěžuje
na to, že neexistuje `clanek/kapitola-1/sekce-1`, kde by se měl vytvořit
adresář `podsekce-1`.

V tomto případě můžeš buď vytvořit jednotlivé adresáře postupně, nebo použít
přepínač `-p` (z angl. *parents*), který vytvoří i všechny potřebné nadřazené
(„rodičovské“) adresáře:

```console
$ mkdir -p clanek/kapitola-1/sekce-1/podsekce-1
```

Příkaz `mkdir` nic nevypsal.
Nevypsal ani chybovou hlášku, což u většiny příkazů znamená, že všechno proběhlo
v pořádku.

Jak si to ověřit?
Příkaz `ls` má přepínač `-R`, který vypíše obsah *všech* adresářů, na které
narazí, a to **R**ekurzivně – když v podadresáři najde další podadresář,
„zanoří“ se i do něj.

```console
$ ls -FR clanek
kapitola-1/

clanek/kapitola-1:
sekce-1/

clanek/kapitola-1/sekce-1:
podsekce-1/

clanek/kapitola-1/sekce-1/podsekce-1:
```

Případně použij příkaz `tree`, který adresářovou strukturu vypíše
„skoro graficky“:

```console
$ tree clanek
clanek
└── kapitola-1
    └── sekce-1
        └── posdekce-1

3 directories, 0 files
```

Pokud dostáváš hlášku „Command 'tree' not found“, je třeba si `tree` prvně nainstalovat.
Na distribucích založených na Debianu (např. Ubuntu) to můžeš udělat následujícím způsobem:

```console
sudo apt update
sudo apt install tree
```

Na distribucích založených na Red Hat (např. Fedora) použij:

```console
sudo dnf install tree
```

> [note]
> Tyhle materiály byly zrevidovány na jaře 2025. V tomto období výstup příkazu
> `tree` nebyl přeložený – narozdíl od hlášek z příkazů projektu GNU, jako
> jsou `ls` nebo `mkdir`.
> Zřejmě se ještě nenašel dobrovolník, který by `tree` přeložil do češtiny, nebo
> dokonce nikdo ani nepřidal podporu pro neanglické jazyky.
> Čím méně používané příkazy budeš zkoušet, tím častěji na angličtinu narazíš.


## Pojmenovávání souborů a adresářů

Teď, když víš, jak vytvářet adresáře, se pojďme zaměřit na to,
jak je pojmenovávat.
Konkrétně jak je pojmenovávat tak, aby práce s nimi byla „v řádce“
co nejjednodušší.

1. Nepoužívej mezery.

   Mezerami se v příkazech oddělují jednotlivá „slova“; jméno souboru
   s mezerou by Bash interpretoval jako dva různé argumenty.
   Místo mezery použij pomlčku nebo podtržítko, jako u `data-shell/`
   nebo `north-pacific-gyre/`.

2. Nezačínej pomlčkou (`-`).

   Většina příkazů považuje vše, co začíná na pomlčku, za přepínače.
   Kdybys chtěla pomocí `ls -FR` vypsat soubor se jménem `-FR`,
   narazila bys na problém.

   Kdybys ale soubor jménem `-FR` měla, můžeš použít cestu, která
   pomlčkou nezačíná.
   Třeba `ls ./-FR`.
   Rozklíčuješ, proč to funguje?

3. Ideálně používej jen anglická písmenka, číslice, `.` (tečku), `-` (pomlčku)
   a `_` (podtržítko).

   Bash používá spoustu speciálních znaků, které znamenají něco jiného než
   „část jména“: už znáš `~` (vlnovku) nebo `/` (lomítko), v této lekci objevíš
   `*` a `?`, a to zdaleka není vše.

4. Vyhni se diakritice.

   Písmena s diakritikou představují jiný problém: nejde je napsat na všech
   klávesnicích.
   Když soubor nasdílíš zahraničnímu kolegovi, bude pro něj mnohem
   jednodušší se zorientovat v souborech pojmenovaných „cesky“ (tj. bez
   diakritiky), kterým jen nerozumí, než aby ještě musel hledat jak napsat `č`.
   (Nehledě na to, že rozlišit `i` od `í` s čárkou občas není jednoduché
   ani pro česky mluvící.)

4. Drž se malých písmen.

   Linux nerozlišuje mezi velkými a malými písmeny, takže `clanek` a
   `Clanek` jsou jména dvou úplně odlišných adresářů.
   Když ale tyhle adresáře např. nasdílíš na počítač s MS Windows
   (nebo na souborový systém podporující Windows, což je i většina
   *flash* disků), vznikne chaos.

   Proto je nejlepší všude používat jen malá písmena.

5. Tečku používej na oddělení přípony.

   Přípona `.txt`, `.mp3`, `.png`, `.pdf` říká *lidem*, co v souboru očekávat:
   text, hudbu, obrázek, resp. dokument.
   Pro počítač neznamená přípona nic zvláštního: když programy pro Linux
   potřebují zjistit, co je to za soubor
   (a jestli ho např. otevřít v obrázkovém editoru nebo přehrát jako zvuk),
   „dívají“ se spíš do samotného souboru než na příponu.
   A přejmenováním `velryba.jpg` na `velryba.mp3` neuděláš z fotky velryby
   nahrávku :)

   Ale ačkoliv počítač přípony ignoruje, pro lidi jsou důležité.

   Mimo oddělení přípony můžeš tečku použít na skrytí souboru
   (např. `.gitignore`), kdybys to někdy potřebovala.

Kdybys musela pracovat se jmény, které tyhle rady nedodržují,
máš dvě možnosti:

* Celé jméno uzavři do jednoduchých uvozovek, `'`.
  To funguje vždy, jen tak nejde napsat samotná jednoduchá uvozovka.
* Celé jméno uzavři do dvojitých uvozovek, `"`.
  Na rozdíl od Pythonu je mezi `'` a `"` rozdíl: ve dvojitých uvozovkách
  mají některé znaky (`$`, <code>`</code> a `!`) stále speciální funkci.
  Je jich ale málo.
* Před speciální znaky dej zpětné lomítko, `\`, které funguje podobně jako
  v Pythonu.
  Zpětná lomítka používá Bash při doplňování pomocí <kbd>Tab</kbd>.

Autor tohoto textu má mezery ve jménech skladeb – autoři hudby většinou
na příkazovou řádku nemyslí a přejmenovávání je otrava.
Tak používám příkazy jako:

```console
$ mplayer "disc 1/11 - On to Grasstown.mp3"
$ mplayer disc\ 1/11\ -\ On\ to\ Grasstown.mp3
```

(Což ti teď nebude fungovat, pokud náhodou nemáš nainstalovaný tenhle
přehrávač a uloženou tuhle hudbu.)


## Vytváření souborů

Přepni se do adresáře `clanek` a vytvoř soubor `osnova.txt` pomocí příkazu
`touch`:

```console
$ cd clanek
$ touch osnova.txt
```

> [note] Různé způsoby práce se soubory
> Vytvářet adresáře a soubory samozřejmě můžeš i z grafického „klikátka“.
> Příkazy v terminálu a grafické programy jsou různé způsoby, jak se soubory
> pracovat, ale samotné soubory jsou vždy stejné.
>
> Ze začátku je práce v příkazové řádce složitější, ale jakmile si zvykneš,
> změní se to.

## Přesouvání souborů a adresářů

Vrať se do adresáře `data-shell`.

```console
cd ~/Dokumenty/data-shell
```

V adresáři `clanek` je teď soubor `osnova.txt`, ve kterém je spíš plán práce
než osnova článku.
Pojď soubor přejmenovat.

*Přejmenování* souboru je to stejné co *přesunutí*: v obou případech se změní
cesta k souboru. Počítači je celkem jedno, jestli se změní adresář nebo
jen poslední část cesty - jméno.
Pro obě operace se používá příkaz `mv` (z angl. *move*, přesuň), který
potřebuje dva argumenty, „odkud“ a „kam“:

```console
$ mv clanek/osnova.txt clanek/plan.txt
```

První argument říká, který existující soubor se má přesunout; druhý je cesta,
kde se soubor bude nacházet po přesunutí.

```console
$ ls clanek/
kapitola-1/  plan.txt
```

> [warning]
> Pozor na to, že pokud poslední argument („kam“) je existující soubor,
> `mv` ho *přepíše*.
> Nemáš-li zálohy, není žádná jednoduchá možnost, jak takový přepsaný soubor
> vrátit zpět.

Jestli se o své soubory bojíš, používej `mv -i` (nebo `mv --interactive`):
přepínač `-i` zajistí, že `mv` před přepsáním souboru poprosí o potvrzení.

> [note]
> Důležité systémy mají často `-i` nastaveno jako výchozí chování,
> ale není radno na to spoléhat :)

Příkaz `mv` umí přesouvat i celé adresáře.

### Přesouvání do adresáře

Teď ale pojď přesunout `plan.txt` do *aktuálního* adresáře.
Opět použiješ `mv`, ale místo celého cílového jména („kam“) zadáš jen jméno
adresáře, kam chceš soubor přesunout.
Adresář `mv` nepřepíše, místo toho soubor uloží dovnitř, pod původním jménem.

Jméno aktuálního adresáře je `.`, to tedy použij jako druhý argument:

```console
mv clanek/plan.txt .
```

> [note]
> U některých příkazů můžeš vynechat argument a vyvolat tím nějaké výchozí
> chování:
> * Příkaz `ls` dělá to samé co `ls .`
> * Příkaz `cd` dělá to samé co `cd ~`
>
> Příkaz `mv` ale podobnou zkratku nemá: argumenty „odkud“ a „kam“ vynechat
> nesmíš.

Pomocí dvou `ls` zkontroluj, že soubor z adresáře `clanek` zmizel, ale objevil
se v aktuálním adresáři, `data-shell`:

```console
$ ls clanek
kapitola-1/
$ ls
creatures  molecules           solar.pdf  writing
data       north-pacific-gyre  pizza.cfg
clanek   notes.txt           plan.txt
```

V aktuálním adresáři teď máš spoustu balastu.
Pomocí `ls` si můžeš místo celého adresáře vypsat i jen jediný soubor:

```console
$ ls plan.txt
plan.txt
```

To se hodí na zjištění, jestli takový soubor existuje. Pokud ano, v terminálu se ti 
vypíše jeho obsah. Pokud ne, terminál tě upozorní chybovou hláškou *Adresář nebo soubor neexistuje*.


### Přesouvání více souborů

Příkaz `mv` umí přesunout i více souborů najednou.
Když mu předáš víc než dva argumenty, všechny kromě posledního označují
soubory k přesunutí („odkud”) a poslední argument označuje cílový adresář, kam se všechny přesunou
(„kam“).

Řekněme že soubor `plan.txt` patří přece jen ke článku.
A stejně tak tam patří i `notes.txt`.
Přesuň je na správné místo pomocí:

```console
$ mv plan.txt notes.txt clanek/
$ ls clanek/
notes.txt  plan.txt
```

Abys zkontrolovala, že na původním místě už soubory nejsou,
můžeš dát příkazu `ls` více argumentů najednou.
Vypíšou se všechny – funguje to podobně jako kdybys `ls` použila pro
každý z nich zvlášť:

```console
$ ls plan.txt
ls: nelze přistoupit k 'plan.txt': Adresář nebo soubor neexistuje
$ ls notes.txt
ls: nelze přistoupit k 'notes.txt': Adresář nebo soubor neexistuje
$ ls plan.txt notes.txt
ls: nelze přistoupit k 'plan.txt': Adresář nebo soubor neexistuje
ls: nelze přistoupit k 'notes.txt': Adresář nebo soubor neexistuje
```


## Kopírování souborů

Příkaz `cp` funguje velice podobně jako `mv`, jen soubory kopíruje místo
přesouvání.

Řekněme že soubor `plan.txt` patří ve skutečnosti na obě místa,
`data-shell/` i `data-shell/clanek/`.
Aktuálně je jen v `clanek/`, ale můžeš ho zkopírovat i do aktuálního adresáře:

```console
$ cp clanek/plan.txt plan.txt
```

Výsledek zkontroluj pomocí `ls`:

```console
$ ls clanek/plan.txt plan.txt
clanek/plan.txt  plan.txt
```

Pomocí příkazu `cp` kopíruješ pouze jednotlivé soubory, ne celé adresáře. Pokud chceš 
kopírovat i celé adresáře včetně jejich podadresářů apod., potřebuješ k tomu přepínač 
`-r` (`--recursive`).

```console
$ cp -r clanek clanek_archiv
$ ls clanek clanek_archiv
clanek:
kap1  notes.txt  plan.txt

clanek_archiv:
kap1  notes.txt  plan.txt
```

> [note]
> Příkaz `mv` takový přepínač nemá - funguje rekurzivně automaticky. Přesunou se ti tedy
> nejen jednotlivé soubory, ale celé adresáře i s jejich zanořeným obsahem.


## Odstraňování souborů a adresářů

Mít dvě kopie souboru `plan.txt` nakonec nebude to nejlepší rozhodnutí
(když jednu změníš, která bude platit?).
Jednu z nich smaž pomocí příkazu `rm` (z angl. *remove* – odeber).

```console
$ rm plan.txt
$ ls plan.txt
ls: nelze přistoupit k 'plan.txt': Adresář nebo soubor neexistuje
```

> [warning] Mazání je nevratné
> Grafické prohlížeče souborů – a to i ty Linuxové – většinou mají „odpadkový
> koš“, kam se „házejí“ smazané soubory, aby se daly zase obnovit.
> Bash takový koš nemá.
> Když soubor smažeš, odstraní se ze souborového systému a místo, které
> zabíral, systém po chvíli přepíše jiným souborem.
>
> Existují nástroje, které s trochou štěstí umí smazané soubory obnovit,
> ale není to zaručeno.
>
> Kdybys někdy smazala důležitý soubor, co nejdřív vypni počítač,
> aby systém neměl čas nic přepsat, a vyhledej pomoc.
> (V extrémním případě počítač „natvrdo“ vypoj ze zásuvky/odstraň baterii,
> stejně jako kdybys ho polila vodou.)
>
> Používej zálohy, které můžeš obnovit, kdyby se něco stalo.
> Existují na to různé nástroje, ale dobře poslouží např. Gitový repozitář,
> který pravidelně `push`-uješ na vzdálený server.


Když zkusíš smazat adresář, `rm` se vztekne:

```console
$ rm clanek
rm: nelze odstranit 'clanek': je adresářem
```

Kdybys opravdu chtěla smazat celý adresář a všechen jeho obsah,
použij přepínač `-r` (`--recursive`).
Doporučuji ho vždy zkombinovat s `-i` (`--interactive`), kdy `rm` u každého
souboru poprosí o potvrzení,
případně s `-v` (`--verbose`), kdy `rm` vypíše, co dělá.

```console
$ rm -rv clanek
adresář 'clanek/kap1/sekce1/posdekce1' smazán
adresář 'clanek/kap1/sekce1' smazán
adresář 'clanek/kap1' smazán
smazáno 'clanek/notes.txt'
smazáno 'clanek/plan.txt'
adresář 'clanek' smazán
```

Ještě že máš zálohu! Zkus ji obnovit.

> [note]
> Co dělá příkaz `rm -rf /`?
> Přepínač `-r` smaže rekurzivně všechno; `/` je adresář,
> který obsahuje úplně všechny soubory v celém systému.
> A `-f` (`--force`) potlačí nastavení systémů,
> které mají `-i` jako výchozí chování.
>
> Tenhle příkaz je jeden z nejjednodušších způsobů, jak zničit celý
> nainstalovaný systém.
> Má jen 8 písmen!
> Byl tak oblíbený u lumpů, kteří ho na internetu doporučovali nováčkům,
> že dnešní verze příkazu `rm` mazání `/` nepovolí bez zvláštního,
> dlouhého přepínače.
>
> Nezadávej příkazy, které najdeš na internetu, aniž bys věděla, co dělají!
> (Pokud tedy nepracuješ ve virtuálním počítači, kde nemáš důležitá data.)


## Práce s více soubory a adresáři

Často budeš potřebovat kopírovat či přesunovat víc souborů najednou.
Pak můžeš všechny potřebné soubory pojmenovat a nebo jich vybrat několik
pomocí *zástupných znaků* (angl. *wildcard*: divoká karta, žolík)


### Opakování: Kopírování s více cestami

Přepni se do adresáře `data-shell/data`.
Co udělá příkaz níže?

```console
$ mkdir zaloha
$ cp amino-acids.txt animals.txt zaloha/
```

{% filter solution %}
Zkopíruje soubory `amino-acids.txt` a `animals.txt`, tj. všechny argumenty
kromě posledního, do adresáře `zaloha`.
Vytvoří tedy soubory `zaloha/amino-acids.txt` a `zaloha/animals.txt`.
{% endfilter %}

Co udělá příkaz níže?

```console
$ ls -F
amino-acids.txt  animals.txt  elements/  morse.txt  pdb/  planets.txt  salmon.txt  sunspot.txt  zaloha/
$ cp amino-acids.txt animals.txt morse.txt
```

{% filter solution %}
Zkopíroval by první dva soubory (`amino-acids.txt` a `animals.txt`)
do adresáře `morse.txt/`.
Jenže `morse.txt` není adresářem, takže příkaz selže.
Do souboru nelze dát další soubory.

```console
$ cp amino-acids.txt animals.txt morse.txt
cp: cíl 'morse.txt' není adresářem
```
{% endfilter %}


### Vybírání více souborů pomocí zástupných znaků

Hvězdička, `*`, je v Bashi *žolík* neboli *zástupný znak*, který odpovídá
libovolnému počtu (0 nebo víc) znaků.
Budeš-li v adresáři `data-shell/molecules`, pak „šablona“ `*.pdb` odpovídá
souborům `ethane.pdb`, `propane.pdb` a všem ostatním, které končí na `.pdb`.
Ale `p*.pdb` odpovídá jen `pentane.pdb` a `propane.pdb` – těm, které zároveň
začínají písmenem `p`:

```console
$ cd ~/Dokumenty/data-shell/molecules
$ ls *.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
$ ls p*.pdb
pentane.pdb  propane.pdb
```

Další zástupný znak je otazník, `?`, který odpovídá jen jednomu znaku.
Takže šablona  `?ethane.pdb` odpovídá jen jménu `methane.pdb` – na rozdíl od
`*ethane.pdb`, čemuž odpovídá jak `methane.pdb`, tak i `ethane.pdb`.

```console
$ ls ?ethane.pdb
methane.pdb
$ ls *ethane.pdb
ethane.pdb  methane.pdb
```

Zástupných znaků můžeš použít víc: `???ane.pdb` odpovídá třem znakům
následovaným `ane.pdb`, tedy `cubane.pdb ethane.pdb octane.pdb`.

Když Bash zástupné znaky zpracovává, vytvoří seznam odpovídajících souborů
ještě předtím, než spustí příslušný příkaz.
Když neodpovídá *žádný* soubor, pošle příkazu argument tak, jak je:

```console
$ ls *.pdf
ls: nelze přistoupit k '*.pdf': Adresář nebo soubor neexistuje
```

Když ale nějaké názvy odpovídají, dostane příkaz tyto příkazy jako jednotlivé
argumenty.
Zpracovává je tedy Bash; samotný příkaz jako `ls` nebo `cp` nemá
k původní šabloně přístup.
