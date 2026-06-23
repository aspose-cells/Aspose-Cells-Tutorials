---
category: general
date: 2026-02-14
description: Rychle vytvořte šablonu slevy a naučte se, jak aplikovat slevu v tabulce,
  vložit data do šablony a definovat proměnný prefix pro chytré značky.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: cs
og_description: Vytvořte šablonu slevy v C#. Naučte se aplikovat slevu v tabulce,
  vložit data do šablony a definovat proměnný prefix pro chytré značky.
og_title: Vytvořte šablonu slev – kompletní průvodce C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Vytvořte šablonu slev v C# – krok za krokem
url: /cs/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření šablony slev – Kompletní průvodce v C#

Už jste někdy potřebovali **create discount template** pro prodejní zprávu, ale nebyli jste si jisti, jak automaticky vložit čísla do tabulky? Nejste v tom sami. V tomto tutoriálu vám přesně ukážeme, jak **create discount template**, poté **apply discount in spreadsheet** buňky, **inject data into template** a dokonce **define variable prefix** pro vaše smart markery — vše pomocí čistého C# kódu.

Začneme popisem problému a poté přejdeme rovnou k funkčnímu řešení, které můžete zkopírovat a vložit. Na konci budete mít znovupoužitelný vzor, který funguje, ať už generujete faktury, ceníky nebo jakoukoli tabulku, která potřebuje dynamické slevy.

---

## Co se naučíte

- Jak navrhnout šablonu tabulky, která je připravena na slevy.
- Jak nakonfigurovat vlastní `VariablePrefix` / `VariableSuffix`, aby byly značky snadno rozpoznatelné.
- Jak předat anonymní objekt (`discountData`) do `SmartMarkerProcessor`.
- Jak výsledná formule (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) automaticky vypočítá konečnou cenu.
- Tipy pro zpracování okrajových případů, jako jsou řádky se nulovou slevou nebo víceúrovňové slevy.

**Prerequisites** – aktuální .NET runtime (≥ .NET 6), odkaz na knihovnu `Aspose.Cells` (nebo podobnou), která poskytuje `SmartMarkerProcessor`, a základní znalost syntaxe C#. Nic exotického.

---

## Krok 1: Vytvořte šablonu slev ve své tabulce

Nejprve otevřete nový sešit (nebo použijte existující) a umístěte zástupný znak tam, kde bude sleva aplikována. Považujte šablonu za obyčejný Excel soubor s „smart markery“, které procesor nahradí.

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

**Why this matters:** Vložením `#Discount#` do formule říkáme procesoru přesně, kam má hodnota slevy patřit. `SmartMarkerProcessor` nahradí `#Discount#` číslem, které později poskytnete, a zbytek formule zůstane nedotčen.

---

## Krok 2: Definujte předponu proměnné pro Smart Markery

Standardně mnoho knihoven hledá `${Variable}` nebo `{{Variable}}`. V našem případě chceme čistý, čitelný pro člověka marker, takže **define variable prefix** a sufix explicitně.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Použití `#` udržuje markery krátké a snadno viditelné ve formulářovém řádku Excelu. Pokud potřebujete předejít kolizím s existujícími funkcemi Excelu, zvolte jinou dvojici (např. `[[` a `]]`).

---

## Krok 3: Vložte data do šablony pomocí SmartMarkerProcessor

Nyní vložíme skutečnou hodnotu slevy. Procesor prohledá list, najde každý `#Discount#` a nahradí jej hodnotou z anonymního objektu, který předáme.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

After this call, the formula in `B2` becomes:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Když se sešit vypočítá, `B2` ukazuje **90**, tj. 10 % sleva aplikovaná na původní cenu 100.

**Why it works:** `StartSmartMarkerProcessing` prochází každou buňku, hledá token `#Discount#` a nahrazuje jej číselnou hodnotou. Protože je token uvnitř `IF` výrazu, tabulka stále zvládá případy, kdy může být sleva nulová.

---

## Krok 4: Aplikujte slevu v tabulce – Ověřte výsledek

Spustíme výpočet a vypíšeme konečnou cenu do konzole. Tento krok dokazuje, že workflow **apply discount in spreadsheet** byl úspěšný.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

Pokud změníte `discountData.Discount` na `0.25` a znovu spustíte procesor, výstup automaticky zobrazí 25 % slevu — žádný další kód není potřeba.

---

## Krok 5: Zpracování okrajových případů a více slev

### Řádky s nulovou slevou

Někdy produkt není v akci. Aby byla formule robustní, `IF`, který jste umístili dříve, již tento scénář pokrývá: když je `#Discount#` `0`, původní cena projde beze změny.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Více sloupců se slevou

Pokud potřebujete samostatné slevy pro každý řádek, dejte každému řádku vlastní marker, např. `#Discount1#`, `#Discount2#`, a předávejte kolekci:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Procesor přiřadí markery sekvenčně, takže každý řádek dostane správnou hodnotu.

---

## Kompletní funkční příklad

Níže je kompletní, připravený ke kopírování program, který zahrnuje všechny výše uvedené kroky. Uložte jej jako `Program.cs`, přidejte odkaz na `Aspose.Cells` a spusťte.

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

Po spuštění tento program vypíše očekávaná čísla a vytvoří soubor `DiscountedPricing.xlsx`, který můžete otevřít v Excelu a vidět již vyřešenou formuli.

---

## Závěr

Nyní víte, jak **create discount template**, **apply discount in spreadsheet**, **inject data into template** a **define variable prefix** pro smart markery — vše pomocí několika stručných řádků C#. Vzor je škálovatelný — stačí změnit anonymní objekt nebo předat kolekci pro hromadné aktualizace a stejná šablona zvládne jakýkoli scénář slev, který na ni hodíte.

Připraveni na další úroveň? Vyzkoušejte:

- Přidání výpočtu daně vedle slev.
- Načtení procentuální slevy z databáze místo pevného kódu.
- Použití podmíněného formátování pro zvýraznění řádků s vysokými slevami.

Tyto rozšíření zachovávají základní myšlenku a zároveň rozšiřují užitečnost vaší šablony slev.

Máte otázky nebo zajímavý případ použití? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}