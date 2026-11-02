---
category: general
date: 2026-10-10
description: Vytvořte sešit Excel v C# a použijte funkci WRAPCOLS k rozdělení dat
  pole do sloupců. Postupujte podle kompletního krok‑za‑krokem průvodce s spustitelným
  kódem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: cs
lastmod: 2026-10-10
og_description: Vytvořte Excel sešit v C# a použijte funkci WRAPCOLS k rozdělení dat
  pole do sloupců. Tento průvodce ukazuje kompletní kód a vysvětluje každý krok.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Vytvořte Excel sešit a rozdělte data pomocí WRAPCOLS v C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak vytvořit sešit Excel a rozdělit data pomocí WRAPCOLS v C#
url: /cs/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit a rozdělit data pomocí WRAPCOLS v C#

Pokud potřebujete **vytvořit Excel sešit** programově, tento průvodce vám přesně ukáže, jak to provést a jak **rozdělit data pole** přes sloupce pomocí funkce `WRAPCOLS`. Získáte kompletní, spustitelný příklad, který vytvoří soubor `.xlsx` s daty rozdělenými do tří sloupců.

Tutoriál pokrývá vše, co potřebujete: požadované NuGet balíčky, každý řádek kódu, proč funguje vzorec `WRAPCOLS`, a jak přizpůsobit řešení pro různé velikosti pole nebo počty sloupců. Na konci budete schopni vložit techniku **use wrapcols function** do libovolného C# projektu, který generuje Excel soubory.

## Požadavky

* .NET 6.0 SDK nebo novější nainstalováno  
* IDE pro C# (Visual Studio, VS Code, Rider, atd.)  
* NuGet balíček **Aspose.Cells for .NET** – knihovna, která poskytuje třídu `Workbook` používanou v příkladech  

Nemusíte mít nainstalovaný Office; Aspose.Cells zapisuje soubor `.xlsx` přímo.

## Krok 1 – vytvořit Excel sešit

