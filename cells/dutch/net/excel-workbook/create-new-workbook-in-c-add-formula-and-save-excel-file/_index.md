---
category: general
date: 2026-02-23
description: Maak een nieuw werkboek programmatisch aan in C# en voeg een formule
  toe aan een cel. Leer hoe je EXPAND gebruikt en sla vervolgens het Excel‑werkboek
  moeiteloos op.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: nl
og_description: Maak een nieuw werkboek via code in C#. Voeg een formule toe aan een
  cel, leer hoe je EXPAND gebruikt, en sla het Excel‑werkboek binnen enkele seconden
  op.
og_title: Maak een nieuw werkboek in C# – Voeg formule toe en sla Excel‑bestand op
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Nieuw werkboek maken in C# – Formule toevoegen en Excel‑bestand opslaan
url: /nl/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

.

Also translate the "Visual Summary" heading etc.

Let's produce the translated content.

We'll keep code block placeholders unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe Werkmap Maken in C# – Formule Toevoegen en Excel‑bestand Opslaan

Heb je je ooit afgevraagd hoe je **nieuwe werkmap**‑objecten vanuit code kunt maken zonder Excel te openen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een spreadsheet on‑the‑fly moeten genereren—misschien voor een rapport, een export, of een snelle data‑dump.  

Het goede nieuws? In deze gids zie je precies hoe je **nieuwe werkmap** maakt, een **formule toevoegt aan een cel**, en vervolgens **excel‑werkmap opslaat** met slechts een paar regels C#. We duiken ook in **hoe je expand gebruikt** zodat je dynamische arrays kunt genereren zonder handmatig te kopiëren. Aan het einde kun je **excel‑bestand programmatisch maken** en naar gebruikers of downstream‑services verzenden.

## Vereisten

- .NET 6.0 of later (elke recente .NET‑runtime werkt)
- Aspose.Cells for .NET (gratis proefversie of gelicentieerde versie) – deze bibliotheek levert de `Workbook`‑ en `Worksheet`‑klassen die hieronder worden gebruikt.
- Een basisbegrip van C#‑syntaxis—geen diepgaande Excel‑kennis vereist.

Als je die al hebt, prima! Zo niet, haal Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) en je bent klaar om te starten.

---

## Stap 1: Nieuwe Werkmap Maken – De Basis

Om te beginnen moeten we een frisse werkmap‑object instantieren. Beschouw het als het openen van een gloednieuwe Excel‑file die volledig leeg is.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Waarom dit belangrijk is:** De `Workbook`‑klasse is het startpunt voor elke Excel‑manipulatie. Door een nieuwe instantie te maken, reserveren we geheugen voor bladen, stijlen en formules—allemaal zonder het bestandssysteem aan te raken.

---

## Stap 2: Toegang tot het Eerste Werkblad

Elke nieuwe werkmap wordt geleverd met een standaard werkblad (genaamd *Sheet1*). We halen dat op zodat we data en formules kunnen plaatsen.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro‑tip:** Als je meerdere bladen nodig hebt, roep dan simpelweg `workbook.Worksheets.Add("MySheet")` aan en werk met het geretourneerde `Worksheet`‑object.

---

## Stap 3: Formule Toevoegen aan Cel – Met EXPAND

Nu het leuke gedeelte: een formule invoegen. De `EXPAND`‑functie is perfect wanneer je een statische array wilt omzetten in een groter, automatisch ingevuld bereik.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Hoe de EXPAND‑Formule Werkt

| Argument | Betekenis |
|----------|-----------|
| `{1,2,3}` | De bronarray (een horizontale lijst van drie getallen) |
| `5`       | Gewenst aantal rijen in het resultaat |
| `1`       | Gewenst aantal kolommen (houd het 1 om verticaal te blijven) |

Wanneer Excel dit evalueert, ontstaat er een **verticale** lijst:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Waarom EXPAND gebruiken?** Het elimineert de noodzaak voor handmatig kopiëren of VBA‑loops. De functie herschikt data dynamisch, waardoor je spreadsheets robuuster en makkelijker te onderhouden zijn.

---

## Stap 4: Excel‑Werkmap Opslaan – Resultaat Vastleggen

Met de formule op zijn plaats is de laatste stap het wegschrijven van de werkmap naar schijf. Je kunt elke map kiezen waar je schrijfrechten voor hebt.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Wat je ziet:** Open `ExpandFormula.xlsx` in Excel, en cel `A1` toont de uitgebreide array. De formule zelf blijft in de cel, dus als je de bronarray wijzigt, wordt de output automatisch bijgewerkt.

---

## Optioneel: Output Programma­matig Verifiëren

Als je liever Excel niet handmatig opent, kun je de waarden teruglezen om te bevestigen dat ze aan de verwachtingen voldoen.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Het uitvoeren van bovenstaande code print:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Veelgestelde Vragen & Randgevallen

| Vraag | Antwoord |
|----------|----------|
| **Kan ik EXPAND gebruiken met een grotere bronarray?** | Absoluut. Vervang simpelweg `{1,2,3}` door elke constante of cel‑bereik, bv. `EXPAND(A1:C1,10,1)`. |
| **Wat als ik een horizontaal resultaat wil?** | Verwissel de rij‑/kolom‑argumenten: `EXPAND({1,2,3},1,5)` levert een 1‑rij, 5‑kolom spreiding op. |
| **Werkt dit op oudere Excel‑versies?** | `EXPAND` is beschikbaar vanaf Excel 365/2021. Voor oudere versies moet je de array simuleren met `INDEX`/`SEQUENCE`. |
| **Moet ik `workbook.CalculateFormula()` aanroepen?** | Nee. Aspose.Cells evalueert formules automatisch bij het opslaan, zodat de waarden direct zichtbaar zijn. |
| **Hoe voeg ik meer dan één blad toe vóór het opslaan?** | Roep `workbook.Worksheets.Add("SecondSheet")` aan en herhaal de cel‑manipulatiestappen op het nieuwe werkblad. |

---

## Volledig Werkend Voorbeeld

Hieronder vind je het complete, kant‑klaar te draaien programma. Kopieer‑plak het in een console‑app, pas het output‑pad aan, en druk op **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Verwachte console‑output:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Open het gegenereerde bestand en je ziet dezelfde getallen in kolom **A**.

---

## Visuele Samenvatting

![Voorbeeld van nieuwe werkmap maken](create-new-workbook.png "Schermafbeelding die een nieuw werkmap toont dat is aangemaakt met create new workbook in C#")

*De afbeelding illustreert de vers net gegenereerde werkmap met het EXPAND‑resultaat.*

---

## Conclusie

Je weet nu hoe je **nieuwe werkmap** maakt, **formule toevoegt aan een cel**, en **excel‑werkmap opslaat** met C#. Door **hoe je expand gebruikt** te beheersen, kun je dynamische arrays genereren zonder handmatige inspanning, en het hele proces stelt je in staat **excel‑bestand programmatisch te maken** voor elke automatiseringsscenario.

Wat nu? Probeer de constante array te vervangen door een bereik‑referentie, experimenteer met verschillende `EXPAND`‑dimensies, of combineer meerdere formules over verschillende bladen. Hetzelfde patroon werkt voor grafieken, opmaak en zelfs draaitabellen—dus blijf ontdekken.

Als je tegen problemen aanloopt, laat dan een reactie achter. Veel plezier met coderen, en geniet van de kracht van programmatisch Excel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}