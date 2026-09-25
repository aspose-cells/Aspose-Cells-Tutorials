---
category: general
date: 2026-05-04
description: Jak vypočítat kotangens při vytváření Excel sešitu v C#. Naučte se používat
  funkci EXPAND, uložit sešit a automatizovat výpočty.
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: cs
og_description: Jak vypočítat kotangens v Excelu pomocí C#. Tento tutoriál ukazuje,
  jak vytvořit sešit Excel, použít funkci EXPAND a soubor uložit.
og_title: Jak vypočítat kotangens v Excelu – Kompletní průvodce C# pracovním sešitem
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak vypočítat kotangens v Excelu pomocí C# – Vytvořit sešit, použít EXPAND
  a uložit
url: /cs/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vypočítat kotangens v Excelu pomocí C# – Kompletní průvodce

Už jste se někdy zamysleli **jak vypočítat kotangens** přímo v souboru Excel vytvořeném pomocí C#? Možná stavíte finanční model, vědeckou zprávu nebo jen automatizujete nudný úkol v tabulce. Dobrá zpráva? Dá se to udělat v několika řádcích kódu—žádné ruční vzorce, žádné kopírování‑vkládání.

V tomto tutoriálu vás provedeme vytvořením Excel sešitu, rozšířením pole pomocí funkce **EXPAND**, vložením vzorce **COT** pro výpočet kotangensu 45° a nakonec uložením souboru, abyste jej mohli otevřít v Excelu a vidět výsledky. Po cestě také pokryjeme **jak použít expand**, **jak uložit workbook** a několik užitečných tipů, které se často přehlížejí.

> **Rychlá odpověď:** Použijte Aspose.Cells (nebo Microsoft Interop) k vytvoření workbooku, nastavte `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`, nastavte `ws.Cells["B1"].Formula = "=COT(PI()/4)"`, a pak zavolejte `workbook.Save("output.xlsx")`.

---

## Co budete potřebovat

- **.NET 6+** (nebo jakýkoli recentní .NET runtime).  
- **Aspose.Cells for .NET** (bezplatná zkušební verze nebo licencovaná verze).  
- Základní pochopení syntaxe C#.  
- Visual Studio, Rider nebo jakýkoli editor, který máte rádi.

Žádné extra doplňky pro Excel nejsou potřeba; vše běží na serveru a výsledný soubor funguje v jakékoli recentní verzi Excelu.

---

## Krok 1: Vytvoření Excel workbooku z C#  

Vytvoření workbooku je základem. Představte si to jako otevření čistého sešitu před tím, než začnete psát.

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**Proč je to důležité:**  
`Workbook` představuje celý balíček `.xlsx`. Ve výchozím nastavení obsahuje jeden list, ke kterému přistupujeme pomocí `Worksheets[0]`. Pokud později potřebujete více listů, můžete je přidat pomocí `workbook.Worksheets.Add()`.

> **Tip:** Pokud cílíte na .NET Core, ujistěte se, že NuGet balíček Aspose.Cells odpovídá vašemu runtime, aby nedošlo k chybějícím nativním závislostem.

---

## Krok 2: Použití funkce EXPAND k vyplnění sloupce  

Funkce **EXPAND** je způsob, jakým Excel převádí statické pole na dynamický rozsah. Je ideální, když chcete vygenerovat sloupec hodnot bez ručního kódování každé buňky.

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### Jak to funguje  

- `{1,2,3}` je zdrojové pole (tři čísla).  
- `5` říká Excelu, aby vytvořil **5 řádků**.  
- `1` říká Excelu, aby vytvořil **1 sloupec**.  

Když otevřete uložený soubor, buňky A1 až A5 budou obsahovat `1, 2, 3, 0, 0` (přebytečné řádky jsou vyplněny nulami).  

**Hraniční případ:** Pokud je argument `rows` menší než délka zdrojového pole, Excel pole ořízne. Takže `=EXPAND({1,2,3},2,1)` zobrazí jen `1` a `2`.

---

## Krok 3: Vložení vzorce COT pro výpočet kotangensu  

