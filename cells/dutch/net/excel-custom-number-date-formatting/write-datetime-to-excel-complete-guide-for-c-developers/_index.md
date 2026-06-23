---
category: general
date: 2026-04-07
description: Schrijf datum en tijd naar Excel met C#. Leer hoe je een datum in een
  werkblad invoegt, de datumwaarde van een Excel-cel verwerkt en een Japanse kalenderdatum
  converteert in slechts een paar stappen.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: nl
og_description: Schrijf datum en tijd snel naar Excel. Deze gids laat zien hoe je
  een datum in een werkblad invoegt, de datumwaarde van een Excel-cel beheert en een
  Japanse kalenderdatum converteert met C#.
og_title: Datum en tijd naar Excel schrijven – Stap‑voor‑stap C#‑tutorial
tags:
- C#
- Excel automation
- Aspose.Cells
title: Datum/tijd naar Excel schrijven – Complete gids voor C#‑ontwikkelaars
url: /nl/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum/tijd naar Excel schrijven – Complete gids voor C#‑ontwikkelaars

Heb je ooit moeten **datum/tijd naar Excel schrijven** maar wist je niet welke API‑aanroep daadwerkelijk een juiste Excel‑datum opslaat? Je bent niet de enige. In veel bedrijfs‑tools moeten we een C# `DateTime` in een spreadsheet plaatsen, en het resultaat moet zich gedragen als een echte Excel‑datum—sorteerbaar, filterbaar en klaar voor draaitabellen.  

In deze tutorial lopen we stap voor stap door hoe je *een datum in een werkblad invoegt* met Aspose.Cells, leggen we uit waarom het instellen van de cultuur belangrijk is, en laten we zelfs zien hoe je **Japanse kalenderdatum** omzet naar een reguliere `DateTime` voordat je deze schrijft. Aan het einde heb je een zelfstandige code‑fragment dat je kunt kopiëren en plakken in elk .NET‑project.

## Wat je nodig hebt

- **.NET 6+** (of een recente .NET‑versie; de code werkt ook op .NET Framework)  
- **Aspose.Cells for .NET** – een NuGet‑pakket waarmee je Excel‑bestanden kunt manipuleren zonder Office geïnstalleerd te hebben.  
- Een basisbegrip van C# `DateTime` en culturen.  

Geen extra bibliotheken, geen COM‑interop en geen Excel‑installatie vereist. Als je al een werkblad‑instantie (`ws`) hebt, ben je klaar om te gaan.

## Stap 1: De Japanse cultuur instellen (Japanse kalenderdatum converteren)

