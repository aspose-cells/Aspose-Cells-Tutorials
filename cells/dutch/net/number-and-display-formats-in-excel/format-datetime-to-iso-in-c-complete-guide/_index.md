---
category: general
date: 2026-03-22
description: Leer hoe je datetime naar ISO kunt formatteren terwijl je een datum uit
  Excel haalt en de ISO‑datum weergeeft met Aspose.Cells in C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: nl
og_description: datetime naar iso formatteren is eenvoudig. Deze gids laat zien hoe
  je een datum uit Excel haalt en de iso‑datum weergeeft met Aspose.Cells.
og_title: datetime formatteren naar ISO in C# – Stapsgewijze tutorial
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Datum/tijd formatteren naar ISO in C# – Complete gids
url: /nl/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# datetime formatteren naar iso in C# – Complete gids

Heb je ooit **datetime naar iso formatteren** nodig gehad, maar bevindt de bron zich in een Excel-werkmap? Misschien bevat de cel een Japanse jaartelling zoals “令和3年5月1日” en krabbel je je hoofd af terwijl je je afvraagt hoe je dat kunt omzetten naar een nette `2021‑05‑01`‑string. Je bent niet de enige. In deze tutorial zullen we **datum uit excel extraheren**, de Japanse jaartelling parseren, en vervolgens **iso‑datum weergeven** op de console—alles met een paar regels C# en Aspose.Cells.

We lopen alles door wat je nodig hebt: het vereiste NuGet‑pakket, de exacte code die je kunt copy‑paste, waarom elke regel belangrijk is, en een reeks edge‑case‑tips. Aan het einde heb je een herbruikbare snippet die datetime naar iso formatteert, ongeacht hoe eigenzinnig de oorspronkelijke Excel‑waarde eruitziet.

## Wat je nodig hebt

- .NET 6.0 of later (de code compileert ook op .NET Framework 4.6+)
- Visual Studio 2022 (of elke editor die je verkiest)
- **Aspose.Cells for .NET** NuGet‑pakket – `Install-Package Aspose.Cells`
- Een Excel‑bestand (of een nieuwe werkmap) dat een datum in Japanse jaartelling‑formaat bevat

Dat is alles. Geen extra bibliotheken, geen COM‑interop, alleen een enkele, goed gedocumenteerde methode.

## Stap 1: Maak een werkmap en schrijf een Japanse jaartelling‑datum  

Eerst hebben we een werkmap nodig om mee te werken. Als je al een Excel‑bestand hebt, kun je het laden met `new Workbook("path")`. Voor dit voorbeeld maken we een nieuwe werkmap in het geheugen en plaatsen we een Japanse jaartelling‑tekst in cel **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Waarom we dit doen:** Aspose.Cells behandelt celwaarden standaard als strings. Door de ruwe jaartelling‑tekst in te voegen simuleren we een real‑world scenario waarin een Japanse klant datums invoert in hun eigen kalender.

## Stap 2: Schakel Japanse jaartelling‑parsing in en extraheer de datum  

Aspose.Cells kan automatisch Japanse jaartelling‑strings vertalen naar .NET `DateTime`‑objecten—mits je het aangeeft. De `DateTimeParseOptions.EnableJapaneseEra`‑vlag doet het zware werk.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** Als je de `EnableJapaneseEra`‑optie vergeet, zal de bibliotheek de originele string teruggeven, en zal je daaropvolgende conversie falen. Controleer altijd `parsed.Type` als je gemengde inhoud verwerkt.

## Stap 3: Converteer de geparseerde DateTime naar ISO 8601  

Nu we een juiste `DateTime` hebben, is het omzetten naar een ISO‑geformatteerde string een fluitje van een cent. Het patroon `"yyyy-MM-dd"` voldoet aan het datumgedeelte van ISO 8601, wat de meeste API's verwachten.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Het uitvoeren van het programma geeft het volgende weer:

```
ISO date: 2021-05-01
```

Dat is de **iso‑datum weergeven** die je zocht.

## Volledig, uitvoerbaar voorbeeld  

Hieronder staat het volledige codeblok dat je rechtstreeks kunt kopiëren in een console‑project. Geen verborgen afhankelijkheden, geen extra configuratie.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Verwachte output:** `ISO date: 2021-05-01`

