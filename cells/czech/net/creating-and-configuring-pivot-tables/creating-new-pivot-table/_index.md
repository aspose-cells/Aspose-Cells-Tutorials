---
title: Vytvořte novou kontingenční tabulku programově v .NET
linktitle: Vytvořte novou kontingenční tabulku programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se vytvářet kontingenční tabulku programově v .NET pomocí Aspose.Cells s naším průvodcem krok za krokem. Efektivně analyzujte svá data.
weight: 13
url: /cs/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte novou kontingenční tabulku programově v .NET

## Zavedení
Vytvoření kontingenční tabulky se může zdát jako zastrašující úkol, zvláště když to děláte programově. Ale nebojte se! S Aspose.Cells pro .NET je sestavování kontingenční tabulky nejen jednoduché, ale také docela výkonné pro analýzu dat. V tomto tutoriálu vás krok za krokem provedeme vytvořením nové kontingenční tabulky v aplikaci .NET. Ať už přidáváte data pro prodej, sport nebo jakoukoli jinou obchodní metriku, tento průvodce vám pomůže rychle zprovoznit kontingenční tabulky.

## Předpoklady
Než se ponoříte dovnitř, ujistěte se, že máte vše připraveno. Zde je to, co musíte udělat:

1. Instalace .NET Framework: Ujistěte se, že máte na svém počítači nainstalovaný .NET Framework. Aspose.Cells podporuje různé verze, ale nejlepší je držet se nejnovější.
2.  Knihovna Aspose.Cells: Musíte mít knihovnu Aspose.Cells. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/)nebo získat a[dočasná licence](https://purchase.aspose.com/temporary-license/) pro hodnocení.
3. Nastavení IDE: Připravte si IDE kompatibilní s C#, jako je Visual Studio, kde můžete začít nový projekt.
4. Základní znalost C#: Znalost programování v C# vám pomůže pokračovat, aniž byste se příliš zabředli.

Jste připraveni? Velký! Pojďme se vrhnout na import potřebných balíčků.

## Importujte balíčky
Nejprve musíte do svého projektu C# importovat požadované jmenné prostory. Otevřete svůj soubor C# a pomocí direktiv přidejte následující:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Tyto jmenné prostory vám poskytují přístup k funkcím sešitu, listu a kontingenční tabulky, které budeme používat v tomto kurzu.

## Krok 1: Vytvořte objekt sešitu
Vytvoření sešitu je začátek vaší cesty. Začněme vytvořením instance nového sešitu a přístupem k prvnímu listu.

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();

// Získání odkazu na nově přidaný list
Worksheet sheet = workbook.Worksheets[0];
```

 V tomto kroku vytvoříme a`Workbook`instance, která představuje náš soubor Excel a vezměte si úplně první pracovní list, který bude naším hřištěm pro kontingenční tabulku.

## Krok 2: Vložte data do buněk
Dále vyplňte náš pracovní list několika ukázkovými daty. Budeme vkládat řádky pro různé sporty, čtvrtletí a údaje o prodeji, aby naše kontingenční tabulka něco shrnula.

```csharp
Cells cells = sheet.Cells;

// Nastavení hodnoty do buněk
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Vyplnění datové buňky = buňky["A2"];
cell.PutValue("Golf");
// ... Více datových záznamů
```

Zde definujeme záhlaví sloupců a vkládáme hodnoty pod každé záhlaví. Tato data budou sloužit jako zdroj pro naši kontingenční tabulku, takže se ujistěte, že jsou uspořádány! Projděte si tento blok a vytvoříte komplexní datovou sadu.

## Krok 3: Přidání kontingenční tabulky
S připravenými daty je čas vytvořit kontingenční tabulku. K přidání naší nové kontingenční tabulky použijeme kolekci kontingenčních tabulek z listu.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Přidání kontingenční tabulky do listu
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

tomto úryvku přidáme do listu kontingenční tabulku, která odkazuje na náš rozsah dat (v tomto případě na buňky A1 až C8). Umístíme kontingenční tabulku počínaje buňkou E3 a pojmenujeme ji "PivotTable2". Docela jednoduché, že?

## Krok 4: Přizpůsobte kontingenční tabulku
Nyní, když máme naši kontingenční tabulku, upravme ji tak, aby zobrazovala smysluplné souhrny. Můžeme ovládat, co se zobrazí v řádcích, sloupcích a datových oblastech kontingenční tabulky.

```csharp
// Přístup k instanci nově přidané kontingenční tabulky
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Nezobrazování celkových součtů pro řádky.
pivotTable.RowGrand = false;

// Přetažením prvního pole do oblasti řádku.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Přetažením druhého pole do oblasti sloupců.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Přetažením třetího pole do datové oblasti.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

V tomto kroku řekneme kontingenční tabulce, aby skryla celkové součty pro řádky, a poté určíme, která pole jdou do oblastí řádků, sloupců a dat. Názvy sportů vyplní řádky, čtvrtletí vyplní sloupce a údaje o prodeji poskytnou souhrny.

## Krok 5: Uložte sešit
Nakonec si chceme uložit náš nově vytvořený sešit, abychom viděli plody naší práce.

```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Stačí zadat správnou cestu a výstup kontingenční tabulky bude uložen do souboru aplikace Excel, který můžete otevřít a zkontrolovat.

## Závěr
Programové vytváření kontingenčních tabulek pomocí Aspose.Cells for .NET vám může výrazně ušetřit čas, zejména při práci s velkými datovými sadami. Naučili jste se, jak nastavit svůj projekt, importovat potřebné balíčky, naplnit data a vytvořit přizpůsobitelnou kontingenční tabulku od začátku. Takže až se příště budete topit v číslech, vzpomeňte si na tento návod a nechte Aspose.Cells, aby za vás udělal těžkou práci.

## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro vytváření a správu tabulek Excelu programově.

### Existuje bezplatná zkušební verze pro Aspose.Cells?
 Ano, můžete získat bezplatnou zkušební verzi[zde](https://releases.aspose.com/).

### Mohu přizpůsobit vzhled kontingenční tabulky?
Absolutně! Formátování, rozvržení a dokonce i styly kontingenční tabulky si můžete přizpůsobit podle svých potřeb.

### Kde najdu další příklady a dokumentaci na Aspose.Cells?
 Můžete zkontrolovat[dokumentace](https://reference.aspose.com/cells/net/) pro komplexní návody a příklady.

### Jak získám podporu pro Aspose.Cells?
 Podporu můžete získat prostřednictvím[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
