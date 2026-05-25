---
category: general
date: 2026-05-04
description: Exportujte oblast listu pomocí C# s vlastním formátováním. Naučte se,
  jak exportovat oblast v Excelu a jak přizpůsobit export buněk během několika jednoduchých
  kroků.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: cs
og_description: Exportujte oblast listu pomocí C#. Tento průvodce ukazuje, jak rychle
  a spolehlivě exportovat oblast Excelu a přizpůsobit export buněk.
og_title: Export rozsahu listu v C# – Kompletní programovací průvodce
tags:
- C#
- Excel
- Data Export
title: Export rozsahu listu v C# – kompletní programovací průvodce
url: /cs/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export rozsahu listu v C# – Kompletní programovací průvodce

Už jste někdy potřebovali **exportovat rozsah listu**, ale výchozí výstup nebyl tím, co jste chtěli? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku, když se snaží převést blok buněk do CSV nebo JSON souboru. Dobrá zpráva? Několika řádky C# můžete nejen **exportovat excel rozsah**, ale také **přizpůsobit export buněk** tak, aby odpovídal libovolnému následnému formátu.

V tomto tutoriálu projdeme reálný scénář: vezmeme buňky *A1:D10* z Excel sešitu, převedeme každou hodnotu na řetězec v hranatých závorkách a zapíšeme výsledek do souboru. Na konci budete přesně vědět **jak exportovat rozsah listu** s plnou kontrolou nad reprezentací každé buňky a získáte několik tipů pro okrajové případy, na které můžete později narazit.

## Co budete potřebovat

- .NET 6 nebo novější (kód funguje také s .NET Framework 4.7+)  
- NuGet balíček **GemBox.Spreadsheet** (nebo jakákoli knihovna, která nabízí `ExportTableOptions`; ukázané API je z GemBox)  
- Základní povědomí o syntaxi C# — nic složitého, jen běžné `using` příkazy a vytváření objektů  

Pokud máte vše výše, můžete se pustit do práce.

## Krok 1: Nastavte možnosti exportu – Hlavní kontrolní bod  

První, co uděláte, je vytvořit instanci `ExportTableOptions` a nastavit ji tak, aby každou buňku zacházela jako s řetězcem. To je základ **jak exportovat excel rozsah** při zachování konzistentního datového typu.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Proč vynutit export jako řetězec?*  
Když později přizpůsobujete každou buňku, budete do ní vkládat závorky a možná i další symboly. Zachování všeho jako řetězce zabraňuje neočekávaným konverzím typů (např. datumy se mění na sériová čísla).

## Krok 2: Připojte se k události CellExport – Přizpůsobení každé buňky  

Nyní přichází zábavná část: **jak přizpůsobit export buněk**. GemBox vyvolá událost `CellExport` pro každou buňku, která se chystá být zapsána. Pokud ji zachytíte, můžete hodnotu obalit závorkami, přidat předponu nebo dokonce buňku úplně přeskočit.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Tip:* Pokud chcete měnit jen číselné buňky, zkontrolujte `e.Value.GetType()` před aplikací závorek. Tato malá ochrana vás může zachránit před nechtěným poškozením textu hlaviček.

## Krok 3: Exportujte požadovaný rozsah – Hlavní akce  

S připravenými možnostmi zavoláte `ExportTable`. Metoda přijímá načtený sešit, adresu rozsahu, který chcete exportovat, a předchozí nastavení.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Přetížení, které jsme použili, zapisuje přímo do souboru (standardně CSV). Pokud dáváte přednost řetězci v paměti, zaměňte poslední argument za `StringWriter` a výsledek si pak přečtěte.

### Plně funkční příklad

Níže je samostatná konzolová aplikace, kterou můžete vložit do nového projektu a spustit okamžitě (jen nahraďte cesty k souborům).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Očekávaný výstup (úryvek CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Každá buňka od *A1* po *D10* je nyní obalena hranatými závorkami, přesně tak, jak jsme definovali v obsluze `CellExport`.

## Řešení běžných okrajových případů  

### 1. Prázdné buňky  
Pokud je buňka prázdná, `e.Value` bude `null`. Pokus o formátování pomocí interpolace řetězce vyvolá výjimku. Ošetřete to:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Velké rozsahy  
Export milionů řádků může narazit na limity paměti. V takovém případě streamujte výstup místo načítání celého sešitu do paměti:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Různé oddělovače  
CSV není jediný formát, který můžete potřebovat. Změňte oddělovač úpravou `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Často kladené otázky  

**Q: Funguje to s .xlsx soubory vytvořenými v Excel 365?**  
Ano. GemBox čte moderní OpenXML formát bez další konfigurace.

**Q: Můžu najednou exportovat více nesouvislých rozsahů?**  
Ne přímo jedním voláním `ExportTable`. Procházejte jednotlivé řetězce rozsahů (`"A1:D10"`, `"F1:H5"` atd.) a výstupy si spojte sami.

**Q: Co když potřebuji použít různý formát podle sloupce?**  
V obsluze `CellExport` máte přístup k `e.ColumnIndex`. Použijte `switch` pro aplikaci logiky specifické pro jednotlivé sloupce.

## Závěr  

Probrali jsme **jak exportovat rozsah listu** s plnou kontrolou nad vzhledem každé buňky, ukázali **jak exportovat excel rozsah** pomocí `ExportTableOptions` a demonstrovali **jak přizpůsobit export buněk** přes událost `CellExport`. Kompletní řešení se vejde do několika desítek řádků C#, přesto je dostatečně flexibilní pro produkční scénáře.

Další kroky? Vyzkoušejte nahradit obalování závorkami formátem vhodným pro JSON, nebo experimentujte s podmíněnou logikou, která přeskočí skryté řádky. Můžete také prozkoumat export přímo do `MemoryStream` pro odpovědi web‑API — žádné dočasné soubory nejsou potřeba.

Pokud jste šli krok po kroku, nyní máte solidní, znovupoužitelný vzor pro export libovolného rozsahu listu přesně tak, jak potřebujete. Šťastné kódování a klidně zanechte komentář, pokud narazíte na problém!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}