---
category: general
date: 2026-04-07
description: Skapa en Excel-arbetsbok, radbryt kolumner i Excel, beräkna formler och
  spara arbetsboken som XLSX med steg-för-steg C#‑kod.
draft: false
keywords:
- create excel workbook
- wrap columns in excel
- save workbook as xlsx
- how to calculate formulas
- how to save excel
language: sv
og_description: Skapa en Excel‑arbetsbok, bryt text i kolumner i Excel, beräkna formler
  och spara arbetsboken som XLSX. Lär dig hela processen med körbar kod.
og_title: Skapa Excel-arbetsbok – Komplett C#-guide
tags:
- csharp
- aspnet
- excel
- automation
title: Skapa Excel-arbetsbok – Radbryt kolumner och spara som XLSX
url: /sv/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok – Wrappa kolumner och spara som XLSX

Har du någonsin behövt **skapa en Excel-arbetsbok** programatiskt och undrat hur du får data att passa snyggt i en flerkolumnslayout? Du är inte ensam. I den här handledningen går vi igenom hur du skapar arbetsboken, applicerar `WRAPCOLS`‑formeln för att **wrappa kolumner i Excel**, tvingar motorn att beräkna resultatet, och slutligen **spara arbetsboken som XLSX** så att du kan öppna den i vilket kalkylprogram som helst.

Vi kommer också att besvara de oundvikliga uppföljningsfrågorna: *Hur beräknar jag formler i farten?* *Vad händer om jag behöver ändra antalet kolumner?* och *Finns det ett snabbt sätt att spara filen?* I slutet har du ett självständigt, färdigt‑att‑köra C#‑snippet som gör allt detta samt några extra tips som du kan kopiera in i dina egna projekt.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+)
- Aspose.Cells‑biblioteket **Aspose.Cells** (eller något annat Excel‑bearbetningspaket som stödjer `WRAPCOLS`; exemplet använder Aspose.Cells eftersom det erbjuder en enkel `CalculateFormula`‑metod)
- En viss erfarenhet av C# – om du kan skriva `Console.WriteLine` är du redo att köra

> **Pro tip:** Om du ännu inte har en licens för Aspose.Cells kan du begära en gratis provnyckel från deras webbplats; provversionen fungerar utmärkt för lärande.

## Steg 1: Skapa Excel-arbetsbok

Det allra första du behöver är ett tomt arbetsboksobjekt som representerar Excel‑filen i minnet. Detta är kärnan i **skapa en Excel-arbetsbok**‑operationen.

```csharp
using Aspose.Cells;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet – it’s already there by default
Worksheet worksheet = workbook.Worksheets[0];
```

*Varför detta är viktigt:* `Workbook`‑klassen är ingångspunkten för all Excel‑manipulation. Genom att skapa den först sätter du upp en ren canvas där efterföljande åtgärder—som att wrappa kolumner—kan tillämpas utan sidoeffekter.

## Steg 2: Fyll i lite exempeldata (valfritt men hjälpsamt)

Innan vi wrappar kolumner, låt oss lägga in en liten dataset i intervallet `A1:D10`. Detta speglar ett verkligt scenario där du har en rå tabell som behöver omformas.

```csharp
// Fill A1:D10 with sample numbers for demonstration
for (int row = 0; row < 10; row++)
{
    for (int col = 0; col < 4; col++)
    {
        worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
    }
}
```

Du kan hoppa över detta block om du redan har data i kalkylbladet; wrappningslogiken fungerar på vilket befintligt intervall som helst.

## Steg 3: Wrappa kolumner i Excel

Nu kommer stjärnan i föreställningen: `WRAPCOLS`‑funktionen. Den tar ett källintervall och ett kolumnantal, och sprider sedan data över den nya layouten. Så här applicerar du den på cell **A1** så att resultatet upptar tre kolumner.

```csharp
// Apply WRAPCOLS to A1 – the result will spill into a 3‑column layout
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";
```

**Vad händer under huven?**  
`WRAPCOLS(A1:D10,3)` instruerar Excel att läsa de 40 cellerna i `A1:D10` och sedan skriva dem rad‑för‑rad i tre kolumner, automatiskt skapa så många rader som behövs. Detta är perfekt för att omvandla en lång lista till en mer kompakt, tidningsliknande vy.

