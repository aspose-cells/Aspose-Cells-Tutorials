---
category: general
date: 2026-10-01
description: Vytvořte PowerPoint z Excelu pomocí Aspose.Cells v C#. Exportujte Excel
  do PowerPointu a rychle převádějte XLSX na PPTX s kompletním ukázkovým kódem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: cs
lastmod: 2026-10-01
og_description: Vytvořte PowerPoint z Excelu pomocí Aspose.Cells v C#. Naučte se exportovat
  Excel do PowerPointu a převést XLSX na PPTX pomocí několika řádků kódu.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Vytvořte PowerPoint z Excelu pomocí Aspose.Cells – rychlý průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Vytvořte PowerPoint z Excelu pomocí Aspose.Cells – krok za krokem
url: /cs/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte PowerPoint z Excelu pomocí Aspose.Cells – krok za krokem průvodce

Pokud potřebujete **vytvořit PowerPoint z Excelu**, tento tutoriál vám ukáže, jak to provést pomocí Aspose.Cells pro .NET. Naučíte se **exportovat Excel do PowerPointu**, převést sešit XLSX na prezentaci PPTX a přizpůsobit výsledné snímky, aniž byste opustili svůj C# projekt.

Průvodce pokrývá vše, co potřebujete ke spuštění kódu na .NET 6 nebo novějším, včetně nastavení projektu, požadovaných NuGet balíčků a kompletního, spustitelného příkladu. Na konci budete mít soubor PowerPoint, který obsahuje původní Excel graf přesně tak, jak se zobrazuje v sešitu.

## Co budete potřebovat

| Požadavek | Důvod |
|---|---|
| .NET 6 SDK nebo novější | Poskytuje runtime pro C# konzolovou aplikaci |
| Visual Studio 2022 (nebo jakékoli IDE) | Umožňuje snadné vytvoření projektu a ladění |
| Aspose.Cells for .NET NuGet package | Poskytuje třídu `Workbook` a exportní API |
| Excel soubor (`.xlsx`) obsahující alespoň jeden graf | Zdrojová data pro PowerPoint snímek |

> **Pro tip:** Aspose.Cells funguje na Windows, Linuxu i macOS, takže můžete spustit stejný kód v Docker kontejnerech nebo CI pipelinech.

## Krok 1: Vytvořte nový konzolový projekt a přidejte Aspose.Cells

Otevřete terminál (nebo Visual Studio Package Manager Console) a spusťte:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

Příkaz `dotnet add package` stáhne nejnovější stabilní verzi **Aspose.Cells**, která zahrnuje metodu `ExportPptx` používanou později.

## Krok 2: Přidejte zdrojový Excel sešit

Umístěte Excel soubor, který chcete převést, do složky projektu. Pro tento tutoriál použijeme `ChartOle.xlsx`, který obsahuje jediný graf na prvním listu.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Krok 3: Napište kód, který **vytvoří PowerPoint z Excelu**

Otevřete `Program.cs` a nahraďte jeho obsah následujícím kódem. Příklad demonstruje **základní export** a také ukazuje, jak zacházet s běžnými okrajovými případy, jako jsou chybějící soubory a nepodporované typy grafů.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Proč to funguje

* `Workbook` načte celý Excel soubor, včetně vložených grafů, tabulek a formátování.  
* `ExportPptx` převádí aktivní list na PPTX sadu snímků. Metoda automaticky transformuje Excel grafy na PowerPoint tvary, zachovávajíc vizuální věrnost.  
* Kód obaluje operaci do bloku `try/catch`, aby zobrazil chyby, jako jsou selhání **convert XLSX to PPTX** způsobené poškozenými soubory.

## Krok 4: Spusťte program a ověřte výstup

Spusťte aplikaci:

```bash
dotnet run
```

Měli byste vidět zprávu v konzoli:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Otevřete `Exported.pptx` v Microsoft PowerPoint nebo jakémkoli kompatibilním prohlížeči. První snímek zobrazuje graf přesně tak, jak byl v `ChartOle.xlsx`. Tím se potvrzuje, že jste úspěšně **vytvořili PowerPoint z Excelu**.

## Krok 5: Pokročilé – export více listů nebo vlastní rozvržení snímků

Základní příklad exportuje pouze první list. Ve skutečných scénářích můžete potřebovat:

* **Exportovat několik listů** do samostatných snímků.  
* **Ovládnout velikost snímku** nebo přidat zástupný text pro název.  
* **Zahrnout skryté listy** do převodu.

Níže je stručný úryvek, který iteruje přes všechny listy a přidá každý jako samostatný snímek:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Poznámka:** Pokročilý úryvek vyžaduje knihovnu **Aspose.Slides for .NET**. Pokud potřebujete jen jednoduchý převod jednoho listu, stačí předchozí volání `ExportPptx`.

## Časté úskalí a jak se jim vyhnout

| Problém | Příčina | Řešení |
|---|---|---|
| Prázdný snímek po exportu | List neobsahuje žádné viditelné objekty | Ujistěte se, že před voláním `ExportPptx` je přítomen alespoň jeden graf, tabulka nebo tvar. |
| Chybějící písma v PowerPointu | Písmo není nainstalováno na počítači, kde se PPTX otevírá | Vložte požadovaná písma do Excel sešitu nebo je nainstalujte na cílovém systému. |
| Neočekávané škálování | Velký graf přesahuje rozměry snímku | Před exportem upravte vlastnost `PageSetup.Zoom` listu. |
| `convert XLSX to PPTX` vyvolá `NotSupportedException` | Typ grafu není podporován Aspose.Cells (např. 3‑D mapy) | Nahraďte graf podporovaným typem nebo nejprve exportujte list jako obrázek. |

Řešením těchto okrajových případů zajistíte spolehlivý **export Excel do PowerPointu** ve výrobním prostředí.

## Závěr

Nyní víte, jak **vytvořit PowerPoint z Excelu** pomocí Aspose.Cells pro .NET. Tutoriál pokryl:

* Nastavení projektu a instalaci NuGet balíčků  
* Načtení Excel sešitu a volání `ExportPptx`  
* Spuštění kódu a ověření vygenerovaného PPTX  
* Rozšíření řešení pro zpracování více listů a vlastní rozvržení snímků  
* Praktické tipy, jak se vyhnout běžným problémům při konverzi  

S těmito znalostmi můžete automatizovat tvorbu reportů, budovat pipeline pro prezentace nebo integrovat převod Excel → PowerPoint do jakékoli C# aplikace. Experimentujte s různými typy grafů, přidávejte názvy snímků nebo kombinujte export s Aspose.Slides pro plnohodnotnou tvorbu prezentací.

--- 

*Chcete objevovat dál? Podívejte se na související témata, jako je **convert Excel to PDF**, **embed Excel data in Word** nebo **use Aspose.Slides to programmatically edit PPTX files**.*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich vlastních projektech.

- [Převést Excel na PowerPoint Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Převést Excel na PowerPoint Aspose Cells .NET](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Převést Excel na PowerPoint Aspose Cells .NET](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}