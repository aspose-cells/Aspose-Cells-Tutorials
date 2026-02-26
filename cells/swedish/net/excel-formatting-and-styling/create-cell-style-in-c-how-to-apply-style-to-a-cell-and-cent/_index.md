---
category: general
date: 2026-02-21
description: Skapa cellstil i C# snabbt. Lär dig hur du tillämpar stil på en cell,
  centrerar text i cellen, ställer in celljustering och behärskar cellformatering.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: sv
og_description: Skapa cellstil i C# och lär dig hur du applicerar stil på en cell,
  centrerar text i cellen och ställer in celljustering med en tydlig steg‑för‑steg‑guide.
og_title: Skapa cellstil i C# – Tillämpa stil på en cell och centrera text
tags:
- C#
- Aspose.Cells
- Excel automation
title: Skapa cellstil i C# – Hur du tillämpar stil på en cell och centrerar text
url: /sv/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

shortcodes and placeholders.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa cellstil i C# – Komplett guide för att tillämpa stilar och centrera text

Har du någonsin behövt **create cell style** i ett Excel‑ark men varit osäker på var du ska börja? Du är inte ensam. I många automationsprojekt är förmågan att **apply style to cell**‑objekt skillnaden mellan ett tråkigt kalkylblad och en polerad rapport.  

I den här handledningen går vi igenom ett komplett, körbart exempel som visar dig **how to center text** i en cell, ställer in justeringen och lägger till en tunn ram — allt på bara några rader C#. I slutet vet du exakt varför varje del är viktig och hur du kan finjustera den för dina egna scenarier.

## Vad du får med dig

- En klar förståelse för **create cell style**‑arbetsflödet med Aspose.Cells (eller något liknande bibliotek).
- Den exakta koden du kan kopiera‑klistra in i en konsolapp för att **apply style to cell**.
- Insikt i **center text in cell**, **set cell alignment**, och hur du hanterar kantfall som sammanslagna celler eller anpassade talformat.
- Tips för att utöka stilen — olika typsnitt, bakgrundsfärger eller villkorsstyrd formatering.

> **Förutsättning:** Visual Studio 2022 (eller någon C#‑IDE) och Aspose.Cells för .NET NuGet‑paketet. Inga andra beroenden krävs.

---

## Steg 1: Ställ in ditt projekt och importera namnrymder

Innan vi kan **create cell style** behöver vi ett projekt som refererar till Excel‑biblioteket.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Varför detta är viktigt:* Att importera `Aspose.Cells` ger oss åtkomst till klasserna `Workbook`, `Worksheet`, `Style` och `Border`. Om du använder ett annat bibliotek (t.ex. EPPlus) ändras klassnamnen men konceptet förblir detsamma.

---

## Steg 2: Skapa en arbetsbok och hämta den första cellen

Nu **create cell style** genom att först få en referens till den cell vi vill formatera.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Observera att vi använde `Cell` istället för den generiska `var` — explicit typning gör koden tydligare för nybörjare. Anropet till `PutValue` skriver en sträng så att vi kan se stilens effekt senare.

---

## Steg 3: Definiera stilen – centrera text, lägg till en tunn ram

Här är kärnan i **create cell style**‑operationen. Vi kommer att sätta horisontell justering, en tunn ram och några valfria fördelar.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Varför vi gör detta:*  
- **HorizontalAlignment** och **VerticalAlignment** tillsammans svarar på frågan “**how to center text** i en cell?”.  
- Att lägga till alla fyra ramar säkerställer att cellen ser ut som en inramad etikett, vilket är användbart för rubriker.  
- Bakgrundsfärgen är inte obligatorisk, men den visar hur du kan utöka stilen senare.

---

## Steg 4: Tillämpa den definierade stilen på den valda cellen

Nu när stilen finns, **apply style to cell** med ett enda metodanrop.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Det är allt — Aspose.Cells tar hand om att kopiera stilen till cellens interna stilkollektion. Om du behöver samma formatering på ett område kan du använda `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Steg 5: Spara arbetsboken och verifiera resultatet

En snabb sparning låter dig öppna filen i Excel och bekräfta att texten verkligen är centrerad och ramen visas.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Förväntat resultat:* När du öppnar **StyledCell.xlsx** innehåller cell **A1** “Hello, styled world!” centrerad både horisontellt och vertikalt, omgiven av en tunn grå ram, och med en ljusgrå bakgrund.

---

## Vanliga variationer och kantfall

### 1. Centrera text i ett sammanslaget område

Om du slår ihop cellerna **A1:C1** och fortfarande vill ha texten centrerad, måste du tillämpa stilen på den översta vänstra cellen **efter** sammanslagningen:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Använda ett numeriskt format

Ibland behöver du **set cell alignment** *och* visa tal med ett specifikt format:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Justeringen förblir centrerad medan talet visas som `12,345.68`.

### 3. Återanvända stilar effektivt

Att skapa en ny `Style` för varje cell kan påverka prestandan negativt. Skapa istället ett stilobjekt och återanvänd det över många celler eller områden. `StyleFlag`‑klassen låter dig bara tillämpa de delar du bryr dig om, vilket sparar minne.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro‑tips & fallgropar att hålla utkik efter

- **Glöm inte vertikal justering** – att bara centrera horisontellt ser ofta fel ut, särskilt med högre rader.
- **Ramtyper**: `CellBorderType.Thin` fungerar för de flesta rapporter, men du kan byta till `Medium` eller `Dashed` för visuell hierarki.
- **Färghantering**: När du riktar dig mot .NET Core, använd `System.Drawing.Color` från `System.Drawing.Common`‑paketet; annars får du ett körningsfel.
- **Sparaformat**: Om du behöver kompatibilitet med äldre Excel‑versioner, ändra `SaveFormat.Xlsx` till `SaveFormat.Xls`.

![Exempel på cellstil](https://example.com/images/create-cell-style.png "Skapa cellstil i C#")
*Alt text: skärmdump som visar en cell med centrerad text och tunn ram skapad av create cell style‑handledningen.*

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Kör detta program, öppna **StyledCell.xlsx**, och du kommer att se exakt det resultat som beskrivits tidigare. Känn dig fri att ändra texten, ramstilen eller bakgrundsfärgen för att matcha ditt varumärke.

---

## Slutsats

Vi har just **created cell style** från grunden, **apply style to cell**, och demonstrerat **how to center text** både horisontellt och vertikalt. Genom att behärska dessa byggstenar kan du nu formatera rubriker, markera summor eller bygga hela rapportmallar utan att någonsin lämna C#.  

Om du är nyfiken på nästa steg, prova:

- **Tillämpa samma stil på en hel rad** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Lägga till villkorsstyrd formatering** för att ändra bakgrunden baserat på cellvärden.
- **Exportera till PDF** samtidigt som stilen bevaras.

Kom ihåg, styling handlar lika mycket om läsbarhet som om estetik. Experimentera, iterera, och snart kommer dina kalkylblad att se lika professionella ut som din kod.

*Lycka till med kodningen!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}