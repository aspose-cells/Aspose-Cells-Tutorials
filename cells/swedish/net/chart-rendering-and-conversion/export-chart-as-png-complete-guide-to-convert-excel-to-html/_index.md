---
category: general
date: 2026-06-30
description: Exportera diagram som PNG medan du konverterar Excel till HTML med Aspose.Cells.
  Lär dig att bädda in bilder som Base64 och spara arbetsboken som HTML på några minuter.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: sv
og_description: Exportera diagram som PNG och bädda in bilder som Base64 när du konverterar
  Excel till HTML. Följ den här steg‑för‑steg C#‑handledningen för att enkelt spara
  arbetsboken som HTML.
og_title: Exportera diagram som PNG – Konvertera Excel till HTML med Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Exportera diagram som PNG – Komplett guide för att konvertera Excel till HTML
  med Aspose.Cells
url: /sv/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Chart as PNG – Komplett guide för att konvertera Excel till HTML med Aspose.Cells

Har du någonsin undrat hur man **export chart as PNG** direkt från en Excel‑arbetsbok samtidigt som du omvandlar hela bladet till ren, responsiv HTML? Du är inte ensam. Många utvecklare stöter på problem när de behöver en webb‑klar rapport som visar diagram utan att jonglera med separata bildfiler. Den goda nyheten är att Aspose.Cells gör detta enkelt.

I den här handledningen går vi igenom de exakta stegen för att **convert Excel to HTML**, **embed images as Base64**, och slutligen **save workbook as HTML**—allt medan vi säkerställer att varje diagram sparas som en PNG‑bild. När du är klar har du en enda HTML‑fil som du kan lägga in på vilken webbsida som helst, och varje diagram visas omedelbart utan extra resurser.

## What You’ll Learn

- Hur du laddar en befintlig arbetsbok som redan innehåller diagram.  
- Vilka `HtmlSaveOptions`‑flaggor som styr bildexport, diagramformat och responsivitet.  
- Den exakta koden som behövs för att **export chart as PNG** och bädda in dessa PNG‑filer som Base64‑strängar.  
- Hur du **save workbook as HTML** med ett enda metodanrop.  
- Tips för felsökning av vanliga fallgropar, som saknade diagrambilder eller för stora Base64‑strängar.  

**Prerequisites:**  
- .NET 6+ (eller .NET Framework 4.6+) installerat.  
- En giltig Aspose.Cells‑licens (eller en tillfällig utvärderingsnyckel).  
- Grundläggande kunskap om C# och Visual Studio (eller din favoriteditor).  

Om någon av dessa punkter känns obekanta, pausa ett ögonblick och sätt upp dem; resten av guiden förutsätter att de är klara.

---

## Step 1: Set Up Your Project and Install Aspose.Cells

Innan vi kan **export chart as PNG** behöver vi ett C#‑projekt som refererar till Aspose.Cells‑biblioteket.

1. Öppna Visual Studio och skapa en ny **Console App** (`dotnet new console`).  
2. Lägg till Aspose.Cells‑NuGet‑paketet:

```bash
dotnet add package Aspose.Cells
```

3. (Valfritt) Om du har en licensfil, placera den i projektets rot och aktivera den vid körning:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Pro tip:** Håll licensfilen utanför källkontrollen. Använd miljövariabler eller säkra hemlagret för produktion.

---

## Step 2: Load the Workbook That Contains the Chart

Nu laddar vi Excel‑filen som redan har diagrammet vi vill **export chart as PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Why this matters:** Att ladda arbetsboken tidigt ger oss åtkomst till alla kalkylblad, diagram och inbäddade objekt. Om arbetsboken misslyckas med att laddas kommer nästa steg **export chart to PNG** aldrig att köras.

---

## Step 3: Configure HTML Save Options

Kärnan i lösningen finns i `HtmlSaveOptions`. Genom att växla några egenskaper kan vi:

- **ExportChartImageFormat = ImageFormat.Png** → säkerställer att varje diagram blir en PNG.  
- **ExportImagesAsBase64 = true** → bäddar in PNG‑data direkt i HTML, eliminerar externa filer.  
- **IsResponsive = true** → gör de genererade tabellerna anpassningsbara för mobila skärmar.  
- **ExportPrintingHeadersFooters = false** → tar bort onödig utskriftsmetadata.  

Här är den fullständiga konfigurationen:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Why These Settings?