Prvním úkolem je vytvořit novou instanci objektu sešitu a získat odkaz na první list. Tento krok je základem pro jakoukoli další manipulaci.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` představuje celý soubor, zatímco `Worksheet` představuje jednotlivý list. Vytvořením sešitu v paměti se vyhnete diskovým I/O, dokud jej výslovně neuložíte.

## Krok 2 – použít WRAPCOLS k rozdělení sloupců pole

Nyní vložíte vzorec do buňky **A1**, který používá `WRAPCOLS`. Funkce přijímá dva argumenty: zdrojové pole a počet sloupců, do kterých má být pole zabaleno.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Proč to funguje:** `WRAPCOLS` vezme ploché pole `{1,2,3,4,5,6}` a vyplní list řádek po řádku, vytvářejíc tři sloupce na řádek. První argument může být jakýkoli Excel literál pole, pojmenovaný rozsah nebo dynamický poleový vzorec. Druhý argument (`3`) říká Excelu, kolik sloupců má vytvořit, než přejde na další řádek.

### Použití funkce s různými typy dat

Funkce `WRAPCOLS` není omezena jen na čísla. Můžete rozdělit textové hodnoty, data nebo smíšené typy:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Když zdrojové pole obsahuje řetězce, Excel automaticky zachází s výsledkem jako s textovými buňkami. Tato flexibilita vám umožní **excel formula split data** pro reportování, dashboardy nebo úlohy migrace dat.

## Krok 3 – vypočítat vzorce, aby byl list naplněn

Vzorce jsou uloženy jako řetězce, dokud nepožádáte sešit o jejich vyhodnocení. Volání `CalculateFormula` vynutí výpočet a zapíše výsledky do buněk.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Bez tohoto volání by uložený soubor obsahoval pouze text vzorce, nikoli vypočtené hodnoty. Metoda funguje napříč celým sešitem, takže můžete umístit další vzorce jinde a všechny budou vyřešeny jedním voláním.

## Krok 4 – uložit sešit a zobrazit výsledek

Nakonec zapište sešit na disk. Vyberte složku, do které máte oprávnění zápisu, a dejte souboru jasný název.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Když otevřete `output.xlsx` v Excelu (nebo v jakémkoli kompatibilním prohlížeči), uvidíte:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Pokud jste použili příklad se smíšenými typy, řádky 3‑4 budou obsahovat text a čísla podle toho.

## Pokročilé varianty a řešení okrajových případů

### Proměnný počet sloupců za běhu

Často počet sloupců, který potřebujete, závisí na vstupu uživatele. Můžete dynamicky sestavit řetězec vzorce:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Velká pole a výkon

`WRAPCOLS` dokáže zpracovat tisíce prvků, ale vyhodnocování extrémně velkých polí v jediné buňce může zvýšit čas výpočtu. Pokud zaznamenáte zpomalení:

* Rozdělte zdrojové pole na menší úseky a zapište každý úsek do samostatné počáteční buňky.  
* Použijte `WorkbookSettings` k povolení vícevláknového výpočtu:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Zpracování prázdných buněk

Pokud zdrojové pole obsahuje prázdné řetězce (`""`) nebo hodnoty `NULL`, `WRAPCOLS` vloží prázdné buňky a zachová rozložení sloupců. Toto chování je užitečné, když potřebujete sloupce jako zástupce pro pozdější zadávání dat.

### Použití pojmenovaných rozsahů místo literálů

Pro udržovatelnost definujte pojmenovaný rozsah, který obsahuje zdrojová data, a poté na něj odkažte:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Nyní vzorec čte data přímo z listu, což umožňuje **how to use wrapcols** v dynamických scénářích reportování.

## Časté úskalí a tipy pro profesionály

* **Nevynechávejte druhý argument.** `WRAPCOLS(array)` bez počtu sloupců vrací jediný sloupec, což zruší smysl rozdělení dat.  
* **Vyhněte se míchání rozměrů pole.** Zdrojové pole musí být jednorozměrné; poskytnutí dvourozměrného pole (např. `{ {1,2},{3,4} }`) vyvolá chybu `#VALUE!`.  
* **Uložte po výpočtu.** Pokud zavoláte `wb.Save` před `CalculateFormula`, soubor bude obsahovat jen text vzorce.  
* **Zkontrolujte oprávnění k souborům.** Při běhu v omezených prostředích (např. ASP.NET) se ujistěte, že identita procesu může zapisovat do cílové složky.  

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat, vložit a spustit. Obsahuje všechny importy, zpracování chyb a komentáře.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Spuštěním programu se vytvoří `output.xlsx` se třemi odlišnými oblastmi, které demonstrují **excel formula split data** pomocí funkce `WRAPCOLS`.

## Závěr

Nyní víte, jak **create Excel workbook** soubory v C# a jak **use wrapcols function** k **split array columns** efektivně. Hlavní kroky—instanciace `Workbook`, vložení vzorce `WRAPCOLS`, výpočet a uložení—tvoří znovupoužitelný vzor pro jakýkoli automatizační úkol, který vyžaduje rozdělení dat do sloupců.

Odtud můžete:

* Kombinovat `WRAPCOLS` s dalšími dynamickými funkcemi pole jako `FILTER` nebo `SORT`.  
* Exportovat velké datové sady z databází a nechat Excel automaticky spravovat rozvržení.  
* Vytvořit uživatelsky řízené reporty, kde je počet sloupců vybírán pomocí UI ovládacího prvku.

Experimentujte s různými zdroji pole, počty sloupců a dalšími vzorci, abyste rozšířili tuto základnu. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak použít WRAPCOLS v C# – Vytvořit Excel sešit s funkcemi Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Vytvořit Excel sešit – Převést pole na matici s WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Vytvořit Excel sešit C# – Průvodce krok za krokem](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}