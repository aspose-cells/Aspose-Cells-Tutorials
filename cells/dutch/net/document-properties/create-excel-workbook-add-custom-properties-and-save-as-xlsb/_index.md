---
category: general
date: 2026-03-22
description: Maak een Excel-werkmap, voeg aangepaste eigenschappen toe, stel de werkbladnaam
  in en sla op als een XLSB-binair bestand met C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: nl
og_description: Maak een Excel-werkmap, voeg aangepaste eigenschappen toe, stel de
  naam van het werkblad in en sla op als een XLSB-binair bestand met C#.
og_title: Excel-werkmap maken – Aangepaste eigenschappen toevoegen en opslaan als
  XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Maak Excel-werkmap – Voeg aangepaste eigenschappen toe en sla op als XLSB
url: /nl/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken – Aangepaste eigenschappen toevoegen en opslaan als XLSB

Heb je ooit **een Excel-werkmap** programmatisch moeten **maken** en tegelijkertijd metadata willen behouden? Misschien bouw je een rapportage‑engine die elk bestand van een rapport‑ID, auteursnaam of versienummer voorziet. In dat geval bespaart het leren hoe je **aangepaste eigenschappen** kunt **toevoegen**, de **werkbladnaam** kunt **instellen** en uiteindelijk **opslaan als XLSB** je veel handmatige nabewerking.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat precies laat zien hoe je een **binaire Excel‑file** schrijft met C#. Je ziet waarom het XLSB‑formaat de juiste keuze is voor het transporteren van aangepaste eigenschappen, hoe je de meest voorkomende valkuilen vermijdt, en wat je moet doen als je oudere Excel‑versies moet ondersteunen.

---

## Wat je nodig hebt

- **.NET 6+** (of .NET Framework 4.6+). De code werkt op elke recente runtime.  
- **Aspose.Cells for .NET** (gratis proefversie of gelicentieerd). Het levert de `Workbook`, `Worksheet` en `CustomProperties`‑klassen die hieronder worden gebruikt.  
- Een IDE waar je je prettig in voelt – Visual Studio, Rider of zelfs VS Code volstaat.  
- Schrijftoegang tot een map waar het gegenereerde bestand wordt opgeslagen.

Er zijn geen andere externe bibliotheken nodig.

---

## Stap 1: Installeer Aspose.Cells

Voeg eerst het Aspose.Cells‑NuGet‑pakket toe aan je project:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Als je op een CI‑server werkt, sla je licentiesleutel op in een omgevingsvariabele en laad je die tijdens runtime – dit voorkomt dat het “evaluation” watermerk in je output verschijnt.

---

## Stap 2: Excel-werkmap maken – Overzicht

De eerste echte handeling is het **maken van een Excel-werkmap**. Dit object vertegenwoordigt het volledige bestand in het geheugen en geeft je toegang tot werkbladen, stijlen en aangepaste eigenschappen.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Waarom een nieuwe `Workbook` instantieren in plaats van een sjabloon te laden? Een lege werkmap garandeert dat er geen verborgen stijlen of achtergebleven aangepaste eigenschappen aanwezig zijn, wat vooral belangrijk is wanneer je van plan bent een **binaire Excel‑file** te **schrijven** voor downstream‑systemen die een schone basis verwachten.

---

## Stap 3: Werkbladnaam instellen (en waarom het belangrijk is)

Excel‑bladen krijgen standaard de namen “Sheet1”, “Sheet2”, enz. Het geven van een blad een betekenisvolle naam maakt downstream‑verwerking – zoals Power Query of VBA‑macro’s – veel makkelijker leesbaar.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Als je probeert een dubbele naam toe te wijzen, zal Aspose.Cells een `ArgumentException` werpen. Om veilig te zijn, kun je `Worksheets.Exists("Data")` controleren voordat je hernoemt.

---

## Stap 4: Aangepaste eigenschappen toevoegen

