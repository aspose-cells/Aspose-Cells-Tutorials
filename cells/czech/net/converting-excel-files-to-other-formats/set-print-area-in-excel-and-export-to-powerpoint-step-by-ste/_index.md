---
category: general
date: 2026-03-22
description: Nastavte oblast tisku v Excelu a převádějte Excel do PowerPointu s editovatelnými
  tvary. Naučte se, jak opakovat řádek s názvem, vytvořit PowerPoint z Excelu a exportovat
  Excel do pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: cs
og_description: Nastavte oblast tisku v Excelu a převedete ji na snímek PowerPointu
  s editovatelnými tvary. Postupujte podle tohoto kompletního průvodce, jak opakovat
  řádek s nadpisem a exportovat Excel do PPTX.
og_title: Nastavení tiskové oblasti v Excelu – Návod na export do PowerPointu
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Nastavte tiskovou oblast v Excelu a exportujte do PowerPointu – průvodce krok
  za krokem
url: /cs/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení oblasti tisku v Excelu a export do PowerPoint – Kompletní programovací tutoriál

Už jste někdy potřebovali **set print area** v listu Excel a pak převést ten výřez na snímek PowerPoint? Nejste v tom sami. V mnoha reportovacích řetězcích je potřeba, aby se data, která se pěkně tisknou, objevila také v prezentaci, často s první řádkou opakovanou jako nadpis. Dobrá zpráva? Několika řádky C# můžete **convert excel to powerpoint**, zachovat všechny textová pole editovatelná a dokonce **repeat title row** automaticky.

V tomto průvodci projdeme vše, co potřebujete vědět: od nastavení oblasti tisku až po vytvoření souboru PPTX, který můžete upravovat přímo v PowerPointu. Na konci budete schopni **create powerpoint from excel**, exportovat výsledek jako **export excel to pptx** a znovu použít stejný kód v jakémkoli .NET projektu. Žádná magie, jen jasné kroky a kompletní, spustitelný příklad.

## Co budete potřebovat

- **.NET 6.0** nebo novější (API funguje také s .NET Framework)
- **Aspose.Cells for .NET** (knihovna, která poskytuje `Workbook`, `ImageOrPrintOptions` atd.)
- Základní C# IDE (Visual Studio, Rider nebo VS Code s rozšířením C#)
- Soubor Excel (`input.xlsx`) obsahující data, která chcete exportovat

To je vše—žádné další NuGet balíčky kromě Aspose.Cells. Pokud knihovnu ještě nepřidali, spusťte:

```bash
dotnet add package Aspose.Cells
```

Nyní jsme připraveni.

## Krok 1: Načtení sešitu – výchozí bod pro export

První věc, kterou musíte udělat, je načíst sešit, který obsahuje list, který chcete převést na snímek. Představte si sešit jako zdrojový dokument; bez něj není nic jiného důležité.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Proč je to důležité:** Načtení sešitu vám poskytuje přístup ke kolekci listů, nastavením stránky a exportnímu enginu. Pokud tento krok přeskočíte, nebudete moci nastavit **print area** ani opakovat žádné řádky.

> **Tip:** Používejte absolutní cestu během testování, poté přepněte na relativní nebo na cestu založenou na konfiguraci pro produkci.

## Krok 2: Konfigurace možností exportu – zachování editovatelných textových polí a tvarů

Při exportu do PowerPointu pravděpodobně chcete, aby byl výsledný snímek editovatelný. Aspose.Cells vám to umožní pomocí `ImageOrPrintOptions`. Nastavením `ExportTextBoxes` a `ExportShapeObjects` na `true` řeknete knihovně, aby zachovala tyto objekty jako nativní prvky PowerPointu místo jejich převodu na obrázek.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Proč je to důležité:** Pokud jste někdy potřebovali **convert excel to powerpoint** a poté ručně upravit snímek, toto nastavení vás zachrání před nutností znovu vytvářet textová pole od začátku. Také zajišťuje, že všechny tvary (např. šipky nebo grafy) zůstávají vektorovými objekty, které můžete měnit velikost.

## Krok 3: Nastavení oblasti tisku a opakování řádku s názvem

