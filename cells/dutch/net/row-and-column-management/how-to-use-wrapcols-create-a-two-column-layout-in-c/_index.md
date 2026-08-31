---
category: general
date: 2026-02-15
description: Hoe WRAPCOLS te gebruiken om een tweekolomsindeling te maken, een formule
  toe te voegen en een sequentie‑array te genereren in C#‑werkbladen – stapsgewijze
  handleiding.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: nl
og_description: Hoe WRAPCOLS te gebruiken om een twee‑kolomindeling te maken, formules
  toe te voegen en een reeksarray te genereren in een C#‑werkblad – volledige gids.
og_title: 'Hoe WRAPCOLS te gebruiken: tweekolomsindeling in C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Hoe WRAPCOLS te gebruiken: Maak een tweekolomsindeling in C#'
url: /nl/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe WRAPCOLS te gebruiken: Maak een tweekolomsindeling in C#

Heb je je ooit afgevraagd **hoe je WRAPCOLS kunt gebruiken** wanneer je een snelle tweekolomsweergave nodig hebt in een Excel‑achtige werkblad? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze proberen een gegenereerde lijst in nette kolommen te splitsen zonder voor elke cel een lus te schrijven. Het goede nieuws? Met de `WRAPCOLS`‑functie kun je een enkele formule in `A1` plaatsen en Excel (of een compatibele engine) het zware werk laten doen.

In deze tutorial lopen we stap voor stap door **hoe je een formule toevoegt** die een **tweekolomsindeling maakt**, laten we je **hoe je kolommen dynamisch maakt** zien, en zelfs **sequence‑array**‑waarden on‑the‑fly genereert. Aan het einde heb je een volledig uitvoerbare C#‑snippet die je in je project kunt plakken, uitvoeren, en direct een nette tweekolomsblok ziet verschijnen.

## Wat je zult leren

- Het doel van `WRAPCOLS` en waarom het een beter alternatief is voor handmatig loopen.  
- Hoe je **een formule toevoegt** aan een werkbladcel met C#.  
- Hoe je een sequence‑array genereert met `SEQUENCE` en deze in `WRAPCOLS` stopt.  
- Tips voor het opnieuw berekenen van het blad zodat de formule onmiddellijk wordt opgelost.  
- Afhandeling van randgevallen (bijv. lege werkbladen, aangepaste kolomtellingen).

Er zijn geen externe bibliotheken nodig buiten een standaard Excel‑verwerkingspakket – we gebruiken **ClosedXML** voor de eenvoudige API, maar de concepten zijn toepasbaar op EPPlus, SpreadsheetGear, of zelfs Google Sheets via de API.

---

## Vereisten

- .NET 6.0 of later (de code compileert op .NET Core en .NET Framework).  
- Een referentie naar **ClosedXML** (`dotnet add package ClosedXML`).  
- Basiskennis van C# – je moet vertrouwd zijn met `using`‑statements en objectinitialisatie.

Als je al een werkmap open hebt, kun je het gedeelte voor het aanmaken van een bestand overslaan en direct naar het formule‑gedeelte gaan.

---

## Stap 1: Het werkblad instellen (Hoe kolommen te maken)

Eerst hebben we een `Worksheet`‑object nodig om mee te werken. In ClosedXML haal je het op van een `XLWorkbook`. De onderstaande snippet maakt een nieuwe werkmap, voegt een blad toe met de naam *Demo*, en pakt een referentie genaamd `worksheet` voor duidelijkheid.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Waarom hernoemen?**  
> Het kort houden van de variabelenaam (`worksheet`) maakt de latere code makkelijker leesbaar, vooral wanneer je meerdere bewerkingen aaneenschakelt. Het weerspiegelt ook de naamgevingsstijl die je in de meeste documentatie ziet, waardoor de cognitieve belasting vermindert.

---

## Stap 2: De formule schrijven (Hoe een formule toe te voegen + sequence‑array genereren)

Nu komt de magische regel. We plaatsen een formule in cel **A1** die twee dingen doet:

1. **Genereer een sequence‑array** van zes getallen (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Wikkel die getallen in twee kolommen** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Wat gebeurt er?**  
> `SEQUENCE(6)` maakt een verticale array `{1;2;3;4;5;6}`. `WRAPCOLS` neemt die array vervolgens en “wrapt” deze in het opgegeven aantal kolommen – in dit geval **2**. Het resultaat is een blok van 3 rij × 2 kolom dat er als volgt uitziet:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Als je het tweede argument wijzigt naar **3**, krijg je in plaats daarvan een drie‑kolomsindeling. Dat is de kern van **hoe je kolommen on‑the‑fly maakt** zonder handmatige lussen.

---

## Stap 3: Het werkblad opnieuw berekenen (Zorg dat de formule wordt geëvalueerd)

ClosedXML evalueert formules niet automatisch wanneer je ze schrijft. Je moet `Calculate()` aanroepen op de werkmap (of op het specifieke werkblad) om evaluatie af te dwingen.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Pro tip:** Als je met grote werkmappen werkt, roep je `Calculate()` alleen aan op de bladen die daadwerkelijk zijn gewijzigd. Dit bespaart geheugen en versnelt de verwerking.

Wanneer je `WrapColsDemo.xlsx` opent, zie je de tweekolomsindeling netjes ingevuld in **A1:B3**. Er was geen extra code nodig om door rijen of kolommen te loopen – `WRAPCOLS` regelde alles.

---

## Stap 4: De uitvoer verifiëren (Wat te verwachten)

Na het uitvoeren van het programma, open je het gegenereerde bestand. Je zou moeten zien:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Als de getallen verticaal verschijnen (dus allemaal in kolom A), controleer dan of je `worksheet.Calculate()` **na** het instellen van de formule hebt aangeroepen. Sommige engines hebben ook `workbook.Calculate()` nodig; de bovenstaande snippet werkt voor de ingebouwde evaluator van ClosedXML.

---

## Veelvoorkomende variaties & randgevallen

### Het aantal kolommen wijzigen

Om een **tweekolomsindeling** te maken met een ander aantal rijen, pas je eenvoudig de grootte van `SEQUENCE` of het tweede argument van `WRAPCOLS` aan:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Dit produceert een blok van 4 rij × 3 kolom (12 getallen verdeeld over drie kolommen).

### Een dynamisch kolomaantal gebruiken

Als je kolomaantal afkomstig is van een variabele, embed je het met stringinterpolatie:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Nu heb je **een formule toegevoegd** die zich aanpast tijdens runtime.

### Lege werkbladen

Als het werkblad leeg is, werkt `Calculate()` nog steeds – de formule vult de cellen vanaf A1. Als je later echter rijen/kolommen verwijdert die het uitvoerbereik kruisen, kun je `#REF!`‑fouten zien. Om dat te voorkomen, maak je eerst het doelbereik leeg:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Compatibiliteit

`WRAPCOLS` en `SEQUENCE` maken deel uit van Excel’s **Dynamic Array**‑functies, geïntroduceerd in Office 365. Als je oudere Excel‑versies target, bestaan deze functies niet, en heb je een handmatige lus nodig. De evaluator van ClosedXML spiegelt het nieuwste Excel‑gedrag, dus het is veilig voor moderne omgevingen.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Verwacht resultaat:** Het openen van *WrapColsDemo.xlsx* toont een nette tweekolomsindeling met de getallen 1‑6 zoals eerder beschreven.

---

## Conclusie

We hebben behandeld **hoe je WRAPCOLS kunt gebruiken** om **een tweekolomsindeling te maken**, laten zien **hoe je een formule programmatically toevoegt**, en gezien hoe `SEQUENCE` je in staat stelt **sequence‑array**‑waarden te **genereren** zonder een lus. Door Excel’s dynamische array‑functies vanuit C# te benutten, kun je je code beknopt, leesbaar en onderhoudbaar houden.

Vervolgens kun je verkennen:

- **Dynamische rijaantallen maken** met `ROWS` of `COUNTA`.  
- **De uitvoer stylen** (randen, getalformaten) met de styling‑API van ClosedXML.  
- **Exporteren naar CSV** nadat de indeling is opgebouwd, voor downstream verwerking.

Probeer het, pas het kolomaantal aan, en zie hoe snel je complexe spreadsheets kunt prototypen. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}