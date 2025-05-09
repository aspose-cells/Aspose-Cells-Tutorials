---
"description": "Naučte se používat Aspose.Cells pro .NET k snadnému formátování kontingenčních tabulek. Prozkoumejte podrobné techniky pro vylepšení prezentace dat."
"linktitle": "Nastavení možností formátování kontingenční tabulky v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Nastavení možností formátování kontingenční tabulky v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/setting-format-options/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení možností formátování kontingenční tabulky v .NET

## Zavedení
Už jste se někdy cítili zahlceni obrovským objemem dat, které máte k dispozici? Nebo jste shledali obtížné prezentovat tato data jasně a srozumitelně? Pokud ano, vítejte na palubě! Dnes se ponoříme do úžasného světa kontingenčních tabulek v Excelu pomocí knihovny Aspose.Cells pro .NET. Kontingenční tabulky mohou být superhrdiny prezentace dat, transformují hromady čísel do strukturovaných a přehledných sestav, které usnadňují rozhodování. Není to převratná změna?
## Předpoklady
Než se pustíme do tutoriálu, ujistěte se, že máte vše potřebné k úspěchu. Zde jsou předpoklady:
1. Základní znalost C#: Měli byste mít základní znalosti programovacího jazyka C#. Pokud se základy vyznáte, jste připraveni se do toho pustit!
2. Visual Studio nebo jakékoli vývojové prostředí C#: Budete potřebovat integrované vývojové prostředí (IDE), jako je Visual Studio. Tady se začne dít ta pravá magie. 
3. Knihovna Aspose.Cells: Abyste mohli využít sílu knihovny Aspose.Cells, budete si muset stáhnout tento balíček. Snadno ho najdete na adrese [Stránka pro stažení Aspose.Cells](https://releases.aspose.com/cells/net/).
4. Soubor Excel: K procvičení tutoriálu je potřeba vzorový soubor Excel. Pro toto cvičení si můžete vytvořit jednoduchý datový soubor v excelovém listu (například „Book1.xls“).
5. .NET Framework: Ujistěte se, že máte v počítači nainstalovaný .NET Framework.
Rozumíte tomu všemu? Skvělé! A teď se vrhněme na první krok.
## Importovat balíčky
Abychom mohli začít používat knihovnu Aspose.Cells, musíme nejprve importovat potřebné balíčky. Postupujte takto:
### Otevřete svůj projekt
Otevřete si Visual Studio (nebo jakékoli C# IDE, které používáte) a vytvořte nový projekt. Vyberte konzolovou aplikaci, protože vám umožní snadno spustit skript.
### Přidat odkaz na Aspose.Cells
1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte Spravovat balíčky NuGet.
3. Do vyhledávacího pole zadejte `Aspose.Cells` a nainstalujte ho.
Nyní jste připraveni nainstalovat knihovnu. Na začátek souboru s kódem budete muset přidat následující direktivu using:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Tento řádek umožňuje přístup ke všem třídám a metodám dostupným v knihovně Aspose.Cells.
Jakmile jsme položili základy, pojďme si krok za krokem projít každou část procesu. Ukážeme si, jak efektivně nastavit různé možnosti formátování kontingenční tabulky.
## Krok 1: Definujte adresář dokumentů
Nejprve je třeba nastavit cestu k adresáři dokumentů, kde se nachází vstupní soubor Excel. Tento řádek kódu určuje, kde se vaše soubory nacházejí.
```csharp
string dataDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kde je uložen soubor „Book1.xls“. To pomůže programu vědět, kde má hledat vstupní soubor.
## Krok 2: Načtěte soubor šablony
Dále načteme soubor Excel, který chceme upravit. To se provádí pomocí `Workbook` třída.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
V podstatě tento příkaz říká vašemu programu, aby otevřel soubor „Book1.xls“, abychom mohli pracovat s jeho daty.
## Krok 3: Získejte první pracovní list
Nyní, když máme otevřený sešit, pojďme se ponořit do listu, který obsahuje naše data. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Zde přistupujeme k prvnímu listu sešitu (protože indexování začíná od nuly). Pokud jsou vaše data na jiném listu, jednoduše upravte index.
## Krok 4: Přístup k kontingenční tabulce
Kontingenční tabulky jsou mocné, ale nejdříve si musíme vybrat tu, se kterou chceme pracovat. Za předpokladu, že znáte index kontingenční tabulky, zde je návod, jak k němu přistupovat.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
V tomto případě přistupujeme k první kontingenční tabulce (index 0) v listu. 
## Krok 5: Nastavení celkových součtů pro řádky v kontingenční tabulce
Začněme s formátováním! Můžeme nakonfigurovat, zda se v naší kontingenční tabulce mají zobrazovat celkové součty pro řádky.
```csharp
pivotTable.RowGrand = true;
```
Nastavení této vlastnosti na `true` zobrazí celkové součty ve spodní části každého řádku v kontingenční tabulce. Je to jednoduchý, ale efektivní způsob, jak poskytnout souhrny.
## Krok 6: Nastavení celkových součtů pro sloupce v kontingenční tabulce
Stejně jako nastavujeme celkové součty pro řádky, můžeme to udělat i pro sloupce.
```csharp
pivotTable.ColumnGrand = true;
```
Po aktivaci této možnosti se součty zobrazí na pravé straně každého sloupce. Vaše kontingenční tabulka je nyní mistrem v sumarizaci dat oběma směry!
## Krok 7: Zobrazení vlastního řetězce pro hodnoty Null
Často přehlíženým detailem je zpracování hodnot null. Možná budete chtít, aby se v buňkách s hodnotami null zobrazoval určitý řetězec. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Díky tomu se v kontingenční tabulce zobrazí hodnota „null“ vždy, když narazí na prázdnou buňku, což dodá vašim sestavám přehlednost a konzistenci.
## Krok 8: Nastavení rozvržení kontingenční tabulky
Kontingenční tabulky mohou mít různá rozvržení a my si je můžeme přizpůsobit podle našich požadavků. Nastavme rozvržení na „DownThenOver“.
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Tento příkaz upraví pořadí, ve kterém se pole zobrazují v sestavě, a usnadní tak její čtení. 
## Krok 9: Uložení souboru Excel
Nakonec, jakmile provedete všechny tyto krásné úpravy, je třeba změny uložit zpět do souboru aplikace Excel. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Tento řádek uloží upravený sešit jako „output.xls“ do vámi zadaného adresáře. 
A takhle jste si vylepšili kontingenční tabulku o všechny tyto fantastické možnosti formátování!
## Závěr
Páni, to jsme spolu urazili pěknou cestu, že? Využitím možností knihovny Aspose.Cells pro .NET můžete bez námahy transformovat vzhled a chování dat v Excelu. Probrali jsme, jak načíst sešit, jak otevřít a naformátovat kontingenční tabulku, a vše jsme završili uložením našich úprav. Data nemusí být fádní a ponurá; s pár úpravami mohou zářit.
## Často kladené otázky
### Co je to kontingenční tabulka?
Kontingenční tabulky jsou funkcí Excelu, která dynamicky shrnuje a analyzuje data.
### Musím mít nainstalovaný Excel, abych mohl používat Aspose.Cells?
Ne, Aspose.Cells je samostatná knihovna, která nevyžaduje instalaci Excelu.
### Mohu vytvářet pivotní tabulky pomocí Aspose.Cells?
Ano, Aspose.Cells umožňuje vytvářet, upravovat a manipulovat s kontingenčními tabulkami.
### Je Aspose.Cells zdarma?
Aspose.Cells je placená knihovna, ale k dispozici je bezplatná zkušební verze.
### Kde najdu další dokumentaci k Aspose.Cells?
Podívejte se na [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobné návody a příklady.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}