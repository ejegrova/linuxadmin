> [warning]
> Toto jsou *zhuštěné poznámky z prvního běhu*, nikoli materiály k samostudiu.

# Linuxová administrace - 1. sraz
Kurz není vlastně čistě o bashi, ale víc o administraci linuxu
Bash bude v prvních dvou hodinách

část o bashi je o projití:
http://swcarpentry.github.io/shell-novice/
TODO: udělat tahák, přeložit do CZ, vymyslet příklady 

## Shell
Co je to shell?
shell je program na spouštění programů
bash je varianta shellu

(příklad)
```
echo $0
/bin/bash
```

Proč používat příkazovou řádku:
* copy & paste, “pomož mi” na fórech
* automatizace, šup s tím do souboru, udělej tohle 1000x s drobnými změnami

## Prompt

`[jmeno@nazevpocitace ~]$`
* už. jméno
* jméno počítače
* ~ 
* za $ se píší příkazy

Zkusit neexistující příkaz, třeba
`ks`
Co se stane?

*V okénkovém prostředí*
funkce programu je k dispozici někde  v menu, tlačítka atd.
*V terminálu*
musím si pamatovat název programu, ale mám jich k dispozici víc

### Úkol:
máme k dispozici data o tom, kde je v moři je kolik např. plastového bince a můžeme ta data zpracovat
1. klikáním, ale to trvá 20s per řádek
1. my si to ale zautomatizujeme (jupí!)

`/`
tzv. root (kořenový) adresář
- obsahuje systémové složky a soubory
- obsahuje složku /home, která obsahuje složky uživatelů počítače
- strom adresářů je oddělován jednoduchým lomítkem 

`/home/uzivatel/`
- první lomítko (viz výše) je také název adresáře
- tzv. domovský adresář
- zde si uživatel ukládá vlastní soubory a složky
- `~` je zkratka pro domovský adresář

Napsáním “ls” spustí program, co se jmenuje **ls**.
`ls -F`

(mezi `s` a `-` je mezera)
**přepínače** (option) začínají pomlčkou, nějak modifikují základní chování programu
**argumenty** - typicky jména souborů, se kterými má pracovat, taky oddělováno mezerou

`ls -F /`

pamatuješ si, co dělá `-F`? Já ne. Každý příkaz má vestavěný přepínač `--help` s offline nápovědou.

Krátká a dlouhá varianta přepínačů (krátká -, dlouhá --). Krátká je s písmenkem, dlouhá typicky s celoslovním názvem (`-h` vs `--help`).
Při psaní skriptů je fajn používat dlouhou variantu, protože se to pak bude lépe číst. 

výstup `--help` je součást programu `ls`.

jiný zdroj nápovědy:
`man ls`
Ovládání: pgdown/pgup, q - vypnout zobrazovač menu
Jsou to takzvané manuálové stránky, zpravidla delší nápověda, vyčerpávající - zabírá hodně místa, a proto lehčí operační systémy ji občas nemají :). 

co udělá `ls`, když přepínač nezná? Odkáže tě na `--help`

cvičení: co dělá?
`ls -h -l`
adresáře mají téměř vždy 4kB

sdružení přepínačů: `ls -lhF`
neplatná kombinace je `--jeden--dlouhy`


`cd` (bez argumentu) - přesun do domovského adresáře
`cd ~` je přesun do adresáře “~”, což je jen odkaz na domovského adresáře


```
ls data-shell
ls data-shell/data
```

automatické doplnění názvu souboru - stačí jen první písmenko
1x tabulator - doplnění nejdelšího prefixu
2x tabulator - zobrazení dalších názvů stejného prefixu
Když vím, co chci napsat, tabem si hodně urychlím práci. 


Cesty je možno spojovat. 
`cd data-shell/data/../data/../..`
^-- cesta, popis, kam v tom adr. stromu chci dojít, což je ekvivalentní s
```
cd data-shell
cd data
cd ..
cd data
cd ..
cd ..
```

Název aktuálního adresář je součástí promptu.

**Tipy:**
* `cd -` tě přesune do posledního navštíveného adresáře
* **vkládání prostředním tl. myši** - vybrat myší text (samo se to zkopíruje), prostředním tl. se to vkládá, funguje všude, i mezi term. a graf. programy. Klasická schránka Ctrl+C/V je samostatná věc, takže je možné mít k dispozici hned dvě různé věci k dispozici
* **Copy & paste** v terminálu se dělá pomocí Ctrl+Shift+C/V, protože ještě než vznikly grafické programy, tak Ctrl+C mělo jiný význam (což stále platí)


## Operace kopie, přesun, přejmenování, mazání

Přesuň se do složky `data-shell/creatures`

**basilisk.dat** - “.dat” je součástí názvu souboru, systému je úplně ukradená, je to vodítko pro lidi. Linux se typicky podívá do samotného souboru a podle toho odhadne jakým programem to má otevřít. Přípona je důležitá pro Windows, který podle ní zjistí, jakým programem soubor otevřít. 


`ls -R`
složky začínají tečkou, příkaz nám rekurzivně zobrazí všechny adresáře a co mají v sobě

`.` - aktuální adresář
`..` - předchozí adresář

### tree
Hezky zobrazí strukturu našich adresářů.

Když potřebuješ dát datum do názvu, tak ve formátu YYYY-MM-DD
povolené znaky: _, -, tečka, mezeru raději ne (protože se používá jako oddělovač argumentů)

### skryté soubory
* začínají tečkou, `ls` je samo o sobě se je nezobrazuje
* `ls --all`
* `..` je speciální složka

