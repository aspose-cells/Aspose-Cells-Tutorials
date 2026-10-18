---
category: general
date: 2026-03-25
description: Maak een nieuw werkboek in C# en leer hoe je EXPAND gebruikt, de cotangens
  berekent en het werkboek opslaat naar een bestand met stap‑voor‑stap code.
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: nl
og_description: Maak een nieuw werkboek in C# en zie meteen hoe je EXPAND gebruikt,
  de cotangens berekent en het werkboek opslaat naar een bestand.
og_title: Maak een nieuw werkboek in C# – Complete programmeergids
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Maak een nieuw werkboek in C# – Complete programmeergids
url: /nl/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuw werkboek maken in C# – Complete programmeergids

Heb je ooit moeten **nieuw werkboek maken** in C# maar wist je niet waar te beginnen? Je bent niet de enige. Of je nu een rapportage‑pipeline automatiseert of gewoon met Excel‑formules in code speelt, de mogelijkheid om een werkboek te creëren, formules zoals `EXPAND` of `COT` toe te voegen, en vervolgens **werkboek opslaan naar bestand** is een kernvaardigheid voor elke .NET‑ontwikkelaar.

In deze tutorial lopen we een real‑world voorbeeld door dat precies dat doet: we maken een nieuw werkboek, gebruiken de `EXPAND`‑functie om een statische array om te zetten in een dynamische kolom, berekenen een cotangens met de `COT`‑functie, en slaan tenslotte **werkboek opslaan naar bestand** op als een `.xlsx`. Aan het einde heb je een kant‑klaar fragment, begrijp je *waarom* elke aanroep belangrijk is, en zie je een paar handige variaties voor randgevallen.

> **Pro tip:** Alle code hieronder werkt met de nieuwste versie van Aspose.Cells voor .NET (vanaf maart 2026). Als je een oudere release gebruikt, is de API‑structuur grotendeels hetzelfde, maar controleer de namespace‑imports nog even.

## Wat je nodig hebt

- .NET 6.0 of later (het voorbeeld richt zich op .NET 6, maar .NET 5 werkt ook)  
- Aspose.Cells voor .NET geïnstalleerd via NuGet (`Install-Package Aspose.Cells`)  
- Een bescheiden hoeveelheid C#‑kennis (je kunt dit)  

Dat is alles—geen extra DLL’s, geen COM‑interop, en zeker geen Excel geïnstalleerd op de machine. Klaar? Laten we beginnen.

