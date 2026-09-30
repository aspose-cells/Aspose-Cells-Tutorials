---
category: general
date: 2026-03-25
description: Naučte se rychle exportovat Excel do DataTable v C#. Tento tutoriál pokrývá
  export Excelu s názvy sloupců a export dat z Excelu jako řetězec pro spolehlivé
  zpracování dat.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: cs
og_description: Exportujte Excel do DataTable v C# s názvy sloupců a konverzí na řetězec.
  Sledujte tento stručný tutoriál pro připravené řešení.
og_title: Export Excel do DataTable v C# – Kompletní průvodce
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Export Excel do DataTable v C# – průvodce krok za krokem
url: /cs/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel do DataTable v C# – krok za krokem průvodce

Už jste někdy potřebovali **export Excel do DataTable**, ale nebyli jste si jisti, které příznaky nastavit? Nejste sami – mnoho vývojářů narazí na stejnou překážku, když poprvé zkusí načíst data z tabulky do `DataTable`.  

Dobrá zpráva? V několika řádcích kódu můžete **exportovat Excel s názvy sloupců** a dokonce **exportovat data z Excelu jako řetězec**, abyste se vyhnuli problémům s nesouladem typů. Níže najdete kompletní, spustitelný příklad plus „proč“ za každým nastavením, takže jej můžete přizpůsobit libovolnému projektu bez hádání.

## Co tento tutoriál pokrývá

* Jak vytvořit sešit v paměti (není potřeba fyzický soubor).  
* Naplnění několika ukázkových řádků, abyste okamžitě viděli výsledek.  
* Konfigurace `ExportTableOptions`, aby každá buňka byla považována za řetězec.  
* Export obdélníkového rozsahu do `DataTable` při zachování prvního řádku jako názvů sloupců.  
* Ověření výstupu a vytištění prvního řádku do konzole.  

Nejsou potřeba žádné externí odkazy na dokumentaci – vše, co potřebujete, je zde. Pokud již máte soubor Excel na disku, stačí nahradit řádek vytvářející sešit za `new Workbook("path/to/file.xlsx")` a můžete pokračovat.

---

## Krok 1: Nastavte projekt a přidejte NuGet balíček Aspose.Cells

Než napíšeme jakýkoli kód, ujistěte se, že váš projekt odkazuje na **Aspose.Cells pro .NET** (knihovna, která poskytuje třídu `Workbook`). Můžete ji přidat pomocí správce balíčků NuGet:

```bash
dotnet add package Aspose.Cells
```

> **Tip:** Použijte nejnovější stabilní verzi (k březnu 2026 je to 22.12), abyste získali nejnovější opravy chyb a vylepšení výkonu.

---

## Krok 2: Vytvořte sešit a naplňte jej ukázkovými daty

Začneme zcela novým `Workbook` a zapíšeme několik řádků, abyste mohli vidět export v akci. Tento krok také ukazuje **jak exportovat excel do datatable**, když jsou zdrojová data pouze v paměti.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Proč je to důležité:* Vložením řádku s hlavičkou jako první (`A1` & `B1`) můžeme později říci exportéru, aby první řádek považoval za názvy sloupců – přesně to, co znamená **export excel s názvy sloupců**.

---

## Krok 3: Řekněte Aspose.Cells, aby každou buňku považoval za řetězec

Když exportujete číselné nebo datumové buňky, Aspose se snaží odhadnout .NET typ. To může způsobit jemné chyby, pokud váš následný kód očekává řetězce. Příznak `ExportTableOptions.ExportAsString` vynutí jednotnou konverzi na řetězec.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Proč to použít?* Představte si sloupec, který někdy obsahuje čísla a někdy text (např. „00123“ vs. „ABC“). Exportováním všeho jako řetězec se vyhnete ztrátě úvodních nul nebo vyvolání výjimek při konverzi typů.

---

## Krok 4: Exportujte požadovaný rozsah do DataTable

Nyní skutečně **exportujeme excel do datatable**. Metoda `ExportDataTable` přijímá počáteční řádek/sloupec, počet řádků/sloupců, příznak pro získání názvů sloupců a možnosti, které jsme právě vytvořili.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Co se děje pod kapotou?*  
- `startRow: 0` ukazuje na první řádek Excelu (hlavičkový řádek).  
- `exportColumnNames: true` říká Aspose, aby přenesl „Name“ a „Age“ do kolekce sloupců `DataTable`.  
- `totalRows`/`totalColumns` mohou být větší než skutečná data; přebytečné buňky se stanou prázdnými řetězci díky `ExportAsString`.

---

## Krok 5: Ověřte výsledek – vytiskněte první řádek

Rychlý výpis do konzole dokazuje, že konverze byla úspěšná a názvy sloupců jsou zachovány.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Expected output**

```
First row: Alice, 30
```

Pokud změníte ukázková data, konzole automaticky odrazí tyto změny – není potřeba žádný další kód.

---

## Často kladené otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Mohu exportovat list, který již existuje na disku?** | Ano – nahraďte `new Workbook()` za `new Workbook("myFile.xlsx")`. Zbytek kroků zůstane stejný. |
| **Co když má můj soubor Excel sloučené buňky?** | Sloučené buňky jsou rozbaleny; hodnota levé horní buňky se použije pro celý sloučený rozsah. |
| **Musím se starat o formáty čísel specifické pro kulturu?** | Ne, pokud je `ExportAsString = true`; vše přijde jako surový řetězec zobrazený v Excelu. |
| **Kolik řádků mohu exportovat najednou?** | Aspose.Cells zvládne miliony řádků, ale spotřeba paměti roste s velikostí `DataTable`. Zvažte stránkování, pokud narazíte na limity. |
| **Co se stane se skrytými sloupci?** | Skryté sloupce jsou exportovány, pokud nenastavíte `ExportHiddenColumns = false` v `ExportTableOptions`. |

---

## Bonus: Export do CSV místo DataTable

Někdy můžete upřednostňovat plochý soubor. Stejné `ExportTableOptions` lze znovu použít s `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Tento jednorázový řádek vám poskytne připravený CSV k importu a stále **exportuje data z Excelu jako řetězec**.

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Spusťte program (`dotnet run`) a uvidíte výsledek **exportu excel do datatable**, který se vytiskne do konzole. Vyměňte ukázková data, změňte `totalRows`/`totalColumns` nebo nasměrujte sešit na skutečný soubor – vše se přizpůsobí.

---

## Závěr

Nyní máte **kompletní, samostatné řešení pro export Excel do DataTable** v C#. Nastavením `ExportTableOptions.ExportAsString` zajistíte, že **exportujete data z Excelu jako řetězec**, a nastavením `exportColumnNames: true` získáte známé názvy sloupců, které očekáváte při **exportu excel s názvy sloupců**.

- Předat `DataTable` do Entity Framework nebo Dapper pro hromadné vkládání.  
- Předat ji do reportovacího enginu jako **FastReport** nebo **RDLC**.  
- Převést ji na JSON pro odpověď API (`JsonConvert.SerializeObject(table)`).

Neváhejte experimentovat – třeba zkuste exportovat větší list, nebo kombinujte toto s **jak exportovat excel do datatable** ze síťového sdílení. Vzor zůstává stejný a kód je připravený pro produkci.

![Diagram of Excel → DataTable conversion flow – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}