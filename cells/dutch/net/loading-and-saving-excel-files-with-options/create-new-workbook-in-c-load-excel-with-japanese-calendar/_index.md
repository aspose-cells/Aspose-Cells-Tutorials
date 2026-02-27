---
category: general
date: 2026-02-26
description: Maak een nieuw werkboek in C# en leer hoe je Excel‑bestanden laadt, de
  kalender op Japans instelt en moeiteloos datums uit Excel haalt.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: nl
og_description: Maak een nieuw werkboek in C# en leer snel hoe je Excel laadt, een
  Japanse kalender instelt en datums uit Excel‑bestanden haalt.
og_title: Maak een nieuw werkboek in C# – Laad Excel met de Japanse kalender
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Nieuw werkboek maken in C# – Excel laden met de Japanse kalender
url: /nl/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe Werkmap Maken in C# – Excel Laden met Japanse Kalender

Heb je ooit **een nieuwe werkmap moeten maken** in C# maar wist je niet hoe je Excel de Japanse kalender moet laten respecteren? Je bent niet de enige. In veel bedrijfsomgevingen ontvang je spreadsheets die datums opslaan in het Japanse jaartelling‑systeem, en die datums correct ophalen kan aanvoelen als het ontcijferen van een geheime taal.

Het punt is: je kunt **een nieuwe werkmap maken**, de lader vertellen dat datums geïnterpreteerd moeten worden met de Japanse kalender, en vervolgens **een datum uit Excel halen** met slechts een paar regels code. In deze gids lopen we *hoe je Excel laadt*, *hoe je de kalender instelt* voor Japanse datums, en uiteindelijk *Japanse datums leest* uit een cel. Geen poespas—alleen een volledig, uitvoerbaar voorbeeld dat je kunt kopiëren‑plakken in je project.

## Voorvereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+)
- De **Aspose.Cells**‑bibliotheek (gratis proefversie of gelicentieerde versie). Installeer deze via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Een Excel‑bestand (`JapanDates.xlsx`) dat Japanse jaartelling‑datums bevat in cel A1.

Dat is alles. Als je die hebt, kunnen we meteen beginnen.

---

## Nieuwe Werkmap Maken en Japanse Kalender Instellen

De eerste stap is om **een nieuwe werkmap** object te **maken** en de `LoadOptions` zo te configureren dat de parser weet welke kalender te gebruiken.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** De `LoadOptions.Calendar` eigenschap accepteert verschillende enums (`Gregorian`, `Japanese`, `Hijri`, etc.). Het kiezen van de juiste zorgt ervoor dat de bibliotheek de era‑tekst (bijv. “令和3年”) vertaalt naar een .NET `DateTime`.

![voorbeeld schermafbeelding nieuwe werkmap](image-url.png "Schermafbeelding van een nieuw werkmap‑instance met Japanse kalenderinstellingen"){: .align-center alt="voorbeeld schermafbeelding nieuwe werkmap"}

### Waarom dit werkt

- **Werkmapcreatie**: `new Workbook()` geeft je een schone lei—geen verborgen werkbladen, geen standaardgegevens.
- **LoadOptions**: Door `CalendarType.Japanese` toe te wijzen *voordat* `Load` wordt aangeroepen, behandelt de parser era‑gebaseerde strings als datums in plaats van platte tekst.
- **GetDateTime()**: Na het laden retourneert `cellA1.GetDateTime()` een echte `DateTime`‑object, waardoor je rekenkundige bewerkingen, opmaak of database‑invoegingen kunt uitvoeren zonder extra conversiestappen.

---

## Hoe Excel‑bestand Correct Laden

Je vraagt je misschien af: “Is er een speciale manier om **Excel te laden** wanneer je met niet‑Gregoriaanse kalenders werkt?” Het antwoord is ja—stel altijd de `LoadOptions` *voor* het aanroepen van `Load` in. Als je eerst laadt en daarna de kalender wijzigt, zijn de datums al onjuist geparseerd.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

