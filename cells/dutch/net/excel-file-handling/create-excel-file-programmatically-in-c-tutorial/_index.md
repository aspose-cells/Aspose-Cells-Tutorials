---
category: general
date: 2026-08-11
description: Maak een Excel‑bestand programmatisch in C# met Aspose.Cells. Parse een
  Japanse era‑datum, schrijf deze naar een cel en sla het werkboek op.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel file programmatically
- datetime.parseexact custom format
- write date to excel cell
- how to save excel file c#
language: nl
lastmod: 2026-08-11
og_description: Maak een Excel‑bestand programmatically in C# met Aspose.Cells. Leer
  hoe je een Japanse jaartelling datum kunt parseren met DateTime.ParseExact met een
  aangepast formaat, schrijf de datum naar een Excel‑cel en sla de werkmap efficiënt
  op.
og_image_alt: Screenshot of an Excel workbook with a parsed Japanese era date in cell
  A1
og_title: Maak een Excel‑bestand programmatically in C# – volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel file programmatically in C# using Aspose.Cells. Parse
    a Japanese era date, write it to a cell, and save the workbook.
  headline: Create excel file programmatically in C# – tutorial
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- DateTime parsing
title: Excel-bestand programmatically maken in C# – tutorial
url: /nl/net/excel-file-handling/create-excel-file-programmatically-in-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een Excel‑bestand programmatisch in C# – tutorial

Als je een **excel‑bestand programmatisch wilt maken** kun je dat doen in een paar regels C#‑code. Deze gids laat zien hoe je een Excel‑werkmap genereert met Aspose.Cells, een Japanse jaartijd‑datum parseert met een **DateTime.ParseExact‑aangepast formaat**, die datum in een werkbladcel schrijft, en uiteindelijk **het Excel‑bestand opslaat in C#‑stijl**. Aan het einde heb je een kant‑klaar *.xlsx*‑bestand dat een correct geconverteerde Gregoriaanse datum bevat.

Je leert hoe je:

* Een werkmap initialiseren zonder een sjabloon.  
* Een op een jaartijd gebaseerd tekenreeks zoals `"R3/04/01"` omzetten naar een `DateTime`.  
* De `DateTime`‑waarde invoegen in een specifieke cel (`A1`).  
* De werkmap opslaan op schijf met één `Save`‑aanroep.

Geen extra bibliotheken nodig naast Aspose.Cells en de .NET base class library.

---

## Vereisten

Zorg er vóór je begint voor dat je het volgende hebt:

* **.NET 6.0** of later geïnstalleerd (de code werkt ook met .NET Framework 4.6+).  
* Een geldige **Aspose.Cells**‑licentie of een gratis evaluatiekopie.  
* Basiskennis van C#‑syntaxis en Visual Studio (of een IDE naar keuze).

---

## Maak excel‑bestand programmatisch – initialiseer werkmap

De eerste stap is het maken van een leeg werkmap‑object. Aspose.Cells biedt een `Workbook`‑klasse die een volledig Excel‑bestand in het geheugen vertegenwoordigt.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();               // creates an empty .xlsx structure
        var worksheet = workbook.Worksheets[0];      // the default first sheet is named "Sheet1"
```

**Waarom dit belangrijk is:**  
Het programmatisch aanmaken van de werkmap elimineert de noodzaak van een fysiek sjabloonbestand, waardoor je implementatie‑voetafdruk klein blijft en je bestanden on‑the‑fly kunt genereren voor rapporten, facturen of data‑exports.

---

## Gebruik DateTime.ParseExact‑aangepast formaat voor Japanse jaartijd‑datums

Datum‑strings die Japanse jaartijd‑symbolen bevatten (bijv. "R" voor Reiwa) kunnen niet worden geparseerd met de standaard `DateTime.Parse`. Je moet een **aangepast formaat** en een Japanse cultuur opgeven die de jaartijd‑aanduiding herkent.

```csharp
        // Step 2: Define the era‑based date string (Reiwa 3, April 1)
        string eraDate = "R3/04/01";

        // Step 3: Create a CultureInfo that knows Japanese eras
        var japaneseCulture = new CultureInfo("ja-JP");

        // Step 4: Parse the era date using a custom format string
        //   "g"  = era designator (R, H, etc.)
        //   "yy" = two‑digit year within the era
        //   "MM" = month (01‑12)
        //   "dd" = day of month (01‑31)
        DateTime parsedDate = DateTime.ParseExact(
            eraDate,
            "ggy/MM/dd",
            japaneseCulture,
            DateTimeStyles.None);
