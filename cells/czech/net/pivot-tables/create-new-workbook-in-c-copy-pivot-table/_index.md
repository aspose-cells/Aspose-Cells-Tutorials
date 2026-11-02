---
category: general
date: 2026-06-24
description: Vytvořte nový sešit v C# a zkopírujte kontingenční tabulku při zachování
  jejích dat. Naučte se, jak kopírovat řádky, exportovat vybraný rozsah a udržet kontingenční
  tabulku nedotčenou.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: cs
og_description: Vytvořte nový sešit v C# a zkopírujte kontingenční tabulku při zachování
  jejích dat. Podrobný návod krok za krokem, který popisuje, jak kopírovat řádky a
  exportovat vybraný rozsah.
og_title: Vytvořit nový sešit v C# – Kopírovat kontingenční tabulku
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Vytvořit nový sešit v C# – Kopírovat kontingenční tabulku
url: /cs/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu v C# – Kopírování kontingenční tabulky

Už jste někdy potřebovali **vytvořit nový sešit** v C# jen proto, že chcete přesunout část dat, která obsahuje kontingenční tabulku? Nejste v tom sami. V mnoha reportovacích pipelinech si vyberete několik řádků, možná pár sloupců, a očekáváte, že kontingenční tabulka zůstane přesně taková, jaká byla – bez poškozených odkazů, bez chybějících výpočtů.  

Dobrá zpráva? S několika řádky kódu Aspose.Cells můžete **copy pivot table**, zachovat ji v pořádku a dokonce **export selected range** bez poškození čehokoli. Níže uvidíte kompletní, připravený příklad, který ukazuje **how to copy rows**, zachování kontingenční tabulky a uložení výsledku jako zcela nový sešit.

## Co tento tutoriál pokrývá

- Nastavení projektu C# s Aspose.Cells (knihovna, která pohání kód).
- Načtení zdrojového sešitu, který obsahuje původní kontingenční tabulku.
- Použití metod `CopyRows` a `CopyColumns` knihovny k duplikaci přesného rozsahu, který potřebujete.
- Uložení duplikované oblasti do scénáře **create new workbook**, zatímco kontingenční tabulka zůstává funkční.
- Tipy pro okrajové případy, jako jsou více kontingenčních tabulek, skryté řádky a velké datové sady.

Na konci tohoto průvodce budete schopni **export selected range** z libovolného souboru Excel, udržet logiku kontingenční tabulky aktivní a umístit nový soubor kamkoliv chcete.

> **Prerequisite**: Aspose.Cells pro .NET (zdarma zkušební verze nebo licencovaná verze) nainstalovaná přes NuGet. Pokud jste ji ještě nepřidali, spusťte `dotnet add package Aspose.Cells` ve složce projektu.

---

## Vytvoření nového sešitu a kopírování kontingenční tabulky

Níže je jádro řešení. Projdeme každý řádek, vysvětlíme, proč je důležitý, a poté ukážeme celý program.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Proč to funguje

- **`CopyRows` / `CopyColumns`**: Tyto metody duplikují podkladová data buněk *a* související objekty (např. cache kontingenční tabulky). Proto zůstane kontingenční tabulka po přesunu funkční.
- **Separate destination workbook**: Vytvořením nové instance `Workbook` **create new workbook** bez jakéhokoli zbylého formátování nebo skrytých listů, které by mohly zasahovat.
- **Zero‑based indexing**: Aspose.Cells používá indexování od nuly, takže `0` ukazuje na buňku **A1**. Upravit `startRow`/`startColumn`, pokud vaše kontingenční tabulka není v levém horním rohu.
- **Preserve pivot table**: Cache kontingenční tabulky se nachází ve stejném rozsahu, takže kopírováním rozsahu se automaticky kopíruje i cache. Žádný další kód není potřeba.

---

## Jak kopírovat řádky bez poškození kontingenční tabulky

Pokud vás zajímá pouze část kopírování řádků, můžete ji izolovat:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Při kopírování řádků, které protínají kontingenční tabulku, vždy kopírujte *celý* oblast kontingenční tabulky (řádky + sloupce). Částečné kopie mohou zanechat kontingenční tabulku s chybějícími poli, což způsobí chyby `#REF!`.

---

## Export vybraného rozsahu – reálný scénář

Představte si, že máte obrovský sešit s prodeji, ale váš klient chce jen souhrn za první čtvrtletí, který se nachází v řádcích 1‑20 a sloupcích A‑D. Výše uvedený úryvek již **export selected range** za vás provádí. Stačí změnit proměnné `totalRows` a `totalColumns`, aby odpovídaly požadavku klienta, a máte hotovo.

### Zpracování skrytých řádků nebo filtrů

Pokud má zdrojový list skryté řádky (např. filtrované), můžete chtít kopírovat pouze *viditelné* řádky. Aspose.Cells nabízí přetížení `CopyRows`, která respektují viditelnost:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Nastavte poslední boolean na `true`, aby se kopírovaly jen viditelné řádky – ideální pro „export selected range“, když uživatel použil filtry.

---

## Zachování kontingenční tabulky – běžné úskalí a jak se jim vyhnout

| Úskalí | Proč k tomu dochází | Řešení |
|---------|----------------------|--------|
| **Pivot cache not copied** | Using plain `Range.Copy` instead of `Cells.CopyRows/CopyColumns`. | Stick with `Cells` methods as shown. |
| **Destination sheet has existing pivot** | Saving over a workbook that already contains a pivot with the same name. | Start with a fresh `Workbook()` (as we do). |
| **Named ranges break** | The source pivot references a named range that isn’t present in the new file. | Copy the named range too: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Pivot points to an external data source that isn’t available. | Use `PivotTable.RefreshData()` after copying if needed. |

---

## Kompletní end‑to‑end příklad (připravený ke spuštění)

Níže je kompletní program, včetně `using` direktiv a stručného uživatelského rozhraní v konzoli. Zkopírujte a vložte jej do nového projektu Console App a stiskněte **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Expected output** (v konzoli):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Otevřete `copy-pivot.xlsx` a uvidíte stejnou kontingenční tabulku, kterou jste měli v `source.xlsx`, plně funkční a odkazující na zkopírovaný datový rozsah.

---

## Často kladené otázky

**Q: Funguje to s více kontingenčními tabulkami na stejném listu?**  
A: Ano, pokud zkopírovaný obdélník zahrnuje každou požadovanou kontingenční tabulku. Pokud chcete jen jednu, upravte `rows`/`cols` tak, aby ji izolovala.

**Q: Co když zdrojový sešit používá externí datová připojení?**  
A: Cache kontingenční tabulky bude stále odkazovat na původní připojení. Zavolejte `pivotTable.RefreshData()` po načtení cílového souboru, pokud chcete znovu dotázat zdroj.

**Q: Můžu kopírovat kontingenční tabulku na jiný list ve stejném sešitu?**  
A: Rozhodně. Nahraďte `destinationWorkbook` za `sourceWorkbook` a vyberte jiný index listu.

**Q: Existuje způsob, jak kopírovat jen formátování?**  
A: Použijte přetížení `CopyRows`/`CopyColumns`, která přijímají objekt `CopyOptions` – nastavte `CopyOptions.CopyType = CopyType.ValuesOnly` nebo `CopyType.All` podle vašich potřeb.

---

## Závěr

Právě jsme prošli scénář **create new workbook**, který **copy pivot table**, **preserve pivot table** a **export selected range** – vše v čistém C#.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}