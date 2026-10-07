---
category: general
date: 2026-05-04
description: Hur man uppdaterar en pivottabell i C# och exporterar den som PNG, sedan
  infogar bilden i kalkylbladet. Följ den här steg‑för‑steg‑guiden med komplett kod.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: sv
og_description: Hur uppdaterar man pivottabellen i C#? Lär dig att exportera pivottabellen
  som en bild och infoga den i ett kalkylblad med kompletta kodexempel.
og_title: Hur man uppdaterar Pivot i C# – Exportera och infoga som bild
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hur man uppdaterar Pivot i C# – Exportera och infoga som bild
url: /sv/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man uppdaterar en pivottabell i C# – Exportera och infoga som bild

Att uppdatera en pivottabell i C# är ett vanligt hinder när du automatiserar Excel‑rapporter. I den här guiden kommer du att se exakt **hur du uppdaterar en pivottabell**, exportera den som en PNG och placera den bilden i en arbetsblads‑platshållare – allt med ett enda körbart program.

Om du också undrar *hur man exporterar en pivottabell* eller behöver **infoga bild i arbetsblad**, är du på rätt plats. Vi går igenom varje rad, förklarar varför den är viktig, och täcker även några kantfall du kan stöta på i verkliga projekt.

---

## Vad du behöver

- **Aspose.Cells for .NET** (biblioteket som tillhandahåller `Workbook`, `Worksheet`, `ImageOrPrintOptions` osv.). Du kan hämta det från NuGet: `Install-Package Aspose.Cells`.
- .NET 6 eller senare (koden nedan är riktad mot .NET 6, men vilken recent version som helst fungerar).
- En grundläggande förståelse för C# och fil‑I/O – inget avancerat.

Det är allt. Inga extra DLL‑filer, ingen COM‑interop, bara en ren C#‑konsolapp.

---

## Steg 1 – Ladda Excel‑arbetsbok i C#‑stil

Först måste vi öppna källfilen. Här sker delen **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Varför?**  
> Att ladda arbetsboken ger oss åtkomst till dess arbetsblad, pivottabeller och bild‑platshållare. Om filen inte hittas kastar Aspose ett tydligt `FileNotFoundException`, som du kan fånga för ett mer användarvänligt gränssnitt.

---

## Steg 2 – Förbered bildalternativ för att exportera pivottabell

Nu talar vi om för Aspose hur den exporterade bilden ska se ut. Detta är kärnan i **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Proffstips:**  
> Om du behöver en JPEG för mindre filstorlek, ändra `SaveFormat.Png` till `SaveFormat.Jpeg` och justera `Quality` därefter.

---

## Steg 3 – Kod för att uppdatera pivottabell

En föråldrad pivottabell visar gammal data. Genom att uppdatera den garanteras att bilden speglar de senaste siffrorna.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Varför uppdatera?**  
> Pivottabeller cachar källdata när de skapas. Om det underliggande arbetsbladet ändras (t.ex. nya rader läggs till) blir cachen föråldrad. Genom att anropa `Refresh()` tvingas Aspose att läsa om källintervallet, så att den exporterade bilden inte fastnar med föråldrade summor.

---

## Steg 4 – Konvertera den uppdaterade pivottabellen till en bild

Här är den magiska raden som faktiskt **export pivot** till en byte‑array.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Vad du får:**  
> `pivotImage` innehåller nu en PNG‑kodad bild av pivottabellen, redo att skrivas till disk eller bäddas in någon annanstans.

---

## Steg 5 – Infoga bild i arbetsblad

Detta är där vi **insert image into worksheet**. Vi placerar bilden i den första bild‑platshållaren (om en sådan finns).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Varför använda en platshållare?**  
> Många Excel‑mallar levereras med en förformaterad bildform (storlek, kant, position). Genom att rikta in oss på `Pictures[0]` behåller vi layouten. Om mallen saknar en platshållare skapar fallback‑alternativet en ny bild förankrad i cell A1.

---

## Steg 6 – Spara arbetsboken (valfritt)

Till sist sparas ändringarna. Du kan skriva över originalet eller spara till en ny fil.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Förväntat resultat:**  
> Öppna `output.xlsx` så ser du att pivottabellen är uppdaterad, exporterad som en skarp PNG och visas i den första bildplatsen. Resten av arbetsboken förblir oförändrad.

---

## Fullt fungerande exempel (klart att kopiera och klistra in)

Nedan är den kompletta kodblocket som du kan klistra in i ett nytt konsolprojekt. Inga delar saknas.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Kör programmet, öppna den resulterande filen och verifiera att pivottabellen speglar den senaste datan och visas som en högupplöst bild.

---

## Vanliga frågor & kantfall

| Question | Answer |
|----------|--------|
| **Vad händer om arbetsboken har flera arbetsblad?** | Ändra `workbook.Worksheets[0]` till rätt index eller namn (`workbook.Worksheets["Sheet2"]`). |
| **Kan jag exportera flera pivottabeller?** | Loopa igenom `worksheet.PivotTables` och upprepa steg 3‑4 för varje. Spara varje bild i en separat platshållare eller kombinera dem i ett blad. |
| **Vad händer med stora pivottabeller som belastar minnet?** | Använd `ImageOrPrintOptions` med lägre DPI eller exportera till JPEG för att minska byte‑array‑storleken. |
| **Behöver jag avyttra något?** | Aspose‑objekt är hanterade; `using`‑satsen är inte obligatorisk, men du kan omsluta `Workbook` i ett `using`‑block om du föredrar deterministisk rensning. |
| **Är detta kompatibelt med .NET Core?** | Ja. Aspose.Cells stödjer .NET Core, .NET 5/6 och .NET Framework. Referera bara till rätt NuGet‑paket. |

---

## Tips & bästa praxis

- **Validera sökvägar**: Använd `Path.Combine` och `Environment.GetFolderPath` för att undvika hårdkodade separatorer.
- **Felsökning**: Omslut hela `Main`‑kroppen i ett `try/catch` och logga `Exception.Message` för produktionsskript.
- **Mall‑design**: Placera en transparent bildform där du vill ha pivottabellens bild; detta bevarar kolumnbredder och radhöjder.
- **Prestanda**: Om du bara behöver bilden kan du hoppa över att spara arbetsboken helt och skriva `pivotImage` till en separat PNG‑fil.

---

## Slutsats

Du vet nu **how to refresh pivot** i C#, exportera den uppdaterade vyn som en bild och **insert image into worksheet** sömlöst. Den kompletta lösningen – att ladda arbetsboken, ställa in exportalternativ, uppdatera pivottabellen, konvertera till PNG och spara filen – täcker hela arbetsflödet du efterfrågade.

Redo för nästa utmaning? Prova att kombinera **how to export pivot** med batch‑bearbetning av flera filer, eller utforska **refresh pivot table code** för dynamiska datakällor som databaser eller CSV‑flöden. Samma mönster gäller: ladda, uppdatera, exportera, infoga, spara.

Lycka till med kodningen, och må dina Excel‑automatiseringar förbli fräscha och bildperfekta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}