## Steg 4: Så beräknar du formler

Att sätta en formel är bara halva striden; Excel beräknar inte resultatet förrän du triggar ett beräkningspass. I Aspose.Cells gör du det med `CalculateFormula()`.

```csharp
// Force the workbook to evaluate all pending formulas
workbook.CalculateFormula();
```

> **Varför du behöver detta:** Utan att anropa `CalculateFormula` skulle cellen `A1` bara innehålla formelsträngen när du öppnar filen, och den wrappade layouten skulle inte visas förrän en användare manuellt beräknar om.

## Steg 5: Spara arbetsboken som XLSX

Slutligen, spara arbetsboken till disk. `Save`‑metoden härleder automatiskt formatet från filändelsen, så att använda **.xlsx** säkerställer att du får det moderna Open XML‑formatet.

```csharp
// Choose a folder you have write access to and save the file
string outputPath = @"C:\Temp\output.xlsx";
workbook.Save(outputPath);
```

När du öppnar `output.xlsx` i Excel kommer du att se den ursprungliga datan snyggt wrappad i tre kolumner, med start i cell **A1**. Resten av bladet förblir orört, vilket är praktiskt om du behöver behålla källtabellen för referens.

### Förväntad resultatbild

<img src="images/wrapcols-result.png" alt="create excel workbook example" />

Bilden ovan illustrerar den slutgiltiga layouten: siffrorna från `A1:D10` visas nu över tre kolumner, med rader som automatiskt genereras för att rymma alla värden.

## Vanliga variationer & kantfall

### Ändra antalet kolumner

Om du behöver ett annat kolumnantal, justera helt enkelt det andra argumentet i `WRAPCOLS`:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,5)"; // five‑column layout
```

Kom ihåg att köra `CalculateFormula()` igen efter någon förändring.

### Wrappa icke‑sammanhängande intervall

`WRAPCOLS` fungerar endast med sammanhängande intervall. Om dina källdata är uppdelade över flera områden, konsolidera dem först (t.ex. med `UNION` i en hjälpkolumn) innan du wrappar.

### Stora dataset

För mycket stora tabeller kan beräkningen ta några sekunder. Du kan förbättra prestandan genom att inaktivera automatisk beräkning innan du sätter formeln och återaktivera den efteråt:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D1000,4)";
workbook.CalculateFormula();
workbook.Settings.CalcMode = CalcMode.Automatic;
```

### Spara till en ström

Om du bygger ett webb‑API och vill returnera filen direkt till klienten kan du skriva till en `MemoryStream` istället för en fysisk fil:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // reset for reading
// return ms as a FileResult in ASP.NET Core, for example
```

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta, kopiera‑och‑klistra‑klara programmet:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Fill A1:D10 with sample data (optional)
        for (int row = 0; row < 10; row++)
        {
            for (int col = 0; col < 4; col++)
            {
                worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
            }
        }

        // 3️⃣ Apply WRAPCOLS to produce a 3‑column layout
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";

        // 4️⃣ Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // 5️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Kör detta program, öppna den genererade `output.xlsx`, och du kommer att se datan wrappad exakt som beskrivet.

## Slutsats

Du vet nu **how to create Excel workbook**‑objekt i C#, hur du applicerar den kraftfulla `WRAPCOLS`‑funktionen för att **wrap columns in Excel**, **calculate formulas** på begäran, och **save workbook as XLSX** för vidare konsumtion. Detta end‑to‑end‑flöde täcker de vanligaste scenarierna, från enkla demo‑exempel till produktionsklassisk automatisering.

### Vad blir nästa?

- Experimentera med andra dynamiska array‑funktioner som `FILTER`, `SORT` eller `UNIQUE`.
- Kombinera `WRAPCOLS` med villkorsstyrd formatering för att markera specifika rader.
- Integrera denna logik i en ASP.NET Core‑endpoint så att användare kan ladda ner en anpassad rapport med ett enda klick.

Känn dig fri att justera kolumnantalet, källintervallet eller utsökvägen för att passa dina egna projektbehov. Om du stöter på problem, lämna en kommentar nedan—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}