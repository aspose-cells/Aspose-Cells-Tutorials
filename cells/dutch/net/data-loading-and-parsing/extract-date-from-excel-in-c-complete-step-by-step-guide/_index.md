---
category: general
date: 2026-02-09
description: Datum extraheren uit Excel in C# met een eenvoudige werkboeklading en
  cellezing. Leer hoe je een werkboek laadt, een Excel-cel leest en Japanse datums
  snel verwerkt.
draft: false
keywords:
- extract date from excel
- read excel cell
- how to load workbook
- read japanese date
- how to read excel date
language: nl
og_description: Ha datum snel uit Excel in C#. Leer hoe je een werkmap laadt, een
  Excel-cel leest en Japanse datums parseert met duidelijke codevoorbeelden.
og_title: Datum extraheren uit Excel in C# – Complete gids
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Datum extraheren uit Excel in C# – Complete stap‑voor‑stap gids
url: /nl/net/data-loading-and-parsing/extract-date-from-excel-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum uit Excel halen – Volledige programmeer‑walkthrough

Heb je ooit **een datum uit Excel moeten halen** maar wist je niet hoe je cultuur‑specifieke notaties moet behandelen? Je bent niet de enige. Of je nu een fiscale periode uit een Japanse spreadsheet haalt of simpelweg datums normaliseert voor een rapportage‑pipeline, de truc is om de werkmap correct te laden, de juiste cel te lezen en .NET te vertellen welke cultuur gebruikt moet worden.

In deze gids laten we je stap voor stap zien hoe je **een datum uit Excel kunt halen** met C#. We behandelen **hoe je een werkmap laadt**, een **excel‑cel leest**, en zelfs **Japanse datums** uitleest zonder te gokken. Aan het einde heb je een kant‑klaar fragment dat je in elk .NET‑project kunt plaatsen.

---

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+)  
- Een referentie naar **Aspose.Cells** (of een andere compatibele bibliotheek die `Workbook`‑ en `Cell`‑objecten biedt)  
- Een Excel‑bestand (`japan.xlsx`) dat een datum in cel **A1** opslaat met het Japanse kalenderformaat  

Dat is zo’n beetje alles—geen extra services, geen COM‑interop, alleen een paar NuGet‑pakketten en een handvol regels code.

---

## Stap 1: Installeer de Excel‑bibliotheek (Hoe een werkmap te laden)

Allereerst heb je een bibliotheek nodig die `.xlsx`‑bestanden kan lezen. Het voorbeeld gebruikt **Aspose.Cells**, maar dezelfde ideeën gelden voor EPPlus, ClosedXML of NPOI. Installeer via NuGet:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Als je op een CI‑server werkt, pin dan de versie (bijv. `Aspose.Cells --version 23.10`) om onverwachte breaking changes te voorkomen.

---

## Stap 2: Laad de werkmap vanaf schijf

Nu de bibliotheek beschikbaar is, laten we de **werkmap laden**. De `Workbook`‑constructor neemt een bestandspad, dus zorg dat het bestand bereikbaar is vanuit de werkmap van je applicatie.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class ExcelDateExtractor
{
    static void Main()
    {
        // Step 2: Load the workbook from a file
        // Adjust the path to point to your own Excel file
        string filePath = @"C:\Data\japan.xlsx";
        Workbook workbook = new Workbook(filePath);
        
        // Continue to the next step…
```

> **Waarom dit belangrijk is:** Het laden van de werkmap is de toegangspoort tot alles. Als het pad onjuist is, krijg je een `FileNotFoundException` nog voordat je bij de cel komt.

---

## Stap 3: Lees de doelcel (Excel‑cel lezen)

Met de werkmap in het geheugen kunnen we **excel‑cel** A1 **lezen**. De index `Worksheets[0]` pakt het eerste blad; je kunt dit vervangen door een naam indien nodig.

```csharp
        // Step 3: Access cell A1 in the first worksheet
        Cell targetCell = workbook.Worksheets[0].Cells["A1"];
```

> **Veelvoorkomende valkuil:** Sommige ontwikkelaars vergeten dat Excel‑kolommen 1‑gebaseerd zijn, terwijl de `Cells`‑collectie van de bibliotheek 0‑gebaseerd is bij numerieke indexen. Het gebruik van de notatie `["A1"]` omzeilt die verwarring.

---

## Stap 4: Haal de waarde op als een DateTime (Japanse datum lezen)

Excel slaat datums op als seriële getallen, maar de visuele weergave kan per locale verschillen. Door een `CultureInfo`‑object mee te geven, vertellen we Aspose.Cells hoe het getal geïnterpreteerd moet worden. Zo lees je **Japanse datum** correct:

```csharp
        // Step 4: Retrieve the cell value as a DateTime using Japanese culture
        // The "ja-JP" culture knows about the Japanese calendar and date separators
        DateTime japaneseDate = targetCell.GetDateTimeValue(new CultureInfo("ja-JP"));
        
        Console.WriteLine($"Extracted date: {japaneseDate:yyyy-MM-dd}");
    }
}
```

**Verwachte output** (ervan uitgaande dat A1 “2023/04/01” bevat in Japans formaat):

```
Extracted date: 2023-04-01
```

> **Waarom `CultureInfo` gebruiken?** Als je de cultuur overslaat, gaat Aspose uit van de huidige thread‑cultuur (vaak en‑US). Dat kan leiden tot verwisselde maand/dag‑waarden of volledig verkeerde jaren bij Japanse jaartelling.

---

## Stap 5: Bescherm tegen lege of niet‑datumcellen (Excel‑datum veilig lezen)

Werkelijke spreadsheets zijn niet altijd netjes. Laten we een snelle controle toevoegen zodat de code geen uitzondering gooit als A1 leeg is of tekst bevat.

```csharp
        // Optional safety net
        if (targetCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("Cell A1 does not contain a valid date.");
            return;
        }
