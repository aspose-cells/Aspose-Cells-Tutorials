---
"description": "Naučte se, jak programově nastavit formáty polí stránek v kontingenčních tabulkách pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného návodu pro bezproblémovou správu dat."
"linktitle": "Nastavení formátu polí stránky programově v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Nastavení formátu polí stránky programově v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení formátu polí stránky programově v .NET

## Zavedení
Vytváření a manipulace s excelovými soubory pomocí kódu může být velmi užitečná, zejména pokud potřebujete analyzovat velké datové sady. Jedním z fantastických nástrojů ve vašem arzenálu je Aspose.Cells pro .NET, který vám umožňuje programově interagovat s excelovými soubory a vytvářet složité struktury sestav. V tomto tutoriálu se ponoříme do toho, jak můžete pomocí této výkonné knihovny nastavit formáty polí stránek v kontingenční tabulce. Ať už jste zkušený vývojář nebo začátečník, na konci tohoto průvodce budete mít důkladnou představu o tom, jak pracovat s kontingenčními tabulkami a jejich různými nastaveními v .NET.
## Předpoklady
Než se po hlavě pustíme do programování, ujistěme se, že máte vše správně nastavené. Budete potřebovat následující:
- Visual Studio: Pracovní prostředí, kde můžete psát a spouštět kód .NET.
- Aspose.Cells: Knihovnu si můžete stáhnout [zde](https://releases.aspose.com/cells/net/).
- Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
- Soubor Excel: Mějte připravený soubor Excel (například `Book1.xls`) obsahující data vhodná pro vytvoření kontingenční tabulky. 
Pokud jste tak ještě neučinili, získejte bezplatnou zkušební verzi Aspose.Cells. [zde](https://releases.aspose.com/).
## Importovat balíčky
Abyste to mohli začít, budete muset do projektu importovat správné balíčky. Začněte přidáním odkazů na knihovnu Aspose.Cells do svého projektu v C#. Zde je návod, jak to udělat:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Tím se stahnou všechny potřebné třídy a metody potřebné k manipulaci s excelovými soubory pomocí Aspose.Cells.
## Krok 1: Nastavení pracovního prostoru
Začněte definováním pracovního adresáře, kam budou uloženy vaše soubory Excelu. Proměnnou můžete deklarovat například takto:
```csharp
string dataDir = "Your Document Directory";
```
## Načítání sešitu
Dále musíme načíst naši šablonu aplikace Excel. To je zásadní krok, protože určuje kontext pro naše operace:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Tento řádek načte existující sešit ze zadaného adresáře.
## Krok 2: Přístup k pracovnímu listu
Jakmile je sešit načten, je čas přistupovat k listu, který obsahuje kontingenční tabulku nebo data, která chcete analyzovat. Zde je návod, jak to udělat:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Tím se načte první list načteného sešitu. Pokud pracujete s více listy, můžete snadno upravit index.
## Krok 3: Přístup k kontingenční tabulce
Pokračujeme dále a otevřeme si kontingenční tabulku v našem vybraném listu. Pokud používáte jednu kontingenční tabulku, můžete její index nastavit na `0`:
```csharp
int pivotindex = 0;
// Přístup k kontingenční tabulce
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Tento úryvek kódu vybere první kontingenční tabulku v listu. 
## Krok 4: Konfigurace kontingenční tabulky
A teď přichází ta vzrušující část! Nastavme kontingenční tabulku tak, aby zobrazovala celkové součty pro řádky:
```csharp
pivotTable.RowGrand = true;
```
Tento řádek zajišťuje, že se v sestavě zobrazí celkové součty, což může být užitečné shrnutí pro analýzu dat.
## Krok 5: Přístup k polím řádků a jejich konfigurace
Dále potřebujeme přístup k polím řádků kontingenční tabulky:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Tato kolekce nám umožňuje manipulovat s poli podle potřeby.
## Konfigurace pole prvního řádku
Chcete nastavit konkrétní typy mezisoučtů? Pojďme se podívat na první pole v naší kolekci a nakonfigurovat ho:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Nastavení mezisoučtů.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
Povolením `Sum` a `Count` mezisoučty, můžeme rychle shrnout data v naší zprávě.
## Krok 6: Nastavení možností automatického řazení
Dále si vyzkoušíme chytré řazení. Tímto způsobem vaše kontingenční tabulka uspořádá data ve smysluplném pořadí:
```csharp
// Nastavení možností automatického řazení.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Použití předdefinovaného třídicího pole.
```
Tento úryvek kódu umožňuje automatické řazení a určuje vzestupné pořadí. 
## Krok 7: Nastavení možností automatického zobrazování
Chcete data dále filtrovat? Možnost Automatické zobrazení je užitečná pro zobrazení konkrétních datových bodů za definovaných podmínek:
```csharp
// Nastavení možností automatického zobrazování.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Zadejte pole, které se má automaticky zobrazit.
```
Díky tomu se v kontingenční tabulce zobrazí pouze relevantní data, což zvyšuje přehlednost a zaostření.
## Krok 8: Uložení vaší práce
Po všech těchto konfiguracích byste nechtěli o svou práci přijít! Uložte upravený sešit takto:
```csharp
workbook.Save(dataDir + "output.xls");
```
Nyní najdete nově vytvořený soubor aplikace Excel ve svém adresáři dokumentů.
## Závěr
A tady to máte! Prošli jsme si komplexním a praktickým přístupem k programovému nastavení formátů polí stránky v kontingenční tabulce pomocí Aspose.Cells pro .NET. S těmito jednoduchými kroky byste si měli být jisti, že upravíte data v Excelu tak, aby vyhovovala vašim potřebám v oblasti reportingu. Je neuvěřitelné, čeho můžete dosáhnout, když zkombinujete sílu jazyka C# s Aspose.Cells.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům programově vytvářet, manipulovat a převádět soubory aplikace Excel.
### Jak nainstaluji Aspose.Cells?
Můžete si ho stáhnout přímo z [Webové stránky Aspose](https://releases.aspose.com/cells/net/).
### Mohu používat Aspose.Cells bez instalace Excelu?
Ano, Aspose.Cells je samostatná knihovna, která nevyžaduje instalaci aplikace Microsoft Excel.
### Kde najdu podrobnou podporu?
Podrobnou podporu a fóra naleznete na adrese [Podpora Aspose](https://forum.aspose.com/c/cells/9).
### Jak mohu získat dočasnou licenci?
Dočasnou licenci můžete získat od [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}