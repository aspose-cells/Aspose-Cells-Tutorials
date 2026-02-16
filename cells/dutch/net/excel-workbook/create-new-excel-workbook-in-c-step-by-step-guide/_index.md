---
category: general
date: 2026-02-15
description: Maak een nieuw Excel‑werkboek en leer hoe je EXPAND gebruikt, een reeks
  uitbreidt en de cotangens berekent. Bekijk ook hoe je het werkboek opslaat naar
  een bestand.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: nl
og_description: Maak een nieuw Excel‑werkboek met C#. Leer hoe je EXPAND gebruikt,
  een reeks uitbreidt, de cotangens berekent en het werkboek opslaat naar een bestand.
og_title: Maak een nieuw Excel-werkboek in C# – Complete programmeergids
tags:
- C#
- Aspose.Cells
- Excel automation
title: Maak een nieuw Excel-werkboek in C# – Stapsgewijze handleiding
url: /nl/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een nieuw Excel-werkboek in C# – Complete programmeergids

Heb je ooit een **create new Excel workbook** nodig gehad vanuit code en wist je niet waar je moest beginnen? Je bent niet de enige; veel ontwikkelaars lopen tegen die muur aan bij het automatiseren van rapporten of het bouwen van datapijplijnen. In deze tutorial laten we je precies zien hoe je een nieuw Excel-werkboek maakt, een paar coole formules schrijft, en vervolgens **save workbook to file** voor later inspectie.  

We duiken ook in de fijne kneepjes van de `EXPAND`‑functie, demonstreren **how to use expand** om een kleine reeks om te zetten in een groot blok, leggen **how to expand sequence** in de praktijk uit, en onthullen uiteindelijk **how to calculate cotangent** direct in Excel. Aan het einde heb je een uitvoerbaar C#‑programma dat je in elk .NET‑project kunt gebruiken.

## Wat je nodig hebt

- **Aspose.Cells for .NET** (gratis proefversie of gelicentieerde versie) – de bibliotheek die ons in staat stelt Excel te manipuleren zonder Office geïnstalleerd.  
- **.NET 6+** (of .NET Framework 4.6+).  
- Een bescheiden IDE zoals Visual Studio 2022, VS Code, of Rider.  

Er zijn geen extra NuGet-pakketten nodig naast `Aspose.Cells`. Als je het nog niet hebt, voer dan uit:

```bash
dotnet add package Aspose.Cells
```

Dat is alles—niets anders om in te stellen.

## Stap 1: Maak een nieuw Excel-werkboek

Het eerste wat we doen is een `Workbook`‑object instantieren. Beschouw het als een leeg canvas waar alle bladen, cellen en formules zullen wonen.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **Waarom dit belangrijk is:** Het maken van het werkboek in het geheugen betekent dat we de schijf nooit aanraken totdat we expliciet besluiten om **save workbook to file**. Dit houdt de bewerking snel en stelt je in staat verdere wijzigingen te ketenen zonder I/O‑overhead.

## Stap 2: Hoe `EXPAND` te gebruiken om een reeks uit te breiden

`EXPAND` is een nieuwere Excel-functie die een kleinere array neemt en uitstrekt tot een gedefinieerde grootte. In ons voorbeeld beginnen we met een verticale reeks van drie rijen en zetten die om in een 5 × 5‑blok.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **Uitleg:** `SEQUENCE(3)` produceert `{1;2;3}` (een verticale array). `EXPAND(...,5,5)` vertelt Excel die array te herhalen totdat het een rechthoek van 5 rijen bij 5 kolommen vult, beginnend bij A1. Het resultaat is een matrix waarbij elke kolom de oorspronkelijke drie getallen herhaalt, en de laatste twee rijen leeg zijn omdat de bron slechts drie rijen heeft.

### Verwachte output

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

Je zult hetzelfde patroon over het bereik zien verspreiden zodra het werkboek in Excel wordt geopend.

## Stap 3: Hoe cotangens te berekenen in Excel

De meeste mensen zijn bekend met `SIN`, `COS` en `TAN`, maar `COT` is een handige snelkoppeling voor het reciproke van tangens. Hier is hoe je de cotangens van 45° (die gelijk is aan 1) krijgt met behulp van radialen.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Waarom COT gebruiken?** Direct `COT` aanroepen vermijdt de extra deling die je nodig zou hebben met `1/TAN(...)`, waardoor de formule duidelijker wordt en iets sneller voor grote bladen.

