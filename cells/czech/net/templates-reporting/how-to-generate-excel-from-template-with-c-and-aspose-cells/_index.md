---
category: general
date: 2026-11-19
description: Naučte se rychle generovat Excel ze šablony v C#. Tento průvodce vám
  také ukáže, jak generovat Excelový report v C# pomocí Smart Markers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel from template
- generate excel report c#
- Aspose.Cells Smart Marker
- master‑detail Excel export
- C# Excel automation
language: cs
lastmod: 2026-11-19
og_description: Vytvořte Excel ze šablony v C# pomocí Aspose.Cells. Sledujte tento
  tutoriál, jak v C# generovat Excel report pomocí Smart Markers a master‑detail dat.
og_image_alt: Screenshot showing C# code that generates Excel from a template file
og_title: Vytvořte Excel ze šablony v C# – kompletní průvodce krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to generate Excel from template in C# quickly. This guide
    also shows you how to generate Excel report C# using Smart Markers.
  headline: How to generate Excel from template with C# and Aspose.Cells
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Jak generovat Excel ze šablony pomocí C# a Aspose.Cells
url: /cs/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generování Excelu ze šablony v C# – kompletní krok‑za‑krokem průvodce

Pokud potřebujete **generovat Excel ze šablony** v .NET projektu, tento tutoriál vám ukáže připravené řešení připravené k okamžitému spuštění. Pomocí Aspose.Cells Smart Markers můžete vyplnit předem navržený sešit daty master‑detail a vytvořit profesionální report, aniž byste museli psát jakékoli Excel‑specifické vzorce.

Také uvidíte, jak stejný přístup umožňuje **generovat Excel report C#** pro faktury, souhrny objednávek nebo jakoukoli hierarchickou datovou sadu. Na konci průvodce budete mít znovupoužitelnou metodu, která převádí soubor šablony na plně vyplněný sešit.

## Co tento tutoriál pokrývá

* Načtení existující šablony `.xlsx`, která již obsahuje zástupné symboly Smart Marker.  
* Příprava objektu master‑detail, který odpovídá hierarchii šablony.  
* Konfigurace `SmartMarkerProcessor` pro vytvoření samostatného listu detailu pro vnořené kolekce.  
* Zpracování listu a uložení výsledku jako nový soubor.  

Nejsou vyžadovány žádné externí služby – stačí knihovna Aspose.Cells pro .NET (bezplatná zkušební verze nebo licencovaná verze) a projekt .NET 6+.

---

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`) | Poskytuje `SmartMarkerProcessor` a API pro manipulaci s Excelem. |
| **.NET 6 SDK** nebo novější | Zajišťuje moderní jazykové funkce a kompatibilitu s nejnovější verzí Aspose.Cells. |
| **Šablona sešitu** (`template.xlsx`) s umístěnými Smart Markery v prvním listu | Smart Markery řídí vazbu dat; šablona definuje rozvržení, styly a statický obsah. |
| Základní znalost kolekcí C# a anonymních typů | Zdroj dat je vytvořen jako anonymní objekt, který odráží strukturu šablony. |

Šablonu můžete vytvořit v Excelu zadáním `&=Orders.Id` pro sloupec s ID objednávky a `&=Orders.Items.Name` pro vnořené položky. Předpona `&=` říká Smart Markers, aby buňku nahradily daty během běhu.

---

## Krok 1: Nastavení C# projektu a přidání Aspose.Cells

Vytvořte konzolovou aplikaci (nebo ji integrujte do existující služby) a přidejte NuGet balíček:

```bash
dotnet new console -n ExcelTemplateDemo
cd ExcelTemplateDemo
dotnet add package Aspose.Cells
```

> **Tip:** Použijte přepínač `--version` pro uzamčení na známou stabilní verzi, např. `Aspose.Cells 23.12`.

---

## Krok 2: Definice datového zdroje master‑detail

Datový zdroj musí odrážet hierarchii použitou v šabloně. V tomto příkladu máme objednávky (master), z nichž každá obsahuje kolekci položek (detail).

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };
```

**Proč to funguje:**  
*Anonymní typ* vám umožňuje rychle vytvořit reprezentaci v paměti bez definování explicitních POCO tříd. Každý `Order` má `Id` a pole `Items`, což odpovídá značkám `&=Orders.Id` a `&=Orders.Items.Name` v šabloně.

---

## Krok 3: Načtení Excel šablony, která obsahuje Smart Markery

```csharp
            // Step 3: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

**Vysvětlení:**  
`Workbook` načte soubor `.xlsx` do paměti. Šablona by již měla mít syntaxi Smart Marker (`&=Orders.Id`, `&=Orders.Items.Name`, atd.) umístěnou tam, kde chcete, aby se data objevila.

---

## Krok 4: Získání listu, kde jsou umístěny Smart Markery

```csharp
            // Step 4: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];   // first sheet (index 0)
