---
category: general
date: 2026-02-15
description: Maak een Excel-werkmap C#-tutorial die laat zien hoe je een aangepaste
  eigenschap toevoegt, de werkmap opslaat als XLSB en de eigenschapswaarde opvraagt
  — alles in een paar regels code.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsb
- retrieve custom property value
- add custom property excel
language: nl
og_description: Maak stap‑voor‑stap een Excel‑werkmap in C#. Leer een aangepaste eigenschap
  toe te voegen, de werkmap op te slaan als XLSB en de eigenschapswaarde op te halen
  met duidelijke codevoorbeelden.
og_title: Excel-werkmap maken C# – Aangepaste eigenschap toevoegen & XLSB opslaan
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Excel-werkmap maken in C# – Aangepaste eigenschap toevoegen en XLSB opslaan
url: /nl/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/
---

Then closing shortcodes remain.

Also note the note: "For Dutch, ensure proper RTL formatting if needed" - not needed.

Now produce final content with all sections.

Make sure to keep shortcodes exactly as original.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap C# – Voeg aangepaste eigenschap toe & sla op als XLSB

Moet je **een Excel-werkmap C#** maken en wat aangepaste metadata insluiten? In deze gids lopen we door het toevoegen van een aangepaste eigenschap, **het opslaan van de werkmap als XLSB**, en later **het ophalen van de waarde van de aangepaste eigenschap**—alles met beknopte, kant‑klaar code.  

Als je je ooit afvroeg waarom een spreadsheet extra gegevens nodig zou hebben die niet zichtbaar zijn in de cellen, ben je hier op de juiste plek. Beschouw aangepaste eigenschappen als verborgen notities die met het bestand meereizen, perfect om een werkmap te koppelen aan een project‑ID, versie‑tag of een andere zakelijke sleutel.

## Wat je zult leren

- Hoe je een nieuwe werkmap instantiateert met Aspose.Cells voor .NET.  
- De exacte stappen om **een aangepaste eigenschap toe te voegen** in Excel‑stijl, met behulp van de `CustomProperties`‑collectie.  
- De werkmap opslaan in het compacte binaire XLSB‑formaat.  
- Het bestand opnieuw laden en de opgeslagen eigenschap weer ophalen.  

Geen externe configuratiebestanden, geen obscure trucjes—gewoon pure C# die je kunt plakken in een console‑app en laten werken. Het enige vereiste is een referentie naar de Aspose.Cells‑bibliotheek (gratis proefversie of gelicentieerde versie).  

Waarom zou je dit willen? Omdat het insluiten van ID’s direct in het bestand de noodzaak van een aparte database‑lookup elimineert wanneer je de werkmap later opent. Het is een kleine gewoonte die uren debuggen kan besparen in grootschalige rapportage‑oplossingen.

---

