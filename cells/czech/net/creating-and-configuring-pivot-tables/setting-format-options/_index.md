---
title: Nastavení možností formátu kontingenční tabulky v .NET
linktitle: Nastavení možností formátu kontingenční tabulky v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se používat Aspose.Cells pro .NET k snadnému formátování kontingenčních tabulek. Prozkoumejte techniky krok za krokem ke zlepšení prezentace dat.
weight: 20
url: /cs/net/creating-and-configuring-pivot-tables/setting-format-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení možností formátu kontingenční tabulky v .NET

## Zavedení
Cítili jste se někdy ohromeni obrovským objemem dat, které máte k dispozici? Nebo je pro vás obtížné prezentovat tato data jasným a srozumitelným způsobem? Pokud ano, vítejte na palubě! Dnes se ponoříme do úžasného světa kontingenčních tabulek v Excelu pomocí knihovny Aspose.Cells pro .NET. Kontingenční tabulky mohou být superhrdiny prezentace dat, které přeměňují hromady čísel na strukturované přehledné zprávy, díky nimž je rozhodování hračkou. Není to změna hry?
## Předpoklady
Než se vrhneme na tutoriál, ujistěte se, že jste vybaveni vším, co potřebujete k úspěchu. Zde jsou předpoklady:
1. Základní znalost C#: Měli byste mít základní znalosti programovacího jazyka C#. Pokud jste spokojeni se základy, jste připraveni to řešit!
2. Visual Studio nebo libovolné C# IDE: Budete potřebovat integrované vývojové prostředí (IDE), jako je Visual Studio. Tady se děje kouzlo. 
3. Knihovna Aspose.Cells: Abyste mohli využít sílu Aspose.Cells, budete si muset stáhnout tento balíček. Můžete jej snadno najít na[Stránka ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/).
4. Soubor Excel: K procvičení výukového programu je vyžadován vzorový soubor Excel. Pro toto cvičení můžete vytvořit jednoduchou datovou sadu v listu aplikace Excel (např. „Sešit1.xls“).
5. .NET Framework: Ujistěte se, že máte na svém počítači nainstalovaný .NET Framework.
Máš to všechno? Fantastický! Nyní přejdeme k prvnímu kroku.
## Importujte balíčky
Abychom mohli začít používat knihovnu Aspose.Cells, musíme nejprve naimportovat potřebné balíčky. Zde je postup:
### Otevřete svůj projekt
Otevřete Visual Studio (nebo jakékoli C# IDE, které používáte) a vytvořte nový projekt. Vyberte si konzolovou aplikaci, protože vám umožní snadno spouštět skript.
### Přidejte odkaz Aspose.Cells
1. Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte Spravovat balíčky NuGet.
3.  Do vyhledávacího pole zadejte`Aspose.Cells` a nainstalujte jej.
Nyní jste připraveni přinést knihovnu. Na začátek souboru kódu budete muset přidat následující direktivu using:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Tento řádek umožňuje přístup ke všem třídám a metodám dostupným v knihovně Aspose.Cells.
Po položení země si projdeme jednotlivé části procesu krok za krokem. Probereme, jak efektivně nastavit různé možnosti formátu pro kontingenční tabulku.
## Krok 1: Definujte svůj adresář dokumentů
Nejprve musíte nastavit cestu k adresáři dokumentů, kde se nachází váš vstupní soubor Excel. Tento řádek kódu určuje, kde jsou umístěny vaše soubory.
```csharp
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde je uložen váš soubor "Book1.xls". To pomáhá programu vědět, kde má hledat vstupní soubor.
## Krok 2: Načtěte soubor šablony
 Dále načteme soubor Excel, se kterým chceme manipulovat. To se provádí pomocí`Workbook` třída.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Tento příkaz v podstatě říká vašemu programu, aby otevřel soubor "Sešit1.xls", abychom mohli pracovat s jeho daty.
## Krok 3: Získejte první pracovní list
Nyní, když máme náš sešit otevřený, pojďme se ponořit do listu, který obsahuje naše data. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Zde přistupujeme k prvnímu listu sešitu (protože indexování začíná od nuly). Pokud jsou vaše data na jiném listu, jednoduše upravte index.
## Krok 4: Přístup ke kontingenční tabulce
Kontingenční tabulky jsou výkonné, ale nejprve musíme uchopit tu, se kterou chceme pracovat. Za předpokladu, že znáte index kontingenční tabulky, zde je návod, jak k němu přistupovat.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
V tomto případě přistupujeme k první kontingenční tabulce (index 0) v listu. 
## Krok 5: Nastavte celkové součty kontingenční tabulky pro řádky
Začněme formátovat! Můžeme nakonfigurovat, zda se mají zobrazovat celkové součty pro řádky v naší kontingenční tabulce.
```csharp
pivotTable.RowGrand = true;
```
 Nastavení této vlastnosti na`true` zobrazí celkové součty ve spodní části každého řádku v kontingenční tabulce. Je to jednoduchý, ale účinný způsob poskytování souhrnů.
## Krok 6: Nastavte celkové součty kontingenční tabulky pro sloupce
Stejně jako nastavujeme celkové součty pro řádky, můžeme to udělat i pro sloupce.
```csharp
pivotTable.ColumnGrand = true;
```
Povolením této možnosti získáte součty na pravé straně každého sloupce. Vaše kontingenční tabulka je nyní mistrem v sumarizaci dat oběma způsoby!
## Krok 7: Zobrazení vlastního řetězce pro hodnoty Null
Často přehlíženým detailem je zpracování nulových hodnot. Možná budete chtít, aby se v buňkách, kde jsou hodnoty null, objevil konkrétní řetězec. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Tím se kontingenční tabulka nastaví tak, aby vždy, když narazí na prázdnou buňku, zobrazovala „null“, což vašim sestavám dodává přehlednost a konzistenci.
## Krok 8: Nastavte rozvržení kontingenční tabulky
Kontingenční tabulky mohou mít různá rozvržení a můžeme je přizpůsobit na základě našich požadavků. Nastavíme rozložení na "DownThenOver".
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Tento příkaz upravuje pořadí, ve kterém jsou pole zobrazena v sestavě, a usnadňuje tak čtení. 
## Krok 9: Uložení souboru Excel
Nakonec, jakmile provedete všechny tyto krásné úpravy, musíte změny uložit zpět do souboru aplikace Excel. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Tento řádek uloží upravený sešit jako „output.xls“ do vámi zadaného adresáře. 
A právě tak jste svou kontingenční tabulku vylepšili o všechny tyto fantastické možnosti formátování!
## Závěr
Páni, ušli jsme spolu docela dlouhou cestu, že? Využitím možností knihovny Aspose.Cells pro .NET můžete bez námahy transformovat, jak vaše data vypadají a chovají se v Excelu. Probrali jsme, jak načíst sešit, získat přístup a formátovat kontingenční tabulku, a vše vyvrcholili uložením našich úprav. Data nemusí být fádní a ponurá; s pár úpravami dokáže skvěle zářit.
## FAQ
### Co je kontingenční tabulka?
Kontingenční tabulky jsou funkce Excelu, která dynamicky shrnuje a analyzuje data.
### Potřebuji k použití Aspose.Cells nainstalovaný Excel?
Ne, Aspose.Cells je samostatná knihovna, která nevyžaduje instalaci Excelu.
### Mohu vytvářet kontingenční tabulky pomocí Aspose.Cells?
Ano, Aspose.Cells umožňuje vytvářet, upravovat a manipulovat s kontingenčními tabulkami.
### Je Aspose.Cells zdarma?
Aspose.Cells je placená knihovna, ale je k dispozici bezplatná zkušební verze.
### Kde najdu další dokumentaci Aspose.Cells?
 Podívejte se na[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobné návody a příklady.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