### Nový adresář
V `data-shell` uděláme novou složku:
```
mkdir thesis
```
Po zmáčknutí Enter to nic neřekne. Když program uspěje, tak je zticha. Chybu samozřejmě zobrazí.

### Vytvoření prázdného souboru
```
cd thesis
vim draft.txt
```
Ten poslední rádek vytvoří nový soubor, otevře stávající, když už existuje.

Stisk `Ctrl` je zkrácený na znak `^` (existuje dalších 6 zápisů, jak vyjádřit stisk `Ctrl` a dalšího písmenka)

Jiný způsob, jak vytvořit soubory (původně pro nastavení data změny souboru, vytvoření nového souboru je vedlejší efekt, ale přitom se to časem stalo nejběžněším use-case):
```
touch soubor.dat
```

### Přesouváme, přejmenováváme
soubor `draft.txt` chceme přejmenovat. Pro větší efekt si to ale zkusíme z jiné složky.

```
cd ..
```


přejmenování souboru je vlastně přesun
```
mv thesis/draft.txt thesis/basnicka.txt
```

výpis obsahu souboru - `cat` (pochází z *concatenate*, původně pro spojování souborů, ale časem se to nejvíc používá pro výpis právě jednoho souboru)
```
cat basnicka.txt basnicka.txt basnicka.txt
```

```
cp thesis/basnicka.txt thesis/basen.txt
```

```
ls soubor1 soubor2 soubor3
```

v _data-shell_ udělat adresář “poznamky”

přesun více souborů najednou:
```
mv thesis/draft.txt thesis/basnicka.txt poznamky
```

Posledním argumentem je cíl, kam se mají všechny předchozí přesunout - pouze pokud má `mv` více než 2 argumenty.
### Kopírujeme
```
cp poznamky notes
```
Ejhle, to se nám nepodaří (protože může být dost velký), přesunout však ano.

Proto je potřeba to říci explicitně.
```
cp -r
```
kopíruje celé složky

### Mažeme
Dneska to nebude krajíc chleba, ale soubory a složky.
```
rm draft.txt soubor.txt
```
je v pohodě, protože to jsou klasické soubory, tzn. ne-složky.
```
rm data-neco     (nejde)
```
```
rm -r
```
maže i adresáře (tzv. rekurzivně).

**Varování: Mazání je napořád, není tu žádný koš!**

```
rm -vr
```
navíc řekne, které soubory to maže. Bez toho přepínače `-v` nám `rm` nic nepoví.

`rm -r /` smaže celý disk, nezadávat!

## Masky názvů souborů

Jak vypsat všechny textové soubory?
nepojmenovávat soubory se speciálními znaky, protože ty znaky mají i svůj speciální význam

```
ls tohle.txt je.txt obsah.txt slozky.txt
ls *.txt
ls */*.pdb
```
hvězdička nahrazuje jednoduché jméno souboru, ale už ne věci za lomítkem

Další spec. znak: `?` - nahrazuje právě jedno libovolné písmeno
```
ls ???????
```

(zobrazí jen soubory, ktré mají 7 písmen v názvu)

```
ls *t*ane.pdb
ls *t?ane.*
ls *t??ane.*
```

Hvězdičky předělává na konkrétní názvy souborů přímo bash, takže program “ls” už dostane konkrétní názvy souborů.

Největší silou bashe je spojování malých prográmků dohromady:
wc data-shell/molecules/cubane.pdb
     20    156    1158   data-shell/molecules/cubane.pdb
řádky    slova    znaky (všechny, vč. mezer)


```
wc molecules/*.pdb
```
(navíc přidá řádek s “total” sumou)


`wc` (bez dalších arg.), Ctrl+D ukončuje stdin (otázka pro zvídavé: Proč zrovna “D”? Odpověď man ascii)
`cat` (bez arg.)

program normálně píše do terminálu, a pomocí > mu řeknu, kam má ten výstup přesměrovat (do souboru)

`sort jmenosouboru`
`sort` (bez arg.)
`sort -n` (numeric sort)


linux umí spoustu takových malých programů a je na vás, abyste si je sami pospojovali

`wc -l *.pdb | sort -n`

`less`, terminálové scrollovátko, ukončení pomocí “q”, v programu se dá vyhledávat stiskem `/` (tím přejdeš do režimu hledání textu) a pak rovnou piš `to_co_hledám`
git log, man, … totiž vezmou svůj výstup a nakrmí ho příkazu less

`head` , tail`

`echo haló haló`

program (od bashe) dostane vždy seznam řetězců

```
$ echo ahoj      halo halooo
ahoj halo haloo
```

`$ echo ahoj *.pdb` (vypíše názvy souborů s příponou .pdb)
`$ echo “ahoj *.pdb”` (vypíše jako jeden řetězec)

`echo $0` - $0 je nahrazen z bashe, echo ho jen tupě vypíše

## Přesměrování výstupu do souboru
```
echo halo halo co se stalo > soubor.txt
```
přesměrováním se přepíše původní soubor

“přesměrování s přidáváním” `>>`

`cat > basnicka.txt` (stdin do souboru)


```
cat ‘halo halo
co se stalo’
``` 
(je název souboru, co obsahuje znak nového řetězce)


`cat` vs. `echo` - neplést si: výpis souboru vs. vypsání argumentů


```
cat data/animals | cut -d ‘,’ -f 2
```


`uniq` - deduplikuje záznamy, ale pamatuje si jen poslední řádek

```
cat | cut | sort | uniq
```

