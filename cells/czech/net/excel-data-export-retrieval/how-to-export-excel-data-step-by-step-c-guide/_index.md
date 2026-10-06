---
category: general
date: 2026-03-29
description: Naučte se, jak exportovat tabulky Excel do prostého textu, zapisovat
  řetězec do souboru a převádět tabulku Excel do CSV nebo TXT pomocí C#. Obsahuje
  kompletní kód a tipy.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: cs
og_description: Jak exportovat tabulky Excel do textových souborů v C#. Získejte kompletní
  řešení, kód a osvědčené postupy pro převod tabulek Excel a ukládání souborů TXT.
og_title: Jak exportovat data z Excelu – kompletní C# tutoriál
tags:
- C#
- Excel
- File I/O
title: Jak exportovat data z Excelu – krok za krokem průvodce C#
url: /cs/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat data z Excelu – Kompletní průvodce C#

Už jste se někdy zamýšleli **jak exportovat data z Excelu** bez ručního otevírání sešitu? Možná potřebujete vypsat tabulku do jednoduchého textového souboru pro starý systém, nebo chcete rychlý CSV export pro datové analytické pipeline. V tomto tutoriálu vás provedeme praktickým, end‑to‑end řešením, které **zapíše řetězec do souboru** a ukáže vám přesně, jak **převést Excel tabulku** do odděleného textového formátu pomocí C#.

Probereme vše od načtení sešitu, výběru správné tabulky, nastavení možností exportu až po uložení výsledku jako souboru `.txt`. Na konci budete schopni **exportovat tabulku jako CSV** (nebo jakýkoli jiný oddělovač, který zvolíte) a uvidíte i několik užitečných triků pro **ukládání txt souborů v C#** projektech. Žádné externí nástroje nejsou potřeba – jen pár NuGet balíčků a trochu kódu.

---

## Co budete potřebovat

- **.NET 6.0+** (nebo .NET Framework 4.7.2, pokud dáváte přednost klasickému)
- **Syncfusion.XlsIO** NuGet balíček (třída `ExportTableOptions` se nachází zde)
- Základní C# IDE (Visual Studio, VS Code, Rider – jakýkoliv vám vyhovuje)
- Excel sešit, který obsahuje alespoň jednu tabulku (v příkladu použijeme `ws.Tables[0]`)

> Tip: Pokud ještě nemáte knihovnu Syncfusion, spusťte  
> `dotnet add package Syncfusion.XlsIO.Net.Core` z příkazové řádky.

---

## Krok 1 – Otevřete sešit a získejte první tabulku  

Prvním krokem je načíst Excel soubor a získat odkaz na list, který tabulku obsahuje. Tento krok je zásadní, protože operace **convert excel table** funguje na objektu `ITable`, nikoli na surových rozsazích buněk.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Proč je to důležité:* Otevření sešitu pomocí `using` zajišťuje uvolnění všech neřízených zdrojů, čímž se předejde problémům se zamčením souboru později, když se pokusíte **write string to file**.

---

## Krok 2 – Nastavte možnosti exportu (čistý text, bez hlaviček, středník jako oddělovač)  

Nyní řekneme Syncfusion, jak má být tabulka serializována. `ExportTableOptions` vám umožní zapnout nebo vypnout zahrnutí hlaviček, zvolit oddělovač a rozhodnout, zda chcete řetězec nebo pole bajtů.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Proč je to důležité:* Nastavení `IncludeHeaders = false` často odpovídá očekáváním downstream systémů, které již znají pořadí sloupců. Změna oddělovače je způsob, jak **export table as CSV** s vlastním separátorem.

---

## Krok 3 – Exportujte tabulku do řetězce  

S připravenými možnostmi zavoláme `ExportToString`. Tato metoda načte celou tabulku (včetně všech řádků) a vrátí jeden řetězec připravený k zápisu do souboru.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Proč je to důležité:* Volání `ExportToString` provádí těžkou práci převodu Excel mřížky do odděleného formátu. Respektuje nastavený `Delimiter`, takže získáte čistý **export table as csv** výstup bez dalšího zpracování.

---

## Krok 4 – Zapište exportovaný text do souboru  

Nakonec uložíme řetězec na disk. `File.WriteAllText` je nejjednodušší způsob, jak **save txt file C#**; automaticky vytvoří soubor, pokud neexistuje, a v opačném případě jej přepíše.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Proč je to důležité:* Přímým zápisem řetězce se vyhnete dalšímu kroku konverze. Soubor nyní obsahuje řádky jako `Value1;Value2;Value3`, připravené pro jakýkoli downstream parser.

---

## Kompletní funkční příklad (všechny kroky na jednom místě)  

Níže najdete kompletní, připravený ke zkopírování program, který kombinuje vše, o čem jsme mluvili. Obsahuje ošetření chyb a komentáře pro přehlednost.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup** (obsah souboru `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Každý řádek odpovídá řádku z původní Excel tabulky, hodnoty jsou odděleny středníky. Pokud změníte `Delimiter = ","`, získáte klasický CSV soubor.

---

## Často kladené otázky a okrajové případy  

### Co když má můj sešit více tabulek?  
Jednoduše změňte `ws.Tables[0]` na požadovaný index, nebo projděte `ws.Tables` v cyklu:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Jak zahrnout záhlaví sloupců?  
Nastavte `IncludeHeaders = true` v `ExportTableOptions`. To je užitečné, když downstream systém očekává řádek s hlavičkou.

### Můžu exportovat do jiného adresáře dynamicky?  
Určitě. Použijte `Path.Combine` s `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` nebo libovolnou cestu zadanou uživatelem, aby bylo řešení flexibilnější.

### Co s velkými soubory?  
U masivních tabulek zvažte streamování výstupu místo načítání celého řetězce do paměti:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Funguje to na .NET Core?  
Ano – Syncfusion.XlsIO podporuje .NET 5/6/7. Stačí odkazovat na příslušný NuGet balíček a jste připraveni.

---

## Pro tipy pro spolehlivé exporty  

- **Ověřte cestu k souboru** před zápisem. Chybějící adresář vyvolá `DirectoryNotFoundException`.  
- **Používejte `ExportAsString`** jen když tabulka pohodlně vejde do paměti; jinak využijte `ExportToStream` pro obrovské datové sady.  
- **Mějte na paměti kulturu**: pokud data obsahují čárky jako desetinné oddělovače, zvolte středník (`;`) nebo tabulátor (`\t`), aby nedošlo k chybám při parsování CSV.  
- **Zamknutí verze**: Syncfusion občas mění API signatury. Připněte verzi NuGet balíčku (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`), aby byl váš build reprodukovatelný.

---

## Závěr  

V tomto průvodci jsme ukázali **jak exportovat Excel** tabulky do čistých textových souborů pomocí C#. Načtením sešitu, nastavením `ExportTableOptions`, exportem tabulky do řetězce a následným **zapsáním řetězce do souboru** máte nyní robustní vzor pro úlohy **convert excel table**, **export table as csv** i **save txt file C#**.

Klidně experimentujte – měňte oddělovač, zahrnujte hlavičky nebo procházejte více tabulek. Stejný přístup funguje pro generování CSV reportů, napájení legacy parserů nebo prosté archivování obsahu sešitu jako lehkých textových souborů.

Máte další scénáře, které chcete řešit? Možná potřebujete **write string to file** asynchronně, nebo chcete výstup během běhu zipovat. Podívejte se na naše další tutoriály o *asynchronous file I/O in C#* a *zipping files with .NET*, abyste udrželi dynamiku.

Šťastné kódování! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}