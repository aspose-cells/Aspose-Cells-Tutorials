---
category: general
date: 2026-10-26
description: Naučte se, jak importovat DataTable do listu Excel pomocí C# a Aspose.Cells,
  přičemž zachováte styly a záhlaví během několika řádků kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: cs
lastmod: 2026-10-26
og_description: jak importovat datovou tabulku do listu Excelu pomocí C# a Aspose.Cells.
  Postupujte podle tohoto kompletního návodu, abyste zachovali styly, záhlaví a formátování.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Jak importovat DataTable do listu Excel – C# krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Jak importovat DataTable do listu Excelu pomocí C#
url: /cs/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak importovat DataTable do listu Excelu pomocí C#

Pokud potřebujete **how to import datatable** do listu Excel, tento průvodce ukazuje přesné kroky v C#. Ať už vytváříte reportingový engine nebo exportujete data z gridu, uvidíte, jak zachovat záhlaví sloupců a styly buněk pomocí Aspose.Cells. Řešení funguje s .NET 6+ a vyžaduje jen několik řádků kódu.

Importování DataTable je běžný úkol při práci s tabulkami, ale vývojáři často zapomínají povolit přenos stylů nebo správně předat příznak záhlaví. V tomto tutoriálu se naučíte, jak nakonfigurovat **ImportTableOptions**, zapnout **ImportDataTableStyle** a bezpečně zavolat `ImportDataTable`. Na konci budete mít připravenou metodu, kterou můžete vložit do libovolného C# projektu.

## Požadavky

* .NET 6 SDK nebo novější nainstalováno.
* Licencovaná kopie **Aspose.Cells for .NET** (bezplatná zkušební verze funguje pro testování).
* Základní znalost `DataTable` a konceptů Excelu.
* IDE, například Visual Studio 2022 (jakýkoli editor podporující C# funguje).

Kromě `Aspose.Cells` nejsou vyžadovány žádné další balíčky NuGet.

## Krok 1: Získání zdrojových dat do DataTable

První věc, kterou uděláte, když odpovídáte na **how to import datatable**, je mít data připravená. Ve většině reálných scénářů `DataTable` pochází z databázového dotazu, CSV parseru nebo kolekce v paměti. Zde je minimální příklad, který vytvoří tabulku s několika řádky:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Proč je to důležité*: Konstrukcí `DataTable` nejprve řídíte pořadí sloupců, datové typy a názvy záhlaví – vše, co je později zachováno při importu tabulky do listu Excel.

## Krok 2: Vytvoření `ImportTableOptions` a povolení importu stylu

Když odpovídáte na **how to import datatable**, dalším rozhodnutím je, zda chcete vizuální styl (písma, barvy, okraje), který může být již definován ve zdrojovém `DataTable`. Aspose.Cells poskytuje třídu `ImportTableOptions` pro jemno‑granulární kontrolu. Nastavení `ImportDataTableStyle = true` zkopíruje informace o stylu do cílového listu.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Proč je to důležité*: Bez povolení `ImportDataTableStyle` by importované buňky používaly výchozí styl listu, čímž by se ztratilo jakékoli vlastní formátování, které jste na `DataTable` aplikovali. Tento příznak je nezbytný pro profesionální export.

## Krok 3: Import DataTable do listu, včetně záhlaví

Nyní máte vše, co potřebujete k odpovědi na **how to import datatable** do souboru Excel. Vytvoříte sešit, vyberete list a zavoláte `ImportDataTable`. Druhý argument metody (`true`) říká Aspose.Cells, aby zapsal názvy sloupců jako první řádek.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Spuštěním `ExportDataTableToExcel("Employees.xlsx")` se vytvoří soubor `Employees.xlsx`, kde první řádek obsahuje **Id**, **Name** a **Department**, a každá buňka si zachová styl definovaný v původním `DataTable`.

### Kompletní spustitelný příklad

Níže je kompletní, samostatný konzolový program, který demonstruje **how to import datatable** a uloží výsledek do aktuálního adresáře. Zkopírujte jej do nového konzolového projektu a spusťte.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Očekávaný výstup**  
Když otevřete `Employees.xlsx`, uvidíte:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Všechny buňky si zachovají výchozí styl DataTable (písmo, zarovnání). Pokud jste před importem na `DataTable` aplikovali vlastní styly, ty se v listu objeví identicky, protože `ImportDataTableStyle` je nastaven na `true`.

## Časté úskalí a tipy pro nejlepší praxi

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Chybějící záhlaví** | Předání `false` jako druhého argumentu funkci `ImportDataTable` přeskočí názvy sloupců. | Vždy použijte `true`, když potřebujete záhlaví, nebo je před importem zapište ručně. |
| **Styl nebyl přenesen** | Zapomenutí povolit `ImportDataTableStyle`. | Nastavte `ImportDataTableStyle = true` v `ImportTableOptions`. |
| **Velké tabulky způsobují zpomalení výkonu** | Importování milionů řádků bez stránkování. | Importujte po dávkách nebo použijte `ImportDataTable` s přetížením `startRow` pro streamování dat. |
| **Nesprávná reference na list** | Použití `workbook.Worksheets[1]`, když existuje pouze jeden list. | Použijte `workbook.Worksheets[0]` nebo vytvořte nový list pomocí `workbook.Worksheets.Add()`. |
| **Vypršení licence** | Zkušební verze Aspose.Cells po 30 dnech přidá vodoznak. | Aplikujte platnou licenci pomocí `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Pro tip**: Pokud potřebujete po importu použít vlastní téma, zavolejte `ws.Cells.ApplyStyle(style)`, kde `style` je objekt `Style`, který nakonfigurujete jednou a použijete napříč řádky.

## Rozšíření řešení

Nyní, když znáte **how to import datatable**, můžete prozkoumat související scénáře:

* **Importování více tabulek** – opakujte import na různých listech.
* **Podmíněné formátování** – po importu přidejte pravidla pomocí `ws.Cells.ApplyConditionalFormatting`.
* **Export do CSV** – použijte `workbook.Save("file.csv", SaveFormat.Csv)`, pokud je požadován formát prostého textu.
* **Načtení zpět do DataTable** – použijte `ws.Cells.ExportDataTable` pro ověření integrity při zpětném převodu.

Všechny tyto rozšíření staví na základním vzoru demonstrovaném výše: získat data, nakonfigurovat možnosti importu a zavolat jedinou metodu Aspose.Cells.

## Závěr

Nyní máte kompletní, připravenou odpověď pro **how to import datatable** do listu Excel pomocí C#. Tutoriál pokryl získání zdrojových dat, konfiguraci `ImportTableOptions` s `ImportDataTableStyle` a provedení importu pomocí `ImportDataTable`. Dodržením ukázkového kódu automaticky zachováte záhlaví a styly a můžete vzor přizpůsobit pro větší datové sady, více listů nebo další požadavky na formátování.

Jste připraveni automatizovat svůj reportingový workflow? Zkuste nahradit ukázkový `DataTable` skutečným databázovým dotazem, experimentujte s vlastními styly buněk a integrujte metodu do vaší existující servisní vrstvy. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak importovat pole do Excelu pomocí Aspose.Cells pro .NET&#58; průvodce krok za krokem](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [Jak importovat XML data do Excelu s Aspose.Cells pro .NET&#58; průvodce krok za krokem](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [Jak importovat HTML‑formátované DataTables do Excelu pomocí Aspose.Cells pro .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}