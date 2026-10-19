---
category: general
date: 2026-09-15
description: Naučte se, jak kopírovat kontingenční tabulku, kopírovat list s kontingenční
  tabulkou a uložit sešit jako pptx pomocí Aspose.Cells v C#. Kompletní krok‑za‑krokem
  průvodce.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: cs
lastmod: 2026-09-15
og_description: Jak zkopírovat kontingenční tabulku, zkopírovat list s kontingenční
  tabulkou a uložit sešit jako pptx pomocí Aspose.Cells. Sledujte kompletní, spustitelné
  příklady v C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Jak zkopírovat kontingenční tabulku a exportovat listy – kompletní průvodce
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak zkopírovat kontingenční tabulku při zachování listů
url: /cs/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku při zachování listů

Pokud potřebujete **jak zkopírovat kontingenční tabulku** z jednoho sešitu do druhého, aniž byste ztratili podkladovou pivotní mezipaměť, tento průvodce poskytuje připravené řešení. Také uvidíte, jak **kopírovat list s pivotem** a jak **uložit sešit jako pptx**, přičemž zachováte editovatelné textové pole. Všechny příklady používají nejnovější Aspose.Cells pro .NET, takže můžete kód vložit do libovolného C# projektu a okamžitě vidět výsledky.

Práce s Excel soubory programově často zahrnuje přesouvání dat mezi sešity, export do prezentací nebo vkládání složitých Smart Markerů. Níže uvedené tři úryvky kódu pokrývají tyto běžné scénáře a vysvětlují, proč je každý krok důležitý.

## Požadavky

Než začnete, ujistěte se, že máte:

* .NET 6.0 nebo novější nainstalovaný  
* Aspose.Cells pro .NET (verze 25.11 nebo novější) přidanou do projektu  
* Složku pojmenovanou `YOUR_DIRECTORY`, odkud budou čteny a zapisovány ukázkové soubory  

Žádné další NuGet balíčky nejsou vyžadovány.

---

## Jak zkopírovat kontingenční tabulku pomocí Aspose.Cells

Kopírování oblasti, která obsahuje kontingenční tabulku, při zachování pivotní mezipaměti, je častý požadavek. Následující kroky ukazují přesné pořadí, které potřebujete.

### Krok 1 – Načtěte zdrojový sešit, který obsahuje kontingenční tabulku

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Proč*: Aspose.Cells načte sešit do paměti, což vám umožní přístup k listům, buňkám a kontingenčním tabulkám.

### Krok 2 – Vytvořte prázdný cílový sešit

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Proč*: Začátek s prázdným sešitem zaručuje, že žádné skryté styly nebo pojmenované oblasti nebudou zasahovat do operace kopírování.

### Krok 3 – Zkopírujte řádky, které zahrnují kontingenční tabulku

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Proč*: `CopyRows` kopíruje surové hodnoty buněk, formáty a odkazy na podkladovou pivotní mezipaměť. Oblast musí zahrnovat celou plochu kontingenční tabulky.

### Krok 4 – Zkopírujte sloupce, které obsahují kontingenční tabulku

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Proč*: Kontingenční tabulky zasahují jak do řádků, tak do sloupců; kopírování sloupců zajišťuje zachování kompletního rozvržení tabulky.

### Krok 5 – Přeneste připravený list do cílového sešitu

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Proč*: Metoda `Copy` klonuje list, včetně pivotní mezipaměti, takže cílový sešit zobrazí identickou kontingenční tabulku.

### Krok 6 – Uložte výsledek – kontingenční tabulka zůstane nedotčena

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Proč*: Uložení sešitu zapisuje všechny vnitřní struktury, což zaručuje, že pivot lze později obnovit.

**Tip**: Po kopírování můžete zavolat `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()`, aby se data aktualizovala, pokud se zdrojová data změnila.

---

## Kopírovat list s pivotem – stručná alternativa

