---
category: general
date: 2026-10-26
description: Leer hoe je de Japanse kalender‑CultureInfo in C# kunt gebruiken bij
  het parseren van era‑datums en het invoegen ervan in een Excel‑werkblad met NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: nl
lastmod: 2026-10-26
og_description: Gebruik de Japanse kalender‑CultureInfo in C# om Reiwa‑era‑datums
  te parseren en ze naar een Excel‑werkblad te schrijven. Complete, uitvoerbare code
  met uitleg.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Gebruik Japanse kalender CultureInfo in C# – volledig Excel‑voorbeeld
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Hoe de Japanse kalender CultureInfo in C# te gebruiken om datums naar Excel
  te schrijven
url: /nl/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe je de Japanese calendar CultureInfo in C# gebruikt om datums naar Excel te schrijven

Als je **Japanese calendar CultureInfo** moet gebruiken bij het werken met datums in C#, laat deze gids je precies zien hoe. Je leert een datum‑string die een Japanse jaartelling bevat (bijvoorbeeld *Reiwa 2/5/1*) te parseren en vervolgens de resulterende `DateTime` in de eerste cel van een Excel‑werkblad te schrijven met behulp van de NPOI‑bibliotheek.

Het parseren van op jaartelling gebaseerde datums zonder de juiste `CultureInfo` leidt tot een `FormatException` of onjuiste maand‑/dagwaarden. Door `CultureInfo` in te stellen op de Japanse kalender, zorg je ervoor dat de .NET‑runtime de jaartelling correct interpreteert en dat de waarde die je in Excel opslaat overeenkomt met de oorspronkelijke Japanse notatie.

In deze tutorial leer je:

* Een `CultureInfo`‑object maken dat de Japanse kalender gebruikt.
* Een Japanse jaartelling‑datumstring parseren met `DateTime.Parse`.
* De geparseerde `DateTime` invoegen in een NPOI‑werkbladcel.
* Het volledige, uitvoerbare programma en de verwachte output bekijken.

> **Prerequisites** – .NET 6.0+ (of .NET Core 3.1+), het **NPOI** NuGet‑pakket, en een basisbegrip van C# en Excel‑bestandsverwerking.

---

## Wat je nodig hebt

| Item | Reden |
|------|-------|
| **.NET SDK** (6.0 of later) | Biedt de runtime en bibliotheken voor `CultureInfo`. |
| **NPOI** (`NPOI` NuGet‑pakket) | Stelt je in staat Excel‑bestanden te maken en te manipuleren zonder Office geïnstalleerd te hebben. |
| **Visual Studio Code**, **Visual Studio**, of een andere C#‑IDE | Om het voorbeeld te compileren en uit te voeren. |
| **Japanse jaartelling‑datumstring** (bijv. `"Reiwa 2/5/1"`) | Demonstreert het gebruik van de Japanse kalender. |

---

## Stap 1: Installeer NPOI

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package NPOI --version 2.6.1
```

Het pakket levert de types `IWorkbook`, `ISheet` en `ICell` die later worden gebruikt.

---

## Stap 2: Maak een CultureInfo die de Japanse kalender gebruikt

De Japanse kalender is een op jaartelling gebaseerde kalender. Je moet de *Japanese* variant van de `ja-JP`‑locale aanvragen en expliciet de kalender instellen op `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – De standaard `ja-JP`‑cultuur gebruikt de Gregoriaanse kalender. Het opnieuw toewijzen van de eigenschap `Calendar` zorgt ervoor dat jaartellingnamen zoals *Reiwa* tijdens het parseren worden herkend.

---

## Stap 3: Parse een Japanse jaartelling‑datumstring

Nu de `CultureInfo` is geconfigureerd, kun je veilig een string die een jaartellingnaam bevat parseren.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

De `Parse`‑methode interpreteert *Reiwa 2* als het Gregoriaanse jaar 2020, maand 5, dag 1.

