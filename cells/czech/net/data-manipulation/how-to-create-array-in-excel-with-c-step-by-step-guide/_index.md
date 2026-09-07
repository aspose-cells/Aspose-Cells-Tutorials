---
category: general
date: 2026-02-09
description: Jak vytvořit pole v Excelu pomocí C# během několika minut – naučte se
  generovat sekvenční čísla, použít COT a uložit sešit jako XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: cs
og_description: Jak vytvořit pole v Excelu pomocí C# je podrobně popsáno krok za krokem,
  včetně generování sekvenčních čísel, použití COT a uložení sešitu jako XLSX.
og_title: Jak vytvořit pole v Excelu pomocí C# – rychlý průvodce
tags:
- C#
- Excel
- Aspose.Cells
title: Jak vytvořit pole v Excelu pomocí C# – krok za krokem
url: /cs/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit pole v Excelu pomocí C# – krok za krokem průvodce

Už jste se někdy zamýšleli **jak vytvořit pole** v Excelu pomocí C# bez trávení hodin prohlížením dokumentace? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují dynamický spill range, rychlou trigonometrickou hodnotu nebo prostě čistý soubor XLSX uložený na disk. V tomto tutoriálu tento problém vyřešíme hned—vytvořením malého sešitu, který zapíše rozšiřující se pole vzorce, vloží výpočet kotangentu a vše uloží jako soubor XLSX.  

Do toho přidáme ještě pár triků: generování čísel sekvence, ovládnutí funkce `COT` a zajištění, aby soubor skončil tam, kde chcete. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu. Žádné zbytečnosti, jen fungující kód.

> **Pro tip:** Příklad používá populární knihovnu **Aspose.Cells**, ale koncepty lze přenést i na jiné balíčky pro automatizaci Excelu (EPPlus, ClosedXML) s jen drobnými úpravami.

---

## Co budete potřebovat

- **.NET 6** nebo novější (kód se také kompiluje na .NET Framework 4.7+)  
- **Aspose.Cells pro .NET** – můžete ji získat z NuGet (`Install-Package Aspose.Cells`)  
- Textový editor nebo IDE (Visual Studio, Rider, VS Code…)  
- Oprávnění k zápisu do složky, kam bude výstupní soubor uložen  

To je vše—žádná další konfigurace, žádný COM interop, jen čistý spravovaný assembly.

## Krok 1: Jak vytvořit pole v Excelu – inicializace sešitu

První věc, když chcete **jak vytvořit pole** v listu Excelu, je vytvořit objekt sešitu. Představte si sešit jako prázdné plátno; list je místo, kde budete malovat své vzorce.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Proč použít `Workbook()` bez parametrů? Poskytuje vám sešit v paměti s výchozím listem, což je ideální pro rychlé programové úlohy. Pokud potřebujete otevřít existující soubor, stačí předat cestu k souboru do konstruktoru.

## Krok 2: Generování čísel sekvence pomocí EXPAND a SEQUENCE

Nyní, když máme list, pojďme vyřešit část hádanky **generování čísel sekvence**. Nové dynamické pole funkce Excelu (`SEQUENCE`, `EXPAND`) nám umožňují vytvořit 3‑řádkový vertikální seznam a automaticky jej rozšířit do rozsahu 3 × 5.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**Co se zde děje?**  
- `SEQUENCE(3,1,1,1)` → vytváří vertikální pole `{1;2;3}`.  
- `EXPAND(...,5,1)` → vezme tento třířádkový sloupec a rozšíří ho na pět sloupců, přičemž doplní prázdné buňky.  

Když otevřete výsledný `output.xlsx`, uvidíte blok 3 × 5 začínající v **A1**, kde první sloupec obsahuje 1, 2, 3 a zbývající čtyři sloupce jsou prázdné. Tato technika je základem **jak vytvořit pole**‑stylu spill rozsahů bez ručního zápisu každé buňky.

## Krok 3: Jak použít COT – přidání trigonometrického vzorce

