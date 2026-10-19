---
category: general
date: 2026-09-11
description: Zkopírujte kontingenční tabulku a exportujte Excel do PPTX pomocí Aspose.Cells.
  Naučte se generovat editovatelný PPTX a uložit sešit jako PPTX v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: cs
lastmod: 2026-09-11
og_description: Zkopírujte kontingenční tabulku a exportujte Excel do PPTX v C# pomocí
  Aspose.Cells. Vytvořte editovatelný PPTX a uložte sešit jako PPTX pomocí několika
  řádků kódu.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Zkopírovat kontingenční tabulku a exportovat Excel do PPTX – kompletní průvodce
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Zkopírovat kontingenční tabulku a exportovat Excel do PPTX pomocí Aspose.Cells
url: /cs/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zkopírujte kontingenční tabulku a exportujte Excel do PPTX pomocí Aspose.Cells

Pokud potřebujete zkopírovat kontingenční tabulku z jednoho listu do druhého a poté exportovat soubor Excel do prezentace PowerPoint, tento návod vám ukáže, jak na to. Pomocí Aspose.Cells můžete během několika řádků C# kódu vygenerovat editovatelný PPTX a uložit sešit jako PPTX.

Tutoriál pokrývá každý krok potřebný k přesunu kontingenční tabulky, zachování její funkčnosti a vytvoření souboru PPTX, kde grafy a tvary zůstávají editovatelné. Nepotřebujete žádné externí nástroje – stačí knihovna Aspose.Cells a vývojové prostředí .NET.

## Co dosáhnete

* **Zkopírovat kontingenční tabulku** ze zdrojového listu do cílového listu při zachování všech datových spojení.  
* **Exportovat Excel do PPTX**, aby výsledný snímek mohl být upravován v PowerPointu.  
* **Vytvořit editovatelný PPTX**, kde grafy, tabulky a tvary nejsou převedeny na obrázky.  
* **Uložit sešit jako PPTX** pomocí stejného volání API Aspose.Cells.  

### Požadavky

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+).  
* Aspose.Cells pro .NET (NuGet balíček `Aspose.Cells`).  
* Základní znalost C# konzolových aplikací.  

> **Pro tip:** Nainstalujte NuGet balíček přes CLI, abyste měli vždy nejnovější verzi:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Jak zkopírovat kontingenční tabulku mezi listy

Prvním krokem je přesunout kontingenční tabulku a zachovat její definici. Aspose.Cells poskytuje metodu `CopyRange` s objektem `CopyOptions`, který obsahuje příznak `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Proč to funguje:**  
`CopyRange` kopíruje data buněk, formátování a když je `CopyPivotTable` nastaveno na true, také cache a metadata kontingenční tabulky. Cílový rozsah začíná buňkou `A1` (řádek 0, sloupec 0), ale můžete změnit offsety a umístit tabulku kamkoli.

**Běžný okrajový případ:** Pokud cílový list již obsahuje kontingenční tabulku se stejným názvem, Aspose.Cells ji automaticky přejmenuje, čímž zabrání kolizi názvů.

## Exportujte Excel do PPTX a vytvořte editovatelný PPTX

Po umístění kontingenční tabulky můžete celý sešit exportovat do souboru PPTX. Třída `ImageOrPrintOptions` umožňuje nastavit `ExportImageFormat = ImageFormat.Pptx`, což říká Aspose.Cells, aby výstup považoval za prezentaci PowerPoint místo rastrového obrázku.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Proč to funguje:**  
Když je `ExportImageFormat` nastaveno na `Pptx`, Aspose.Cells převádí každý list na snímek. Tvary, grafy a kontingenční tabulky jsou zapsány jako nativní objekty PowerPointu, takže je můžete v PowerPointu dvojklikem otevřít a upravit podkladová data.

**Tip pro velké sešity:** Pokud potřebujete jen podmnožinu listů, použijte `workbook.Worksheets.RemoveAt(index)` pro listy, které nechcete exportovat, před voláním `Save`. Tím snížíte velikost souboru PPTX.

## Úplný, spustitelný příklad

Níže je kompletní program, který spojuje předchozí kroky. Nahraďte `YOUR_DIRECTORY` skutečnou cestou na vašem počítači.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Očekávaný výstup

Spuštěním programu se vypíše:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Když otevřete `output.pptx` v Microsoft PowerPoint, uvidíte snímek, který obsahuje zkopírovanou kontingenční tabulku jako editovatelný graf. Dvojklik na graf otevře editor grafu v PowerPointu, kde můžete měnit řady, osy a popisky dat bez nutnosti návratu do Excelu.

## Řešení typických problémů

| Problém | Příčina | Řešení |
|-------|-------|-----|
| Kontingenční tabulka se zobrazuje jako statický obrázek | Vynechán příznak `CopyPivotTable` nebo `ExportImageFormat` nastaven na `Png` | Zajistěte `CopyPivotTable = true` a `ExportImageFormat = ImageFormat.Pptx`. |
| Cílový list ukazuje prázdné buňky | Zdrojový rozsah nepokrývá celou oblast kontingenční tabulky | Rozšiřte rozsah (např. `"A1:H30"`), aby zahrnoval všechna pole tabulky. |
| Exportovaný PPTX je obrovský | Do souboru jsou zahrnuty zbytečné listy | Odstraňte nepotřebné listy před voláním `Save`. |
| PowerPoint nedokáže upravit graf | Používáte starší verzi Aspose.Cells, která nepodporuje PPTX | Aktualizujte na nejnovější verzi Aspose.Cells (zkontrolujte poznámky k vydání). |

## Další kroky a související témata

* **Exportovat list Excelu do PPTX s vlastními rozvrženími snímků** – prozkoumejte `WorksheetToPdfConverter` pro jemnější kontrolu vzhledu snímků.  
* **Exportovat Excel do PDF** – nahraďte `ImageFormat.Pptx` za `ImageFormat.Pdf` a vygenerujte PDF.  
* **Programově upravit PPTX po exportu** – použijte knihovnu `Aspose.Slides` k přidání animací nebo poznámek k řečníkovi.  

Ovládnutím **copy pivot table**, **export excel to pptx** a **generate editable pptx** můžete vytvořit kompletní reportingové pipeline, které přenášejí data z tabulek přímo do prezentačních decků bez ztráty editovatelnosti.

---


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}