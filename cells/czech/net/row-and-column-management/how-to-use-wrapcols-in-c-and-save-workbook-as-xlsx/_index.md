---
category: general
date: 2026-10-26
description: Naučte se, jak v C# použít WRAPCOLS k rozdělení oblasti do sloupců, použít
  WRAPROWS pro řádky a programově uložit sešit jako XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: cs
lastmod: 2026-10-26
og_description: Jak použít WRAPCOLS v C# k rozdělení dat do sloupců, použít WRAPROWS
  pro řádky a uložit sešit jako XLSX. Postupujte podle kompletního průvodce krok za
  krokem.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Jak použít WRAPCOLS v C# – rozdělit rozsahy a uložit jako XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak použít WRAPCOLS v C# a uložit sešit jako XLSX
url: /cs/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít WRAPCOLS v C# a uložit sešit jako XLSX

Pokud potřebujete **jak použít WRAPCOLS** k reorganizaci dat v souboru Excel, tento průvodce vám ukáže kompletní, spustitelné řešení. Uvidíte **excel wrapcols příklad**, naučíte se **rozdělit oblast do řádků** pomocí WRAPROWS a zakončíte **uložením sešitu jako XLSX**—vše provedené **programaticky**.

Práce s Excelem z C# často zahrnuje vytvoření sešitu, aplikaci vzorců a uložení souboru. Kód níže používá knihovnu Aspose.Cells, která vám umožní manipulovat se soubory Excel bez nutnosti instalace Microsoft Office. Na konci tohoto tutoriálu budete schopni **vytvořit excel sešit programaticky**, rozdělit data horizontálně i vertikálně a vytvořit čistý soubor `.xlsx` připravený pro další zpracování.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
* Odkaz na NuGet balíček **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Základní znalost C# a Excel vzorců

## Krok 1: Jak použít WRAPCOLS k rozdělení oblasti do sloupců

Funkce **WRAPCOLS** přijímá jednorozměrnou oblast a rozprostře její hodnoty do zadaného počtu sloupců. V tomto příkladu začínáme s hodnotami v `A1:A10` a požadujeme, aby WRAPCOLS vytvořil tři sloupce.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Výsledek:** Buňky `C1:E4` nyní obsahují původních deset položek uspořádaných ve třech sloupcích (poslední sloupec obsahuje zbývající položky).

![Screenshot ilustrující, jak použít WRAPCOLS k rozdělení oblasti do sloupců v Excelu](image-url.png)

## Krok 2: Rozdělení oblasti do řádků pomocí WRAPROWS

Zatímco **WRAPCOLS** funguje horizontálně, **WRAPROWS** dělá opak: rozprostře oblast přes zadaný počet řádků. Zde vezmeme hodnoty z `B1:B10` a uspořádáme je do dvou řádků počínaje `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Výsledek:** Vzorec vyplní buňky `F1:K2` deseti hodnotami rozdělenými do dvou řádků.

## Krok 3: Uložení sešitu jako XLSX

Po aplikaci vzorců je posledním krokem uložení souboru. Operace **save workbook as xlsx** zapíše sešit v paměti na disk v moderním formátu OpenXML.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Jak vypadá uložený soubor

Když otevřete `wrapcols_wraprows_output.xlsx` v Excelu, uvidíte:

| C | D | E |
|---|---|---|
| Položka 1 | Položka 4 | Položka 7 |
| Položka 2 | Položka 5 | Položka 8 |
| Položka 3 | Položka 6 | Položka 9 |
|        |        | Položka 10 |

a

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Hodnota 1 | Hodnota 3 | Hodnota 5 | Hodnota 7 | Hodnota 9 | |
| Hodnota 2 | Hodnota 4 | Hodnota 6 | Hodnota 8 | Hodnota 10 | |

Vzorce zůstávají v buňkách, takže jakékoli pozdější změny ve zdrojových oblastech se automaticky projeví.

## Krok 4: Běžné varianty a okrajové případy

### Změna počtu sloupců nebo řádků

* **Více sloupců:** Zvyšte druhý argument funkce `WRAPCOLS`.  
  Příklad: `=WRAPCOLS(A1:A10,5)` vytvoří pět sloupců, přičemž prázdné buňky zůstanou tam, kde data dojdou.
* **Dynamický počet sloupců:** Použijte odkaz na buňku místo pevně zadaného čísla.  
  `=WRAPCOLS(A1:A10, G1)`, kde `G1` obsahuje požadovaný počet sloupců.

### Zpracování prázdných nebo ne‑číselných buněk

WRAPCOLS a WRAPROWS ve výchozím nastavení ignorují prázdné buňky, ale zachovávají pořadí ne‑prázdných hodnot. Pokud potřebujete zachovat prázdná místa, obalte zdrojovou oblast funkcemi `IFERROR` nebo `TEXT` před použitím WRAPCOLS.

### Ukládání do jiných formátů

I když se tento tutoriál zaměřuje na **save workbook as xlsx**, Aspose.Cells podporuje mnoho formátů (`.xls`, `.csv`, `.pdf`, atd.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Profesionální tipy a úskalí

* **Pro tip:** Nastavte `Workbook.Settings.CalcEngineEnabled = true`, pokud plánujete okamžitě po uložení vyhodnocovat vzorce.
* **Dejte si pozor na:** Velké zdrojové oblasti mohou vytvořit velmi velké rozléhající se oblasti, což může ovlivnit výkon. Omezte velikost oblasti nebo rozdělte operaci do více listů.
* **Bezpečnost vláken:** Objekt Aspose.Cells **není** bezpečný pro více vláken. Vytvořte samostatnou instanci `Workbook` pro každé vlákno, pokud zpracováváte soubory paralelně.

## Závěr

Nyní víte **jak použít WRAPCOLS** k rozdělení vertikální oblasti do více sloupců, **rozdělit oblast do řádků** pomocí WRAPROWS a **uložit sešit jako XLSX** po provedení těchto transformací. Dodržením výše uvedených kroků můžete **vytvořit excel sešit programaticky**, aplikovat výkonné spill vzorce a generovat připravené ke sdílení soubory Excel bez ručního zásahu.

### Co dál?

* Prozkoumejte **conditional formatting** pro zvýraznění rozléhajících se dat.
* Kombinujte **WRAPCOLS** s **SORT** nebo **FILTER** pro dynamické dashboardy.
* Použijte **charting API** Aspose.Cells k vizualizaci přeuspořádaných dat přímo z kódu.

Šťastné programování a užívejte si automatizaci vašich Excel pracovních postupů!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobným vysvětlením krok za krokem, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [jak použít wrapcols v C# – Kompletní průvodce s Excel WRAPROWS a přepočítáním vzorců](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Jak použít WRAPCOLS v C# – Přetvořit pole na matici v Excelu](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Jak použít WRAPCOLS – Kompletní průvodce pro automatizaci Excelu v C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}