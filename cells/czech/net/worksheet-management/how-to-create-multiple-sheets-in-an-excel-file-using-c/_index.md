---
category: general
date: 2026-11-25
description: Naučte se, jak vytvořit více listů v souboru Excel pomocí C#. Tento průvodce
  se zabývá ukládáním sešitu jako XLSX a řešením duplicitních názvů listů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: cs
lastmod: 2026-11-25
og_description: Vytvořte v souboru Excel více listů pomocí C#. Sledujte tento kompletní
  návod, jak uložit sešit jako XLSX a spravovat duplicitní názvy listů.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: Vytvořte více listů v souboru Excel pomocí C# – průvodce krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Jak vytvořit více listů v souboru Excel pomocí C#
url: /cs/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit více listů v souboru Excel pomocí C#

Pokud potřebujete **vytvořit více listů** v sešitu Excel z C#, tento tutoriál vám poskytne připravené řešení k okamžitému spuštění. Na konci průvodce budete mít program, který generuje hlavní list, vytváří podrobné listy pomocí smart markerů a uloží výsledek jako soubor **XLSX** — přičemž bezpečně ošetřuje **duplicitní názvy listů**.  

Také uvidíte, jak **vytvořit excel soubor c#** projekty s knihovnou Aspose.Cells, populární volbou pro server‑side automatizaci tabulek.

## Požadavky

* .NET 6.0 SDK nebo novější nainstalovaný  
* Visual Studio 2022 (nebo jakékoli IDE podporující .NET)  
* NuGet balíček **Aspose.Cells for .NET** (`Aspose.Cells`) – poskytuje třídy `Workbook`, `Worksheet` a `SmartMarkersFactory` používané v kódu.  

Balíček můžete přidat následujícím příkazem CLI:

```bash
dotnet add package Aspose.Cells
```

> **Tip:** Použijte soukromý NuGet feed nebo bezplatnou komunitní edici, pokud potřebujete jen základní funkce.

## Přehled řešení

Přístup se skládá ze čtyř logických kroků:

1. **Vytvořit nový sešit** a pojmenovat první list *Master*.  
2. **Vložit smart marker**, který říká Aspose.Cells, jak pojmenovat podrobné listy.  
3. **Zpracovat smart marker** s datovým zdrojem, který může obsahovat duplicitní názvy.  
4. **Uložit sešit** jako soubor XLSX.  

Každý krok je podrobně vysvětlen níže a kompletní zdrojový soubor je uveden na konci článku.

## Krok 1: Vytvořit nový sešit a přidat hlavní list

`Třída` `Workbook` představuje celý soubor Excel. Když ji vytvoříte bez parametrů, Aspose.Cells vytvoří výchozí sešit, který již obsahuje jeden list. Přejmenování tohoto listu na *Master* jasně vyjadřuje jeho účel.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Proč je to důležité:**  
Začátek s čistým sešitem zabraňuje zbytkovému formátování nebo skrytým listům z předchozích běhů. Pojmenování listu *Master* vám pomůže později najít smart marker a udržuje soubor čitelný pro netechnické uživatele.

## Krok 2: Vložit smart marker, který určuje názvy podrobných listů

Smart markery jsou zástupné symboly, které Aspose.Cells během běhu nahrazuje daty. Syntaxe `&=DetailSheetNewName=Detail` říká enginu, aby vytvořil nový list pro každý řádek v datovém zdroji a použil hodnotu sloupce `Detail` jako název listu.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Proč je to důležité:**  
Smart marker eliminuje potřebu psát smyčku, která ručně přidává listy. Také automaticky kopíruje rozvržení hlavního listu do každého nově vytvořeného listu, což zajišťuje konzistentní styl.

## Krok 3: Zpracovat smart marker s datovým zdrojem, který může obsahovat duplicity

