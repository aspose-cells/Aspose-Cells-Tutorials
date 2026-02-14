---
category: general
date: 2026-02-14
description: Maak een Excel-werkmap met Aspose.Cells en leer hoe je JSON kunt verwerken,
  JSON naar Excel kunt converteren en JSON in Excel kunt laden in een paar eenvoudige
  stappen.
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: nl
og_description: Maak een Excel-werkmap met Aspose.Cells, leer hoe je JSON verwerkt,
  converteer JSON naar Excel en laad JSON snel en betrouwbaar in Excel.
og_title: Maak een Excel-werkmap van JSON – Stapsgewijze Aspose.Cells‑tutorial
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Maak Excel-werkmap van JSON – Complete Aspose.Cells-gids
url: /nl/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap van JSON – Complete Aspose.Cells-gids

Heb je ooit een **Excel-werkmap** moeten maken van een stuk JSON, maar wist je niet waar te beginnen? Je bent niet de enige. Veel ontwikkelaars lopen tegen hetzelfde probleem aan wanneer ze een JSON‑payload hebben en een nette spreadsheet nodig hebben voor rapportage of gegevensuitwisseling.  

Het goede nieuws? Met **Aspose.Cells** kun je die JSON omzetten in een volledig uitgeruste Excel‑bestand met slechts een paar regels code. In deze tutorial lopen we door **hoe je JSON verwerkt**, **JSON naar Excel converteert**, en **JSON in Excel laadt** met behulp van de krachtige `SmartMarkerProcessor`. Aan het einde heb je een klaar‑te‑opslaan werkmap en een duidelijk beeld van de opties die je kunt aanpassen.

## Wat je zult leren

- Hoe je een Aspose.Cells‑project instelt voor JSON‑verwerking.  
- De exacte code die nodig is om een **Excel-werkmap** te **maken** van een JSON‑array.  
- Waarom de `ArrayAsSingle`‑optie belangrijk is en wanneer je deze wilt wijzigen.  
- Tips voor het verwerken van grotere JSON‑structuren, foutafhandeling en het opslaan van het bestand.  

> **Voorvereisten:** .NET 6+ (of .NET Framework 4.6+), Aspose.Cells for .NET NuGet‑pakket, en een basiskennis van C#. Er zijn geen andere bibliotheken nodig.

---

## Stap 1: Installeer Aspose.Cells en voeg de vereiste namespace toe

Voordat er code wordt uitgevoerd, moet de Aspose.Cells‑bibliotheek in je project worden gerefereerd.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **Pro‑tip:** Als je Visual Studio gebruikt, doet de NuGet Package Manager‑UI hetzelfde—zoek gewoon naar *Aspose.Cells* en klik op Installeren.

---

## Stap 2: Bereid de JSON‑gegevens voor die je wilt converteren

De `SmartMarkerProcessor` werkt met elke JSON‑string, maar je moet bepalen hoe de bibliotheek arrays moet interpreteren. In dit voorbeeld behandelen we een eenvoudige numerieke array als een **enkel record**, wat handig is wanneer je alleen een platte lijst met waarden nodig hebt.

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **Waarom dit belangrijk is:** Standaard behandelt Aspose.Cells elk array‑element als een apart record. Door `ArrayAsSingle = true` in te stellen, wordt de hele array samengevoegd tot één record, wat bij veel rapportagescenario's past.

---

## Stap 3: Maak een nieuw Workbook‑object aan

Nu maken we daadwerkelijk een **Excel-werkmap** in het geheugen. Er wordt nog geen bestand geschreven; we bereiden alleen de container voor.

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

Op dit moment is `workbook.Worksheets[0]` een leeg blad met de naam *Sheet1*. Je kunt het later hernoemen als je wilt.

---

## Stap 4: Configureer SmartMarker‑opties voor JSON‑verwerking

De `SmartMarkerOptions`‑klasse geeft je fijne controle over hoe JSON wordt geïnterpreteerd. De belangrijkste vlag voor ons scenario is `ArrayAsSingle`.

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **Wanneer je dit moet wijzigen:** Als je JSON een verzameling rijen vertegenwoordigt (bijv. een array van objecten), laat `ArrayAsSingle` dan op `false`. Elk object wordt automatisch een nieuwe rij.

---

## Stap 5: Voer Smart Marker‑verwerking uit op het werkblad

Met de werkmap en opties klaar, voeren we de JSON in de processor. De processor scant het werkblad op smart markers (plaatsaanduidingen) en vervangt deze door gegevens uit de JSON. Omdat we geen expliciete markers hebben, maakt de processor gewoon een standaardindeling.

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

