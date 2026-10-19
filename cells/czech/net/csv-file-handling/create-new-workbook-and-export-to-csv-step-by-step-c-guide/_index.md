---
category: general
date: 2026-04-07
description: Vytvořte nový sešit v C# a naučte se, jak exportovat CSV s významnými
  číslicemi. Obsahuje tipy na uložení sešitu jako CSV a export Excelu do CSV.
draft: false
keywords:
- create new workbook
- save workbook as csv
- how to export csv
- save file as csv
- export excel to csv
language: cs
og_description: Vytvořte nový sešit v C# a exportujte jej do CSV s plnou kontrolou
  nad významnými číslicemi. Naučte se uložit sešit jako CSV a exportovat Excel do
  CSV.
og_title: Vytvořte nový sešit a exportujte do CSV – kompletní tutoriál C#
tags:
- C#
- Aspose.Cells
- CSV export
- Excel automation
title: Vytvořte nový sešit a exportujte do CSV – krok za krokem průvodce C#
url: /cs/net/csv-file-handling/create-new-workbook-and-export-to-csv-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu a export do CSV – kompletní C# tutoriál

Už jste někdy potřebovali **vytvořit nový sešit** v C# a přemýšleli, *jak exportovat CSV* bez ztráty přesnosti? Nejste v tom sami. V mnoha projektech datových pipeline je posledním krokem čistý CSV soubor a správné nastavení formátování může být oříšek.

V tomto průvodci projdeme celý proces: od vytvoření nového sešitu, naplnění číselnou hodnotou, nastavení možností exportu pro významné číslice a nakonec **uložení sešitu jako CSV**. Na konci budete mít připravený CSV soubor a pevné pochopení workflow *export excel to CSV* pomocí Aspose.Cells.

## Co budete potřebovat

- **Aspose.Cells for .NET** (NuGet balíček `Aspose.Cells` – verze 23.10 nebo novější).  
- Vývojové prostředí .NET (Visual Studio, Rider nebo `dotnet` CLI).  
- Základní znalost C#; žádné pokročilé Excel interop triky nejsou potřeba.  

To je vše — žádné další COM reference, žádná instalace Excelu.

## Krok 1: Vytvoření instance nového sešitu

Nejprve potřebujeme zcela nový objekt sešitu. Představte si ho jako prázdný list, který existuje jen v paměti.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();
```

> **Proč?** Třída `Workbook` je vstupním bodem pro jakoukoli manipulaci s Excelem v Aspose.Cells. Vytvoření programově znamená, že nejste závislí na existujícím souboru, což udržuje krok **save file as CSV** čistý a předvídatelný.

## Krok 2: Získání první listu

Každý sešit obsahuje alespoň jeden list. Vytáhneme první a pojmenujeme ho přátelsky.

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "Data";
```

> **Tip:** Přejmenování listů pomáhá, když později otevřete CSV v prohlížeči, který respektuje názvy listů, i když CSV samotné názvy neukládá.

## Krok 3: Zapsání číselné hodnoty do buňky A1

Nyní vložíme číslo, které má více desetinných míst, než chceme nakonec zachovat. To nám umožní ukázat funkci *significant digits*.

```csharp
// Step 3: Write a numeric value into cell A1
worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Co když potřebujete více dat?** Stačí dál používat `PutValue` v dalších buňkách (`B2`, `C3`, …) — stejné nastavení exportu se použije na celý list, když **save workbook as CSV**.

## Krok 4: Nastavení možností exportu pro významné číslice

Aspose.Cells vám umožňuje řídit, jak se čísla zobrazí v CSV výstupu. Zde požadujeme čtyři významné číslice a zapneme tuto funkci.

```csharp
// Step 4: Configure export options to use significant digits
ExportOptions exportOptions = new ExportOptions
{
    SignificantDigits = 4,      // keep only 4 significant digits
    UseSignificantDigits = true // enable the feature
};
```

> **Proč používat významné číslice?** Při práci s vědeckými daty nebo finančními výkazy často záleží na přesnosti spíše než na čistých desetinných místech. Toto nastavení zajistí, že CSV odráží požadovanou přesnost, což je častý požadavek při *how to export CSV* pro následnou analytiku.

## Krok 5: Uložení sešitu jako CSV soubor

Nakonec zapíšeme sešit na disk ve formátu CSV a s předchozími možnostmi.

```csharp
// Step 5: Save the workbook as a CSV file using the configured options
string outputPath = @"C:\Temp\out.csv";
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

