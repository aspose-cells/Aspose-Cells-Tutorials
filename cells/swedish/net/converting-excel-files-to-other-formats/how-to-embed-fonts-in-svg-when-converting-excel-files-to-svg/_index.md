---
category: general
date: 2026-09-15
description: Lär dig hur du bäddar in typsnitt i SVG och exporterar Excel-diagram
  till PowerPoint, inklusive konvertering av XLSX till SVG och konvertering av XLSX
  till PPTX med kompletta kodexempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: sv
lastmod: 2026-09-15
og_description: Bädda in typsnitt i SVG och exportera Excel‑diagram till PowerPoint
  med steg‑för‑steg C#‑kod. Konvertera XLSX till SVG och XLSX till PPTX snabbt och
  pålitligt.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Bädda in typsnitt i SVG och exportera Excel-diagram till PowerPoint – komplett
  guide
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man bäddar in teckensnitt i SVG när man konverterar Excel-filer till SVG
  och PowerPoint
url: /sv/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man bäddar in typsnitt i SVG när man konverterar Excel-filer till SVG och PowerPoint  

If you need to **embed fonts in SVG** while converting an Excel workbook, this guide shows you exactly how to do it. You’ll also learn how to **export Excel chart to PowerPoint**, and how to **convert XLSX to SVG** and **convert XLSX to PPTX** with editable charts.  

Att arbeta med Excel-data programatiskt innebär ofta att du måste flytta samma visuella innehåll mellan olika filformat. Att manuellt återskapa ett diagram i PowerPoint eller återapplicera typsnitt i en SVG är felbenäget och tidskrävande. I slutet av den här handledningen kommer du att ha ett enda, återanvändbart C#‑snutt som:

* Sparar en arbetsbok som en SVG‑fil med inbäddade typsnitt och font‑variation selectors.  
* Exporterar samma arbetsbok till en PPTX‑fil där diagrammet förblir redigerbart.  

Det enda förutsättningen är en recent version of **Aspose.Cells for .NET** (2024‑x eller senare) och en .NET‑utvecklingsmiljö som Visual Studio 2022.

---

## Vad du behöver  

* .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.8).  
* Aspose.Cells for .NET NuGet‑paket (`Install-Package Aspose.Cells`).  
* En Excel‑fil (`input.xlsx`) som innehåller minst ett diagram.  
* Skrivbehörighet till utmatningskatalogen.  

---

## Bädda in typsnitt i SVG vid konvertering av XLSX till SVG  

Att bädda in typsnitt säkerställer att SVG renderas korrekt på alla enheter, även om målssystemet saknar de ursprungliga typsnitten. Klassen `SvgSaveOptions` tillhandahåller två flaggor som möjliggör detta: `EmbedFonts` och `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Varför detta fungerar:**  
* `EmbedFonts = true` kopierar typsnitts‑filerna till SVG‑filens `<defs>`‑sektion, vilket eliminerar externa beroenden.  
* `FontVariationSelectors = true` lägger till de nödvändiga selector‑erna för typsnitt som stödjer OpenType‑funktioner, och bevarar glyf‑variationer såsom ligaturer.  

**Förväntat resultat:** Öppna `WithFonts.svg` i någon modern webbläsare; texten i diagrammet eller cellerna visas med exakt samma typsnitt som används i Excel, även på maskiner som inte har det typsnittet installerat.

---

## Exportera Excel‑diagram till PowerPoint med redigerbara diagram  

När du behöver bädda in ett diagram i en PowerPoint‑bild men ändå låta mottagaren redigera diagramdata, erbjuder Aspose.Cells `PptxSaveOptions` flaggan `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Varför detta är viktigt:**  
Att sätta `ExportEditableChart` till `true` sparar diagrammet som ett Office Open XML‑diagramobjekt istället för en statisk bild. När du öppnar `EditableChart.pptx` i PowerPoint kan du högerklicka på diagrammet → **Edit Data** och ändra serierna precis som i ett inbyggt PowerPoint‑diagram.

**Verifieringssteg:**  

