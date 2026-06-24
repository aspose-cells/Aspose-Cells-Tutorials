---
category: general
date: 2026-06-24
description: Použijte pole vzorců v Excelu pomocí C#. Naučte se, jak uložit soubor
  Excel v C# a vytvořit sešit Excel v C# s funkcí Expand a vygenerovat soubor Excel
  s vzorci.
draft: false
keywords:
- apply array formula excel
- save excel file c#
- create excel workbook c#
- use expand function excel
- generate excel file with formulas
language: cs
og_description: Použijte pole vzorců v Excelu v C# a naučte se rychle uložit soubor
  Excel v C#. Tento průvodce vám ukáže, jak vytvořit sešit Excel v C# a použít funkci
  Expand v Excelu.
og_title: Aplikace pole vzorců v Excelu v C# – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  headline: Apply Array Formula Excel in C# – Complete Guide
  type: TechArticle
- description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  name: Apply Array Formula Excel in C# – Complete Guide
  steps:
  - name: What if the target folder doesn’t exist?
    text: '`Workbook.Save` will throw a `DirectoryNotFoundException`. A quick fix
      is to ensure the directory exists before calling `Save`:'
  - name: Can I apply the array formula to a range other than A1?
    text: 'Absolutely. Just change the cell address:'
  - name: Does the calculation engine respect Excel’s precision settings?
    text: Aspose.Cells follows IEEE‑754 double‑precision arithmetic, which matches
      Excel’s default. If you need custom precision, you can tweak the `CalculationOptions`
      object before calling `CalculateFormula`.
  - name: What about older Excel versions that don’t support `EXPAND`?
    text: 'If you need backward compatibility, replace `EXPAND` with a combination
      of `INDEX` and `SEQUENCE` or simply write the values directly via C# loops.
      The library also lets you write values without formulas:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Použít pole vzorců v Excelu v C# – Kompletní průvodce
url: /cs/net/excel-formulas-and-calculation-options/apply-array-formula-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití pole vzorce v Excelu v C# – Kompletní programovací tutoriál

Už jste někdy potřebovali **apply array formula excel**, ale nebyli jste si jisti, jak to udělat z C# kódu? Nejste v tom sami. Mnoho vývojářů narazí na problém, když se snaží vygenerovat tabulku, která obsahuje dynamické pole vzorců jako `EXPAND` nebo `COT`.  

V tomto tutoriálu projdeme praktickým příkladem, který **creates an excel workbook c#**, vloží pole vzorce, použije funkci `EXPAND` a nakonec **save excel file c#**, abyste jej mohli otevřít v Excelu a vidět výsledky. Na konci také budete vědět, jak **generate excel file with formulas** v produkčně připraveném způsobu.

> **Tip:** Tento přístup funguje s nejnovějšími verzemi Excelu, které podporují dynamické pole funkce (Office 365, Excel 2021+). Pokud potřebujete zpětnou kompatibilitu, budete muset použít starší techniky vzorců.

![Snímek obrazovky Excelu zobrazující výsledek pole vzorce – apply array formula excel](apply-array-formula-excel.png)

*(Image alt text: apply array formula excel – snímek Excel sešitu s dynamickým polem vzorce)*

## Co budete potřebovat

- **.NET 6+** (nebo jakékoli aktuální .NET runtime) – kód se kompiluje jak s .NET Core, tak s .NET Framework.  
- **Aspose.Cells for .NET** (bezplatná zkušební verze nebo licencovaná verze). Tato knihovna vám umožňuje manipulovat se soubory Excel bez nutnosti mít nainstalovaný Excel.  
- Oblíbené IDE (Visual Studio, Rider, VS Code).  
- Základní znalost C# – nic složitého, jen dost na to, abyste mohli sledovat kód.

Pokud je už máte, skvělé – pojďme na to.

---

## Krok 1 – Apply Array Formula Excel: Vytvoření sešitu

Prvním krokem je **create excel workbook c#** pomocí Aspose.Cells. To nám poskytne čistý objekt sešitu, který můžeme později naplnit vzorci.

```csharp
using System;
using Aspose.Cells;

namespace ExcelArrayFormulaDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new workbook
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

> **Proč je to důležité:** Vytvoření objektu `Workbook` je vstupním bodem pro jakoukoli automatizaci Excelu. Reprezentuje celý soubor a první list je vhodné místo pro zahájení testování vzorců.

## Krok 2 – Use Expand Function Excel: Naplnění pole

Nyní **use expand function excel** převádí jednoduché statické pole `{1,2,3}` na vertikální rozlití pěti řádků. Funkce `EXPAND` je součástí dynamického pole motoru Excelu a automaticky vyplní oblast.

```csharp
            // Set a formula that expands an array into 5 rows, 1 column
            // The formula will spill into A1:A5
            worksheet.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

> **Vysvětlení:**  
> - `{1,2,3}` je literální pole konstant.  
> - `5` říká Excelu, aby vrátil pět řádků, zatímco `1` udržuje jediný sloupec.  
> - Když soubor otevřete, buňky A1 až A5 zobrazí `1, 2, 3, 0, 0` (přebytečné řádky jsou doplněny nulami).

## Krok 3 – Přidání klasického matematického vzorce (Cotangent)

Dynamické pole nejsou jedinými vzorci, které můžete vložit. Také **generate excel file with formulas**, který vypočítá kotangens π/4. To ukazuje, že běžné vzorce fungují vedle dynamických.

