---
category: general
date: 2026-09-15
description: Vytvořte sešit Excel v C# a naučte se, jak uložit sešit jako PDF při
  rozšiřování dynamických polí pomocí funkce EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: cs
lastmod: 2026-09-15
og_description: Vytvořte sešit Excel v C# a rychle jej uložte jako PDF při použití
  funkce EXPAND k rozšíření dynamického pole.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Vytvořte sešit v Excelu a uložte jej jako PDF s dynamickými poli
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Vytvořte sešit Excel a uložte jej jako PDF s dynamickými poli
url: /cs/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření sešitu Excel a uložení jako PDF s dynamickými poli

Pokud potřebujete **programově vytvořit sešit Excel** a poté **uložit sešit jako PDF**, tento průvodce vám ukáže kompletní řešení od začátku do konce v C#. Také uvidíte, jak **rozšířit výsledky dynamického pole** pomocí **funkce EXPAND**, což je moderní způsob generování polí bez VBA.  

Ať už budujete reportingovou službu, exportní funkci pro ERP systém nebo datově řízený dashboard, níže uvedené kroky vám umožní vygenerovat sešit, naplnit jej daty Smart‑Marker a vytvořit PDF, které zachová pokročilé typografické funkce.

## Předpoklady

Než začnete, ujistěte se, že máte:

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.8)
* Aktuální verzi **Aspose.Cells for .NET** (v25.8 nebo novější) – poskytuje `Workbook`, `PdfSaveOptions` a `SmartMarkerProcessor`.
* IDE, například Visual Studio 2022 (libovolný editor, který dokáže kompilovat C#).

Přidejte NuGet balíček do svého projektu:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Krok 1: Vytvoření sešitu Excel a nastavení první listu

Prvním úkolem je **vytvořit sešit Excel** a získat odkaz na výchozí list. Tento list bude hostit dynamické pole a šablonu Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Proč je to důležité*: Instancování `Workbook` alokuje interní strukturu sešitu, zatímco přístup k `Worksheets[0]` vám poskytne připravený list bez nutnosti jej ručně přidávat.

## Krok 2: Rozšíření dynamického pole pomocí funkce EXPAND

**Funkce EXPAND** v Excelu dokáže převést statický literál pole na rozšířený rozsah libovolné velikosti. Zde požádáme Excel, aby rozšířil `{1,2,3}` na rozsah 5 řádků × 1 sloupce začínající v `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Proč je to důležité*: Použití `EXPAND` eliminuje potřebu ručních smyček v C#. Engine vypočítá rozšířený rozsah a uloží hodnoty přímo do listu, což se později projeví v PDF.

## Krok 3: Uložení sešitu jako PDF se zachováním selektorů variací fontu

Když potřebujete **uložit sešit jako PDF**, můžete také povolit pokročilé typografické funkce, jako jsou selektory variací fontu (k dispozici od Aspose.Cells v25.8). To zajišťuje správné vykreslení složitých skriptů v PDF.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Proč je to důležité*: Nastavení `FontVariationSelectors` na `true` je nezbytné pro jazyky, které spoléhají na variace glyfů (např. čínština, japonština, emoji). Vytvořené PDF odráží přesně to, co vidíte v Excelu.

## Krok 4: Vložení šablony Smart Marker, která odkazuje na vnořený zdroj dat

Smart Markery vám umožňují vkládat zástupné symboly přímo do listu. Šablona níže vygeneruje seznam objednávek a jejich položek.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Proč je to důležité*: Umístěním šablony do `A1` říkáte Aspose.Cells, kde má začít rozšiřování dat. Syntaxe `:` (`Items:ItemName`) říká procesoru, aby iteroval přes vnořenou kolekci.

## Krok 5: Definice vnořeného zdroje dat (objednávky obsahující položky)

Vytvoříme anonymní pole objednávek, z nichž každá obsahuje vlastní kolekci objektů položek. To odráží typický scénář master‑detail.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Proč je to důležité*: Vnořená struktura demonstruje **jak vytvořit dynamické pole v Excelu** pomocí Smart Markerů, bez psaní VBA nebo ručních smyček v buňkách.

## Krok 6: Zpracování Smart Markerů a uložení finálního souboru Excel

Nyní předáme sešit a zdroj dat `SmartMarkerProcessor`. Po zpracování jsou zástupné symboly nahrazeny skutečnými řádky a výsledek uložíme jako běžný soubor `.xlsx`.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Proč je to důležité*: `SmartMarkerProcessor` automaticky rozšíří šablonu, vytvoří potřebné řádky a naplní je daty. Finální sešit lze otevřít v Excelu a ověřit, že každá objednávka a její položky jsou správně zobrazeny.

## Očekávaný výstup

* **VarSelector.pdf** – PDF soubor, který zobrazuje čísla 1‑3 rozšířená do pěti řádků, vykreslená s jakýmikoli OpenType variacemi fontu, které jste povolili.
* **NestedSmartMarker.xlsx** – Excel soubor s následujícími řádky (začínající v `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

Verze PDF zachovává stejný číselný spill, protože stav listu byl uložen před zpracováním Smart Marker; můžete PDF uložit i po zpracování, pokud potřebujete finální data v PDF.

## Praktické tipy a časté úskalí

| Tip | Vysvětlení |
|-----|------------|
| **Znovu použijte stejný `PdfSaveOptions`** | Vytvoření objektu možností jednou a jeho opakované použití eliminuje drobné rozdíly v renderování (např. chybějící selektory variací). |
| **Volání `ws.Calculate()` po nastavení vzorců** | Bez explicitního výpočtu může být rozšířený rozsah prázdný při programové inspekci sešitu. |
| **Umístěte šablony Smart Marker na čistý list** | Míchání šablon s existujícími daty může způsobit neočekávané vkládání řádků. Použijte vyhrazený list, pokud je to možné. |
| **Dávejte pozor na cesty k souborům** | Použijte `Path.Combine(Environment.CurrentDirectory, "output.pdf")`, abyste se vyhnuli pevně zakódovaným adresářům na různých počítačích. |
| **Kontrola verze** | `FontVariationSelectors` je k dispozici až od verze 25.8; starší verze tuto vlastnost ignorují bez vyhození výjimky. |

## Další kroky

Nyní, když už víte, jak **vytvořit sešit Excel**, **rozšířit dynamické pole** a **uložit sešit jako PDF**, můžete zkusit:

* Přidat grafy nebo obrázky před konverzí do PDF.
* Exportovat stejný sešit do jiných formátů (např. HTML, CSV) pomocí přetížených metod `Save`.
* Použít **výrazy Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) pro výpočet agregací za běhu.
* Integrovat tento kód do ASP.NET Core API, aby si uživatelé mohli stáhnout vygenerované PDF přímo z webového endpointu.

---

**Shrnutí** – Tento tutoriál vám ukázal, jak **vytvořit sešit Excel**, použít **funkci EXPAND** k **rozšíření dynamického pole**, vložit **Smart Marker**, který pracuje s vnořeným zdrojem dat, a nakonec **uložit sešit jako PDF** se zachováním pokročilých typografických funkcí. Kompletní, spustitelný příklad můžete zkopírovat do libovolného C# projektu a přizpůsobit svým vlastním datovým strukturám. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}