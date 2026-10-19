---
category: general
date: 2026-05-23
description: Vytvořte nový list v C# s podrobným návodem krok za krokem. Naučte se,
  jak vytvořit sešit, použít dynamický poleový vzorec, exportovat seřazená data a
  uložit sešit.
draft: false
keywords:
- create new worksheet
- how to create workbook
- how to save workbook
- export sorted data
- dynamic array formula
language: cs
og_description: Vytvořte nový list v C# pomocí Aspose.Cells. Tento průvodce ukazuje,
  jak vytvořit sešit, použít dynamický poleový vzorec, exportovat seřazená data a
  uložit sešit.
og_title: Vytvořte nový pracovní list v C# – Kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create new worksheet in C# with a step‑by‑step tutorial. Learn how
    to create workbook, use a dynamic array formula, export sorted data and save workbook.
  headline: Create New Worksheet in C# – Complete Guide to Dynamic Array Formulas
  type: TechArticle
- questions:
  - answer: The file will open, but the `SORT` formula will appear as text and show
      a `#NAME?` error. For backward compatibility, generate the sorted list in code
      and write the values directly.
    question: Does this work on older Excel versions that don’t support dynamic arrays?
  - answer: Absolutely. Use `=SORT(A2:C10, {1,2}, {1,-1})` where the second argument
      specifies the column indices and the third the sort order.
    question: Can I sort by multiple columns?
  - answer: 'After saving the workbook, load it again and call `worksheet.Cells.ExportDataTableAsString`
      or use `CsvSaveOptions` if your library provides one. --- ## Next Steps - **Explore
      other dynamic array functions** such as `FILTER`, `UNIQUE`, and `SEQUENCE`.
      - **Automate chart creation** on the same worksh'
    question: What if I need to export the sorted data to CSV?
  type: FAQPage
tags:
- C#
- Excel Automation
- Aspose.Cells
- Spreadsheet
title: Vytvořit nový list v C# – Kompletní průvodce dynamickými maticovými vzorci
url: /cs/net/excel-worksheet-csharp-tutorials/create-new-worksheet-in-c-complete-guide-to-dynamic-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového listu v C# – Kompletní průvodce dynamickými polemi

Už jste se někdy zamysleli, jak **vytvořit nový list** v C# bez ručního otevírání Excelu? Nejste v tom sami. Mnoho vývojářů potřebuje generovat reporty, řadit data za běhu a odeslat výsledek jako soubor .xlsx – vše z kódu.  

V tomto tutoriálu vás provedeme přesně tímto: ukážeme **jak vytvořit workbook**, vložíme **dynamic array formula** do zcela nového listu, **exportujeme setříděná data** a nakonec **jak uložit workbook**, abyste jej mohli sdílet s kýmkoli. Žádné zbytečnosti, jen solidní, spustitelný příklad, který můžete dnes zkopírovat a vložit.

## Co se naučíte

- Předpoklady pro použití Aspose.Cells (nebo jakékoli srovnatelné .NET Excel knihovny).  
- Jak **vytvořit nový list**, zapsat `SORT` formulář a nechat Excel automaticky vyplnit spill oblast.  
- Tipy pro zacházení s okrajovými případy, jako jsou prázdné zdrojové oblasti nebo velké datové sady.  
- Jak **exportovat setříděná data** do nového souboru a ověřit výstup.  
- Rychlý pohled na alternativní přístupy, pokud dáváte přednost `OpenXML` nebo `EPPlus`.  

Na konci tohoto průvodce budete mít samostatný program, který vytvoří setříděný seznam v novém listu, připravený pro další zpracování.

---

## Krok 1: Nastavení projektu – Jak vytvořit Workbook

Nejprve připravme prostředí. Použijeme **Aspose.Cells for .NET**, protože podporuje plný výpočetní engine Excelu, včetně nejnovějších **dynamic array formulas** jako `SORT`. Pokud používáte jinou knihovnu, koncepty zůstávají stejné – stačí vyměnit jmenný prostor.

```csharp
// Add the Aspose.Cells NuGet package
//   dotnet add package Aspose.Cells
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook();   // <-- this is how we **how to create workbook**
```

