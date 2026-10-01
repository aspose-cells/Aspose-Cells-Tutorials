---
category: general
date: 2026-03-01
description: Vytvořte nový sešit a zkopírujte list do sešitu s kontingenční tabulkou.
  Naučte se, jak exportovat kontingenční tabulku, zkopírovat list a zkopírovat kontingenční
  tabulku v C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: cs
og_description: Vytvořte nový sešit v C# a zkopírujte list do sešitu při zachování
  kontingenční tabulky. Podrobný návod krok za krokem s kompletním kódem.
og_title: Vytvořit nový sešit – Kopírovat list a kontingenční tabulku v C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Vytvořit nový sešit – Jak zkopírovat list s kontingenční tabulkou
url: /cs/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu – Kopírování listu a kontingenční tabulky v C#

Už jste někdy potřebovali **create new workbook**, který obsahuje připravenou kontingenční tabulku, aniž byste ji museli stavět od nuly? Nejste jediní. V mnoha scénářích reportování máte hlavní soubor (`src.xlsx`) s komplexní kontingenční tabulkou a chcete odeslat čistou kopii (`dest.xlsx`) klientovi nebo jinému systému. Dobrá zpráva? Můžete to udělat pouhými dvěma řádky C# — a tento průvodce vám přesně ukáže, jak.

Projdeme celý proces: načtení zdrojového sešitu, zkopírování prvního listu (který obsahuje kontingenční tabulku) a uložení jako zcela nový sešit. Na konci budete vědět **how to copy sheet**, jak **export pivot table** data, pokud je potřebujete, a také několik tipů pro okrajové případy, jako je kopírování do existujícího souboru.

## Požadavky

- .NET 6.0 nebo novější (jakákoli recentní verze funguje)
- Aspose.Cells pro .NET (bezplatná zkušební verze nebo licencovaná verze) – tato knihovna poskytuje třídu `Workbook` použitou níže.
- Zdrojový soubor Excel (`src.xlsx`), který již obsahuje kontingenční tabulku na svém prvním listu.

Pokud ještě nemáte Aspose.Cells, přidejte jej přes NuGet:

```bash
dotnet add package Aspose.Cells
```

A to je vše — žádné extra COM interop, žádný Excel nainstalovaný na serveru.

## Co tento tutoriál pokrývá

- **Create new workbook** z existujícího listu, který obsahuje kontingenční tabulku.
- **Copy worksheet to workbook** při zachování všech definic kontingenční tabulky.
- **Export pivot table** data do DataTable (volitelné).
- Běžné úskalí při použití **how to copy pivot** v různých prostředích.
- Kompletní, spustitelný příklad, který můžete vložit do konzolové aplikace.

---

## Krok 1: Načtení zdrojového sešitu (How to Copy Sheet)

Prvním krokem je otevřít sešit, který obsahuje kontingenční tabulku. Použití Aspose.Cells to usnadňuje, protože soubor načte do paměti, aniž by spouštěl Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Proč je to důležité:** Načtení souboru ověří, že kontingenční tabulka existuje, a poskytne vám přístup ke kolekci listů. Pokud je soubor poškozený, `Workbook` vyhodí jasnou výjimku, čímž vás ochrání před pozdějšími záhadnými výstupy.

## Krok 2: Kopírování listu do nového sešitu (Copy Worksheet to Workbook)

Nyní skutečně **copy worksheet to workbook**. Metoda `CopyTo` z Aspose.Cells klonuje celý list — včetně vzorců, formátování a pivot cache — do nového souboru.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Pro tip:** `CopyTo` vytvoří zcela nový sešit na pozadí, takže není potřeba vytvářet další objekt `Workbook`. To udržuje nízkou spotřebu paměti a zajišťuje, že definice kontingenční tabulky zůstane nedotčena.

## Krok 3: Ověření zkopírované kontingenční tabulky (How to Copy Pivot)

Po dokončení kopírování je dobré otevřít nový soubor a potvrdit, že kontingenční tabulka stále funguje. Můžete to provést programově nebo jen otevřít v Excelu.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

Spuštěním programu se vytiskne něco jako:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Pokud vidíte tyto hodnoty, krok **how to copy pivot** byl úspěšný.

## Krok 4: (Volitelné) Export dat kontingenční tabulky do DataTable

Někdy potřebujete surová čísla z kontingenční tabulky bez otevírání Excelu. Aspose.Cells vám umožní načíst data kontingenční tabulky do `DataTable` — ideální pro další zpracování nebo odpovědi API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Proč byste to mohli chtít:** Export vám umožní **export pivot table** obsah do databáze, JSON payloadu nebo jakéhokoli jiného formátu bez ručního kopírování‑vkládání.

## Krok 5: Okrajové případy a běžné úskalí

### Kopírování do existujícího sešitu

Pokud potřebujete **copy worksheet to workbook**, který již obsahuje jiné listy, použijte přetíženou metodu, která přijímá cílovou instanci `Workbook`:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Zachování externích zdrojů dat

Kontingenční tabulky, které čerpají z externích připojení (např. Power Query), mohou po kopírování ztratit odkaz. V takových případech nastavte `pivot.RefreshDataOnOpen = true` před uložením:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### Velké soubory a výkon

Pro soubory větší než 50 MB zvažte povolení `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;`, aby se snížil tlak na paměť.

---

![create new workbook – copying a worksheet with a pivot table](https://example.com/images/create-new-workbook.png "Create new workbook")

*Text obrázku: create new workbook – copying a worksheet with a pivot table*

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní, připravená ke spuštění konzolová aplikace. Zkopírujte a vložte ji do nového `.csproj` a stiskněte **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Očekávaný výsledek

- `dest.xlsx` se objeví v `YOUR_DIRECTORY`.
- První list vypadá přesně jako originál, včetně kontingenční tabulky.
- Spuštěním konzole se vytisknou metadata kontingenční tabulky a malý náhled dat, což potvrzuje úspěšné kopírování.

---

## Závěr

Nyní víte, jak **create new workbook** kopírováním listu, který obsahuje kontingenční tabulku, jak **copy worksheet to workbook**, a dokonce jak **export pivot table** data pro následné zpracování. Ať už budujete reportingovou službu, automatizujete distribuci Excelu, nebo jen potřebujete rychlý způsob, jak duplikovat kontingenční tabulku, výše uvedené kroky vám poskytují spolehlivé, připravené pro produkci řešení.

**Next steps** you might explore:

- Kombinujte více listů (použijte `CopyTo` opakovaně) – ideální pro vytvoření kompletního reportu.
- Upravit nastavení obnovy pivot cache, když se změní zdrojová data.
- Použijte techniky **how to copy sheet** k duplikaci grafů, obrázků nebo VBA modulů.
- Prozkoumejte `WorkbookDesigner` z Aspose.Cells pro generování reportů založených na šablonách.

Vyzkoušejte to, upravte cesty a uvidíte, jak snadné je distribuovat čisté, připravené sešity s kontingenčními tabulkami. Máte otázky ohledně okrajových případů nebo licencování? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}