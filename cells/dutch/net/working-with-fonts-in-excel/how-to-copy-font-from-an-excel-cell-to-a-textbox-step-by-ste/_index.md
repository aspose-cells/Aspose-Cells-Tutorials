---
category: general
date: 2026-02-15
description: hoe je lettertype kopieert en celstijl toepast in C# met een eenvoudig
  voorbeeld. Leer hoe je de celstijl verkrijgt en celopmaak gebruikt om de lettergrootte
  van een tekstvak in te stellen.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: nl
og_description: hoe je het lettertype van een werkbladcel kopieert en de celstijl
  toepast op een tekstvak. Deze gids laat zien hoe je de celstijl krijgt, celopmaak
  gebruikt en de lettergrootte van het tekstvak instelt.
og_title: hoe je lettertype van een Excel-cel kopieert – Complete C#‑tutorial
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Hoe je het lettertype van een Excel-cel naar een tekstvak kopieert – Stapsgewijze
  handleiding
url: /nl/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe je lettertype van een Excel-cel naar een TextBox kopieert – Complete C# Tutorial

Heb je ooit **lettertype** moeten **kopiëren** van een spreadsheetcel en een UI‑tekstvak er precies hetzelfde uit laten zien? Je bent niet de enige. In veel rapportagetools of aangepaste dashboards haal je gegevens uit Excel en probeer je vervolgens de visuele getrouwheid—lettertypefamilie, grootte en kleur—ongewijzigd te houden.  

Het goede nieuws is dat je met slechts een paar regels C# **celstijl kunt ophalen**, de lettertype‑eigenschappen kunt lezen, en **celstijl kunt toepassen** op elk tekstvak‑control. In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien hoe je **celopmaak kunt gebruiken** en zelfs **textbox‑lettergrootte kunt instellen** via code.

---

## Wat je zult leren

- Hoe je een `TextBox`‑object uit een grid‑component (`gridJs` in ons voorbeeld) kunt ophalen
- Hoe je de lettertypefamilie, grootte en kleur van een specifieke Excel‑cel (`B2`) kunt lezen
- Hoe je die lettertype‑attributen naar het tekstvak kopieert zodat de UI de spreadsheet weerspiegelt
- Veelvoorkomende valkuilen (bijv. kleurconversie) en een paar **pro‑tips** om je code robuust te houden
- Een kant‑klaar code‑fragment dat je kunt plakken in een console‑applicatie of WinForms‑project

**Prerequisites**  
Je moet het volgende hebben:

1. .NET 6+ (of .NET Framework 4.8) geïnstalleerd  
2. Het EPPlus‑NuGet‑pakket (voor Excel‑verwerking)  
3. Een grid‑control die een `TextBoxes`‑dictionary exposeert (het voorbeeld gebruikt een fictieve `gridJs`, maar het idee werkt met elke UI‑bibliotheek)

Laten we nu de handen uit de mouwen steken.

---

## Stap 1: Het project opzetten en het werkblad laden

Eerst maak je een nieuw console‑ of WinForms‑project aan en voeg je EPPlus toe:

```bash
dotnet add package EPPlus --version 6.*
```

Laad vervolgens de werkmap en pak de cel waarvan je de stijl wilt kopiëren.

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

**Waarom dit belangrijk is:** EPPlus geeft je directe toegang tot het `Style`‑object, dat het `Font`‑subobject bevat. Vanuit daar kun je `Name`, `Size` en `Color` lezen. Dit is de kern van de **get cell style**‑operatie.

---

## Stap 2: Haal het doel‑TextBox‑object uit je grid

Aangenomen dat je UI‑grid (`gridJs`) tekstvakken opslaat in een dictionary met de kolomnaam als sleutel, kun je het gewenste vak als volgt ophalen:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Als je WinForms gebruikt, kan `notesTextBox` een `TextBox`‑control zijn; voor WPF kan het een `TextBox`‑element zijn, en voor een web‑gebaseerd grid kan het een JavaScript‑interop‑object zijn. Het belangrijkste is dat je een referentie hebt die je kunt manipuleren.

---

## Stap 3: Kopieer de lettertypefamilie

