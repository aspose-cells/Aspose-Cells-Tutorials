---
category: general
date: 2026-03-18
description: Jak exportovat data z Excelu do DataTable v C# s kódem, který pracuje
  se specifickými buňkami, převádí Excel na DataTable a formátuje čísla. Naučte se
  exportovat konkrétní buňky a další.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: cs
og_description: Jak exportovat data z Excelu do DataTable v C#. Tento tutoriál ukazuje,
  jak exportovat konkrétní buňky, převést Excel na DataTable a snadno formátovat čísla.
og_title: Jak exportovat Excel do DataTable v C# – Kompletní průvodce
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Jak exportovat Excel do DataTable v C# – průvodce krok za krokem
url: /cs/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat Excel do DataTable v C# – Průvodce krok za krokem

Už jste se někdy zamysleli, **jak exportovat Excel** data do `DataTable` bez ztráty formátování? Nejste jediní – vývojáři často potřebují načíst část tabulky do paměti pro reportování, validaci nebo hromadné vkládání. Dobrá zpráva? Několika řádky C# můžete exportovat přesný rozsah (např. *A1:F11*), vynutit, aby každá buňka byla považována za řetězec, a dokonce použít vlastní formát čísel.

V tomto tutoriálu pokryjeme vše, co potřebujete vědět: od načtení sešitu, nastavení **export specific cells**, převodu rozsahu na `DataTable` a řešení okrajových případů, jako jsou prázdné řádky nebo čísla závislá na locale. Na konci budete mít znovupoužitelnou metodu, která funguje v scénářích **excel to datatable c#** v produkčním kódu.

> **Požadavky** – Budete potřebovat knihovnu Aspose.Cells pro .NET (nebo jakékoli podobné API, které nabízí `ExportDataTable`). Příklad předpokládá .NET 6+, ale koncepty platí i pro starší verze.

---

## Co se naučíte

- Jak **převést Excel na DataTable** pomocí Aspose.Cells.
- Export vlastního rozsahu (`excel range to datatable`) při zacházení se všemi hodnotami jako řetězci.
- Použití formátu čísel se dvěma desetinnými místy (`#,#00.00`) během exportu.
- Běžné úskalí (null řádky, skryté sloupce) a jak se jim vyhnout.
- Připravený k kopírování, plně spustitelný ukázkový kód.

## Požadavky a nastavení

Než se ponoříme do kódu, ujistěte se, že máte:

1. **Aspose.Cells for .NET** nainstalovaný přes NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Soubor Excel (`input.xlsx`) umístěný ve složce, na kterou můžete odkazovat, např. `YOUR_DIRECTORY/input.xlsx`.
3. Projekt cílící na .NET 6 nebo novější (příkazy `using` uvedené níže fungují ihned).

> **Tip:** Pokud používáte jinou knihovnu (např. EPPlus nebo ClosedXML), koncept zůstává stejný – načtěte sešit, vyberte rozsah a zavolejte metodu, která vrátí `DataTable`.

## Krok 1: Načtení sešitu a získání první listu

Prvním, co potřebujete, je objekt `Workbook`, který představuje váš Excel soubor. Jakmile jej máte, můžete přistupovat k libovolnému listu podle indexu nebo názvu.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Proč je to důležité:** Včasné načtení sešitu vám umožní prozkoumat jeho strukturu (skryté listy, ochrana), než se rozhodnete, které buňky exportovat. Pokud je soubor velký, zvažte použití `LoadOptions` pro streamování jen potřebných částí.

## Krok 2: Nastavení možností exportu – zacházet se všemi hodnotami jako s řetězci

Když exportujete data pro následné zpracování (např. hromadné vkládání do SQL), často chcete **konzistentní řetězcovou reprezentaci**. To později zabraňuje chybám typu.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Vysvětlení:**  
- `ExportAsString = true` říká Aspose.Cells, aby ignoroval nativní typ buňky a vrátil formátovaný text.  
- `NumberFormat = "#,##0.00"` zajistí, že čísla jako `1234.5` se stanou `"1,234.50"` – užitečné pro finanční reporty.

Pokud potřebujete původní datové typy, jednoduše nastavte `ExportAsString` na `false` a konverzi proveďte sami.

## Krok 3: Export konkrétního rozsahu (A1:F11) do DataTable