## Stap 4: Evalueer alle formules

Aspose.Cells berekent formules niet automatisch tenzij je het vertelt. De `CalculateFormula`‑methode dwingt een volledige evaluatie af zodat de resulterende waarden in de cellen worden opgeslagen.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **Tip:** Als je veel dure formules hebt, kun je een `CalculationOptions`‑object doorgeven om de prestaties fijn af te stemmen (bijv. multi‑threading inschakelen).

## Stap 5: Sla werkboek op naar bestand

Nu alles klaar is, slaan we eindelijk **save workbook to file** op. Kies een map waar je schrijfrechten voor hebt, en geef het bestand een betekenisvolle naam.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Wat gebeurt er op schijf?** De `Save`‑aanroep schrijft een volledig gevormd `.xlsx`‑pakket, compleet met de uitgevoerde array van `EXPAND` en de berekende cotangenswaarde. Open het bestand in Excel en je ziet het 5 × 5‑blok beginnend bij A1 en het getal `1` in B1.

![Excel-uitvoer die uitgebreide reeks en cotangenswaarde toont](excel-output.png "voorbeeldoutput van nieuw excel-werkboek maken")

*Afbeeldingsalt‑tekst: voorbeeldoutput van nieuw excel-werkboek maken*

### Snelle verificatie

1. Open `output.xlsx`.  
2. Controleer dat cellen **A1:E5** het herhaalde 1‑2‑3‑patroon bevatten.  
3. Kijk naar **B1** – deze moet `1` weergeven.  

Als alles overeenkomt, gefeliciteerd—je hebt Excel succesvol geautomatiseerd!

## Hoe een reeks uit te breiden in andere scenario's

Hoewel het voorbeeld hierboven een statische `SEQUENCE(3)` gebruikt, kun je deze gemakkelijk vervangen door een dynamisch bereik of een andere formule:

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**Wanneer te gebruiken?**  
- Het genereren van placeholder‑tabellen voor sjablonen.  
- Snel een koprij over veel kolommen repliceren.  
- Heat‑map‑roosters bouwen zonder handmatig kopiëren‑plakken.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| `#VALUE!` after `EXPAND` | Bronarray is geen geldig bereik (bijv. bevat fouten) | Maak de brongegevens schoon of wikkel ze in `IFERROR`. |
| Cotangent returns `#DIV/0!` for 0° | `COT(0)` is wiskundig oneindig | Bescherm met `IF(PI()/4=0,0,COT(...))`. |
| Workbook not saved | Pad is ongeldig of er ontbreken schrijfrechten | Gebruik `Path.GetFullPath` en controleer of de map bestaat. |
| Formulas not calculated | `CalculateFormula` weggelaten | Roep het altijd aan vóór `Save`. |

## Bonus: Styling toevoegen (optioneel)

Als je wilt dat de output er mooier uitziet, kun je na de berekeningen een eenvoudige stijl toepassen:

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

Dit fragment is optioneel, maar het illustreert hoe je **create new Excel workbook**‑logica kunt combineren met opmaak in één stap.

## Samenvatting

We hebben het volledige proces doorlopen:

1. **Create new Excel workbook** met Aspose.Cells.  
2. Gebruik **how to use expand** om een kleine `SEQUENCE` om te zetten in een 5 × 5‑matrix.  
3. Toon **how to calculate cotangent** direct in een cel.  
4. Forceer berekening met `CalculateFormula`.  
5. **Save workbook to file** en verifieer het resultaat.

Dit alles is zelf‑voorzien, draait op elke recente .NET-runtime, en vereist slechts één NuGet‑pakket.

## Wat is het volgende?

- **Dynamic data sources:** Haal gegevens op uit een database en voer ze in `EXPAND` in.  
- **Multiple worksheets:** Loop over een verzameling bladen om een volledig rapportboek te genereren.  
- **Advanced formulas:** Verken `LET`, `LAMBDA`, of array‑gebaseerde conditionele logica voor slimmere spreadsheets.

Voel je vrij om te experimenteren—verwissel het `SEQUENCE`‑argument, probeer verschillende hoeken voor `COT`, of combineer met grafiekgeneratie. De mogelijkheden zijn eindeloos wanneer je **create new Excel workbook** programmatisch kunt maken.

---

*Veel plezier met coderen! Als je ergens tegenaan loopt, laat dan een reactie achter of ping me op Twitter @YourHandle. Ik help je graag.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}