**Proč je to důležité:**  
Vytvoření objektu `Workbook` vytvoří v‑paměti reprezentaci souboru Excel. Není potřeba COM interop ani instalace Excelu. To činí řešení přenosným napříč Windows, Linux a Docker kontejnery.

> **Pro tip:** Pokud již máte soubor šablony, předávejte jeho cestu do `new Workbook("template.xlsx")` místo zahájení od nuly.

---

## Krok 2: Přidání nového listu – Vytvořit nový list

Nyní, když máme workbook, potřebujeme místo pro naše data. Ve výchozím nastavení Aspose vytvoří jediný list s názvem „Sheet1“. Přidáme další, aby příklad zůstal přehledný.

```csharp
            // Step 2: Add a new worksheet to hold the sorted output
            int newSheetIndex = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[newSheetIndex];   // <-- **create new worksheet**
```

**Co se děje pod kapotou?**  
`Worksheets.Add()` vrací index nově přidaného listu počínaje nulou. Poté získáme objekt `Worksheet`, abychom mohli přímo manipulovat s buňkami.

> **Pozor:** Pokud voláte `Add()` opakovaně bez uložení indexu, můžete ztratit přehled, do kterého listu zapisujete. Vždy si uchovejte referenci.

---

## Krok 3: Vložení ukázkových dat (volitelné)

Aby `SORT` formulář měl na čem pracovat, potřebujeme zdrojovou oblast. Naplňme `A2:A6` několika neřazenými hodnotami.

```csharp
            // Populate source data (A2:A6) – this mimics a raw data table
            string[] rawValues = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < rawValues.Length; i++)
            {
                sheet.Cells[i + 1, 0].PutValue(rawValues[i]); // Row i+1, Column 0 (A column)
            }
```

Proč umístit data na *stejný* list? Protože funkce `SORT` může odkazovat na oblast ve stejném listu; to udržuje ukázku kompaktní. Ve skutečných scénářích můžete číst z databáze, CSV nebo jiného listu.

---

## Krok 4: Zapsání dynamic array formula – Export setříděných dat

Zde je jádro tutoriálu: vložíme **dynamic array formula**, která automaticky rozšíří setříděný seznam do sousedních buněk.

```csharp
            // Step 4: Write a SORT formula into cell A1 (row 0, column 0)
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";   // <-- **dynamic array formula**
```

Když Excel vyhodnotí `=SORT(A2:A6)`, vytvoří vertikální pole hodnot v abecedním pořadí. Díky spill chování zavedenému v Excelu 365 výsledky automaticky zaplní `A1:A5`.

> **Častá otázka:** *Co když je zdrojová oblast prázdná?*  
> Formulář vrátí chybu `#SPILL!`. Chraňte se tím, že před zápisem formuláře zkontrolujete `rawValues.Length`, nebo jej obalíte do `IFERROR(SORT(...), "")`.

---

## Krok 5: Vynucení výpočtu – Nechte formulář běžet

```csharp
            // Recalculate the workbook so the spill range is populated
            workbook.CalculateFormula();   // <-- triggers **export sorted data**
```

**Za scénou:** Výpočetní engine parsuje strom formuláře, řeší odkazy na buňky a zapíše výsledné pole zpět do listu. Tento krok je nezbytný; jinak byste v souboru viděli surový text `=SORT(A2:A6)`.

---

## Krok 6: Uložení souboru – Jak uložit Workbook

Nakonec uložíme workbook na disk. Můžete zvolit libovolnou složku; jen se ujistěte, že proces má oprávnění k zápisu.

