---
category: general
date: 2026-02-21
description: Sla Excel op als txt met precieze controle over significante cijfers.
  Exporteer Excel naar txt in C# en stel significante cijfers eenvoudig in.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: nl
og_description: Sla Excel snel op als txt. Leer hoe je Excel naar txt exporteert,
  significante cijfers instelt en de tekstoutput beheert met C#.
og_title: Excel opslaan als txt – Getallen exporteren met significante cijfers in
  C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excel opslaan als txt – Complete C#‑gids voor het exporteren van getallen met
  significante cijfers
url: /nl/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

with bold **text**.

Also blockquote >.

Also list items.

Also code block placeholders remain.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel opslaan als txt – Complete C# gids om getallen met significante cijfers te exporteren

Heb je ooit **Excel als txt moeten opslaan** maar was je bang dat de getallen hun precisie zouden verliezen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze Excel naar txt exporteren en eindigen met ofwel te veel decimalen of een afgerond geheel geheel.  

In deze tutorial laten we je een eenvoudige manier zien om **Excel naar txt te exporteren** terwijl je **significante cijfers instelt**, zodat de uitvoer er precies zo uitziet als jij wilt. Aan het einde heb je een kant‑klaar C#‑fragment dat een werkmap opslaat als tekst, getallen naar txt exporteert, en volledige controle geeft over het numerieke formaat.

## Wat je zult leren

- Hoe je een nieuwe werkmap maakt en numerieke data schrijft.
- De juiste manier om **significante cijfers in te stellen** met `TxtSaveOptions`.
- Hoe je **werkmap als tekst opslaat** en het resultaat verifieert.
- Afhandeling van randgevallen (grote getallen, negatieve waarden, locale‑problemen).
- Snelle tips om de uitvoer verder aan te passen (delimiter‑wijzigingen, codering).

### Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+).
- Het **Aspose.Cells** NuGet‑pakket (`Install-Package Aspose.Cells`).
- Een basisbegrip van C#‑syntaxis — geen diepgaande Excel‑interop‑kennis vereist.

> **Pro tip:** Als je Visual Studio gebruikt, schakel *nullable reference types* in (`<Nullable>enable</Nullable>`) om mogelijke null‑bugs vroegtijdig te detecteren.

---

## Stap 1: Initialiseert de werkmap en schrijf een getal

Eerst hebben we een werkmap‑object nodig. Beschouw het als de in‑memory weergave van een Excel‑bestand.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Waarom dit belangrijk is:**  
Het programmatic maken van de werkmap vermijdt de overhead van COM‑interop, en `PutValue` detecteert automatisch het gegevenstype, waardoor de cel als een getal wordt behandeld — niet als een string.

---

## Stap 2: Configureer TxtSaveOptions om significante cijfers te beheersen

De `TxtSaveOptions`‑klasse is waar de magie gebeurt. Door `SignificantDigits` in te stellen, vertel je Aspose.Cells hoeveel betekenisvolle cijfers behouden moeten blijven wanneer het bestand wordt weggeschreven.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Waarom je dit moet instellen:**  
Wanneer je **getallen naar txt exporteert**, heb je vaak een beknopte weergave nodig (bijvoorbeeld voor rapportagesystemen die slechts een bepaalde precisie accepteren). De eigenschap `SignificantDigits` garandeert consistente afronding, ongeacht de oorspronkelijke lengte van het getal.

---

## Stap 3: Sla de werkmap op als tekstbestand

Nu schrijven we de werkmap naar schijf met de opties die we zojuist hebben gedefinieerd.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Wat je zult zien:**  
Open `Numbers.txt` en je krijgt één enkele regel:

```
12350
```

Het oorspronkelijke `12345.6789` is afgerond naar **vier significante cijfers**, precies zoals gevraagd.

---

## Stap 4: Verifieer de uitvoer (optioneel maar aanbevolen)

Geautomatiseerde tests zijn een goede gewoonte. Hier is een snelle controle die je direct na het opslaan kunt uitvoeren:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Het uitvoeren van dit blok zal een groen vinkje afdrukken als alles klopt, waardoor je vertrouwen krijgt dat de **save excel as txt**‑operatie zich heeft gedragen zoals bedoeld.

---

## Veelvoorkomende variaties & randgevallen

### Meerdere cellen of bereiken exporteren

Als je een **excel naar txt moet exporteren** voor een heel bereik, vul dan gewoon meer cellen voordat je opslaat:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Dezelfde `TxtSaveOptions` past de 4‑cijfer‑regel toe op elke waarde, resulterend in:

```
12350
0.0001235
-98800
```

### De delimiter wijzigen

Sommige downstream‑systemen verwachten tab‑gescheiden waarden. Pas de delimiter als volgt aan:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Nu wordt elke cel in een rij gescheiden door een tab.

### Locale‑specifieke decimale scheidingstekens behandelen

Als je publiek komma’s gebruikt voor decimalen, stel dan de cultuur in:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

De uitvoer respecteert de locale en zet `12350` om in `12 350` (spatie als duizendtallen‑scheidingsteken in het Frans).

---

## Volledig werkend voorbeeld (Kopieer‑en‑plak klaar)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Verwachte inhoud van `Numbers.txt` (standaard delimiter, 4 significante cijfers):**

```
12350	0.0001235	-98800
```

De tab (`\t`) verschijnt omdat we de delimiter in het voorbeeld op de standaardwaarde (tab) hebben gelaten; wijzig deze naar een komma als je CSV wilt.

---

## Conclusie

Je weet nu precies **hoe je Excel als txt kunt opslaan** terwijl je het aantal significante cijfers beheert. De stappen — een werkmap maken, `TxtSaveOptions.SignificantDigits` instellen, en opslaan — zijn alles wat je nodig hebt om **excel naar txt te exporteren** betrouwbaar uit te voeren.  

Vanaf hier kun je:

- **Getallen naar txt exporteren** voor grotere datasets.
- Delimiters, codering of cultuursinstellingen aanpassen om aan elk downstream‑systeem te voldoen.
- Deze aanpak combineren met andere Aspose.Cells‑functies (stijlen, formules) vóór export.

Probeer het, pas `SignificantDigits` aan naar 2 of 6, en zie hoe de uitvoer verandert. De flexibiliteit van **save workbook as text** maakt het een handig hulpmiddel in elke data‑uitwisselingspipeline.

---

### Gerelateerde onderwerpen die je hierna kunt verkennen

- **Export Excel to CSV** met aangepaste kolomvolgorde.
- **Lees txt‑bestanden terug in een werkmap** (`Workbook.Load` met `LoadOptions`).
- **Batchverwerking** van meerdere werkbladen en deze consolideren in één txt‑bestand.
- **Prestatie‑optimalisatie** voor grootschalige exports (streaming vs. in‑memory).

Laat gerust een reactie achter als je ergens vastloopt, of deel hoe jij de export hebt aangepast voor jouw eigen projecten. Veel programmeerplezier!  

---  

*Afbeelding: Een screenshot van het gegenereerde `Numbers.txt`‑bestand met afgeronde waarden.*  
*Alt‑tekst: “Numbers.txt‑bestand dat 12350, 0.0001235, en -98800 toont na het opslaan van Excel als txt met 4 significante cijfers.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}