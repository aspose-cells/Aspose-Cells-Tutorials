---
category: general
date: 2026-10-04
description: Leer hoe je een Excel-werkboek maakt in C# en EXPAND gebruikt, de formuleberekening
  forceert, en het werkboek opslaat als XLSX terwijl je een kolom met getallen vult.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: nl
lastmod: 2026-10-04
og_description: Maak een Excel-werkmap in C# met Aspose.Cells. Deze tutorial laat
  zien hoe je EXPAND gebruikt, de formuleberekening forceert en de werkmap opslaat
  als XLSX terwijl je een kolom vult met getallen.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Excel-werkboek maken in C# – volledige gids met EXPAND en XLSX opslaan
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Hoe maak je een Excel-werkmap in C# met de EXPAND-functie
url: /nl/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel-werkmap te maken in C# met de EXPAND‑functie

Als je **een Excel‑werkmap** programmatically wilt **maken**, laat deze gids je een complete, kant‑klaar oplossing zien. Je ziet hoe je een **kolom met cijfers vult**, de **EXPAND**‑functie toepast om gegevens horizontaal te laten uitvloeien, **formule‑berekening forceert**, en uiteindelijk de **werkmap opslaat als XLSX**.  

Deze tutorial behandelt elke stap die je nodig hebt, van het initialiseren van de werkmap tot het verifiëren van het resultaat. Geen externe documentatie nodig – kopieer de code, voer hem uit, en je hebt een volledig functioneel Excel‑bestand.

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+)
- Aspose.Cells for .NET NuGet‑pakket (`Install-Package Aspose.Cells`)
- Basiskennis van C#‑syntaxis
- Een IDE zoals Visual Studio of VS Code

## Stap 1: Excel‑werkmap maken en toegang krijgen tot het eerste werkblad

De eerste handeling is het **maken van een Excel‑werkmap** en een referentie verkrijgen naar het standaardwerkblad. Aspose.Cells voegt automatisch een werkblad toe op index 0, zodat je er meteen mee kunt werken.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Waarom dit belangrijk is:* Het instantieren van `Workbook` reserveert de interne bestandsstructuur, en het ophalen van `Worksheets[0]` geeft je een concreet `Worksheet`‑object om rijen, kolommen en cellen te manipuleren.

## Stap 2: Kolom met cijfers vullen

Vervolgens vul je een verticale lijst in kolom A. Dit demonstreert **kolom met cijfers vullen** en levert de bronbereik voor de EXPAND‑functie.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Pro‑tip:* Gebruik `PutValue` voor ruwe cijfers, strings, datums of elke .NET‑primitive. De methode bepaalt automatisch het celtype.

## Stap 3: Hoe EXPAND te gebruiken – de lijst horizontaal laten uitvloeien

