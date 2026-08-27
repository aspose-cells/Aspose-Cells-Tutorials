---
category: general
date: 2026-02-09
description: Hoe maak je een array in Excel met C# uitgelegd in enkele minuten – leer
  reeksnummers genereren, COT gebruiken en het werkboek opslaan als XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: nl
og_description: Hoe je een array in Excel maakt met C# wordt stap voor stap behandeld,
  inclusief het genereren van opeenvolgende nummers, het gebruik van COT en het opslaan
  van de werkmap als XLSX.
og_title: Hoe maak je een array in Excel met C# – Snelle gids
tags:
- C#
- Excel
- Aspose.Cells
title: Hoe maak je een array in Excel met C# – Stapsgewijze handleiding
url: /nl/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een array te maken in Excel met C# – Stapsgewijze gids

Heb je je ooit afgevraagd **hoe je een array** in Excel met C# kunt maken zonder uren te zoeken in documentatie? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een dynamisch spill‑bereik nodig hebben, een snelle trigonometrische waarde, of gewoon een schoon XLSX‑bestand dat op schijf wordt opgeslagen. In deze tutorial lossen we dat probleem meteen op—door een klein werkboek te bouwen dat een uitklapende array‑formule schrijft, een cotangens‑berekening invoegt, en alles opslaat als een XLSX‑bestand.  

We zullen ook een paar extra trucjes toevoegen: reeksenummers genereren, de `COT`‑functie beheersen, en ervoor zorgen dat het bestand terechtkomt waar jij het wilt. Aan het einde heb je een herbruikbare snippet die je in elk .NET‑project kunt plaatsen. Geen poespas, alleen werkende code.

> **Pro tip:** Het voorbeeld maakt gebruik van de populaire **Aspose.Cells**‑bibliotheek, maar de concepten zijn toepasbaar op andere Excel‑automatiseringspakketten (EPPlus, ClosedXML) met slechts kleine aanpassingen.

---

## Wat je nodig hebt

- **.NET 6** of later (de code compileert ook op .NET Framework 4.7+)  
- **Aspose.Cells for .NET** – je kunt het ophalen via NuGet (`Install-Package Aspose.Cells`)  
- Een teksteditor of IDE (Visual Studio, Rider, VS Code…)  
- Schrijfrechten op een map waar het uitvoerbestand wordt opgeslagen  

Dat is alles—geen extra configuratie, geen COM‑interop, alleen een schoon beheerd assembly.

---

## Stap 1: Hoe een array te maken in Excel – Werkboek initialiseren

Het allereerste wat je moet doen wanneer je **een array wilt maken** in een Excel‑blad, is een workbook‑object aanmaken. Beschouw het workbook als een leeg canvas; het werkblad is waar je je formules gaat schilderen.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Waarom `Workbook()` zonder parameters gebruiken? Het geeft je een in‑memory workbook met een standaardblad, wat perfect is voor snelle, programmatiche taken. Als je een bestaand bestand moet openen, geef je simpelweg het bestandspad door aan de constructor.

---

## Stap 2: Reeksenummers genereren met EXPAND en SEQUENCE

Nu we een blad hebben, laten we het **reeksnummers genereren** deel van de puzzel beantwoorden. De nieuwe dynamische array‑functies van Excel (`SEQUENCE`, `EXPAND`) laten ons een verticale lijst van 3 rijen maken en automatisch laten uitvloeien naar een 3 × 5‑bereik.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**Wat gebeurt er hier?**  
- `SEQUENCE(3,1,1,1)` → produceert een verticale array `{1;2;3}`.  
- `EXPAND(...,5,1)` → neemt die drie‑rijen kolom en strekt deze uit tot vijf kolommen, waarbij de extra cellen met lege waarden worden gevuld.  

Wanneer je het resulterende `output.xlsx` opent, zie je een 3 × 5‑blok beginnend bij **A1** waarbij de eerste kolom 1, 2, 3 bevat en de overige vier kolommen leeg zijn. Deze techniek is de ruggengraat van **array‑stijl spill‑bereiken** zonder handmatig elke cel te schrijven.

---