Aangepaste eigenschappen worden opgeslagen in de interne XML van de werkmap en reizen mee met het bestand, ongeacht het formaat. Ze zijn perfect om zaken als `ReportId` of `GeneratedBy` in te sluiten.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Waarom aangepaste eigenschappen gebruiken?**  
> • Ze zijn toegankelijk via het Excel‑paneel “Bestand → Info → Eigenschappen”.  
> • Code die de werkmap consumeert kan ze lezen zonder celinhoud te scannen.  
> • Ze overleven formaatconversies (XLSX ↔ XLSB) omdat ze deel uitmaken van de metadata van het bestand.

Je kunt ook datums, booleans of zelfs binaire blobs opslaan, maar houd de payload klein – Excel is geen database.

---

## Stap 5: Opslaan als XLSB (Binaire Excel‑file schrijven)

Het XLSB‑formaat slaat gegevens op in een binaire structuur, waardoor het bestand kleiner en sneller te openen is. Belangrijker nog voor deze tutorial: **aangepaste eigenschappen worden ingebakken in de binaire stroom**, waardoor ze gegarandeerd meereizen met het bestand.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Verwacht resultaat

Na het uitvoeren van het programma vind je `WithCustomProps.xlsb` op je bureaublad. Open het in Excel, ga naar **Bestand → Info → Eigenschappen**, en je ziet `ReportId` en `GeneratedBy` onder *Aangepast* staan.

---

## Stap 6: Randgevallen & Veelgestelde vragen

### Wat als de doelmap alleen‑lezen is?

Omring de `Save`‑aanroep met een `try/catch`‑blok en val terug op een locatie waar de gebruiker wel schrijfrechten heeft, zoals `%TEMP%`. Dit voorkomt dat de applicatie crasht bij permissiefouten.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Kan ik **opslaan als XLSX** en toch de aangepaste eigenschappen behouden?

Ja – wijzig simpelweg `SaveFormat.Xlsb` naar `SaveFormat.Xlsx`. De eigenschappen worden opgeslagen in hetzelfde XML‑deel, dus ze overleven de formatwissel. XLSX‑bestanden zijn echter groter omdat ze zip‑XML zijn, terwijl XLSB betere prestaties biedt voor grote datasets.

### Hoe lees ik later de aangepaste eigenschappen?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Dit fragment print elke aangepaste eigenschap, waardoor downstream‑services eenvoudig de herkomst van het bestand kunnen verifiëren.

---

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je kunt copy‑pasten in een nieuw console‑project. Er ontbreken geen onderdelen – van `using`‑statements tot de laatste `Console.WriteLine` is alles inbegrepen.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Voer het programma uit, open het resulterende bestand en controleer de aangepaste eigenschappen. Dat is het volledige proces van **excel‑werkmap maken**, **aangepaste eigenschappen toevoegen**, **werkbladnaam instellen** en **opslaan als XLSB** in één nette workflow.

---

## Conclusie

Je weet nu precies hoe je een **Excel‑werkmap** maakt, het blad een duidelijke **werkbladnaam** geeft, nuttige metadata **toevoegt met aangepaste eigenschappen**, en uiteindelijk **opslaat als XLSB** om een compact, binair Excel‑bestand te produceren. Deze workflow is betrouwbaar, werkt over .NET‑versies heen en schaalt goed, of je nu één rapport of duizend genereert.

Wat nu? Probeer een datatabel toe te voegen aan het “Data”‑blad, experimenteer met verschillende eigenschapstypen (datums, booleans), of schakel de output over naar **opslaan als XLSB** voor enorme datasets. Je kunt ook de werkmap beveiligen met een wachtwoord – Aspose.Cells maakt dat met één regel code.

Laat gerust een reactie achter als je ergens vastloopt, of deel hoe je dit patroon in je eigen projecten hebt uitgebreid. Veel programmeerplezier!  

---  

![Create Excel workbook screenshot](image.png){alt="Create Excel workbook with custom properties"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}