Als je wilt bepalen in welke cel de gegevens beginnen, kun je vóór het uitvoeren van de processor een marker zoals `${Array}` toevoegen aan cel **A1**. Voor deze tutorial vertrouwen we op het standaardgedrag, dat de array‑waarden in opeenvolgende cellen vanaf **A1** schrijft.

---

## Stap 6: Sla de werkmap op naar schijf (of stream)

De laatste stap is het opslaan van de werkmap. Je kunt opslaan naar een bestand, een geheugen‑stream, of zelfs direct teruggeven vanuit een web‑API.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Het uitvoeren van het volledige programma produceert een Excel‑bestand met de getallen **1**, **2** en **3** geplaatst in respectievelijk de cellen **A1**, **A2** en **A3**.

---

## Volledig werkend voorbeeld

Hieronder staat de volledige, kant‑klaar console‑applicatie die alle stappen combineert. Kopieer‑en‑plak deze in een nieuw C# console‑project en druk op **F5**.

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Verwachte output in Excel**

| Numbers |
|---------|
| 1       |
| 2       |
| 3       |

De koprij (“Numbers”) is optioneel maar laat zien hoe je handmatige celbewerkingen kunt combineren met smart‑marker verwerking.

---

## Veelgestelde vragen & randgevallen

### Wat als mijn JSON een object is, geen array?

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

Je kunt nog steeds `SmartMarkerProcessor` gebruiken. Plaats markers zoals `${Name}`, `${Age}`, `${Country}` in het werkblad en roep vervolgens `StartSmartMarkerProcessing` aan. De processor zal elke marker vervangen door de bijbehorende waarde.

### Hoe ga ik om met grote JSON‑bestanden (megabytes)?

- **Stream de JSON**: In plaats van de volledige string te laden, lees je het bestand in met een `StreamReader` en geef je de tekst door aan `StartSmartMarkerProcessing`.  
- **Verhoog de geheugenlimiet**: Stel `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` in als je een `OutOfMemoryException` tegenkomt.  
- **Chunk‑verwerking**: Splits de JSON in kleinere arrays en verwerk elk deel op een nieuw werkblad.

### Kan ik exporteren naar CSV in plaats van XLSX?

Absoluut. Na de verwerking roep je simpelweg aan:

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

De gegevensindeling blijft hetzelfde; alleen het bestandsformaat verandert.

### Wat als ik cellen moet opmaken (lettertypen, kleuren) na het laden van JSON?

Je kunt opmaak toepassen na de smart‑marker stap:

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

Omdat de processor eerst wordt uitgevoerd, wordt elke opmaak die je daarna toepast niet overschreven.

---

## Tips & best practices

- **Stel `ArrayAsSingle` altijd bewust in** – het vergeten van deze vlag is een veelvoorkomende oorzaak van onverwachte rij‑duplicatie.  
- **Valideer JSON vóór verwerking** – een misvormde string veroorzaakt een `JsonParseException`. Plaats de aanroep in een `try/catch`‑blok voor een nette foutafhandeling.  
- **Gebruik benoemde smart markers** (`${Orders}`) voor leesbaarheid, vooral bij geneste JSON‑objecten.  
- **Houd de werkmap in het geheugen** als je deze teruggeeft vanuit een web‑API; het verzenden van een `MemoryStream` voorkomt onnodige schijf‑I/O.  
- **Versie‑compatibiliteit**: De bovenstaande code werkt met Aspose.Cells 23.12 en later. Controleer de release‑notes als je een oudere versie gebruikt.

---

## Conclusie

We hebben je zojuist laten zien hoe je een **Excel-werkmap** maakt vanuit JSON met Aspose.Cells, van het installeren van de bibliotheek tot het opslaan van het uiteindelijke bestand. Door `SmartMarkerProcessor` en de opties te beheersen, kun je **JSON in Excel laden**, **JSON naar Excel converteren**, en zelfs de output aanpassen voor complexe rapportagescenario's.  

Klaar voor de volgende stap? Probeer een geneste JSON‑array van objecten te verwerken, voeg voorwaardelijke opmaak toe, of exporteer het resultaat als PDF — allemaal met dezelfde Aspose.Cells‑API. Je data‑naar‑Excel‑pijplijnen zijn nu slechts een paar regels verwijderd.

Als je vragen hebt of tegen een probleem aanloopt, laat dan een reactie achter. Veel plezier met coderen, en geniet van het omzetten van JSON naar mooie spreadsheets! 

![Create Excel workbook with JSON data](/images/create-excel-workbook-json.png "Illustration of a JSON array being transformed into an Excel sheet")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}