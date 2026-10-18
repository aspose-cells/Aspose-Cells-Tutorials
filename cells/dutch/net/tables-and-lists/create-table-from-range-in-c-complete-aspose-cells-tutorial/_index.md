---
category: general
date: 2026-03-30
description: Tabel maken van bereik in C# met Aspose.Cells – gegevens toevoegen aan
  cellen, bereik converteren naar ListObject en Excel opslaan zonder filter.
draft: false
keywords:
- create table from range
- create excel workbook c#
- add data to cells
- convert range to listobject
- save excel without filter
language: nl
og_description: Maak een tabel van een bereik in C# met Aspose.Cells. Leer hoe je
  gegevens aan cellen toevoegt, een bereik converteert naar een ListObject en Excel
  opslaat zonder filter.
og_title: Tabel maken vanuit bereik in C# – Complete Aspose.Cells tutorial
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Tabel maken vanuit bereik in C# – Complete Aspose.Cells‑tutorial
url: /nl/net/tables-and-lists/create-table-from-range-in-c-complete-aspose-cells-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabel maken vanuit bereik in C# – Complete Aspose.Cells tutorial

Heb je ooit moeten **create table from range** in C# maar wist je niet hoe je een eenvoudige gegevensblok in een volledig uitgeruste Excel‑tabel kon omzetten? Je bent niet de enige. Of je nu rapporten automatiseert, scorekaarten genereert, of gewoon gegevens opschoont voor downstream‑analyse, het beheersen van deze kleine truc kan je veel handmatig werk besparen.

In deze gids lopen we het volledige proces door: **create excel workbook c#**, **add data to cells**, **convert range to ListObject**, en uiteindelijk **save excel without filter**. Aan het einde heb je een kant‑klaar fragment dat je in elk .NET‑project dat Aspose.Cells gebruikt, kunt plaatsen.

---

## Vereisten

- .NET 6+ (of .NET Framework 4.7.2+) geïnstalleerd  
- Aspose.Cells voor .NET (NuGet‑pakket `Aspose.Cells`) – de nieuwste versie op het moment van schrijven (23.10) werkt perfect.  
- Een basisbegrip van C#‑syntaxis – geen diepgaande Excel‑interop‑kennis vereist.

Als je dat hebt, laten we beginnen.

---

## Stap 1: Een Excel‑werkmap maken in C#

Eerst hebben we een nieuw workbook‑object nodig. Beschouw dit als het lege Excel‑bestand dat uiteindelijk onze tabel zal bevatten.

```csharp
using Aspose.Cells;

// Initialize a new workbook – this is equivalent to opening a blank .xlsx file.
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first (default) worksheet.
```

> **Pro tip:** `Workbook()` zonder argumenten maakt een workbook met één standaardwerkblad, wat perfect is voor snelle demo's. Als je meerdere bladen nodig hebt, kun je ze later toevoegen met `workbook.Worksheets.Add()`.

---

## Stap 2: Gegevens toevoegen aan cellen

Nu vullen we het blad met een kleine dataset – twee kolommen (Name, Score) en drie rijen met waarden. Dit demonstreert **add data to cells** op een nette, leesbare manier.

```csharp
// Header row
worksheet.Cells["A1"].PutValue("Name");
worksheet.Cells["B1"].PutValue("Score");

// Data rows
worksheet.Cells["A2"].PutValue("Alice");
worksheet.Cells["B2"].PutValue(85);
worksheet.Cells["A3"].PutValue("Bob");
worksheet.Cells["B3"].PutValue(92);
```

Waarom `PutValue` gebruiken? Het detecteert automatisch het gegevenstype (string vs. numeriek) en formatteert de cel dienovereenkomstig, waardoor je niet met `Style`‑objecten hoeft te rommelen voor eenvoudige scenario's.

> **Verwachte output:** Na deze stap, als je de workbook in Excel opent, zie je een raster van twee kolommen met de koppen “Name” en “Score”, gevolgd door twee rijen met gegevens.

---

## Stap 3: Het bereik omzetten naar een ListObject (tabel)

Hier gebeurt de magie: dat eenvoudige bereik omzetten in een Excel‑tabel (genaamd een **ListObject** in de Aspose.Cells‑API). Dit voegt niet alleen visuele opmaak toe, maar maakt ook ingebouwde functies mogelijk zoals sorteren, filteren en gestructureerde verwijzingen.

```csharp
// Define the range boundaries.
// startRow and startColumn are zero‑based indexes.
// rowCount includes the header row.
int startRow = 0;          // Row 1 in Excel
int startColumn = 0;       // Column A
int rowCount = 3;          // Header + 2 data rows
int columnCount = 2;       // Two columns: Name & Score

// Add a ListObject to the worksheet and retrieve the object.
int listIndex = worksheet.ListObjects.Add(startRow, startColumn, rowCount, columnCount);
ListObject table = worksheet.ListObjects[listIndex];

// Turn on the UI filter dropdowns so users can interact with the table.
table.ShowAutoFilter = true;
```

> **Waarom een ListObject gebruiken?**  
> - **Structured references**: Formules kunnen naar kolommen verwijzen op naam.  
> - **Auto‑filter UI**: Gebruikers krijgen dropdown‑pijltjes voor snelle filtering.  
> - **Styling**: Je kunt later met één regel ingebouwde tabelstijlen toepassen.

---

## Stap 4: De AutoFilter‑UI verwijderen (Excel opslaan zonder filter)