```csharp
            // Step 6: Save the workbook to view the result
            string outputPath = @"YOUR_DIRECTORY\sorted_output.xlsx";
            workbook.Save(outputPath);   // <-- **how to save workbook**
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Proč použít `Save` místo `SaveCopyAs`?**  
`Save` přepíše cílový soubor, což je v pořádku pro jednorázový export. Pokud potřebujete zachovat originál nedotčený, nejprve zavolejte `workbook.SaveCopyAs("backup.xlsx")`.

---

## Kompletní funkční příklad

Poskládáním všeho dohromady zde máte kompletní program, který můžete právě teď zkompilovat:

```csharp
using Aspose.Cells;
using System;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a fresh worksheet
            int sheetIdx = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[sheetIdx];

            // 3️⃣ Seed unsorted data (A2:A6)
            string[] values = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < values.Length; i++)
                sheet.Cells[i + 1, 0].PutValue(values[i]);

            // 4️⃣ Insert the SORT dynamic array formula in A1
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";

            // 5️⃣ Calculate so the spill range fills
            workbook.CalculateFormula();

            // 6️⃣ Save the workbook
            string outFile = @"C:\Temp\sorted_output.xlsx";
            workbook.Save(outFile);
            Console.WriteLine($"✅ Workbook saved – open {outFile} to see the sorted list.");
        }
    }
}
```

### Očekávaný výstup

Když otevřete `sorted_output.xlsx`, buňka **A1** bude obsahovat „Alpha“, **A2** „Bravo“, **A3** „Charlie“, **A4** „Delta“ a **A5** „Echo“. Původní neřazený seznam zůstane v **A2:A6** (zdrojová oblast), což dokazuje, že **dynamic array formula** úspěšně exportovala setříděná data.

---

## Řešení okrajových případů a variant

| Situace | Co dělat |
|-----------|------------|
| **Zdrojová oblast větší než 1 048 576 řádků** | Platí limit řádků Excelu; rozdělte data do více listů nebo použijte databázi pro těžší zpracování. |
| **Smíšené datové typy (čísla + text)** | `SORT` standardně umístí čísla před text. Použijte `SORTBY` s vlastním klíčem řazení, pokud potřebujete jiný pořádek. |
| **Potřebujete setříděné hodnoty jako statickou oblast** | Po výpočtu zkopírujte spill oblast a vložte pouze hodnoty (`PasteSpecial`), poté odstraňte formulář. |
| **Použití OpenXML/EPPlus místo Aspose** | Kroky jsou identické; stačí nahradit `Workbook`/`Worksheet` ekvivalenty knihovny a zavolat `Package.Save()`. |

---

## Často kladené otázky

**Q: Funguje to i ve starších verzích Excelu, které nepodporují dynamické pole?**  
A: Soubor se otevře, ale `SORT` formulář se zobrazí jako text a ukáže chybu `#NAME?`. Pro zpětnou kompatibilitu vygenerujte setříděný seznam v kódu a přímo zapište hodnoty.

**Q: Můžu řadit podle více sloupců?**  
A: Rozhodně. Použijte `=SORT(A2:C10, {1,2}, {1,-1})`, kde druhý argument určuje indexy sloupců a třetí směr řazení.

**Q: Co když potřebuji exportovat setříděná data do CSV?**  
A: Po uložení workbooku jej znovu načtěte a zavolejte `worksheet.Cells.ExportDataTableAsString` nebo použijte `CsvSaveOptions`, pokud vaše knihovna takovou možnost poskytuje.

---

## Další kroky

- **Prozkoumejte další dynamic array funkce** jako `FILTER`, `UNIQUE` a `SEQUENCE`.  
- **Automatizujte vytváření grafů** na stejném listu pro vizualizaci setříděných výsledků.  
- **Integrujte s ASP.NET Core**, aby uživatelé mohli stáhnout vygenerovaný soubor přímo z webového API.  

Každé z těchto témat staví na základech zde pokrytých – vytvoření workbooku, přidání listu, aplikace formulářů a uložení souboru.

---

## Závěr

We právě ukázali, jak **vytvořit nový list** v C#, vložit **dynamic array formula**, **exportovat setříděná data** a nakonec **jak uložit workbook**. Přístup je jednoduchý, vyžaduje jen několik řádků kódu a spolehlivě funguje napříč platformami.  

Vyzkoušejte to, upravte zdrojovou oblast, vyměňte `SORT` za `FILTER` nebo nasměrujte výstup do reportovací služby. Možnosti jsou neomezené, jakmile ovládnete základy programové manipulace s Excelem.  

Šťastné kódování a ať jsou vaše tabulky vždy setříděné!

## Související tutoriály

- [Jak vytvořit a uložit Excel workbook jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Vytvořit a uložit Excel workbook jako PDF v ASP.NET pomocí Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Jak vytvořit a stylovat Excel tabulky pomocí Aspose.Cells pro .NET | Průvodce krok za krokem](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}