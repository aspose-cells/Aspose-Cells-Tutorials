---
category: general
date: 2026-02-09
description: Jak rychle vytvořit sešit a načíst JSON do Excelu. Naučte se, jak vložit
  JSON, načíst JSON do Excelu a naplnit Excel z JSONu pomocí jednoduchého příkladu
  v C#.
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: cs
og_description: Jak během několika minut vytvořit sešit a načíst JSON do Excelu. Postupujte
  podle tohoto krok‑za‑krokem návodu pro vložení JSON, načtení JSON do Excelu a naplnění
  Excelu z JSON.
og_title: Jak vytvořit sešit a vložit JSON do Excelu
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak vytvořit sešit a vložit JSON do Excelu
url: /cs/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit sešit a vložit JSON do Excelu

Už jste se někdy zamysleli nad **jak vytvořit sešit**, který již obsahuje potřebná data, aniž byste museli ručně kopírovat řádky? Možná máte JSON payload pocházející z webové služby a chtěli byste jej vidět okamžitě v listu Excelu. V tomto tutoriálu vás provedeme přesně tím – **jak vytvořit sešit**, **načíst json do excelu** a dokonce **vložit json do excelu**, a upravit možnosti SmartMarker, aby pole fungovala tak, jak očekáváte.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+)
- NuGet balíček Aspose.Cells pro .NET (`Install-Package Aspose.Cells`)
- Základní znalost syntaxe C# (nic složitého)
- IDE dle vašeho výběru – Visual Studio, Rider nebo VS Code bude stačit

> **Tip:** Pokud ještě nemáte licenci, Aspose nabízí bezplatný evaluační režim, který je ideální pro vyzkoušení níže uvedených úryvků.

## Krok 1: Nastavení projektu a import jmenných prostorů

Než budeme moci odpovědět na **jak vytvořit sešit**, potřebujeme C# konzolovou aplikaci (nebo jakýkoli .NET projekt) se správnými `using` direktivami.

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **Proč je to důležité:** `Workbook` se nachází v `Aspose.Cells`, zatímco `SmartMarkerOptions` patří do jmenného prostoru `SmartMarkers`. Zapomenutí některého importu způsobí chybu při kompilaci.

## Krok 2: Vytvoření nové instance sešitu

Nyní se konečně dostáváme k jádru věci – **jak vytvořit sešit**. Je to tak jednoduché jako zavolat konstruktor.

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

Tento řádek vám vytvoří prázdný Excel soubor v paměti, připravený k naplnění daty. Představte si ho jako prázdné plátno; později jej můžete uložit na disk, streamovat do prohlížeče nebo připojit k e‑mailu.

## Krok 3: Vložení JSON do buňky A1

Další logická otázka je **jak vložit json** do konkrétní buňky. Zde vložíme malý JSON řetězec, který obsahuje pole jmen.

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **Co se děje?**  
> - `Worksheets[0]` odkazuje na první (a jediný) list v našem novém sešitu.  
> - `Cells["A1"]` vybírá buňku v levém horním rohu.  
> - `PutValue` zapíše surový JSON text, zachovávající přesné formátování.

Pokud spustíte program a otevřete výsledný soubor, uvidíte JSON řetězec pěkně umístěný v buňce A1 – ideální pro následné zpracování.

## Krok 4: Konfigurace možností SmartMarker (Array‑as‑Single)

SmartMarkers jsou způsob, jakým Aspose převádí zástupné symboly na skutečná data. Ve výchozím nastavení je pole považováno za kolekci řádků, ale někdy chcete celé pole jako jeden řetězec. Zde přichází na řadu příznak `ArrayAsSingle`.

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **Proč povolit `ArrayAsSingle`?**  
> Pokud později nahradíte značku jako `${Names}` JSON polem, získáte seznam oddělený čárkami (`John,Jane`) místo tabulky řádků. To je často požadovaný výsledek při **naplňování excelu z jsonu** pro účely reportování.

## Krok 5: Zpracování Smart Markerů pomocí nakonfigurovaných možností