Nyní přicházíme k jádru tutoriálu: **set print area** a nastavení, aby se první řádek opakoval na každé tištěné stránce (nebo, v našem případě, na exportovaném snímku). Oblast tisku říká Excelu, které buňky mají být považovány za tisk – nebo v našem scénáři za export.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Proč je to důležité:** Omezením exportu na `A1:G20` se vyhnete načítání obrovských prázdných oblastí, což urychlí konverzi a udrží snímek přehledný. Řádek `PrintTitleRows` způsobí, že první řádek funguje jako záhlaví – přesně to, co chcete, když **repeat title row** v prezentaci.

> **Okrajový případ:** Pokud data začínají na řádku 2, upravte oblast odpovídajícím způsobem (např. `PrintTitleRows = "$2:$2"`).

## Krok 4: Uložení listu jako soubor PowerPoint

Nakonec zapíšeme snímek na disk. Metoda `Save` přijímá cílový název souboru a možnosti, které jsme dříve nakonfigurovali. Výsledkem je soubor PPTX s editovatelnými textovými poli a tvary, připravený k otevření v PowerPointu.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Co uvidíte:** Otevřete `SheetWithEditableShapes.pptx` v PowerPointu. První řádek se zobrazí jako nadpis, všechny buňky od `A1:G20` jsou vykresleny a všechny tvary, které jste přidali v Excelu, jsou stále přesouvatelné a editovatelné. Žádné rastrové obrázky – jen nativní objekty PowerPointu.

## Kompletní funkční příklad – všechny kroky dohromady

Níže je kompletní program připravený ke zkopírování a vložení. Spusťte jej jako konzolovou aplikaci nebo jej vložte do libovolného většího řešení.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Očekávaný výstup:** Po spuštění programu konzole vypíše zprávu o úspěchu a soubor PPTX se objeví na určeném místě. Otevření souboru zobrazí jeden snímek s vybranou oblastí, editovatelnými textovými poli a původními tvary.

## Často kladené otázky a úskalí

| Question | Answer |
|----------|--------|
| **Funguje to s více listy?** | Ano. Procházejte `workbook.Worksheets` a opakujte stejné kroky pro každý list, při každém změňte název výstupního souboru. |
| **Co když potřebuji exportovat více než jeden snímek?** | Zavolejte `workbook.Save` vícekrát s různými objekty `ImageOrPrintOptions`, každý nakonfigurovaný s jiným `PageSetup`, pokud je potřeba. |
| **Mohu změnit velikost snímku?** | Použijte `exportOptions.ImageFormat` k nastavení DPI, nebo upravte `sheet.PageSetup.PaperSize` před uložením. |
| **Je Aspose.Cells zdarma?** | Nabízí bezplatnou zkušební verzi s vodoznaky. Pro produkci je vyžadována licence. |
| **Co s Excelovými vzorci?** | Exportované hodnoty jsou **calculated results** v době exportu. Pokud potřebujete živé vzorce v PowerPointu, budete potřebovat jiný přístup. |

## Tipy pro plynulý pracovní postup

- **Tip:** Nastavte `Workbook.Settings.CalcMode = CalculationModeType.Automatic` před exportem, aby byly všechny vzorce aktuální.
- **Dejte si pozor na:** Velmi velké oblasti mohou způsobit tlak na paměť. Ořízněte oblast tisku na co nejmenší potřebnou oblast.
- **Tip pro výkon:** Znovu použijte jedinou instanci `ImageOrPrintOptions`, pokud exportujete mnoho listů; vytváření nové při každém exportu přidává režii.
- **Poznámka k verzi:** Výše uvedený kód cílí na Aspose.Cells 23.10 (vydáno v listopadu 2023). Pozdější verze zachovávají stejné API, ale vždy si ověřte poznámky k vydání kvůli možným nekompatibilitám.

## Závěr

Probrali jsme, jak **set print area** v listu Excel, opakovat první řádek jako nadpis a poté **export excel to pptx** při zachování editovatelných textových polí a tvarů. Stručně řečeno, nyní znáte spolehlivý způsob, jak **convert excel to powerpoint**, **repeat title row** a **create powerpoint from excel** pomocí několika řádků C#.

Jste připraveni na další krok? Zkuste automatizovat hromadnou konverzi desítek reportů nebo přidat vlastní rozvržení snímků pomocí PowerPoint SDK po exportu. Možnosti jsou neomezené – experimentujte, zkoušejte nové věci a užívejte si sílu programového generování dokumentů.

Pokud se vám tento tutoriál hodil, sdílejte ho, zanechte komentář s vlastními úpravami nebo prozkoumejte naše další návody o **export excel to pptx** a souvisejících automatizačních tématech. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}