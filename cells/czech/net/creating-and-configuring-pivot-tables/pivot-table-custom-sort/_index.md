---
title: Vlastní řazení kontingenční tabulky Programově v .NET
linktitle: Vlastní řazení kontingenční tabulky Programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se programově třídit kontingenční tabulky v .NET pomocí Aspose.Cells. Podrobný průvodce nastavením, konfigurací, řazením a ukládáním výsledků jako soubory Excel a PDF.
weight: 29
url: /cs/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní řazení kontingenční tabulky Programově v .NET

## Zavedení
Pokud jde o práci s Excelem v prostředí .NET, jedna knihovna vyniká mezi ostatními: Aspose.Cells. Nemáte rádi, když vám nástroj umožňuje programově manipulovat s tabulkami? To je přesně to, co Aspose.Cells dělá! V dnešním tutoriálu se ponoříme hluboko do světa kontingenčních tabulek a ukážeme vám, jak programově implementovat vlastní řazení pomocí této univerzální knihovny.
## Předpoklady
Než si vyhrneme rukávy a pustíme se do kódu, ujistěte se, že máte připraveno několik věcí:
1. Visual Studio: Budete potřebovat funkční verzi sady Visual Studio. Je to hřiště, kde se dějí všechna kouzla.
2. .NET Framework: Znalost programování .NET je nezbytná. Ať už jste nadšenci pro .NET Core nebo .NET Framework, můžete začít.
3.  Knihovna Aspose.Cells: Musíte nainstalovat knihovnu Aspose.Cells. Můžete to získat z[Odkaz ke stažení](https://releases.aspose.com/cells/net/) a přidejte jej do svého projektu.
4. Základní porozumění kontingenčním tabulkám: I když nemusíte být odborníkem, při procházení tohoto výukového programu vám pomůže trocha znalostí o tom, jak kontingenční tabulky fungují.
5.  Ukázkový soubor aplikace Excel: Pojmenujte si ukázkový soubor aplikace Excel`SamplePivotSort.xlsx` připraven ve vašem pracovním adresáři k testování.
## Importujte balíčky
Jakmile máte všechny své předpoklady seřazeny, prvním krokem je import potřebných balíčků. Chcete-li to provést, vložte do horní části kódu následující řádky:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Tento balíček poskytuje všechny funkce, které potřebujete pro manipulaci se soubory Excel pomocí Aspose.Cells.

Dobře, pojďme do zábavné části! Proces vytváření kontingenční tabulky a použití vlastního řazení rozdělíme do zvládnutelných kroků.
## Krok 1: Nastavte sešit
Abychom to mohli začít, musíme nastavit náš sešit. Postup je následující:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 V tomto kroku inicializujeme nový`Workbook` instance s cestou k našemu souboru Excel. Funguje to jako plátno, kde naše kontingenční tabulka ožije.
## Krok 2: Otevřete sešit
Dále musíme přistupovat k listu, kam přidáme naši kontingenční tabulku.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Zde vezmeme první pracovní list v našem sešitu a zavoláme na něj`PivotTableCollection`. Tato kolekce nám umožňuje spravovat všechny kontingenční tabulky na tomto listu.
## Krok 3: Vytvořte svou první kontingenční tabulku
Nyní je čas vytvořit naši kontingenční tabulku.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Do našeho listu přidáváme novou kontingenční tabulku, která určuje rozsah dat a jejich umístění. "E3" označuje, kde chceme, aby naše kontingenční tabulka začínala. Na tuto novou kontingenční tabulku pak odkazujeme pomocí jejího indexu.
## Krok 4: Konfigurace nastavení kontingenční tabulky
Pojďme nakonfigurovat naši kontingenční tabulku! To znamená kontrolovat aspekty, jako jsou celkové součty a uspořádání pole.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Zajistíme, aby se nezobrazovaly celkové součty pro řádky a sloupce, což může čistit data. Poté přidáme první pole do oblasti řádku, což umožňuje automatické řazení a řazení vzestupně.
## Krok 5: Přidejte sloupcová a datová pole
Jakmile jsou řádky nastaveny, přidejte sloupec a datová pole.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Druhé pole přidáme jako sloupec a naformátujeme jej jako datum. Opět povolujeme automatické třídění a vzestupné pořadí, abychom měli věci uspořádané. Nakonec musíme do naší datové oblasti přidat třetí pole:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Krok 6: Obnovte a vypočítejte kontingenční tabulku
Po přidání všech nezbytných polí se ujistěte, že je naše kontingenční tabulka čerstvá a připravená.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Tyto metody obnoví data a přepočítají je, čímž zajistí, že vše bude aktuální a správně zobrazeno v naší kontingenční tabulce.
## Krok 7: Vlastní řazení na základě hodnot polí řádků
Pojďme přidat trochu vkusu tím, že seřadíme kontingenční tabulku podle konkrétních hodnot, jako je „mořské plody“.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Opakujeme proces vytvořením další kontingenční tabulky a jejím nastavením podobně jako první. Nyní jej můžeme dále přizpůsobit:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Krok 8: Další přizpůsobení řazení Zkusme jinou metodu řazení na základě konkrétního data:
```csharp
// Přidání další kontingenční tabulky pro řazení podle data
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Opakujte nastavení řádků a sloupců podobně jako v předchozích krocích
```
Stačí opakovat stejný proces a vytvořit třetí kontingenční tabulku s kritérii řazení přizpůsobenými vašim potřebám.
## Krok 9: Uložte WorkbookTime, abyste ušetřili veškerou tvrdou práci, kterou jsme do toho vložili!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Zde uložíte sešit jako soubor Excel a PDF. The`PdfSaveOptions` umožňuje lepší formátování a zajišťuje, že se každý list po převodu zobrazí na samostatné stránce.
## Krok 10: Dokončete UpWolte to všechno tím, že dáte uživateli vědět, že je vše v pořádku.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Závěr
Nyní jste se naučili, jak využít sílu Aspose.Cells k vytváření a přizpůsobení kontingenčních tabulek ve vašich aplikacích .NET. Od počátečního nastavení až po vlastní třídění se každý krok spojuje a poskytuje bezproblémový zážitek. Ať už potřebujete prezentovat roční údaje o prodeji nebo sledovat statistiky zásob, tyto dovednosti vám dobře poslouží!
## FAQ
### Co je kontingenční tabulka?
Kontingenční tabulka je nástroj pro zpracování dat v Excelu, který umožňuje sumarizovat a analyzovat data a poskytuje flexibilní způsob snadného získávání přehledů.
### Jak nainstaluji Aspose.Cells?
 Můžete jej nainstalovat přes NuGet ve Visual Studiu nebo si jej stáhnout přímo z[Odkaz ke stažení](https://releases.aspose.com/cells/net/).
### Existuje zkušební verze Aspose.Cells?
 Ano! Můžete si to vyzkoušet zdarma návštěvou[Odkaz na bezplatnou zkušební verzi](https://releases.aspose.com/).
### Mohu seřadit více polí v kontingenční tabulce?
Absolutně! Můžete přidat a seřadit více polí na základě vašich požadavků.
### Kde najdu podporu pro Aspose.Cells?
 Komunita je poměrně aktivní a na jejím fóru můžete klást otázky[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