De bovenstaande code laat een veelvoorkomende valkuil zien. De juiste volgorde (zoals getoond in de vorige sectie) garandeert dat de engine de cellen *als datums* interpreteert vanaf het begin.

---

## Hoe Kalender Instellen voor Japanse Datums

Als je kalenders dynamisch moet wisselen—bijvoorbeeld bij het verwerken van een batch bestanden die verschillende era‑systemen gebruiken—kun je telkens hetzelfde `Workbook`‑object hergebruiken met een nieuwe `LoadOptions`.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Het aanroepen van `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` levert hetzelfde resultaat op als ons hoofdvoorbeeld, terwijl `CalendarType.Gregorian` dezelfde cel als een gewone string zou behandelen (of een uitzondering zou werpen als het formaat niet herkenbaar is).

---

## Datum Uit Excel Halen – Japanse Datums Lezen

Nu de werkmap is geladen met de juiste kalender, is het ophalen van de datum eenvoudig. De `Cell.GetDateTime()`‑methode retourneert een `DateTime` die de era‑conversie respecteert.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Randgevallen & Wat‑Als Scenario's

| Situatie                              | Wat te doen                                                                                               |
|---------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Cel bevat **tekst** in plaats van een datum | Roep eerst `cell.GetString()` aan, valideer met `DateTime.TryParse`, of dwing gegevensvalidatie af in Excel. |
| Meerdere werkbladen moeten worden verwerkt | Loop door `workbook.Worksheets` en pas dezelfde extractielogica toe op elk blad.                           |
| Datums zijn opgeslagen als **nummers** (Excel-serial) | `cell.GetDateTime()` werkt nog steeds omdat Aspose.Cells automatisch seriële getallen converteert.          |
| Bestand is **wachtwoord‑beveiligd**   | Gebruik `LoadOptions.Password = "yourPwd"` vóór het aanroepen van `Load`.                                 |

---

## Volledig Werkend Voorbeeld (Klaar om te Kopiëren‑Plakken)

Hieronder staat het volledige programma dat je in een console‑app kunt plaatsen. Het bevat foutafhandeling en demonstreert alle vier de secundaire trefwoorden in context.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Verwachte output** (ervan uitgaande dat A1 “令和3年5月12日” bevat):

```
Japanese date in A1 → 2021-05-12
```

Als de cel een Gregoriaanse datum bevat, zoals “2021‑05‑12”, werkt dezelfde code nog steeds omdat de bibliotheek elegant terugvalt op de Gregoriaanse interpretatie.

## Conclusie

Je weet nu hoe je **een nieuwe werkmap maakt**, correct **Excel laadt**, de juiste **kalender instelt**, en uiteindelijk **een datum uit Excel haalt** terwijl je **Japanse datums leest** zonder handmatige parsing. Het belangrijkste inzicht is dat de kalender *voor* het laden moet worden gedefinieerd; zodra de werkmap in het geheugen staat, zijn de datums al gematerialiseerd als juiste `DateTime`‑objecten.

### Wat nu?

- **Batchverwerking**: Loop door een map met bestanden en roep `LoadWithCalendar` voor elk bestand aan.
- **Exporteren naar andere formaten**: Gebruik `workbook.Save("output.csv")` na conversie.
- **Lokalisatie**: Combineer `CultureInfo` met `DateTime.ToString` om datums weer te geven in de voorkeurstaal van de gebruiker.

Voel je vrij om te experimenteren—verwissel `CalendarType.Japanese` voor `CalendarType.Hijri` of `CalendarType.Gregorian` en zie hoe dezelfde code zich automatisch aanpast. Als je tegen problemen aanloopt, laat dan een reactie achter of raadpleeg de Aspose.Cells‑documentatie voor diepere API‑inzichten.

Veel plezier met coderen, en geniet van het omzetten van die mysterieuze Japanse era‑datums naar nette .NET `DateTime`‑waarden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}