```

**Proč první list?**  
Většina šablon udržuje hlavní tabulku na prvním listu, ale můžete odkazovat na libovolný list podle názvu (`workbook.Worksheets["SheetName"]`), pokud se váš návrh liší.

---

## Krok 5: Konfigurace procesoru SmartMarker

`SmartMarkerProcessor` zajišťuje těžkou práci. Nastavením `DetailSheetNewName` instruujeme Aspose.Cells, aby vytvořil nový list pro každou vnořenou kolekci.

```csharp
            // Step 5: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";
```

**Co to dělá:**  
Když procesor narazí na kolekci uvnitř kolekce (pole `Items`), vytvoří nový list s názvem `OrderDetails` a vyplní jej souvisejícími řádky. To udržuje hlavní list přehledný a napodobuje typické rozložení reportu master‑detail.

---

## Krok 6: Zpracování listu pomocí datového zdroje

```csharp
            // Step 6: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);
```

Metoda `Process` nahradí každý Smart Marker odpovídající hodnotou z `orderData`. Také rozšíří řádky podle potřeby, takže nemusíte předem alokovat místo v šabloně.

---

## Krok 7: Uložení vyplněného sešitu

```csharp
            // Step 7: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Výsledek:**  
- `masterDetail.xlsx` obsahuje hlavní list s ID objednávek.  
- Nový list `OrderDetails` obsahuje názvy položek pro každou objednávku.  
- Veškeré formátování (písma, ohraničení, šířky sloupců) ze šablony je zachováno.

Soubor můžete otevřít v Excelu a ověřit, že data odpovídají zdrojovému objektu.

---

## Kompletní zdrojový kód (připravený ke kopírování)

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };

            // Step 2: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Step 3: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 4: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";

            // Step 5: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);

            // Step 6: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Očekávaný výstup v Excelu**

| **Objednávky** (hlavní list) |
|---|
| Id |
| 1 |
| 2 |

*OrderDetails* list:

| **Položky** |
|---|
| Název |
| A |
| B |
| C |

Řádky jsou automaticky přidávány tak, aby odpovídaly počtu položek na objednávku.

---

## Běžné varianty a okrajové případy

| Situace | Jak upravit kód |
|-----------|-----------------------|
| **Více úrovní detailu** (např. Orders → Items → SubItems) | Přidejte další vlastnost kolekce (`SubItems`) a nastavte `DetailSheetNewName` na jinou hodnotu pro každou úroveň. Aspose.Cells automaticky vytvoří další listy. |
| **Vlastní pojmenování listu pro každý hlavní záznam** | Použijte `smartMarkerProcessor.Options.DetailSheetNameFromData = true;` a zahrňte pole `SheetName` v hlavní kolekci. |
| **Velké datové sady (10 000+ řádků)** | Zavolejte `workbook.Settings.MemorySetting = MemorySetting.MemoryOptimized;` před načtením šablony pro snížení spotřeby paměti. |
| **Šablona bez detailního listu** (plochý report) | Vynechte `DetailSheetNewName`; procesor zapíše vnořená data přímo do hlavního listu a rozšíří řádky podle potřeby. |
| **Spuštění v ASP.NET Core** | Nahraďte `Console.WriteLine` logováním (`ILogger`) a použijte `Path.Combine` pro určení umístění souborů relativně k `wwwroot`. |

---

## Tipy pro spolehlivé generování Excelu

* **Uchovávejte zástupné symboly v samostatném řádku** – Smart Markery rozšiřují řádky pod značkou; umístění do řádku záhlaví zachovává formátování.  
* **Vyhněte se slučování buněk v datové oblasti** – Sloučené buňky mohou způsobit neočekávané posuny řádků během rozšiřování.  
* **Testujte s minimální datovou sadou** nejprve; jakmile rozvržení funguje, přejděte na reálná data.  
* **Uzamčení verze** – Zaznamenejte verzi Aspose.Cells, kterou jste použili (`Aspose.Cells 23.12`), abyste se vyhnuli breaking changes při aktualizaci.  

---

## Závěr

Nyní víte, jak **generovat Excel ze šablony** v C# pomocí Aspose.Cells Smart Markers, a můžete snadno rozšířit stejný vzor na **generování Excel reportu C#** pro jakýkoli scénář master‑detail. Přístup odděluje rozvržení (šablonu) od dat (objekt C#), což vám poskytuje udržovatelný, znovupoužitelný reportingový engine.

Dále prozkoumejte tato související témata:

* **Styling cells programmatically** – naučte se, jak aplikovat podmíněné formátování po naplnění dat.  
* **Exporting to PDF** – Aspose.Cells může převést vygenerovaný sešit do PDF jedním voláním.  
* **Integrating with ASP.NET Core** – streamujte vygenerovaný soubor přímo do prohlížeče bez zápisu na disk.

Vyzkoušejte kód, upravte šablonu tak, aby odpovídala vaší značce, a nechte generované Excel reporty stát se jádrem vašich .NET aplikací. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak generovat Excel report sloučením Excel šablony se Smart Markers](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/)
- [Jak generovat Excel report v C# – kompletní průvodce s použitím SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)
- [Aspose Cells Smart Markers: Generování Excelu z modelu v C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}