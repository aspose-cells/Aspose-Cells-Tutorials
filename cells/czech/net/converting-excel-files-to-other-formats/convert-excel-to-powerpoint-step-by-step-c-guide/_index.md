---
category: general
date: 2026-03-01
description: Rychle převádějte Excel do PowerPointu pomocí C#. Naučte se, jak v několika
  řádcích kódu vygenerovat PowerPoint z Excel sešitu pomocí Aspose.Cells.
draft: false
keywords:
- convert excel to powerpoint
- generate powerpoint from excel
- convert xlsx to pptx
- how to convert excel
- create pptx from excel
language: cs
og_description: Převod Excelu do PowerPointu v C#. Tento průvodce vám ukáže, jak vytvořit
  PowerPoint ze souboru Excel pomocí Aspose.Cells, s kompletním kódem a tipy.
og_title: Převod Excelu do PowerPointu – kompletní C# tutoriál
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
title: Převod Excelu do PowerPointu – krok za krokem průvodce v C#
url: /cs/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod Excelu do PowerPointu – krok za krokem průvodce v C#

Už jste někdy potřebovali **převést Excel do PowerPointu**, ale nebyli jste si jisti, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku, když se snaží převést datově bohaté tabulky na prezentace připravené k předvedení.  

Dobrou zprávou je, že s několika řádky C# můžete **vytvořit PowerPoint z Excelu** automaticky, bez nutnosti ručního kopírování a vkládání. V tomto tutoriálu projdeme celý proces, od načtení souboru `.xlsx` až po uložení vylepšeného `.pptx`, který můžete otevřít v Microsoft PowerPoint nebo v jakémkoli kompatibilním prohlížeči.

> **Co získáte:** spustitelný program, který načte Excel sešit, nastaví možnosti uložení PowerPointu a zapíše soubor PowerPoint — vše pomocí knihovny Aspose.Cells.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód funguje také na .NET Framework 4.7+).  
- **Aspose.Cells for .NET** – můžete jej získat z NuGet (`Install-Package Aspose.Cells`).  
- Základní znalost C# (nic složitého, jen běžné `using` příkazy).  
- Soubor Excel (`input.xlsx`), který chcete převést na sadu snímků  

To je vše. Žádné další nástroje třetích stran, žádné COM interop, žádná složitá automatizace PowerPointu. Ponořme se do toho.

![Pracovní postup převodu Excelu do PowerPointu](convert-excel-to-powerpoint.png "Převod Excelu do PowerPointu")

*Alt text: Diagram pracovního postupu převodu Excelu do PowerPointu*

## Převod Excelu do PowerPointu pomocí Aspose.Cells

### Krok 1 – Načtení Excel sešitu

Prvním krokem je načíst tabulku do paměti. Aspose.Cells to usnadňuje pouhým voláním konstruktoru `Workbook` a předáním cesty k souboru.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the Excel workbook
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
```

**Proč je to důležité:** Načtení sešitu nám poskytuje přístup ke každému listu, grafu a dokonce i vloženým obrázkům. Odtud můžeme rozhodnout, co zachovat a co zahodit před konverzí.

### Krok 2 – Nastavení možností uložení prezentace

Aspose.Cells podporuje více výstupních formátů a pro PowerPoint používáme `PresentationSaveOptions`. Tento objekt nám umožňuje nastavit cílový `SaveFormat.Pptx` a upravit několik užitečných nastavení, například zda vložit makra nebo zachovat původní šířky sloupců.

```csharp
            // Step 2: Set up presentation save options for PowerPoint format
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                // Optional: keep the original Excel formatting as much as possible
                // (true by default, but we set it explicitly for clarity)
                KeepOriginalFormatting = true
            };
```

**Proč je to důležité:** Bez správných možností by výsledné snímky mohly vypadat stlačeně nebo ztratit stylování. Tím, že řekneme Aspose.Cells, že chceme skutečný soubor PPTX, zajistíme, že konverze respektuje rozvržení Excelu.

### Krok 3 – Uložení sešitu jako PowerPoint prezentace

Nyní se děje magie. Jediné volání `Save` zapíše soubor `.pptx`, který odráží první list sešitu (nebo všechny listy, v závislosti na verzi knihovny). Pro většinu scénářů stačí první list, ale později můžete experimentovat.

```csharp
            // Step 3: Save the workbook as a PowerPoint presentation
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"Success! '{outputPath}' has been created.");
        }
    }
}
```

**Co uvidíte:** Otevřete `output.pptx` v PowerPointu a zjistíte, že každý list byl převeden na snímek. Textové buňky se stanou textovými poli, grafy se změní na nativní PowerPoint grafy a i obrázky zachovají původní rozlišení.

## Vytvoření PowerPointu z Excelu – tipy pro nastavení projektu

- **Instalace přes NuGet:** Spusťte `dotnet add package Aspose.Cells` ve složce projektu. Tím se stáhne nejnovější stabilní verze (k březnu 2026, verze 23.10).  
- **Cílová platforma:** Pokud používáte .NET Core, ujistěte se, že váš `csproj` obsahuje `<TargetFramework>net6.0</TargetFramework>`.  
- **Cesty k souborům:** Používejte `Path.Combine` pro bezpečnost napříč platformami, zejména pokud váš kód běží v Linux kontejnerech.  

```csharp
using System.IO;