```

**Waarom dit belangrijk is:**  
`DateTime.ParseExact` garandeert dat de invoer overeenkomt met het patroon dat je opgeeft, waardoor locale‑afhankelijke ambiguïteiten worden voorkomen. Het patroon "ggy/MM/dd" vertelt .NET om het eerste teken als een jaartijd (`g`) te behandelen, gevolgd door een twee‑cijferig jaar (`yy`), maand en dag. Het gebruik van `japaneseCulture` zorgt ervoor dat de jaartijd‑symbolen correct worden geïnterpreteerd, waardoor een Gregoriaanse `DateTime` (`2021‑04‑01` in het voorbeeld) ontstaat.

---

## Schrijf datum naar Excel‑cel met Aspose.Cells

Nu je een `DateTime`‑instantie hebt, kun je deze in elke werkbladcel plaatsen. Aspose.Cells formatteert de cel automatisch volgens de standaard datumstijl van de werkmap.

```csharp
        // Step 5: Write the DateTime value into cell A1
        worksheet.Cells["A1"].PutValue(parsedDate);

        // Optional: Apply a custom number format if you want a specific display
        worksheet.Cells["A1"].Style.Number = 14; // 14 = "m/d/yyyy" in Excel
```

**Waarom dit belangrijk is:**  
Door `PutValue` te gebruiken laat je Aspose.Cells het celtype (datum, getal, tekst) afleiden van het .NET‑type dat je opgeeft. Deze aanpak is veiliger dan het schrijven van een geformatteerde string, omdat Excel de datumsemantiek behoudt—waardoor je later kunt sorteren, filteren of berekeningen op de kolom kunt uitvoeren.

---

## Hoe excel‑bestand opslaan in C# – werkmap finaliseren

De laatste stap is het opslaan van de werkmap in het geheugen naar een fysiek bestand. Aspose.Cells ondersteunt vele formaten; hier gebruiken we het moderne `.xlsx`‑formaat.

```csharp
        // Step 6: Save the workbook to the desired location
        string outputPath = @"C:\Temp\JapaneseEra.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Waarom dit belangrijk is:**  
Het aanroepen van `Save` met `SaveFormat.Xlsx` schrijft een standaard‑conform Office Open XML‑bestand dat kan worden geopend in Excel, LibreOffice of elke viewer die het formaat ondersteunt. De methode behandelt ook alle onderliggende compressie en verpakking, zodat je zelf geen zip‑streams hoeft te beheren.

---

## Verwacht resultaat

Wanneer je het programma uitvoert:

| Cel  | Waarde (weergave) | Onderliggend type |
|------|-------------------|-------------------|
| A1   | 4/1/2021          | Date (DateTime)   |

Het bestand `JapaneseEra.xlsx` zal één blad bevatten met de naam **Sheet1** en de Gregoriaanse datum `2021‑04‑01` in cel **A1**. Excel zal de cel als een datum behandelen, waardoor verdere berekeningen mogelijk zijn, zoals `=A1+30` om 30 dagen toe te voegen.

---

## Veelvoorkomende variaties en randgevallen

| Situatie | Oplossing |
|----------|-----------|
| **Andere jaartijd** (bijv. Heisei `H30/12/31`) | Wijzig de invoer‑string; hetzelfde patroon "ggy/MM/dd" werkt omdat de Japanse `CultureInfo` alle jaartijden kent. |
| **Viercijferig jaar** (bijv. `R2023/04/01`) | Gebruik "ggyyyy/MM/dd" als formaat‑string. |
| **Ontbrekend jaartijd‑symbool** | Geef een fallback‑formaat op zoals "yyyy/MM/dd" en probeer `DateTime.TryParseExact` met meerdere patronen. |
| **Ongeldige datum** (bijv. `R3/13/01`) | Plaats `ParseExact` in een `try/catch`‑blok of gebruik `DateTime.TryParseExact` om parse‑fouten op een nette manier af te handelen. |

**Pro tip:** Valideer altijd de geparseerde `DateTime` voordat je deze naar het werkblad schrijft, vooral wanneer de brondata afkomstig is van gebruikersinvoer of externe bestanden.

---

## Samenvatting

* Je **hebt een excel‑bestand programmatisch gemaakt** met Aspose.Cells.  
* Je hebt een Japanse jaartijd‑string geparseerd met **DateTime.ParseExact‑aangepast formaat**.  
* Je **hebt een datum naar een excel‑cel geschreven** met `PutValue`.  
* Je leerde **hoe je een excel‑bestand opslaat in C#** met één `Save`‑aanroep.

Deze vier stappen vormen een herbruikbaar patroon voor elk scenario waarin je cultureel specifieke datums in Excel‑rapporten moet importeren.

---

## Volgende stappen

* Verken **celopmaak** (lettertypen, kleuren, randen) om je rapporten een gepolijste uitstraling te geven.  
* Gebruik **Workbook.Save** met andere formaten (`Csv`, `Pdf`) om data te exporteren voor verschillende doelgroepen.  
* Combineer deze techniek met **bulk‑data‑invoer** (`Cells.ImportDataTable`) voor grootschalige importen.  

Voel je vrij om te experimenteren met verschillende jaartijd‑symbolen, aangepaste getalformaten of meerdere werkbladen. Dezelfde kernlogica—creëren, parseren, schrijven, opslaan—geldt voor alle Excel‑automatiseringstaken in C#.

---

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een Excel‑werkmap te maken en op te slaan als ODS met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hoe specifieke pagina's van een Excel‑bestand op te slaan als PDF met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Hoe een Excel‑werkmap te maken en op te slaan als SVG met Aspose.Cells voor Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}