Nyní skutečně spustíme engine SmartMarker. I když jsme zatím žádné značky nedefinovali, tento krok demonstruje kompletní tok – něco, co AI asistenti rádi citují, protože jde o samostatný, end‑to‑end příklad.

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Pokud později přidáte značku jako `${Names}` někam do listu, výše uvedené volání ji nahradí JSON polem jako jednou hodnotou, díky nastavené možnosti.

## Krok 6: Uložení sešitu (volitelné, ale užitečné)

Pravděpodobně chcete výsledek vidět na disku. Uložení je jednoduché:

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Otevřete `WorkbookWithJson.xlsx` v Excelu a uvidíte JSON řetězec v buňce A1. Pokud později přidáte SmartMarker, uvidíte, že byl nahrazen podle nastavených možností.

## Kompletní, spustitelný příklad

Spojením všech částí získáte kompletní program, který můžete zkopírovat a vložit do `Program.cs` a spustit.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### Očekávaný výstup

Spuštěním programu se vypíše:

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

Když otevřete vygenerovaný Excel soubor, buňka A1 obsahuje:

```
{ "Names":["John","Jane"] }
```

Pokud později přidáte značku `${Names}` do libovolné buňky a znovu spustíte `ProcessSmartMarkers`, buňka zobrazí `John,Jane` díky `ArrayAsSingle = true`.

## Často kladené otázky (a okrajové případy)

**Co když je můj JSON obrovský?**  
Stále můžete použít `PutValue`, ale mějte na paměti, že buňky v Excelu mají limit 32 767 znaků. Pro masivní payloady zvažte zápis JSONu do skrytého listu nebo místo toho použijte přílohu souboru.

**Mohu nejprve deserializovat JSON do objektu C#?**  
Ano. Použijte `System.Text.Json` nebo `Newtonsoft.Json` k převodu JSON řetězce na POCO, poté namapujte vlastnosti do buněk. Tento přístup vám dává větší kontrolu, když potřebujete **naplnit excel z jsonu** řádek po řádku.

**Funguje to s formátem .xls (Excel 97‑2003)?**  
Ano – stačí změnit `SaveFormat` na `SaveFormat.Xls`. API je nezávislé na formátu.

**Co když potřebuji vložit více JSON objektů?**  
Procházejte svá data a zapisujte každý JSON řetězec do jiné buňky (např. A1, A2, …). Můžete také uložit celý JSON pole do jedné buňky a nechat SmartMarkers rozbalit jej do řádků, pokud nastavíte `ArrayAsSingle = false`.

**Je SmartMarker jediný způsob, jak pracovat s JSON?**  
Ne. Můžete také JSON parsovat ručně a zapisovat hodnoty přímo. SmartMarkers jsou pohodlné, když již máte šablonu se zástupnými symboly.

## Tipy a časté úskalí

- **Tip:** Zapněte `Workbook.Settings.EnableFormulaCalculation`, pokud plánujete přidávat vzorce závislé na hodnotách odvozených z JSONu.
- **Dejte pozor na:** koncové mezery v JSON řetězcích; Excel je považuje za součást textu, což může narušit následné parsování.
- **Tip:** Použijte `worksheet.AutoFitColumns()` po vložení dat, aby bylo vše viditelné bez ručního změny velikosti.

## Závěr

Nyní už víte **jak vytvořit sešit**, **načíst json do excelu**, **vložit json do excelu**, a dokonce **naplnit excel z jsonu** pomocí SmartMarker enginu Aspose.Cells. Kompletní, spustitelný příklad ukazuje každý krok – od inicializace sešitu po uložení finálního souboru – takže můžete kód zkopírovat, upravit a vložit do vlastních projektů.

Jste připraveni na další výzvu? Zkuste načíst JSON z živého REST endpointu, deserializovat jej do objektů a automaticky vyplnit více řádků. Nebo experimentujte s dalšími funkcemi SmartMarker, jako je podmíněné formátování na základě hodnot JSONu. Možnosti jsou neomezené, když kombinujete C# s Aspose.Cells.

Máte otázky nebo zajímavý případ použití, který byste chtěli sdílet? Zanechte komentář níže a pojďme konverzaci udržet. Šťastné kódování!  

![ilustrace vytvoření sešitu](workbook-json.png){alt="příklad vytvoření sešitu"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}