// Example of safe path building
string baseDir = AppDomain.CurrentDomain.BaseDirectory;
string inputPath = Path.Combine(baseDir, "input.xlsx");
string outputPath = Path.Combine(baseDir, "output.pptx");
```

## Převod Xlsx na Pptx – práce s více listy

Ve výchozím nastavení Aspose.Cells převádí **pouze aktivní list**. Pokud potřebujete snímek pro každý list, můžete projít kolekci a uložit každý zvlášť:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet sheet = workbook.Worksheets[i];
    sheet.IsSelected = true; // Make this sheet the active one
    string slidePath = Path.Combine(baseDir, $"Slide_{i + 1}.pptx");
    workbook.Save(slidePath, saveOptions);
}
```

**Tip:** Po každé iteraci zavolejte `workbook.Worksheets[i].IsSelected = false`, pokud plánujete znovu použít stejný objekt `Workbook` pro další operace.

## Jak převést Excel – práce s velkými soubory

Velké sešity (stovky megabajtů) mohou zatížit paměť. Několik triků udrží proces plynulý:

1. **Povolit streamování:** `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` nutí Aspose.Cells používat dočasné soubory místo načítání všeho do RAM.  
2. **Přeskočit prázdné řádky/sloupce:** Nastavte `saveOptions.IgnoreEmptyRows = true`, aby se snížil nepořádek na snímcích.  
3. **Změnit velikost obrázků:** Pokud váš Excel obsahuje obrázky s vysokým rozlišením, můžete je před konverzí zmenšit pomocí `ImageResizeOptions`.  

```csharp
workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;
saveOptions.IgnoreEmptyRows = true;
saveOptions.ImageResizeOptions = new ImageResizeOptions
{
    Width = 1024,
    Height = 768,
    ResizeMode = ResizeMode.Proportional
};
```

## Vytvoření Pptx z Excelu – ověření výsledku

Po dokončení volání `Save` budete chtít ověřit, že soubor je použitelný:

```csharp
if (File.Exists(outputPath))
{
    var fileInfo = new FileInfo(outputPath);
    Console.WriteLine($"File size: {fileInfo.Length / 1024} KB");
    // Optionally launch PowerPoint automatically (Windows only)
    System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
    {
        FileName = outputPath,
        UseShellExecute = true
    });
}
else
{
    Console.Error.WriteLine("Something went wrong – the PPTX was not created.");
}
```

Po otevření souboru by se měla zobrazit sada snímků, která odráží rozvržení původní tabulky, včetně grafů, tabulek a všech vložených obrázků.

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| *Mohu zachovat makra v Excelu?* | Ne. PowerPoint nepodporuje VBA makra z Excelu. Budete muset jakoukoli automatizaci vytvořit znovu přímo v PowerPointu. |
| *Co s komentáři buněk?* | Převádějí se na samostatná textová pole na snímku, ale můžete je skrýt nastavením `saveOptions.IncludeCellComments = false`. |
| *Vyhodnocují se vzorce?* | Ano — Aspose.Cells vyhodnocuje vzorce před konverzí, takže snímek zobrazuje vypočtené hodnoty, nikoli samotné vzorce. |
| *Existuje způsob, jak přizpůsobit design snímků?* | Po konverzi můžete použít šablonu PowerPointu pomocí třídy `Presentation` z Aspose.Slides a poté do ní zkopírovat vygenerované snímky. |

## Kompletní funkční příklad (veškerý kód na jednom místě)

```csharp
using Aspose.Cells;
using System;
using System.IO;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build safe file paths
            string baseDir = AppDomain.CurrentDomain.BaseDirectory;
            string inputPath = Path.Combine(baseDir, "input.xlsx");
            string outputPath = Path.Combine(baseDir, "output.pptx");

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Optional: improve memory usage for huge files
            workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;

            // Configure PowerPoint save options
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                KeepOriginalFormatting = true,
                IgnoreEmptyRows = true,
                ImageResizeOptions = new ImageResizeOptions
                {
                    Width = 1024,
                    Height = 768,
                    ResizeMode = ResizeMode.Proportional
                }
            };

            // Save as PowerPoint
            workbook.Save(outputPath, saveOptions);

            // Verify the result
            if (File.Exists(outputPath))
            {
                Console.WriteLine($"Success! '{outputPath}' created ({new FileInfo(outputPath).Length / 1024} KB).");
                // Open the file automatically (Windows only)
                System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            else
            {
                Console.Error.WriteLine("Failed to create the PowerPoint file.");
            }
        }
    }
}
```

Spusťte program a získáte zcela nový soubor `.pptx`, připravený pro další schůzku s klientem, prezentaci v zasedací místnosti nebo interní briefing.

## Závěr

Nyní víte **jak převést Excel do PowerPointu** pomocí C# a Aspose.Cells. Základní kroky — načtení sešitu, nastavení `PresentationSaveOptions` a volání `Save` — jsou jednoduché, přičemž tutoriál také pokrýval nuance **vytvoření PowerPointu z Excelu** jako například správu paměti,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}