---
category: general
date: 2026-02-14
description: Skapa rabattmall snabbt och lär dig hur du tillämpar rabatt i kalkylblad,
  injicerar data i mallen och definierar variabelt prefix för smarta markörer.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: sv
og_description: Skapa rabattmall med C#. Lär dig att tillämpa rabatt i kalkylblad,
  injicera data i mallen och definiera variabelprefix för smarta markörer.
og_title: Skapa rabattmall – Fullständig C#‑genomgång
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Skapa rabattmall i C# – Steg‑för‑steg‑guide
url: /sv/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

as given.

Make sure to keep all shortcodes exactly.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa rabattmall – Fullständig C#‑genomgång

Har du någonsin behövt **create discount template** för en försäljningsrapport men varit osäker på hur du automatiskt matar in siffrorna i ett kalkylblad? Du är inte ensam. I den här handledningen visar vi exakt hur du **create discount template**, sedan **apply discount in spreadsheet** celler, **inject data into template**, och även **define variable prefix** för dina smarta markörer – allt med ren C#‑kod.

Vi börjar med att beskriva problemet, och hoppar sedan rakt in i en fungerande lösning som du kan kopiera‑klistra in. I slutet har du ett återanvändbart mönster som fungerar oavsett om du genererar fakturor, prislistor eller något kalkylblad som behöver dynamiska rabatter.

---

## Vad du kommer att lära dig

- Hur du designar en rabatt‑medveten kalkylblads‑mall.
- Hur du konfigurerar ett anpassat `VariablePrefix` / `VariableSuffix` så att markörerna är lätta att hitta.
- Hur du skickar ett anonymt objekt (`discountData`) till `SmartMarkerProcessor`.
- Hur den resulterande formeln (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) automatiskt beräknar slutpriset.
- Tips för att hantera kantfall som rader utan rabatt eller flera rabattnivåer.

**Förutsättningar** – en aktuell .NET‑runtime (≥ .NET 6), en referens till `Aspose.Cells` (eller liknande) bibliotek som tillhandahåller `SmartMarkerProcessor`, samt en grundläggande förståelse för C#‑syntax. Inget exotiskt.

---

## Steg 1: Skapa en rabattmall i ditt kalkylblad

Först, öppna en ny arbetsbok (eller använd en befintlig) och placera en platshållare där rabatten ska tillämpas. Tänk på mallen som en enkel Excel‑fil med “smart markers” som processorn kommer att ersätta.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Varför detta är viktigt:** Genom att bädda in `#Discount#` i formeln talar vi om för processorn exakt var rabattvärdet ska placeras. `SmartMarkerProcessor` kommer att ersätta `#Discount#` med det tal du anger senare, och lämna resten av formeln orörd.

---

## Steg 2: Definiera variabelprefix för smarta markörer

Direkt ur lådan söker många bibliotek efter `${Variable}` eller `{{Variable}}`. I vårt fall vill vi ha en ren, mänskligt läsbar markör, så vi **define variable prefix** och suffix explicit.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Proffstips:** Att använda `#` håller markörerna korta och lätta att hitta i Excels formelfält. Om du någonsin behöver undvika krockar med befintliga Excel‑funktioner, välj ett annat par (t.ex. `[[` och `]]`).

---

## Steg 3: Injicera data i mallen med SmartMarkerProcessor

Nu matar vi in det faktiska rabattvärdet. Processorn skannar kalkylbladet, hittar varje `#Discount#` och ersätter det med värdet från det anonyma objektet vi skickar.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Efter detta anrop blir formeln i `B2`:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

När arbetsboken beräknas visar `B2` **90**, dvs. en 10 % rabatt på det ursprungliga priset 100.

**Varför det fungerar:** `StartSmartMarkerProcessing` går igenom varje cell, letar efter token `#Discount#` och ersätter den med det numeriska värdet. Eftersom token sitter i ett `IF`‑uttryck hanterar kalkylbladet fortfarande fall där rabatten kan vara noll.

---

## Steg 4: Tillämpa rabatt i kalkylblad – verifiera resultatet

Låt oss trigga beräkningen och skriva ut det slutgiltiga priset till konsolen. Detta steg visar att arbetsflödet **apply discount in spreadsheet** lyckades.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Förväntad output**

```
Original: 100
Discounted (10%): 90
```

Om du ändrar `discountData.Discount` till `0.25` och kör processorn igen, kommer resultatet automatiskt att visa en 25 % rabatt – ingen extra kod behövs.

---

## Steg 5: Hantera kantfall & flera rabatter

### Rader utan rabatt

Ibland är en produkt inte på rea. För att hålla formeln robust täcker `IF`‑satsen du placerade tidigare redan detta scenario: när `#Discount#` är `0` passerar det ursprungliga priset oförändrat.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Flera rabattkolumner

Om du behöver separata rabatter per rad, ge varje rad sin egen markör, t.ex. `#Discount1#`, `#Discount2#`, och skicka en samling:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Processorn matchar markörerna sekventiellt, så varje rad får rätt värde.

---

## Fullt fungerande exempel

Nedan är det kompletta, kopieringsklara programmet som innehåller alla steg ovan. Spara det som `Program.cs`, lägg till en referens till `Aspose.Cells` och kör.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

När du kör detta skrivs de förväntade siffrorna ut och en `DiscountedPricing.xlsx`‑fil skapas som du kan öppna i Excel för att se formeln redan löst.

---

## Slutsats

Du vet nu hur du **create discount template**, **apply discount in spreadsheet**, **inject data into template**, och **define variable prefix** för smarta markörer – allt med ett fåtal koncisa C#‑rader. Mönstret skalar – ändra bara det anonyma objektet eller mata in en samling för massuppdateringar, så hanterar samma mall alla rabatt‑scenarier du kastar på den.

Redo för nästa nivå? Prova:

- Lägga till skatteberäkningar tillsammans med rabatter.
- Hämta rabattprocent från en databas istället för att hårdkoda dem.
- Använda villkorsstyrd formatering för att markera rader med höga rabatter.

Dessa tillägg behåller kärnidén intakt samtidigt som de utökar nytten av din rabattmall.

Har du frågor eller ett coolt användningsfall? Lägg en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}