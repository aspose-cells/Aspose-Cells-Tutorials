---
category: general
date: 2026-08-14
description: Export Excel do PowerPointu pomocí Aspose.Cells a naučte se, jak vypočítat
  Excelové vzorce v kódu. Krok za krokem příklad v C# s kompletním zdrojovým kódem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: cs
lastmod: 2026-08-14
og_description: Exportujte Excel do PowerPointu pomocí Aspose.Cells a vypočítejte
  Excelové vzorce v kódu. Následujte tento kompletní průvodce pro vytvoření editovatelných
  souborů PPTX ze sešitů.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Export Excel do PowerPointu s Aspose.Cells – kompletní C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Export Excel do PowerPointu pomocí Aspose.Cells – kompletní programovací průvodce
url: /cs/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel do PowerPointu pomocí Aspose.Cells – kompletní programovací průvodce

Pokud potřebujete **exportovat Excel do PowerPointu** programově, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.Cells pro .NET. Také se naučíte, jak **vypočítat Excelové vzorce v kódu**, kopírovat kontingenční tabulky bez ztráty definic a použít novou funkci Office‑365 EXPAND pro dynamické pole.

V následujících sekcích projdeme reálný příklad v C#, vysvětlíme, proč je každá řádka důležitá, a pokryjeme běžné úskalí, abyste mohli řešení přizpůsobit svým projektům.

## Co tento tutoriál pokrývá

* Načtení existujícího sešitu (`input.xlsx`)  
* Kopírování rozsahu, který obsahuje kontingenční tabulku, při zachování její definice  
* Exportování sešitu do PowerPointu (`.pptx`) s editovatelnými textovými poli a tvary  
* Exportování rozsahu buněk jako řetězců pomocí vlastní logiky  
* Vypočítání Excelových vzorců v kódu, včetně funkce Office‑365 EXPAND  
* Uložení finálního sešitu se všemi provedenými změnami  

**Požadavky**  
* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7.2+)  
* Aspose.Cells pro .NET v25.11 nebo novější (volba `CopyPivotTable` byla zavedena ve verzi v25.11)  
* Základní pochopení C# a konceptů Excelu, jako jsou rozsahy, kontingenční tabulky a vzorce  

> **Pro tip:** Nainstalujte Aspose.Cells přes NuGet (`Install-Package Aspose.Cells`), aby byl váš projekt aktuální s nejnovějšími funkcemi.

## Export Excel do PowerPointu pomocí Aspose.Cells

Prvním hlavním úkolem je převést sešit do prezentace PowerPoint, přičemž všechny vizuální prvky zůstávají editovatelné. To je nezbytné, pokud chcete automaticky generovat sady snímků z finančních zpráv nebo dashboardů.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Proč to funguje

* **`Workbook`** načte celý soubor Excel do paměti a poskytne vám plný přístup k API.  
* **`CopyRange`** s `CopyPivotTable = true` zajišťuje, že zdroj dat kontingenční tabulky, cache a rozložení jsou přesně duplikovány – něco, co starší verze Aspose.Cells nedokázaly.  
* Přidání nového listu (`Copy`) vám umožní ponechat původní list nedotčený, což je užitečné pro auditní stopy.

## Exportujte sešit do PowerPointu s editovatelnými objekty

Nyní převádíme sešit do souboru PowerPoint. Povolením `ExportEditableObjects` se každý graf, tvar nebo textové pole stane nativním objektem PowerPointu, který uživatelé mohou po exportu přímo upravovat.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Vysvětlení

* **`WorkbookDesigner`** je vysoceúrovňový pomocník, který připravuje sešit k exportu, zpracovává Smart Markers, pojmenované rozsahy a úpravy rozložení.  
* Nastavením `ExportEditableObjects = true` říkáte Aspose.Cells, aby převáděl kresby Excelu na tvary PowerPointu místo jejich zploštění do obrázků. To poskytuje **plně editovatelnou** sadu snímků.

> **Edge case:** Pokud váš sešit obsahuje složité grafy vytvořené z externích datových spojení, ujistěte se, že tato spojení jsou vyřešena před voláním `ExportToPptx`, jinak se graf může zobrazit prázdný.

## Exportujte rozsah jako řetězce pomocí vlastní logiky

Někdy potřebujete surové řetězcové hodnoty pro následné zpracování (např. předání CSV parseru). Třída `ExportTableOptions` vám umožňuje řídit, jak je každá buňka převedena.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Proč byste to mohli použít

