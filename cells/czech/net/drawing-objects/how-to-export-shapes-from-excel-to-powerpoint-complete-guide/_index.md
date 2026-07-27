---
category: general
date: 2026-07-26
description: Jak exportovat tvary z listu Excelu do PowerPointu během několika kroků
  – rychlý tutoriál pro vývojáře o exportu Excel do PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: cs
lastmod: 2026-07-26
og_description: Jak krok za krokem exportovat tvary z Excelu do PowerPointu. Sledujte
  tento tutoriál exportu Excel do PPTX a uvidíte, jak se vaše listy promění v editovatelné
  snímky.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Jak exportovat tvary z Excelu do PowerPointu – rychle a snadno
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Jak exportovat tvary z Excelu do PowerPointu – kompletní průvodce
url: /cs/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat tvary z Excelu do PowerPointu – Kompletní průvodce

Už jste se někdy zamýšleli **jak exportovat tvary** z Excelového souboru a zachovat je editovatelné v PowerPointové prezentaci? Nejste v tom sami. Ať už budujete reportingový pipeline nebo jen potřebujete rychlý způsob, jak převést tabulku na prezentaci, schopnost **převést list do PowerPointu** bez ztráty editovatelnosti tvarů vám může ušetřit hodiny manuální práce.

V tomto **excel to powerpoint tutorial** projdeme plně funkčním příkladem v C#, který načte sešit, nastaví správné možnosti exportu a vytvoří soubor PPTX, kde textová pole a další kreslicí objekty zůstávají editovatelné. Žádné vágní odkazy – jen kód, který můžete dnes zkopírovat, vložit a spustit.

## Co se naučíte

- Přesné kroky k **exportu excel do pptx** s zachováním editovatelnosti tvarů.  
- Jak knihovna `Aspose.Cells` a její `PptxSaveOptions` řídí chování exportu.  
- Tipy pro práci s více listy, chybějícími soubory a vlastními nastaveními tvarů.  
- Kompletní, spustitelný program, který můžete vložit do libovolného .NET projektu.

### Předpoklady

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+).  
- Platná licence pro **Aspose.Cells for .NET** (zdarma zkušební verze stačí pro testování).  
- Excelový sešit (např. `ShapesDemo.xlsx`) obsahující alespoň jedno textové pole nebo tvar.  
- Vývojové prostředí – Visual Studio, Rider nebo VS Code jsou v pořádku.

Pokud máte vše připravené, pojďme na to.

## Krok 1: Načtení sešitu – Výchozí bod pro export tvarů  

Nejprve musíme otevřít Excelový soubor, který obsahuje tvary, jež chceme zachovat editovatelné.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Proč je to důležité:**  
Objekt `Workbook` je vstupní bránou ke každé buňce, grafu i kreslicímu objektu v souboru. Tím, že získáme první list (`Worksheets[0]`), pracujeme s známým listem, ale můžete nahradit index názvem (`workbook.Worksheets["Sheet2"]`), pokud potřebujete konkrétní kartu.

> **Tip:** Zabalte volání načtení do `try / catch` bloku, abyste získali přátelskou chybu při špatné cestě k souboru.

## Krok 2: Nastavení možností exportu PPTX – Jádro exportu tvarů  

Nyní řekneme Aspose.Cells, aby vygenerovaný PPTX zachoval tvary editovatelné.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Proč tyto příznaky?**  
- `ExportEditableTextBoxes` převádí Excelová textová pole na PowerPointové textové zástupce, které můžete dvojklikem upravit.  
- `ExportEditableShapes` dělá totéž pro tvary jako šipky, obdélníky a SmartArt. Bez nich se objekty stanou statickými obrázky, což by zničilo smysl **convert worksheet to powerpoint** workflow.

Můžete také upravit `PptxSaveOptions` pro nastavení velikosti snímku, motivu nebo vložení fontů – užitečné, když prezentace musí odpovídat firemnímu brandingu.