Pokud potřebujete jen duplikovat celý list, který již obsahuje kontingenční tabulku, můžete přeskočit kroky kopírování řádků/sloupců a použít přímo metodu `Copy` na úrovni listu.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Tento přístup je užitečný, když list neobsahuje žádná další data mimo oblast pivotu. Operace **copy worksheet with pivot** automaticky zachovává veškeré formátování, pojmenované oblasti a pivotní mezipaměti.

---

## Uložit sešit jako PPTX s editovatelnými textovými poli

Export listu Excelu, který obsahuje editovatelné textové pole, do PowerPointu může být vyžadován pro reportovací dashboardy. Níže uvedený kód ukazuje **save workbook as pptx** při zachování editovatelnosti textového pole.

### Krok 1 – Načtěte sešit, který obsahuje textové pole

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Krok 2 – Nakonfigurujte možnosti uložení PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Proč*: Nastavení `ExportEditableTextBox` říká Aspose.Cells, aby přeložil Excel textové pole na PowerPoint tvar, který zůstane po exportu editovatelný.

### Krok 3 – Uložte sešit jako PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Očekávaný výsledek**: Otevřete `Result.pptx` v PowerPointu, vyberte textové pole a upravte jeho obsah stejně jako u jakéhokoli nativního tvaru.

**Častá otázka**: *Co když potřebuji textové pole zamknout?*  
Nastavte `pptxOptions.ExportEditableTextBox = false`; tvar bude převeden na statický obrázek.

---

## Exportovat Smart Marker, který obsahuje JSON pole jako hodnotu jedné buňky

Smart Markery vám umožňují naplnit Excel šablony složitými datovými strukturami. Níže je kompletní příklad, který demonstruje **jak zkopírovat kontingenční tabulku**‑stylové zpracování dat při vkládání JSON pole do jedné buňky.

### Krok 1 – Připravte SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Krok 2 – Vložte Smart Marker do buňky A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Krok 3 – Definujte zdroj dat s polem ve stylu JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Krok 4 – Zpracujte sešit

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Krok 5 – Uložte výsledný sešit

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Ověření výsledku**: Otevřete `JsonSingleCell.xlsx` a potvrďte, že buňka A1 obsahuje `A,B,C`. To ukazuje, jak zacházet s kolekcí jako s hodnotou jedné buňky, což je vzor často potřebný při exportu dat pro downstream systémy.

---

## Kompletní funkční příklad

Níže je jeden program, který kombinuje všechny tři scénáře. Kód můžete zkopírovat do konzolové aplikace, upravit cesty k souborům a spustit ho, abyste viděli všechny tři výstupy.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Spuštění tohoto programu vytvoří:

* `CopyWithPivot.xlsx` – dokonalou kopii původní kontingenční tabulky.  
* `Result.pptx` – snímek PowerPointu s editovatelným textovým polem.  
* `JsonSingleCell.xlsx` – list, kde se JSON pole zobrazuje v jedné buňce.

---

## Závěr

Nyní víte, **jak zkopírovat kontingenční tabulku** bezpečně, **jak kopírovat list s pivotem** jedním voláním a **jak uložit sešit jako pptx** při zachování editovatelných textových polí. Tyto vzory pokrývají nejčastější workflowy Excel‑to‑PowerPoint a Excel‑to‑JSON, se kterými se setkáte v podnikovém automatizačním prostředí.

Dále můžete zkoumat:

* Obnovování zkopírovaných kontingenčních tabulek programově (`PivotTable.Refresh()`)  
* Export do dalších formátů, jako PDF nebo HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Používání pokročilých možností Smart Markeru, jako jsou vlastní funkce nebo podmíněné formátování  

Neváhejte experimentovat s různými oblastmi, více listy nebo většími JSON strukturami. API Aspose.Cells vám poskytuje detailní kontrolu, takže můžete tyto příklady přizpůsobit jakémukoli reálnému scénáři. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Vytvořit nový sešit – Jak zkopírovat list s kontingenční tabulkou](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Jak zkopírovat kontingenční tabulku v C# – Převést Excel na PPTX, kopírovat oblast a vytvořit textové pole](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Kopírovat listy v rámci sešitu pomocí Aspose.Cells pro .NET – Krok za krokem](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}