### Edge case: handling invalid eras

Als een gebruiker een niet‑ondersteunde jaartelling opgeeft (bijv. `"Heisei 31/4/30"` nadat het Heisei‑tijdperk is geëindigd), gooit `DateTime.Parse` een `FormatException`. Plaats de aanroep in een try‑catch‑blok om een vriendelijke foutmelding te geven:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Stap 4: Schrijf de geparseerde DateTime naar een Excel‑werkblad

Met het `DateTime`‑object klaar, kun je het opslaan in een Excel‑cel. NPOI formatteert `DateTime`‑waarden automatisch als Excel‑datums.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Result** – Het openen van *JapaneseEraDate.xlsx* toont de datum **2020‑05‑01** in cel A1.

### Why use NPOI?

*Works on any platform* (Windows, Linux, macOS) and does **not** require Microsoft Office. This makes the solution suitable for CI pipelines, Docker containers, or server‑side processing.

---

## Stap 5: Volledig, uitvoerbaar programma

Alles bij elkaar, hier is een complete console‑applicatie die de volledige flow demonstreert:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**How to run**

```bash
dotnet run
```

Na uitvoering vind je `JapaneseEraDate.xlsx` in de projectmap met de correct geparseerde datum.

---

## Veelvoorkomende valkuilen en best‑practice tips

| Valkuil | Oplossing / Aanbeveling |
|---------|------------------------|
| Vergeten om `japaneseCulture.DateTimeFormat.Calendar` in te stellen | Wijs altijd een `JapaneseCalendar`‑instantie toe; anders wordt de jaartellingnaam niet herkend. |
| `DateTime.TryParse` gebruiken zonder de aangepaste `CultureInfo` | Geef dezelfde `japaneseCulture` door aan `TryParse` om consistent gedrag te behouden. |
| Verwachten dat Excel de jaartellingnaam weergeeft | De ingebouwde datumformaten van Excel zijn alleen Gregoriaans. Als je de jaartelling wilt tonen, sla de originele string op in een aparte kolom of maak een aangepast tekstformaat. |
| De `FileStream` niet disposen | Gebruik een `using`‑blok (zoals getoond) om ervoor te zorgen dat de bestandshandle snel wordt vrijgegeven. |
| `CultureInfo`‑objecten door elkaar halen over threads | `CultureInfo` is thread‑safe voor alleen‑lezen operaties, maar vermijd het wijzigen van de eigenschap `Calendar` na de initiële configuratie. |

---

## Conclusie

Je weet nu hoe je **Japanese calendar CultureInfo** in C# kunt gebruiken om Japanse jaartelling‑datums nauwkeurig te parseren en de resulterende `DateTime` in een Excel‑werkblad te schrijven met NPOI. Het volledige voorbeeld behandelt configuratie, parsing, foutafhandeling en Excel‑output, en biedt een solide basis voor elke geïternationaliseerde rapportage‑ of data‑uitwisselingsscenario.

Vervolgens kun je verkennen:

* **Formatting dates with custom text** om de jaartellingnaam binnen Excel te behouden.
* **Reading dates from Excel** met `cell.DateCellValue` terwijl je de Japanse kalender respecteert.
* **Applying the same technique** voor andere op jaartelling gebaseerde kalenders (bijv. de Thaise Boeddhistische kalender) door `JapaneseCalendar` te vervangen door de juiste `Calendar`‑subklasse.

Voel je vrij om te experimenteren met verschillende jaartelling‑strings, grotere datasets, of deze logica te integreren in ASP.NET Core‑API’s die Excel‑rapporten on‑the‑fly genereren. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak Excel‑werkmap met Japanse kalenderdatums – Volledige gids](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanse jaartelling‑datums in Excel – Volledige gids voor C#‑ontwikkelaars](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Hoe een Excel‑werkmap te maken en Japanse datums te parseren in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}