1. Öppna `EditableChart.pptx` i PowerPoint.  
2. Hitta bilden som innehåller diagrammet.  
3. Välj **Chart Tools → Design → Edit Data**.  
4. Bekräfta att Excel‑liknande datagrid visas och att du kan ändra värden.

---

## Konvertera XLSX till SVG – fullständig arbetsflödesöversikt  

Nedan är en kompakt version som kombinerar inläsning, valfri datamanipulation och sparande som SVG. Använd detta när du bara behöver SVG‑utdata.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Anropa metoden så här:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Tips för kantfall:** Om din arbetsbok innehåller anpassade typsnitt som inte är installerade på servern, bädda in dem manuellt innan du anropar `Save`. Använd `FontInfoCollection` för att lägga till typsnitts‑filerna till `SvgSaveOptions` via egenskapen `CustomFonts` (tillgänglig i nyare Aspose.Cells‑utgåvor).

---

## Konvertera XLSX till PPTX – bevara diagramredigerbarhet  

Följande hjälpfunktion demonstrerar **convert XLSX to PPTX**‑vägen samtidigt som den säkerställer att diagrammet förblir redigerbart.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Användning:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Vanlig fråga:** *Vad händer om min arbetsbok har flera kalkylblad med diagram?*  
**Svar:** Aspose.Cells exporterar det första kalkylbladet som standard. För att inkludera ytterligare blad, iterera över `workbook.Worksheets`, kopiera varje diagram till en ny bild, och spara varje bild individuellt med `Presentation`‑objekt från Aspose.Slides. Detta avancerade scenario ligger utanför det grundläggande flödet “save workbook as SVG” och “export Excel chart to PowerPoint”, men de centrala flaggorna förblir desamma.

---

## Praktiska tips och fallgropar  

* **Performance:** Att bädda in typsnitt ökar SVG‑filens storlek. Om storlek är ett problem, sätt `EmbedFonts = false` och förlita dig på web‑säkra typsnitt.  
* **Font licensing:** Säkerställ att du har rätt att bädda in de typsnitt du använder; vissa kommersiella typsnitt begränsar inbäddning.  
* **Chart compatibility:** Redigerbara diagram sparas som `chart.xml`‑delar i PPTX‑filen. Mycket komplexa diagram (t.ex. 3‑D‑ eller kombinationsdiagram) kan förlora viss formatering när de redigeras i PowerPoint. Testa de vanligaste diagramtyperna du behöver.  
* **Version mismatches:** Flaggan `ExportEditableChart` kräver Aspose.Cells 20.10 eller senare. Att använda en äldre version faller tyst tillbaka till en raster‑bild.  
* **Thread safety:** Workbook‑objekt är inte trådsäkra. Skapa en ny `Workbook`‑instans per begäran i ett webbtjänstscenario.  

---

## Fullständigt end‑to‑end‑exempel  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

När du kör detta program skapas två filer:

* **WithFonts.svg** – en SVG som renderas exakt som Excel‑vyn, med typsnitt inkluderade.  
* **EditableChart.pptx** – en PowerPoint‑presentation där diagrammet kan redigeras direkt.

---

## Slutsats  

Du vet nu hur du **embed fonts in SVG** när du **convert XLSX to SVG**, och hur du **export Excel chart to PowerPoint** samtidigt som du behåller diagrammet redigerbart. Samma kod visar också ett enkelt sätt att **save workbook as SVG** och **convert XLSX to PPTX** med minimal ansträngning.  

Härifrån kan du utforska ytterligare ämnen såsom:

* Lägga till anpassade typsnitt programatiskt (`svgOptions.CustomFonts`).  
* Batch‑processa flera arbetsböcker i en bakgrundstjänst.  
* Använda Aspose.Slides för att skapa PPTX‑filer med flera bilder som kombinerar flera Excel‑diagram.  

Experimentera med alternativen, anpassa snuttarna till ditt projekt, och njut av pålitliga Excel‑till‑SVG/PPTX‑konverteringar utan manuell efterbehandling. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}