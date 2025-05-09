---
"description": "Naučte se programově vytvářet kontingenční tabulku v .NET pomocí Aspose.Cells s naším podrobným návodem. Efektivně analyzujte svá data."
"linktitle": "Programové vytvoření nové kontingenční tabulky v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové vytvoření nové kontingenční tabulky v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové vytvoření nové kontingenční tabulky v .NET

## Zavedení
Vytvoření kontingenční tabulky se může zdát jako zastrašující úkol, zvláště když to děláte programově. Ale nebojte se! S Aspose.Cells pro .NET je sestavení kontingenční tabulky nejen jednoduché, ale také poměrně výkonné pro analýzu dat. V tomto tutoriálu vás krok za krokem provedeme tím, jak vytvořit novou kontingenční tabulku v aplikaci .NET. Ať už přidáváte data pro prodej, sport nebo jakoukoli jinou obchodní metriku, tento průvodce vám pomůže s provozem vašich kontingenčních tabulek v mžiku.

## Předpoklady
Než se do toho pustíme, ujistěte se, že máte vše připravené. Zde je to, co musíte udělat:

1. Instalace .NET Frameworku: Ujistěte se, že máte na svém počítači nainstalovaný .NET Framework. Aspose.Cells podporuje různé verze, ale nejlepší je držet se té nejnovější.
2. Knihovna Aspose.Cells: Potřebujete mít knihovnu Aspose.Cells. Můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/) nebo si pořiďte [dočasná licence](https://purchase.aspose.com/temporary-license/) pro hodnocení.
3. Nastavení IDE: Mějte připravené IDE kompatibilní s C#, například Visual Studio, kde můžete začít nový projekt.
4. Základní znalost C#: Znalost programování v C# vám pomůže sledovat text, aniž byste se příliš zasekli.

Jste připraveni? Skvělé! Pojďme se pustit do importu potřebných balíčků.

## Importovat balíčky
Nejdříve je potřeba importovat požadované jmenné prostory do projektu v C#. Otevřete soubor v C# a pomocí direktiv do něj přidejte následující:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Tyto jmenné prostory vám poskytují přístup k funkcím sešitu, listu a kontingenční tabulky, které budeme v tomto tutoriálu používat.

## Krok 1: Vytvoření objektu sešitu
Vytvoření sešitu je začátkem vaší cesty. Začněme vytvořením instance nového sešitu a přístupem k prvnímu listu.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvoření instance objektu Workbook
Workbook workbook = new Workbook();

// Získání reference nově přidaného listu
Worksheet sheet = workbook.Worksheets[0];
```

V tomto kroku vytvoříme `Workbook` instanci, která představuje náš excelový soubor, a vezmeme si úplně první list, který bude sloužit jako hřiště pro pivotní tabulku.

## Krok 2: Vložení dat do buněk
Dále si naplníme náš pracovní list vzorovými daty. Vložíme řádky pro různé sporty, čtvrtletí a údaje o prodeji, abychom naši kontingenční tabulku shrnuli.

```csharp
Cells cells = sheet.Cells;

// Nastavení hodnoty buňkám
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Vyplnění datové buňky = buňky["A2"];
cell.PutValue("Golf");
// ... Další datové položky
```

Zde definujeme záhlaví sloupců a vkládáme hodnoty pod každé záhlaví. Tato data budou sloužit jako zdroj pro naši kontingenční tabulku, proto se ujistěte, že jsou uspořádaná! Pokračujte v tomto bloku a vytvoříte komplexní datovou sadu.

## Krok 3: Přidání kontingenční tabulky
Jakmile máme data připravená, je čas vytvořit kontingenční tabulku. K přidání naší nové kontingenční tabulky použijeme kolekci kontingenčních tabulek z pracovního listu.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Přidání kontingenční tabulky do listu
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

V tomto úryvku kódu přidáme do listu kontingenční tabulku, která odkazuje na naši datovou oblast (v tomto případě buňky A1 až C8). Kontingenční tabulku umístíme na začátek buňky E3 a pojmenujeme ji „KontrolníTable2“. Docela jednoduché, že?

## Krok 4: Přizpůsobení kontingenční tabulky
Nyní, když máme naši kontingenční tabulku, si ji upravme tak, aby zobrazovala smysluplné souhrny. Můžeme ovládat, co se zobrazí v řádcích, sloupcích a datových oblastech kontingenční tabulky.

```csharp
// Přístup k instanci nově přidané kontingenční tabulky
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Nezobrazují se celkové součty pro řádky.
pivotTable.RowGrand = false;

// Přetažení prvního pole do oblasti řádků.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Přetažení druhého pole do oblasti sloupců.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Přetažení třetího pole do datové oblasti.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

V tomto kroku řekneme kontingenční tabulce, aby skryla celkové součty pro řádky, a poté určíme, která pole se vloží do oblasti řádků, sloupců a dat. Názvy sportů vyplní řádky, čtvrtletí sloupce a souhrny poskytnou údaje o prodeji.

## Krok 5: Uložení sešitu
Nakonec si chceme uložit nově vytvořený sešit, abychom viděli plody naší práce.

```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Stačí zadat správnou cestu a výstup kontingenční tabulky bude uložen do souboru aplikace Excel, který si můžete otevřít a prohlédnout.

## Závěr
Programové vytváření pivotních tabulek pomocí Aspose.Cells pro .NET vám může výrazně ušetřit čas, zejména při práci s velkými datovými sadami. Naučili jste se, jak nastavit projekt, importovat potřebné balíčky, naplnit data a vytvořit přizpůsobitelnou pivotní tabulku od nuly. Takže až se příště budete topit v číslech, vzpomeňte si na tento tutoriál a nechte Aspose.Cells, aby za vás udělal těžkou práci.

## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro programovou tvorbu a správu tabulek v Excelu.

### Existuje bezplatná zkušební verze pro Aspose.Cells?
Ano, můžete získat bezplatnou zkušební verzi [zde](https://releases.aspose.com/).

### Mohu si přizpůsobit vzhled kontingenční tabulky?
Rozhodně! Formátování, rozvržení a dokonce i styly kontingenční tabulky si můžete přizpůsobit podle svých potřeb.

### Kde najdu další příklady a dokumentaci k Aspose.Cells?
Můžete zkontrolovat [dokumentace](https://reference.aspose.com/cells/net/) pro komplexní návody a příklady.

### Jak získám podporu pro Aspose.Cells?
Podporu můžete získat prostřednictvím [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}