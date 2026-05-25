---
category: general
date: 2026-03-30
description: Skapa PowerPoint från Excel snabbt med Aspose.Cells och Aspose.Slides.
  Lär dig hur du exporterar kalkylblad som bild och sparar presentationen som PPTX
  i C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: sv
og_description: Skapa PowerPoint från Excel i C# med Aspose. Exportera kalkylbladet
  som bild, behåll former redigerbara och spara resultatet som PPTX.
og_title: Skapa PowerPoint från Excel – Komplett C#-handledning
tags:
- Aspose
- C#
- Office Automation
title: Skapa PowerPoint från Excel – Steg‑för‑steg C#‑guide
url: /sv/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PowerPoint från Excel – Komplett C#‑handledning

Har du någonsin behövt **skapa PowerPoint från Excel** men inte varit säker på vilket bibliotek som kan hålla dina diagram redigerbara? Du är inte ensam. I många rapporteringsscenario vill du omvandla ett kalkylblad till en bildspel utan att förlora möjligheten att justera textrutor senare. Denna guide visar exakt hur du **konverterar Excel till PowerPoint** med Aspose.Cells och Aspose.Slides, samt hur du **exporterar arbetsblad som bild** och slutligen **sparar presentationen som PPTX**.

Vi går igenom varje kodrad, förklarar *varför* varje inställning är viktig, och diskuterar även vad du ska göra om din arbetsbok innehåller komplexa diagram som du hellre exporterar som en bild. I slutet har du en färdig‑att‑köra C#‑konsolapp som tar `ShapesDemo.xlsx` och genererar `Result.pptx` – med redigerbara textrutor och skarpa bilder.

## Vad du behöver

- .NET 6.0 eller senare (API‑et fungerar även med .NET Framework, men .NET 6 är den optimala versionen).  
- **Aspose.Cells** och **Aspose.Slides** NuGet‑paket (gratis provlicenser fungerar för testning).  
- En grundläggande förståelse för C#‑syntax – om du kan skriva en `Console.WriteLine` är du redo att köra.  

Ingen extra COM‑interop, ingen Office‑installation på servern och ingen manuell kopiering‑och‑klistra av bilder. Allt hanteras programatiskt.

---

## Skapa PowerPoint från Excel – Ladda arbetsbok och ställ in exportalternativ

Det första vi gör är att öppna Excel‑filen och tala om för Aspose.Cells hur vi vill att bladet ska renderas. Objektet `ImageOrPrintOptions` är där magin sker: vi aktiverar `ExportShapes` och `ExportEditableTextBoxes` så att alla former (inklusive diagram) blir en del av sliden **och** förblir redigerbara efter konverteringen.

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

**Varför dessa flaggor?**  
- `OnePagePerSheet` förhindrar att bladet delas upp på flera slides – du får en enda bild i full storlek.  
- `ExportShapes` instruerar Aspose.Cells att rasterisera diagram *och* vektorformer, vilket bevarar deras utseende.  
- `ExportEditableTextBoxes` är den hemliga ingrediensen som låter dig dubbelklicka på en textruta i PowerPoint och redigera texten utan att öppna Excel igen.

> **Proffstips:** Om du bara behöver en statisk bild av ett diagram, sätt `ExportShapes = false` och använd metoden `ExportExcelChartAsPicture` senare (se sista avsnittet).

---

## Konvertera Excel till PowerPoint – Generera bild från arbetsblad

Med alternativen klara omvandlar vi nu arbetsbladet till en `System.Drawing.Image`. `WorksheetToImageConverter` gör det tunga lyftet och använder de inställningar vi just definierat.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Argumentet `0` anger den första sidan (vi har bara en på grund av `OnePagePerSheet`). Den resulterande `sheetImage` behåller original‑DPI, så din slide blir inte pixelerad även på högupplösta skärmar.

---

## Spara presentation som PPTX – Infoga bild i en slide