## Krok 3: Uložení listu jako PPTX – Poslední krok exportu Excel do PowerPointu  

S nastavenými možnostmi je uložení přímočaré.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Co se děje pod kapotou?**  
Aspose.Cells prochází každý kreslicí objekt na listu, mapuje jej na odpovídající třídu PowerPointu a zapisuje XML, které PowerPoint načte. Protože jsme povolili editovatelné příznaky, XML označuje každý objekt jako `Shape` místo `Picture`, takže PowerPoint s ním zachází jako s živým objektem.

## Krok 4: Potvrzení exportu – Rychlá zpětná vazba pro uživatele  

Malá zpráva v konzoli vám dá vědět, že proces proběhl úspěšně.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Pokud program spustíte a zobrazí se zpráva, otevřete `ShapesEditable.pptx` v PowerPointu. Klikněte na libovolné textové pole – mělo by být možné text přímo upravit, a přetahování tvaru by ho mělo přesunout stejně jako nativní objekt PowerPointu.

## Krok 5: Řešení reálných scénářů  

Níže jsou běžné varianty, se kterými můžete při **excel to powerpoint tutorial** narazit.

### Více listů

Pokud potřebujete exportovat několik listů do jednoho PPTX, projděte `workbook.Worksheets` a zavolejte `worksheet.Save` se stejným `pptxOptions`. Aspose.Cells automaticky přidá nový snímek pro každý list.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Vlastní rozvržení snímků

Můžete nastavit `pptxOptions.SlideSize` (např. `SlideSizeType.Widescreen`) tak, aby odpovídalo rozměrům vaší firemní prezentace.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### Chybějící soubory nebo oprávnění

Zabalte celý `Main` metod do `try` bloku:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Tím učiníte proces **export excel workbook powerpoint** odolným pro produkční pipeline.

## Kompletní funkční příklad

Zde je celý program, který můžete zkompilovat hned teď. Uložte jej jako `ExportEditableShapes.cs`, upravte cesty k souborům a spusťte `dotnet run`.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup** při spuštění programu:

```
Exported worksheet with editable shapes.
```

Otevřete vygenerovaný `ShapesEditable.pptx` a uvidíte, že každý Excelový tvar je plně editovatelný objekt v PowerPointu – přesně to, co jste hledali při zadání **how to export shapes**.

## Často kladené otázky

- **Funguje to i se staršími formáty Excelu (.xls)?**  
  Ano. `Workbook` může otevřít `.xls`, `.xlsx` i CSV soubory. Export tvarů funguje stejným způsobem.

- **Co když potřebuji zachovat editovatelnost grafů?**  
  Grafy jsou již exportovány jako nativní PowerPointové grafy; není potřeba žádné další příznaky.

- **Mohu exportovat do PDF místo PPTX?**  
  Rozhodně – stačí nahradit `SaveFormat.Pptx` za `SaveFormat.Pdf` a vynechat `PptxSaveOptions`.

## Závěr

Nyní máte solidní, end‑to‑end řešení pro **how to export shapes** z Excelu do editovatelné PowerPointové prezentace. Využitím `Aspose.Cells` `PptxSaveOptions` zachováte každé textové pole i kreslicí objekt, čímž proměníte statickou tabulku v dynamickou prezentaci s minimálním úsilím.

Připravení na další výzvu? Zkuste přidat vlastní slide mastery, vkládat obrázky programově nebo propojit tento export do CI/CD pipeline, která automaticky generuje týdenní prodejní decky. Svět **export excel workbook powerpoint** je otevřený – jděte ho prozkoumat!

--- 

*Pokud se vám tento **excel to powerpoint tutorial** líbil, dejte mu hvězdičku na GitHubu nebo jej sdílejte s kolegou, který stále kopíruje‑vkládá tabulky do slidů. Šťastné kódování!*

## Co se naučíte dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [How to Export Excel Cells as Images Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}