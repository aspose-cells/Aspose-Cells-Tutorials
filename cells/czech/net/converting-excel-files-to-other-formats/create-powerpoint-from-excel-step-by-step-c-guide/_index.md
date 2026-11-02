---
category: general
date: 2026-03-30
description: Vytvořte PowerPoint z Excelu rychle pomocí Aspose.Cells a Aspose.Slides.
  Naučte se, jak exportovat list jako obrázek a uložit prezentaci jako PPTX v C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: cs
og_description: Vytvořte PowerPoint z Excelu v C# pomocí Aspose. Exportujte list jako
  obrázek, zachovejte editovatelnost tvarů a uložte výsledek jako PPTX.
og_title: Vytvořte PowerPoint z Excelu – kompletní C# tutoriál
tags:
- Aspose
- C#
- Office Automation
title: Vytvořte PowerPoint z Excelu – krok za krokem průvodce C#
url: /cs/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PowerPointu z Excelu – Kompletní C# tutoriál

Už jste někdy potřebovali **vytvořit PowerPoint z Excelu**, ale nebyli jste si jisti, která knihovna umožní zachovat editovatelnost vašich grafů? Nejste v tom sami. V mnoha scénářích reportování budete chtít převést tabulku na sadu snímků, aniž byste ztratili možnost později upravit textová pole. Tento průvodce vám ukáže přesně, jak **převést Excel do PowerPointu** pomocí Aspose.Cells a Aspose.Slides, a zároveň jak **exportovat list jako obrázek** a nakonec **uložit prezentaci jako PPTX**.

Projdeme každý řádek kódu, vysvětlíme *proč* má každé nastavení význam, a dokonce se podíváme, co dělat, pokud váš sešit obsahuje složité grafy, které raději exportujete jako obrázek. Na konci budete mít připravenou spustitelnou C# konzolovou aplikaci, která vezme `ShapesDemo.xlsx` a vytvoří `Result.pptx` – vše s editovatelnými textovými poli a ostrými obrázky.

## Co budete potřebovat

- .NET 6.0 nebo novější (API funguje také s .NET Framework, ale .NET 6 je optimální).  
- **Aspose.Cells** a **Aspose.Slides** NuGet balíčky (licence zdarma pro zkušební verzi fungují pro testování).  
- Základní znalost syntaxe C# – pokud umíte napsat `Console.WriteLine`, jste připraveni.  

Žádná další COM interop, žádný Office nainstalovaný na serveru a žádné ruční kopírování obrázků. Vše je zpracováno programově.

---

## Vytvoření PowerPointu z Excelu – Načtení sešitu a nastavení exportních možností

Prvním krokem je otevřít soubor Excel a říct Aspose.Cells, jak má být list vykreslen. Objekt `ImageOrPrintOptions` je místem, kde se děje kouzlo: povolíme `ExportShapes` a `ExportEditableTextBoxes`, aby se všechny tvary (včetně grafů) staly součástí snímku **a** zůstaly po konverzi editovatelné.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Proč tyto příznaky?**  
- `OnePagePerSheet` zabraňuje rozdělení listu na více snímků – získáte jeden, plně velký obrázek.  
- `ExportShapes` říká Aspose.Cells, aby rasterizoval grafy *a* vektorové tvary, zachovávajíc jejich vzhled.  
- `ExportEditableTextBoxes` je tajná ingredience, která vám umožní dvojklikem na textové pole v PowerPointu upravit text, aniž byste znovu otevírali Excel.

> **Tip:** Pokud potřebujete jen statický obrázek grafu, nastavte `ExportShapes = false` a později použijte metodu `ExportExcelChartAsPicture` (viz závěrečná část).

---

## Převod Excelu do PowerPointu – Vytvoření obrázku z listu

S připravenými možnostmi nyní převedeme list na `System.Drawing.Image`. `WorksheetToImageConverter` provádí těžkou práci a aplikuje nastavení, která jsme právě definovali.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Argument `0` označuje první stránku (máme jen jednu kvůli `OnePagePerSheet`). Výsledný `sheetImage` zachovává původní DPI, takže váš snímek nebude pixelovaný ani na displejích s vysokým rozlišením.

