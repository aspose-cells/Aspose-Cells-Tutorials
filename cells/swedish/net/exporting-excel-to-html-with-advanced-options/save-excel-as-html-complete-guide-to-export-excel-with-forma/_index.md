---
category: general
date: 2026-07-14
description: Spara Excel som HTML snabbt och lär dig hur du konverterar Excel till
  HTML med full formatering. Exportera Excel med formatering med Aspose.Cells på några
  minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: sv
lastmod: 2026-07-14
og_description: Spara Excel som HTML direkt. Den här guiden visar hur du konverterar
  Excel till HTML samtidigt som du bevarar stilar och möjliggör nummerformatering
  med Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Spara Excel som HTML – Steg‑för‑steg-export med full formatering
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Spara Excel som HTML – Komplett guide för att exportera Excel med formatering
url: /sv/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara Excel som HTML – Komplett guide för att exportera Excel med formatering

Har du någonsin undrat hur du **sparar Excel som HTML** utan att förlora färger, kantlinjer eller talformat? Du är inte ensam. I många rapporteringsscenarier behöver du en webb‑klar vy av en arbetsbok, och det snabbaste sättet är att exportera filen direkt till HTML.  

I den här handledningen går vi igenom de exakta stegen för att **konvertera Excel till HTML** med Aspose.Cells, aktivera Grid.js‑nummerformatering och säkerställa att resultatet ser exakt ut som den ursprungliga kalkylbladet. När du är klar har du en färdig HTML‑fil som du kan leverera från vilken webbserver som helst.

## Vad du kommer att lära dig

- Förutsättningar och paketinstallation  
- Laddar en befintlig arbetsbok (eller skapar en på flygande fot)  
- Konfigurerar `HtmlSaveOptions` för perfekt visuell återgivning  
- Aktiverar `GridJsOptions.EnableNumberFormat` för att behålla numerisk stil intakt  
- Sparar filen och verifierar resultatet  

Om du någonsin har försökt **exportera Excel med formatering** med en generisk CSV‑dump, vet du hur frustrerande det kan vara när siffror blir ren text. Den här guiden undviker den fallgroparna.

---

## Förutsättningar – Ställ in din utvecklingsmiljö

