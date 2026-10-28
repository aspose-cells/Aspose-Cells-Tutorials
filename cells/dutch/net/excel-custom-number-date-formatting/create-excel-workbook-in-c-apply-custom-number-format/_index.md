---
category: general
date: 2026-05-23
description: Maak een Excel-werkboek in C# en leer hoe je een aangepast getalformaat
  toepast, de celstijl programmatic instelt, een cel in wetenschappelijke notatie
  formatteert, en vervolgens het werkboek opslaat als xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: nl
og_description: Maak snel een Excel-werkmap in C#. Leer hoe je een aangepast getalformaat
  toepast, cellen via code opmaakt, wetenschappelijke notatie formatteert en opslaat
  als xlsx.
og_title: Excel-werkmap maken in C# – Aangepast getalformaat toepassen
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
title: Excel-werkmap maken in C# – Aangepast getalformaat toepassen
url: /nl/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken in C# – Aangepast getalformaat toepassen

Een Excel-werkmap maken in C# is makkelijker dan je misschien denkt. In deze gids lopen we je stap voor stap door het toepassen van een aangepast getalformaat, het formatteren van een cel in wetenschappelijke notatie, het programmatically instellen van de celstijl, en uiteindelijk het opslaan van de werkmap naar een xlsx‑bestand.

Als je ooit naar een leeg spreadsheet hebt gekeken en je afvroeg hoe je het hele proces kunt automatiseren—van het vullen van gegevens tot het laten zien van cijfers precies zoals je wilt—dan is deze tutorial voor jou. Aan het einde heb je een volledig functioneel Excel‑bestand dat je in elk spreadsheet‑programma kunt openen, en begrijp je **waarom** elke stap belangrijk is, niet alleen **hoe** je de code moet typen.

## Wat je nodig hebt

- **.NET 6+** (of een recent .NET Framework dat de bibliotheek ondersteunt)  
- **Aspose.Cells for .NET** (of een andere API die de klassen `Workbook`, `Cell` en `CellFormat` blootlegt)  
- Een bescheiden hoeveelheid C#‑ervaring – als je een `Console.WriteLine` kunt schrijven, ben je klaar om te beginnen.  

Geen extra configuratiebestanden, geen COM‑interop, en zeker geen handmatige Excel‑installatie vereist.

---

## Excel-werkmap maken – Het Workbook‑object initialiseren

Het eerste wat we moeten doen is een lege werkmap aanmaken. Beschouw de `Workbook`‑klasse als het lege canvas waarop je rijen, kolommen en stijlen gaat schilderen.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Dat is alles—één regel en je hebt een gloednieuwe Excel‑file in het geheugen. De `Workbook`‑constructor maakt de standaard werkbladcollectie aan, zodat je meteen data kunt toevoegen.

> **Pro tip:** Als je meerdere werkbladen nodig hebt, kun je `workbook.Worksheets.Add()` aanroepen voordat je begint met het vullen van cellen.

![Voorbeeld van het maken van een Excel-werkmap](image-placeholder.png "Schermafbeelding van het maken van een Excel-werkmap")

*Afbeeldingsalt‑tekst: voorbeeld van het maken van een Excel-werkmap die een leeg Excel‑blad in de IDE toont.*

## Aangepast getalformaat toepassen op een cel

Nu de werkmap bestaat, laten we een getal in cel **A1** plaatsen en er een aangepast formaat aan geven. Aangepaste getalformaten laten je bepalen hoe cijfers worden weergegeven—valuta, percentages, datums, of in ons geval wetenschappelijke notatie.

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

Waarom eerst de stijl ophalen? Omdat het `Cell`‑object een **Style**‑object opslaat dat lettertypen, randen, uitlijning en getalopmaak op één plek bevat. Door de `Custom`‑eigenschap te bewerken, vertellen we Excel: “toon deze waarde in wetenschappelijke notatie met twee decimalen.”

> **Veelgestelde vraag:** *Kan ik een ingebouwd formaat gebruiken in plaats van een aangepast?*  
> Ja—stel `style.Number = 10` in voor een ingebouwd wetenschappelijk formaat, maar de aangepaste string geeft je precieze controle over het aantal decimalen.

## Celstijl programmatically instellen (buiten getalformaat)

Vaak wil je meer dan alleen een getalformaat. Laten we een vet lettertype en een lichtgrijze achtergrond toevoegen zodat de cel opvalt.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Merk op dat we hetzelfde `style`‑object hergebruiken dat we eerder hebben aangepast. Dat is het mooie van **celstijl programmatically instellen**—je haalt de stijl maar één keer op, wijzigt de gewenste eigenschappen, en schrijft het terug. Geen noodzaak om objecten opnieuw te maken of het al ingestelde getalformaat te verliezen.

## Cel formatteren in wetenschappelijke notatie (edge‑case handling)

Als je werkt met zeer grote of zeer kleine getallen, is wetenschappelijke notatie een redding. Het aangepaste formaat dat we gebruikten (`0.00E+00`) garandeert twee cijfers na de decimale punt en dwingt een plusteken af voor de exponent. Hier is een snelle controle:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Wanneer je het resulterende bestand opent, zal B2 verschijnen als `1.23E-05`, wat bevestigt dat de **cel formatteren in wetenschappelijke notatie** werkt voor zowel grote als kleine getallen.

## Werkmap opslaan als XLSX

Het plezier stopt wanneer je het bestand daadwerkelijk naar schijf schrijft. De `Save`‑methode doet het zware werk, door de in‑memory representatie om te zetten naar een correct `.xlsx`‑pakket.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Die regel bereikt het **werkmap opslaan als xlsx**‑doel. Als de map niet bestaat, zal `Save` een uitzondering werpen—zorg er dus voor dat de map van tevoren wordt aangemaakt of wikkel de aanroep in een try/catch‑blok.

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

Nu heb je een kant‑en‑klaar Excel‑bestand met een mooi opgemaakte wetenschappelijke notatie, vet gestylede tekst en een lichtgrijze achtergrond.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑en‑klaar te kopiëren programma dat alle onderdelen samenvoegt. Het compileert als een console‑app, maar je kunt de logica in elk C#‑project gebruiken.

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

**Verwacht resultaat:** Open `CustomFormatted.xlsx` en je ziet:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Beide cellen zijn vet, hebben een lichtgrijze vulling, en tonen cijfers in wetenschappelijke notatie met twee decimalen.

---

## Samenvatting

We hebben zojuist **een Excel-werkmap gemaakt** vanaf nul, **een aangepast getalformaat toegepast**, **cel in wetenschappelijke notatie geformatteerd**, **celstijl programmatically ingesteld**, en **de werkmap opgeslagen als xlsx**—alles in een handvol C#‑regels. De aanpak schaalt: loop gewoon over rijen, kloon het `style`‑object, en je hebt binnen enkele seconden een volledig gestylede rapport.

### Wat is het volgende?

- **Dynamische opmaak:** Wissel formaten op basis van de waarde‑grootte (bijv. valuta vs. percentage).  
- **Meerdere werkbladen:** Gebruik `workbook.Worksheets.Add("Summary")` om dashboards te bouwen.  
- **Geavanceerde styling:** Randen, voorwaardelijke opmaak en gegevensvalidatie


## Gerelateerde tutorials

- [Hoe een Excel-werkmap maken en opslaan als ODS met Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Excel-werkmap maken en opslaan Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Excel-werkmap maken en opslaan als PDF Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}