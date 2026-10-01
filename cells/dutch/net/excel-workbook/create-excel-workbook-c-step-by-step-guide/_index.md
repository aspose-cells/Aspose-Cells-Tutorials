---
category: general
date: 2026-02-14
description: Maak een Excel-werkmap in C# en leer hoe je uitbreidt en de cotangens
  berekent. Volg deze volledige tutorial om een formule naar een cel te schrijven,
  een Excel‑bestand op te slaan in C# en Excel‑automatisering onder de knie te krijgen.
draft: false
keywords:
- create excel workbook c#
- how to use expand
- how to calculate cotangent
- save excel file c#
- write formula to cell
language: nl
og_description: Maak een Excel-werkmap in C# met Aspose.Cells. Leer hoe je expand
  gebruikt, de cotangens berekent, een formule in een cel schrijft en een Excel-bestand
  in C# in enkele minuten opslaat.
og_title: Maak Excel-werkboek C# – Volledige programmeertutorial
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Maak een Excel‑werkmap in C# – Stapsgewijze handleiding
url: /nl/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken met C# – Stapsgewijze handleiding

Altijd al **een Excel-werkmap met C#** willen maken die formules schrijft en het bestand opslaat, maar niet wisten waar te beginnen? Je bent niet de enige. In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien **hoe je EXPAND gebruikt**, **hoe je cotangens berekent**, en precies **hoe je een formule naar een cel schrijft** met de populaire Aspose.Cells‑bibliotheek. Aan het einde heb je een .xlsx‑bestand dat je direct in Excel kunt openen en de resultaten kunt zien.

## Wat je gaat leren

We behandelen alles, van het opzetten van het project tot het opslaan van de uiteindelijke werkmap:

* **Create Excel workbook C#** – maak een instantie van de werkmap en pak het eerste werkblad.  
* **How to use EXPAND** – vergroot een klein bereik tot een 5 × 5‑matrix met één enkele formule.  
* **How to calculate cotangent** – gebruik de COT‑functie op π/4 en krijg een waarde van 1.  
* **Write formula to cell** – wijs formules programmatically toe, niet alleen statische waarden.  
* **Save Excel file C#** – sla de werkmap op schijf zodat je deze in Excel kunt openen.

Geen externe services, geen verborgen magie—alleen plain C# en één NuGet‑pakket.

> **Pro tip:** Aspose.Cells werkt met .NET 6, .NET 7 en het volledige .NET Framework, dus je kunt dit in elk modern C#‑project gebruiken.

