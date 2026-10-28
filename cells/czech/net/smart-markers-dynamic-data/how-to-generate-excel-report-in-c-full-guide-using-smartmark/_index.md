---
category: general
date: 2026-03-22
description: Jak vygenerovat Excel report v C# s šablonou master‑detail. Naučte se
  rychle naplnit Excel šablonu v C# pomocí SmartMarkeru pro opakovatelná listy.
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: cs
og_description: Jak generovat Excel report v C# pomocí znovupoužitelné šablony. Tento
  krok‑za‑krokem průvodce vám ukáže, jak naplnit Excel šablonu v C# hlavní‑detailními
  daty.
og_title: Jak generovat Excel report v C# – Kompletní tutoriál SmartMarker
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: Jak vygenerovat Excel report v C# – Kompletní průvodce s použitím SmartMarker
url: /cs/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vygenerovat Excel report v C# – Kompletní průvodce s použitím SmartMarker

Už jste se někdy zamýšleli **jak vygenerovat Excel report** v C# bez psaní nekonečného kódu buňka‑po‑buňce? Nejste v tom sami. Většina vývojářů narazí na problém, když potřebují vylepšený, více‑listový report, který odráží vztahy master‑detail – například objednávky a položky – a nechtějí pokaždé znovu vymýšlet kolo.

Dobrá zpráva? S připravenou Excel šablonou a **SmartMarker** enginem od Aspose.Cells můžete **populate Excel template C#** během několika řádků kódu. V tomto tutoriálu projdeme reálný scénář, vysvětlíme, proč je každý krok důležitý, a poskytneme kompletní, spustitelný příklad, který můžete dnes zkopírovat‑vložit.

> **Co získáte:** master‑detail Excel report, kde každá objednávka vytvoří svůj vlastní list, vše řízené čistými C# objekty. Žádné ruční procházení buněk, žádné křehké vzorce – jen čistý, udržovatelný kód.

---

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- **.NET 6.0** (nebo novější) nainstalovaný – kód cílí na .NET 6, ale funguje i na .NET Framework 4.7+.
- **Aspose.Cells for .NET** NuGet balíček (`Install-Package Aspose.Cells`) – poskytuje třídy `Workbook`, `SmartMarkerProcessor` a související.
- Excel soubor pojmenovaný **MasterDetailTemplate.xlsx** umístěný v `YOUR_DIRECTORY`. Měl by obsahovat SmartMarker blok jako `{{Orders.OrderId}}` v prvním listu a vnořený blok `{{Orders.Items.Prod}}` pro položky.
- Základní povědomí o anonymních typech v C# – použijeme je k modelování objednávek a položek.

Pokud vám některý z těchto bodů není známý, nebojte se. Později zmíníme alternativy (např. pomocí EPPlus), ale základní koncept zůstává stejný.

---

## Krok 1: Načtení Excel šablony obsahující SmartMarker bloky

