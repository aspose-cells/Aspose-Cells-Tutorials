---
category: general
date: 2026-07-29
description: Zkopírujte řádky z jednoho listu do druhého a naučte se, jak programově
  načíst sešit Excel pomocí Aspose.Cells v podrobném tutoriálu krok za krokem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: cs
lastmod: 2026-07-29
og_description: Kopírujte řádky z jednoho listu do druhého pomocí Aspose.Cells. Naučte
  se načíst sešit Excel programově a zachovat kontingenční tabulky během několika
  řádků C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Kopírování řádků z jednoho listu do druhého – Průvodce automatizací Excelu
  v C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Kopírování řádků z jednoho listu do druhého – kompletní průvodce C#
url: /cs/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopírování řádků z jednoho listu do druhého – Kompletní průvodce v C#  

Už jste někdy potřebovali **kopírovat řádky z jednoho listu do druhého**, ale nebyli jste si jisti, jak zachovat vzorce a kontingenční tabulky? Nejste v tom sami. V mnoha reportingových pipelinech musíme vyjmout část dat z hlavního listu a vložit ji do nového sešitu pro další zpracování. Dobrá zpráva? S Aspose.Cells to můžete provést programově a celá operace zabere jen několik řádků.  

V tomto tutoriálu vás provedeme načtením Excel sešitu programově, výběrem oblasti a následným kopírováním těchto řádků do zcela nového sešitu při zachování všech vložených kontingenčních tabulek. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného C# projektu – bez nutnosti ručního kopírování a vkládání.  

## Co dosáhnete

- **Načíst Excel sešit programově** pomocí třídy `Workbook` z Aspose.Cells.  
- Definovat **oblast buněk**, která obsahuje řádky, které chcete přesunout.  
- **Kopírovat řádky z jednoho listu do druhého** jedním voláním metody, která zachová kontingenční tabulky.  
- Uložit výsledek do nového souboru připraveného k distribuci nebo dalšímu zpracování.  

### Požadavky

- .NET 6.0 nebo novější (kód funguje jak na .NET Core, tak na .NET Framework).  
- Platná licence Aspose.Cells (nebo dočasný evaluační klíč).  
- Dva adresáře na disku: jeden pro zdrojový sešit (`Source.xlsx`) a druhý pro cílový (`Destination.xlsx`).  

Pokud je máte, pojďme na to.  

## Krok 1: Načíst Excel sešit programově

Nejprve—než budete moci cokoli kopírovat, musíte načíst zdrojový soubor do paměti. Aspose.Cells to usnadňuje:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Proč je to důležité:** Načtení sešitu programově vám dává plnou kontrolu nad obsahem souboru, aniž byste museli otevírat Excel na serveru. Také se tím vyhnete problémům s COM interop a funguje to v headless prostředích, jako jsou CI pipeline.  

## Krok 2: Definovat zdrojovou oblast, která obsahuje řádky

Dále přesně určete, které řádky chcete přenést. Objekt `CellArea` vám umožní specifikovat obdélníkový blok pomocí adresy levého horního a pravého dolního buňky:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Tip:** Pokud se velikost vašich dat dynamicky mění, můžete vypočítat `EndRow` pomocí `sourceWorksheet.Cells.MaxDataRow`, abyste vždy zachytili celou tabulku.  

## Krok 3: Vytvořit nový sešit pro cíl

Nyní vytvořte prázdný sešit, který přijme zkopírované řádky. Tento sešit má ve výchozím nastavení jeden list:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Proč nový sešit?** Začít s čistým sešitem zajišťuje, že nebudete omylem přepisovat existující data, a poskytuje předvídatelné prostředí pro testování.  

## Krok 4: Kopírovat řádky z jednoho listu do druhého (se zachováním kontingenčních tabulek)

Zde je jádro tutoriálu. Metoda `CopyRows` kopíruje vybrané řádky a když jako poslední argument předáte `true`, také zkopíruje všechny kontingenční tabulky, které se nacházejí v oblasti:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Co se děje pod kapotou?

