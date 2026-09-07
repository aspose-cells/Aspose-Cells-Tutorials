---
category: general
date: 2026-02-21
description: Skapa PowerPoint från Excel snabbt. Lär dig hur du exporterar Excel till
  PowerPoint med redigerbar text och diagram med Aspose.Cells på bara några rader
  C#‑kod.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: sv
og_description: Skapa PowerPoint från Excel med redigerbar text och diagram. Följ
  den här detaljerade guiden för att exportera Excel till PowerPoint med Aspose.Cells.
og_title: Skapa PowerPoint från Excel – Steg‑för‑steg C#‑guide
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Skapa PowerPoint från Excel – Komplett C#‑handledning
url: /sv/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PowerPoint från Excel – Komplett C#-handledning

Har du någonsin behövt **skapa PowerPoint från Excel** men varit osäker på vilket API du ska använda? Du är inte ensam. Många utvecklare stöter på problem när de vill omvandla ett data‑rikt kalkylblad till en polerad bildspel, särskilt när de behöver att textrutorna förblir redigerbara efter konverteringen.  

I den här guiden visar vi dig hur du **exporterar Excel till PowerPoint** samtidigt som du bevarar redigerbar text, diagramkvalitet och layout—allt med några få rader C#. I slutet har du en färdig PPTX‑fil som du kan justera i PowerPoint precis som vilken manuellt byggd bild som helst.

## Vad du kommer att lära dig

- Hur du laddar ett Excel‑arbetsbok som innehåller diagram och former.  
- Hur du konfigurerar `PresentationExportOptions` så att textrutor förblir redigerbara (`export editable text`).  
- Hur du faktiskt **exporterar Excel‑diagram till PowerPoint** och får ett rent bildspel.  
- Små variationer du kan använda när du behöver **konvertera Excel‑diagram till PowerPoint** för olika sidinställningar eller flera arbetsblad.  

### Förutsättningar

- En .NET‑utvecklingsmiljö (Visual Studio 2022 eller senare).  
- Aspose.Cells för .NET (gratis provversion eller licensierad version).  
- En Excel‑fil (`ChartWithShape.xlsx`) som innehåller minst ett diagram och en form du vill behålla redigerbar.  

Om du har dem, låt oss dyka ner—utan onödig prat, bara en praktisk, körbar lösning.

## Skapa PowerPoint från Excel – Steg för steg

Under varje steg visar vi ett kort kodexempel, förklarar **varför** vi gör det och pekar på vanliga fallgropar. Känn dig fri att kopiera‑klistra in hela exemplet längst ner på sidan.

### Steg 1: Ladda Excel‑arbetsboken

Först måste vi läsa in källarbetsboken i minnet. Aspose.Cells läser filen och bygger en rik objektsmodell som vi kan manipulera.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Varför detta är viktigt:**  
Att ladda arbetsboken är grunden. Om filvägen är fel eller arbetsboken är korrupt, kommer alla efterföljande `export excel to powerpoint`-steg att misslyckas. En kontroll ger dig tidig återkoppling istället för ett vagt “filen kunde inte hittas” senare.

### Steg 2: Förbered exportalternativ

Aspose.Cells ger dig ett `PresentationExportOptions`-objekt som styr hur PPTX‑filen kommer att se ut. Här bestämmer du om du vill att texten ska förbli redigerbar.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Varför detta är viktigt:**  
Utan att konfigurera `PresentationExportOptions` använder biblioteket sina standardinställningar, vilket kanske inte matchar din företagsmall för bildspel. Att justera bildstorleken i förväg förhindrar behovet av manuell storleksändring senare.

### Steg 3: Aktivera redigerbara textrutor

Den magiska flaggan `ExportEditableTextBoxes` talar om för Aspose.Cells att behålla alla textformer som PowerPoint‑textrutor, inte som statiska bilder.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Varför detta är viktigt:**  
Om du hoppar över den här raden kommer den resulterande PPTX‑filen att innehålla rasteriserad text—vilket betyder att du inte kan redigera etiketten eller bildtexten i PowerPoint. Att sätta `export editable text` är nyckeln till ett riktigt återanvändbart bildspel.

### Steg 4: Exportera arbetsbladet till PPTX

Nu skriver vi faktiskt PPTX‑filen. Du kan välja vilket arbetsblad som helst; här använder vi det första (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Varför detta är viktigt:**  
`SaveToPptx` respekterar sidinställningarna (marginaler, orientering) du definierade i Excel, så bilden speglar den layout du redan har designat. Detta är kärnan i **export excel chart powerpoint**.

### Steg 5: Verifiera resultatet (Valfritt men rekommenderat)

Efter konverteringen, öppna den genererade `Result.pptx` i PowerPoint och kontrollera:

1. Diagrammen visas skarpa och behåller dataserier.  
2. Textrutor är valbara och redigerbara.  
3. Bildstorleken matchar dina förväntningar.

Om något ser fel ut, gå tillbaka till `exportOptions`—till exempel kan du behöva sätta `exportOptions.IncludePrintArea = true` för att respektera ett namngivet utskriftsområde.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Steg 6: Avancerade varianter (Exportera flera blad)

Ofta vill du **konvertera excel chart powerpoint** för flera arbetsblad samtidigt. Loopa över samlingen och ge varje bild ett unikt namn:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Proffstips:** Om du behöver alla blad i en *enda* PPTX, skapa ett nytt `Presentation`‑objekt, importera varje bild och spara sedan en gång. Det är lite mer invecklat men sparar dig från att hantera många filer.

## Fullständigt fungerande exempel

Här är hela programmet så att du kan klistra in det i en konsolapp och köra det omedelbart.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Förväntat resultat:**  
När du öppnar `Result.pptx` ser du en bild som speglar Excel‑arbetsbladets layout. Alla diagram du placerade i Excel visas som ett inbyggt PowerPoint‑diagram, och bildtexten du lade till som en form är nu en fullt redigerbar textruta.

## Vanliga frågor & specialfall

- **Fungerar detta med makro‑aktiverade arbetsböcker (`.xlsm`)?**  
  Ja. Aspose.Cells läser makron men kör dem inte. Konverteringsprocessen ignorerar VBA, så du får fortfarande det visuella innehållet.

- **Vad händer om mitt arbetsblad innehåller flera diagram?**  
  Alla synliga diagram överförs till samma bild. Om du behöver varje diagram på en egen bild, dela upp arbetsbladet eller använd loopen som visas i Steg 6.

- **Kan jag bevara anpassade PowerPoint‑teman?**  
  Inte direkt under export. Efter konverteringen kan du applicera ett tema i PowerPoint eller programmässigt via Aspose.Slides.

- **Finns det ett sätt att bara exportera ett valt område?**  
  Ställ in ett namngivet utskriftsområde i Excel (`Page Layout → Print Area`) och aktivera `exportOptions.IncludePrintArea = true`.

## Slutsats

Du vet nu hur du **skapar PowerPoint från Excel** med Aspose.Cells, med full kontroll över redigerbar text, diagramkvalitet och bildstorlek. Det korta kodexemplet vi delade hanterar det vanligaste scenariot, och de extra tipsen ger dig flexibilitet när du behöver **export excel to powerpoint** för flera blad eller anpassade layouter.  

Redo för nästa utmaning? Prova att kombinera detta tillvägagångssätt med **Aspose.Slides** för att programmässigt lägga till övergångar, talarnoter eller till och med bädda in de genererade bilderna i en större presentation. Eller experimentera med att konvertera en hel arbetsbok till ett multi‑bildspel—perfekt för automatiserade rapporteringspipelines.

Har du frågor eller har du upptäckt ett smart knep? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}