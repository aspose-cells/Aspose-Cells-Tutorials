---
category: general
date: 2026-10-10
description: Převod JSON do XLSX v C# s pomocí SmartMarker – naučte se, jak importovat
  JSON do Excelu a programově naplnit sešit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: cs
lastmod: 2026-10-10
og_description: Převod JSON do XLSX v C# pomocí SmartMarker. Postupujte podle tohoto
  průvodce, jak importovat JSON do Excelu, vytvořit Excel sešit v C# a naplnit Excel
  z JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Převod JSON do XLSX v C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Převod JSON do XLSX v C# pomocí SmartMarker
url: /cs/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod JSON do XLSX v C# pomocí SmartMarker

Pokud potřebujete **převést JSON do XLSX v C#**, tento průvodce vám ukáže, jak **importovat JSON do Excelu** a **naplnit Excel z JSON** pomocí několika řádků kódu. Uvidíte, jak **vytvořit Excel sešit v C#**, nakonfigurovat procesor SmartMarker a nakonec **importovat JSON do buněk listu**.

> **Co získáte** – plně spustitelný příklad, který načte pole JSON, zachází s ním jako s jedním záznamem a zapíše data do souboru `.xlsx` připraveného pro následné reportování nebo analýzu.

## Převod JSON do XLSX – přehled

SmartMarker je součástí knihovny Aspose.Cells a umožňuje vám vázat JSON, XML nebo jakýkoli .NET objekt přímo na šablonu Excelu. V tomto tutoriálu:

1. **Vytvořit Excel sešit** v paměti.
2. **Načíst JSON data**, která představují jednoduchý seznam lidí.
3. **Konfigurovat SmartMarker**, aby zacházel s polem JSON jako s jedním záznamem (`ArrayAsSingle = true`).
4. **Zpracovat list**, nechat SmartMarker nahradit značky hodnotami z JSON.
5. **Uložit sešit** jako soubor `.xlsx`.

Celý proces běží na .NET 6+ a vyžaduje pouze balíček `Aspose.Cells` z NuGet.

## Krok 1: Vytvořit Excel sešit v C#

Nejprve přidejte balíček Aspose.Cells do svého projektu:

```bash
dotnet add package Aspose.Cells
```

Nyní můžete vytvořit novou instanci `Workbook`. Sešit začíná prázdný, ale můžete přidat list a umístit značky SmartMarker tam, kde by se měla objevit data z JSON.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Proč nejprve vytváříme sešit** – SmartMarker pracuje s existujícím objektem `Worksheet`; sešit poskytuje kontejner pro všechny následné operace.

## Krok 2: Definovat JSON data a konfigurovat SmartMarker

Použijeme malý JSON payload, který uvádí dva lidi. Volba `ArrayAsSingle` říká SmartMarkeru, aby zacházel s celým polem jako s jedním logickým záznamem, což je ideální, když chcete jednoduchou tabulku bez vnořených smyček.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **Tip:** Pokud vynecháte `ArrayAsSingle`, SmartMarker se pokusí vytvořit samostatný záznam pro každý prvek pole, což může vést k duplicitním řádkům nebo neočekávanému rozložení.

## Krok 3: Vložit značky SmartMarker do listu

Značky SmartMarker jsou prosté textové zástupce obklopené `&`. Umístěte je do buněk, kde chcete, aby se objevily hodnoty z JSON. V tomto příkladu zapisujeme značky přímo pomocí kódu, ale můžete také nejprve navrhnout šablonu v Excelu.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **Vysvětlení:** `&=Name&` říká SmartMarkeru, aby nahradil buňku polem `Name` z JSON objektu, zatímco `&=Age&` dělá totéž pro `Age`.

## Krok 4: Zpracovat list – naplnit Excel z JSON

Nechte nyní SmartMarker přečíst řetězec JSON a vyplnit zástupce.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

Za scénou SmartMarker parsuje `jsonData`, mapuje každou vlastnost objektu na odpovídající značku a automaticky rozšiřuje řádky, protože `ArrayAsSingle` je `true`. Po zpracování list vypadá takto:

| Jméno | Věk |
|------|-----|
| John | 30  |
| Anna | 25  |

## Krok 5: Uložit soubor XLSX

Nakonec zapište naplněný sešit na disk.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Spuštěním programu se na ploše vytvoří `SmartMarkerJson.xlsx`. Otevření souboru v Excelu zobrazí čistou tabulku s JSON daty správně importovanými.

## Časté úskalí při importu JSON do listu

| Problém | Proč k tomu dochází | Jak tomu předejít |
|---------|----------------------|-------------------|
| **Chybějící značky SmartMarker** | SmartMarker nahrazuje pouze buňky, které obsahují `&=...&`. | Dvakrát zkontrolujte přesné pravopis a velikost písmen značky. |
| **Nesprávný formát JSON** | Jednoduché uvozovky (`'`) nejsou platným JSON pro vestavěný parser. | Použijte dvojité uvozovky (`"`) nebo nechte Aspose.Cells zpracovat uvolněný formát, jak je ukázáno. |
| **Pole je považováno za více záznamů** | Výchozí hodnota `ArrayAsSingle` je `false`. | Nastavte `processor.Options.ArrayAsSingle = true`, pokud chcete plochou tabulku. |
| **Ukládání do složky jen pro čtení** | `workbook.Save` vyvolá výjimku. | Vyberte zapisovatelný adresář (např. Plocha nebo dočasná složka). |

## Rozšíření řešení

- **Více listů:** Vytvořte další listy a zavolejte `processor.Process` na každém s různými JSON zdroji.
- **Styling:** Po zpracování aplikujte styly buněk (písma, okraje) stejně jako u jakékoli běžné operace Aspose.Cells.
- **Velké datové sady:** Pro tisíce řádků zvažte streamování sešitu pro snížení spotřeby paměti (`WorkbookDesigner` nebo `SaveOptions` s `EnableMemoryOptimization`).

## Závěr

Nyní víte, jak **převést JSON do XLSX v C#** pomocí Aspose.Cells SmartMarker. Kompletní pracovní postup – **vytvořit Excel sešit v C#**, přidat značky SmartMarker, nakonfigurovat procesor, **naplnit Excel z JSON** a uložit soubor – vám umožní **importovat JSON do buněk listu** s minimálním množstvím kódu.

Neváhejte experimentovat s komplexnějšími strukturami JSON, přidávat vzorce nebo generovat grafy přímo z naplněných dat. Pokud se vám tento průvodce líbil, vyzkoušejte další tutoriál o **tom, jak importovat JSON do Excelu** pro tvorbu grafů nebo o **vytvoření Excel sešitu v C#** s pokročilým formátováním.

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převod JSON do Excelu s C# – krok za krokem průvodce](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Jak vložit JSON do šablony Excel – krok za krokem](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Vytvořit Excel sešit v C# – vložit JSON a uložit jako XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}