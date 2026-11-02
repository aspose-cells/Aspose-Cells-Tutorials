---
category: general
date: 2026-09-27
description: Naučte se, jak v C# mazat řádky z tabulky Excel pomocí podrobného návodu,
  který také ukazuje, jak rychle načíst sešit Excel v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: cs
lastmod: 2026-09-27
og_description: Odstraňte řádky z tabulky Excel v C# s jasným příkladem. Tento tutoriál
  také pokrývá, jak načíst sešit Excel v C# a řešit běžné okrajové případy.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Smazání řádků z Excel tabulky v C# – kompletní průvodce kódem
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Jak smazat řádky z tabulky Excel pomocí C#
url: /cs/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odstranění řádků z tabulky Excel v C# – kompletní programovací průvodce

Pokud potřebujete **odstranit řádky z tabulky Excel** v souboru .xlsx, tento tutoriál vám přesně ukáže, jak to provést v C#. Uvidíte stručný, spustitelný příklad, který načte sešit Excel, odstraní konkrétní řádky z první tabulky a uloží výsledek. Přístup funguje s populární knihovnou Aspose.Cells a lze jej přizpůsobit dalším .NET Excel API.

Odstraňování řádků z tabulky je běžný úkol při čištění importovaných dat, zkracování částí reportů nebo automatizaci aktualizací tabulek. Na konci tohoto průvodce budete schopni **načíst sešit Excel v C#**, najít tabulku (ListObject), smazat libovolné řádky a zapsat upravený soubor zpět na disk.

## Požadavky

* .NET 6.0 nebo novější nainstalovaný (kód také funguje s .NET Framework 4.7+).
* Odkaz na NuGet balíček **Aspose.Cells** (nebo jakoukoli kompatibilní knihovnu, která poskytuje typy `Workbook`, `Worksheet` a `ListObject`).
* Vstupní soubor pojmenovaný `input.xlsx` umístěný ve složce, na kterou můžete odkazovat z projektu.
* Základní znalost syntaxe C# a Visual Studio (nebo vašeho preferovaného IDE).

> **Tip:** Pokud dáváte přednost open‑source alternativě, stejnou logiku lze použít s **ClosedXML** – stačí nahradit třídy specifické pro Aspose třídami `XLWorkbook`, `IXLWorksheet` a `IXLTable`.

## Krok 1: Načtení sešitu Excel v C#

Prvním krokem je načíst zdrojový soubor do paměti. Načtení sešitu je pro typické velikosti tabulek levné a poskytuje vám plný přístup k listům, tabulkám a hodnotám buněk.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Proč je to důležité:* `Workbook` parsuje strukturu Open XML souboru .xlsx a poskytuje kolekci objektů `Worksheet`. Pokud soubor nelze najít, Aspose vyhodí `FileNotFoundException`, takže se ujistěte, že cesta je správná.

## Krok 2: Přístup k cílovému listu

Většina tabulek obsahuje více listů; musíte vybrat ten, který obsahuje tabulku, kterou chcete upravit. Zde používáme první list (`Worksheets[0]`), což je bezpečná výchozí volba pro jednoduché soubory.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Proč je to důležité:* `Worksheet` je kontejner pro tabulky (`ListObjects`). Přístup k správnému listu zabraňuje neúmyslným změnám v nesouvisejících datech.

## Krok 3: Odstranění řádků z tabulky Excel

Tabulky Excel jsou reprezentovány objekty `ListObject`. První tabulka na listu je `ListObjects[0]`. Metoda `DeleteRows(startIndex, rowCount)` odstraňuje řádky **relativně k datové oblasti tabulky**, nikoli k absolutním číslům řádků listu.  

