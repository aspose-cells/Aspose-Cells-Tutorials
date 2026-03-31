---
category: general
date: 2026-03-30
description: Vytvořte Excel sešit v C# pomocí Aspose.Cells. Naučte se použít lambda
  funkci v Excelu, funkci sekvence v Excelu, rozšířit pole v Excelu a uložit sešit
  jako xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: cs
og_description: Rychle vytvořte sešit Excelu v C#. Tento průvodce ukazuje, jak použít
  lambda funkci v Excelu, funkci sekvence v Excelu, rozšířit pole v Excelu a uložit
  sešit jako xlsx.
og_title: Vytvoření Excel sešitu v C# – Průvodce Lambda, SEQUENCE a EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvoření Excel sešitu v C# – Průvodce Lambda, SEQUENCE a EXPAND
url: /cs/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu C# – Lambda, SEQUENCE a EXPAND průvodce

Už jste někdy potřebovali **vytvořit Excel sešit C#** pro automatizovanou zprávu, ale nebyli jste si jisti, které API volání použít? Nejste v tom sami — mnoho vývojářů narazí na stejnou překážku, když poprvé vstoupí do programového generování Excelu. V tomto průvodci uvidíte kompletní, spustitelný příklad, který pokrývá vše od nové **SEQUENCE funkce Excel** po výkonnou **LAMBDA funkci Excel**, a dokonce i to, jak **expandovat pole Excel** výsledky.

Ukážeme vám také přesné kroky k **uložení sešitu jako xlsx**, abyste mohli soubor předat komukoli, kdo používá Excel. Na konci tohoto tutoriálu budete mít solidní, produkčně připravený úryvek kódu, který můžete vložit do libovolného .NET projektu. Žádné vágní odkazy typu „viz dokumentace“ — jen kód, který funguje dnes.

## Co budete potřebovat

- **.NET 6.0 nebo novější** — příklad cílí na .NET 6, ale funguje na jakékoli nedávné verzi.  
- **Aspose.Cells pro .NET** — nainstalujte přes NuGet (`Install-Package Aspose.Cells`).  
- Základní porozumění syntaxi C# (proměnné, objekty a lambda výrazy).  
- IDE, ve kterém se cítíte pohodlně (Visual Studio, Rider nebo VS Code).  

To je vše. Žádné extra COM interop, žádný Office nainstalovaný na serveru — Aspose.Cells vše zvládne v paměti.

## Vytvoření Excel sešitu C# – krok za krokem implementace

Níže rozdělujeme proces na malé kroky. Každý krok má jasný nadpis, krátký úryvek kódu a vysvětlení **proč** to děláme. Klidně zkopírujte celý blok na konci a spusťte jej jako konzolovou aplikaci.

### Krok 1 – Inicializace nového sešitu

Nejprve potřebujeme prázdný objekt sešitu, který představuje Excel soubor v paměti.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Proč je to důležité:* `Workbook` je vstupní bod pro všechny operace Aspose.Cells. Tím, že získáme první `Worksheet`, máme plátno, kam můžeme zapisovat vzorce, hodnoty nebo formátování.  

> **Tip:** Pokud potřebujete více listů, stačí zavolat `workbook.Worksheets.Add()` a uchovat si odkaz na každý z nich.

### Krok 2 – Použití funkce SEQUENCE v Excelu k vygenerování dat

**sequence function excel** vytváří dynamické pole čísel bez jakéhokoli VBA. Umístíme ji do buňky `A1` a necháme Excel automaticky rozšířit výsledek.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Proč je to důležité:* `SEQUENCE(3)` vrací `[1,2,3]`. Zabalíme ji do `EXPAND`, čímž vynutíme výsledek do 5‑řádkového rozsahu, přičemž další řádky budou prázdné. Tím demonstrujeme jak **sequence function excel**, tak **expand array excel** najednou.

### Krok 3 – Agregace čísel pomocí funkce LAMBDA v Excelu

Nyní představíme schopnost **lambda function excel**. Sečteme čísla 1‑5 pomocí nové funkce `REDUCE`, která interně používá lambda výraz.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Proč je to důležité:* `REDUCE` iteruje přes pole vytvořené `SEQUENCE(5)`, předává každý prvek (`b`) do lambda výrazu spolu s akumulátorem (`a`). Lambda `a+b` je sčítá a výsledek `15` zůstane v `B1`. Jedná se o čistý, jen‑vzorcový způsob provádění redukcí bez cyklů v C#.

### Krok 4 – Použití trigonometrických funkcí přímo v buňkách

Vestavěné matematické funkce Excelu jsou užitečné pro rychlé výpočty. Umístíme kotangens a hyperbolický kotangens do sousedních buněk.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Proč je to důležité:* Ukazuje, že můžete kombinovat klasické matematické funkce s novějšími dynamickými poli. Není nutné tyto hodnoty počítat v C#, pokud nemáte konkrétní důvod pro výkon.

### Krok 5 – Vypočítání všech vzorců

Aspose.Cells automaticky nevyhodnocuje vzorce, když je nastavíte. Musíte jej požádat o výpočet.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Proč je to důležité:* Po tomto volání obsahuje vlastnost `Value` každé buňky vyhodnocený výsledek, připravený k uložení nebo zpětnému čtení.

### Krok 6 – Uložení sešitu jako Xlsx

Nakonec uložíme sešit na disk pomocí vzoru **save workbook as xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Proč je to důležité:* Metoda `Save` automaticky rozpozná příponu souboru. Použitím „.xlsx“ zajistíme kompatibilitu souboru s moderními verzemi Excelu. Cesta ukazuje na plochu pro snadný přístup během testování.

### Úplný funkční příklad

Níže je kompletní program, který můžete vložit do nového konzolového projektu. Obsahuje všechny výše uvedené kroky a malý ověřovací blok, který vypíše vypočítané hodnoty do konzole.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Očekávaný výstup v konzoli**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

A když otevřete *NewFunctions.xlsx*, uvidíte stejné čísla uspořádané v prvních čtyřech sloupcích.

![snímek obrazovky vytvoření excel sešitu c# výsledného tabulky](/images/create-excel-workbook-csharp.png)

## Okrajové případy, tipy a časté otázky

- **Co když potřebuji více než jeden list?**  
  Stačí zavolat `workbook.Worksheets.Add()` a opakovat přiřazování vzorců na každém novém objektu `Worksheet`.  

- **Mohu použít starší verze Excelu?**  
  Dynamické pole funkce (`SEQUENCE`, `EXPAND`, `REDUCE`) vyžadují Excel 365 nebo Excel 2021+. Pokud cílíte na starší verze, držte se klasických vzorců nebo vypočítejte hodnoty v C# před jejich zápisem.  

- **Obavy o výkon?**  
  Pro tisíce řádků je nastavení vzorců na rozsah a následné volání `CalculateFormula` obvykle rychlejší než cyklické přiřazování hodnot po jedné.  

- **Ukládání do proudu místo souboru?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}