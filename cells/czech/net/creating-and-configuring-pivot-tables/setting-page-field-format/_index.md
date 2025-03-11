---
title: Nastavení formátu pole stránky programově v .NET
linktitle: Nastavení formátu pole stránky programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak nastavit formáty polí stránky v kontingenčních tabulkách programově pomocí Aspose.Cells for .NET. Postupujte podle našeho podrobného návodu pro bezproblémovou správu dat.
weight: 21
url: /cs/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení formátu pole stránky programově v .NET

## Zavedení
Vytváření a manipulace se soubory Excel prostřednictvím kódu může být docela posilující, zvláště když potřebujete analyzovat velké datové sady. Jedním z fantastických nástrojů ve vašem arzenálu je Aspose.Cells for .NET, který vám umožňuje programově pracovat se soubory aplikace Excel a vytvářet složité struktury sestav. V tomto kurzu se ponoříme do toho, jak můžete nastavit formáty polí stránky v kontingenční tabulce pomocí této výkonné knihovny. Ať už jste zkušený vývojář nebo začátečník, na konci této příručky budete mít jasno v tom, jak pracovat s kontingenčními tabulkami a jejich různými nastaveními v .NET.
## Předpoklady
Než se po hlavě vrhneme do kódování, ujistěte se, že máte vše správně nastavené. Budete potřebovat následující:
- Visual Studio: Pracovní prostředí, kde můžete psát a spouštět svůj kód .NET.
-  Aspose.Cells: Můžete si stáhnout knihovnu[zde](https://releases.aspose.com/cells/net/).
- Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
-  Soubor Excel: Připravte si soubor Excel (např`Book1.xls`) obsahující data vhodná pro vytvoření kontingenční tabulky. 
 Pokud jste tak ještě neučinili, získejte bezplatnou zkušební verzi Aspose.Cells[zde](https://releases.aspose.com/).
## Importujte balíčky
Chcete-li to nastartovat, budete muset do svého projektu importovat správné balíčky. Začněte přidáním odkazů na knihovnu Aspose.Cells ve vašem projektu C#. Jak na to:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Tím získáte všechny potřebné třídy a metody potřebné k manipulaci se soubory aplikace Excel pomocí Aspose.Cells.
## Krok 1: Nastavte svůj pracovní prostor
Začněte definováním pracovního adresáře, kde budou uloženy vaše soubory Excel. Proměnnou můžete deklarovat například takto:
```csharp
string dataDir = "Your Document Directory";
```
## Načítání sešitu
Dále musíme načíst naši excelovou šablonu. Toto je zásadní krok, protože vytváří kontext pro naše operace:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Tento řádek načte existující sešit ze zadaného adresáře.
## Krok 2: Otevřete sešit
Po načtení sešitu je čas otevřít list, který obsahuje kontingenční tabulku nebo data, která chcete analyzovat. Můžete to udělat takto:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Tím se získá první list načteného sešitu. Pokud pracujete s více listy, můžete index snadno upravit.
## Krok 3: Přístup ke kontingenční tabulce
 Pokračujeme, zpřístupníme kontingenční tabulku v našem vybraném listu. Pokud používáte jednu kontingenční tabulku, můžete její index nastavit na`0`:
```csharp
int pivotindex = 0;
// Přístup ke kontingenční tabulce
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Tento fragment kódu vybere první kontingenční tabulku v listu. 
## Krok 4: Konfigurace kontingenční tabulky
Nyní přichází ta vzrušující část! Nastavíme kontingenční tabulku tak, aby zobrazovala celkové součty pro řádky:
```csharp
pivotTable.RowGrand = true;
```
Tento řádek zajišťuje, že váš přehled zobrazí celkové součty, které mohou být užitečným souhrnem pro analýzu dat.
## Krok 5: Přístup k polím řádků a jejich konfigurace
Dále musíme získat přístup k polím řádků kontingenční tabulky:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Tato kolekce nám umožňuje manipulovat s poli podle potřeby.
## Nakonfigurujte pole prvního řádku
Chcete nastavit konkrétní typy mezisoučtů? Přistupme k prvnímu poli v naší kolekci a nakonfigurujeme jej:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Nastavení mezisoučtů.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 Povolením`Sum` a`Count` mezisoučty, můžeme rychle shrnout data v naší zprávě.
## Krok 6: Nastavení možností automatického třídění
Dále zapojme do hry chytré třídění. Tímto způsobem vaše kontingenční tabulka uspořádá data ve smysluplném pořadí:
```csharp
// Nastavení možností automatického třídění.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Použití předdefinovaného třídícího pole.
```
Tento fragment kódu umožňuje automatické řazení a určuje vzestupné pořadí. 
## Krok 7: Nastavení možností AutoShow
Chcete svá data dále filtrovat? Možnost AutoShow je užitečná pro zobrazení konkrétních datových bodů za definovaných podmínek:
```csharp
// Nastavení možností autoShow.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Zadejte pole pro automatické zobrazení.
```
Tím je zajištěno, že kontingenční tabulka zobrazuje pouze relevantní data, což zvyšuje přehlednost a zaměření.
## Krok 8: Uložte svou práci
Po všech těch konfiguracích byste nechtěli přijít o svou práci! Upravený sešit uložte takto:
```csharp
workbook.Save(dataDir + "output.xls");
```
Nyní můžete najít nově vytvořený soubor Excel v adresáři dokumentů.
## Závěr
A tady to máte! Prošli jsme komplexním a praktickým přístupem k programovému nastavení formátů polí stránky v kontingenční tabulce pomocí Aspose.Cells pro .NET. Pomocí poskytnutých jednoduchých kroků byste si měli být jisti, že upravíte data aplikace Excel tak, aby vyhovovala vašim potřebám vytváření sestav. Je neuvěřitelné, čeho můžete dosáhnout, když spojíte sílu C# s Aspose.Cells.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory Excelu programově.
### Jak nainstaluji Aspose.Cells?
 Můžete si jej stáhnout přímo z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
### Mohu používat Aspose.Cells bez instalace Excelu?
Ano, Aspose.Cells je samostatná knihovna, která nevyžaduje instalaci aplikace Microsoft Excel.
### Kde najdu podrobnou podporu?
 Podrobnou podporu a fóra získáte na adrese[Aspose Support](https://forum.aspose.com/c/cells/9).
### Jak mohu získat dočasnou licenci?
 Dočasnou licenci můžete získat od[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