![Create Excel Workbook C# screenshot](/images/create-excel-workbook.png){: .align-center alt="Create Excel Workbook C# example"}

## Vereisten

* Visual Studio 2022 (of een andere IDE naar keuze).  
* .NET 6 SDK of hoger.  
* **Aspose.Cells for .NET** – voeg het toe via NuGet: `Install-Package Aspose.Cells`.  
* Basiskennis van C#‑syntaxis—geen geavanceerde kennis nodig.

---

## Stap 1: Het Excel‑werkmap‑object in C# maken

Allereerst hebben we een `Workbook`‑instantie nodig, die het volledige Excel‑bestand vertegenwoordigt. De constructor maakt een lege werkmap met een standaardwerkblad al aanwezig.

```csharp
using Aspose.Cells;

public class ExcelDemo
{
    public static void Main()
    {
        // Step 1 – create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx
        Worksheet ws = workbook.Worksheets[0];            // the default sheet is index 0
```

Waarom pakken we `Worksheets[0]`? Omdat de werkmap altijd start met één blad met de naam “Sheet1”. Direct toegang tot dit blad bespaart ons later een `Add`‑aanroep.

---

## Stap 2: Hoe je EXPAND gebruikt – Een klein bereik uitbreiden tot een 5×5‑matrix

De **EXPAND**‑functie is een dynamische‑array‑eigenschap die een bronbereik “uitspreidt” over een groter gebied. In C# stellen we simpelweg de formule‑string in; Excel doet het zware werk wanneer het bestand wordt geopend.

```csharp
        // Step 2 – apply EXPAND to grow A2:B3 into a 5×5 matrix starting at A1
        // The source range A2:B3 will spill over the cells A1:E5 when you open the file.
        ws.Cells["A1"].Formula = "=EXPAND(A2:B3,5,5)";
```

Merk op dat we het bronbereik (`A2:B3`) niet van tevoren hoeven te vullen. Excel evalueert het on‑the‑fly. Als je later waarden in `A2:B3` schrijft, wordt de uitgepriete matrix automatisch bijgewerkt.

---

## Stap 3: Hoe je cotangens berekent – Met de COT‑functie

COT is geen .NET‑methode; het is een Excel‑werkbladfunctie. Door de formule aan een cel toe te wijzen, laten we Excel het resultaat berekenen.

```csharp
        // Step 3 – calculate cotangent of π/4 (which equals 1)
        ws.Cells["C1"].Formula = "=COT(PI()/4)";
```

Wanneer je de opgeslagen werkmap opent, toont cel **C1** `1`. Dit laat zien dat elke native Excel‑functie—trigonometrisch, statistisch of tekst‑gebaseerd—vanuit C# kan worden geïnjecteerd.

---

## Stap 4: Formule naar cel schrijven – Een snelle samenvatting

Als je je afvraagt **hoe je een formule naar een cel schrijft** zonder de aanhalingstekensregels te breken, is het patroon simpel:

```csharp
        ws.Cells["<address>"].Formula = "<Excel formula>";
```

* Begin de string altijd met een gelijkteken (`=`).  
* Gebruik dubbele aanhalingstekens voor de C#‑string en escape interne aanhalingstekens indien nodig.  
* Het is niet nodig `CalculateFormula` aan te roepen—Aspose.Cells behoudt de formule zodat Excel deze bij het laden kan evalueren.

---

## Stap 5: Excel‑bestand opslaan met C# – De werkmap bewaren

Tot slot schrijven we de werkmap naar schijf. Je kunt elk pad kiezen dat je wilt; zorg er alleen voor dat de map bestaat.

```csharp
        // Step 5 – save the workbook so you can open it in Excel
        string outputPath = @"C:\Temp\output.xlsx";   // change to your preferred folder
        workbook.Save(outputPath);
    }
}
```

Na het uitvoeren van het programma navigeer je naar `C:\Temp\output.xlsx` en open je het bestand. Je zou moeten zien:

| A | B | C | D | E |
|---|---|---|---|---|
| *uitgespreide matrix* (5 × 5) | … | **1** (in C1) | … | … |

De matrix vult de cellen **A1:E5**, en **C1** toont het cotangens‑resultaat.

---

## Veelgestelde vragen & randgevallen

### Wat als ik een groter uitgespreid gebied nodig heb?

Verander simpelweg de tweede en derde argumenten van `EXPAND`. Voor een 10 × 10‑uitspreiding gebruik je `=EXPAND(A2:B3,10,10)`.

### Kan ik EXPAND gebruiken met een benoemd bereik?

Zeker. Vervang `A2:B3` door de naam van je bereik, bijvoorbeeld `=EXPAND(MyRange,5,5)`.

### Evalueert Aspose.Cells de formules automatisch?

Standaard **behoudt** Aspose.Cells de formules zodat Excel ze kan berekenen. Als je de waarden server‑side wilt laten berekenen, roep dan `workbook.CalculateFormula()` aan vóór het opslaan.

### Wat als de doelmap niet bestaat?

Plaats de `Save`‑aanroep in een try‑catch‑blok, of maak de map eerst aan:

```csharp
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
workbook.Save(outputPath);
```

---

## Volledig werkend voorbeeld (Klaar om te kopiëren)

```csharp
using System;
using System.IO;
using Aspose.Cells;

public class ExcelDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Apply EXPAND to grow A2:B3 into a 5×5 matrix starting at A1
        ws.Cells["A1"].Formula = "=EXPAND(A2:B3,5,5)";

        // Compute cotangent of π/4 (result should be 1)
        ws.Cells["C1"].Formula = "=COT(PI()/4)";

        // Optional: write some sample data into the source range so the spill shows numbers
        ws.Cells["A2"].PutValue(10);
        ws.Cells["B2"].PutValue(20);
        ws.Cells["A3"].PutValue(30);
        ws.Cells["B3"].PutValue(40);

        // Save the workbook to disk
        string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "output.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Het uitvoeren van dit programma maakt een `output.xlsx` op je bureaublad. Open het in Excel en je ziet direct de uitgespreide matrix en de cotangens‑waarde.

---

## Conclusie

We hebben zojuist laten zien **hoe je een Excel-werkmap met C# maakt** vanaf nul, **hoe je EXPAND gebruikt** om dynamische arrays te genereren, **hoe je cotangens berekent**, en de exacte stappen om **een formule naar een cel te schrijven** en **een Excel‑bestand met C# op te slaan**. De aanpak is eenvoudig, maakt gebruik van één goed onderhouden bibliotheek, en werkt op alle moderne .NET‑runtime‑omgevingen.

Vervolgens kun je overwegen:

* Grafieken of voorwaardelijke opmaak toe te voegen met Aspose.Cells.  
* `workbook.CalculateFormula()` te gebruiken voor berekeningen aan de server‑kant.  
* De werkmap te exporteren naar PDF of CSV voor rapportage‑pijplijnen.

Probeer deze ideeën, experimenteer met andere Excel‑functies, en laat de automatisering het zware werk doen. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}