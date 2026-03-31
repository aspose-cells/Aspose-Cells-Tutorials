---
category: general
date: 2026-03-30
description: Leer hoe je datum in ISO-formaat kunt formatteren terwijl je Excel-datetime-waarden
  leest en datetime-Excel-gegevens extraheert met Aspose.Cells in C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: nl
og_description: Format datum ISO van Excel-gegevens met Aspose.Cells. Deze gids laat
  zien hoe je Excel-datum/tijd leest, datum/tijd-waarden uit Excel extraheert en ISO-datums
  uitvoert.
og_title: ISO-datum formatteren vanuit Excel – Stapsgewijze C#-tutorial
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: ISO-datum formatteren vanuit Excel – Complete C#-gids
url: /nl/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ISO‑datum opmaken vanuit Excel – Complete C#‑gids

Heb je ooit **format date iso** moeten gebruiken bij het ophalen van datums uit een Excel‑blad? Misschien werk je met Japanse jaartelling, of wil je gewoon een nette `yyyy‑MM‑dd`‑string voor een API‑payload. In deze tutorial zie je precies hoe je **read Excel datetime**‑cellen, **extract datetime Excel**‑waarden kunt lezen en omzetten naar ISO‑8601‑formaat—zonder giswerk.

We lopen door een real‑world voorbeeld dat Aspose.Cells gebruikt, leggen uit waarom elke regel belangrijk is, en tonen je de uiteindelijke output die je kunt kopiëren‑plakken in je project. Aan het einde kun je eigenzinnige era‑strings zoals “令和3年5月1日” verwerken en een standaard ISO‑datum produceren, klaar voor databases, JSON, of waar je het ook nodig hebt.

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework)
- Aspose.Cells voor .NET (gratis proefversie of gelicentieerde versie)
- Basiskennis van C# en Excel‑concepten
- Visual Studio of een C#‑editor naar keuze

Er zijn geen extra NuGet‑pakketten nodig naast Aspose.Cells, dus de installatie is vrij eenvoudig.

---

## Stap 1: Maak een Workbook aan en richt je op het eerste werkblad

Het eerste wat je doet, is een nieuw `Workbook`‑object aanmaken. Dit geeft je een in‑memory‑representatie van een Excel‑bestand, die je vervolgens kunt manipuleren of uit kunt lezen.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Waarom dit belangrijk is:*  
Het programmatically aanmaken van de workbook voorkomt dat je tijdens het testen met fysieke bestanden moet werken. Het zorgt er ook voor dat de werkblad‑referentie altijd geldig is—geen null‑reference‑verrassingen later wanneer je probeert **read Excel datetime**‑waarden te lezen.

---

## Stap 2: Schrijf een Japanse era‑datumsleutel in een cel

Ons doel is om het parseren van een niet‑Gregoriaanse datum te demonstreren. We plaatsen de era‑string direct in cel **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Pro tip:* Als je gegevens uit een bestaand workbook haalt, zou je de `PutValue`‑aanroep overslaan en gewoon de cel refereren die al de datum bevat. Het belangrijkste is dat de cel een **string** bevat die een datum in de Japanse lunisolaire kalender voorstelt.

---

## Stap 3: Configureer een Culture die de Japanse lunisolaire kalender begrijpt

.NET’s `CultureInfo`‑klasse laat je specificeren hoe datums geïnterpreteerd moeten worden. Door de standaard Gregoriaanse kalender te vervangen door `JapaneseLunisolarCalendar`, geef je de parser de benodigde context.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Waarom we dit doen:*  
Als je “令和3年5月1日” met de standaardcultuur probeert te parseren, zou .NET een `FormatException` gooien. Het vervangen door de lunisolaire kalender vertelt de runtime precies hoe “令和3年” (het 3e jaar van het Reiwa‑era) moet worden gemapt naar het Gregoriaanse jaar 2021.

---

## Stap 4: Parse de celwaarde als een `DateTime` met de geconfigureerde cultuur