Nyní hvězda představení: **jak vypočítat kotangens** v Excelu. Funkce `COT` očekává úhel v radiánech, takže jí předáme `PI()/4` (což odpovídá 45°).

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### Proč použít COT místo TAN?  

Kotangens je reciprokou hodnotou tangensu (`cot = 1 / tan`). I když byste mohli napsat `=1/TAN(PI()/4)`, použití `COT` je čistší a zabraňuje chybám dělení nulou, když je úhel 0° nebo 180°.

**Očekávaný výstup:** Otevřením `output.xlsx` uvidíte v B1 `1`, protože kotangens 45° (π/4 radiánů) je roven 1.

**Co když potřebuji stupně?**  
Trigonometrické funkce v Excelu pracují v radiánech. Převod stupňů provádějte pomocí `RADIANS(deg)`. Například: `=COT(RADIANS(60))`.

---

## Krok 4: Uložení workbooku, abyste mohli vidět výsledky  

Ukládání je poslední část skládanky. Můžete zapisovat do libovolné složky, ke které máte právo zápisu.

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Jak uložit v různých formátech  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

Pokud někdy potřebujete soubor streamovat (např. pro webové API), použijte místo toho `workbook.Save(stream, SaveFormat.Xlsx)`.

---

## Kompletní funkční příklad  

Spojením všeho dohromady získáte samostatný program, který můžete zkopírovat a vložit do konzolové aplikace.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**Ověření výsledku:**  
- Otevřete `output.xlsx`.  
- Sloupec A by měl obsahovat `1, 2, 3, 0, 0`.  
- Buňka B1 by měla zobrazovat `1`.  

Pokud vidíte tyto hodnoty, úspěšně jste se naučili **jak vypočítat kotangens** programově a jak **vytvořit excel workbook**, **použít expand funkci** a **uložit workbook**—vše najednou.

---

## Časté otázky a úskalí  

### Funguje `COT` ve starších verzích Excelu?  

Ano, `COT` existuje od Excelu 2007. Pokud cílíte na Excel 2003 (`.xls`), budete muset nahradit `COT` výrazem `1/TAN(...)`, protože `COT` tam není k dispozici.

### Co když se vzorec automaticky nepřepočítá?  

Aspose.Cells vyhodnocuje vzorce líně. Zavolejte `workbook.CalculateFormula()` před uložením, pokud potřebujete, aby se vypočtené hodnoty zapsaly do souboru.

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### Můžu zapsat výsledek přímo bez vzorce?  

Jistě, můžete vypočítat hodnotu v C# (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) a přiřadit ji `ws.Cells["B1"].Value = result;`. Tutoriál se zaměřuje na Excel vzorce, protože zůstávají dynamické—změna úhlu později se automaticky aktualizuje.

---

## Profesionální tipy pro reálné projekty  

- **Dávkové operace:** Pokud vyplňujete tisíce řádků, během zápisu vypněte výpočet (`workbook.Settings.CalculateFormulaOnOpen = false`), a po dokončení jej znovu zapněte.  
- **Pojmenování oblastí:** Použijte `ws.Cells.CreateRange("MyArray", "A1:A5")` a odkazujte na název ve vzorcích pro přehlednější tabulky.  
- **Zpracování chyb:** Zabalte `workbook.Save` do try/catch, aby se zobrazily problémy s oprávněním (`UnauthorizedAccessException`).

---

## Závěr  

Probrali jsme **jak vypočítat kotangens** v Excel listu generovaném pomocí C#, ukázali **jak použít expand** k naplnění sloupce a předvedli **jak uložit workbook** pro okamžitou kontrolu. Kompletní, spustitelný příklad výše vám poskytuje pevný základ pro automatizaci jakékoli tabulky, která kombinuje statická data s trigonometrickými výpočty.

Další kroky? Zkuste nahradit úhel ve vzorci `COT` odkazem na buňku (`=COT(PI()*A1/180)`), aby uživatelé mohli zadávat stupně. Nebo prozkoumejte další matematické funkce jako `SIN`, `COS` a `ATAN2`—vše funguje stejným způsobem v generovaném workbooku.

Šťastné kódování a ať jsou vaše tabulky bez chyb! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}