```

Je kunt ook terugvallen op `DateTime.TryParse` met een specifieke opmaakstring als de cel een tekenreeksrepresentatie bevat in plaats van een echte Excel‑datum.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het **complete, uitvoerbare programma** dat laat zien hoe je **een datum uit Excel haalt**, **excel‑cel leest**, en **Japanse datum** uitleest in één soepele stroom.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class ExcelDateExtractor
{
    static void Main()
    {
        // ---- 1️⃣ Load the workbook -------------------------------------------------
        string filePath = @"C:\Data\japan.xlsx";          // adjust as needed
        Workbook workbook = new Workbook(filePath);

        // ---- 2️⃣ Grab the target cell ------------------------------------------------
        Cell targetCell = workbook.Worksheets[0].Cells["A1"];

        // ---- 3️⃣ Validate the cell content -----------------------------------------
        if (targetCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("Cell A1 does not contain a valid date.");
            return;
        }

        // ---- 4️⃣ Extract the date using Japanese culture ----------------------------
        DateTime extractedDate = targetCell.GetDateTimeValue(new CultureInfo("ja-JP"));

        // ---- 5️⃣ Show the result ----------------------------------------------------
        Console.WriteLine($"Extracted date: {extractedDate:yyyy-MM-dd}");
    }
}
```

**Voer het uit** (`dotnet run`) en je ziet de geformatteerde datum op de console verschijnen. Pas het bestandspad, de werkblad‑index of de celreferentie aan voor jouw eigen werkmap, en hetzelfde patroon blijft werken.

---

## Randgevallen & Variaties

| Situatie                              | Wat moet je aanpassen                                                            |
|---------------------------------------|-----------------------------------------------------------------------------------|
| **Cel bevat een tekenreeks** (bijv. “2023‑04‑01”) | Gebruik `DateTime.TryParseExact(targetCell.StringValue, "yyyy-MM-dd", new CultureInfo("ja-JP"), DateTimeStyles.None, out var dt)` |
| **Meerdere bladen**                   | Vervang `Worksheets[0]` door `Worksheets["SheetName"]` of loop door `workbook.Worksheets` |
| **Andere cultuur** (bijv. Frans)      | Geef `new CultureInfo("fr-FR")` door in plaats van `"ja-JP"`                     |
| **Groot bestand** ( > 10 000 rijen)   | Overweeg `Workbook.LoadOptions` met `MemorySetting` om RAM‑gebruik te beperken    |

---

## Veelgestelde vragen

**V: Werkt dit ook met .xls‑bestanden?**  
A: Ja. Aspose.Cells detecteert het formaat automatisch, dus je kunt `Workbook` op een ouder‑type `.xls` laten wijzen en dezelfde code gebruiken.

**V: Wat als ik de datum in het Japanse jaartal (bijv. Reiwa 5) nodig heb?**  
A: Gebruik `japaneseDate.ToString("gg y年M月d日", new CultureInfo("ja-JP"))` om te formatteren met era‑symbolen.

**V: Kan ik veel datums tegelijk extraheren?**  
A: Zeker. Loop over een bereik—`Cells["A1:A100"]`—en pas dezelfde `GetDateTimeValue`‑logica toe binnen de lus.

---

## Conclusie

Je beschikt nu over een solide **datum‑uit‑Excel**‑recept dat **hoe je een werkmap laadt**, **excel‑cel leest**, en **Japanse datum** uitleest zonder te gokken. De code is zelf‑voorzienend, werkt met de nieuwste .NET‑versie, en bevat veiligheidscontroles voor veelvoorkomende valkuilen.

Volgende stap? Combineer dit fragment met **hoe je een excel‑datum leest** voor een volledige kolom, exporteer de resultaten naar CSV, of voer ze in een database in. Als je nieuwsgierig bent naar andere culturen, verwissel dan de `CultureInfo`‑string en zie de magie gebeuren.

Veel programmeerplezier, en moge elke spreadsheet die je tegenkomt schone, correct geparseerde datums opleveren!  

*Laat gerust een reactie achter als je ergens vastloopt of een cool gebruiksgeval wilt delen.*  

---  

![Extract date from Excel example](image.png "Extract date from Excel"){: alt="extract date from excel"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}