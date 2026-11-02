---
category: general
date: 2026-03-22
description: Jak používat lambda výrazy v C# pro práci s Excelovými vzorci. Naučte
  se zapisovat vzorec do buňky, převádět oblast na pole, zobrazit pole v konzoli a
  vypočítat kotangens v Excelu.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: cs
og_description: Jak použít lambda v C# k manipulaci s Excelovými vzorci, převodu rozsahu
  na pole, zápisu vzorce do buňky, zobrazení pole v konzoli a výpočtu kotangensu v
  Excelu.
og_title: Jak používat lambda v C# s Excelovými vzorci – krok za krokem
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Jak používat lambda v C# s Excelovými vzorci – kompletní průvodce
url: /cs/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat lambda v C# s Excelovými vzorci – Kompletní průvodce

Už jste se někdy zamysleli **jak používat lambda**, když automatizujete Excel z C#? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují zkombinovat sílu nových dynamických polecích funkcí Excelu s možností `LAMBDA` v C#. Dobrá zpráva? Je to ve skutečnosti docela jednoduché, jakmile vidíte, jak se jednotlivé části doplňují.

V tomto tutoriálu projdeme **zápisem vzorce do buňky**, **převodem oblasti na pole**, **zobrazením tohoto pole v konzoli** a dokonce **výpočtem kotangensu v Excelu** — vše při tom, že vám ukážeme **jak používat lambda** uvnitř volání `REDUCE`. Na konci budete mít spustitelný úryvek, který můžete vložit do libovolného .NET projektu, který odkazuje na Aspose.Cells (nebo podobnou knihovnu).

---

## Co se naučíte

- Jak **zapsat vzorec do buňky** pomocí C#.
- Jak **převést oblast na pole** pomocí funkce `EXPAND`.
- Jak **zobrazit pole v konzoli** po výpočtu.
- Jak **vypočítat kotangens v Excelu** pomocí `COT` a `COTH`.
- Přesná syntaxe **jak používat lambda** uvnitř Excel funkce `REDUCE` z C#.

> **Předpoklad:** Potřebujete aktuální verzi .NET (Core 6+ nebo .NET Framework 4.7+) a knihovnu Aspose.Cells pro .NET nainstalovanou přes NuGet.

---

## Krok 1: Nastavení sešitu a zápis vzorce do buňky

Prvním krokem je vytvořit nový sešit a získat první list. Pak **zapíšeme vzorec do buňky** — v tomto případě `A1` bude obsahovat výsledek volání `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Proč je to důležité:** Zapsání vzorce přímo z kódu vám umožní generovat složité tabulky za běhu, aniž byste museli otevírat Excel. Navíc to připraví půdu pro další krok, kde **převádíme oblast na pole**.

---

## Krok 2: Převod oblasti na pole pomocí EXPAND

`EXPAND` je Excelův způsob, jak z malé oblasti vytvořit větší matici. Umístěním vzorce do `A1` Excel rozšíří blok 4 × 5 začínající v této buňce. Z C# nemusíme ručně kopírovat hodnoty — knihovna udělá těžkou práci, když zavoláme `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Jak používat lambda:** Zatím ne, ale zůstaňte s námi. Nejprve potřebujeme data v listu, poté je zredukujeme pomocí lambda výrazu.

---

## Krok 3: Použití LAMBDA uvnitř REDUCE – Jádro „Jak používat lambda“

Excel 365 zavedl `REDUCE`, který přijímá **počáteční hodnotu**, **oblast** a **LAMBDA**, která určuje, jak kombinovat každý prvek. Z C# jen přiřadíme řetězec vzorce; lambda žije uvnitř Excel vzorce, ne v C# kódu.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Vysvětlení:**  
- `0` je počáteční akumulátor (`acc`).  
- `A1:D4` je oblast, kterou chceme zpracovat (první čtyři sloupce rozšířeného bloku).  
- `LAMBDA(acc, x, acc + x)` říká Excelu, aby k akumulátoru přičetl každou buňku (`x`).  

To je podstata **jak používat lambda** pro agregaci v kontextu tabulky.

---

## Krok 4: Výpočet kotangensu v Excelu – Ze stupňů na hyperbolický

Pokud potřebujete trigonometrické výsledky, funkce Excelu `COT` a `COTH` jsou velmi jednoduché. Umístíme je do `G1` a `G2`.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Proč je to užitečné:** Znalost **výpočtu kotangensu v Excelu** vám může ušetřit psaní vlastního matematického kódu, zejména když bude sešit sdílen s ne‑vývojáři.

---

## Krok 5: Vynucení výpočtu a získání rozšířeného pole

Nyní řekneme sešitu, aby vyhodnotil všechny vzorce, a pak vytáhneme rozšířené pole z `A1`. Zde **zobrazíme pole v konzoli**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Co uvidíte:**  
- Hezky formátovanou matici 4 × 5 vytištěnou řádek po řádku.  
- Součet vypočtený `REDUCE` lambda výrazem.  
- Dvě hodnoty kotangensu.

Tím je dokončen celý tok od **zápisu vzorce do buňky** až po **zobrazení pole v konzoli**.

---

## Kompletní funkční příklad (připravený ke kopírování)

Níže je celý program, který můžete vložit do konzolové aplikace. Nezapomeňte nejprve přidat NuGet balíček `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Očekávaný výstup v konzoli (hodnoty se mohou lišit podle výchozího obsahu B1:C2, které jsou ve výchozím nastavení 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Klidně naplňte `B1:C2` vlastními čísly před spuštěním — matice bude odrážet tyto hodnoty.

---

## Pro tipy a časté úskalí

- **Pro tip:** Pokud chcete, aby se rozšířená oblast začínala jinde, stačí změnit cílovou buňku (`A1`). Funkce `EXPAND` respektuje kotvu.
- **Dejte si pozor na:** Prázdné buňky ve zdrojové oblasti se v rozšířeném poli stanou `0`, což může ovlivnit součet v `REDUCE`.
- **Hraniční případ:** Když sešit obsahuje vzorce závislé na volatilních funkcích (např. `NOW()`), zavolejte `workbook.Calculate()` po nastavení všech vzorců, aby byl výsledek aktuální.
- **Poznámka o výkonu:** Pro velké rozšíření zvažte omezení velikosti v volání `EXPAND`; jinak můžete alokovat více paměti, než je potřeba.
- **Kompatibilita:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}