Soms heb je een schoon blad nodig zonder filterpijltjes – bijvoorbeeld wanneer de workbook een eindrapport is. Aspose.Cells 23.10 introduceerde een eenvoudige manier om de filter‑UI volledig te verwijderen.

```csharp
// Remove the filter UI completely.
table.AutoFilter = null;        // Clears the underlying filter object.
table.ShowAutoFilter = false;   // Hides the dropdown arrows.
```

Merk op dat we de gegevens niet verwijderen; we schakelen alleen de visuele filterbesturingen uit. Dit voldoet aan de **save excel without filter**‑vereiste.

---

## Stap 5: De workbook opslaan

Tot slot schrijf je de workbook naar schijf. Het bestand zal de tabel bevatten, maar zonder enige filter‑UI.

```csharp
// Choose a folder you have write access to.
string outputPath = @"C:\Temp\NoAutoFilter.xlsx";
workbook.Save(outputPath);
```

Open `NoAutoFilter.xlsx` in Excel – je ziet de tabel gestyled met de standaardopmaak, maar zonder filterpijltjes. De gegevens blijven intact, en het bestand is klaar voor distributie.

---

![Screenshot showing create table from range in Excel using Aspose.Cells](image.png "Create table from range screenshot")

*Image alt text:* **Schermafbeelding die het maken van een tabel vanuit bereik in Excel met Aspose.Cells toont** – visueel bewijs dat de tabel bestaat zonder filter‑dropdowns.

---

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een console‑applicatie. Het bevat alle bovenstaande stappen, plus een paar extra opmerkingen voor duidelijkheid.

```csharp
using System;
using Aspose.Cells;

namespace AsposeTableDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add data to cells – this is the “add data to cells” part.
            worksheet.Cells["A1"].PutValue("Name");
            worksheet.Cells["B1"].PutValue("Score");
            worksheet.Cells["A2"].PutValue("Alice");
            worksheet.Cells["B2"].PutValue(85);
            worksheet.Cells["A3"].PutValue("Bob");
            worksheet.Cells["B3"].PutValue(92);

            // 3️⃣ Convert the range into a ListObject (i.e., create table from range).
            int startRow = 0, startColumn = 0, rowCount = 3, columnCount = 2;
            int listIdx = worksheet.ListObjects.Add(startRow, startColumn, rowCount, columnCount);
            ListObject table = worksheet.ListObjects[listIdx];
            table.ShowAutoFilter = true;   // optional UI filter

            // 4️⃣ Remove the AutoFilter UI – “save excel without filter”.
            table.AutoFilter = null;
            table.ShowAutoFilter = false;

            // 5️⃣ Save the workbook.
            string filePath = @"C:\Temp\NoAutoFilter.xlsx";
            workbook.Save(filePath);

            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

Voer het programma uit en open vervolgens `C:\Temp\NoAutoFilter.xlsx`. Je ziet een mooi opgemaakte tabel, geen filterpijltjes, en de gegevens die we hebben ingevoerd. Dat is de volledige **create excel workbook c#**‑workflow in minder dan 60 regels code.

---

## Veelgestelde vragen & randgevallen

**Q: Wat als mijn gegevensbereik niet aaneengesloten is?**  
A: Aspose.Cells vereist een rechthoekig bereik voor `ListObjects.Add`. Als je niet‑aaneengesloten gegevens hebt, bouw dan eerst een tijdelijk bereik (bijv. kopieer de delen naar een nieuw werkblad) en zet dat bereik vervolgens om.

**Q: Kan ik een aangepaste tabelstijl toepassen?**  
A: Zeker. Na het maken van de `ListObject`, stel `table.TableStyleType = TableStyleType.TableStyleMedium9;` in (of een van de 65 ingebouwde stijlen). Dit is een handige manier om de tabel aan te laten sluiten bij je bedrijfsbranding.

**Q: Hoe houd ik het filter maar verberg ik de pijltjes?**  
A: De filterlogica zit in `table.AutoFilter`. Het instellen van `ShowAutoFilter = false` verbergt alleen de UI; het onderliggende filter blijft bestaan. Dus je kunt later nog steeds programmatisch rijen filteren.

**Q: Hoe zit het met grote datasets (10k+ rijen)?**  
A: Dezelfde API werkt, maar overweeg automatische berekeningen uit te schakelen (`workbook.CalcEngine = false`) vóór bulk‑invoegingen voor betere prestaties, en schakel ze daarna weer in.

---

## Samenvatting

We hebben zojuist behandeld hoe je **create table from range** in C# kunt gebruiken met Aspose.Cells, stap voor stap — van **create excel workbook c#**, via **add data to cells**, naar **convert range to ListObject**, en uiteindelijk **save excel without filter**. De code is compleet, uitvoerbaar en klaar voor productie.

Vervolgens kun je overwegen om:

- Voorwaardelijke opmaak toevoegen om de hoogste scores te markeren.  
- De workbook exporteren naar PDF met `workbook.Save("Report.pdf", SaveFormat.Pdf);`.  
- `table.Columns["Score"].DataBodyRange.Sort` gebruiken om de tabel programmatisch te sorteren.

Voel je vrij om te experimenteren met verschillende datasets, tabelstijlen, of zelfs meerdere werkbladen. De API is flexibel genoeg om alles aan te kunnen, van een kleine scoretabel tot een enorme financiële grootboek.

Heb je vragen of loop je tegen een probleem aan? Laat een reactie achter hieronder of stuur me een bericht op GitHub. Veel plezier met coderen, en geniet van het omzetten van ruwe bereiken in gepolijste Excel‑tabellen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}