Nu skapar vi en ny PowerPoint‑fil, lägger till en slide och placerar bitmap‑bilden på den. Aspose.Slides behandlar bilden som en *picture frame*-form, som du senare kan ändra storlek på eller flytta precis som vilken inbyggd PowerPoint‑objekt som helst.

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

> **Vad händer om bilden är större än slide‑storleken?**  
> PowerPoint klipper automatiskt allt som överskrider slide‑dimensionerna. En snabb lösning är att skala bilden innan du infogar den:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Du kan sedan skicka `newWidth` och `newHeight` till `AddPictureFrame`.

---

## Exportera arbetsblad som bild – Spara PPTX‑filen

Till sist sparar vi presentationen till disk. Flaggan `SaveFormat.Pptx` garanterar det moderna OpenXML‑formatet, som fungerar i alla aktuella versioner av PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

När du öppnar `Result.pptx` ser du en enda slide som ser exakt ut som ditt Excel‑blad, men du kan fortfarande klicka på någon textruta och redigera innehållet direkt i PowerPoint.

---

## Exportera Excel‑diagram som bild – När rasterbilder föredras

Ibland behöver du inte redigerbara former; en högkvalitativ PNG av ett diagram räcker. Aspose.Cells kan exportera ett specifikt diagram till en bild utan att konvertera hela bladet:

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

Du kan sedan bädda in `chart.png` i en slide på samma sätt som vi lade till `sheetImage`. Detta minskar PPTX‑filens storlek och är användbart när den omgivande datan inte behövs på sliden.

---

## Vanliga fallgropar & hur du undviker dem

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| **Text blir suddig** | Exporterad med låg DPI (standard 96). | Sätt `imageOptions.Dpi = 300;` innan konvertering. |
| **Former försvinner** | `ExportShapes` var `false`. | Säkerställ `ExportShapes = true` när du behöver redigerbara grafik. |
| **Slide‑storlek matchar inte** | Bilden är större än slide‑dimensionerna. | Skala bilden (se kodsnutt) eller ändra slide‑storlek via `presentation.SlideSize`. |
| **Licensundantag** | Använder provversion utan korrekt aktivering. | Anropa `License license = new License(); license.SetLicense("Aspose.Total.lic");` tidigt i `Main`. |

---

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

Nedan är hela programmet, redo att klistras in i ett nytt konsolprojekt. Byt ut `YOUR_DIRECTORY` mot mappen som innehåller din Excel‑fil.

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

**Förväntad utskrift:**  
När programmet körs skrivs `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. När du öppnar PPTX‑filen visas en enda slide som speglar det ursprungliga Excel‑bladet, med redigerbara textrutor.

---

## Sammanfattning & Nästa steg

Du vet nu hur du **skapar PowerPoint från Excel** med Asposes kraftfulla API:er, hur du **exporterar arbetsblad som bild**, och hur du **sparar presentation som PPTX** samtidigt som du bevarar redigerbarhet. Samma mönster fungerar för arbetsböcker med flera blad – bara loopa igenom `workbook.Worksheets` och lägg till en ny slide för varje.

**Vad kan du utforska härnäst?**  

- **Batchkonvertering:** Loopa över en mapp med Excel‑filer och generera ett bildspel per fil.  
- **Dynamiska layouter:** Använd `slide.LayoutSlide` för att tillämpa fördesignade PowerPoint‑mallar.  
- **Endast‑diagram‑export:** Kombinera kodsnutten “Export Excel chart as picture” med slide‑platshållare för ett slankare bildspel.  
- **Avancerad styling:** Lägg till anpassade slide‑bakgrunder, övergångar eller animationer via Aspose.Slides.

Känn dig fri att experimentera – ändra DPI, byt `ShapeType.Ellipse` mot en cirkulär bildram, eller bädda in flera bilder per slide. Möjligheterna är oändliga när du har programmatisk kontroll över

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}