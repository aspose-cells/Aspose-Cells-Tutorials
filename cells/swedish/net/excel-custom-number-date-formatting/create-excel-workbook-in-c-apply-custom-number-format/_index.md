---
category: general
date: 2026-05-23
description: Skapa en Excel-arbetsbok i C# och lär dig hur du tillämpar anpassat talformat,
  sätter cellstil programatiskt, formaterar cellen i vetenskaplig notation och sedan
  sparar arbetsboken som xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: sv
og_description: Skapa Excel-arbetsbok i C# snabbt. Lär dig att tillämpa anpassade
  talformat, formatera celler programatiskt, formatera vetenskaplig notation och spara
  till xlsx.
og_title: Skapa Excel-arbetsbok i C# – Använd anpassat talformat
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Skapa Excel-arbetsbok i C# – Använd anpassat talformat
url: /sv/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i C# – Använd anpassat talformat

Att skapa en Excel-arbetsbok i C# är enklare än du tror. I den här guiden går vi igenom hur du applicerar ett anpassat talformat, formaterar en cell i vetenskaplig notation, sätter cellstilen programatiskt och slutligen sparar arbetsboken till en xlsx‑fil.

Om du någonsin har stirrat på ett tomt kalkylblad och undrat hur du automatiserar hela processen—från att fylla i data till att få siffrorna att se exakt ut som du vill—så är den här tutorialen för dig. I slutet kommer du att ha en fullt fungerande Excel‑fil som du kan öppna i vilket kalkylprogram som helst, och du kommer att förstå **varför** varje steg är viktigt, inte bara **hur** du skriver koden.

## Vad du behöver

- **.NET 6+** (eller någon nyare .NET Framework som stöder biblioteket)  
- **Aspose.Cells for .NET** (eller ett annat API som exponerar klasserna `Workbook`, `Cell` och `CellFormat`)  
- En viss mängd C#‑erfarenhet – om du kan skriva en `Console.WriteLine` är du redo att köra.  

Inga extra konfigurationsfiler, ingen COM‑interop och absolut ingen manuell Excel‑installation krävs.

---

## Skapa Excel-arbetsbok – Initiera Workbook‑objektet

Det första vi måste göra är att skapa en tom arbetsbok. Tänk på `Workbook`‑klassen som en tom duk där du kan måla rader, kolumner och stilar.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Klart—en rad och du har en helt ny Excel‑fil i minnet. `Workbook`‑konstruktorn skapar standardkollektionen av kalkylblad, så du kan börja lägga till data omedelbart.

> **Proffstips:** Om du behöver flera blad kan du anropa `workbook.Worksheets.Add()` innan du börjar fylla i celler.

![Skapa excel arbetsbok exempel som visar ett tomt Excel‑blad i IDE:n](image-placeholder.png "Skärmdump av skapa excel arbetsbok")

## Applicera anpassat talformat på en cell

Nu när arbetsboken finns, låt oss lägga in ett tal i cell **A1** och ge den ett anpassat format. Anpassade talformat låter dig styra hur siffror visas—valuta, procent, datum eller, i vårt fall, vetenskaplig notation.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Varför hämta stilen först? Eftersom `Cell`‑objektet lagrar ett **Style**‑objekt som innehåller teckensnitt, kantlinjer, justering och talformat på ett och samma ställe. Genom att redigera `Custom`‑egenskapen säger vi till Excel att “visa detta värde i vetenskaplig notation med två decimaler”.

> **Vanlig fråga:** *Kan jag använda ett inbyggt format istället för ett anpassat?*  
> Ja—sätt `style.Number = 10` för ett inbyggt vetenskapligt format, men den anpassade strängen ger dig exakt kontroll över decimalerna.

## Ställ in cellstil programatiskt (bortom talformat)

Ofta vill du ha mer än bara ett talformat. Låt oss lägga till ett fetstilteckensnitt och en ljusgrå bakgrund för att få cellen att sticka ut.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Observera att vi återanvänder samma `style`‑objekt som vi justerade tidigare. Det är fördelarna med **set cell style programmatically**—du hämtar stilen bara en gång, ändrar de egenskaper du behöver och skriver tillbaka den. Ingen anledning att återskapa objekt eller förlora det talformat du redan har satt.

## Formatera cell i vetenskaplig notation (hantering av kantfall)

Om du hanterar mycket stora eller mycket små tal är vetenskaplig notation en räddare i nöden. Det anpassade formatet vi använde (`0.00E+00`) garanterar två siffror efter decimalpunkten och tvingar ett plustecken för exponenten. Här är en snabb kontroll:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

När du öppnar den resulterande filen kommer B2 att visas som `1.23E-05`, vilket bekräftar att **format cell scientific notation**‑direktivet fungerar för både stora och små tal.

## Spara arbetsbok till XLSX

Allt det roliga slutar när du faktiskt skriver filen till disk. `Save`‑metoden sköter det tunga arbetet, konverterar representationen i minnet till ett korrekt `.xlsx`‑paket.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Den raden uppfyller målet **save workbook to xlsx**. Om katalogen inte finns kommer `Save` att kasta ett undantag—så se till att mappen skapas i förväg eller omslut anropet med en try/catch‑block.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Nu har du en färdig‑att‑dela Excel‑fil med ett snyggt formaterat vetenskapligt tal, fet stil och en ljusgrå bakgrund.

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet som binder ihop alla delar. Det kompileras som en konsolapp, men du kan lägga in logiken i vilket C#‑projekt som helst.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Förväntat resultat:** Öppna `CustomFormatted.xlsx` och du kommer att se:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Båda cellerna är i fet stil, har en ljusgrå fyllning och visar tal i vetenskaplig notation med två decimaler.

---

## Sammanfattning

Vi har precis **create excel workbook** från grunden, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically** och **save workbook to xlsx**—allt i ett fåtal rader C#. Metoden skalar: loopa bara över rader, klona `style`‑objektet, så får du en fullständigt stylad rapport på sekunder.

### Vad blir nästa?

- **Dynamic formatting:** Byt format baserat på värdets storlek (t.ex. valuta vs. procent).  
- **Multiple sheets:** Använd `workbook.Worksheets.Add("Summary")` för att bygga instrumentpaneler.  
- **Advanced styling:** Kantlinjer, villkorsstyrd formatering och datavalidering

## Relaterade handledningar

- [Hur man skapar och sparar en Excel-arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Skapa och spara Excel-arbetsbok Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Skapa och spara Excel-arbetsbok PDF Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}