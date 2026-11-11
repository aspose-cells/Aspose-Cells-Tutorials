---
category: general
date: 2026-09-15
description: Skapa en Excel‑arbetsbok i C# och lär dig hur du sparar arbetsboken som
  PDF medan du låter dynamiska arrayer spilla ut med EXPAND‑funktionen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: sv
lastmod: 2026-09-15
og_description: Skapa en Excel-arbetsbok i C# och spara snabbt arbetsboken som PDF
  samtidigt som du använder EXPAND-funktionen för att spilla en dynamisk matris.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Skapa Excel-arbetsbok och spara som PDF med dynamiska arrayer
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Skapa Excel-arbetsbok och spara som PDF med dynamiska arrayer
url: /sv/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok och spara som PDF med dynamiska arrayer

Om du behöver **create Excel workbook** programatiskt och sedan **save workbook as PDF**, visar den här guiden en komplett, end‑to‑end‑lösning i C#. Du får också se hur du **spill dynamic array**‑resultat genom att använda **EXPAND function**, vilket är det moderna sättet att generera arrayer utan VBA.  

Oavsett om du bygger en rapporteringstjänst, en exportfunktion för ett ERP‑system eller en datadriven instrumentpanel, låter stegen nedan dig skapa en arbetsbok, fylla den med smart‑marker‑data och producera en PDF som bevarar avancerade teckensnittsegenskaper.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.8)
* En aktuell version av **Aspose.Cells for .NET** (v25.8 eller nyare) – den tillhandahåller `Workbook`, `PdfSaveOptions` och `SmartMarkerProcessor`.
* En IDE såsom Visual Studio 2022 (vilken som helst redigerare som kan kompilera C# fungerar).

Add the NuGet package to your project:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Steg 1: Skapa Excel-arbetsbok och konfigurera det första kalkylbladet

Den första uppgiften är att **create Excel workbook** och få en referens till standardkalkylbladet. Detta kalkylblad kommer att innehålla den dynamiska arrayen och Smart Marker‑mallen.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Varför detta är viktigt*: Att instansiera `Workbook` allokerar den interna arbetsboksstrukturen, medan åtkomst till `Worksheets[0]` ger dig ett färdigt kalkylblad utan att du behöver lägga till ett manuellt.

## Steg 2: Spill dynamic array med EXPAND‑funktionen

Excels **EXPAND function** kan omvandla en statisk array‑literal till ett spill‑område av valfri storlek. Här ber vi Excel expandera `{1,2,3}` till ett 5‑rad × 1‑kolumn‑område som börjar på `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Varför detta är viktigt*: Att använda `EXPAND` undviker manuella loopar i C#. Motorn beräknar spill‑området och lagrar värdena direkt i kalkylbladet, vilket senare visas i PDF‑filen.

## Steg 3: Spara arbetsbok som PDF samtidigt som du bevarar font variation selectors

När du behöver **save workbook as PDF**, kan du också aktivera avancerade typografiska funktioner som font variation selectors (tillgängliga från Aspose.Cells v25.8). Detta säkerställer att PDF‑filer renderar komplexa skript korrekt.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Varför detta är viktigt*: Att sätta `FontVariationSelectors` till `true` är avgörande för språk som förlitar sig på glyf‑variation (t.ex. kinesiska, japanska, emoji). Den genererade PDF‑filen speglar Excel‑vyn på skärmen.

## Steg 4: Infoga en Smart Marker‑mall som refererar till en nästlad datakälla

Smart Markers låter dig bädda in platshållare direkt i kalkylbladet. Mallen nedan kommer att generera en lista över order och deras artiklar.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Varför detta är viktigt*: Genom att placera mallen i `A1` talar du om för Aspose.Cells var dataexpansionen ska börja. `:`‑syntaxen (`Items:ItemName`) instruerar processorn att iterera över en nästlad samling.

## Steg 5: Definiera den nästlade datakällan (order som innehåller artiklar)

Vi skapar en anonym array av order, där varje order innehåller sin egen samling av artikelobjekt. Detta speglar ett typiskt master‑detail‑scenario.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Varför detta är viktigt*: Den nästlade strukturen demonstrerar **how to create dynamic array in Excel** via Smart Markers, utan att skriva någon VBA eller manuella cell‑loopar.

## Steg 6: Bearbeta Smart Markers och spara den slutgiltiga Excel‑filen

Nu överlämnar vi arbetsboken och datakällan till `SmartMarkerProcessor`. Efter bearbetning ersätts platshållarna med faktiska rader, och vi sparar resultatet som en vanlig `.xlsx`‑fil.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Varför detta är viktigt*: `SmartMarkerProcessor` expanderar automatiskt mallen, skapar de nödvändiga raderna och fyller dem med data. Den slutgiltiga arbetsboken kan öppnas i Excel för att verifiera att varje order och dess artiklar visas korrekt.

## Förväntat resultat

* **VarSelector.pdf** – en PDF‑fil som visar siffrorna 1‑3 som spillar ner fem rader, renderad med eventuella OpenType‑font‑variationer du har aktiverat.
* **NestedSmartMarker.xlsx** – en Excel‑fil med följande rader (börjar på `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF‑versionen behåller samma numeriska spill eftersom kalkylbladsstatusen sparades innan Smart Marker‑bearbetning; du kan upprepa PDF‑sparandet efter bearbetning om du även behöver de slutgiltiga data i PDF.

## Pro‑tips och vanliga fallgropar

| Tips | Förklaring |
|------|------------|
| **Reuse the same `PdfSaveOptions`** | Att skapa options‑objektet en gång och återanvända det undviker subtila skillnader i rendering (t.ex. saknade variation selectors). |
| **Call `ws.Calculate()` after setting formulas** | Utan en explicit beräkning kan spill‑området förbli tomt när du inspekterar arbetsboken programatiskt. |
| **Place Smart Marker templates on a clean sheet** | Att blanda mallar med befintliga data kan orsaka oväntad radinsättning. Använd ett dedikerat blad om möjligt. |
| **Mind the file paths** | Använd `Path.Combine(Environment.CurrentDirectory, "output.pdf")` för att undvika hårdkodade kataloger på olika maskiner. |
| **Version check** | `FontVariationSelectors` är endast tillgänglig från version 25.8; äldre versioner ignorerar egenskapen utan att kasta ett fel. |

## Nästa steg

Nu när du vet hur du **create Excel workbook**, **spill dynamic array** och **save workbook as PDF**, kan du utforska:

* Lägga till diagram eller bilder innan PDF‑konverteringen.
* Exportera samma arbetsbok till andra format (t.ex. HTML, CSV) med `Save`‑overloads.
* Använda **Smart Marker expressions** (`${Orders.Total:SUM(Items.Price)}`) för att beräkna aggregat i realtid.
* Integrera denna kod i ett ASP.NET Core‑API så att användare kan ladda ner den genererade PDF‑filen direkt från en web‑endpoint.

---

**Sammanfattning** – Denna handledning visade hur du **create Excel workbook**, använder **EXPAND function** för att **spill dynamic array**, bäddar in en **Smart Marker** som fungerar med en nästlad datakälla, och slutligen **save workbook as PDF** samtidigt som du bevarar avancerade teckensnittsegenskaper. Det kompletta, körbara exemplet kan kopieras in i vilket C#‑projekt som helst och anpassas till dina egna datastrukturer. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa och spara Excel-arbetsbok som PDF i ASP.NET med Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Hur man skapar och sparar en Excel-arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hur man skapar och sparar en Excel-arbetsbok som SVG med Aspose.Cells för Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}