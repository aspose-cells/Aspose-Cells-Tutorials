---
category: general
date: 2026-11-16
description: Naučte se, jak uložit Excel jako PowerPoint a programově převést Excel
  do PowerPointu. Tento krok‑za‑krokem průvodce také zahrnuje export Excelu do PPTX
  a uložení sešitu jako PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: cs
lastmod: 2026-11-16
og_description: Uložte Excel jako PowerPoint pomocí Aspose.Cells. Postupujte podle
  tohoto návodu, jak převést Excel na PowerPoint, exportovat Excel do PPTX a uložit
  sešit jako PPTX během několika minut.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Uložení Excelu jako PowerPoint – Kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Jak uložit Excel jako PowerPoint pomocí Aspose.Cells v C#
url: /cs/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit Excel jako PowerPoint pomocí Aspose.Cells v C#

Pokud potřebujete **uložit Excel jako PowerPoint** programově, tento tutoriál vám poskytne kompletní, připravené řešení. Ať už vytváříte reportingový engine nebo automatizovaný generátor snímků, níže uvedené kroky vám umožní převést list Excelu na editovatelný PPTX snímek během několika řádků kódu.

Naučíte se, jak **převést Excel do PowerPointu**, exportovat list do souboru PPTX a zachovat textová pole a tvary editovatelná – vše bez opuštění prostředí .NET.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7.2+)
* Platná licence Aspose.Cells (bezplatná zkušební verze funguje pro hodnocení)
* Visual Studio 2022 (nebo jakékoli C# IDE)
* Excel sešit, který obsahuje data a tvary, které chcete exportovat

## Krok 1: Nainstalujte Aspose.Cells

Přidejte NuGet balíček Aspose.Cells do svého projektu:

```bash
dotnet add package Aspose.Cells
```

> **Tip:** Použijte přepínač `-v` k cílení konkrétní verze, např. `Aspose.Cells.24.5`.

## Krok 2: Načtěte sešit, který chcete exportovat

Prvním krokem ve workflow **uložit Excel jako PowerPoint** je načtení zdrojového sešitu.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Proč je to důležité:* Načtení sešitu vám poskytne přístup k jeho listům, nastavení stránky a kreslicím objektům, které se stanou editovatelnými tvary v PowerPointu.

## Krok 3: Nakonfigurujte možnosti exportu pro editovatelný PPTX snímek

Pro **převod Excelu do PowerPointu** při zachování editovatelnosti musíte nastavit několik vlastností na `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Vysvětlení:*  
* `SaveFormat = SaveFormat.Pptx` říká Aspose.Cells, aby vytvořil soubor PowerPoint.  
* `ExportEditableText` a `ExportEditableShapes` zajišťují, že výsledný snímek se chová jako nativní PowerPoint snímek – můžete kliknout na textové pole nebo tvar a upravit jej přímo v PowerPointu.

## Krok 4: Definujte oblast exportu a přizpůsobte ji jedné snímku

Když **exportujete Excel do PPTX**, obvykle chcete, aby se na snímku zobrazila konkrétní oblast. Nastavení tiskové oblasti a možností přizpůsobení zaručuje čistý výstup na jediném snímku.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Proč je to důležité:* `PrintArea` omezuje export na buňky A1 až G30, zatímco `FitToPagesTall` a `FitToPagesWide` vše zkomprimují do jednoho snímku, čímž zabrání nechtěným dalším stránkám.

## Krok 5: Uložte list jako editovatelný PPTX soubor

Nyní můžete konečně **uložit sešit jako PPTX** a dokončit proces **uložení Excelu jako PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Po spuštění programu otevřete `EditableShapes.pptx` v Microsoft PowerPoint. Uvidíte snímek, který odráží vybranou oblast Excelu, a všechna textová pole a tvary jsou plně editovatelné.

### Očekávaný výstup

* Soubor pojmenovaný `EditableShapes.pptx` umístěný v `C:\Output\`.
* Jeden PowerPoint snímek obsahující oblast A1:G30.
* Textová pole, grafy a tvary, které můžete dvojklikem upravit přímo v PowerPointu.

## Kompletní zdrojový kód (připravený ke zkopírování)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Časté otázky a řešení okrajových případů

| Otázka | Odpověď |
|----------|--------|
| **Co když mám více listů?** | Procházejte `workbook.Worksheets` a opakujte kroky 3‑5 pro každý list, přičemž měňte název výstupního souboru (např. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Mohu exportovat celý sešit do jedné PowerPoint prezentace?** | Ano. Nastavte `ExportAllSheets = true` na `ImageOrPrintOptions`. Každý list se stane samostatným snímkem. |
| **Moje tvary se zobrazují jako obrázky, ne jako editovatelné objekty.** | Ujistěte se, že `ExportEditableShapes = true` a že používáte Aspose.Cells 24.5+ (starší verze tuto funkci nemají). |
| **Vygenerovaný PPTX je příliš velký.** | Zmenšete tiskovou oblast nebo snižte rozlišení obrázku pomocí `exportOptions.ImageResolution`. |
| **Potřebuji licenci pro produkční použití?** | Placená licence odstraňuje vodoznak pro hodnocení a odemyká plný výkon. Bezplatná zkušební verze funguje pro testování. |

## Tipy pro robustní produkční kód

* **Ověřte souborové cesty** před voláním `Workbook` nebo `Save`, aby nedošlo k `FileNotFoundException`.  
* **Zabalte export do try/catch** bloku pro ošetření chyb licence (`Aspose.Cells.LicenseException`).  
* **Uvolněte sešit** (`workbook.Dispose()`) po dokončení, aby se uvolnily neřízené prostředky.  
* **Používejte async I/O** (`FileStream` s `await`), pokud exportujete mnoho velkých listů ve webové službě.

## Další kroky

Nyní, když víte, jak **uložit Excel jako PowerPoint**, můžete prozkoumat související témata:

* **Export Excel do PPTX s vlastními rozvrženími snímků** – upravte `SlideSize` a přidejte hlavní snímek.  
* **Převod Excel snímku do PDF** – použijte `SaveFormat.Pdf` pro tiskovou verzi.  
* **Dávkový převod složky sešitů** – zkombinujte výše ukázaný cyklus s `Directory.GetFiles`.  

Experimentujte s různými tiskovými oblastmi, možnostmi škálování a motivy PowerPointu, abyste výstup přizpůsobili brandingu vaší organizace.

---

*Šťastné programování! Pokud vám tento průvodce pomohl **převést Excel do PowerPointu**, neváhejte jej sdílet s kolegy nebo otevřít issue v repozitáři Aspose.Cells na GitHubu pro další pomoc.*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak uložit Excel jako PowerPoint pomocí C# a Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Jak uložit PPTX z Excelu – Kompletní průvodce exportem listu Excel do PowerPointu](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Převod Excelu do PowerPointu – Kompletní krok‑za‑krokem průvodce](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}