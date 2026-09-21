---
category: general
date: 2026-01-14
description: Jak zkopírovat kontingenční tabulku pomocí Aspose.Cells a zároveň se
  naučit převést Excel do PPTX, zkopírovat oblast do jiného sešitu a vytvořit editovatelný
  textový rámeček v PPTX v jedné výukové lekci.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: cs
og_description: Jak zkopírovat kontingenční tabulku a poté převést Excel do PPTX,
  zkopírovat oblast do jiného sešitu a udělat textové pole editovatelné v PPTX — vše
  pomocí Aspose.Cells.
og_title: Jak zkopírovat kontingenční tabulku v C# – Kompletní průvodce převodem Excel
  do PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Jak zkopírovat kontingenční tabulku v C# – převést Excel na PPTX, zkopírovat
  oblast a učinit textové pole editovatelným
url: /cs/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zkopírovat kontingenční tabulku v C# – Kompletní průvodce převodem Excel do PPTX

Jak zkopírovat kontingenční tabulku z jednoho sešitu do druhého je častá otázka při automatizaci reportů založených na Excelu. V tomto tutoriálu projdeme tři reálné scénáře s využitím **Aspose.Cells for .NET**: kopírování rozsahu s kontingenční tabulkou, export listu do souboru PPTX s editovatelným textovým polem a naplnění jedné buňky JSON polem pomocí Smart Markers.

Ukážeme si také, jak **převést Excel do PPTX**, **zkopírovat rozsah do jiného sešitu** a **udělat textové pole v PPTX editovatelné** bez narušení formátování. Na konci budete mít připravený kód, který můžete vložit do libovolného .NET projektu.

> **Tip:** Všechny příklady cílí na Aspose.Cells 23.12, ale stejné koncepty platí i pro starší verze s drobnými úpravami API.

![Diagram ukazující, jak se kopíruje kontingenční tabulka, jak se list exportuje do PPTX a jak se vloží JSON pole – workflow kopírování kontingenční tabulky](how-to-copy-pivot-table-diagram.png)

---

## Co budete potřebovat