Innan vi dyker ner i koden, se till att du har:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 eller senare (handledningen använder .NET 6) | Moderna API:er och bättre prestanda |
| Visual Studio 2022 (eller VS Code med C#‑tillägg) | Bekväm redigering och felsökning |
| Aspose.Cells för .NET NuGet‑paket | Biblioteket som driver `HtmlSaveOptions` och `GridJsOptions` |
| En exempel‑Excel‑fil (`sample.xlsx`) eller en arbetsbok du genererar i kod | Källan du kommer att konvertera |

Installera Aspose.Cells med följande kommando i Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

> **Proffstips:** Om du kör i en CI‑pipeline, lägg till samma `dotnet add package`‑rad i ditt byggskript så att beroendet alltid finns.

---

## Steg 1: Ladda eller skapa en arbetsbok

Du kan antingen ladda en befintlig fil eller bygga en programatiskt. Här är ett minimalt exempel som skapar en arbetsbok med några formaterade celler så att du kan se formateringen överleva exporten.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Varför detta är viktigt:** Genom att explicit sätta talformat kommer du senare att se att `GridJsOptions.EnableNumberFormat` behåller dessa format i HTML‑utdata.

---

## Steg 2: Konfigurera HTML‑sparaalternativ

Nu skapar vi en `HtmlSaveOptions`‑instans. Detta objekt talar om för Aspose.Cells exakt hur du vill att HTML ska renderas.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Aktivera Grid.js‑nummerformatering

Om du planerar att bädda in HTML i en sida som använder **Grid.js** för interaktiva tabeller, vill du att siffrorna ska behålla sin formatering (t.ex. valutasymboler, tusentalsavgränsare). Följande rad gör exakt det:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Vad händer under huven?** `EnableNumberFormat` injicerar ett litet JavaScript‑snutt som instruerar Grid.js att tolka cellens `data-format`‑attribut, vilket bevarar Excel‑stilens formatering i webbläsaren.

---

## Steg 3: Spara arbetsboken som en HTML‑fil

När arbetsboken är klar och alternativen justerade, skriver den sista raden HTML‑filen till disk.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Running the program produces an `gridjs.html` file that looks like this (simplified view):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Öppna filen i vilken webbläsare som helst så ser du ett snyggt formaterat bord, komplett med ljusgrå bakgrund i rubriken och valutaformatering. Om du placerar sidan på en webbplats som redan laddar Grid.js kommer siffrorna automatiskt att visas med rätt kommatecken och symboler.

---

## Vanliga fallgropar när du **konverterar Excel till HTML**

| Issue | Why it occurs | How to avoid it |
|-------|---------------|-----------------|
| **Förlorade formler** | HTML är statisk; formler blir rena värden. | Om du behöver levande beräkningar, behåll arbetsboken på servern och använd JavaScript‑bibliotek som SheetJS. |
| **Saknade bilder** | Bilder lagras som separata resurser. | Ställ in `HtmlSaveOptions.ExportImagesAsBase64 = true` för att bädda in dem direkt. |
| **Stora filer** | Stora arbetsböcker genererar enorm HTML + JS. | Använd `ExportOnlyVisibleSheets` eller dela upp i flera sidor via `HtmlSaveOptions.OnePagePerSheet`. |
| **Felaktig tal‑lokal** | Excel lagrar siffror i invariant kultur, webbläsare kan tillämpa lokala inställningar. | Ställ explicit in `htmlOptions.Encoding = Encoding.UTF8` och använd `GridJsOptions.EnableNumberFormat`. |

---

## Avancerat: Exportera flera blad med individuella Grid.js‑instanser

Om din arbetsbok innehåller flera blad och du vill att varje ska bli sin egen Grid.js‑tabell, kan du loopa igenom arbetsbladen och spara varje separat:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Varje fil kommer att innehålla sitt eget `<table class="gridjs-table">`‑element, redo för oberoende manipulation.

---

## Verifiera resultatet – Snabbchecklista

1. **Stil intakt?** Jämför cellbakgrundsfärger och kantlinjer med den ursprungliga Excel‑vyn.  
2. **Talformat bevarade?** Leta efter `data-format`‑attributet på `<td>`‑elementen.  
3. **Bilder visas?** Om du exporterade bilder som Base64 bör de visas inline.  
4. **Webbläsarkonsol ren?** Inga JavaScript‑fel relaterade till Grid.js.  

Om någon av dessa kontroller misslyckas, gå tillbaka till motsvarande `HtmlSaveOptions`‑egenskap – de flesta problem beror på en saknad flagga.

---

## Slutsats

Du har nu en solid, produktionsklar metod för att **spara Excel som HTML** samtidigt som du behåller varje stil, kantlinje och numerisk representation intakt. Genom att konfigurera `HtmlSaveOptions` och slå på `GridJsOptions.EnableNumberFormat` har du förvandlat ett statiskt kalkylblad till ett webb‑vänligt bord som fungerar sömlöst med Grid.js.

Kort sagt visar den här handledningen hur du **konverterar Excel till HTML** och **exporterar Excel med formatering** med Aspose.Cells. Känn dig fri att experimentera: prova olika teman, bädda in diagram eller till och med leverera HTML via en ASP.NET‑endpoint för konvertering i realtid.

---

## Vad blir nästa?

- **Utforska andra exportformat**: PDF, PNG eller CSV via `Workbook.Save`.  
- **Integrera med ASP.NET Core**: Returnera HTML‑strängen direkt från en controller‑action.  
- **Kombinera med SheetJS**: Ladda den genererade HTML‑filen tillbaka in i en JavaScript‑arbetsbok för redigering på klientsidan.  

Om du stöter på problem, lämna en kommentar nedan eller kolla Aspose.Cells‑dokumentationen för djupare konfigurationsalternativ. Lycka till med kodandet!

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur du exporterar Excel till HTML med rutlinjer med Aspose.Cells för .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Exportera Excel till HTML och bevara kantlinjestilar med Aspose.Cells för Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Konvertera HTML till Excel med Aspose.Cells .NET: En omfattande guide](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}