Prvním krokem je otevřít soubor šablony. Šablonu si představte jako kostru; SmartMarker ji později naplní skutečnými daty.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Proč je to důležité:** Oddělením rozvržení (šablony) od dat (C# objektů) uspokojíte jak designéry, tak vývojáře. Designéři mohou měnit písma, barvy nebo vzorce, aniž by zasahovali do kódu.

---

## Krok 2: Vytvoření master‑detail datového zdroje

Dále vytvoříme data, která šablonu naplní. Pro typický report objednávek máte kolekci objednávek, z nichž každá obsahuje vlastní kolekci položek.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **Tip:** Použijte silně typované třídy místo anonymních typů, pokud potřebujete opakované použití napříč více reporty. Anonymní přístup udržuje příklad stručný.

**Proč je to důležité:** SmartMarker funguje tak, že porovnává názvy vlastností (`Orders`, `OrderId`, `Items`, `Prod`, `Qty`) s placeholdery v šabloně. Hierarchie se musí přesně shodovat, jinak engine tyto sekce přeskočí.

---

## Krok 3: Řekněte SmartMarkeru, aby vytvořil nový list pro každý master záznam

Ve výchozím nastavení SmartMarker zapisuje všechny řádky do jednoho listu. My chceme, aby každá objednávka měla svůj vlastní list, což je ideální pro tisk nebo pozdější e‑mailování PDF per‑order.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**Proč je to důležité:** `EnableRepeatingSheet` eliminuje potřebu ručního klonování listů. Engine zkopíruje původní list, vloží data objednávky a automaticky přejmenuje list (obvykle podle hodnoty v první buňce).

---

## Krok 4: Zpracování šablony s vašimi daty

Nyní vše spojíme. `SmartMarkerProcessor` prochází sešitem, nahrazuje tagy a vytváří nové listy podle instrukcí.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**Proč je to důležité:** Tento jediný řádek provádí těžkou práci – parsování šablony, iteraci přes kolekce a zpracování vnořených tabulek. Je to jádro **populate Excel template C#** bez jakýchkoli ručních smyček.

---

## Krok 5: Uložení hotového reportu

Nakonec zapíšeme naplněný sešit na disk. Můžete ho také přímo streamovat do HTTP odpovědi pro webové aplikace.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**Proč je to důležité:** Uložení do souboru vám poskytne konkrétní artefakt, který můžete otevřít v Excelu, sdílet se stakeholdery nebo předat dalším procesům, jako je konverze do PDF.

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je celý program, včetně `using` direktiv a metody `Main`. Vložte jej do konzolové aplikace, upravte cesty k souborům a spusťte.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### Očekávaný výstup

Po otevření `MasterDetailResult.xlsx` uvidíte:

- **List “Order_1”** – obsahuje hlavičku objednávky 1 a dva řádky pro produkty A a B.
- **List “Order_2”** – obsahuje hlavičku objednávky 2 a jeden řádek pro produkt C.
- Všechny vzorce, formátování a grafy z původní šablony jsou zachovány.

![Excel report with separate sheets for each order – example of populated workbook](/images/excel-report-example.png "Generated Excel report with master‑detail data")

*Alt text obrázku: vygenerovaný Excel report s oddělenými listy pro každou objednávku, ukazující, jak generovat Excel report pomocí C# a SmartMarker.*

---

## Často kladené otázky a okrajové případy

### Co když potřebuji statický list (např. souhrn) vedle opakujících se listů?

Nastavte `EnableRepeatingSheet = true` **pouze** na listu, který obsahuje master blok. Ostatní listy zůstanou nedotčeny, takže můžete v původní šabloně zachovat souhrnnou stránku.

### Můžu místo anonymních objektů použít DataTable?

Určitě. SmartMarker funguje s libovolným objektem, který implementuje `IEnumerable`. Stačí nahradit anonymní typ `DataTable` a zajistit, aby názvy sloupců odpovídaly tagům.

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### Jak změním pojmenování generovaných listů?

Implementujte vlastní rozhraní `ISmartMarkerSheetNaming` (nebo manipulujte s `workbook.Worksheets` po zpracování). Většina vývojářů jednoduše přejmenuje listy podle hodnoty buňky:

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### Co když moje šablona používá jinou syntaxi placeholderů?

SmartMarker umožňuje vlastní oddělovače pomocí `SmartMarkerOptions`. Například pro použití `<< >>` místo `{{ }}`:

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

---

## Tipy pro škálování tohoto přístupu

- **Cacheujte šablonu** v paměti, pokud generujete mnoho reportů na požádání; načítání z disku při každém požadavku zvyšuje latenci.
- **Kombinujte s konverzí do PDF** (`workbook.Save("report.pdf", SaveFormat.Pdf)`) pro výstupy vhodné k e‑mailu.
- **Parametrizujte cesty k souborům** pomocí konfiguračních souborů nebo proměnných prostředí, aby byla řešení přenosná mezi vývojovým, testovacím a produkčním prostředím.
- **Jednotkově testujte datovou vrstvu** odděleně; SmartMarker je deterministický, takže stačí ověřit, že data, která předáváte, odpovídají očekávanému schématu.

---

## Závěr

Probrali jsme **jak vygenerovat Excel report** v C# od načtení šablony s podporou SmartMarker až po uložení více‑listového sešitu, který odráží master‑detail vztahy. Díky **populate Excel template C#** s několika řádky kódu se vyhnete křehké logice buňka‑po‑buňce a umožníte designérům svobodu při tvorbě finálního vzhledu.

Dále můžete zkusit:

- Použít **populate Excel template C#** s grafy, které se automaticky aktualizují na každém listu.
- Integrovat **excel smartmarker c#** s ASP.NET Core pro streamování reportů přímo do prohlížeče.
- Automatizovat **c# excel automation** pipeline, která tahá data z API nebo databází.

Vyzkoušejte to, upravte šablonu a sledujte, jak rychle můžete proměnit surová data v elegantní Excel report. Máte otázky nebo zajímavý případ použití? Zanechte komentář níže – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}