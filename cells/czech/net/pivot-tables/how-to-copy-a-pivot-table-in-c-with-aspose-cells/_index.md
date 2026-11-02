---
category: general
date: 2026-09-27
description: Naučte se, jak zkopírovat kontingenční tabulku v C# pomocí Aspose.Cells.
  Zahrnuje kopírování řádků s formátováním, kopírování kontingenční tabulky na jiný
  list a export kontingenční tabulky do nového sešitu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: cs
lastmod: 2026-09-27
og_description: Jak zkopírovat kontingenční tabulku v C# pomocí Aspose.Cells. Postupujte
  podle podrobného návodu, jak kopírovat řádky s formátováním, přesunout kontingenční
  tabulku na jiný list a exportovat ji do nového sešitu.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Jak zkopírovat kontingenční tabulku v C# – kompletní průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Jak zkopírovat kontingenční tabulku v C# pomocí Aspose.Cells
url: /cs/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku v C# pomocí Aspose.Cells

Pokud potřebujete **zkopírovat kontingenční tabulku** z jednoho listu do druhého, naučení se **jak zkopírovat kontingenční tabulku** v C# s Aspose.Cells vám může ušetřit hodiny ruční práce. Tento přístup vám také umožní **zkopírovat řádky s formátováním**, zachovat pivotní cache a dokonce **exportovat kontingenční tabulku do nového sešitu**, když potřebujete samostatný soubor.

Tento tutoriál vás provede kompletním pracovním postupem:

* vytvořit sešit,  
* zkopírovat oblast kontingenční tabulky při zachování formátování,  
* umístit zkopírovaná data na nový list a  
* uložit výsledek jako samostatný soubor.

Uvidíte, proč je vestavěná metoda `CopyRows` nejspolehlivějším způsobem, jak **zkopírovat kontingenční tabulku do jiného listu**, a získáte tipy pro řešení okrajových případů, jako jsou skryté řádky nebo externí zdroje dat.

## Požadavky

Než začnete, ujistěte se, že máte:

| Požadavek | Proč je to důležité |
|-----------|---------------------|
| .NET 6.0 nebo novější | Aspose.Cells podporuje .NET 6+ a poskytuje nejlepší výkon. |
| Visual Studio 2022 (nebo jakékoli C# IDE) | Potřebujete editor, který dokáže obnovit NuGet balíčky. |
| Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`) | Tato knihovna poskytuje API `CopyRows` použité v příkladu. |
| Zdrojový Excel soubor (`source.xlsx`) obsahující kontingenční tabulku v rozsahu `A1:G20` | Kód kopíruje právě tento rozsah; pokud je vaše kontingenční tabulka větší, upravte rozsah. |

Knihovnu nainstalujte pomocí NuGet CLI nebo Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Načtěte sešit, který obsahuje kontingenční tabulku

První řádek vytvoří objekt `Workbook`, který představuje celý Excel soubor. Načtení souboru jednou vám poskytne čtení i zápis ke všem listům.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Proč je tento krok důležitý** – Bez načtení sešitu nemohou žádné následné volání `CopyRows` odkazovat na zdrojová data ani na pivotní cache.

## Krok 2: Připravte zdrojové a cílové listy

Potřebujete cílový list, kam bude zkopírovaná kontingenční tabulka umístěna. Níže uvedený kód získá první list (kde se nachází původní kontingenční tabulka) a přidá nový list pojmenovaný **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tip:** Pokud cílový list již existuje, nejprve zavolejte `Worksheets.RemoveAt(index)`, abyste předešli duplicitním názvům.

## Krok 3: Definujte oblast buněk, která obklopuje kontingenční tabulku

Objekt `CellArea` popisuje buňky v levém horním a pravém dolním rohu rozsahu, který chcete přesunout. V tomto příkladu kontingenční tabulka zabírá `A1:G20`. Pro větší tabulky upravte souřadnice.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Krok 4: Zkopírujte řádky s formátováním a zachovejte pivotní cache

Metoda `CopyRows` kopíruje **řádky** ze zdrojového listu do cílového listu. Předáním `CopyOptions.CopyAll` zajistíte, že hodnoty, formátování, grafy i vložené objekty – vše, co je součástí kontingenční tabulky – bude přeneseno.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Proč `CopyRows` funguje lépe než `Copy` u kontingenčních tabulek

* `CopyRows` respektuje interní pivotní cache, takže zkopírovaná kontingenční tabulka zůstává funkční.
* Zachovává **copy rows with formatting** přesně tak, jak vypadají v původním listu.
* Na rozdíl od jednoduchého `Copy` rozsahu také přesouvá skryté řádky a všechny související slicery.

## Krok 5: Uložte sešit se zkopírovanou kontingenční tabulkou

Nakonec zapíšete upravený sešit na disk. Nový soubor obsahuje původní list plus list **Copy**, který drží plně funkční duplikát původní kontingenční tabulky.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Očekávaný výsledek

Po otevření `pivot_copied.xlsx`:

* List **Sheet1** stále obsahuje původní data a kontingenční tabulku.
* List **Copy** zobrazuje identickou kontingenční tabulku se stejným rozvržením, filtry i formátováním.
* Všechny vzorce a datové spojení zůstávají nedotčeny, protože pivotní cache byla zkopírována spolu s řádky.

## Jak zkopírovat kontingenční tabulku do jiného listu ve stejném sešitu

Pokud potřebujete kontingenční tabulku jen v jiném existujícím listu (např. “Report”), nahraďte krok vytvoření cílového listu odkazem na cílový list:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Tento úryvek ukazuje **copy pivot table to another sheet** bez vytváření nového listu.

## Export kontingenční tabulky do nového sešitu

Někdy chcete kontingenční tabulku v naprosto samostatném souboru. Po operaci kopírování můžete odstranit všechny listy kromě toho, který obsahuje zkopírovanou tabulku, a poté uložit:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Nyní `pivot_only.xlsx` obsahuje jediný list s duplikovanou kontingenční tabulkou, čímž splňuje požadavek **export pivot table to new workbook**.

## Jak zkopírovat řádky Excelu bez ztráty formátování

Stejné volání `CopyRows` funguje pro libovolný rozsah, nejen pro kontingenční tabulky. Pokud potřebujete **copy excel rows** zahrnující podmíněné formátování, datovou validaci nebo sloučené buňky, použijte stejnou metodu:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Protože `CopyOptions.CopyAll` přenáší vše, řádky v cíli vypadají naprosto stejně jako řádky ve zdroji.

## Časté úskalí a jak se jim vyhnout

| Problém | Příznak | Řešení |
|---------|---------|--------|
| Zdrojový rozsah neobsahuje celou kontingenční tabulku | Zkopírovaná tabulka je oříznutá. | Ověřte, že `CellArea` zahrnuje všechny řádky/sloupce tabulky. |
| Cílový list již obsahuje data | Přepsané řádky způsobí ztrátu dat. | Vyberte prázdný list nebo začněte kopírovat od vyššího řádku. |
| Kontingenční tabulka používá externí datový zdroj | Kopie ztratí spojení. | Po kopírování zavolejte `pivotTable.RefreshData()` pro obnovení odkazu. |
| Skryté řádky jsou vynechány | Některé řádky v kopii chybí. | `CopyRows` automaticky kopíruje skryté řádky; ujistěte se, že nepoužíváte `CopyOptions.CopyValuesOnly`. |

## Kompletní, spustitelný příklad

Níže je samostatný program, který můžete vložit do nového konzolového projektu. Ukazuje každý krok zmíněný výše.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Spuštěním programu** vytvoříte `pivot_copied.xlsx` s duplikátem původní kontingenční tabulky na novém listu pojmenovaném **Copy**.

## Závěr

Nyní víte **jak zkopírovat kontingenční tabulku** v C# pomocí


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}