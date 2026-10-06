---
category: general
date: 2026-06-05
description: Maak snel een Excel-werkboek in C# en leer hoe je het getalformaat van
  een cel instelt, een Excel-cel exporteert en de celwaarde converteert naar een string
  met twee decimalen.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: nl
og_description: Maak een Excel-werkmap in C# en beheer het instellen van het getalformaat
  van cellen, exporteer een Excel-cel als een string en formatteer getallen met twee
  decimalen.
og_title: Excel-werkmap maken in C# – Volledige stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Excel-werkmap maken in C# – Complete programmeergids
url: /nl/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel Workbook in C# – Complete Programmeergids

Heb je je ooit afgevraagd hoe je een **Excel workbook** in C# kunt maken zonder te worstelen met COM‑interoperabiliteit of rommelige CSV‑trucs? Je bent niet de enige. Veel ontwikkelaars hebben een schone, .NET‑native manier nodig om een .xlsx‑bestand te genereren, een getal in een cel te plaatsen en vervolgens die waarde als een mooi opgemaakte string te exporteren.  

In deze tutorial lopen we precies dat stap voor stap door — beginnend met een lege workbook, het instellen van het getalformaat van de cel, het opmaken van het getal met twee decimalen, en uiteindelijk leren we **how to export Excel cell** gegevens als een string. Aan het einde zie je ook hoe je **convert cell value to string** kunt doen zonder precisie te verliezen.

> **Pro tip:** De onderstaande aanpak maakt gebruik van de **Aspose.Cells for .NET** bibliotheek, die een beproefde, commerciële API is. Als je een gratis alternatief zoekt, werken EPPlus of ClosedXML op een vergelijkbare manier, maar de code‑fragmenten zullen iets afwijken.

## Vereisten

- .NET 6.0 SDK (of een recente .NET‑versie) geïnstalleerd.
- Visual Studio 2022 of VS Code met de C#‑extensie.
- Het **Aspose.Cells** NuGet‑pakket (`Install-Package Aspose.Cells`).

Er zijn geen andere afhankelijkheden nodig — alles andere zit in de bibliotheek.

## Stap 1: Installeer Aspose.Cells en zet het project op

Open je terminal (of Package Manager Console) en voer uit:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Dit maakt een nieuwe console‑app met de naam `ExcelDemo` aan en haalt de `Aspose.Cells`‑assembly binnen.  

Waarom deze stap belangrijk is: zonder de bibliotheek kun je geen **Excel workbook**‑objecten maken of cellen op een type‑veilige manier manipuleren.

## Stap 2: Maak de Workbook en haal het eerste Worksheet op

Open nu `Program.cs` en vervang de standaardcode door de onderstaande snippet. Het toont het allereerste wat je doet bij het **create Excel workbook** — een instantie van de `Workbook`‑klasse maken en een referentie naar het standaardblad ophalen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Waarom?** Het `Workbook`‑object is de in‑memory representatie van een Excel‑bestand. Standaard bevat het één worksheet, die we benaderen via de nul‑gebaseerde index.

## Stap 3: Plaats een numerieke waarde in een specifieke cel

Laten we rij 5, kolom 2 (nul‑gebaseerde indexen) targeten en een decimaal getal invoegen. Dit demonstreert later **format number with two decimals**.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

De `PutValue`‑methode slaat de ruwe double op. Op dit moment zou Excel de volledige precisie weergeven tenzij we een formaat toepassen.

## Stap 4: Stel celnummerformaat in (twee decimalen)

Hier stellen we de **set cell number format** in. We gebruiken het `Style`‑object om een aangepast nummerformaat `"0.00"` te definiëren — exact twee decimalen.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Waarom een stijl gebruiken in plaats van stringconversie? De cel als numeriek type behouden behoudt zijn berekenbare aard (je kunt nog steeds optellen, middelen, enz.) terwijl je precies weergeeft wat je nodig hebt.