Wanneer je een datum ontvangt zoals `"R02/05/01"` (Reiwa 2, 1 mei) moet je .NET vertellen hoe de era‑symbolen geïnterpreteerd moeten worden. De Japanse kalender is niet de standaard Gregoriaanse kalender, dus maken we een `CultureInfo` aan die de kalender vervangt door `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Waarom dit belangrijk is:**  
Als je de tekenreeks parseert met de standaardcultuur, zal .NET een format‑exception gooien omdat het `R` (de Reiwa‑era) niet kan koppelen aan een jaar. Door `JapaneseCalendar` te gebruiken, begrijpt de parser era‑symbolen en vertaalt ze naar het juiste Gregoriaanse jaar.

## Stap 2: De era‑gebaseerde tekenreeks omzetten naar een `DateTime`

Nu de cultuur klaar is, kunnen we veilig `DateTime.ParseExact` aanroepen. De opmaak‑string `"ggyy/MM/dd"` vertelt de parser:

- `gg` – era‑aanduiding (bijv. `R` voor Reiwa)  
- `yy` – twee‑cijferig jaartal binnen de era  
- `MM/dd` – maand en dag.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Pro‑tip:** Als je mogelijk data in andere formaten ontvangt (bijv. `"Heisei 30/12/31"`), wikkel het parsen dan in een `try/catch` en val terug op `DateTime.TryParseExact`. Zo voorkom je dat je hele importtaak crasht door één slechte rij.

## Stap 3: De `DateTime` in een Excel‑cel schrijven (Excel‑cel datumwaarde)

Aspose.Cells behandelt een .NET `DateTime` als een native Excel‑datum wanneer je `PutValue` gebruikt. De bibliotheek zet de ticks automatisch om naar het seriële getal van Excel (het aantal dagen sinds 1900‑01‑00). Dit betekent dat de cel een juiste **excel‑cel datumwaarde** weergeeft en je later kunt opmaken met de ingebouwde datumstijlen van Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Wat je in Excel zult zien:**  
Cel C1 bevat nu het seriële getal `44796`, dat Excel weergeeft als `2020‑05‑01` (of welk formaat je ook hebt toegepast). De onderliggende waarde is een echte datum, geen tekenreeks, zodat sorteren werkt zoals verwacht.

## Stap 4: Het werkboek opslaan (Afsluiting)

Als je het werkboek nog niet hebt opgeslagen, doe dat nu. Deze stap gaat niet strikt over het schrijven van de datum/tijd, maar maakt de workflow compleet.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Dat is alles—vier beknopte stappen, en je hebt succesvol **datum/tijd naar Excel geschreven**, inclusief een Japanse era‑datum.

---

![schrijf datum/tijd naar excel voorbeeld](/images/write-datetime-to-excel.png "Schermafbeelding die een C#‑project toont dat een DateTime in Excel‑cel C1 schrijft")

*De bovenstaande afbeelding illustreert het uiteindelijke Excel‑bestand met de datum correct weergegeven in cel C1.*

## Veelgestelde vragen & randgevallen

### Wat als de werkblad‑variabele nog niet klaar is?

Je kunt een nieuw werkboek on‑the‑fly aanmaken:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Hoe bewaar ik de originele Japanse era‑tekenreeks in het blad?

Als je zowel de originele tekenreeks als de geparseerde datum nodig hebt, schrijf ze dan naar aangrenzende cellen:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Werkt dit met oudere .NET‑versies?

Ja. `JapaneseCalendar` bestaat sinds .NET 2.0, en Aspose.Cells ondersteunt .NET Framework 4.5+. Zorg er alleen voor dat je de juiste assembly referereert.

### Wat met tijdzones?

`DateTime.ParseExact` retourneert een **Kind** van `Unspecified`. Als je bron‑datums UTC zijn, converteer ze dan eerst:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Kan ik een aangepast datumformaat instellen (bijv. “yyyy年MM月dd日”)?

Absoluut. Gebruik de eigenschap `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Nu toont Excel `2020年05月01日` terwijl er nog steeds een echte datumwaarde wordt opgeslagen.

## Samenvatting

We hebben alles behandeld wat je nodig hebt om **datum/tijd naar Excel te schrijven** vanuit C#:

1. **Configureer** een Japanse cultuur met `JapaneseCalendar` om **Japanse kalenderdatum**‑strings te **converteren**.  
2. **Parse** de era‑gebaseerde tekenreeks met `DateTime.ParseExact`.  
3. **Voeg** de resulterende `DateTime` in een cel in, zodat er een juiste **excel‑cel datumwaarde** ontstaat.  
4. **Sla** het werkboek op zodat de gegevens behouden blijven.

Met deze vier stappen kun je veilig **datum in werkblad invoegen** ongeacht het bronformaat. De code is volledig uitvoerbaar, vereist alleen Aspose.Cells, en werkt op elke moderne .NET‑runtime.

## Wat is de volgende stap?

- **Bulk‑import:** Loop door rijen in een CSV, parse elke Japanse datum en schrijf ze naar opeenvolgende cellen.  
- **Styling:** Pas voorwaardelijke opmaak toe om vervallen data te markeren.  
- **Performance:** Gebruik `WorkbookDesigner` of `CellStyle`‑caching bij duizenden rijen.  

Voel je vrij om te experimenteren—verwissel de Japanse era voor de Gregoriaanse kalender, wijzig de doelcel, of exporteer naar een ander bestandsformaat (CSV, ODS). Het kernidee blijft hetzelfde: parse, converteer, en **datum/tijd naar Excel schrijven** met vertrouwen.

Happy coding, en moge je spreadsheets altijd correct sorteren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}