---

## Uložení prezentace jako PPTX – Vložení obrázku do snímku

Nyní vytvoříme nový soubor PowerPoint, přidáme snímek a vložíme na něj bitmapu. Aspose.Slides zachází s obrázkem jako s tvarem *picture frame*, který můžete později měnit velikost nebo přesouvat stejně jako jakýkoli nativní objekt PowerPointu.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Co když je obrázek větší než velikost snímku?**  
> PowerPoint automaticky ořízne vše, co přesahuje rozměry snímku. Rychlé řešení je před vložením obrázek změnit měřítko:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Poté můžete předat `newWidth` a `newHeight` metodě `AddPictureFrame`.

---

## Export listu jako obrázek – Uložení souboru PPTX

Nakonec uložíme prezentaci na disk. Příznak `SaveFormat.Pptx` zajišťuje moderní formát OpenXML, který funguje ve všech recentních verzích PowerPointu.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Když otevřete `Result.pptx`, uvidíte jeden snímek, který vypadá přesně jako váš list v Excelu, ale stále můžete kliknout na jakékoli textové pole a upravit jeho obsah přímo v PowerPointu.

---

## Export grafu z Excelu jako obrázek – Když jsou preferovány rastrové obrázky

Někdy nepotřebujete editovatelné tvary; stačí vysoce kvalitní PNG grafu. Aspose.Cells může exportovat konkrétní graf jako obrázek, aniž by převáděl celý list:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Poté můžete vložit `chart.png` do snímku stejným způsobem, jakým jsme přidali `sheetImage`. Tento přístup snižuje velikost souboru PPTX a je užitečný, když okolní data na snímku nejsou potřeba.

---

## Časté problémy a jak se jim vyhnout

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Text vypadá rozmazaně** | Exportováno při nízkém DPI (výchozí 96). | Nastavte `imageOptions.Dpi = 300;` před konverzí. |
| **Tvary zmizí** | `ExportShapes` bylo nastaveno na `false`. | Ujistěte se, že `ExportShapes = true`, když potřebujete editovatelné grafiky. |
| **Neshoda velikosti snímku** | Obrázek je větší než rozměry snímku. | Změňte velikost obrázku (viz úryvek kódu) nebo změňte velikost snímku pomocí `presentation.SlideSize`. |
| **Výjimka licence** | Použití zkušební verze bez řádné aktivace. | Zavolejte `License license = new License(); license.SetLicense("Aspose.Total.lic");` na začátku metody `Main`. |

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je celý program, připravený vložit do nového konzolového projektu. Nahraďte `YOUR_DIRECTORY` složkou, která obsahuje váš soubor Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Očekávaný výstup:**  
Spuštěním programu se vypíše `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Otevřením PPTX uvidíte jeden snímek odrážející původní list v Excelu, s editovatelnými textovými poli.

---

## Shrnutí a další kroky

Nyní víte, jak **vytvořit PowerPoint z Excelu** pomocí výkonných API od Aspose, jak **exportovat list jako obrázek** a jak **uložit prezentaci jako PPTX** při zachování editovatelnosti. Stejný vzor funguje i pro sešity s více listy – stačí projít `workbook.Worksheets` a pro každý přidat nový snímek.

**Co dál zkoušet?**  

- **Hromadná konverze:** Procházet složku s Excel soubory a pro každý vytvořit sadu snímků.  
- **Dynamické rozvržení:** Použít `slide.LayoutSlide` k aplikaci předpřipravených šablon PowerPointu.  
- **Export pouze grafu:** Kombinovat úryvek “Export Excel chart as picture” s placeholdery snímků pro úspornější prezentaci.  
- **Pokročilé stylování:** Aplikovat vlastní pozadí snímků, přechody nebo animace pomocí Aspose.Slides.

Neváhejte experimentovat – změňte DPI, zaměňte `ShapeType.Ellipse` za kruhový rámeček obrázku, nebo dokonce vložte více obrázků na jeden snímek. Možnosti jsou neomezené, když máte programatickou kontrolu nad

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}