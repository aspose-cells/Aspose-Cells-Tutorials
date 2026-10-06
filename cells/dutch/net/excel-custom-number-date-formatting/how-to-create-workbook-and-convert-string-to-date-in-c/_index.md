---
category: general
date: 2026-02-15
description: Hoe een werkmap te maken, een tekenreeks naar datum te converteren en
  een cel als datum te formatteren met Aspose.Cells. Leer hoe je het getalformaat
  van een cel instelt en Excel-datums eenvoudig leest.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: nl
og_description: Hoe een werkmap te maken, een tekenreeks om te zetten naar een datum
  en de cel als datum te formatteren. Complete stapsgewijze handleiding voor het lezen
  van Excel‑datums.
og_title: Hoe een werkmap te maken en een string naar datum te converteren in C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hoe een werkmap te maken en een string naar datum te converteren in C#
url: /nl/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een werkmap te maken en een tekenreeks naar datum te converteren in C#

Heb je je ooit afgevraagd **hoe je een werkmap maakt** die een platte tekst zoals `"R3-04-01"` omzet in een echte `DateTime` waarde? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan bij het ophalen van gegevens uit legacy‑systemen of gebruikersinvoer. Het goede nieuws? Met een paar regels C# en Aspose.Cells kun je het in een handomdraai doen, zonder handmatige parsing.

In deze tutorial lopen we het volledige proces door: een werkmap maken, een datum‑tekenreeks invoegen, een juiste **format cell as date** toepassen, de engine dwingen **set cell number format** uit te voeren, en uiteindelijk **read excel date** terug te lezen als een `DateTime`. Aan het einde heb je een uitvoerbare code‑fragment die je in elk .NET‑project kunt gebruiken.

## Vereisten

- .NET 6+ (of .NET Framework 4.7.2+)
- **Aspose.Cells for .NET** NuGet‑pakket (`Install-Package Aspose.Cells`)
- Een basisbegrip van C#‑syntaxis
- Een IDE zoals Visual Studio of VS Code (elk werkt)

Er is geen extra configuratie nodig—Aspose.Cells verzorgt alle zware taken intern.

## Stap 1: Hoe een werkmap te maken – initialiseert het Excel‑bestand

Eerst hebben we een nieuw workbook‑object nodig. Beschouw het als een leeg notitieboek waarin elk werkblad een pagina is.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Waarom dit belangrijk is:* Het maken van de werkmap geeft ons een container voor cellen, stijlen en formules. Zonder deze is er nergens om de datum‑tekenreeks te plaatsen.

## Stap 2: Tekenreeks naar datum converteren – ruwe tekst invoegen

Nu plaatsen we de ruwe datum‑tekenreeks in cel **A1** van het eerste werkblad. De tekenreeks gebruikt een aangepast formaat (`R3-04-01`) dat Excel niet direct herkent.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Waarom we dit doen:* `PutValue` slaat de letterlijke tekst op. Als we direct een `DateTime` zouden instellen, zou het aangepaste formaat verloren gaan. Het als tekst behouden stelt ons later in staat een **set cell number format** toe te passen die Excel vertelt hoe het moet interpreteren.

## Stap 3: Cel opmaken als datum – stijlnummer 14 toepassen

Excel's ingebouwde datumstijl 14 komt overeen met `mm-dd-yy`. Door deze stijl toe te wijzen vertellen we de engine: “Behandel de inhoud van deze cel als een datum.”

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*Wat er onder de motorkap gebeurt:* De eigenschap `Number` verwijst naar Excel's interne nummer‑formaat‑ID’s. Wanneer de werkmap opnieuw berekent, zal Excel proberen de tekst om te zetten naar een seriële datum met behulp van het opgegeven formaat.

## Stap 4: Celnummerformaat instellen – herberekening forceren

Excel zal de tekst niet magisch converteren totdat we het vragen formules te evalueren (of in dit geval de cel opnieuw te interpreteren). Het aanroepen van `CalculateFormula` triggert die conversie.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Tip:* Als je met veel cellen werkt, kun je `CalculateFormula` één keer aanroepen nadat je alle opmaak hebt voltooid—dit bespaart enkele milliseconden.

## Stap 5: Excel‑datum lezen – de DateTime‑waarde ophalen

Ten slotte halen we de `DateTime`‑representatie uit de cel. Aspose.Cells maakt deze beschikbaar via `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Verwachte output (ervan uitgaande dat de standaard Gregoriaanse kalender wordt gebruikt):**

```
2023-04-01 00:00:00
```

Merk op hoe het `"R3-"`‑voorvoegsel wordt genegeerd omdat Excel's datum‑parser zich richt op het numerieke gedeelte wanneer de stijl een datum is. Als je tekenreeksen andere voorvoegsels bevatten, moet je ze mogelijk vooraf verwerken, maar voor veel legacy‑formaten werkt deze aanpak perfect.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het volledige, kant‑klaar programma:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Sla dit op als `Program.cs`, herstel het Aspose.Cells‑pakket, en voer `dotnet run` uit. Je zou de opgemaakte `DateTime` in de console moeten zien.

## Veelvoorkomende variaties & randgevallen

### Verschillende datum‑tekenreeksen

Als je brongegevens eruitzien als `"2023/04/01"` of `"01‑Apr‑2023"`, kun je nog steeds dezelfde workflow gebruiken—verander gewoon de **Number**‑eigenschap naar een formaat dat bij het patroon past (bijv. `Number = 15` voor `d-mmm-yy`).  

### Locale‑specifieke formaten

Excel respecteert de locale‑instellingen van de werkmap. Om US‑stijl parsing af te dwingen, stel je de cultuur van de werkmap in:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### Wanneer de tekenreeks niet wordt herkend

Soms kan Excel geen datum afleiden (bijv. `"R3-13-40"`). In die gevallen moet je de tekenreeks vooraf verwerken:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Pas vervolgens hetzelfde nummerformaat toe.

## Pro‑tips & valkuilen

- **Pro tip:** Gebruik `StyleFlag` om alleen het nummerformaat te wijzigen, terwijl andere stijl‑attributen onaangeroerd blijven.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Watch out for:** Het overschrijven van bestaande stijlen op een cel die al randen of lettertypen heeft. De `StyleFlag`‑aanpak voorkomt dat.
- **Performance note:** Als je duizenden rijen verwerkt, batch je de `CalculateFormula`‑aanroep nadat je alle updates hebt voltooid; het per rij aanroepen voegt onnodige overhead toe.

## Conclusie

Je weet nu **hoe je een werkmap maakt**, **tekenreeks naar datum converteert**, **cel opmaakt als datum**, **celnummerformaat instelt**, en uiteindelijk **excel‑datum leest** terug in een `DateTime`. Het patroon is eenvoudig: ruwe tekst invoegen, een datumstijl toepassen, herberekening forceren, en vervolgens de waarde lezen.  

Vanaf hier kun je de logica uitbreiden naar volledige kolommen, CSV‑gegevens importeren, of zelfs rapporten genereren die legacy‑datum‑tekenreeksen automatisch omzetten naar juiste Excel‑datums.  

Klaar om een stap hoger te gaan? Probeer een aangepast nummerformaat toe te passen (`Number = 22`) om datums weer te geven als `yyyy-mm-dd`, of verken Aspose.Cells’ `DateTimeConversion`‑hulpmiddelen voor complexere scenario’s.

Veel programmeerplezier! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}