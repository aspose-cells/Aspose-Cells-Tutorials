---
category: general
date: 2026-02-15
description: hur man kopierar teckensnitt och tillämpar cellstil i C# med ett enkelt
  exempel. Lär dig hur du hämtar cellstil och använder cellformatering för att ställa
  in textrutans teckensnittsstorlek.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: sv
og_description: hur man kopierar teckensnitt från en kalkylbladscell och tillämpar
  cellstil på en textruta. Denna guide visar hur man hämtar cellstil, använder cellformatering
  och ställer in textrutans teckenstorlek.
og_title: hur man kopierar teckensnitt från en Excel-cell – komplett C#‑handledning
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: så här kopierar du teckensnittet från en Excel‑cell till en textruta – steg‑för‑steg‑guide
url: /sv/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur att kopiera teckensnitt från en Excel‑cell till en TextBox – Komplett C#‑handledning

Har du någonsin behövt **kopiera teckensnitt** från en kalkylarkscell och få en UI‑textbox att se exakt likadan ut? Du är inte ensam. I många rapporteringsverktyg eller anpassade instrumentpaneler hamnar du ofta med att hämta data från Excel och sedan försöka behålla den visuella integriteten—teckensnittsfamilj, storlek och färg—oförändrad.  

Den goda nyheten är att med bara några rader C# kan du **hämta cellstil**, läsa dess teckensnittsegenskaper och **tillämpa cellstil** på vilken text‑box‑kontroll som helst. I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur du **använder cellformatering** och till och med **sätter textboxens teckenstorlek** programatiskt.

---

## Vad du kommer att lära dig

- Hur du hämtar ett `TextBox`‑objekt från en grid‑komponent (`gridJs` i vårt exempel)
- Hur du läser teckensnittsfamilj, storlek och färg från en specifik Excel‑cell (`B2`)
- Hur du kopierar dessa teckensnittsattribut till textboxen så att UI‑et speglar kalkylbladet
- Vanliga fallgropar (t.ex. färgkonvertering) och några **pro‑tips** för att hålla din kod robust
- En färdig‑att‑köra kodsnutt som du kan klistra in i en konsolapp eller WinForms‑projekt

**Förutsättningar**  
Du bör ha:

1. .NET 6+ (eller .NET Framework 4.8) installerat  
2. EPPlus NuGet‑paketet (för Excel‑hantering)  
3. En grid‑kontroll som exponerar en `TextBoxes`‑dictionary (exemplet använder en fiktiv `gridJs` men idén fungerar med vilket UI‑bibliotek som helst)

Nu, låt oss kavla upp ärmarna.

---

## Steg 1: Ställ in projektet och läs in arbetsbladet

Först, skapa ett nytt konsol‑ eller WinForms‑projekt och lägg till EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Läs sedan in arbetsboken och hämta cellen vars stil du vill kopiera.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Varför detta är viktigt:** EPPlus ger dig direkt åtkomst till `Style`‑objektet, som innehåller `Font`‑subobjektet. Därifrån kan du läsa `Name`, `Size` och `Color`. Detta är kärnan i **hämta cellstil**‑operationen.

---

## Steg 2: Hämta mål‑TextBoxen från ditt grid

Om ditt UI‑grid (`gridJs`) lagrar text‑boxar i en dictionary nycklad med kolumnnamn, kan du hämta den du vill ha så här:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Om du använder WinForms kan `notesTextBox` vara en `TextBox`‑kontroll; för WPF kan det vara ett `TextBox`‑element, och för ett webbaserat grid kan det vara ett JavaScript‑interop‑objekt. Huvudpoängen är att du har en referens du kan manipulera.

---

## Steg 3: Överför teckensnittsfamiljen

