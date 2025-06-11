---
"description": "Naučte se, jak programově změnit zdrojová data kontingenční tabulky pomocí Aspose.Cells pro .NET s naším komplexním podrobným tutoriálem."
"linktitle": "Programová změna zdrojových dat kontingenční tabulky v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programová změna zdrojových dat kontingenční tabulky v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programová změna zdrojových dat kontingenční tabulky v .NET

## Zavedení
Ve světě analýzy dat jen málo nástrojů září tak jasně jako Microsoft Excel. Každý den se na Excelu spoléhá nespočet uživatelů pro správu a analýzu dat, ale v zákulisí je to mnohem složitější než jen klikání a tažení. Pokud jste někdy chtěli programově manipulovat s excelovými soubory – konkrétně změnit zdrojová data kontingenční tabulky – jste na správném místě! V této příručce prozkoumáme, jak toho můžete dosáhnout pomocí Aspose.Cells pro .NET. Ať už jste zkušený vývojář, nebo se teprve ponořujete do moře programování, tento tutoriál je plný cenných informací, které se snadno snášejí.
## Předpoklady
Než se pustíme do změny zdrojových dat kontingenční tabulky, ujistěme se, že máte vše nastavené a připravené k použití:
1. Visual Studio: Ujistěte se, že máte nainstalovanou kopii Microsoft Visual Studia, protože zde budeme psát náš kód.
2. Knihovna Aspose.Cells: Budete si muset stáhnout knihovnu Aspose.Cells a odkazovat na ni ve svém projektu. Můžete si ji stáhnout [zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: I když je tento tutoriál zjednodušený, znalost C# vám pomůže lépe porozumět kódu.
4. Soubor Excel: Měli byste mít ukázkový soubor Excel (například „Book1.xlsx“) obsahující kontingenční tabulku, se kterou můžeme manipulovat.
Dobře, s těmito předpoklady můžeme pokračovat v importu potřebných balíčků a začít s kódováním!
## Importovat balíčky
Nejdříve to nejdůležitější – importujme balíčky, které budeme potřebovat. Otevřete si projekt C# ve Visual Studiu a pomocí direktiv přidejte následující kód na začátek souboru s kódem:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Tyto jmenné prostory vám poskytnou přístup k základním třídám potřebným pro práci s excelovými soubory a manipulaci s jejich obsahem pomocí Aspose.Cells.

Nyní si celý proces rozdělme na několik snadno zvládnutelných kroků. Projdeme si otevřením souboru aplikace Excel, úpravou listu, změnou zdroje dat kontingenční tabulky a uložením výsledků.
## Krok 1: Definujte adresář dokumentů
Nejprve je třeba určit, kde se nachází váš soubor Excel. Upravte `dataDir` proměnnou, která bude odkazovat na složku obsahující váš soubor „Book1.xlsx“.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Tento řádek nastaví adresář, kde je uložen váš soubor Excel, což usnadní jeho pozdější přístup.
## Krok 2: Zadejte vstupní cestu
Dále vytvořme řetězec, který určí úplnou cestu k vašemu vstupnímu souboru aplikace Excel:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
To pomáhá zefektivnit přístup k souborům; nebudete muset v celém kódu opakovaně zadávat stejnou cestu.
## Krok 3: Vytvoření souborového streamu
Nyní je čas otevřít soubor aplikace Excel. Vytvoříme `FileStream` který vám umožní číst obsah souboru aplikace Excel:
```csharp
// Vytvoření proudu souborů obsahujícího soubor Excel, který se má otevřít
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Tento řádek otevře soubor v režimu čtení, což nám umožní přístup k jeho datům.
## Krok 4: Načtení sešitu
Po nastavení proudu souborů je dalším krokem načtení sešitu:
```csharp
// Otevření souboru Excelu prostřednictvím souborového proudu
Workbook workbook = new Workbook(fstream);
```
Tento příkaz vezme váš soubor Excelu a načte ho do `Workbook` objekt. Po načtení můžete soubor dle potřeby upravovat.
## Krok 5: Přístup k pracovnímu listu
Je čas ponořit se do detailů. Zpřístupníme první list v sešitu:
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Díky tomu máte přímý přístup k datům v prvním listu, což usnadňuje jejich úpravy.
## Krok 6: Naplnění nových dat
Dále chceme do buněk vložit nová data. V tomto příkladu přidáme několik vzorových dat:
```csharp
// Naplnění buněk listu novými daty
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Zde uvádíme hodnoty „Golf“, „Qtr4“ a `7000` do konkrétních buněk. Tyto hodnoty můžete změnit dle svých potřeb.
## Krok 7: Změna pojmenovaného rozsahu
Nyní změníme pojmenovaný rozsah, na který se odkazuje kontingenční tabulka. To zahrnuje vytvoření nebo aktualizaci rozsahu:
```csharp
// Změna pojmenovaného rozsahu „Zdroj dat“
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Definováním nového rozsahu zajistíme, že kontingenční tabulka tato nová data použije při aktualizaci.
## Krok 8: Uložení upraveného souboru aplikace Excel
Po všech změnách je zásadní si práci uložit! Uložme si upravený sešit:
```csharp
// Uložení upraveného souboru aplikace Excel
workbook.Save(dataDir + "output.xls");
```
Tento příkaz uloží sešit do nového souboru, takže nepřepíšete původní soubor, pokud nechcete!
## Krok 9: Zavřete souborový stream
Nakonec je nezbytné zavřít souborový stream, abyste uvolnili všechny používané zdroje:
```csharp
// Uzavření souborového proudu pro uvolnění všech zdrojů
fstream.Close();
```
Tento krok zajistí, že vaše aplikace nebude mít únik paměti a zůstane efektivní.
## Závěr
Gratulujeme! Právě jste úspěšně programově změnili zdrojová data kontingenční tabulky v .NET pomocí Aspose.Cells. Tato funkce otevírá mnoho možností pro automatizaci úloh v Excelu a zlepšení vašeho pracovního postupu. Ať už aktualizujete finanční výkazy, sledujete prodejní data nebo si jen hrajete s datovými sadami, schopnost provádět to programově vám může ušetřit spoustu času a snížit riziko chyb.

## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro práci s excelovými soubory, která uživatelům umožňuje programově vytvářet, upravovat a manipulovat s excelovými dokumenty.
### Mohu touto metodou změnit zdrojová data existujících kontingenčních tabulek?
Rozhodně! Tato metoda umožňuje aktualizovat zdroj dat pro existující kontingenční tabulky v sešitu aplikace Excel.
### Musím mít nainstalovaný Office, abych mohl používat Aspose.Cells?
Ne! Aspose.Cells je samostatná knihovna, což znamená, že pro práci se soubory aplikace Excel nepotřebujete nainstalovaný Microsoft Office.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plnou funkčnost si budete muset zakoupit licenci. Podrobnosti naleznete [zde](https://purchase.aspose.com/buy).
### Kde najdu další příklady a podporu?
Pro více příkladů a podporu se podívejte na [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) a jejich komunitní fórum [zde](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}