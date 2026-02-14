---
category: general
date: 2026-02-14
description: Hur man exporterar en pivottabell från en Excel-arbetsbok till PNG med
  Aspose.Cells. Lär dig hur du laddar en Excel-arbetsbok, renderar pivottabellen till
  en bild och sparar pivottabellens bild utan ansträngning.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: sv
og_description: hur man exporterar en pivottabell från Excel till PNG i C#. Den här
  guiden visar hur du laddar en Excel-arbetsbok, renderar en pivottabell till PNG
  och sparar pivottabellens bild.
og_title: hur man exporterar pivot till png i C# – Komplett handledning
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man exporterar pivot till PNG i C# – Steg‑för‑steg‑guide
url: /sv/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man exporterar pivot till PNG i C# – Komplett handledning

Har du någonsin funderat **hur man exporterar pivot** från ett Excel‑blad som en skarp PNG‑fil? Du är inte ensam—utvecklare behöver ofta en snabb visuell av en pivottabell för rapporter, instrumentpaneler eller e‑postbilagor. Den goda nyheten? Med Aspose.Cells kan du ladda Excel‑arbetsboken, hämta den första pivottabellen, omvandla den till en bild och **spara pivottabellens bild** med bara några rader C#.

I den här handledningen går vi igenom allt du behöver: från grunderna för **load excel workbook**, till att rendera en **pivot table to png**, och slutligen spara filen på disk. När du är klar har du ett självständigt, körbart program som du kan lägga in i vilket .NET‑projekt som helst.

---

## Vad du behöver

- **.NET 6 eller senare** (koden fungerar även på .NET Framework 4.7+)
- **Aspose.Cells for .NET** NuGet‑paket (version 23.12 vid skrivande stund)
- En Excel‑fil (`input.xlsx`) som innehåller minst en pivottabell
- En Visual Studio‑ eller VS Code‑miljö som du är bekväm med

Inga extra bibliotek, ingen COM‑interop och ingen Excel‑installation krävs—Aspose.Cells hanterar allt i minnet.

---

## Steg 1 – Ladda Excel‑arbetsboken

Det första är att läsa in arbetsboken i minnet. Det är här nyckelordet **load excel workbook** glänser.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Varför detta är viktigt:**  
> Att ladda arbetsboken en gång gör operationen snabb och undviker att låsa källfilen. Aspose.Cells läser filen till en hanterad ström, så du kan även ladda från en byte‑array eller en nätverksplats senare.

---

## Steg 2 – Rendera pivottabellen till en bild

Nu när arbetsboken är i minnet kan vi komma åt dess pivottabeller. API‑et erbjuder en praktisk `ToImage()`‑metod som returnerar en `System.Drawing.Image`.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Proffstips:** Om din arbetsbok innehåller flera pivottabeller, loopa helt enkelt över `worksheet.PivotTables` och exportera var och en. Anropet `ToImage()` respekterar den aktuella vyn (filter, slicers, etc.), så du får exakt det som användaren ser.

---

## Steg 3 – Spara den genererade PNG‑filen

Till sist sparar vi bitmapen till disk. `Save`‑överladdningen väljer automatiskt formatet baserat på filändelsen.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

När programmet körs skapas en `pivot.png` som ser exakt ut som pivottabellen i Excel. Öppna den med någon bildvisare så ser du rader, kolumner och totaler renderade pixel‑perfekt.

---

## Hantera vanliga kantfall

### Flera kalkylblad eller pivottabeller

Om din arbetsbok lagrar pivottabellen på ett annat blad, ändra bladindexet eller använd bladnamnet:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Loop sedan:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Stora pivottabeller

För mycket stora pivottabeller kan standardbildstorleken bli enorm. Du kan kontrollera renderingsstorleken genom att justera bladets zoomfaktor innan du anropar `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Minneshantering

`System.Drawing.Image` implementerar `IDisposable`. I produktionskod omsluter du bilden i ett `using`‑block för att snabbt frigöra inhemska resurser:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Fullt fungerande exempel

Nedan är det kompletta, körklara programmet. Klistra in det i ett nytt konsolprojekt, justera filsökvägarna och tryck **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Förväntat resultat:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

Och filen `pivot.png` kommer att innehålla en visuell kopia av den ursprungliga pivottabellen.

---

## Vanliga frågor

- **Fungerar detta med .xlsx‑filer som innehåller diagram?**  
  Ja. `ToImage()`‑metoden bryr sig bara om pivottabellens layout; diagram påverkas inte.

- **Kan jag exportera till JPEG eller BMP istället för PNG?**  
  Absolut—byt bara `ImageFormat`‑argumentet i `Save`. PNG är förlustfri, vilket är varför vi rekommenderar det för skarpa data.

- **Vad händer om arbetsboken är lösenordsskyddad?**  
  Ladda den med lösenords‑överladdningen:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Sammanfattning

Vi har just gått igenom **hur man exporterar pivot** från en Excel‑fil till en PNG‑bild med Aspose.Cells. Stegen—**load excel workbook**, lokalisera **pivot table to png**, och **save pivot image**—är enkla, men ändå tillräckligt kraftfulla för verkliga rapporteringspipeline.

Nästa steg kan du utforska:

- Automatisera exporten för alla pivottabeller i en mapp (export excel pivot in bulk)  
- Bädda in PNG‑filen i en PDF eller HTML‑e‑post (kombinera med iTextSharp eller Razor)  
- Lägga till vattenstämplar eller anpassad stil på den exporterade bilden  

Prova dem och låt bilderna tala i ditt nästa instrumentpanel.

![exempel på export av pivot](assets/pivot-export-example.png "exempel på export av pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}