- **Zdrojový list**: `sourceWorkbook.Worksheets[0]` ukazuje na první list ve zdrojovém souboru.  
- **Indexy řádků**: Aspose.Cells používá nulové indexování, takže `StartRow` a `EndRow` odpovídají řádkům, které jste definovali v `sourceRange`.  
- **Počáteční řádek cíle**: Začínáme na řádku 0 v novém listu, čímž se zkopírovaný blok umístí úplně na začátek.  
- **Příznak `true`**: Toto je magický přepínač, který říká Aspose.Cells, aby klonoval všechny kontingenční tabulky nalezené v zkopírovaných řádcích, a zachoval jejich cache a spojení.  

> **Upozornění na okrajový případ:** Pokud zdrojová oblast obsahuje sloučené buňky, které přesahují definovanou oblast, tyto sloučení budou oříznuty. Pro zachování jejich integrity rozšiřte oblast tak, aby plně pokrývala sloučený region.  

## Krok 5: Uložit cílový sešit

Nakonec zapište nový soubor na disk. Můžete si vybrat libovolný adresář; jen se ujistěte, že proces má oprávnění k zápisu:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Když otevřete `Destination.xlsx`, uvidíte řádky A1‑H20 duplikované, včetně všech původně vložených kontingenčních tabulek. Zbytek sešitu zůstane prázdný, připravený k přidání dalších listů nebo dat později.  

## Úplný funkční příklad

Spojením všech částí získáte kompletní, spustitelný program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Očekávaný výstup** (konzole):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Otevřete cílový soubor a ověřte, že data, formátování a kontingenční tabulky vypadají přesně jako ve zdroji. Pokud chybí nějaká data, dvakrát zkontrolujte, že `sourceRange` plně zahrnuje relevantní řádky.  

## Časté otázky a tipy

- **Mohu kopírovat do konkrétního listu místo prvního?**  
  Samozřejmě. Nahraďte `destinationWorkbook.Worksheets[0]` za `destinationWorkbook.Worksheets["TargetSheet"]` (list nejprve vytvořte, pokud neexistuje).  

- **Co když potřebuji kopírovat jen hodnoty, ne vzorce?**  
  Použijte `CopyRows` s přetížením, které přijímá objekt `CopyRowsOptions`, a nastavte `PasteType` na `PasteType.Values`.  

- **Jak zacházet s velkými soubory, aniž by došlo k vyčerpání paměti?**  
  Aspose.Cells podporuje **streamování** pomocí `LoadOptions` s `MemorySetting.MemoryPreference`. Načtěte zdrojový sešit s menší spotřebou paměti a operace kopírování bude i nadále efektivní.  

- **Zůstávají kontingenční tabulky propojené s původním zdrojem dat?**  
  Když nastavíte příznak `true`, pivotní cache se duplikuje, takže kontingenční tabulky v novém sešitu odkazují na zkopírovaná data, nikoli na původní soubor.  

## Závěr

Nyní víte, jak **kopírovat řádky z jednoho listu do druhého** při zachování všech kontingenčních tabulek, a viděli jste, jak **načíst Excel sešit programově** pomocí Aspose.Cells. Tento vzor je pevnou základnou pro tvorbu automatizovaných reportingových pipeline, skriptů pro migraci dat nebo jakýkoli scénář, kde potřebujete dynamicky spojovat data z Excelu.  

Co dál? Zkuste rozšířit úryvek na:

- Procházet více zdrojových oblastí a agregovat je do jednoho cílového souboru.  
- Aplikovat podmíněné formátování po kopírování pro zvýraznění klíčových metrik.  
- Exportovat finální sešit do PDF nebo CSV pro další využití.  

Neváhejte experimentovat a pokud narazíte na problém, zanechte komentář níže. Šťastné kódování!  

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.  

- [How to Copy Rows in Excel Using Aspose.Cells for .NET&#58; A C# Guide](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)  
- [Copy Worksheet from One Workbook to Another using Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)  
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step‑By‑Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}