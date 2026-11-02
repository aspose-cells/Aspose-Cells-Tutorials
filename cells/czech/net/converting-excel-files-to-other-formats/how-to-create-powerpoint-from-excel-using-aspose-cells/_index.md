---
category: general
date: 2026-09-18
description: Vytvořte PowerPoint z Excelu pomocí Aspose.Cells – zkopírujte kontingenční
  tabulky, exportujte rozsahy a uložte jako PPTX v několika řádcích C# kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: cs
lastmod: 2026-09-18
og_description: Rychle vytvořte PowerPoint z Excelu. Naučte se, jak kopírovat kontingenční
  tabulky, exportovat oblasti a uložit sešit jako PPTX pomocí Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Vytvořte PowerPoint z Excelu pomocí Aspose.Cells – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Jak vytvořit PowerPoint z Excelu pomocí Aspose.Cells
url: /cs/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit PowerPoint z Excelu pomocí Aspose.Cells

Pokud potřebujete vytvořit PowerPoint z Excelu, tento průvodce vám ukáže stručné, komplexní řešení. Uvidíte, jak zkopírovat kontingenční tabulku, exportovat vybraný rozsah a uložit výsledek jako soubor PPTX pomocí několika řádků C#.

Generování sady snímků přímo z dat tabulky odstraňuje ruční krok kopírování‑vkládání, který zpomaluje workflow reportování. Tutoriál pokrývá vše, co potřebujete, od nastavení projektu až po finální soubor PPTX, a funguje s nejnovější verzí Aspose.Cells pro .NET.

## Požadavky

* **Aspose.Cells for .NET** (verze 23.12 nebo novější). Nainstalujte jej pomocí NuGet: `Install-Package Aspose.Cells`.
* Vývojové prostředí **.NET 6+** (Visual Studio 2022 nebo VS Code).
* Excel sešit (`Source.xlsx`), který obsahuje data a kontingenční tabulku, kterou chcete znovu použít.
* Oprávnění k zápisu do výstupní složky.

Žádné další knihovny třetích stran nejsou vyžadovány.

## Vytvoření PowerPointu z Excelu – krok za krokem

Proces se skládá ze čtyř logických kroků, které odpovídají příkladu kódu, který uvidíte níže.

### Krok 1: Načtení zdrojového sešitu a definování rozsahu

Musíte načíst sešit, který obsahuje zdrojová data a kontingenční tabulku. Výběrem přesného rozsahu zajistíte, že budou přeneseny pouze potřebné buňky, což udržuje výsledný snímek lehký.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Proč je to důležité:**  
`CreateRange` vytvoří objekt `Range`, který lze zkopírovat jako celek. Omezením rozsahu na `A1:G20` se vyhnete přenášení nesouvisejících buněk, které by jinak mohly nafouknout soubor PowerPoint.

### Krok 2: Připravení cílového sešitu

Aspose.Cells zachází s PowerPoint snímkem jako sešitem, když jej ukládáte ve formátu PPTX. Vytvoření nového sešitu vám poskytne čisté plátno pro zkopírovaný rozsah.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** Pokud potřebujete více snímků, můžete přidat další listy a později uložit každý jako samostatný soubor PPTX.

### Krok 3: Kopírování rozsahu při zachování kontingenční tabulky

Metoda `CopyRange` přijímá objekt `PasteOptions`. Nastavením `CopyPivotTables = true` říkáte Aspose.Cells, aby zachoval strukturu kontingenční tabulky nedotčena, nejen vykreslené hodnoty.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Jak to funguje:**  
Když je `CopyPivotTables` nastaven na true, cílový list získá jak zdrojová data, tak i cache kontingenční tabulky. To znamená, že kontingenční tabulka zůstane plně funkční a může být později obnovena, pokud se změní zdrojová data.

### Krok 4: Uložení sešitu jako soubor PowerPoint

Nakonec exportujte sešit do formátu PPTX. Příznak `SaveFormat.Pptx` říká Aspose.Cells, aby zapsal list jako snímek PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Výsledek:**  
`CopyWithPivot.pptx` se otevře v Microsoft PowerPoint (nebo jakémkoli kompatibilním prohlížeči) s jedním snímkem, který zobrazuje zkopírovaný rozsah, včetně živé kontingenční tabulky, s níž lze v PowerPointu pracovat.

## Kompletní spustitelný příklad

Níže je kompletní program, který můžete vložit do nového konzolového projektu a okamžitě spustit.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Očekávaný výstup:**  
Spuštěním programu se vypíše „PowerPoint file created successfully.“ a vytvoří se soubor s názvem `CopyWithPivot.pptx`. Otevření souboru v PowerPointu zobrazí jeden snímek, kde se zkopírovaný Excel rozsah objeví přesně tak, jak byl ve zdrojovém listu, s aktivní kontingenční tabulkou, kterou lze v PowerPointu obnovit.

## Běžné varianty a okrajové případy

| Situace | Co změnit |
|-----------|----------------|
| **Více kontingenčních tabulek** | Definujte samostatné objekty `Range` pro každou tabulku a zavolejte `CopyRange` pro každou z nich, nebo zkopírujte celý list, pokud sdílejí stejný zdroj dat. |
| **Velké datové sady** | Zvětšete rozsah (např. `"A1:Z5000"`). Zvažte povolení `PasteOptions.CompressData = true` pro snížení velikosti PPTX. |
| **Různé rozvržení snímků** | Po uložení jako PPTX otevřete soubor v PowerPointu a použijte vlastní rozvržení nebo motiv; data zůstávají editovatelná. |
| **Ukládání do proudu** | Použijte `destinationWorkbook.Save(stream, SaveFormat.Pptx)`, když potřebujete vrátit PPTX přes webové API. |
| **Zachování formátování buněk** | Nastavte `PasteOptions.PasteType = PasteType.All`, aby se zachovaly písma, barvy a ohraničení. |

**Pro tip:** Vždy ověřte, že cílová složka existuje před voláním `Save`. Pokud složka chybí, `Save` vyhodí `DirectoryNotFoundException`.

## Závěr

Nyní víte, jak vytvořit PowerPoint z Excelu, zkopírovat kontingenční tabulku a exportovat výsledek jako soubor PPTX pomocí Aspose.Cells. Kroky – načtení zdrojového sešitu, definování rozsahu, kopírování s `CopyPivotTables` a uložení jako PPTX – pokrývají celý pracovní postup spolehlivým, připraveným pro produkci způsobem.

Dále prozkoumejte **jak exportovat Excel do PPTX** pro více listů, nebo se naučte **jak kopírovat rozsah mezi sešity**, když potřebujete sloučit data z několika zdrojů před vytvořením sady snímků. Obě témata staví na stejném API a lze je kombinovat pro automatizaci složitých reportingových pipeline.

Šťastné programování a užijte si převod vašich tabulek na profesionální prezentace!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak zkopírovat kontingenční tabulku v C# – převod Excelu do PPTX, kopírování rozsahu a vytvoření textového pole](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Vytvořit nový sešit – Jak zkopírovat list s kontingenční tabulkou](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Jak vytvářet a ukládat Excel soubory pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}