---
category: general
date: 2026-09-24
description: Parse DateTime met de Japanse keizerlijke regeerperiode met Aspose.Cells
  in C#. Schakel de Japanse era‑kalender in, schrijf era‑strings en haal nauwkeurige
  DateTime‑waarden op.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: nl
lastmod: 2026-09-24
og_description: Parse DateTime met Japanse keizerlijke regeerperiode met Aspose.Cells
  in C#. Deze tutorial laat zien hoe je de Japanse era‑kalender inschakelt, era‑strings
  schrijft en een correcte DateTime terugleest.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: DateTime parseren met de regeerperiode van de Japanse keizer met Aspose.Cells
  – C#‑handleiding
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Datum en tijd parseren met de Japanse keizerlijke regeerperiode met Aspose.Cells
url: /nl/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DateTime parseren met Japanse keizerlijke regeerperiode met Aspose.Cells

Als je **DateTime met Japanse keizerlijke regeerperiode** moet parseren in een .NET‑applicatie, laat deze gids je precies zien hoe je dat doet met Aspose.Cells. Door de Japanse era‑kalender in te schakelen, een era‑gebaseerde string te schrijven en de resulterende `DateTime`‑waarde te lezen, krijg je betrouwbare, cultuur‑bewuste datums zonder handmatige stringmanipulatie.

Werken met Japanse era‑datums is gebruikelijk in financiën, overheid en legacy‑systemen die nog steeds datums opslaan zoals “令和3年5月10日”. Deze tutorial behandelt de volledige workflow, van projectconfiguratie tot het ophalen van een `DateTime`‑object dat je kunt gebruiken in berekeningen, logging of UI‑weergave.

## Wat je zult leren

- Hoe je het Aspose.Cells NuGet‑pakket toevoegt aan een C#‑project.  
- Hoe je de **Japanese era calendar** inschakelt via `Workbook.Settings`.  
- Hoe je een Japanse era‑datumsstring in een cel schrijft en Aspose.Cells deze automatisch laat parseren.  
- Hoe je de geparseerde `DateTime` leest met de `DateTimeValue`‑eigenschap.  

**Voorvereisten**  
- .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+).  
- Basiskennis van C# en Visual Studio (of een andere IDE).  
- Internettoegang om het Aspose.Cells‑pakket te downloaden.

---

## Stap 1: Installeer Aspose.Cells

Open je projectmap in een terminal of de NuGet Package Manager Console en voer uit:

```bash
dotnet add package Aspose.Cells
```

Of, in Visual Studio, klik met de rechtermuisknop op het project → **Manage NuGet Packages** → zoek naar **Aspose.Cells** en klik op **Install**.  
Dit voegt de `Aspose.Cells`‑assembly toe, die de `Workbook`, `Worksheet` en parse‑functionaliteit levert die we nodig hebben.

## Stap 2: Schakel de Japanse era‑kalender in

Aspose.Cells schakelt Japanse era‑parsing standaard uit. Je moet het inschakelen via de `Workbook.Settings.UseJapaneseEraCalendar`‑vlag.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Het instellen van `UseJapaneseEraCalendar` op `true` vertelt de bibliotheek om strings die era‑namen bevatten (`令和`, `平成`, `昭和`, etc.) te interpreteren volgens de officiële Japanse kalenderregels.

## Stap 3: Schrijf een Japanse era‑datumsstring naar een cel

Haal vervolgens het eerste werkblad op en plaats een Japanse era‑datumsstring in cel **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Waarom dit werkt:**  
Wanneer `UseJapaneseEraCalendar` actief is, onderzoekt `PutValue` de string, detecteert het era‑voorvoegsel (`令和`) en converteert het intern naar het overeenkomstige Gregoriaanse jaar (2021). De bibliotheek slaat de waarde vervolgens op als een echt `DateTime`‑object, niet alleen als tekst.

## Stap 4: Haal de geparseerde `DateTime`‑waarde op

Lees nu de `DateTimeValue` van de cel. Aspose.Cells retourneert automatisch de Gregoriaanse datum.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Running the program prints:

```
Parsed Gregorian date: 2021-05-10
```

De uitvoer bevestigt dat **Parse DateTime with Japanese Emperor Reign** correct “令和3年5月10日” heeft omgezet naar 10 mei 2021.

## Stap 5: Afhandelen van randgevallen en veelvoorkomende variaties

### Meerdere era‑formaten
Aspose.Cells herkent verschillende era‑representaties:

| Era (Japanese) | Gregorian year range |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

Als je brongegevens volledige breedte‑tekens, spaties, of het kanji “年”, “月”, “日” gebruiken, slaagt de parser nog steeds. Bijvoorbeeld, `"平成31年4月30日"` wordt `2019-04-30`.

### Ongeldige strings
Wanneer de string niet kan worden geparseerd (bijv. `"令和99年13月40日"`), retourneert `DateTimeValue` `DateTime.MinValue`. Je kunt deze toestand controleren:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### De functie uitschakelen
Als je later ruwe era‑strings wilt opslaan zonder conversie, zet je de vlag terug op `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Prestatietip
Het inschakelen van de era‑kalender voegt een kleine overhead toe aan elke `PutValue`‑aanroep die strings bevat. Als je slechts een handvol cellen parseert, schakel de vlag dan direct vóór de bewerking in en daarna weer uit om de impact te minimaliseren.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je direct kunt kopiëren, plakken en uitvoeren.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Verwachte uitvoer**

```
Parsed Gregorian date: 2021-05-10
```

Het programma demonstreert de end‑to‑end‑stroom voor **Parse DateTime with Japanese Emperor Reign** met Aspose.Cells, van het maken van een werkboek tot het verkrijgen van een bruikbaar `DateTime`‑object.

---

## Conclusie

Je weet nu hoe je **Parse DateTime with Japanese Emperor Reign** in C# kunt uitvoeren door:

1. **Aspose.Cells** installeren.  
2. De **Japanese era calendar** inschakelen via `Workbook.Settings`.  
3. Era‑gebaseerde strings naar cellen schrijven.  
4. De resulterende `DateTimeValue` lezen.  

Deze aanpak elimineert handmatige parse‑logica, respecteert officiële era‑grenzen, en integreert naadloos met bestaande .NET‑datum‑verwerkingscode.

**Volgende stappen**  
- Verken andere cultuurspecifieke functies van Aspose.Cells, zoals **C# date parsing** voor Hijri‑ of Thaise Boeddhistische kalenders.  
- Combineer deze techniek met **Workbook Settings** zoals `CalcEngine` om formules te evalueren die naar era‑datums verwijzen.  
- Gebruik de geparseerde `DateTime` in rapportage, databaseopslag, of UI‑componenten die Gregoriaanse datums vereisen.

Voel je vrij om te experimenteren met verschillende era‑strings, ongeldige invoer af te handelen, en de oplossing te integreren in grotere data‑import‑pijplijnen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}