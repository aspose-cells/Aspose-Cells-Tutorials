---
category: general
date: 2026-05-30
description: Jak používat AutoFilter v automatizaci Excelu v C#. Naučte se, jak vytvořit
  sešit Excel, filtrovat řádky podle hodnoty a zefektivnit své úkoly v tabulce.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: cs
og_description: Jak používat AutoFilter v automatizaci Excelu v C#. Ovládněte tvorbu
  sešitu Excel, filtrování řádků podle hodnoty a automatizaci tabulek s lehkostí.
og_title: Jak používat AutoFilter v automatizaci Excelu v C# – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Jak použít AutoFilter v automatizaci Excelu v C# – Kompletní krok‑za‑krokem
  průvodce
url: /cs/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat AutoFilter v C# Excel automatizaci – Kompletní průvodce

Už jste se někdy zamysleli **jak používat AutoFilter**, když generujete soubory Excel z C# kódu? Nejste sami – mnoho vývojářů narazí na tento problém, když potřebují skrýt řádky, které neodpovídají určitému kritériu.  

V tomto tutoriálu projdeme konkrétní, spustitelný příklad, který **vytvoří Excel sešit**, přidá tabulku a poté **filtrování řádků podle hodnoty** ve sloupci B. Na konci budete mít čistý, znovupoužitelný úryvek, který můžete vložit do libovolného C# projektu, který potřebuje Excel automatizaci.

## Co se naučíte

- Nastavení C# projektu s knihovnou Aspose.Cells (nebo Microsoft.Office.Interop).  
- **Vytvoření Excel sešitu** programově a přidání stylované tabulky.  
- Použití **AutoFilter** k zobrazení pouze řádků, kde **sloupec B** odpovídá konkrétnímu řetězci.  
- Kompletní odstranění filtru a obnovení celého datasetu.  
- Tipy pro řešení okrajových případů, jako jsou chybějící sloupce nebo více kritérií filtru.

Žádná předchozí zkušenost s Excel‑VBA není vyžadována; stačí základní znalost C# a NuGet balíčků.

---

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| .NET 6.0 nebo novější (nebo .NET Framework 4.7+) | Moderní runtime poskytuje lepší výkon a jednodušší správu balíčků. |
| Aspose.Cells for .NET (nebo Microsoft.Office.Interop.Excel) nainstalovaný přes NuGet | Tato knihovna poskytuje objekty `Workbook`, `Worksheet` a `Table`, které jsou použity v kódu. |
| Editor kódu (Visual Studio, VS Code, Rider, atd.) | Budete potřebovat zkompilovat a spustit příklad. |
| Základní znalost C# | Tutoriál vysvětluje *proč* každá řádka existuje, ne jen *co* dělá. |

Můžete nainstalovat Aspose.Cells pomocí:

```bash
dotnet add package Aspose.Cells
```

---

## Jak používat AutoFilter s Aspose.Cells v C#

Níže je kompletní, samostatný program. Uložte jej jako `Program.cs` v konzolovém projektu a spusťte – v výstupní složce se vytvoří soubor `FilteredWorkbook.xlsx`.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Jak kód funguje

