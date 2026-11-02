---
category: general
date: 2026-05-23
description: Jak používat značky s Aspose.Cells k dosažení dynamického pojmenování
  listů v automatizaci Excelu. Naučte se chytré značky, vazbu dat JSON a vytváření
  listů během několika minut.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: cs
og_description: Jak používat značky v Aspose.Cells k vytváření Excel souborů s dynamickým
  pojmenováním listů. Kompletní krok‑za‑krokem průvodce s úplným příkladem v C#.
og_title: Jak používat značky – Dynamické pojmenování listů v Excelu s Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak používat značky v Aspose.Cells pro dynamické pojmenování listů v Excelu
url: /cs/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat značky v Aspose.Cells pro dynamické pojmenování listů v Excelu

Už jste se někdy zamýšleli **jak používat značky** k přeměně statické šablony Excelu na plnohodnotnou master‑detail sešit? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují *dynamic sheet naming excel* funkce, zejména když názvy listů musí odrážet hodnoty pocházející z JSON nebo databáze.  

V tomto tutoriálu projdeme kompletním, připraveným příkladem v C#, který ukazuje **jak používat značky** s **Aspose.Cells** smart markers, svázat JSON data a nechat procesor vytvořit listy, jejichž názvy se mění za běhu. Žádné zbytečnosti, jen přesný kód, který můžete vložit do Visual Studia a okamžitě vidět výsledek.

## Co se naučíte

- Koncept **smart markers** a proč jsou ideální pro scénáře master‑detail.  
- Jak vložit značky do sešitu, které budou později nahrazeny skutečnými názvy listů.  
- Nastavení **dynamic sheet naming excel** pomocí volby `DetailSheetNewName`.  
- Spuštění `SmartMarkerProcessor` proti JSON datům pro automatické generování více listů.  
- Ověření výstupu a několik užitečných tipů, jak se vyhnout častým úskalím.

> **Předpoklady** – Potřebujete aktuální .NET runtime (≥ .NET 6 je v pořádku), knihovnu Aspose.Cells pro .NET (můžete si stáhnout bezplatnou zkušební verzi z Aspose) a základní znalost C#.  

---

![příklad použití značek v Aspose.Cells](example.png "příklad použití značek v Aspose.Cells")

## Jak používat značky k vytvoření dynamického pojmenování listů (Krok 1)

Prvním krokem je prázdný sešit, který bude sloužit jako naše šablona. V reálném projektu byste pravděpodobně začali s existujícím souborem `.xlsx`, který už obsahuje rozvržení, formátování a placeholder buňky. Pro přehlednost vše vytvoříme programově.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Proč je to důležité*: Objekt `Worksheet` je místem, kam vložíme naše **smart marker** značky. Představte si je jako malé placeholdery, které procesor později nahradí skutečnými hodnotami z JSON.  

## Vložení značek smart marker (Krok 2)

Nyní umístíme značky přímo do buněk. Syntaxe `${...}` říká Aspose.Cells „toto je značka“. V našem příkladu potřebujeme dvě značky: jednu pro název hlavního listu a druhou pro název detailního listu.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Tip** – Udržujte názvy značek krátké a výstižné; stanou se klíči, které použijete ve svém JSON payloadu.

## Příprava JSON dat (Krok 3)