## Stap 5: Exporteer de celwaarde als een opgemaakte string

Soms heb je de **how to export excel cell** waarde nodig als platte tekst — misschien om het in een logbestand te schrijven of via een web‑API te verzenden. Aspose.Cells laat je exportopties aan een cel koppelen, waardoor de bibliotheek de waarde als een string rendert met hetzelfde nummerformaat.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

Nu, wanneer we de celwaarde lezen via de export‑API, ontvangen we een string die al de twee‑decimalen‑regel respecteert.

## Stap 6: Haal de opgemaakte string op (Convert Cell Value to String)

Laten we de export daadwerkelijk uitvoeren en het resultaat bekijken. De `ExportString`‑methode retourneert de inhoud van de cel als een string, waarbij eventuele `ExportTableOptions` die we hebben gekoppeld worden toegepast.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Wanneer je het programma uitvoert, print de console:

```
Formatted cell value: 12345.68
```

Let op de afronding van `12345.6789` naar `12345.68` — dat is het effect van **format number with two decimals**.

## Stap 7: (Optioneel) Sla de Workbook op schijf

Als je het resultaat ook in een echt `.xlsx`‑bestand wilt zien, roep dan simpelweg `Save` aan:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Het openen van `DemoWorkbook.xlsx` toont hetzelfde getal in cel **C6**, opgemaakt met twee decimalen.

## Randgevallen & Veelgestelde Vragen

### Wat als de cel al een stijl heeft?

De `GetStyle`‑methode retourneert een kopie van de bestaande stijl, zodat eerdere opmaak (lettertype, kleur, enz.) behouden blijft. Je overschrijft alleen de `Custom`‑eigenschap, waardoor de rest onaangeroerd blijft.

### Hoe beïnvloedt cultuur de decimale scheidingsteken?

Aspose.Cells respecteert de `CultureInfo` van de thread. Als je een komma in plaats van een punt nodig hebt, stel dan in:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Hetzelfde `"0.00"`‑formaat zal nu `12 345,68` weergeven.

### Kan ik een bereik van cellen in één keer exporteren?

Ja — gebruik `Worksheet.ExportDataTable` of `Worksheet.ExportString` met een bereikadres. De `ExportTableOptions` die je voor één cel hebt gedefinieerd, kun je hergebruiken voor het hele bereik.

### Wat als ik de waarde niet wil afronden maar afkappen?

Verander het aangepaste formaat naar `"0.00"` met een afrondingsmodus, of knip handmatig af voordat je de waarde plaatst:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Volledig Werkend Voorbeeld (Klaar om te Kopiëren‑Plakken)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Verwachte console‑output**

```
Formatted cell value: 12345.68
```

Open `DemoWorkbook.xlsx` → ga naar cel **C6** → je ziet hetzelfde getal met twee decimalen.

## Conclusie

We hebben zojuist alles behandeld wat je nodig hebt om een **Excel workbook** in C# te **create**, **set cell number format**, **format number with two decimals** toe te passen, **how to export Excel cell** gegevens te begrijpen, en **convert cell value to string** voor verdere verwerking.  

De belangrijkste inzichten zijn:

1. Gebruik `Workbook` en `Worksheet` om een Excel‑bestand in het geheugen te creëren.  
2. Pas een aangepaste stijl (`"0.00"`) toe om een weergave met twee decimalen af te dwingen.  
3. Koppel `ExportTableOptions` aan een cel wanneer je een string‑representatie nodig hebt die hetzelfde formaat respecteert.  

Vanaf hier kun je experimenteren — meer cellen toevoegen, conditionele opmaak toepassen, of zelfs grafieken genereren. Als je nieuwsgierig bent naar het stylen van lettertypen of het toevoegen van formules, bekijk dan de Aspose.Cells‑documentatie over **cell styling** en **formula evaluation**.

Heb je meer vragen over Excel‑automatisering in C#? Laat een reactie achter, en veel plezier met coderen!

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}