Nu komt het hart van de operatie—het omzetten van die era‑string naar een juist `DateTime`‑object. Aspose.Cells biedt een handige `GetDateTime`‑overload die een `CultureInfo` accepteert.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Wat er onder de motorkap gebeurt:*  
`GetDateTime` leest de ruwe string, past de kalenderregels van de opgegeven cultuur toe, en retourneert een `DateTime` die hetzelfde moment in de Gregoriaanse kalender weergeeft. Dit is het moment waarop je **extract datetime Excel**‑gegevens krijgt in een vorm die je in .NET kunt gebruiken.

---

## Stap 5: Geef de geparseerde datum weer in ISO‑8601‑formaat

Tot slot formatteren we de `DateTime` als een ISO‑string—`yyyy‑MM‑dd`—die universeel wordt geaccepteerd door API’s, databases en front‑end‑frameworks.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Waarom ISO?*  
ISO 8601 elimineert ambiguïteit. “05/01/2021” kan 1 mei of 5 januari betekenen, afhankelijk van de locale. `2021-05-01` is glashelder, daarom **format date iso** we in bijna elk integratiescenario.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Kopieer het in een console‑app‑project, voeg de Aspose.Cells‑referentie toe, en druk op **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Verwachte output**

```
2021-05-01
```

Voer het één keer uit, en je ziet de ISO‑geformatteerde datum op de console afgedrukt. Dat is de volledige pijplijn van **read Excel datetime** naar **format date iso**.

---

## Veelvoorkomende randgevallen afhandelen

### 1. Cellen met echte Excel‑datumnummers

Soms slaat Excel datums op als seriële getallen (bijv. `44204`). In dat geval heb je geen cultuur nodig; roep gewoon `GetDateTime()` aan zonder parameters:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Lege of ongeldige cellen

Als een cel leeg is of een niet‑parseerbare string bevat, zal `GetDateTime` een fout gooien. Plaats de aanroep in een `try/catch` of controleer eerst `IsDateTime`:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Verschillende era‑formaten

Andere Japanse eras (Heisei, Showa) volgen hetzelfde patroon. Dezelfde `JapaneseLunisolarCalendar` zal ze automatisch verwerken, dus je hebt geen extra logica nodig—voer gewoon de string in.

---

## Pro‑tips & valkuilen

- **Performance:** Bij het verwerken van grote spreadsheets, hergebruik een enkele `CultureInfo`‑instantie in plaats van elke keer een nieuwe te maken binnen een lus.
- **Thread Safety:** `CultureInfo`‑objecten zijn alleen‑lezen nadat je de kalender hebt ingesteld, dus ze zijn veilig om te delen tussen threads.
- **Aspose.Cells Licensing:** Als je de gratis proefversie gebruikt, onthoud dan dat sommige functies beperkt kunnen zijn nadat de proefperiode is verlopen. De hier getoonde datum‑parsing werkt zowel in de proef‑ als licentiemodus.
- **Time Zones:** De `DateTime` die je krijgt is **unspecified** (geen tijdzone). Als je UTC nodig hebt, roep `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` aan of converteer met `TimeZoneInfo`.

---

## Conclusie

We hebben alles behandeld wat je nodig hebt om **format date iso** uit een Excel‑workbook te halen met C#. Beginnend met een ruwe Japanse era‑string, **read Excel datetime**, de juiste cultuur ingesteld, **extract datetime Excel**‑gegevens opgehaald, en uiteindelijk een nette ISO‑8601‑string uitgegeven. De aanpak werkt voor elke datumrepresentatie die Excel je kan geven, of het nu een serienummer, een locale‑specifieke string, of een traditioneel era‑formaat is.

Volgende stappen? Probeer een hele kolom datums te doorlopen, schrijf de ISO‑resultaten terug naar een nieuw blad, of voer ze direct in een JSON‑payload voor een webservice in. Als je nieuwsgierig bent naar andere kalendersystemen (Hebreeuws, Islamitisch), maken Aspose.Cells en .NET’s `CultureInfo` die experimenten net zo eenvoudig.

Heb je vragen of een lastig datumformaat dat je niet kunt kraken? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}