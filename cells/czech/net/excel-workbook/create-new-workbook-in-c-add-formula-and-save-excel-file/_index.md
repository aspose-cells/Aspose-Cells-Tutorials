---
category: general
date: 2026-02-23
description: Vytvořte nový sešit programově v C# a přidejte vzorec do buňky. Naučte
  se používat funkci EXPAND a poté snadno uložte Excel sešit.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: cs
og_description: Vytvořte nový sešit programově v C#. Přidejte vzorec do buňky, naučte
  se používat funkci EXPAND a uložte Excelový sešit během několika sekund.
og_title: Vytvořte nový sešit v C# – přidejte vzorec a uložte soubor Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Vytvořte nový sešit v C# – Přidejte vzorec a uložte soubor Excel
url: /cs/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit nový sešit v C# – Přidat vzorec a uložit Excel soubor

Už jste se někdy zamýšleli, jak **vytvořit nový sešit** objektů z kódu, aniž byste otevírali Excel? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují za běhu vygenerovat tabulku – třeba pro report, export nebo rychlé vypsání dat.  

Dobrá zpráva? V tomto průvodci uvidíte přesně, jak **vytvořit nový sešit**, **přidat vzorec do buňky** a poté **uložit excel sešit** pomocí několika řádků C#. Také se podíváme na **jak použít EXPAND**, abyste mohli generovat dynamické pole bez ručního kopírování. Na konci budete schopni **vytvořit excel soubor programově** a distribuovat jej uživatelům nebo downstream službám.

## Požadavky

- .NET 6.0 nebo novější (jakékoli aktuální .NET runtime)
- Aspose.Cells pro .NET (zkušební verze nebo licencovaná) – tato knihovna poskytuje třídy `Workbook` a `Worksheet`, které používáme níže.
- Základní znalost syntaxe C# – není potřeba hluboká znalost Excelu.

Pokud už máte vše připravené, skvělé! Pokud ne, stáhněte si Aspose.Cells z NuGet (`Install-Package Aspose.Cells`) a můžete začít.

---

## Krok 1: Vytvořit nový sešit – Základ

Nejprve musíme vytvořit novou instanci sešitu. Představte si to jako otevření zcela nového, prázdného Excel souboru.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Proč je to důležité:** Třída `Workbook` je vstupním bodem pro jakoukoli manipulaci s Excelem. Vytvořením nové instance alokujeme paměť pro listy, styly a vzorce – a to vše bez zásahu do souborového systému.

---

## Krok 2: Přístup k prvnímu listu

Každý nový sešit obsahuje výchozí list (nazvaný *Sheet1*). Získáme jej, abychom mohli umístit data a vzorce.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Tip:** Pokud potřebujete více listů, jednoduše zavolejte `workbook.Worksheets.Add("MySheet")` a pracujte s vráceným objektem `Worksheet`.

---

## Krok 3: Přidat vzorec do buňky – Použití funkce EXPAND

A teď ta zábavná část: vložení vzorce. Funkce `EXPAND` je ideální, když chcete ze statického pole vytvořit větší, automaticky vyplněný rozsah.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Jak funguje vzorec EXPAND

| Argument | Význam |
|----------|--------|
| `{1,2,3}` | Zdrojové pole (horizontální seznam tří čísel) |
| `5`       | Požadovaný počet řádků ve výsledku |
| `1`       | Požadovaný počet sloupců (ponechte 1 pro vertikální výsledek) |

Když Excel tento vzorec vyhodnotí, vytvoří **vertikální** seznam:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Proč použít EXPAND?** Odstraňuje potřebu ručního kopírování nebo VBA smyček. Funkce dynamicky přetváří data, což dělá vaše tabulky robustnější a snadněji udržovatelné.

---

## Krok 4: Uložit Excel sešit – Uložit výsledek

Po vložení vzorce je posledním krokem zapsat sešit na disk. Můžete zvolit libovolnou složku, do které máte právo zápisu.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Co uvidíte:** Otevřete `ExpandFormula.xlsx` v Excelu a buňka `A1` zobrazí rozšířené pole. Samotný vzorec zůstane v buňce, takže pokud upravíte zdrojové pole, výstup se automaticky aktualizuje.

---

## Volitelné: Ověřit výstup programově

Pokud raději nechcete otevírat Excel ručně, můžete zpětně načíst hodnoty a ověřit, že odpovídají očekáváním.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Spuštěním výše uvedeného kódu se vypíše:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|--------|---------|
| **Mohu použít EXPAND s větším zdrojovým polem?** | Samozřejmě. Stačí změnit `{1,2,3}` na libovolnou konstantu nebo oblast buněk, např. `EXPAND(A1:C1,10,1)`. |
| **Co když potřebuji horizontální výsledek?** | Prohoďte argumenty řádek/sloupec: `EXPAND({1,2,3},1,5)` vytvoří 1‑řádkový, 5‑sloupcový výsledek. |
| **Bude to fungovat ve starších verzích Excelu?** | `EXPAND` je k dispozici od Excel 365/2021. Ve starších verzích byste museli simulovat pole pomocí `INDEX`/`SEQUENCE`. |
| **Musím volat `workbook.CalculateFormula()`?** | Ne. Aspose.Cells automaticky vyhodnocuje vzorce při uložení, takže hodnoty jsou okamžitě k dispozici. |
| **Jak přidat více listů před uložením?** | Zavolejte `workbook.Worksheets.Add("SecondSheet")` a opakujte kroky manipulace s buňkami na novém listu. |

---

## Úplný funkční příklad

Níže je kompletní, připravený k běhu program. Zkopírujte jej do konzolové aplikace, upravte cestu k výstupu a stiskněte **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Očekávaný výstup v konzoli:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Otevřete vygenerovaný soubor a uvidíte stejná čísla vyplněná ve sloupci **A**.

---

## Vizualizace

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*Obrázek ilustruje čerstvě vytvořený sešit s výsledkem funkce EXPAND.*

---

## Závěr

Nyní víte, jak **vytvořit nový sešit**, **přidat vzorec do buňky** a **uložit excel sešit** pomocí C#. Ovládnutím **jak použít EXPAND** můžete generovat dynamické pole bez ručního úsilí a celý proces vám umožní **vytvořit excel soubor programově** pro jakýkoli automatizační scénář.

Co dál? Zkuste nahradit konstantní pole odkazem na oblast, experimentujte s různými rozměry `EXPAND` nebo propojte více vzorců napříč listy. Stejný vzor funguje i pro grafy, stylování a dokonce kontingenční tabulky – tak pokračujte v objevování.

Pokud narazíte na problémy, zanechte komentář níže. Šťastné programování a užívejte si sílu programového Excelu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}