## Stapsgewijze uitsplitsing (Waarom elk onderdeel belangrijk is)

| Stap | Wat gebeurt er | Waarom het belangrijk is |
|------|----------------|--------------------------|
| **Werkmap maken** | Initialiseert een in‑memory Excel‑container. | Geeft je een sandbox om te testen zonder het bestandssysteem aan te raken. |
| **PutValue** | Slaat de ruwe Japanse jaartelling‑string op in **A1**. | Imiteert echte gegevensinvoer; zorgt ervoor dat de parser de exacte tekst ziet. |
| **GetValue met `EnableJapaneseEra`** | Converteert de jaartelling‑string naar een .NET `DateTime`. | Verwerkt de kalenderconversie automatisch—geen handmatige opzoektabellen nodig. |
| **`ToString("yyyy-MM-dd")`** | Formateert de `DateTime` naar ISO 8601. | Garandeert een cultuur‑onafhankelijke, sorteerbare datumstring die door REST‑API's, databases, enz. wordt geaccepteerd. |
| **Console.WriteLine** | Toont de uiteindelijke ISO‑datum. | Bevestigt dat de volledige pijplijn end‑to‑end werkt. |

## Veelvoorkomende variaties afhandelen  

### 1. Verschillende celposities  

Als je datum zich bevindt in **B2** of een benoemd bereik, vervang dan simpelweg `"A1"` door het juiste adres:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Meerdere datums in een kolom  

Wanneer je **datum uit excel moet extraheren** voor veel rijen, loop je door het gebruikte bereik:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Fallback voor niet‑jaartelling‑datums  

Als een cel al een standaard datumstring bevat, werkt de parser nog steeds, maar je wilt misschien een vangnet:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

De `TryParse`‑vlag voorkomt uitzonderingen en retourneert de originele waarde als de conversie mislukt.

### 4. Tijdcomponent  

Mocht je ook het tijdgedeelte nodig hebben, gebruik dan `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Dat levert een volledige ISO 8601‑tijdstempel op (`2021-05-01T00:00:00`).

## Visuele hulp  

![voorbeeld van datetime formatteren naar iso](image.png "Een voorbeeld van datetime formatteren naar iso in C#")

*Alt-tekst:* *voorbeeld van datetime formatteren naar iso, console‑output tonend*

## Veelgestelde vragen  

- **Kan ik dit gebruiken met .xls‑bestanden?**  
  Ja. Aspose.Cells ondersteunt `.xls`, `.xlsx`, `.csv` en vele andere formaten out‑of‑the‑box.

- **Wat als de werkmap met een wachtwoord beveiligd is?**  
  Laad deze met `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Is het ISO‑formaat afhankelijk van de locale?**  
  Nee. Het patroon `"yyyy-MM-dd"` is cultuur‑onafhankelijk, waardoor dezelfde string op elke machine gegarandeerd is.

- **Werkt dit op .NET Core?**  
  Absoluut—Aspose.Cells voldoet aan .NET Standard 2.0.

## Samenvatting  

We hebben behandeld hoe je **datetime naar iso kunt formatteren** door **datum uit excel te extraheren**, Japanse jaartelling‑strings te parseren, en uiteindelijk **iso‑datum weer te geven** op de console. De kernstappen—een werkmap maken, de jaartelling‑tekst schrijven of laden, Japanse jaartelling‑parsing inschakelen, en formatteren met `ToString("yyyy-MM-dd")`—zijn alles wat je nodig hebt voor de meeste scenario's.

Vervolgens wil je misschien:

- De ISO‑datums terugschrijven naar een andere kolom voor downstream‑verwerking.
- De getransformeerde werkmap exporteren naar CSV voor bulk‑import.
- Deze logica combineren met een web‑API die Excel‑uploads accepteert en JSON‑gecodeerde ISO‑datums retourneert.

Voel je vrij om te experimenteren met verschillende datumformaten, tijdzones, of zelfs aangepaste kalenders. De flexibiliteit van Aspose.Cells betekent dat je zelden tegen een muur aanloopt.

Veel plezier met coderen, en moge al je datums perfect ISO‑conform zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}