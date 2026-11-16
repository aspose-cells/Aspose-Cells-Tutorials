---
category: general
date: 2026-11-16
description: Naučte se, jak v Excelu rozšířit pole pomocí Aspose.Cells, dynamických
  funkcí pole a lambda reduktoru, a poté zapsat soubor Excel z C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: cs
lastmod: 2026-11-16
og_description: Jak rozšířit pole v Excelu pomocí Aspose.Cells, dynamických funkcí
  pole a lambda reduktoru. Sledujte kompletní příklad v C# pro zápis souboru Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Jak rozšířit pole v Excelu pomocí Aspose.Cells – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak rozšířit pole v Excelu pomocí Aspose.Cells
url: /cs/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak rozšířit pole v Excelu pomocí Aspose.Cells

Pokud potřebujete **how to expand array** v listu Excelu z C#, tento tutoriál ukazuje přesné kroky. Vytvoříte Excel sešit, použijete funkce dynamických polí jako `EXPAND` a `REDUCE`, aplikujete **lambda** akumulátor a nakonec **write Excel file** na disk. Přístup funguje s Aspose.Cells 23.10 nebo novějším a nevyžaduje žádnou ruční instalaci Excelu.

Na konci tohoto průvodce budete mít plně funkční `ExpandReduceDemo.xlsx`, který demonstruje sílu dynamických polí ve vzorcích v programovacím kontextu.

## Co budete potřebovat

- .NET 6.0 (nebo jakákoli verze .NET podporovaná Aspose.Cells)
- Aspose.Cells pro .NET balíček (`dotnet add package Aspose.Cells`)
- Editor kódu nebo IDE (Visual Studio, VS Code, Rider, atd.)

Žádná další COM interop nebo instalace Office není vyžadována, protože Aspose.Cells interně zpracovává formát souboru.

## Krok 1: Vytvořit Excel sešit

Prvním úkolem je **create excel workbook** v paměti. Aspose.Cells poskytuje třídu `Workbook`, která představuje celý soubor XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Why this matters:** Vytvoření instance `Workbook` vám poskytne čisté plátno. Výchozí list je již připraven, takže jej nemusíte přidávat ručně, pokud nechcete více listů.

## Krok 2: Vložit svislou konstantu pole

Engine dynamických polí v Excelu může pracovat s doslovnými konstantami pole. Vložíme svislé pole `{1;2;3;4;5}` do buňky **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tip:** Středník (`;`) odděluje řádky v konstantě, zatímco čárka (`,`) by oddělovala sloupce. To odráží syntaxi Excelu.

## Krok 3: Rozšířit pole do matice

Nyní odpovíme na hlavní otázku – **how to expand array** – pomocí funkce `EXPAND`. Vzorec rozšíří jednosloupcové pole do matice 5 řádků × 2 sloupců, počínaje buňkou **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Why EXPAND?** `EXPAND(source, rows, cols)` vynutí, aby zdrojová oblast zabírala zadanou velikost, případně doplní prázdné buňky. Je to nejčitelnější způsob, jak vytvořit větší matici z jediného pole.

## Krok 4: Redukovat matici pomocí lambda akumulátoru

Funkce `REDUCE` iteruje přes oblast a agreguje hodnoty pomocí **lambda** výrazu. Zde sečteme hodnoty každého sloupce do jediného sloupce a výsledek umístíme do **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **How to use lambda:** `LAMBDA(acc, val, acc+val)` přijímá aktuální akumulátor (`acc`) a další hodnotu buňky (`val`). Vrací nový akumulátor, čímž efektivně provádí průběžný součet. Toto ukazuje **how to use lambda** ve vzorcích Excelu z kódu.

## Krok 5: Vypočítat vzorce, aby se zobrazily výsledky

Aspose.Cells automaticky nevyhodnocuje vzorce při jejich nastavení. Volání `CalculateFormula` vynutí, aby engine vypočítal každý vzorec v sešitu.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Note:** Pokud otevřete vygenerovaný soubor v Excelu, hodnoty již budou viditelné, protože byly předem vypočítány.

## Krok 6: Zapsat Excel soubor na disk

Nakonec **write excel file** pomocí metody `Save`. Vyberte složku, do které máte oprávnění zapisovat.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Očekávaný výsledek

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Column B** a **C** obsahují matici 5 × 2 vytvořenou pomocí `EXPAND`.
- **Cell D1** zobrazuje `15`, součet všech čísel, vypočítaný pomocí `REDUCE` + **lambda** vzorce.

## Časté otázky a okrajové případy

- **Can I expand to more columns than the source provides?**  
  Ano. `EXPAND` doplní chybějící sloupce prázdnými buňkami. Totéž platí pro řádky.

- **What if the source array is horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` bude považovat zdroj za jediný řádek; stále můžete zadat řádky a sloupce pro jeho přetvoření.

- **Does `REDUCE` work with non‑numeric data?**  
  Lambda musí vracet hodnotu kompatibilní s typem akumulátoru. Pro spojování textu můžete použít `LAMBDA(acc, val, acc & val)`.

- **Do I need to call `CalculateFormula` for every change?**  
  Pouze když potřebujete vypočtené hodnoty před uložením. Excel přepočítá při otevření, pokud to vynecháte.

## Profesionální tipy

- **Performance:** Pro velké sešity volejte `workbook.CalculateFormula` jednou po nastavení všech vzorců, místo po každé buňce.
- **Version safety:** `EXPAND` a `REDUCE` jsou k dispozici v Excel 365 a novějším. Aspose.Cells je implementuje bez ohledu na cílovou verzi Excelu, protože výpočetní engine je vestavěný.
- **Debugging formulas:** Použijte `sheet.Cells["B1"].Formula` k načtení přesného řetězce, který jste nastavili; to pomáhá při dynamickém vytváření vzorců.

## Závěr

Nyní víte **how to expand array** v Excelu pomocí Aspose.Cells, využít **dynamic array functions**, aplikovat **lambda** s `REDUCE` a **write excel file** z C#. Tento kompletní příklad lze přizpůsobit složitějším transformacím dat, jako je transpozice matice, kumulativní součty nebo vlastní agregace.

---

*Další kroky:*  
- Prozkoumejte další dynamické funkce jako `FILTER`, `SORT` a `UNIQUE`.  
- Kombinujte více `LAMBDA` výrazů pro vytvoření znovupoužitelných uživatelem definovaných funkcí.  
- Integrujte generování sešitu do ASP.NET Core API pro tvorbu reportů za běhu.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}