1. **Vytvoření sešitu** – `new Workbook()` vám dává čistý soubor; `Worksheets[0]` získá výchozí list.  
2. **Naplnění ukázkových dat** – Zapíšeme malý dataset, abyste viděli filtr v akci.  
3. **Přidání tabulky** – `ListObjects.Add` převádí rozsah na Excel tabulku, která automaticky podporuje filtrování a stylování.  
4. **Použití AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` říká enginu: „Zobraz jen řádky, kde druhý sloupec (B) je roven *Apple*.“  
5. **Ukládání souborů** – Vytvoří se dva soubory: jeden filtrovaný, druhý s odstraněným filtrem, což dokazuje, že `RemoveAutoFilter()` funguje podle očekávání.

> **Pro tip:** Pokud potřebujete filtrovat podle více kritérií (např. “Apple” *nebo* “Banana”), použijte přetížení `Filter(int columnIndex, string criteria1, string criteria2)` nebo předávejte pole řetězců.

---

## Filtrování řádků podle hodnoty – Běžné varianty

Zatímco výše uvedený příklad se zaměřuje na **filtr sloupce B**, můžete chtít filtrovat jiné sloupce nebo použít číselná kritéria. Zde je rychlý cheat sheet:

| Požadovaný filtr | Ukázka kódu |
|----------------|--------------|
| Textová shoda ve sloupci C | `table.AutoFilter.Filter(2, "Cherry");` |
| Čísla větší než 10 ve sloupci C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Více hodnot ve sloupci B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Okrajový případ:** Pokud je název sloupce překlep nebo je index sloupce mimo rozsah, Aspose.Cells vyhodí `ArgumentException`. Chraňte se tím, že před aplikací filtru zkontrolujete `table.ListColumns.Count`.

---

## Odstranění AutoFilter – Kdy resetovat

Někdy potřebujete znovu zobrazit celý dataset (např. po vymazání vyhledávacího pole uživatelem). Volání `table.RemoveAutoFilter()` to zařídí jedním řádkem. Pokud používáte Microsoft.Office.Interop, zavoláte `worksheet.AutoFilterMode = false;`.

---

## Kompletní funkční příklad – shrnutí

Níže je *celý* program znovu, bez komentářů pro ty, kteří preferují stručný pohled:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Po spuštění získáte dva soubory:

- **FilteredWorkbook.xlsx** – viditelné jen řádky s *Apple*.  
- **UnfilteredWorkbook.xlsx** – původní data obnovena.

---

## Často kladené otázky

**Q: Funguje to se staršími soubory .xls?**  
A: Ano. Aspose.Cells může ukládat jak do `.xlsx`, tak do `.xls` změnou přípony souboru nebo použitím `SaveOptions`.

**Q: Co když potřebuji filtrovat *po* uložení sešitu?**  
A: Načtěte soubor pomocí `new Workbook("path.xlsx")`, aplikujte filtr a poté znovu `Save`.

**Q: Můžu použít filtr na *rozsah*, který není tabulkou?**  
A: Rozhodně. Použijte `worksheet.AutoFilter.Range = "A1:C5";` a pak `worksheet.AutoFilter.ApplyFilter();`. Tabulky však poskytují vestavěné stylování a jednodušší odkazování na sloupce.

---

## Image – Visual Confirmation

![Screenshot showing AutoFilter applied to column B in an Excel workbook created with C#](/images/autofilter-column-b.png "AutoFilter on column B")

*(Obrázek ilustruje filtrovaný pohled, kde zůstávají jen řádky obsahující “Apple”.)*

---

## Závěr

Právě jsme prošli **jak používat AutoFilter** v scénáři C#‑driven Excel automatizace, od **vytvoření Excel sešitu** po **filtrování řádků podle hodnoty** ve **sloupci B**, a nakonec **odstranění filtru**, když již není potřeba. Základní kroky – inicializace, přidání tabulky, aplikace filtru a úklid – jsou znovupoužitelné v jakémkoli projektu, který potřebuje **excel automation c#**.

Připravený na další výzvu? Zkuste:

- Přidání podmíněného formátování pro zvýraznění filtrovaných řádků.  
- Export filtrovaných dat do CSV pro další zpracování.  
- Kombinování více filtrů (např. “Apple” *a* množství > 8).

Experimentujte, rozbíjejte věci a pak je opravujte—

## Co byste se měli naučit dál?

- [Jak implementovat AutoFilter v Excelu pomocí Aspose.Cells pro .NET (průvodce analýzou dat)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Jak použít Autofilter Not Contains v Aspose.Cells .NET pro analýzu dat v Excelu](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Jak implementovat Excel Autofilter 'EndsWith' pomocí Aspose.Cells pro .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}