Procesor pracuje s libovolným zdrojem dat, který lze reprezentovat jako JSON, `DataSet` nebo i prostý objekt. Zde je minimální JSON řetězec, který obsahuje kolekci master‑detail. Všimněte si, že každá objednávka obsahuje jak `MasterSheetName`, tak `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Proč JSON?* Je lehký, čitelný pro člověka a skvěle funguje s webovými API. Stejně tak můžete tato data získat z SQL dotazu a serializovat je pomocí `Newtonsoft.Json`.

## Inicializace SmartMarkerProcessor (Krok 4)

`SmartMarkerProcessor` je motor, který prohledá sešit, najde značky a provede svázání dat. Jeho vytvoření je jednorázová jedna řádka.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Definování dynamického pojmenování listů (Krok 5)

Zde **dynamic sheet naming excel** opravdu zazáří. Nastavením `DetailSheetNewName` říkáme procesoru, aby pro každou objednávku vytvořil nový detailní list a pojmenoval jej podle `OrderId`. Placeholder `${OrderId}` je během zpracování vyřešen z aktuálního záznamu.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Pozor** – Pokud zapomenete zahrnout syntaxi `${}`, list bude doslova pojmenován “Detail_${OrderId}” místo “Detail_1”, “Detail_2” atd.

## Aplikace JSON a generování listů (Krok 6)

Nyní necháme procesor udělat těžkou práci. Přečte JSON, nahradí značky a vytvoří nové listy podle potřeby.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Co se děje pod kapotou?

1. Procesor načte pole `Orders`.  
2. Pro každou objednávku vytvoří **hlavní list** (pomocí `${Orders.MasterSheetName}`) a **detailní list** (pomocí vzoru `DetailSheetNewName`).  
3. Hodnoty buněk jsou nahrazeny odpovídajícími JSON poli, takže první buňka hlavního listu skončí s “Master_1”, “Master_2” atd.  

## Uložení a ověření výsledku (volitelné)

Nakonec zapíšeme sešit na disk. Otevřete soubor v Excelu a měli byste vidět dva hlavní listy (`Master_1`, `Master_2`) a dva dynamicky pojmenované detailní listy (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Očekávaný výstup** – Po otevření `output.xlsx` uvidíte:

- List **Master_1** s buňkou A1 = “Master_1”.  
- List **Detail_1** s buňkou A1 = “Detail_1”.  
- List **Master_2** s buňkou A1 = “Master_2”.  
- List **Detail_2** s buňkou A1 = “Detail_2”.  

To je kompletní cyklus **jak používat značky** k dosažení **dynamic sheet naming excel** pomocí **Aspose.Cells smart markers**.

---

## Často kladené otázky a okrajové případy

### Co když potřebuji více než dvě úrovně hierarchie?

Můžete vnořit značky do nově vytvořených detailních listů. Stačí umístit další `${...}` značky do šablonového listu před zpracováním. Procesor automaticky projde každou úroveň.

### Můžu místo JSON použít DataTable?

Určitě. `SmartMarkerProcessor` má přetížení pro `DataSet`, `DataTable` i vlastní objekty. Jediná změna je volání `ApplyJson` – místo toho použijete `ApplyDataSet(myDataSet)`.

### Jak ovlivním pořadí vytváření listů?

Pořadí následuje sekvenci zdrojové kolekce. Pokud potřebujete vlastní řazení, jednoduše seřaďte JSON pole (nebo DataTable) před předáním procesoru.

### Existuje způsob, jak po zpracování skrýt šablonový list?

Ano. Nastavte `sm.Options.RemoveTemplateSheets = true;` před voláním `ApplyJson`. Původní list (index 0) bude z finálního sešitu odstraněn.

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní program, který můžete zkopírovat a vložit do nového C# konzolového projektu. Ujistěte se, že máte přidaný NuGet balíček `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Spusťte program, otevřete `output.xlsx` a uvidíte dynamické listy přesně tak, jak bylo popsáno výše.

---

## Závěr

Právě jsme prošli **jak používat značky** v Aspose.Cells k přeměně obyčejného sešitu na master‑detail řešení s **dynamic sheet naming excel**. Klíčové body jsou:

1. Umístěte `${...}` smart markers tam, kde chcete, aby se data objevila.  
2. Předávejte JSON (nebo jiný podporovaný zdroj) `SmartMarkerProcessoru`.  
3. Použijte `DetailSheetNewName`, aby procesor pojmenoval nové listy za běhu.  

Odtud můžete zkoumat pokročilejší scénáře – přidávat tabulky, stylovat buňky nebo dokonce vkládat grafy, vše řízené automaticky.

## Související tutoriály

- [Jak implementovat Aspose.Cells Smart Markers v C# pro dynamické Excel reportování](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Generování dynamických Excel reportů pomocí Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Mistrovství Aspose.Cells .NET: Implementace Smart Markers a vlastních štítků pro dynamické Excel reporty](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}