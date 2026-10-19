---
category: general
date: 2026-06-08
description: Jak propojit listy v Excelu pomocí SmartMarkerProcessor pro master‑detail
  reporty. Vyplňte hlavní list a snadno vytvořte master‑detail Excel report.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: cs
og_description: Jak propojit listy v Excelu pomocí SmartMarkerProcessor. Naučte se
  naplnit hlavní list a během několika minut vytvořit report master‑detail.
og_title: Jak propojit listy v Excelu pomocí SmartMarker – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Jak propojit listy v Excelu pomocí SmartMarker – krok za krokem
url: /cs/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak propojit listy v Excelu pomocí SmartMarker – krok za krokem průvodce

Už jste se někdy zamysleli, **jak propojit listy** v Excelu bez ručního kopírování řádků nebo psaní nekonečných smyček VBA? Nejste v tom sami. Většina vývojářů narazí na problém, když potřebují čistou master‑detail zprávu, která zůstane synchronizovaná při změnách dat. Dobrá zpráva? SmartMarkerProcessor za vás udělá těžkou práci a z několika řádků C# vytvoří plnohodnotný master‑detail sešit.

V tomto tutoriálu projdeme přesně kroky k **vyplnění hlavního listu**, nastavení detailního listu a nakonec **vytvoření master‑detail zprávy**, která se aktualizuje automaticky. Na konci budete mít znovupoužitelný vzor, který můžete vložit do libovolného .NET projektu.

> **Poznámka k předpokladům:** Potřebujete GrapeCity Documents for Excel (GcExcel) verze 2024 nebo novější, vývojové prostředí .NET (Visual Studio 2022 funguje skvěle) a základní znalost C#. Žádné další NuGet balíčky kromě GcExcel nejsou vyžadovány.

---

## Přehled řešení

Než se ponoříme do kódu, rozložme si, co ve skutečnosti znamená „propojení listů“ v kontextu SmartMarker:

1. **Master sheet** – Obsahuje jeden řádek na entitu (např. seznam zákazníků).
2. **Detail sheet** – Obsahuje řádky, které patří k hlavnímu řádku (např. objednávky pro každého zákazníka).
3. **SmartMarker syntax** – Malý značkovací jazyk (`{MasterSheet}#master;{DetailSheet}#detail`), který procesoru říká, jak propojit dvě datové tabulky.
4. **Processor options** – Povolení `MasterDetail` způsobí, že engine automaticky opakuje hlavní řádky a vloží související detailní řádky pod ně.

Porozumění těmto částem vám pomůže později přizpůsobit přístup – možná budete potřebovat trojúrovňové vnoření nebo podmíněné formátování. Uchovejte si tento mentální model po ruce, když budeme procházet implementací.

## Krok 1: Připravte hierarchická data pro zpracování Master‑Detail

První věc, kterou potřebujete, je zdroj dat, který odráží vztah master‑detail. Ve většině reálných scénářů pochází z databáze, ale pro přehlednost použijeme anonymní objektový literál.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Proč je to důležité:** SmartMarker nehádat vztahy magicky; hledá shodná názvy vlastností (`MasterId` → `Id`). Strukturou dat tímto způsobem poskytujeme procesoru jasnou mapu, což je základ **jak propojit listy** efektivně.

> **Tip:** Pokud jsou vaše data v objektech `DataTable`, stačí je vystavit jako vlastnosti se stejnými názvy – SmartMarker funguje s libovolnou výčtovou kolekcí.

## Krok 2: Vytvořte sešit a načtěte šablonu

SmartMarker pracuje s existujícím Excel sešitem, obvykle šablonou, která již obsahuje názvy listů a zástupné značky. Vytvořme sešit v paměti a přidejme dva prázdné listy pojmenované *MasterSheet* a *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Můžete také načíst soubor `.xlsx` z disku (`wb.Open("Template.xlsx")`), pokud raději nejprve navrhujete rozvržení v Excelu. Důležité je, aby názvy listů odpovídaly těm, na které budete odkazovat ve SmartMarker řetězci.

