---
category: general
date: 2026-03-01
description: Hoe maak je snel een werkmap in C#—leer een waarde naar een cel te schrijven,
  het getalformaat van een cel in te stellen en een celgetal te formatteren met eenvoudige
  stappen.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: nl
og_description: Hoe maak je een werkmap in C#? Deze gids laat je zien hoe je een waarde
  naar een cel schrijft, het getalformaat van een cel instelt en een celnummer formatteert
  in slechts een paar regels code.
og_title: Hoe een werkmap maken in C# – Waarde schrijven & getal opmaken
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hoe een werkmap maken in C# – Waarde schrijven en getal opmaken
url: /nl/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Workbook maken in C# – Waarde schrijven & Getal opmaken

Hoe een workbook maken in C# is een veelvoorkomende taak wanneer je Excel‑bestanden on‑the‑fly moet genereren. In deze gids lopen we stap voor stap door hoe je een waarde naar een cel schrijft en het getal in de cel opmaakt zodat het uiteindelijke blad er gepolijst uitziet.

Als je ooit naar een lege spreadsheet hebt gekeken en je afvroeg waarom de getallen te veel decimalen tonen, ben je niet de enige. We behandelen alles, van het initialiseren van het workbook‑object tot het instellen van een aangepast getalformaat, en we geven een paar tips voor randgevallen die je later kunt tegenkomen.

## Wat je zult leren

- **Initialize** een nieuw `Workbook`‑object.  
- **Write value to cell** met de `PutValue`‑methode.  
- **Set cell number format** met een `Style`‑object, waardoor je een nette weergave met twee decimalen krijgt.  
- Verifieer het resultaat door de cel terug te lezen of het bestand in Excel te openen.  

Er zijn geen externe bibliotheken nodig buiten de standaard Aspose.Cells (of een vergelijkbare API), en de code draait op .NET 6+ zonder extra configuratie.

---

## Hoe een Workbook maken – Het object initialiseren

Allereerst heb je een workbook‑object nodig om je bladen in op te slaan. Beschouw de `Workbook` als het volledige Excel‑bestand, terwijl elke `Worksheet` een enkel tabblad is.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Waarom dit belangrijk is:* Het aanmaken van het workbook reserveert de interne structuren die later rijen, kolommen en opmaak bevatten. Zonder dit object is er nergens om een waarde naar een cel te schrijven.

> **Pro tip:** Als je met een bestaand bestand wilt werken, vervang `new Workbook()` door `new Workbook("template.xlsx")` om een sjabloon te laden en de stijlen te behouden.

## Waarde naar cel schrijven

Nu we een workbook hebben, laten we een getal in cel **A1** van het eerste werkblad plaatsen.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Waarom we `PutValue` gebruiken*: Deze methode detecteert automatisch het gegevenstype, zodat je niet handmatig hoeft te casten of converteren. Ze respecteert ook de bestaande stijl van de cel, wat handig is wanneer je later **set cell number format** toepast.

### Snelle controle

Als je de cel terugleest, zie je de ruwe waarde:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

Dat is het getal voordat er enige opmaak op is toegepast.

## Getalformaat van cel instellen

Een ruwe double met veel decimalen weergeven is niet altijd gebruiksvriendelijk. Laten we het beperken tot twee significante cijfers.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

De eigenschap `Number` correspondeert met de ingebouwde getalformaat‑ID’s van Excel. `2` betekent “Number with two decimal places”. Als je een ander formaat nodig hebt — bijvoorbeeld valuta of een datum — gebruik je een andere ID of een aangepaste opmaak‑string.

### Alternatief: Aangepaste opmaak‑string

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Waarom een aangepaste stijl kiezen?* Het geeft je volledige controle, vooral wanneer de ingebouwde ID’s niet passen bij je regionale instellingen.

## Output verifiëren (optioneel maar aanbevolen)

Na het toepassen van de stijl kun je het workbook opslaan en in Excel openen om het uiterlijk te bevestigen.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Je zou **123.46** in cel A1 moeten zien — precies twee decimalen, dankzij het ingestelde formaat.

---

### Volledig werkend voorbeeld

Alles bij elkaar, hier is een zelfstandig programma dat je kunt kopiëren‑plakken in een console‑applicatie.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Verwachte output wanneer je het programma uitvoert:**

```
Cell A1 shows: 123.46
```

Open `FormattedWorkbook.xlsx` in Excel en je ziet dezelfde opgemaakte waarde.

---

## Veelvoorkomende variaties & randgevallen

### 1. Verschillende getalformaten

| Doel | Formaat‑ID | Codefragment |
|------|------------|--------------|
| Valuta (twee decimalen) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Percentage (geen decimalen) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Wetenschappelijke notatie | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Als geen van de ingebouwde ID’s past, kun je terugvallen op een aangepaste string zoals eerder getoond.

### 2. Cultuurspecifieke decimale scheidingstekens

Sommige regio’s gebruiken komma’s voor decimalen. Je kunt een cultuur‑bewuste opmaak afdwingen:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Tekst in plaats van getallen schrijven

Wanneer je **how to write cell** met een string moet vullen, geef je gewoon een string door aan `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Er is geen getalformaat nodig, maar je kunt nog steeds lettertype‑stijlen toepassen.

### 4. Grote datasets

Als je duizenden rijen vult, is batch‑invoeging (`Cells.ImportArray`) sneller dan een lus met `PutValue`. De opmaakbenadering blijft hetzelfde; je past de stijl gewoon toe op een bereik:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Veelgestelde vragen

**Q: Werkt dit met .NET Core?**  
A: Absoluut. Aspose.Cells ondersteunt .NET Standard 2.0 en later, dus je kunt targeten op .NET 5, .NET 6 of .NET 7 zonder wijzigingen.

**Q: Wat als ik meer dan twee decimalen nodig heb?**  
A: Verander de `Number`‑eigenschap naar de juiste ingebouwde ID (bijv. `3` voor drie decimalen) of pas de aangepaste opmaak‑string aan (`"#,##0.000"`).

**Q: Kan ik het formaat in één keer op een hele kolom toepassen?**  
A: Ja. Gebruik `Cells["A:A"]` om de volledige kolom te krijgen en vervolgens `SetStyle`.

---

## Conclusie

Je weet nu **hoe je een workbook** maakt in C#, **waarde naar een cel schrijft**, en **het getalformaat van een cel instelt** zodat getallen precies verschijnen zoals jij wilt. Door deze basis onder de knie te krijgen, kun je professionele Excel‑rapporten, facturen of data‑exports genereren met minimale inspanning.

Vervolgens kun je **format cell number** verkennen voor datums, percentages of voorwaardelijke opmaak — elk bouwt voort op dezelfde principes die we hebben behandeld. Duik in de Aspose.Cells‑documentatie voor uitgebreidere stijlopti​es, of probeer meerdere werkbladen te combineren in één workbook voor rijkere rapporten.

Happy coding, and remember: a well‑formatted spreadsheet is just

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}