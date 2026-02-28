---
category: general
date: 2026-02-28
description: Hoe maak je een array in Excel met C#. Leer hoe je getallen genereert,
  formules evalueert, een Excel-werkmap maakt en een Excel-bestand in enkele minuten
  opslaat.
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: nl
og_description: Hoe maak je een array in Excel met C#. Deze tutorial laat zien hoe
  je getallen genereert, een formule evalueert, een werkmap maakt en het bestand opslaat.
og_title: Hoe maak je een array in Excel met C# – Complete gids
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Hoe maak je een array in Excel met C# – Stapsgewijze handleiding
url: /nl/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je een array in Excel met C# – Complete programmeertutorial

Heb je je ooit afgevraagd **hoe je een array** in Excel programmatically kunt maken met C#? Je bent niet de enige—ontwikkelaars vragen constant om een snelle manier om een blok getallen te genereren zonder ze handmatig in te typen. In deze gids lopen we stap voor stap door hoe je **een Excel‑werkmap maakt**, een formule toevoegt die **getallen genereert**, **de formule evalueert**, en tenslotte **het Excel‑bestand opslaat** zodat je het in Excel kunt openen en het resultaat kunt zien.

We gebruiken de Aspose.Cells‑bibliotheek omdat deze ons volledige controle geeft over formules en berekeningen zonder dat Excel geïnstalleerd hoeft te zijn. Als je een andere bibliotheek verkiest, blijven de concepten hetzelfde—vervang gewoon de API‑aanroepen.

## Wat deze tutorial behandelt

- Het opzetten van een C#‑project met het benodigde NuGet‑pakket.  
- Het aanmaken van een nieuwe werkmap (dat is het *create excel workbook*‑deel).  
- Het schrijven van een formule die een 4‑rij × 3‑kolom‑array bouwt met `SEQUENCE` en `WRAPCOLS`.  
- Het dwingen van de engine om **de formule te evalueren** zodat de array tot leven komt.  
- Het opslaan van de werkmap naar schijf (**save excel file**) en het controleren van de output.  

Aan het einde heb je een uitvoerbaar programma dat een Excel‑blad produceert dat er als volgt uitziet:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![How to create array in Excel – resulting sheet after running the C# code](image.png)

*(Afbeeldings‑alt‑tekst bevat het primaire trefwoord “how to create array” voor SEO.)*

---

## Vereisten

- .NET 6.0 SDK of later (de code werkt ook op .NET Framework 4.6+).  
- Visual Studio 2022 of een andere editor naar keuze.  
- NuGet‑pakket **Aspose.Cells** (gratis proefversie beschikbaar).  

Er is geen extra Excel‑installatie nodig omdat Aspose.Cells de berekeningsengine intern bevat.

---

## Stap 1: Het project opzetten en Aspose.Cells importeren

Om te beginnen maak je een console‑app en voeg je de bibliotheek toe:

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

Open nu **Program.cs** en voeg de namespace toe:

```csharp
using Aspose.Cells;
```

*Waarom dit belangrijk is*: Het importeren van `Aspose.Cells` geeft ons de `Workbook`, `Worksheet` en berekeningsklassen die we nodig hebben om **excel workbook te maken** en met formules te werken.

---

## Stap 2: De werkmap en doel‑werkblad maken

We hebben een verse `Workbook`‑object nodig; het eerste werkblad (`Worksheets[0]`) zal onze array hosten.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*Uitleg*: De `Workbook`‑klasse vertegenwoordigt het volledige Excel‑bestand. Standaard bevat het één blad, wat perfect is voor een eenvoudige demo. Als je later meer bladen nodig hebt, kun je `workbook.Worksheets.Add()` aanroepen.

---

## Stap 3: Een formule schrijven die **getallen genereert** en een array vormt

De dynamische‑array‑functies van Excel (`SEQUENCE` en `WRAPCOLS`) laten ons een blok waarden produceren met één enkele formule. Dit is de exacte string die we gaan toewijzen:

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*Waarom dit werkt*:  
- `SEQUENCE(12,1,1,1)` geeft een verticale lijst van de getallen 1‑12.  
- `WRAPCOLS(...,3)` neemt die lijst en vult deze over drie kolommen, waarbij het automatisch over de volgende rijen “spilt”.  

Als je de werkmap in Excel **zonder** de formule eerst te evalueren opent, zie je alleen de formule‑tekst in `A1`. De volgende stap dwingt de berekening af.

---

## Stap 4: **De formule evalueren** zodat de array tot leven komt

Aspose.Cells rekent formules niet automatisch opnieuw uit bij het schrijven, dus roepen we expliciet de berekeningsengine aan:

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*Wat er gebeurt*: `Calculate()` doorloopt elke cel die een formule bevat, berekent het resultaat en schrijft de waarden terug. Dit is het **how to evaluate formula**‑deel van onze tutorial. Na deze aanroep bevatten de cellen A1:C4 de getallen 1‑12, net als een native Excel‑spill.

---

## Stap 5: **Excel‑bestand opslaan** en het resultaat verifiëren

Tot slot slaan we de werkmap op schijf op:

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Open `output.xlsx` in Excel en je ziet de 4 × 3‑array die we hebben gegenereerd. Als je een versie van Excel ouder dan 365/2019 gebruikt, worden de dynamische‑array‑functies niet herkend—Aspose.Cells schrijft nog steeds de geëvalueerde waarden, zodat het bestand bruikbaar blijft.

*Pro‑tip*: Gebruik `SaveFormat.Xlsx` als je een specifiek formaat moet forceren, bijv. `workbook.Save(outputPath, SaveFormat.Xlsx);`.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

Hieronder staat het complete programma. Plak het in **Program.cs**, voer `dotnet run` uit, en je krijgt `output.xlsx` in de projectmap.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**Verwachte console‑output**:

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

Open het bestand en je ziet de getallen 1‑12 precies zoals eerder getoond.

---

## Variaties & randgevallen

### 1. Oudere Excel‑versies zonder dynamische arrays  
Als je doelgroep Excel 2016 of ouder gebruikt, bestaan `SEQUENCE` en `WRAPCOLS` niet. Een snelle oplossing is om de getallen in C# te genereren en direct te schrijven:

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

Deze handmatige lus bootst hetzelfde resultaat na, zij het met meer code. Het **how to generate numbers**‑concept blijft identiek.

### 2. De grootte van de array aanpassen  
Wil je een 5 × 5‑rooster met getallen 1‑25? Pas simpelweg de `SEQUENCE`‑argumenten en het kolomaantal van `WRAPCOLS` aan:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. Naam‑bereiken gebruiken voor hergebruik  
Je kunt het uitgespilde bereik een naam geven voor latere formules:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

Nu kan elk ander blad direct `MyArray` refereren.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---|---|---|
| **Formule spilt niet** | `Calculate()` weggelaten of aangeroepen vóór het instellen van de formule. | Roep altijd `workbook.Calculate()` **na** het toewijzen van de formule aan. |
| **Bestand opgeslagen maar leeg** | Per ongeluk `SaveFormat.Csv` gebruikt. | Gebruik `SaveFormat.Xlsx` of laat het formaat weg zodat Aspose het inferreert. |
| **Dynamische |  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}