- Visual Studio 2022 (nebo jakékoli C# IDE)
- .NET 6.0 nebo novější runtime
- NuGet balíček Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Dva ukázkové soubory Excel (`source.xlsx`, `chartWithTextbox.xlsx`) umístěné ve složce, kterou ovládáte (nahraďte `YOUR_DIRECTORY` skutečnou cestou).

Žádné další knihovny nejsou potřeba; stejný sestavení `Aspose.Cells` zpracovává Excel, PPTX i Smart Markers.

---

## Jak zkopírovat kontingenční tabulku a zachovat její data

Při kopírování rozsahu, který obsahuje kontingenční tabulku, je výchozí chování vložit pouze **hodnoty**. Chcete‑li zachovat definici kontingenční tabulky, musíte povolit příznak `CopyPivotTable`.

### Krok za krokem

1. **Načtěte zdrojový sešit**, který obsahuje kontingenční tabulku.  
2. **Vytvořte prázdný cílový sešit** – ten přijme zkopírovaný rozsah.  
3. **Použijte `CopyRange` s `CopyPivotTable = true`**, aby se definice kontingenční tabulky přenesla spolu s daty.  
4. **Uložte cílový soubor** kamkoli potřebujete.

#### Úplný příklad kódu

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Proč to funguje:**  
`CopyOptions.CopyPivotTable` říká Aspose.Cells, aby klonoval podkladový objekt `PivotTable` místo pouhých vykreslených hodnot. Cílový sešit nyní obsahuje plně funkční kontingenční tabulku, kterou můžete programově aktualizovat nebo upravovat.

**Okrajový případ:** Pokud zdrojový sešit používá externí datové zdroje, možná budete muset po kopírování vložit data nebo upravit řetězce připojení, jinak se kontingenční tabulka zobrazí jako “#REF!”.

---

## Převod Excelu do PPTX a vytvoření editovatelného textového pole

Export listu do PowerPointu je užitečný pro tvorbu prezentací přímo z dat. Ve výchozím nastavení se exportované textové pole stane statickým tvarem, ale nastavení `IsTextBoxEditable` toto chování obrátí.

### Krok za krokem

1. **Otevřete sešit**, který obsahuje graf a textové pole, které chcete exportovat.  
2. **Nastavte `ImageOrPrintOptions`** s `SaveFormat = SaveFormat.Pptx`.  
3. **Definujte oblast tisku**, která zahrnuje textové pole.  
4. **Povolte `IsTextBoxEditable`**, aby bylo možné text po otevření PPTX upravovat.  
5. **Uložte soubor PPTX**.

#### Úplný příklad kódu

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Výsledek:** Otevřete `result.pptx` v PowerPointu – textové pole, které jste umístili v Excelu, bude nyní běžným textovým polem, do kterého můžete psát. Není potřeba jej ručně znovu vytvářet.

**Častý úskalí:** Pokud list obsahuje sloučené buňky, které protínají oblast tisku, může se výsledný snímek posunout. Před exportem upravte oblast tisku nebo sloučené buňky rozpojte.

---

## Kopírování rozsahu do jiného sešitu pomocí Smart Markers (JSON → Jedna buňka)

Někdy potřebujete vložit JSON pole do jedné buňky Excelu, například při předávání dat do downstream systémů, které očekávají JSON řetězec. Smart Markery v Aspose.Cells mohou serializovat pole jako jednu buňku, pokud nastavíte `ArrayAsSingle = true`.

### Krok za krokem

1. **Načtěte šablonový sešit**, který obsahuje placeholder Smart Marker (např. `&=Items.Name`).  
2. **Připravte datový objekt** – anonymní typ s polem `Items`.  
3. **Vytvořte `SmartMarkerProcessor`** a aplikujte data s `ArrayAsSingle`.  
4. **Uložte naplněný sešit**.

#### Úplný příklad kódu

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Vysvětlení:**  
Když je `ArrayAsSingle` true, Aspose.Cells spojí každý prvek `Items.Name` do řetězce ve stylu JSON (`["A","B"]`) a zapíše jej do buňky, která obsahovala smart marker. Tím se vyhnete vytvoření samostatného řádku pro každý prvek pole.

**Kdy použít:** Ideální pro export konfiguračních tabulek, API payloadů nebo jakýkoli scénář, kde příjemce očekává kompaktní JSON řetězec místo tabulkového rozložení.

---

## Další tipy a řešení okrajových případů

| Scénář | Na co si dát pozor | Navrhované řešení |
|----------|-------------------|---------------|
| **Velké kontingenční tabulky** | Spotřeba paměti prudce roste při kopírování obrovských cache kontingenčních tabulek. | Použijte `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` před načtením. |
| **Export do PPTX s obrázky** | Obrázky mohou být rasterizovány při nízkém DPI. | Nastavte `pptxOptions.ImageResolution = 300` pro ostřejší snímky. |
| **Formátování JSON ve Smart Marker** | Speciální znaky (`"` , `\`) mohou rozbít JSON. | Escapujte je ručně nebo použijte `JsonSerializer` k předserializaci před předáním Smart Markerům. |
| **Kopírování rozsahu mezi různými verzemi Excelu** | Starší soubory `.xls` mohou ztratit formátování. | Uložte cíl jako `.xlsx`, aby se zachovaly moderní funkce. |

---

## Shrnutí – Jak zkopírovat kontingenční tabulku a mnohem víc

Začali jsme odpovědí na otázku **jak zkopírovat kontingenční tabulku** při zachování její funkčnosti, poté jsme vám ukázali, jak **převést Excel do PPTX**, **udělat textové pole v PPTX editovatelné**, a nakonec, jak **zkopírovat rozsah do jiného sešitu** pomocí Smart Markers pro vložení JSON pole do jedné buňky.  

Všechny tři úryvky jsou samostatné; můžete je vložit do nového konzolového aplikace, upravit cesty k souborům a spustit je ještě dnes.

---

## Co dál?

- **Prozkoumejte další exportní formáty** – Aspose.Cells také podporuje PDF, XPS a HTML.  
- **Obnovte kontingenční tabulky programově** pomocí `PivotTable.RefreshData()` po kopírování.  
- **Kombinujte Smart Markery s grafy** pro generování dynamických dashboardů, které se aktualizují automaticky.  

Pokud máte zájem o **uložení sešitu jako PPTX** s vlastními rozvrženími snímků, podívejte se na dokumentaci Aspose.Cells k `SlideOptions`.  

Neváhejte experimentovat – změňte oblast tisku, vyzkoušejte různé `CopyOptions` nebo předávejte složitější JSON payload. API je dostatečně flexibilní pro většinu reportingových pipeline.

---

### Často kladené otázky

**Q: Kopíruje `CopyPivotTable` také slicery?**  
A: Ne přímo. Slicery jsou samostatné objekty; po kopírování je budete muset znovu vytvořit nebo je zkopírovat pomocí kolekce `Worksheet.Shapes`.

**Q: Můžu exportovat více listů do jedné PPTX prezentace?**  
A: Ano. Procházejte každý list, zavolejte `Save` se stejnými `ImageOrPrintOptions` a nastavte `pptxOptions.StartSlideNumber`, aby se číslování pokračovalo.

**Q: Co když moje JSON pole obsahuje vnořené objekty?**  
A: Nastavte `ArrayAsSingle = false` a použijte vlastní šablonu, která iteruje přes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}