Nu när vi har både källstilen och destinationskontrollen, kopiera teckensnittsfamiljen.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro‑tip:** Inte alla UI‑ramverk exponerar en `FontFamily`‑property som accepterar en ren sträng. I WinForms skulle du sätta `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Anpassa efter behov.

---

## Steg 4: Överför teckenstorleken

Teckenstorleken lagras som en `float` i EPPlus. Tillämpa den direkt:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Om din kontroll använder punkter (vilket de flesta gör) kan du tilldela värdet utan konvertering. För CSS‑baserade grid kan du behöva lägga till `"pt"`.

---

## Steg 5: Överför teckenfärgen

Färgkonvertering är den svåraste delen eftersom EPPlus lagrar färger som ARGB‑heltal, medan många UI‑ramverk förväntar sig en `System.Drawing.Color` eller en CSS‑hex‑sträng.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Varför detta fungerar:** `GetColor()` löser temabaserade färger och returnerar en konkret `System.Drawing.Color`. Om cellen använder standardfärgen (ingen explicit inställning) faller vi tillbaka på svart för att undvika null‑referens‑undantag.

---

## Fullt fungerande exempel

När allt sätts ihop får du en minimal konsolapp som läser en Excel‑fil, extraherar teckensnittet från **B2**, och tillämpar det på en mock‑textbox.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Förväntad utskrift (förutsatt att B2 använder Arial, 12 pt, blå):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Kör programmet, öppna ditt UI, och du kommer att se att “Notes”‑textboxen nu speglar exakt teckensnittsstilen i cell **B2**. Ingen manuell justering behövs.

---

## Vanliga frågor & edge‑cases

### Vad händer om cellen använder en temafärg istället för ett explicit RGB‑värde?

EPPlus `GetColor()` löser automatiskt temafärger till en konkret `System.Drawing.Color`. Om du använder ett äldre bibliotek som bara returnerar temaindexen måste du själv mappa den indexen till en färgpalett.

### Kan jag kopiera andra stilattribut (t.ex. fet, kursiv)?

Absolut. `ExcelStyle.Font`‑objektet exponerar även `Bold`, `Italic`, `Underline` och `Strike`. Sätt bara motsvarande egenskaper på ditt UI‑element:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Vad händer om grid‑kontrollen inte exponerar en `FontColor`‑property?

De flesta moderna UI‑ramverk har det, men om ditt bara accepterar en CSS‑sträng, konvertera `Color` till hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Hur hanterar jag flera celler samtidigt?

Loopa över önskat område, hämta varje cells stil och tillämpa den på motsvarande textbox. Kom ihåg att cacha stilobjekten om du bearbetar många rader för att undvika prestandaproblem.

---

## Pro‑tips & vanliga fallgropar

- **Cachea ExcelPackage** – att öppna och stänga filen för varje cell är dyrt. Läs in arbetsboken en gång och återanvänd `ExcelWorksheet`‑objektet.
- **Var uppmärksam på null‑färger** – en cell som ärver standardfärgen returnerar `null`. Tillhandahåll alltid en reservfärg (svart eller kontrollens standard).
- **Tänk på DPI‑skalning** – om du riktar dig mot hög‑DPI‑monitorer kan teckenstorlekar visas något större. Justera med `Graphics.DpiX` vid behov.
- **Trådsäkerhet** – EPPlus är inte trådsäker. Om du bearbetar många blad parallellt, skapa ett separat `ExcelPackage` per tråd.

---

## Slutsats

Du vet nu **hur du kopierar teckensnitt** från en Excel‑cell och **tillämpar cellstil** på vilken text‑box‑kontroll som helst med C#. Genom att hämta cellens `Style`, extrahera dess `Font`‑egenskaper och tilldela dem till UI‑elementet bevarar du visuell konsistens utan manuell kopiering.  

Den kompletta lösningen – att ladda arbetsboken, hämta cellstilen och sätta textboxens teckensnittsfamilj, storlek och färg – täcker kärnan i **använd cellformatering** och demonstrerar hur du **sätter textboxens teckenstorlek** korrekt.  

Nästa steg är att utöka exemplet för att kopiera bakgrundsfärger, kantlinjer eller till och med hela cellinnehåll. Om du arbetar med ett data‑grid‑bibliotek som stödjer rik cellrendering kan du nu mata in exakt samma stilinformation som du hämtade från Excel, så att ditt UI och dina rapporter hålls perfekt synkroniserade.

Har du fler frågor? Lämna en kommentar eller utforska relaterade ämnen som “dynamisk Excel‑till‑UI‑bindning” och “temabaserad färgkonvertering”. Lycka till med kodandet!

---

![exempel på att kopiera teckensnitt](placeholder-image.jpg "hur man kopierar teckensnitt från Excel‑cell till TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}