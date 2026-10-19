---
category: general
date: 2026-06-30
description: Rychle vytvořte čárový sparkline v Excelu pomocí C#. Naučte se, jak přidat
  sparkline, vytvořit Excel sešit v C# a přidat sparkline do buňky během několika
  kroků.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: cs
og_description: Vytvořte čárový sparkline v Excelu pomocí C#. Tento tutoriál ukazuje,
  jak přidat sparkline, vytvořit Excel sešit v C# a vložit sparkline do buňky.
og_title: Vytvořte čárový sparkline v Excelu pomocí C# – krok za krokem.
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvořte čárový sparkline v Excelu s C# – Kompletní programovací průvodce
url: /cs/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření čárového sparkline v Excelu pomocí C# – Kompletní programovací průvodce

Už jste se někdy zamýšleli, jak **vytvořit čárový sparkline** v souboru Excel pomocí C#? Nejste jediní — vývojáři se neustále ptají: „jak přidám sparkline do reportu, aniž bych otevíral Excel ručně?“ Dobrou zprávou je, že s několika řádky kódu můžete vygenerovat elegantní čárový sparkline přímo v sešitu, bez jakéhokoli UI.

V tomto tutoriálu projdeme vše, co potřebujete vědět: od základů **create Excel workbook C#**, přes naplnění dat, až po přesné kroky pro **add line sparkline** a **add sparkline to cell**. Na konci budete mít připravený *.xlsx* soubor, který na první pohled vizualizuje měsíční prodeje. Žádné zbytečnosti, jen praktické, spustitelné řešení.

---

## Co vytvoříte

- Čerstvý Excel sešit pojmenovaný *KPI_Sparklines.xlsx*  
- List nazvaný **KPI** obsahující ukázková čísla prodeje  
- **Čárový sparkline** umístěný v buňce **D2**, který odkazuje na datový rozsah **B2:B13**  
- Základní formátování (barva, tloušťka čáry), aby sparkline vynikl  

Požadavky? Pouze .NET SDK (3.1+ nebo .NET 6) a bezplatná knihovna Aspose.Cells pro .NET (k dispozici přes NuGet). Pokud jste s Aspose.Cells dosud nepracovali, představte si ji jako výkonný Excel engine, který můžete volat z kódu — žádná COM interop, žádná instalace Excelu.

---