* **Jednotný datový typ:** Exportování jako řetězce zabraňuje chybám typu‑mismatch, když spotřebitel očekává text.  
* **Vlastní formátování:** Nahraďte `value.ToString()` libovolným vlastním formátovačem (např. `value.ToString("yyyy-MM-dd")` pro data).  

## Vypočítejte Excelové vzorce v kódu

Častým požadavkem je **vypočítat Excelové vzorce v kódu** bez otevírání Excelu. Aspose.Cells poskytuje vestavěný výpočetní engine, který funguje offline a podporuje nejnovější funkce Office‑365, včetně `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Jak funguje výpočetní engine

* Vlastnost `Formula` ukládá výraz přesně tak, jak byste jej zadali v Excelu.  
* `CalculateFormula()` spustí úplnou rekalkulaci sešitu, respektujíc závislosti mezi buňkami.  
* Funkce `EXPAND` (dostupná v Excel 365) vrací rozšířený rozsah na základě zdrojové buňky (`B1`) a zadaných řádků (`5`) a sloupců (`3`).  

> **Tip:** Pokud potřebujete vypočítat jen podmnožinu sešitu, použijte `Worksheet.CalculateFormula()` k omezení rozsahu a zlepšení výkonu.

## Uložte sešit se všemi provedenými změnami

Nakonec zapíšete upravený sešit zpět na disk. Můžete uložit v libovolném podporovaném formátu (`.xlsx`, `.xls`, `.csv`, atd.) změnou přípony souboru.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Co ověřit

* Otevřete `result.xlsx` v Excelu a ověřte kopii kontingenční tabulky, výsledek vzorce `EXPAND` a všechny vlastní exportované řetězce.  
* Otevřete `output.pptx` v PowerPointu; měli byste vidět snímek, který odráží rozložení Excelu, a všechny grafy/textová pole by měly být editovatelné.

## Časté otázky a řešení problémů

| Question | Answer |
|----------|--------|
| **Potřebuji licenci k použití Aspose.Cells?** | Ano. Zkušební verze funguje pro hodnocení, ale plná licence odstraňuje vodoznaky hodnocení a odemyká funkci `CopyPivotTable`. |
| **Co když exportovaný PPTX zobrazuje prázdné tvary?** | Ověřte, že kreslicí objekty sešitu nejsou skryté (`Visible = true`) a že všechny externí odkazy na obrázky jsou před exportem vloženy. |
| **Mohu exportovat více listů do samostatných PPTX snímků?** | Použijte `WorkbookDesigner.ExportToPptx` v cyklu, přičemž pro každý list specifikujete odlišné `ExportOptions`, nebo je spojte do jedné prezentace přidáním snímků ručně pomocí Aspose.Slides. |
| **Je `CalculateFormula` thread‑safe?** | Ne. Provádějte výpočty na jediném vlákně nebo klonujte sešit pro každé vlákno, aby se předešlo závodním podmínkám. |

## Závěr

Nyní máte **kompletní, end‑to‑end řešení pro export Excel do PowerPoint** pomocí Aspose.Cells a rozumíte, jak **vypočítat Excelové vzorce v kódu**—včetně moderní funkce `EXPAND`. Tutoriál pokryl načítání sešitu, kopírování kontingenčních tabulek, export do editovatelného PowerPointu, vlastní export řetězců, výpočet vzorců a finální uložení.

Zde můžete:

* Rozšířit export tak, aby zahrnoval více snímků na list (sekundární klíčové slovo: *calculate Excel formulas in code* lze znovu použít při generování dat pro grafy).  
* Integrovat Aspose.Slides pro přidání animací nebo hlavních rozvržení snímků.  
* Nahradit jednoduchý delegát `CustomExport` formátováním citlivým na locale pro mezinárodní projekty.  

Neváhejte experimentovat s různými rozsahy, prozkoumat další funkce Office‑365 (např. `FILTER`, `SORT`) a kombinovat tento pracovní postup s automatizovaným doručováním e‑mailů pro plně autonomní reportingové pipeline.

---


## Co byste se měli učit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Automatizace exportu dat z Excelu pomocí Aspose.Cells pro .NET&#58; Průvodce krok za krokem](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Jak exportovat grafy Excelu do PDF pomocí Aspose.Cells pro .NET&#58; Průvodce krok za krokem](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export buněk Excelu do obrázku pomocí Aspose.Cells .NET&#58; Průvodce krok za krokem](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}