> **Očekávaný výstup:** Soubor `out.csv` bude obsahovat jediný řádek:

```
12350
```

Všimněte si, že `12345.6789` bylo zaokrouhleno na `12350` — to je výsledek zachování čtyř významných číslic.

### Rychlý kontrolní seznam pro ukládání CSV

- **Existence cesty:** Ujistěte se, že adresář (`C:\Temp` v příkladu) existuje, jinak `Save` vyvolá výjimku.
- **Oprávnění k souboru:** Proces musí mít právo zápisu; jinak se objeví `UnauthorizedAccessException`.
- **Kódování:** Aspose.Cells používá ve výchozím nastavení UTF‑8, což funguje pro většinu locale. Pokud potřebujete jinou kódovou stránku, nastavte `exportOptions.Encoding` před voláním `Save`.

## Běžné varianty a okrajové případy

### Export více listů

CSV je inherentně formát pro jeden list. Pokud zavoláte `Save` na sešitu s několika listy, Aspose.Cells je spojí a oddělí každý list prázdným řádkem. Pro **save file as CSV** jen konkrétního listu dočasně skryjte ostatní:

```csharp
// Hide all sheets except the one you want to export
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.IsVisible = false;
}
worksheet.IsVisible = true; // the sheet we prepared earlier
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

### Řízení oddělovačů

Ve výchozím nastavení Aspose.Cells používá čárku (`,`) jako oddělovač. Pokud potřebujete středník (`;`) pro evropské locale, upravte `CsvSaveOptions`:

```csharp
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    Separator = ';',
    ExportOptions = exportOptions
};
workbook.Save(outputPath, csvOptions);
```

### Velké datové sady

Při exportu milionů řádků zvažte streamování CSV, aby nedošlo k vysoké spotřebě paměti. Aspose.Cells nabízí přetížení `Workbook.Save`, která přijímají `Stream`, což umožňuje zapisovat přímo do souboru, síťové lokace nebo cloudového úložiště.

## Kompletní funkční příklad

Níže je kompletní, připravený program, který spojuje všechny kroky. Zkopírujte jej do konzolové aplikace a stiskněte **F5**.

```csharp
using System;
using Aspose.Cells;

namespace CsvExportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Get the first worksheet and give it a name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Insert a numeric value (more precision than we need)
            worksheet.Cells["A1"].PutValue(12345.6789);

            // 4️⃣ Set up export options – 4 significant digits
            ExportOptions exportOptions = new ExportOptions
            {
                SignificantDigits = 4,
                UseSignificantDigits = true
            };

            // 5️⃣ Define where the CSV will be saved
            string outputPath = @"C:\Temp\out.csv";

            // 6️⃣ Save as CSV using the configured options
            workbook.Save(outputPath, SaveFormat.Csv, exportOptions);

            Console.WriteLine($"CSV file created at: {outputPath}");
        }
    }
}
```

Spusťte program, pak otevřete `C:\Temp\out.csv` v Poznámkovém bloku nebo Excelu. Měli byste vidět zaokrouhlenou hodnotu `12350`, což potvrzuje, že **export excel to CSV** s významnými číslicemi funguje podle očekávání.

## Závěr

Probrali jsme vše, co potřebujete k **vytvoření nového sešitu**, naplnění daty, nastavení přesnosti exportu a nakonec **uložení sešitu jako CSV**. Hlavní body:

- Použijte `ExportOptions` k řízení číselného formátování, když *how to export CSV*.
- Metoda `Save` s `SaveFormat.Csv` je nejjednodušší cesta k **save file as CSV**.
- Pro pokročilé scénáře upravte oddělovače, viditelnost listů nebo použijte streamování výstupu.

### Co dál?

- **Dávkové zpracování:** Procházejte kolekci datových tabulek a generujte samostatné CSV soubory najednou.
- **Vlastní formátování:** Kombinujte `NumberFormat` s `ExportOptions` pro měny nebo datumové styly.
- **Integrace:** Posílejte CSV přímo do Azure Blob Storage nebo S3 bucketu pomocí přetížení se streamem.

Klidně experimentujte s těmito nápady a dejte vědět v komentáři, pokud narazíte na problémy. Šťastné kódování a ať vaše CSV exporty vždy zachovají správný počet významných číslic! 

![Ilustrace C# sešitu ukládaného jako CSV soubor – vytvoření nového sešitu](/images/create-new-workbook-csv.png "ilustrace vytvoření nového sešitu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}