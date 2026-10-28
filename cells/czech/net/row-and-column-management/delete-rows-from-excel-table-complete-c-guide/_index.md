---
category: general
date: 2026-08-07
description: Odstraňte řádky z tabulky Excel pomocí C#. Naučte se, jak bezpečně odstranit
  datové řádky v Excelu a zároveň chránit hlavičkový řádek, a to během několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: cs
lastmod: 2026-08-07
og_description: Programově odstraňujte řádky z tabulky Excel. Tento průvodce vám ukáže,
  jak bezpečně odstranit datové řádky v Excelu a chránit řádek záhlaví v Excelu pomocí
  Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: Odstranit řádky z tabulky Excel – rychlé řešení v C#
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: Smazání řádků z tabulky Excel – kompletní průvodce C#
url: /cs/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete rows from Excel table – complete C# guide

Pokud potřebujete **delete rows from Excel table** v .NET projektu, tento tutoriál vám ukáže spolehlivý způsob, jak to provést. Ať už čistíte importovaná data nebo zkracujete zprávu, uvidíte, jak odstranit řádky dat v Excelu, zatímco API automaticky **protect header row excel** před neúmyslným smazáním.

V následujících krocích se naučíte, jak načíst sešit, bezpečně smazat řádky a nakonec uložit změny. Průvodce také pokrývá častou chybu pokusu o smazání řádku záhlaví a vysvětluje, proč knihovna brání jeho smazání. Na konci budete schopni **remove data rows excel** s jistotou v jakémkoli řešení založeném na Aspose.Cells.

## Prerequisites

- .NET 6.0 nebo novější nainstalováno.
- **Aspose.Cells for .NET** NuGet balíček (verze 23.10 nebo novější). Nainstalujte jej pomocí:

  ```bash
  dotnet add package Aspose.Cells
  ```

- Excel soubor (`TableWithHeader.xlsx`) obsahující strukturovanou tabulku s řádkem záhlaví v první listu.
- Základní znalost C# a Visual Studio (nebo libovolného IDE, které preferujete).

## Step 1: Load the workbook containing a table with a header row

Prvním krokem je otevřít sešit, který obsahuje tabulku, kterou chcete upravit. Aspose.Cells načte soubor do paměti, aniž by bylo potřeba mít nainstalovaný Excel.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**Proč je to důležité:** Načtení sešitu vytvoří objekt `Workbook`, který vám poskytuje přístup k listům, tabulkám a buňkám. Bez tohoto objektu nemůžete manipulovat se strukturou Excelu.

## Step 2: Access the first worksheet and its first table

Většina jednoduchých příkladů umisťuje tabulku do prvního listu a na index 0, ale můžete indexy upravit podle svého scénáře.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**Proč je to důležité:** `ListObject` představuje Excel tabulku, která zahrnuje řádek záhlaví, datové řádky a jakékoli formátování. Práce s objektem tabulky zajišťuje, že respektujete semantiku tabulek v Excelu, například ochranu řádku záhlaví.

## Step 3: Attempt to delete the header row (demonstrating protection)

Aspose.Cells vyvolá výjimku, pokud se pokusíte smazat řádek záhlaví, protože API **protect header row excel** je navrženo tak, aby jej chránilo. Zobrazení tohoto chování vám pomůže pochopit, proč přímé smazání selže.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**Expected output**

```
Deletion prevented: Cannot delete the header row of a table.
```

**Vysvětlení:** Metoda `DeleteRows` přijímá nulovým indexem počáteční index a počet. Index 0 ukazuje na řádek záhlaví, který knihovna chrání, aby zachovala strukturu tabulky.

## Step 4: Delete data rows only – the correct way to **remove data rows excel**

Nyní, když víte, že řádek záhlaví je chráněn, smažte pouze datové řádky, které začínají za záhlavím. Ve většině tabulek je první datový řádek na indexu 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**Proč to funguje:** Začátkem na indexu 1 přeskočíte řádek záhlaví, takže operace splňuje pravidlo **protect header row excel**. Metoda `DeleteRows` automaticky aktualizuje interní rozsah tabulky.

## Step 5: Save the modified workbook

Uložte změny do nového souboru, aby originál zůstal nedotčen.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**Výsledek:** Po spuštění programu obsahuje `TableHeaderProtected.xlsx` stejný řádek záhlaví, ale určené datové řádky jsou odstraněny. Otevření souboru v Excelu ukazuje čistou tabulku bez odstraněných řádků.

## Common pitfalls and how to avoid them

| Problém | Proč k tomu dochází | Řešení |
|---------|---------------------|--------|
| Snažíte se smazat řádek záhlaví | Aspose.Cells vynucuje integritu tabulky | Vždy začněte mazání na indexu 1 nebo vyšším |
| Mazání více řádků, než existuje | `DeleteRows` vyvolá `ArgumentOutOfRangeException` | Zkontrolujte `table.DataRange.RowCount` před voláním `DeleteRows` |
| Práce s rozsahem, který není tabulkou | `ListObject` metody platí jen pro strukturované tabulky | Převést rozsah na tabulku nejprve (`worksheet.Tables.Add`), pokud je potřeba |

**Tip:** Pokud potřebujete vymazat celou tabulku, ale zachovat záhlaví, použijte `table.DeleteRows(1, table.DataRange.RowCount - 1);`. Tím se odstraní každý datový řádek bez ohledu na to, kolik řádků tabulka aktuálně obsahuje.

## Alternative: Deleting rows by cell address

Někdy můžete znát přesnou adresu buňky místo indexu řádku. Adresu můžete převést na index řádku pomocí kolekce `Cells`:

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

Tento přístup je užitečný, když jsou řádky k odstranění identifikovány podle obsahu místo pevného počtu.

## Testing your implementation

1. Spusťte program s ukázkovým sešitem, který obsahuje alespoň pět datových řádků.  
2. Ověřte, že konzole vypíše “Rows deleted and workbook saved successfully.”  
3. Otevřete `TableHeaderProtected.xlsx` v Excelu a potvrďte:
   - Řádek záhlaví je stále přítomen.
   - Chybí pouze zamýšlené datové řádky.

Pokud řádek záhlaví zmizí, pravděpodobně jste zahájili mazání na indexu 0 — zkontrolujte **Krok 4**.

## Conclusion

Nyní víte, jak bezpečně **delete rows from Excel table** pomocí C#. Průvodce pokryl načtení sešitu, přístup k tabulce, dodržení pravidla **protect header row excel**, správné **remove data rows excel** a uložení výsledku. Dodržením těchto kroků se vyhnete častým chybám a udržíte své Excel tabulky dobře strukturované.

### Next steps

- Prozkoumejte funkce **Aspose.Cells**, jako je vkládání řádků, aplikování stylů nebo filtrování dat.
- Kombinujte mazání řádků s **Excel formuláři** pro automatizaci úklidu na základě výsledků výpočtů.
- Podívejte se na související témata, jako je **export Excel do CSV** nebo **efektivní čtení velkých sešitů**.

Neváhejte experimentovat s různým počtem řádků, více tabulkami nebo podmíněným mazáním. Pokud narazíte na okrajové případy, vraťte se k ošetření chyb ukázanému v **Krok 3** — knihovna vždy ochrání řádek záhlaví za vás. Šťastné programování!

## What Should You Learn Next?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Odstranění více řádků v Excelu pomocí Aspose.Cells .NET: Kompletní průvodce pro manipulaci s daty](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Jak vkládat a mazat řádky v Excelu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Jak odstranit prázdné řádky v Excelu pomocí Aspose.Cells .NET pro čištění dat](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}