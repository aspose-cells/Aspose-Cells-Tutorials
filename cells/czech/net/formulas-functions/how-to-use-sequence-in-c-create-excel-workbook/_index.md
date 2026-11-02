---
category: general
date: 2026-07-03
description: Jak použít SEQUENCE v C# k generování inkrementálních čísel v Excelu.
  Naučte se vytvořit Excel sešit v C# a ASP.NET a vytvořit Excel soubor pomocí několika
  řádků kódu.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: cs
og_description: Jak použít SEQUENCE v C# k generování postupně se zvyšujících čísel
  v Excelu. Krok za krokem průvodce tvorbou Excel sešitu v C# a ASP.NET, vytvoření
  Excel souboru.
og_title: Jak použít SEQUENCE v C# – Vytvořit sešit Excelu
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Jak použít SEQUENCE v C# – Vytvořit Excel sešit
url: /cs/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít SEQUENCE v C# – Vytvořit Excel sešit

Už jste se někdy zamýšleli **jak použít SEQUENCE** k vypsání seznamu čísel v listu Excelu z C#? Nejste v tom sami. Ať už vytváříte dashboard pro reportování, napájíte datovou mřížku, nebo jen potřebujete rychlý způsob, jak generovat ID, zvládnutí tohoto triku vás ušetří od manipulace s cykly.

V tomto tutoriálu **vytvoříme Excel sešit v C#**, vložíme dynamický‑pole `SEQUENCE` do buňky A1 a získáme pěkný sloupec postupně se zvyšujících čísel. Také uvidíme, jak tento soubor naservírovat z ASP.NET kontroleru—ano, **ASP.NET create Excel file** je také pokryto. Na konci budete schopni **generate incremental numbers Excel**‑styl jedním řádkem kódu.

## Co budete potřebovat

- .NET 6+ (kód funguje také na .NET Framework 4.6+)  
- Balíček **Aspose.Cells for .NET** NuGet (nebo jakákoli knihovna, která poskytuje objekty `Workbook`/`Worksheet`)  
- Základní projekt ASP.NET Core nebo MVC, pokud chcete vyzkoušet část stahování přes web  

To je vše. Žádné další COM interop, není potřeba instalace Office.

---

## Jak použít SEQUENCE k vygenerování postupně se zvyšujících čísel

Funkce Excel `SEQUENCE(rows, [columns], [start], [step])` vrací **spill** oblast. V našem případě chceme 5 řádků, 1 sloupec, začátek na 10, krok 2. Vzorec vypadá takto:

```excel
=SEQUENCE(5,1,10,2)
```

Když Excel tento vzorec vyhodnotí, buňky A1:A5 budou obsahovat **10, 12, 14, 16, 18**. Krása je v tom, že nemusíme psát žádné C# smyčky—vzorec udělá těžkou práci.

Níže je kompletní úryvek C# kódu, který vytvoří sešit, vloží vzorec, vynutí výpočet a uloží soubor.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Očekávaný výstup** – otevřete *DynamicArray.xlsx* a uvidíte:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

To je celý příběh **how to use sequence** v C#. Jednoduché, že? Ale pojďme se ponořit trochu hlouběji.

### Proč použít SEQUENCE místo smyčky?

- **Performance** – Excel provádí výpočty ve svém vlastním engine, který je vysoce optimalizovaný.
- **Maintainability** – Vzorec je samodokumentující; kdokoli otevře list okamžitě pozná záměr.
- **Dynamic resizing** – Změníte-li argument `rows`, spill oblast se automaticky rozšíří.

---

## Vytvořit Excel sešit C# – Krok za krokem

Pokud jste noví v **create excel workbook c#**, následující kontrolní seznam vám pomůže vyhnout se běžným úskalím.

1. **Add the Aspose.Cells package**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Můžete také použít ClosedXML nebo EPPlus, ale ukázané API odpovídá výše uvedenému kódu.)

2. **Set a license** (volitelné pro zkušební verzi).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instantiate `Workbook`** – získáte tak čerstvý, prázdný sešit.

4. **Reference the worksheet** – `workbook.Worksheets[0]` je výchozí list pojmenovaný *Sheet1*.

5. **Apply the SEQUENCE formula** – jak bylo ukázáno dříve.

6. **Calculate** – `workbook.CalculateFormula()` vynutí spill; jinak by soubor obsahoval jen vzorec.

7. **Save** – můžete zapisovat na disk, do `MemoryStream`, nebo přímo do HTTP odpovědi.

### Pro tip

Pokud potřebujete sešit v paměti (např. pro odeslání přes webové API), použijte `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Streamování do prohlížeče

Nyní, když známe **create excel workbook c#**, integrujme to do ASP.NET Core kontroleru, aby si uživatelé mohli soubor stáhnout za běhu.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Když uživatel zavolá `/api/excel/download`, prohlížeč nabídne stažení *DynamicArray.xlsx*. Soubor již obsahuje sloupec **generated incremental numbers excel** díky vzorci `SEQUENCE`.

### Co když klient používá starší verzi Excelu?

Dynamické pole (včetně `SEQUENCE`) byla zavedena v Excel 365/2019. Pokud potřebujete zpětnou kompatibilitu, přejděte na ruční vyplnění:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Tento úryvek ukazuje klasický přístup **generate incremental numbers excel** bez spoléhání se na novou funkci.

---

## Časté otázky a okrajové případy

- **Do I need to enable iterative calculation?**  
  Ne. `SEQUENCE` je ne‑iterativní funkce; stačí jednoduché volání `CalculateFormula()`.

- **What if I want a horizontal spill?**  
  Změňte druhý argument: `=SEQUENCE(1,5,10,2)` rozlévá přes B1:F1.

- **Can I combine SEQUENCE with other functions?**  
  Rozhodně. Například `=INDEX(A:A, SEQUENCE(5,1,10,2))` může načíst řádky z jiného sloupce.

- **Is the workbook size a concern?**  
  Dopad velikosti souboru způsobený vzorcem je zanedbatelný. Velikost se stane problémem jen při ručním naplnění milionů buněk.

---

## Závěr

Prošli jsme **how to use sequence** v C# k **create excel workbook c#**, naservírovali tento sešit přes **ASP.NET create excel file** a ukázali čistý způsob **generate incremental numbers excel** bez psaní smyček. Hlavní myšlenka: nechte Excelův vlastní engine dynamických polí provádět počítání a nechte váš .NET kód soustředit se na orchestraci.

Neváhejte experimentovat—měňte argumenty `rows`, `start` nebo `step`, rozlévejte horizontálně, nebo kombinujte vzorec s `IF` či `FILTER` pro sofistikovanější reporty. Až budete připraveni, zkuste propojit více listů dohromady nebo exportovat sešit jako CSV pro downstream systémy.

Máte nějaký tip, který byste chtěli sdílet? Zanechte komentář níže nebo mě kontaktujte na GitHubu. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}