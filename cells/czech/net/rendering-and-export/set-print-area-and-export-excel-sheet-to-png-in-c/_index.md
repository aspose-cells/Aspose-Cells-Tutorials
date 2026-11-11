---
category: general
date: 2026-10-26
description: Nastavte oblast tisku a exportujte list Excelu do PNG v C#. Naučte se
  možnosti exportu obrázku, jak exportovat PNG a získat tisknutelný obrázek ze sešitu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: cs
lastmod: 2026-10-26
og_description: Nastavte oblast tisku a exportujte list Excelu do PNG v C#. Tento
  krok‑za‑krokem tutoriál pokrývá možnosti exportu obrázků a jak exportovat PNG ze
  sešitu.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Nastavte oblast tisku a exportujte list Excelu do PNG – průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Nastavte oblast tisku a exportujte list Excelu do PNG v C#
url: /cs/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavte oblast tisku a exportujte list Excelu do PNG v C#

Pokud potřebujete **nastavit oblast tisku** před exportem listu Excelu do PNG, tento průvodce vám ukáže, jak na to. Uvidíte kompletní příklad v C#, který konfiguruje možnosti exportu obrázku, upravuje oblast tisku listu a uloží výsledek jako obrázek.

Export listu Excelu do PNG je běžná potřeba, když chcete vložit snímek listu do zprávy, e‑mailu nebo webové stránky. Níže uvedený kód funguje s libovolnou sešitem, který obsahuje kontingenční tabulku, ale technika se vztahuje i na běžné datové oblasti. Nejsou vyžadovány žádné externí nástroje – stačí knihovna Aspose.Cells pro .NET.

## Požadavky

- .NET 6.0 nebo novější (ukázka cílí na .NET 6, ale funguje s libovolnou aktuální verzí .NET)
- Aspose.Cells pro .NET (instalace přes NuGet: `Install-Package Aspose.Cells`)
- Základní znalost C# a konceptů Excelu, jako jsou listy a oblasti tisku

## Krok 1: Nakonfigurujte možnosti exportu obrázku

Prvním krokem je vytvořit instanci `ImageOrPrintOptions`. Tento objekt říká Aspose.Cells, jak vykreslit list jako obrázek.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Proč je to důležité:** `ImageOrPrintOptions` řídí výstupní formát, rozlišení a další podrobnosti vykreslování. Použití PNG zajišťuje bezztrátovou kvalitu, což je ideální pro zprávy vyžadující ostrý text a grafiku.

## Krok 2: Načtěte sešit a přistupte k cílovému listu

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Proč je to důležité:** Musíte pracovat s konkrétním objektem `Worksheet`, protože oblast tisku je nastavení na úrovni listu.

## Krok 3: Identifikujte oblast, kterou chcete tisknout

V mnoha scénářích jsou data, o která vám jde, uvnitř kontingenční tabulky. Následující kód získá datovou oblast první kontingenční tabulky na listu.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Pokud váš list neobsahuje kontingenční tabulku, můžete nahradit `pivotDataRange` libovolným `CellArea`, který vytvoříte ručně, např.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Krok 4: **Nastavte oblast tisku** tak, aby odpovídala vybrané oblasti

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Proč je to důležité:** Oblast tisku říká Excelu (a Aspose.Cells), které buňky zahrnout při vykreslování listu do obrázku. Zarovnáním oblasti tisku s oblastí dat kontingenční tabulky se vyhnete prázdným okrajům a zajistíte, že exportované PNG obsahuje pouze relevantní data.

## Krok 5: Exportujte list do PNG obrázku

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Proč je to důležité:** `worksheet.ToImage` respektuje dříve nastavenou oblast tisku, takže PNG soubor obsahuje přesně buňky, které jste definovali. Přiřazení obrázku k tvaru obrázku vám umožní vložit jej zpět do sešitu, pokud je to potřeba, a uložení na disk vám poskytne samostatný soubor.

## Kompletní funkční příklad

Spojením všech kroků získáte samostatný program, který můžete spustit okamžitě.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Očekávaný výstup

Spuštěním programu se vytvoří `C:\Temp\WorksheetExport.png`. Otevřením souboru uvidíte ostrý PNG obrázek, který obsahuje pouze buňky definované **nastavenou oblastí tisku** (data kontingenční tabulky v tomto příkladu). Obrázek lze vložit do dokumentů Word, snímků PowerPoint nebo webových stránek bez dalších konverzních kroků.

## Práce s více listy nebo kontingenčními tabulkami

- **Více listů:** Procházejte `wb.Worksheets` a opakujte kroky 3‑5 pro každý list, který potřebujete exportovat.
- **Více kontingenčních tabulek:** Vyberte vhodný `PivotTables[index]` nebo iterujte přes `worksheet.PivotTables` a exportujte každou tabulku samostatně.
- **Žádná kontingenční tabulka:** Vytvořte `CellArea` ručně (viz komentář v kroku 3) a přiřaďte jej k `PrintArea`.

## Praktické tipy (E‑E‑A‑T)

- **Pro tip:** Nastavte `HorizontalResolution` a `VerticalResolution` na 300 DPI pro tiskové PNG; nižší hodnoty snižují velikost souboru pro webové použití.
- **Dejte pozor na prázdné tvary obrázků:** Pokud list neobsahuje žádné tvary obrázků, přidejte jeden před přiřazením obrázku:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Výkon:** Opakované používání jedné instance `ImageOrPrintOptions` pro více listů zabraňuje zbytečným alokacím.
- **Kompatibilita:** Aspose.Cells 23.9+ plně podporuje .NET 6 a novější; starší verze mohou vyžadovat úpravy názvů API.

## Závěr

Nyní už víte, jak **nastavit oblast tisku** a exportovat Excel

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak exportovat Excel do PNG – kompletní krok za krokem průvodce](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Jak exportovat oblast Excelu jako obrázek pomocí C# a Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [list Excel do PNG – Export kontingenční tabulky jako PNG v C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}