![create excel workbook c# example](https://example.com/images/create-excel-workbook-csharp.png "create excel workbook c# example")

*Afbeelding toont een minimale C# console‑project dat een Excel‑werkmap maakt, een aangepaste eigenschap toevoegt en deze opslaat als XLSB.*

## Stap 1: Initialiseer de werkmap & voeg een aangepaste eigenschap toe

Het allereerste wat je nodig hebt is een nieuw `Workbook`‑object. Zodra je dat hebt, biedt de `Worksheets[0].CustomProperties`‑collectie een nette plek om sleutel/waarde‑paren op te slaan.

```csharp
using Aspose.Cells;

namespace ExcelCustomPropDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Create a new workbook instance
            Workbook workbook = new Workbook();

            // Step 2 – Add a custom property named "ProjectId" with a numeric value
            // This is the "add custom property excel" part of the tutorial.
            workbook.Worksheets[0].CustomProperties.Add("ProjectId", 12345);
```

**Waarom dit belangrijk is:**  
- `Workbook()` maakt een in‑memory representatie van een Excel‑bestand, nog geen schijf‑I/O.  
- Het toevoegen van de eigenschap aan het *eerste* werkblad (index 0) zorgt ervoor dat deze op werkmap‑niveau wordt opgeslagen, waardoor hij toegankelijk is ongeacht welk blad de gebruiker bekijkt.  

> **Pro tip:** Aangepaste eigenschappen kunnen strings, nummers, datums of zelfs Booleaanse waarden bevatten. Kies het type dat het beste past bij de gegevens die je wilt opslaan.

## Stap 2: Sla de werkmap op als XLSB

XLSB (Excel Binary Workbook) is een compact, snel‑ladend formaat—ideaal voor grote datasets. De `Save`‑methode neemt een bestandspad en een `SaveFormat`‑enum.

```csharp
            // Step 3 – Save the workbook to disk in XLSB format
            string outputPath = @"C:\Temp\CustomProp.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // At this point the file on disk already contains the custom property.
```

**Waarom XLSB gebruiken?**  
- Het verkleint de bestandsgrootte tot wel 70 % ten opzichte van het klassieke XLSX.  
- Binaire opslag versnelt zowel schrijf‑ als leesbewerkingen, wat handig is voor server‑side automatisering.

## Stap 3: Laad de opgeslagen werkmap en haal de eigenschap op

Nu draaien we het scenario om: open het bestand dat we net hebben geschreven en haal de verborgen waarde weer op. Dit toont aan dat de eigenschap de ronde‑trip heeft overleefd.

```csharp
            // Step 4 – Load the workbook we just saved
            Workbook loadedWorkbook = new Workbook(outputPath);

            // Step 5 – Retrieve the value of the "ProjectId" custom property
            object projectIdValue = loadedWorkbook.Worksheets[0]
                                                .CustomProperties["ProjectId"]
                                                .Value;

            // Display the retrieved value
            System.Console.WriteLine($"Retrieved ProjectId: {projectIdValue}");
        }
    }
}
```

**Wat je zou moeten zien:**  
```
Retrieved ProjectId: 12345
```

Als de eigenschapsnaam verkeerd gespeld is of niet bestaat, gooit de `CustomProperties`‑indexer een `KeyNotFoundException`. Een defensieve aanpak zou zijn:

```csharp
if (loadedWorkbook.Worksheets[0].CustomProperties.Contains("ProjectId"))
{
    // safe to read
}
```

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het volledige programma, klaar om te kopiëren‑en‑plakken in een nieuw console‑project. Geen extra scaffolding nodig.

```csharp
using Aspose.Cells;
using System;

namespace ExcelCustomPropDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a custom property named "ProjectId" (add custom property excel)
            workbook.Worksheets[0].CustomProperties.Add("ProjectId", 12345);

            // 3️⃣ Save the workbook as XLSB (save workbook as xlsb)
            string filePath = @"C:\Temp\CustomProp.xlsb";
            workbook.Save(filePath, SaveFormat.Xlsb);

            // 4️⃣ Load the saved workbook back into memory
            Workbook loaded = new Workbook(filePath);

            // 5️⃣ Retrieve the custom property value (retrieve custom property value)
            object retrieved = loaded.Worksheets[0].CustomProperties["ProjectId"].Value;
            Console.WriteLine($"Retrieved ProjectId: {retrieved}");
        }
    }
}
```

Voer het programma uit, open `C:\Temp\CustomProp.xlsb` in Excel, en je zult niets ongewoons aan de oppervlakte merken—omdat aangepaste eigenschappen per ontwerp verborgen zijn. Toch staan de gegevens er, klaar voor elke downstream‑process.

## Randgevallen & Variaties

| Situatie | Wat aan te passen |
|-----------|-------------------|
| **Meerdere werkbladen** | Voeg de eigenschap toe aan elk blad; deze wordt gerepliceerd op werkmap‑niveau. |
| **String‑eigenschap** | `CustomProperties.Add("Status", "Approved")` – werkt op dezelfde manier. |
| **Ontbrekende eigenschap** | Gebruik `Contains` vóór het indexeren om uitzonderingen te voorkomen. |
| **Grote numerieke ID’s** | Sla ze op als `long` of `string` om overflow te voorkomen. |
| **Cross‑platform** | Aspose.Cells werkt op .NET Core, .NET Framework en zelfs Mono, dus dezelfde code draait in Linux‑containers. |

## Veelgestelde vragen

**V: Werkt dit met de gratis Aspose.Cells‑trial?**  
**A: Ja. De trial ondersteunt volledig `CustomProperties` en het opslaan als XLSB; onthoud alleen het watermerk op het uitvoerbestand.**

**V: Kan ik aangepaste eigenschappen bekijken in Excel?**  
**A: In Excel ga je naar *Bestand → Info → Eigenschappen → Geavanceerde eigenschappen → Aangepast*. Je “ProjectId” wordt daar vermeld.**

**V: Wat als ik een eigenschap moet verwijderen?**  
**A: Roep `CustomProperties.Remove("ProjectId")` aan vóór het opslaan.**

## Samenvatting

Je weet nu hoe je **een Excel-werkmap C#** maakt, een aangepaste eigenschap insluit, **de werkmap opslaat als XLSB**, en later **de waarde van de aangepaste eigenschap** ophaalt. De volledige flow past in één enkele methode, waardoor het een eitje is om te integreren in grotere rapportage‑pijplijnen of document‑generatieservices.

### Wat is het volgende?

- Verken **het toevoegen van meerdere aangepaste eigenschappen** voor versiebeheer, auteur of afdelingscodes.  
- Combineer deze techniek met **cel‑niveau data** om zelf‑beschrijvende rapporten te bouwen.  
- Bekijk **het lezen van aangepaste eigenschappen** uit bestaande derde‑partij XLSX‑bestanden—Aspose.Cells ondersteunt die ook.

Voel je vrij om het voorbeeld aan te passen, de numerieke ID te vervangen door een GUID, of te experimenteren met verschillende bestandsformaten. De API is eenvoudig; de echte kracht komt voort uit hoe je de verborgen metadata gebruikt in je bedrijfslogica.

Veel plezier met coderen! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}