![Schermafbeelding die laat zien hoe je een nieuw werkboek maakt in C#](assets/create-new-workbook.png){alt="Schermafbeelding die laat zien hoe je een nieuw werkboek maakt in C#"}

## Stap 1: Maak een nieuw werkboek

Het eerste wat je moet doen is de `Workbook`‑klasse instantieren. Beschouw het als het openen van een leeg Excel‑bestand in het geheugen. Dit object bevat een collectie werkbladen, stijlen en alles wat je later nodig zult hebben.

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Waarom meteen het eerste werkblad pakken? De meeste quick‑start voorbeelden werken met één blad, en de `Worksheets[0]` accessor is de snelste manier om een referentie te krijgen zonder te loopen. Als je later meerdere bladen nodig hebt, kun je ze toevoegen met `workbook.Worksheets.Add()`.

## Stap 2: Hoe gebruik je EXPAND om dynamische bereiken te genereren

`EXPAND` is een nieuwere Excel‑functie die een array neemt en deze aanvult tot een opgegeven grootte. In onze code breiden we de letterlijke array `{1,2,3}` uit tot een **5‑rijen kolom** beginnend bij cel `A1`. De syntaxis binnen de string is precies wat je in Excel zou typen, dus je kunt het later rechtstreeks in een cel plakken als je wilt.

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### Wat gebeurt er onder de motorkap?

- `{1,2,3}` is een horizontale array‑literal.  
- Het tweede argument (`5`) vertelt Excel de array uit te breiden tot **5 rijen**.  
- Het derde argument (`1`) dwingt een **enkele kolom** als output.  

Als je het derde argument weglaten, zal Excel proberen de oorspronkelijke vorm te behouden, wat je een 5×3 blok kan geven in plaats van één kolom. Dat is een veelvoorkomende valkuil bij het eerste experimenteren met `EXPAND`.

#### Variaties die je misschien nodig hebt

| Gewenste vorm | Formule‑voorbeeld |
|---------------|-------------------|
| 3‑rijen, 2‑kolom blok | `=EXPAND({1,2,3},3,2)` |
| Alleen naar beneden vullen (zelfde kolom) | `=EXPAND({10,20},10,1)` |
| Uitbreiden naar een groter aantal kolommen | `=EXPAND({5},5,4)` |

Voel je vrij om de literals of de afmetingen te wijzigen zodat ze passen bij je data‑generatielogica.

## Stap 3: Hoe bereken je cotangens met de COT‑functie

De `COT`‑functie geeft de cotangens van een hoek uitgedrukt in radialen. In ons voorbeeld berekenen we de cotangens van 45° (π/4 radialen). Het resultaat, `1`, komt terecht in cel `B1`.

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### Waarom COT gebruiken in plaats van handmatig te berekenen?

Excel weet al hoe het de trigonometrische conversie moet uitvoeren, zodat je floating‑point afrondingsfouten vermijdt die kunnen ontstaan als je `1 / TAN(angle)` probeert. Bovendien blijft de formule leesbaar voor iedereen die later de spreadsheet bekijkt.

#### Randgeval: hoeken buiten 0‑360°

Als je een hoek groter dan `2*PI()` (of een negatieve) invoert, zal Excel deze automatisch omzetten, maar het resultaat kan verrassend zijn. Om veilig te zijn, kun je de hoek eerst normaliseren:

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

Dat fragment laat zien hoe je `MOD` combineert met `COT` voor robuuste berekeningen.

## Stap 4: Hoe werkboek opslaan naar bestand (Excel)

Nu de formules op hun plaats staan, is de laatste stap **werkboek opslaan naar bestand**. Je kunt elk pad kiezen dat je wilt—zorg er alleen voor dat de map bestaat en je schrijfrechten hebt.

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Wat wordt er precies opgeslagen?

Wanneer je `output.xlsx` in Excel opent, zie je:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- Kolom **A** bevat de uitgebreide array `{1,2,3}` gevolgd door twee lege cellen (omdat we om 5 rijen vroegen).  
- Cel **B1** toont `1`, de cotangens van 45°.  

Als je het werkboek vernieuwt (druk op `F9` of schakel automatische berekening in), zal Excel de formules evalueren en de resultaten tonen. Aspose.Cells biedt ook een `CalculateFormula`‑methode als je de waarden nodig hebt zonder Excel te openen:

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## Veelgestelde vragen & valkuilen

| Vraag | Antwoord |
|-------|----------|
| **Moet ik de berekening handmatig activeren?** | Nee. Standaard slaat Aspose.Cells formules op zoals ze zijn; Excel berekent ze bij het openen. Gebruik `workbook.CalculateFormula()` voor pre‑calculatie. |
| **Kan ik formules in meerdere cellen tegelijk schrijven?** | Absoluut. Gebruik `ws.Cells["D1:D5"].Formula = "=RAND()"` om een bereik te vullen met willekeurige getallen. |
| **Wat als mijn doelmap niet bestaat?** | Maak deze eerst aan: `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **Wordt `EXPAND` ondersteund in oudere Excel‑versies?** | `EXPAND` kwam met Excel 365/2019. Als je compatibiliteit met oudere bestanden nodig hebt, overweeg dan `INDEX`/`SEQUENCE`‑combinaties. |
| **Hoe verberg ik de formule‑weergave?** | Stel `ws.Cells["A1"].FormulaHidden = true;` in en bescherm het blad als je niet wilt dat gebruikers de onderliggende formule zien. |

## Wrap‑Up

Je weet nu **hoe je een nieuw werkboek** maakt in C#, de kracht van de `EXPAND`‑functie benut om dynamische arrays te genereren, een cotangens berekent met `COT`, en **werkboek opslaan naar bestand** als een nette Excel‑document. Het volledige, uitvoerbare voorbeeld staat in de code‑fragmenten hierboven—kopieer het naar een console‑app, druk op `F5`, en open het resulterende `output.xlsx` om de magie te zien.

### Wat is de volgende stap?

- **Verken andere dynamische array‑functies** zoals `SEQUENCE`, `FILTER` en `SORT`.  
- **Automatiseer het maken van grafieken** met de rijke chart‑API van Aspose.Cells.  
- **Integreer met gegevensbronnen** (SQL, CSV) en voer die waarden programmatically in formules in.  
- **Leer hoe je Excel opslaat als PDF** of andere formaten—perfect voor rapportage‑pipelines.

Voel je vrij om te experimenteren: wijzig de array‑waarden, pas de hoek aan, of schrijf het resultaat naar een ander blad. De mogelijkheden zijn eindeloos wanneer je C# combineert met de moderne formule‑engine van Excel.

Happy coding, and may your spreadsheets always calculate correctly!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}