Het **hoe EXPAND te gebruiken**‑deel is de kern van deze tutorial. De `EXPAND`‑functie breidt een bronbereik uit naar een nieuwe vorm. Hier breiden we het verticale bereik `A1:A3` uit naar één rij die drie kolommen beslaat, beginnend bij `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Uitleg:*  
- Het eerste argument (`A1:A3`) is het bronbereik.  
- Het tweede argument (`1`) dwingt het resultaat **1** rij te hebben.  
- Het derde argument (`3`) dwingt het resultaat **3** kolommen te hebben.  

Wanneer de werkmap opnieuw berekent, bevatten de cellen `B1`, `C1` en `D1` respectievelijk `1`, `2` en `3`.

## Stap 4: Formule‑berekening forceren

Aspose.Cells evalueert formules niet automatisch nadat je ze hebt ingesteld, dus je moet **formule‑berekening forceren** vóór het opslaan. Dit zorgt ervoor dat het EXPAND‑resultaat in het bestand wordt vastgelegd.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Waarom je het nodig hebt:* Zonder een aanroep van `CalculateFormula` zou het opgeslagen bestand de ruwe formule‑tekst bevatten, en Excel zou pas bij het openen opnieuw berekenen. Voor geautomatiseerde pipelines wil je meestal dat de waarden direct worden weggeschreven.

## Stap 5: Werkmap opslaan als XLSX

Nu de werkmap volledig is voorbereid, **sla de werkmap op als XLSX** op een locatie naar keuze. De bestandsextensie bepaalt het uitvoerformaat; `.xlsx` maakt een Office Open XML‑werkmap.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Tip:* Als je een ander formaat nodig hebt (CSV, PDF, enz.), wijzig dan simpelweg de bestandsextensie of gebruik `workbook.Save(outputPath, SaveFormat.Xls)` voor oudere Excel‑versies.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samenvoegen levert een zelfstandige applicatie die **een Excel‑werkmap maakt**, een kolom vult, **EXPAND** gebruikt, berekening forceert, en **de werkmap opslaat als XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Verwachte output

Na het uitvoeren van het programma, open `ExpandFunction.xlsx` in Excel. Je zou moeten zien:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

De waarden `1`, `2`, `3` in de cellen `B1:D1` bevestigen dat de **EXPAND**‑functie heeft gewerkt en dat de stap **formule‑berekening forceren** de resultaten succesvol heeft vastgelegd.

## Veelvoorkomende variaties en randgevallen

| Scenario | Aanpassing |
|----------|------------|
| **Dynamisch bronbereik** | Gebruik `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` om zoveel rijen uit te breiden als er zijn ingevuld. |
| **Andere uitvoerafmetingen** | Wijzig het tweede en derde argument van `EXPAND` om rijen en kolommen te regelen. |
| **Meerdere werkbladen** | Loop door `workbook.Worksheets` en pas dezelfde logica toe op elk blad. |
| **Grote datasets** | Roep `workbook.CalculateFormula()` één keer aan nadat alle formules zijn ingesteld om herhaalde herberekeningen te vermijden. |
| **Opslaan naar geheugen‑stream** | Vervang `workbook.Save(path)` door `workbook.Save(stream, SaveFormat.Xlsx)` wanneer je het bestand in een web‑API‑respons nodig hebt. |

## Checklist voor probleemoplossing

- **Formule wordt niet uitgebreid:** Controleer of `CalculateFormula()` *na* het instellen van de formule wordt aangeroepen.  
- **Bestand niet gevonden bij opslaan:** Zorg dat de doelmap bestaat en dat het proces schrijfrechten heeft.  
- **Onjuist gegevenstype:** Gebruik `PutValue` voor cijfers; voor datums, gebruik `PutValue(DateTime.Now)` of `PutDateTime`.  
- **Versiemismatch:** De EXPAND‑functie vereist een Excel 365‑compatibele berekeningsengine; Aspose.Cells 23.9+ ondersteunt dit.

## Conclusie

Je weet nu hoe je **een Excel‑werkmap maakt** in C#, **een kolom met cijfers vult**, de **EXPAND**‑functie toepast, **formule‑berekening forceert**, en **de werkmap opslaat als XLSX**. Dit end‑to‑end‑voorbeeld kan worden aangepast voor rapportage, datatransformatie, of elke automatiseringsscenario dat dynamische Excel‑output vereist.

### Volgende stappen

- Verken andere dynamische array‑functies zoals `FILTER`, `SORT` en `UNIQUE`.  
- Integreer de werkmapgeneratie in een ASP.NET Core API om Excel‑bestanden on‑demand te leveren.  
- Vervang de hard‑gecodeerde cijfers door gegevens uit een database of CSV‑bestand voor real‑world rapportage.

Voel je vrij om te experimenteren met verschillende bereiken, bladnamen en uitvoerformaten. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe cotangens te berekenen in Excel met C# – Werkmap maken, EXPAND gebruiken](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Hoe WRAPCOLS te gebruiken in C# – Excel‑werkmap maken met wrap‑functies](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Hoe een Excel‑werkmap maken en opslaan als ODS met Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}