- **ExportChartImageFormat = ImageFormat.Png** är det enda sättet att garantera en förlustfri, webbsäker diagrambild.  
- **ExportImagesAsBase64 = true** betyder att du kan **embed images as Base64**, vilket är perfekt för e‑postrapporter eller enkel‑fil‑distributioner.  
- **IsResponsive = true** löser ett vanligt klagomål: tabeller som rinner över på smartphones.  
- **ExportPrintingHeadersFooters = false** håller HTML‑filen lättviktig—ingen dold skrivarinfo som aldrig används på webben.  

---

## Step 4: Save the Workbook as HTML

Med alternativen satta är den sista raden ett enda anrop som både **convert excel to html** och **export chart as PNG** bakom kulisserna.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

När detta anrop är klart har du en fil som heter `Report.html`. Öppna den i vilken webbläsare som helst, så ser du:

- All data från kalkylbladen renderade som rena HTML‑tabeller.  
- Varje diagram visas som en inbäddad PNG‑bild (tack vare Base64‑inbäddning).  
- Inga extra bildfiler ligger bredvid HTML‑filen.  

### Expected Output

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Lägg märke till attributet `src="data:image/png;base64,..."`—det är **embed images as base64**‑magin i arbete. Inga separata `.png`‑filer skapas på disken.

---

## Step 5: Verify the PNG Export and Tweak If Needed

Ibland kan ett diagram se lite felaktigt ut efter konverteringen, särskilt om det använder anpassade typsnitt eller komplexa gradienter. Så här dubbelkollar du:

1. Öppna den genererade HTML‑filen i Chrome. Högerklicka på diagrammet och välj **Open image in new tab**. URL‑adressen kommer fortfarande att börja med `data:image/png;base64,`.  
2. Om bilden blir suddig, överväg att öka diagrammets upplösning innan du sparar:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. För diagram som förlitar sig på externa datakällor, se till att arbetsboken är helt uppdaterad innan du sparar:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Dessa justeringar säkerställer att steget **export excel chart to png** ger skarpa, produktionsklara grafik.

---

## Step 6: Deploy the HTML Anywhere

Eftersom alla bilder är inbäddade kan du nu:

- E‑mailla HTML‑filen som en enda bilaga.  
- Klistra in HTML‑koden i ett CMS som accepterar rå kod.  
- Värda den på en statisk webbplats utan att oroa dig för saknade PNG‑filer.  

Om du någonsin behöver PNG‑filerna som separata resurser (kanske för en PDF senare), kan du byta `ExportImagesAsBase64` till `false` och låta `HtmlSaveOptions` peka på en utmatningsmapp för bilder.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Nu kommer HTML‑filen att referera till externa PNG‑filer, men fortfarande säkerställa **export chart as png** samtidigt som du får individuella bildfiler för andra användningsområden.

---

## Common Pitfalls & How to Avoid Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Chart missing from HTML | `ExportChartImageFormat` left at default (`Jpeg`) and the browser blocks mixed content. | Set `ExportChartImageFormat = ImageFormat.Png`. |
| HTML file huge (several MB) | Large charts or many high‑resolution images embedded as Base64. | Reduce `htmlOptions.ImageResolution` or compress the chart in Excel before conversion. |
| Tables overflow on mobile | `IsResponsive` not enabled. | Ensure `IsResponsive = true` in `HtmlSaveOptions`. |
| Base64 strings contain newline characters | Older .NET versions may wrap long strings. | Upgrade to .NET 6+ or set `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bonus: Wrap It All in a Reusable Method

Om du kommer att göra den här konverteringen ofta, kapsla in logiken:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Nu kan du anropa `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` var som helst i din kodbas.

---

## Conclusion

Du har precis lärt dig hur du **export chart as PNG** samtidigt som du **convert Excel to HTML**, **embed images as Base64**, och **save workbook as HTML** med Aspose.Cells. Huvudpoängen är att några väl valda `HtmlSaveOptions`‑inställningar ger dig en enda, självständig HTML‑fil som fungerar på alla enheter—utan extra PNG‑filer, utan röriga mappar.

Redo för nästa utmaning? Prova att kombinera detta tillvägagångssätt med **export excel chart to PNG** för PDF‑generering, eller experimentera med anpassad CSS för att styla tabellerna ytterligare. Himlen är gränsen när du kontrollerar både data och presentation programatiskt.

Känn dig fri att lämna en kommentar om du stöter på problem, eller dela hur du har anpassat detta mönster i dina egna projekt. Happy coding!

## What Should You Learn Next?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}