Pokud vás také zajímá **jak použít cot** uvnitř Excelového vzorce, funkce `COT` je praktický způsob, jak získat kotangens úhlu vyjádřeného v radiánech. Vypočítejme `cot(π/4)`, který by měl vyhodnotit na **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Všimněte si, že jsme použili `PI()` pro získání radiánové hodnoty 180°, pak jsme vydělili 4, abychom dostali 45°. Excel udělá těžkou práci a buňka **B1** zobrazí `1` po otevření sešitu. Toto demonstruje **jak použít cot** pro rychlé inženýrské nebo finanční výpočty bez nutnosti načítat samostatnou matematickou knihovnu.

## Krok 4: Uložení sešitu jako XLSX – uložení souboru

Všechen ten zábavný proces vytváření pole a vkládání vzorců je zbytečný, pokud soubor nikdy neuložíte na disk. Zde je jednoduchý způsob, jak **uložit sešit jako xlsx** pomocí Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Proč specifikovat `SaveFormat.Xlsx`? Zaručuje moderní formát OpenXML, který je univerzálně čitelný (Excel, LibreOffice, Google Sheets). Pokud potřebujete starší soubor `.xls`, stačí vyměnit enum.

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní, připravený k spuštění program. Zkopírujte jej do konzolového projektu, obnovte NuGet balíček Aspose.Cells a stiskněte **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Očekávaný výsledek** po otevření `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Sloupec A zobrazuje čísla 1‑3 vygenerovaná pomocí `SEQUENCE`.  
- Sloupec B obsahuje hodnotu **1** z `COT` vzorce.  
- Sloupce C‑E jsou prázdné, což ilustruje efekt vyplnění funkcí `EXPAND`.

## Často kladené otázky a okrajové případy

### Co když potřebuji více řádků nebo sloupců?

Jednoduše upravte argumenty `SEQUENCE` a `EXPAND`.  
- `SEQUENCE(10,2,5,2)` by vrátil matici 10 řádků × 2 sloupců začínající na 5 a s krokem 2.  
- `EXPAND(...,10,5)` by doplnil výsledek na 10 sloupců a 5 řádků.

### Funguje to s staršími verzemi Excelu?

Dynamické pole funkce (`SEQUENCE`, `EXPAND`) vyžadují Excel 365 nebo 2019+. Pro starší soubory můžete použít klasické vzorce nebo zapisovat hodnoty přímo pomocí `Cells[row, col].PutValue(value)`.

### Mohu psát vzorec ve stylu R1C1?

Určitě. Nahraďte `A1` za `Cells[0, 0]` a použijte vlastnost `FormulaR1C1`:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### Co s kulturou‑specifickými desetinnými oddělovači?

Aspose.Cells respektuje nastavení lokality sešitu. Pokud potřebujete konkrétní kulturu, nastavte `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` před zápisem vzorců.

## Vizualizovaný souhrn

![jak vytvořit pole v Excelu pomocí C#](/images/how-to-create-array-excel-csharp.png "jak vytvořit pole v Excelu pomocí C#")

*Snímek obrazovky ukazuje konečný spill rozsah a výsledek kotangentu.*

## Závěr

Tady to máte—**jak vytvořit pole** v Excelu pomocí C# od začátku, generovat čísla sekvence, využít funkci `COT` a **uložit sešit jako XLSX** v jednom přehledném programu. Hlavní body jsou:

1. Použijte objekty `Workbook` a `Worksheet` pro zahájení automatizace Excelu.  
2. Využijte dynamické pole funkce (`SEQUENCE`, `EXPAND`) pro flexibilní spill rozsahy.  
3. Vložte trigonometrické funkce jako `COT` pro rychlé výpočty bez dalších knihoven.  
4. Uložte výsledek pomocí `SaveFormat.Xlsx`, abyste získali univerzálně čitelný soubor.

Jste připraveni na další krok? Zkuste nahradit `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}