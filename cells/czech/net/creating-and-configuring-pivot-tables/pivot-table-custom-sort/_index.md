---
"description": "Naučte se, jak programově třídit kontingenční tabulky v .NET pomocí Aspose.Cells. Podrobný návod, který zahrnuje nastavení, konfiguraci, třídění a ukládání výsledků do souborů Excel a PDF."
"linktitle": "Vlastní řazení kontingenčních tabulek programově v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vlastní řazení kontingenčních tabulek programově v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní řazení kontingenčních tabulek programově v .NET

## Zavedení
Pokud jde o práci s Excelem v prostředí .NET, jedna knihovna mezi ostatními vyniká: Aspose.Cells. Nemilujete, když vám nástroj umožňuje programově manipulovat s tabulkami? Přesně to Aspose.Cells dělá! V dnešním tutoriálu se ponoříme hlouběji do světa kontingenčních tabulek a ukážeme vám, jak programově implementovat vlastní řazení pomocí této všestranné knihovny.
## Předpoklady
Než si vyhrneme rukávy a pustíme se do kódu, ujistěte se, že máte připraveno několik věcí:
1. Visual Studio: Budete potřebovat funkční verzi Visual Studia. Je to hřiště, kde se děje všechna magie.
2. .NET Framework: Znalost programování v .NET je nezbytná. Ať už jste nadšencem pro .NET Core nebo .NET Framework, jste připraveni začít.
3. Knihovna Aspose.Cells: Je třeba nainstalovat knihovnu Aspose.Cells. Můžete ji získat z [Odkaz ke stažení](https://releases.aspose.com/cells/net/) a přidejte ho do svého projektu.
4. Základní znalost pivotních tabulek: I když nemusíte být odborníkem, trocha znalostí o fungování pivotních tabulek bude v tomto tutoriálu užitečná.
5. Ukázkový soubor Excelu: Mějte ukázkový soubor Excelu s názvem `SamplePivotSort.xlsx` připraveno ve vašem pracovním adresáři k testování.
## Importovat balíčky
Jakmile máte všechny potřebné požadavky vyřešené, prvním krokem je import potřebných balíčků. Chcete-li to provést, vložte na začátek kódu následující řádky:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Tento balíček poskytuje veškeré funkce, které potřebujete pro manipulaci s excelovými soubory pomocí Aspose.Cells.

Dobře, pojďme k té zábavné části! Rozebereme si proces vytvoření kontingenční tabulky a použití vlastního řazení do snadno zvládnutelných kroků.
## Krok 1: Nastavení sešitu
Abychom to mohli začít, musíme si připravit sešit. Postupujte takto:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
V tomto kroku inicializujeme nový `Workbook` instanci s cestou k našemu excelovému souboru. To slouží jako plátno, na kterém se naše kontingenční tabulka zobrazí.
## Krok 2: Přístup k pracovnímu listu
Dále potřebujeme přístup k listu, kam přidáme naši kontingenční tabulku.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Zde vezmeme první list v našem sešitu a zavoláme na `PivotTableCollection`Tato kolekce nám umožňuje spravovat všechny kontingenční tabulky na tomto listu.
## Krok 3: Vytvořte si první kontingenční tabulku
Nyní je čas vytvořit naši kontingenční tabulku.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Do našeho listu přidáme novou kontingenční tabulku, v níž určíme rozsah dat a její umístění. „E3“ označuje, kde má naše kontingenční tabulka začínat. Na tuto novou kontingenční tabulku se pak odkážeme pomocí jejího indexu.
## Krok 4: Konfigurace nastavení kontingenční tabulky
Pojďme si nakonfigurovat naši kontingenční tabulku! To znamená ovládat aspekty, jako jsou celkové součty a uspořádání polí.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Zajistíme, aby se nezobrazovaly celkové součty pro řádky a sloupce, což může data vylepšit. Poté přidáme první pole do oblasti řádků, čímž povolíme automatické řazení a vzestupné řazení.
## Krok 5: Přidání sloupců a datových polí
Jakmile jsou řádky nastaveny, přidejme sloupce a datová pole.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Druhé pole přidáme jako sloupec a naformátujeme ho jako datum. Opět povolíme automatické řazení a vzestupné řazení, abychom vše udrželi v pořádku. Nakonec musíme do naší datové oblasti přidat třetí pole:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Krok 6: Obnovení a výpočet kontingenční tabulky
Po přidání všech potřebných polí se ujistěme, že je naše kontingenční tabulka aktuálně připravená.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Tyto metody aktualizují data a přepočítávají je, čímž zajišťují, že je vše aktuální a správně zobrazeno v naší kontingenční tabulce.
## Krok 7: Vlastní řazení na základě hodnot polí řádků
Přidejme trochu šmrncu seřazením kontingenční tabulky na základě konkrétních hodnot, například „Mořské plody“.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Postup opakujeme vytvořením další kontingenční tabulky a jejím nastavením podobným jako u první. Nyní ji můžeme dále přizpůsobit:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Krok 8: Další úpravy řazeníVyzkoušejme jinou metodu řazení na základě konkrétního data:
```csharp
// Přidání další kontingenční tabulky pro řazení podle data
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Opakujte nastavení řádků a sloupců podobně jako v předchozích krocích
```
Stejným procesem jednoduše projdete iterací a vytvoříte třetí kontingenční tabulku s kritérii řazení přizpůsobenými vašim potřebám.
## Krok 9: Uložte si sešit. Ušetřete si veškerou tvrdou práci, kterou jsme do toho vložili!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Zde uložíte sešit jako soubor aplikace Excel a PDF. `PdfSaveOptions` umožňuje lepší formátování a zajišťuje, že se každý list po převodu zobrazí na samostatné stránce.
## Krok 10: DokončeteToto vše zakončete tím, že uživateli dáte vědět, že je vše v pořádku.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Závěr
Nyní jste se naučili, jak využít sílu Aspose.Cells k vytváření a úpravě kontingenčních tabulek ve vašich .NET aplikacích. Od počátečního nastavení až po vlastní řazení se každý krok spojuje a zajišťuje bezproblémový zážitek. Ať už potřebujete prezentovat roční údaje o prodeji nebo sledovat statistiky zásob, tyto dovednosti vám dobře poslouží!
## Často kladené otázky
### Co je to kontingenční tabulka?
Kontingenční tabulka je nástroj pro zpracování dat v Excelu, který umožňuje shrnout a analyzovat data a poskytuje flexibilní způsob, jak snadno získat potřebné informace.
### Jak nainstaluji Aspose.Cells?
Můžete si ho nainstalovat pomocí NuGetu ve Visual Studiu nebo si ho stáhnout přímo z... [Odkaz ke stažení](https://releases.aspose.com/cells/net/).
### Existuje zkušební verze Aspose.Cells?
Ano! Můžete si to vyzkoušet zdarma na adrese [Odkaz na bezplatnou zkušební verzi](https://releases.aspose.com/).
### Mohu v kontingenční tabulce seřadit více polí?
Rozhodně! Můžete přidat a seřadit více polí podle vašich požadavků.
### Kde najdu podporu pro Aspose.Cells?
Komunita je docela aktivní a můžete klást otázky na jejich fóru. [zde](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}