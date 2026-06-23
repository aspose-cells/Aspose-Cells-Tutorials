---
category: general
date: 2026-05-30
description: Wijzig de lettergrootte van een tekstvak in Excel met C#. Leer hoe je
  het lettertype van een Excel‑tekstvak snel kunt aanpassen met stap‑voor‑stap code.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: nl
og_description: Verander de lettergrootte van een tekstvak in Excel met C#. Deze gids
  laat zien hoe je het lettertype van een Excel-tekstvak veilig en efficiënt kunt
  aanpassen.
og_title: Tekstvaklettergrootte wijzigen in Excel met C# – Volledige tutorial
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
title: Tekstvaklettergrootte wijzigen in Excel met C# – Complete gids
url: /nl/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekstvaklettergrootte wijzigen in Excel met C# – Complete gids

Moet je **change textbox font size** in een Excel-werkblad vanuit C#? Je bent op de juiste plek. Of je nu rapporten genereert, een dashboard bouwt, of gewoon een sjabloon aanpast, het aanpassen van het uiterlijk van een tekstvak kan je spreadsheet er veel professioneler uit laten zien.

In deze tutorial zullen we ook **modify excel textbox font** aanpassen, niet alleen de grootte—denk aan lettertypefamilie, vetgedrukt en zelfs het omgaan met meerdere vormen. Aan het einde heb je een kant‑klaar fragment dat elk aspect van het proces aanraakt, van het openen van de werkmap tot het opruimen van COM‑objecten. Geen poespas, alleen praktische code die je vandaag nog in je project kunt gebruiken.

## Voorvereisten — Wat je nodig hebt

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Levert de C#-compiler en runtime. |
| **Microsoft.Office.Interop.Excel** NuGet package | Geeft ons de COM-interoperatietypen die nodig zijn om met Excel te communiceren. |
| **Excel installed** (any recent version) | De Interop-laag werkt alleen wanneer de Office-app aanwezig is. |
| **Basic C# knowledge** | Je kunt gemakkelijk volgen, maar we leggen elke regel uit. |

Als een van deze ontbreekt, pauzeer dan nu en installeer ze; de rest van de gids gaat ervan uit dat ze aanwezig zijn.

## Stap 1: Het project opzetten en namespaces importeren

Allereerst—maak een nieuwe console‑app (of integreer in een bestaande) en haal de interop‑namespace binnen.

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

> **Pro tip:** Als je .NET 6+ target, voeg dan het `Microsoft.Office.Interop.Excel`‑pakket toe via `dotnet add package Microsoft.Office.Interop.Excel`. Dit zorgt ervoor dat de `Excel`‑alias correct wordt opgelost.

## Stap 2: Open de werkmap en haal het doel‑werkblad op

Nu moeten we Excel starten, het bestand openen en naar het blad wijzen dat het tekstvak bevat. Het omhullen van dit in een `try/finally`‑blok garandeert dat de COM‑objecten worden vrijgegeven, zelfs als er iets misgaat.

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

### Waarom dit belangrijk is

Het openen van de werkmap via COM geeft ons een live objectmodel—wat betekent dat elke wijziging die we maken onmiddellijk in het bestand wordt weergegeven. Het instellen van `Visible = false` versnelt het proces en voorkomt pop‑up vensters tijdens automatisering.

## Stap 3: Haal de tekstvak‑vorm op

Excel behandelt tekstvakken als `Shape`‑objecten in de `Shapes`‑collectie, niet als een speciale `TextBox`‑collectie. Daarom ziet de onderstaande code er iets anders uit dan het fragment dat je online misschien hebt gezien.

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

> **Watch out:** De `Shapes`‑collectie is 1‑gebaseerd, dus we voegen `+1` toe aan de nul‑gebaseerde `textboxIndex` die je doorgeeft. Het vergeten hiervan leidt tot “index out of range”‑fouten die frustrerend kunnen zijn om te debuggen.

## Stap 4: Tekstvaklettergrootte wijzigen (en naam)

Hier wijzigen we eindelijk **change textbox font size**. De `TextFrame2`‑eigenschap geeft ons toegang tot de rich‑text opmaakopties, waaronder `Font.Name` en `Font.Size`.

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

### Waarom we `TextFrame2` gebruiken

`TextFrame2` is het nieuwere objectmodel geïntroduceerd met Office 2007. Het ondersteunt geavanceerde typografische functies en is over het algemeen betrouwbaarder dan de oudere `TextFrame`. Het gebruik ervan zorgt ervoor dat onze **change textbox font size**‑operatie werkt in moderne Excel‑versies.

## Stap 5: Opslaan, opruimen en verifiëren

Na het aanpassen van het lettertype moeten we de wijzigingen opslaan en elke COM‑referentie vrijgeven. Het overslaan van opruimen kan leiden tot verweesde Excel‑processen die op de achtergrond blijven hangen.

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

> **Pro tip:** Als je **modify excel textbox font** op veel werkbladen moet toepassen, wikkel dan de interne logica in een lus die over `Workbook.Worksheets` itereren. Vergeet niet `textboxIndex` voor elk blad opnieuw in te stellen.

## Omgaan met randgevallen — Meerdere tekstvakken en ontbrekende vormen

In de praktijk bevatten spreadsheets zelden slechts één tekstvak. Hieronder staan twee snelle strategieën die je kunt toepassen zonder de hele methode opnieuw te schrijven.

### 1. *Alle* tekstvakken op een blad wijzigen

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

### 2. Een tekstvak identificeren op basis van zijn **Name** in plaats van index

Als je je tekstvak een betekenisvolle naam hebt gegeven (bijv. “TitleBox”), kun je het direct ophalen:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Beide benaderingen laten je **modify excel textbox font** met precisie toepassen, ongeacht hoe de werkmap is gestructureerd.

## Visueel overzicht (optioneel)

Als je de voorkeur geeft aan een snelle visuele hint, stel je dan het volgende diagram voor:

![Schermafbeelding van een Excel-werkblad met een gemarkeerd tekstvak – toont hoe je de tekstvaklettergrootte wijzigt](change-textbox-font-size.png)

*Alt‑tekst:* *tekstvaklettergrootte wijzigen in Excel – gemarkeerd tekstvak klaar voor lettertype‑aanpassing.*

## Volledig werkend voorbeeld

Alles samenvoegend, hier is een enkel bestand dat je kunt kopiëren‑plakken in een console‑project en direct kunt uitvoeren (pas alleen het bestandspad en de bladnaam aan).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

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
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Wat moet je hierna leren?

- [Lettergrootte wijzigen in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Hoe de lettergrootte in Excel-cellen aanpassen met Aspose.Cells .NET | Complete gids](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Hoe letterstijlen instellen in Excel met Aspose.Cells voor .NET (Stapsgewijze gids)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}