## Stap 3: Hoe COT te gebruiken – Een trigonometrische formule toevoegen

Als je ook benieuwd bent naar **hoe je cot gebruikt** binnen een Excel‑formule, is de `COT`‑functie een handige manier om de cotangens van een hoek in radialen te krijgen. Laten we `cot(π/4)` berekenen, wat **1** moet opleveren.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Merk op dat we `PI()` hebben gebruikt om de radiale waarde van 180° te krijgen, en vervolgens door 4 delen om 45° te bereiken. Excel doet het zware werk, en de cel **B1** zal `1` tonen zodra het werkboek wordt geopend. Dit toont **hoe je cot gebruikt** voor snelle engineering‑ of financiële berekeningen zonder een aparte wiskundebibliotheek te gebruiken.

---

## Stap 4: Werkboek opslaan als XLSX – Het bestand bewaren

Al het plezier van het maken van een array en het invoegen van formules is verloren als je het bestand nooit naar schijf schrijft. Hier is de eenvoudige manier om **werkboek op te slaan als xlsx** met Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Waarom `SaveFormat.Xlsx` specificeren? Het garandeert het moderne OpenXML‑formaat, dat universeel leesbaar is (Excel, LibreOffice, Google Sheets). Als je een ouder `.xls`‑bestand nodig hebt, verwissel je gewoon de enum.

---

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het volledige, kant‑klaar programma. Kopieer‑en‑plak het in een console‑project, herstel het Aspose.Cells‑NuGet‑pakket, en druk op **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Verwacht resultaat** na het openen van `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Kolom A toont de getallen 1‑3 die door `SEQUENCE` zijn gegenereerd.  
- Kolom B bevat de waarde **1** uit de `COT`‑formule.  
- Kolommen C‑E zijn leeg, wat het opvul‑effect van `EXPAND` illustreert.

---

## Veelgestelde vragen & randgevallen

### Wat als ik meer rijen of kolommen nodig heb?

Pas simpelweg de argumenten van `SEQUENCE` en `EXPAND` aan.  
- `SEQUENCE(10,2,5,2)` zou een matrix van 10 rijen × 2 kolommen opleveren, beginnend bij 5 en oplopend met 2.  
- `EXPAND(...,10,5)` zou het resultaat opvullen tot 10 kolommen en 5 rijen.

### Werkt dit met oudere Excel‑versies?

Dynamische array‑functies (`SEQUENCE`, `EXPAND`) vereisen Excel 365 of 2019+. Voor legacy‑bestanden kun je terugvallen op klassieke formules of waarden direct schrijven via `Cells[row, col].PutValue(value)`.

### Kan ik de formule schrijven in R1C1‑stijl?

Absoluut. Vervang `A1` door `Cells[0, 0]` en gebruik de `FormulaR1C1`‑eigenschap:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### Hoe zit het met cultuurspecifieke decimale scheidingstekens?

Aspose.Cells respecteert de locale van het werkboek. Als je een specifieke cultuur nodig hebt, stel dan `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` in vóór het schrijven van formules.

---

## Visuele samenvatting

![hoe een array te maken in Excel met C#](/images/how-to-create-array-excel-csharp.png "hoe een array te maken in Excel met C#")

*De screenshot toont het uiteindelijke spill‑bereik en het cotangens‑resultaat.*

---

## Conclusie

Daar heb je het—**hoe je een array maakt** in Excel met C# vanaf nul, reeksenummers genereert, de `COT`‑functie benut, en **het werkboek opslaat als XLSX** in één net programma. De belangrijkste punten zijn:

1. Gebruik `Workbook`‑ en `Worksheet`‑objecten om je Excel‑automatisering te starten.  
2. Benut dynamische array‑functies (`SEQUENCE`, `EXPAND`) voor flexibele spill‑bereiken.  
3. Voeg trigonometrische functies zoals `COT` toe voor snelle wiskunde zonder extra bibliotheken.  
4. Bewaar het resultaat met `SaveFormat.Xlsx` om een universeel leesbaar bestand te krijgen.

Klaar voor de volgende stap? Probeer `COT(PI()/4)` te vervangen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}