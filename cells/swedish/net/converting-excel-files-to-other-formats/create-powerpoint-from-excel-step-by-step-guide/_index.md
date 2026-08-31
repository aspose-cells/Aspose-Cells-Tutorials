---
category: general
date: 2026-02-09
description: Skapa PowerPoint från Excel på några minuter – lär dig hur du konverterar
  Excel till PowerPoint och exporterar Excel till PPT med ett enkelt C#‑kodexempel.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: sv
og_description: Skapa PowerPoint från Excel snabbt. Denna guide visar hur du konverterar
  Excel till PowerPoint, exporterar Excel till PPT och genererar PPT från Excel med
  C#.
og_title: Skapa PowerPoint från Excel – Komplett programmeringsguide
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Skapa PowerPoint från Excel – Steg‑för‑steg guide
url: /sv/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PowerPoint från Excel – Komplett programmeringsguide

Har du någonsin behövt **create PowerPoint from Excel** men varit osäker på vilken API du ska anropa? Du är inte ensam. Många utvecklare stöter på problem när de vill omvandla kalkylblad till bildspel utan manuell kopiering‑och‑klistring.  

God nyhet: med några rader C# kan du **convert Excel to PowerPoint**, exportera bladets former och få en färdig‑att‑presentera PPTX‑fil. I den här handledningen går vi igenom hela processen, förklarar varför varje steg är viktigt och visar hur du hanterar de vanligaste fallgroparna.

## Vad du kommer att lära dig

- Hur du laddar en Excel‑arbetsbok som innehåller diagram, bilder eller SmartArt.
- Det exakta anropet som **export Excel to PPT** med Aspose.Cells‑biblioteket.
- Hur du sparar den genererade presentationen och verifierar resultatet.
- Tips för att hantera arbetsböcker utan former, justera bildstorlek och felsöka versionskonflikter.

Inga externa verktyg, ingen COM‑interop, bara ren .NET‑kod som körs var som helst där .NET Core eller .NET 5+ stöds.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. **Aspose.Cells for .NET** (biblioteket som tillhandahåller `SaveToPresentation`). Du kan hämta det från NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. Ett aktuellt .NET SDK (6.0 eller senare rekommenderas).  
3. En Excel‑fil (`shapes.xlsx`) som innehåller minst en form, ett diagram eller en bild som du vill ha på en bild.

Det är allt—ingen Office‑installation, inga licensproblem för detta demoändamål (den fria utvärderingen fungerar bra).

---

## Steg 1: Ladda Excel‑arbetsboken (Create PowerPoint from Excel)

Det första vi behöver är ett `Workbook`‑objekt som pekar på källfilen. Detta objekt representerar hela Excel‑dokumentet, inklusive alla arbetsblad, diagram och inbäddade objekt.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Pro tip:** Om du är osäker på om filen finns, omslut konstruktorn med en `try/catch` och ge ett hjälpsamt felmeddelande. Det sparar dig från ett kryptiskt `FileNotFoundException` senare.

---

## Steg 2: Konvertera arbetsboken till en PowerPoint‑presentation (Export Excel to PPT)

Aspose.Cells levereras med en inbyggd exportör som omvandlar hela arbetsboken—eller bara utvalda blad—till en PowerPoint‑presentation. Metoden `SaveToPresentation` gör det tunga arbetet.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

Om du bara behöver **generate ppt from excel** för ett delmängd av blad, kan du använda överlagringen som accepterar en `SheetOptions`‑samling. För de flesta scenarier är standardkonverteringen tillräcklig.

---

## Steg 3: Spara den genererade presentationen (How to Convert Excel to PPTX)

Nu när vi har en `Presentation`‑instans är det enkelt att spara den till disk. Utdata blir en standard `.pptx`‑fil som vilken modern version av PowerPoint som helst kan öppna.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **Vad händer om arbetsboken saknar former?**  
> Exportören kommer fortfarande att skapa bilder, men de blir tomma. Du kan kontrollera `workbook.Worksheets[i].Shapes.Count` innan konvertering och besluta om du ska hoppa över det bladet.

---

## Valfritt: Finjustera utskriften (Advanced Export Excel to PPT)

Ibland är standardbildstorleken (standard 4:3) inte idealisk för widescreen‑presentationer. Du kan justera bildens dimensioner innan du sparar:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

Dessa justeringar visar **how to convert Excel to PowerPoint** med ett professionellt utseende, inte bara en rå dataexport.

---

## Fullständigt fungerande exempel (Alla steg kombinerade)

Nedan är det kompletta, färdiga programmet. Kopiera‑klistra in det i en konsolapp, justera filsökvägarna och tryck **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Förväntat resultat:** Öppna `shapes.pptx` i PowerPoint. Du kommer att se en bild per arbetsblad, där varje bevarar de ursprungliga diagrammen, bilderna och andra former. Den valfria titelsliden visas i början, vilket ger presentationen en polerad introduktion.

---

## Vanliga frågor & edge‑cases

| Question | Answer |
|----------|--------|
| *What if I need only a single sheet?* | Använd `Workbook.Worksheets[0]` och anropa `SaveToPresentation` på det bladet via `SheetOptions`. |
| *Can I preserve Excel formulas?* | Nej—formler renderas som statiska värden på bilden. Om du behöver live‑data, överväg att länka PPTX‑filen till Excel‑filen senare. |
| *Does this work on Linux/macOS?* | Ja. Aspose.Cells är plattformsoberoende; installera bara .NET‑runtime och du är klar. |
| *What about password‑protected workbooks?* | Ladda med `LoadOptions` som inkluderar lösenordet innan du anropar `SaveToPresentation`. |
| *Why am I getting blank slides?* | Kontrollera att arbetsboken faktiskt innehåller former (`Shapes.Count > 0`). Tomma bilder skapas för tomma blad. |

---

## Slutsats

Du har nu en tydlig, end‑to‑end‑lösning för **create PowerPoint from Excel** med C#. Genom att ladda arbetsboken, anropa `SaveToPresentation` och spara resultatet kan du **convert Excel to PowerPoint**, **export Excel to PPT** och **generate PPT from Excel** med bara några få rader.  

Från här kan du utforska:

- Lägga till animationer i de genererade bilderna med Aspose.Slides.  
- Automatisera hela pipeline‑processen (t.ex. läsa filer från en mapp, batch‑konvertera dem).  
- Integrera koden i ett ASP.NET Core‑API så att användare kan ladda upp en Excel‑fil och få en PPTX direkt.

Prova det, justera bildstorleken, lägg till en egen titel—det finns gott om utrymme att göra utskriften helt din egen. Har du frågor eller stöter på problem? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}