```csharp
            // Set a formula that calculates the cotangent of π/4 (≈1)
            worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Proč to zahrnout?** Ukazuje, že můžete kombinovat starší a nové funkce bez jakékoli další konfigurace. Funkce `COT` je dostupná ve všech moderních verzích Excelu.

## Krok 4 – Přepočítání všech vzorců v sešitu

Aspose.Cells nevyhodnocuje automaticky vzorce při jejich nastavení. Musíte říct enginu **recalculate** před uložením, jinak soubor bude obsahovat jen surové vzorce.

```csharp
            // Force calculation of all formulas
            workbook.CalculateFormula();
```

> **Co se děje pod kapotou?** Knihovna parsuje každý vzorec, vytváří strom výrazů a vyhodnocuje jej pomocí vlastního výpočetního enginu. Tento krok je zásadní, pokud chcete, aby vygenerovaný soubor ukazoval hodnoty okamžitě po otevření.

## Krok 5 – Uložení Excel souboru C# – Uložení výsledků

Nakonec **save excel file c#** na disk. Můžete zvolit libovolnou složku; jen se ujistěte, že aplikace má práva zápisu.

```csharp
            // Define the output path (adjust as needed)
            string outputPath = @"C:\Temp\output.xlsx";

            // Save the workbook – this writes the calculated values into the file
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Když otevřete `output.xlsx` v Excelu, měli byste vidět:

| A   | B |
|-----|---|
| 1   | 1 |
| 2   |   |
| 3   |   |
| 0   |   |
| 0   |   |

- Sloupec **A** zobrazuje rozlitý pole vytvořené funkcí `EXPAND`.  
- Buňka **B1** zobrazuje `1`, výsledek `COT(π/4)`.

To je kompletní workflow **generate excel file with formulas**.

---

## Časté otázky a okrajové případy

### Co když cílová složka neexistuje?

`Workbook.Save` vyhodí `DirectoryNotFoundException`. Rychlé řešení je zajistit, aby adresář existoval před voláním `Save`:

```csharp
if (!System.IO.Directory.Exists(System.IO.Path.GetDirectoryName(outputPath)))
{
    System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath));
}
```

### Mohu použít pole vzorce na jiný rozsah než A1?

Ano. Stačí změnit adresu buňky:

```csharp
worksheet.Cells["D4"].Formula = "=EXPAND({10,20,30},3,1)";
```

Rozlití začne v D4 a vyplní D4:D6.

### Respektuje výpočetní engine nastavení přesnosti Excelu?

Aspose.Cells používá dvojitou přesnost IEEE‑754, která odpovídá výchozímu nastavení Excelu. Pokud potřebujete vlastní přesnost, můžete upravit objekt `CalculationOptions` před voláním `CalculateFormula`.

```csharp
var options = new CalculationOptions { PrecisionAsDisplayed = true };
workbook.CalculateFormula(options);
```

### Co starší verze Excelu, které nepodporují `EXPAND`?

Pokud potřebujete zpětnou kompatibilitu, nahraďte `EXPAND` kombinací `INDEX` a `SEQUENCE` nebo jednoduše zapište hodnoty přímo pomocí C# smyček. Knihovna vám také umožní zapisovat hodnoty bez vzorců:

```csharp
object[] values = { 1, 2, 3, 0, 0 };
for (int i = 0; i < values.Length; i++)
{
    worksheet.Cells[i, 0].PutValue(values[i]); // Column A
}
```

## Tipy pro práci s vzorci v C#

- **Dávkové výpočty:** Pokud vkládáte stovky vzorců, zavolejte `CalculateFormula` jednou po všech vloženích. Tím snížíte zátěž CPU.  
- **Vyhněte se volatilním funkcím:** Funkce jako `NOW()` se přepočítávají při každém otevření, což může zpomalit velké sešity.  
- **Používejte pojmenované oblasti:** Usnadňují čtení a údržbu vzorců, zejména když je generujete programově.  
- **Udržujte knihovnu aktuální:** Vydání Aspose.Cells často obsahují vylepšení výkonu a podporu nových Excel funkcí (např. `XLOOKUP`, `FILTER`).  

## Shrnutí – Co jsme pokryli

Začali jsme s **apply array formula excel** na novém sešitu, poté **use expand function excel** pro rozlití statického pole přes pět řádků. Dále jsme přidali klasický výpočet `COT`, vynutili úplné přepočítání a nakonec **save excel file c#** na disk. Výsledkem je připravený sešit, který ukazuje jak chování dynamických polí, tak vyhodnocení běžných vzorců – solidní základ pro jakýkoli projekt **generate excel file with formulas**.

## Další kroky

- **Styling výstupu:** Použijte písma, okraje nebo podmíněné formátování pomocí Aspose.Cells, aby list vypadal profesionálně.  
- **Přidání grafů:** Využijte API grafů knihovny k automatické vizualizaci dat pole.  
- **Export do dalších formátů:** Ten samý sešit lze uložit jako CSV, PDF nebo HTML jedním voláním metody (`workbook.Save("output.pdf")`).  
- **Integrace do ASP.NET:** Poskytněte vygenerovaný soubor přímo uživatelům přes webové API.

Neváhejte experimentovat – zaměňte `EXPAND` za `SEQUENCE`, vyzkoušejte rozlití do více sloupců nebo generujte celé dashboardy programově. Možnosti jsou neomezené, když víte, jak **apply array formula excel** z C#.

Šťastné kódování! 🚀

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit a uložit Excel soubor Aspose Cells .NET](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Jak uložit konkrétní stránky Excel souboru jako PDF pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Jak vytvořit a uložit Excel sešit jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}