Níže vytvoříme `DataTable`, která simuluje datový zdroj. Všimněte si, že sloupec *Detail* obsahuje duplicitní hodnoty (`"Report"` se vyskytuje dvakrát). Metoda `SmartMarkersFactory.Process` respektuje nastavení `AllowDuplicateSheetNames`, které je v tomto příkladu ve výchozím stavu **true**.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Důležité:** Pokud potřebujete zajistit jedinečné názvy listů, nastavte `workbook.Settings.CheckDuplicateSheetNames = true;` před zpracováním. Výchozí chování vytváří listy se stejným názvem, což Excel umožňuje, ale může být matoucí při navigaci v souboru.

## Krok 4: Uložit sešit jako soubor XLSX

Nakonec uložte vygenerovaný sešit na disk. Metoda `Save` automaticky vybere vhodný zapisovač na základě přípony souboru.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Očekávaný výsledek**

| Název listu | Obsah (první řádek) |
|------------|---------------------|
| Master     | Zástupný symbol smart markeru (žádná data) |
| Report     | Datový řádek 1 (`123.45`) |
| Summary    | Datový řádek 2 (`67.89`) |
| Report (2) | Datový řádek 3 (`101.12`) |

Druhý list *Report* je automaticky přejmenován na *Report (2)* knihovnou Aspose.Cells, aby se předešlo tvrdé chybě, přičemž stále odráží původní duplicitní záměr.

## Kompletní zdrojový kód

Zkopírujte následující soubor do konzolového projektu (`dotnet new console`) a spusťte jej. Program demonstruje kompletní workflow pro **vytvoření více listů** a **uložení sešitu xlsx** při zacházení s **duplicitními názvy listů**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Spusťte `dotnet run` ze složky projektu. Po dokončení otevřete vygenerovaný soubor a ověřte, že byly vytvořeny tři podrobné listy, přičemž dva z nich sdílejí základní název **Report**.

## Řešení okrajových případů a osvědčené postupy

| Situace | Doporučený přístup |
|-----------|----------------------|
| **Velmi velké datové sady** ( > 10 000 řádků) | Použijte `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` ke snížení zatížení paměti. |
| **Vlastní pravidla pojmenování listů** | Před voláním `Process` předzpracujte sloupec `Detail` a nahraďte nelegální znaky (`/ \ ? * [ ] :`). |
| **Potřeba skutečně jedinečných názvů** | Nastavte `workbook.Settings.CheckDuplicateSheetNames = true;` a poskytněte náhradní schéma pojmenování (např. připojit GUID). |
| **Generování PDF místo XLSX** | Po uložení zavolejte `workbook.Save("output.pdf", SaveFormat.Pdf);` – Aspose.Cells může exportovat přímo do PDF. |
| **Spuštění ve webové službě** | Zapište sešit do `MemoryStream` a vraťte jej jako stažení souboru, aby se předešlo I/O na disku. |

### Tip: znovu použít stejnou instanci `Workbook` pro více exportů

Pokud vaše aplikace vytváří několik reportů na požadavek, udržujte v paměti jediný objekt `Workbook`, vymažte jeho listy (`workbook.Worksheets.Clear();`) a opakujte kroky. Tím se vyhnete režii opakovaného načítání runtime Aspose.Cells.

## Závěr

Nyní víte, jak **vytvořit více listů** v sešitu Excel pomocí C#, jak **vytvořit excel soubor c#** s Aspose.Cells, jak spravovat **duplicitní názvy listů** a jak **spolehlivě uložit sešit xlsx**. Kompletní příklad ukazuje čistý, udržovatelný vzor, který škáluje od rychlých skriptů po služby produkční úrovně.

### Co dál?

* Prozkoumejte **podmíněné formátování** na vygenerovaných listech pro zvýraznění klíčových hodnot.  
* Použijte **Smart Markery** k automatickému naplnění tabulek, grafů nebo kontingenčních tabulek.  
* Integrujte kód do ASP.NET Core API a vraťte soubor XLSX jako stream ke stažení.  

Neváhejte experimentovat s různými datovými zdroji (JSON, XML nebo databáze) a přizpůsobit syntaxi smart markeru vašim potřebám reportování. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit Excel sešit C# – krok za krokem průvodce zápisem dat a uložením jako XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Vytvořit nový sešit v C# – přidat vzorec a uložit Excel soubor](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Vytvořit excel sešit a uložit jej do souboru v C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}