V tomto příkladu odstraňujeme druhý a třetí řádek tabulky (hlavička je řádek 0, takže začínáme na indexu 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Co když má tabulka jiný název nebo pozici?

* **Pojmenovaná tabulka:** Použijte `ws.ListObjects["MyTableName]` místo indexu.
* **Více tabulek:** Projděte `ws.ListObjects` a vyberte tu, která splňuje podmínku (např. názvy sloupcových hlaviček).
* **Dynamický počet řádků:** Můžete vypočítat `rowCount` za běhu inspekcí `ws.ListObjects[0].DataRange.RowCount`.

### Ošetření okrajových případů

| Situace                              | Doporučená změna kódu                                      |
|--------------------------------------|------------------------------------------------------------|
| Tabulka je prázdná nebo má méně řádků | Zkontrolujte `ws.ListObjects[0].DataRange.RowCount` před mazáním. |
| Počet řádků k odstranění přesahuje velikost tabulky | Ořízněte `rowCount` na `DataRange.RowCount - startIndex`. |
| Potřeba odstranit řádky na základě podmínky (např. hodnota ve sloupci C) | Procházejte `DataRange.Rows` a sbírejte odpovídající indexy, poté odstraňujte v opačném pořadí, aby indexy zůstaly stabilní. |

## Krok 4: Uložení upraveného sešitu

Po odstranění zapište sešit zpět do nového souboru (nebo přepište originál, pokud chcete). Uložení vytvoří nový .xlsx, který odráží aktualizovanou tabulku.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Proč je to důležité:* `Save` serializuje reprezentaci v paměti na disk. Pokud potřebujete zachovat původní soubor, vždy zapisujte na jinou cestu.

## Kompletní, spustitelný příklad

Spojením všech kroků dohromady získáte samostatný program, který můžete zkopírovat, vložit a spustit.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Očekávaný výstup** (konzole):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Otevřete `output.xlsx` – první tabulka nyní postrádá řádky, které jste odstranili, zatímco řádek s hlavičkou zůstává nedotčen.

## Časté otázky a varianty

### Jak mohu odstranit řádky ze **všech** tabulek v sešitu?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Mohu odstranit řádky na základě **hodnoty buňky**?

Ano. Prohledejte `DataRange` pro odpovídající buňky, shromážděte jejich nulové indexy a poté odstraňujte v sestupném pořadí:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Co když potřebuji **zachovat formátování**?

`DeleteRows` odstraní celý řádek z tabulky, ale zachová styl tabulky pro zbývající řádky. Pokud potřebujete zachovat konkrétní formátování na řádku, který mažete, zkopírujte styl na jiný řádek před smazáním.

### Funguje to s **.xls** (Excel 97‑2003) soubory?

Ano. Aspose.Cells automaticky detekuje formát souboru, takže stejný kód funguje s `.xls`. Stačí změnit příponu souboru v konstruktoru `Workbook`.

## Tipy pro výkon

* **Dávkové mazání:** Mazání mnoha řádků po jednom může být pomalejší. Použijte jediné volání `DeleteRows(start, count)`, pokud je to možné.
* **Vyhněte se blokování UI vlákna:** Pokud tuto funkci integrujete do desktopové aplikace, provádějte manipulaci sešitu na pozadí, aby UI zůstalo responzivní.
* **Správné uvolnění:** I když Aspose.Cells používá spravovanou paměť, zabalte `Workbook` do bloku `using`, pokud pracujete s velkými soubory, aby se prostředky uvolnily okamžitě.

## Závěr

Nyní máte kompletní, připravený příklad pro produkci, který **odstraňuje řádky z tabulky Excel** pomocí C#. Průvodce pokryl, jak **načíst sešit Excel v C#**, najít požadovaný `ListObject`, bezpečně odstranit řádky a uložit aktualizovaný soubor. S obsahem ošetření okrajových případů a tipy pro výkon můžete tento vzor přizpůsobit složitějším scénářům, jako jsou podmíněná mazání, více tabulek nebo alternativní .NET Excel knihovny.

### Další kroky

* Prozkoumejte **ClosedXML** nebo **EPPlus**, pokud dáváte přednost plně open‑source stacku.
* Kombinujte mazání řádků s **validací dat**, abyste vyčistili tabulky před importem do databáze.
* Automatizujte proces pro složku sešitu pomocí `Directory.GetFiles` a smyčky.

Neváhejte experimentovat s různými rozsahy řádků, názvy tabulek a podmíněnou logikou. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Načíst soubor Excel C# – Jak odstranit řádky a odstranit konkrétní řádky](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Jak vložit a odstranit řádky v Excelu s Aspose.Cells pro .NET: Komplexní průvodce](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Jak odstranit prázdné řádky v Excelu pomocí Aspose.Cells .NET pro čištění dat](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}