![Create line sparkline in Excel using C#](https://example.com/images/create-line-sparkline.png "Create line sparkline in Excel with C#")

*Image alt text: vytvoření čárového sparkline v Excelu pomocí C# ukázkový kód*

---

## Krok 1: **Create Excel workbook C#** – Nastavení souboru a listu

Nejprve potřebujeme objekt sešitu a list, kde budou data. To je základ pro jakoukoli automatizaci Excelu, ať už později **add line sparkline** nebo zapisujete vzorce.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Proč je to důležité:** Třída `Workbook` představuje celý soubor, zatímco `Worksheet` je plátno pro řádky, sloupce a nakonec i náš sparkline. Pojmenování listu hned na začátku udržuje soubor přehledný a samo‑dokumentující.

---

## Krok 2: Naplnění dat – Zdrojový rozsah pro sparkline

Sparkline potřebuje data, která vykreslí. Simulujme 12 měsíců prodejních čísel. Můžete je načíst z databáze, ale pro přehlednost je vygenerujeme za běhu.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Tip:** `PutValue` automaticky rozpozná datový typ, takže není nutné přetypovávat na `double` nebo `int`. Pokud budete chtít buňky formátovat (měna, oddělovač tisíců), můžete později použít objekt `Style`.

---

## Krok 3: **Create line sparkline** – Přidání sparkline do konkrétní buňky

Nyní přichází hvězda show: **čárový sparkline**. Aspose.Cells seskupuje sparkline, takže nejprve vytvoříme `SparklineGroup` typu `Line` a pak určíme, kam se vizuál umístí.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Jak to funguje:**  
> - `firstRow/firstColumn` a `lastRow/lastColumn` definují *cílovou buňku* (kde se sparkline zobrazí).  
> - `firstDataRow/lastDataRow` ukazují na zdrojový rozsah.  
> Protože používáme **čárový sparkline**, vizuál bude jednoduchá tenká čára, která sleduje trend čísel.

### Volitelné: **How to add sparkline** s vlastním stylováním

Chcete‑li, aby sparkline vynikl, upravte pár vlastností:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Proč stylovat?** Tmavě modrá čára na bílém pozadí je příjemná pro oči, zatímco značky (markers) poskytují rychlou představu o jednotlivých bodech — užitečné při prezentacích.

---

## Krok 4: Uložení sešitu – Ověření výsledku

Po přidání sparkline stačí soubor zapsat na disk. Vyberte složku, do které máte právo zápisu; příklad používá zástupnou cestu, kterou byste měli nahradit.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Ověření:** Otevřete vygenerovaný soubor v Excelu (nebo v libovolném prohlížeči podporujícím .xlsx). V buňce **D2** by se měl zobrazit **čárový sparkline**, který odráží rostoucí prodejní čísla ve sloupci **B**. Přechodem myší nad sparkline se zobrazí tooltip s podkladovými hodnotami.

---

## Krok 5: Časté problémy při **add sparkline to cell**

I jednoduchý příklad může nováčky překvapit. Zde je několik věcí, na které si dát pozor:

| Problém | Proč k tomu dochází | Řešení |
|---------|---------------------|--------|
| Špatné souřadnice buňky | Cíl sparkline používá nul‑indexovaný sloupec, ale jednorozměrný řádek je jednorozměrný. | Pamatujte, že `Cells[row, column]` má `row` i `column` nul‑indexované. V `SparklineGroup.Add` jsou řádky a sloupce **1‑based**. |
| Data se nezobrazují | Zdrojový rozsah je prázdný nebo obsahuje ne‑číselné hodnoty. | Ujistěte se, že rozsah (např. `B2:B13`) obsahuje čísla. Použijte `PutValue` s číselnými typy. |
| Sparkline zmizí po uložení | Nesoulad verzí knihovny nebo chybějící licence. | Použijte nejnovější balíček Aspose.Cells a zadejte platnou licenci, pokud překračujete limity evaluace. |
| Styl se neaplikoval | Změny stylu provedené před přidáním sparkline. | Nastavte styl **po** vytvoření skupiny, jak je ukázáno výše. |

---

## Kompletní zdrojový kód – Kopírujte a vložte

Níže je kompletní, připravený program. Vložte jej do nového konzolového projektu, přidejte NuGet balíček Aspose.Cells a stiskněte **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Očekávaný výstup:** Po otevření *KPI_Sparklines.xlsx* sloupec **B** obsahuje dvanáct čísel (5 000 → 13 250) a buňka **D2** zobrazuje hladký tmavě modrý čárový sparkline, který stoupá rovnoměrně. Pokud jste povolili `ShowMarkers`, značky se zobrazí jako malé oranžovo‑červené tečky.

---

## Co dál? Rozšiřování vašich Sparkline dovedností

Po zvládnutí **create line sparkline** s Aspose.Cells můžete zkusit následující témata:

- **Add column sparkline** – ideální pro zobrazení vrstvených dat.  
- **Create multi‑sparkline groups** na stejném listu pro srovnání vedle sebe.  
- **Export to PDF** při zachování sparkline (Aspose.Cells podporuje konverzi do PDF).  
- **Dynamic data sources** – načtěte reálná prodejní čísla z SQL databáze místo pevně zakódovaných hodnot.  

Všechna tato témata staví na stejných základních konceptech: **create Excel workbook C#**, naplnění dat a **add sparkline to cell** ve zvoleném stylu.

---

### TL;DR

Ukázali jsme, jak **vytvořit čárový sparkline** v Excel sešitu pomocí C#. Kroky — *create workbook, fill data, add sparkline, style it, and save* — jsou všechny zahrnuty v jednom, samostatném programu. Klidně upravte barvy, tloušťku čáry nebo zdrojový rozsah podle vašich reportovacích potřeb.

Máte vlastní tip nebo úpravu? Zanechte komentář níže a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, abyste mohli zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve svých projektech.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}