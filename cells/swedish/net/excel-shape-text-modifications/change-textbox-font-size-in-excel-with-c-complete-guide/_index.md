---
category: general
date: 2026-05-30
description: Ändra textrutans teckenstorlek i Excel med C#. Lär dig hur du snabbt
  modifierar teckensnittet i en Excel‑textruta med steg‑för‑steg‑kod.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: sv
og_description: Ändra teckenstorlek på textrutan i Excel med C#. Den här guiden visar
  hur du på ett säkert och effektivt sätt modifierar teckensnittet i en Excel‑textruta.
og_title: Ändra textrutans teckenstorlek i Excel med C# – Fullständig handledning
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Ändra textrutans teckenstorlek i Excel med C# – Komplett guide
url: /sv/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ändra textrutans teckenstorlek i Excel med C# – Komplett guide

Behöver du **ändra textrutans teckenstorlek** i ett Excel‑arbetsblad från C#? Du har kommit till rätt ställe. Oavsett om du genererar rapporter, bygger en instrumentpanel eller bara finjusterar en mall, kan justering av en textrutas utseende få ditt kalkylblad att se mycket mer professionellt ut.

I den här handledningen kommer vi också att **modifiera Excel‑textrutans teckensnitt** bortom bara storleken – tänk på teckensnittsfamilj, fetstil och även hantering av flera former. När du är klar har du ett färdigt kodexempel som täcker hela processen, från att öppna arbetsboken till att rensa upp COM‑objekt. Inga onödiga detaljer, bara praktisk kod som du kan klistra in i ditt projekt idag.

## Förutsättningar — Vad du behöver

| Krav | Varför det är viktigt |
|------|------------------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Tillhandahåller C#‑kompilatorn och körmiljön. |
| **Microsoft.Office.Interop.Excel** NuGet package | Ger oss de COM‑interop‑typer som behövs för att kommunicera med Excel. |
| **Excel installed** (any recent version) | Interop‑lagret fungerar endast när Office‑programmet är installerat. |
| **Basic C# knowledge** | Du kommer att kunna följa med enkelt, men vi förklarar varje rad. |

Om någon av dessa saknas, pausa nu och installera dem; resten av guiden förutsätter att de finns på plats.

## Steg 1: Ställ in projektet och importera namnrymder

Först och främst—skapa en ny konsolapp (eller integrera i en befintlig) och importera interop‑namnrymden.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Proffstips:** Om du riktar dig mot .NET 6+ lägger du till paketet `Microsoft.Office.Interop.Excel` via `dotnet add package Microsoft.Office.Interop.Excel`. Detta säkerställer att aliaset `Excel` löser sig korrekt.

## Steg 2: Öppna arbetsboken och hämta mål‑arbetsbladet

Nu behöver vi starta Excel, öppna filen och peka på bladet som innehåller textrutan. Genom att omsluta detta i ett `try/finally`‑block garanteras att COM‑objekten frigörs även om något går fel.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Varför detta är viktigt

Att öppna arbetsboken via COM ger oss en levande objektmodell – vilket betyder att varje ändring vi gör reflekteras omedelbart i filen. Genom att sätta `Visible = false` går processen snabbare och förhindrar att fönster poppar upp under automatiseringen.

## Steg 3: Hämta textrutans form

Excel behandlar textrutor som `Shape`‑objekt i `Shapes`‑samlingen, inte som en egen `TextBox`‑samling. Därför ser koden nedan lite annorlunda ut än det kodexempel du kanske har sett på nätet.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Observera:** `Shapes`‑samlingen är 1‑baserad, så vi lägger till `+1` till det noll‑baserade `textboxIndex` du skickar in. Att glömma detta leder till felmeddelandet “index out of range” som kan vara frustrerande att felsöka.

## Steg 4: Ändra textrutans teckenstorlek (och namn)

Här är där vi slutligen **ändrar textrutans teckenstorlek**. Egenskapen `TextFrame2` ger oss tillgång till avancerade formateringsalternativ, inklusive `Font.Name` och `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Varför vi använder `TextFrame2`

`TextFrame2` är den nyare objektmodellen som introducerades med Office 2007. Den stödjer avancerade typografiska funktioner och är generellt mer pålitlig än den äldre `TextFrame`. Genom att använda den säkerställer vi att vår **ändra textrutans teckenstorlek**‑operation fungerar i moderna Excel‑versioner.

## Steg 5: Spara, rensa upp och verifiera

Efter att ha justerat teckensnittet måste vi spara ändringarna och frigöra varje COM‑referens. Att hoppa över rensning kan lämna föräldralösa Excel‑processer som hänger kvar i bakgrunden.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Proffstips:** Om du behöver **modifiera Excel‑textrutans teckensnitt** på många arbetsblad, omslut den inre logiken i en loop som itererar över `Workbook.Worksheets`. Kom bara ihåg att återställa `textboxIndex` för varje blad.

## Hantera kantfall — Flera textrutor och saknade former

I verkliga kalkylblad är det sällan bara en textruta. Nedan följer två snabba strategier du kan använda utan att skriva om hela metoden.

### 1. Ändra *alla* textrutor på ett blad

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identifiera en textruta efter dess **namn** istället för index

Om du har gett din textruta ett meningsfullt namn (t.ex. “TitleBox”) kan du hämta den direkt:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Båda tillvägagångssätten låter dig **modifiera Excel‑textrutans teckensnitt** med precision, oavsett hur arbetsboken är strukturerad.

## Visuell översikt (valfritt)

Om du föredrar en snabb visuell ledtråd, föreställ dig följande diagram:

![Skärmbild som visar ett Excel‑arbetsblad med en markerad textruta – demonstrerar hur man ändrar textrutans teckenstorlek](change-textbox-font-size.png)

*Alt‑text:* *ändra textrutans teckenstorlek i Excel – markerad textruta redo för teckenändring.*

## Fullständigt fungerande exempel

När vi sätter ihop allt, här är en enda fil som du kan kopiera‑klistra in i ett konsolprojekt och köra direkt (uppdatera bara filsökvägen och bladnamnet).



## Vad bör du lära dig härnäst?

- [Ändra teckenstorlek i Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Hur man anpassar teckenstorlek i Excel‑celler med Aspose.Cells .NET \| Komplett guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Hur man ställer in teckensnittsstilar i Excel med Aspose.Cells för .NET (Steg‑för‑steg‑guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}