Nu we zowel de bronstijl als het bestemmings‑control hebben, kopiëren we de lettertypefamilie.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Niet alle UI‑frameworks bieden een `FontFamily`‑property die een eenvoudige string accepteert. In WinForms stel je bijvoorbeeld `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Pas dit aan naar de eigenschap die jouw framework biedt.

---

## Stap 4: Kopieer de lettergrootte

De lettergrootte wordt in EPPlus opgeslagen als een `float`. Pas deze direct toe:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Als je control punten gebruikt (wat de meeste doen), kun je de waarde zonder conversie toewijzen. Voor CSS‑gebaseerde grids moet je mogelijk `"pt"` toevoegen.

---

## Stap 5: Kopieer de letterkleur

Kleurconversie is het lastigste deel omdat EPPlus kleuren opslaat als ARGB‑integers, terwijl veel UI‑frameworks een `System.Drawing.Color` of een CSS‑hex‑string verwachten.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Waarom dit werkt:** `GetColor()` lost thema‑gebaseerde kleuren op en geeft een concrete `System.Drawing.Color` terug. Als de cel de standaardkleur gebruikt (geen expliciete instelling), vallen we terug op zwart om null‑reference‑exceptions te voorkomen.

---

## Volledig werkend voorbeeld

Alles samengevoegd, hier is een minimale console‑app die een Excel‑bestand leest, het lettertype van **B2** extraheert en toepast op een mock‑textbox.

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

**Verwachte output (ervan uitgaande dat B2 Arial, 12 pt, blauw gebruikt):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Voer het programma uit, open je UI, en je ziet dat het “Notes”‑tekstvak nu exact de lettertype‑opmaak van cel **B2** weerspiegelt. Geen handmatige aanpassingen meer nodig.

---

## Veelgestelde vragen & randgevallen

### Wat als de cel een themakleur gebruikt in plaats van een expliciete RGB‑waarde?

EPPlus’s `GetColor()` lost themakleuren automatisch op naar een concrete `System.Drawing.Color`. Als je echter een oudere bibliotheek gebruikt die alleen de themapindex teruggeeft, moet je die index zelf naar een kleurenpalet vertalen.

### Kan ik andere stijl‑attributen kopiëren (bijv. vet, cursief)?

Zeker. Het `ExcelStyle.Font`‑object biedt ook `Bold`, `Italic`, `Underline` en `Strike`. Stel simpelweg de overeenkomstige eigenschappen van je UI‑control in:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Wat als de grid‑control geen `FontColor`‑property exposeert?

De meeste moderne UI‑frameworks hebben dat, maar als jouw control alleen een CSS‑string accepteert, converteer dan de `Color` naar hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Hoe ga ik om met meerdere cellen tegelijk?

Loop over het gewenste bereik, haal voor elke cel de stijl op en pas deze toe op het overeenkomstige tekstvak. Cache de stijl‑objecten bij het verwerken van veel rijen om prestatie‑verlies te voorkomen.

---

## Pro‑tips & veelvoorkomende valkuilen

- **Cache de ExcelPackage** – het bestand voor elke cel openen en sluiten is duur. Laad de werkmap één keer en hergebruik het `ExcelWorksheet`‑object.
- **Let op null‑kleuren** – een cel die de standaardkleur erft geeft `null` terug. Voorzie altijd een fallback (zwart of de standaard van het control).
- **Houd DPI‑scaling in de gaten** – bij high‑DPI‑monitoren kunnen lettergroottes iets groter lijken. Pas eventueel aan met `Graphics.DpiX`.
- **Thread‑safety** – EPPlus is niet thread‑safe. Als je veel bladen parallel verwerkt, maak dan een aparte `ExcelPackage` per thread aan.

---

## Conclusie

Je weet nu **hoe je lettertype** van een Excel‑cel kunt **kopiëren** en **celstijl kunt toepassen** op elk tekstvak‑control met C#. Door de `Style` van de cel op te halen, de `Font`‑eigenschappen te extraheren en deze aan het UI‑element toe te wijzen, behoud je visuele consistentie zonder handmatig werk.  

De complete oplossing – werkmap laden, celstijl ophalen en de lettertypefamilie, grootte en kleur van de textbox instellen – dekt de kern van **use cell formatting** en laat zien hoe je **set textbox font size** correct toepast.  

Probeer nu het voorbeeld uit te breiden naar het kopiëren van achtergrondkleuren, randen of zelfs volledige celinhoud. Werk je met een data‑grid‑bibliotheek die rijke cel‑rendering ondersteunt, dan kun je nu exact dezelfde stijl‑informatie die je uit Excel haalt, aan die grid doorgeven, zodat je UI en rapporten perfect synchroon blijven.

Meer vragen? Laat een reactie achter of verken gerelateerde onderwerpen zoals “dynamic Excel‑to‑UI binding” en “theme‑aware colour conversion”. Happy coding!

---

![hoe je lettertype voorbeeld](placeholder-image.jpg "hoe je lettertype van Excel-cel naar TextBox kopieert")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}