---
category: general
date: 2026-02-21
description: Rychle vytvořte styl buňky v C#. Naučte se, jak aplikovat styl na buňku,
  vycentrovat text v buňce, nastavit zarovnání buňky a ovládnout formátování buňky.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: cs
og_description: Vytvořte styl buňky v C# a naučte se, jak aplikovat styl na buňku,
  centrovat text v buňce a nastavit zarovnání buňky pomocí přehledného, krok‑za‑krokem
  průvodce.
og_title: Vytvořit styl buňky v C# – Použít styl na buňku a zarovnat text na střed
tags:
- C#
- Aspose.Cells
- Excel automation
title: Vytvořit styl buňky v C# – Jak použít styl na buňku a zarovnat text na střed
url: /cs/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření stylu buňky v C# – Kompletní průvodce aplikací stylů a centrováním textu

Už jste někdy potřebovali **vytvořit styl buňky** v listu Excel, ale nevedeli ste, kde začít? Nejste sami. V mnoha automatizačních projektech je schopnost **aplikovat styl na buňku** rozdílem mezi nudnou tabulkou a profesionální zprávou.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže **jak centrovat text** uvnitř buňky, nastavit zarovnání a přidat tenkou ohraničení – vše během několika řádků C#. Na konci přesně pochopíte, proč je každá část důležitá a jak ji upravit pro vlastní scénáře.

## Co si z toho odnesete

- Jasné pochopení workflow **create cell style** pomocí Aspose.Cells (nebo jakékoli podobné knihovny).
- Přesný kód, který můžete zkopírovat a vložit do konzolové aplikace pro **apply style to cell**.
- Přehled o **center text in cell**, **set cell alignment** a řešení okrajových případů, jako jsou sloučené buňky nebo vlastní číselné formáty.
- Tipy, jak rozšířit styl – jiné fonty, barvy pozadí nebo podmíněné formátování.

> **Předpoklad:** Visual Studio 2022 (nebo jakékoli C# IDE) a NuGet balíček Aspose.Cells pro .NET. Žádné další závislosti nejsou potřeba.

---

## Krok 1: Nastavte projekt a importujte jmenné prostory

Než budeme moci **create cell style**, potřebujeme projekt, který odkazuje na knihovnu Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Proč je to důležité:* Importování `Aspose.Cells` nám poskytuje přístup ke třídám `Workbook`, `Worksheet`, `Style` a `Border`. Pokud používáte jinou knihovnu (např. EPPlus), názvy tříd se změní, ale koncept zůstane stejný.

---

## Krok 2: Vytvořte sešit a získejte první buňku

Nyní **create cell style** provedeme tak, že nejprve získáme odkaz na buňku, kterou chceme formátovat.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Všimněte si, že používáme `Cell` místo obecného `var` – explicitní typování činí kód přehlednějším pro nováčky. Volání `PutValue` zapíše řetězec, abychom později viděli efekt stylu.

---

## Krok 3: Definujte styl – centrovat text, přidat tenkou ohraničení

Zde je jádro operace **create cell style**. Nastavíme vodorovné zarovnání, tenkou ohraničení a několik volitelných vylepšení.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Proč to děláme:*  
- **HorizontalAlignment** a **VerticalAlignment** společně odpovídají na otázku “**how to center text** in a cell?”.  
- Přidání všech čtyř ohraničení zajistí, že buňka vypadá jako ohraničený štítek, což je užitečné pro záhlaví.  
- Barva pozadí není povinná, ale ukazuje, jak můžete styl později rozšířit.

---

## Krok 4: Aplikujte definovaný styl na vybranou buňku

Jakmile styl existuje, **apply style to cell** jedním voláním metody.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

A to je vše – Aspose.Cells se postará o zkopírování stylu do interní kolekce stylů buňky. Pokud potřebujete stejné formátování na rozsah, můžete použít `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Krok 5: Uložte sešit a ověřte výsledek

Rychlé uložení vám umožní otevřít soubor v Excelu a potvrdit, že text je skutečně centrovaný a ohraničení se zobrazuje.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Očekávaný výstup:* Po otevření **StyledCell.xlsx** obsahuje buňka **A1** text „Hello, styled world!“ centrovaný vodorovně i svisle, obklopený tenkou šedou ohraničením a na světle šedém pozadí.

---

## Běžné varianty a okrajové případy

### 1. Centrovat text ve sloučeném regionu

Pokud sloučíte buňky **A1:C1** a stále chcete text centrovaný, musíte styl aplikovat na buňku v levém horním rohu **po** sloučení:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Použití číselného formátu

Někdy potřebujete **set cell alignment** *a* zobrazit čísla ve specifickém formátu:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Zarovnání zůstane centrované, zatímco číslo se zobrazí jako `12,345.68`.

### 3. Efektivní opětovné použití stylů

Vytváření nového `Style` pro každou buňku může snížit výkon. Místo toho vytvořte jeden objekt stylu a znovu jej použijte napříč mnoha buňkami nebo rozsahy. Třída `StyleFlag` vám umožní aplikovat jen ty části, na které vám záleží, a ušetřit paměť.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Profesionální tipy a úskalí

- **Nezapomeňte na svislé zarovnání** – centrování jen vodorovně často vypadá nepřirozeně, zejména u vyšších řádků.  
- **Typy ohraničení**: `CellBorderType.Thin` funguje pro většinu reportů, ale můžete přepnout na `Medium` nebo `Dashed` pro vizuální hierarchii.  
- **Zpracování barev**: Při cílení na .NET Core použijte `System.Drawing.Color` z balíčku `System.Drawing.Common`; jinak narazíte na runtime chybu.  
- **Formát ukládání**: Pokud potřebujete kompatibilitu se staršími verzemi Excelu, změňte `SaveFormat.Xlsx` na `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt text: screenshot showing a cell with centered text and thin border created by the create cell style tutorial.*

---

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Spusťte tento program, otevřete **StyledCell.xlsx** a uvidíte přesně výsledek popsaný výše. Klidně změňte text, styl ohraničení nebo barvu pozadí, aby odpovídaly vaší firemní identitě.

---

## Závěr

Právě jsme **vytvořili styl buňky** od nuly, **aplikovali styl na buňku** a ukázali **jak centrovat text** vodorovně i svisle. Ovládnutím těchto stavebních bloků můžete nyní formátovat záhlaví, zvýrazňovat součty nebo vytvářet celé šablony reportů, aniž byste opustili C#.  

Pokud vás zajímají další kroky, zkuste:

- **Aplikovat stejný styl na celý řádek** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).  
- **Přidat podmíněné formátování**, které změní pozadí podle hodnot buňky.  
- **Exportovat do PDF** při zachování stylu.

Pamatujte, že stylování je stejně o čitelnosti jako o estetice. Experimentujte, iterujte a brzy budou vaše tabulky vypadat tak profesionálně jako váš kód.

*Šťastné programování!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}