Nyní přichází jádro **export specific cells**. Metoda `ExportDataTable` přijímá indexy počátečního a koncového řádku/sloupce (nulové) a příznak pro zahrnutí hlavičky.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Co získáte:** `DataTable` s 11 řádky (včetně hlavičky) a 6 sloupci (`A`‑`F`). Všechny hodnoty jsou řetězce formátované podle `exportOptions`.

## Krok 4: Ověření výsledku – výpis do konzole

Vždy je dobré provést kontrolu výstupu, než předáte tabulku dalšímu komponentu.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Měli byste vidět něco jako:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Všimněte si, že číselné sloupce zobrazují dvě desetinná místa, přesně jak jsme určili.

## Kompletní funkční příklad (připravený ke kopírování)

Níže je kompletní program, který spojuje všechny části. Vložte jej do nového konzolového projektu, upravte cestu k souboru a spusťte – není potřeba žádná další konfigurace.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Klíčové poznatky z kódu:**

- Objekt `ExportTableOptions` je znovupoužitelný; můžete jej předat více voláním `ExportDataTable`, pokud potřebujete exportovat několik rozsahů.
- Indexování začíná na **0**, takže `A1` odpovídá `(0,0)`.
- Nastavením `includeColumnNames` na `true` se automaticky použije první řádek jako názvy sloupců – skvělé pro následné operace s `DataTable`.

## Řešení okrajových případů a časté otázky

### Co když list obsahuje skryté řádky nebo sloupce?

Aspose.Cells respektuje viditelnost ve výchozím nastavení. Pokud potřebujete exportovat skrytá data, nastavte `exportOptions.ExportHiddenRows = true` a `ExportHiddenColumns = true`.

### Můj Excel soubor obsahuje vzorce – dostanu vypočtené hodnoty?

Ano. Ve výchozím nastavení `ExportDataTable` vrací **zobrazenou hodnotu** (výsledek vzorce). Pokud chcete surový text vzorce, nastavte `exportOptions.ExportFormulas = true`.

### Jak přeskočím zcela prázdné řádky?

Po exportu můžete oříznout `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Můžu exportovat nespojitý rozsah (např. A1:B5 a D1:E5)?

Aspose.Cells nepodporuje nespojitý rozsah v jednom volání. Místo toho exportujte každý blok samostatně a poté ručně sloučte vzniklé `DataTable`.

## Tipy pro výkon

- **Znovu použijte `ExportTableOptions`** pro více exportů; vytvoření nové instance pokaždé přidává zanedbatelnou zátěž, ale kódu přidává nepořádek.
- **Streamujte velké soubory** pomocí `LoadOptions`, abyste se vyhnuli načítání celého sešitu do paměti.
- **Vyhněte se `DataTable`**, pokud potřebujete jen rychlý CSV export – `ExportDataTable` je pohodlný, ale není nejpaměťově úsporný pro obrovské listy.

## Závěr

Prošli jsme **jak exportovat Excel** data do `DataTable` při kontrole formátování, zpracování konkrétních rozsahů buněk a zajištění, že každá hodnota přijde jako řetězec. Kompletní příklad ukazuje čistý, produkčně připravený přístup, který můžete přizpůsobit pro **convert excel to datatable**, **export specific cells** nebo jakýkoli scénář **excel range to datatable**, se kterým se setkáte.

Neváhejte experimentovat: změňte rozsah, přepněte `ExportAsString` nebo přeneste `DataTable` přímo do Entity Framework pro hromadné vkládání. Možnosti jsou neomezené, jakmile máte tuto pevnou základnu.

### Další kroky a související témata

- **Import DataTable zpět do Excelu** – naučte se opačnou operaci pomocí `ImportDataTable`.
- **Hromadné vkládání DataTable do SQL Serveru** – použijte `SqlBulkCopy` pro bleskově rychlé načtení.
- **Práce s EPPlus nebo ClosedXML** – podívejte se, jak vypadá stejný úkol s alternativními knihovnami.
- **Formátování buněk při exportu** – prozkoumejte `ExportTableOptions` dále pro formáty data, vlastní nastavení kultury a další.

Máte otázky nebo jiný případ použití? Zanechte komentář a pojďme konverzaci dál. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}