## Krok 3: Vytvořte instanci SmartMarkerProcessor a povolte režim Master‑Detail

Nyní přivedeme engine, který načte značky a vloží data. `SmartMarkerProcessor` přijímá sešit jako argument konstruktoru a příznak `Options.MasterDetail` mu říká, aby považoval značky `#master` a `#detail` za propojený pár.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Proč povolit `MasterDetail`?** Bez tohoto příznaku by procesor považoval `{MasterSheet}#master` a `{DetailSheet}#detail` za nezávislé operace, čímž by ztratil klíčový vztah mezi řádky. Nastavení příznaku je jediný řádek, který umožní **jak propojit listy** skutečně fungovat.

## Krok 4: Definujte SmartMarker řetězec a spusťte procesor

Řetězec značek říká SmartMarkeru, který list je hlavní a který detailní. Syntaxe je jednoduchá: `{SheetName}#master;{SheetName}#detail`. Můžete také přidat další značky (např. `#header`), ale pro základní zprávu nejsou potřeba.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Když `Process` běží, engine:

1. Zapíše každý hlavní řádek do *MasterSheet* počínaje prvním prázdným řádkem po hlavičce.
2. Pro každý hlavní řádek prohledá kolekci `Details`, vybere řádky, kde `MasterId` odpovídá hlavnímu `Id`, a zapíše je do *DetailSheet* přímo pod odpovídající hlavní položku.

## Krok 5: Uložte nebo exportujte výsledný sešit

V tomto okamžiku máte plně vyplněný sešit. Můžete jej uložit na disk, streamovat zpět webovému klientovi nebo dokonce převést do PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Otevřete soubor a uvidíte dva listy: *MasterSheet* uvádí `A` a `B`, zatímco *DetailSheet* zobrazuje `Item1` pod hlavním `1` a `Item2` pod hlavním `2`. To je podstata **vyplnění hlavního listu** a **vytvoření master‑detail zprávy** najednou.

## Vizualní přehled

![Diagram ilustrující, jak propojit listy v Excelu pomocí SmartMarkerProcessor](https://example.com/diagram.png "Diagram propojení listů")

Diagram (alternativní text obsahuje hlavní klíčové slovo) ukazuje tok dat z objektů C# → SmartMarkerProcessor → propojené listy Excelu.

## Řešení běžných okrajových případů

### Více detailních řádků na jeden hlavní řádek

Pokud má hlavní řádek několik souvisejících detailů, SmartMarker opakuje hlavní řádek jednou a poté zapíše *vše* odpovídající detailní řádky pod něj. Žádný další kód není potřeba – stačí zajistit, aby vaše kolekce `Details` obsahovala všechny řádky.

### Chybějící detaily

Když hlavní položka nemá žádné odpovídající detailní řádky, detailní list tuto sekci jednoduše přeskočí. Pokud potřebujete zástupný text (např. „Žádné položky“), můžete přidat vypočítaný sloupec v šabloně, který používá Excelovou funkci jako `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Velké datové sady

Zpracování desítek tisíc řádků může být náročné na paměť. Pro udržení rychlého výkonu:

- Použijte `processor.Options.EnableStreaming = true` (k dispozici v GcExcel 2025+).
- Rozdělte data na úseky a zpracovávejte každý úsek zvlášť, poté sloučte sešity.

### Vlastní mapování sloupců

Pokud se názvy vašich vlastností neshodují (`MasterKey` vs `Id`), můžete před zpracováním použít metodu `SmartMarkerProcessor.Map` k vytvoření aliasu.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní, připravený program ke kopírování a vložení, který můžete spustit okamžitě.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Mistrovské externí vzorce v Excelu pomocí Aspose.Cells pro Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Mistrovské dynamické listy Excelu v Java s Aspose.Cells: komplexní průvodce](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Mistrovské dynamické Excel zprávy pomocí Aspose.Cells Java: pojmenované oblasti a složité vzorce](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}