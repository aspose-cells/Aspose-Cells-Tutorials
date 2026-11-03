---
category: general
date: 2026-10-13
description: Naučte se, jak uložit Excel jako TXT pomocí Aspose.Cells. Tento průvodce
  pokrývá export Excelu do TXT, zápis hodnoty do buňky a nastavení významných číslic
  během několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: cs
lastmod: 2026-10-13
og_description: Uložte Excel jako TXT pomocí Aspose.Cells. Naučte se, jak exportovat
  Excel do TXT, zapisovat hodnotu do buňky a nastavit významné číslice pomocí několika
  řádků kódu v C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Uložení Excelu jako TXT – krok za krokem průvodce pro .NET vývojáře
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Jak uložit Excel jako TXT pomocí Aspose.Cells v C#
url: /cs/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit Excel jako TXT pomocí Aspose.Cells v C#

Pokud potřebujete **uložit Excel jako TXT** rychle, tento tutoriál vám ukáže kompletní postup během pěti minut. Uvidíte, jak exportovat Excel do TXT, zapsat hodnotu do buňky a nastavit významné číslice, aby textový soubor obsahoval přesně data, která očekáváte.

Export tabulky jako TXT je užitečný, když následné systémy přijímají jen prostý text, když potřebujete generovat logy, nebo když chcete lidsky čitelný výpis výpočtů. Níže uvedený příklad funguje s Aspose.Cells v25.10 nebo novějším a běží na libovolném .NET 6+ runtime.

## Požadavky

Než začnete, ujistěte se, že máte:

* Licencovanou kopii **Aspose.Cells for .NET** (zdarma zkušební verze stačí pro testování).
* Nainstalovaný .NET 6 SDK nebo novější.
* IDE, například Visual Studio 2022, VS Code nebo Rider.
* Základní znalosti C# – není potřeba pokročilá zkušenost s automatizací Excelu.

Aspose.Cells NuGet balíček můžete nainstalovat pomocí:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Vytvořte sešit a přistupte k prvnímu listu (save excel as txt)

Prvním krokem, když chcete **uložit Excel jako TXT**, je vytvořit objekt `Workbook`. Tento objekt představuje celý Excel soubor v paměti.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Proč je to důležité:** Třída `Workbook` je vstupním bodem pro všechny operace s tabulkami. Začínáním s novým sešitem se vyhnete skrytému formátování, které by mohlo ovlivnit výstup prostého textu.

## Krok 2: Zapište číslo s vysokou přesností do buňky (write value to cell)

Nyní potřebujete **write value to cell** A1. Metoda `PutValue` automaticky rozpozná datový typ a uloží jej jako číselnou hodnotu.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** Pokud později potřebujete zapisovat řetězce, data nebo vzorce, funguje stejná metoda `PutValue` – stačí předat odpovídající .NET typ.

## Krok 3: Nakonfigurujte možnosti exportu pro zachování požadované přesnosti (set significant digits)

Při exportu do TXT souboru často chcete omezit počet číslic, aby byl soubor malý nebo aby splňoval specifikaci downstream systému. Třída `TxtSaveOptions` poskytuje vlastnost `SignificantDigits` právě pro tento účel.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Proč nastavit významné číslice:** Bez tohoto nastavení Aspose.Cells zapisuje plnou hodnotu double‑precision, což může vytvořit dlouhé řetězce jako `12345.6789012345`. Nastavením `SignificantDigits = 6` oříznete výstup na `12345.7`, což vyhovuje většině požadavků na reportování.

## Krok 4: Exportujte sešit jako TXT soubor (export excel to txt)

Nakonec **export Excel to TXT** zavoláním `Workbook.Save` s dříve nakonfigurovanými možnostmi.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Po dokončení kódu soubor `LimitedDigits.txt` obsahuje:

```
12345.7
```

> **Ověření výsledku:** Otevřete soubor v libovolném textovém editoru (Notepad, VS Code) a potvrďte, že jsou přítomny jen šest významných číslic a že se neobjevily žádné extra čárky nebo tabulátory.

## Kompletní, spustitelný příklad

Níže je samostatná konzolová aplikace, kterou můžete zkopírovat, vložit a okamžitě spustit.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Vysvětlení jednotlivých bloků**

| Blok | Účel |
|------|------|
| `using Aspose.Cells;` | Importuje jmenný prostor Aspose.Cells potřebný pro `Workbook`, `Worksheet` a `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Vytvoří prázdný Excel sešit v paměti. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 s číslem double‑precision. |
| `TxtSaveOptions` | Konfiguruje chování **set significant digits** pro export do TXT. |
| `workbook.Save(..., txtOptions);` | Provede operaci **export excel to txt**, čímž vytvoří soubor prostého textu. |

## Okrajové případy a další tipy

| Scénář | Jak postupovat |
|--------|----------------|
| **Velké listy** (mnoho řádků/sloupců) | Použijte `txtOptions.Encoding = Encoding.UTF8`, pokud potřebujete podporu Unicode, a zvažte streamování souboru pomocí `Workbook.Save(Stream, txtOptions)`, abyste se vyhnuli vysoké spotřebě paměti. |
| **Vlastní oddělovače** (CSV) | `TxtSaveOptions` také nabízí `Separator` – nastavte jej na `','` pro vytvoření CSV‑stylu výstupu, přičemž formát zůstane TXT. |
| **Zachování vzorců** | Nastavte `txtOptions.ExportFormulas = true`, aby se zapisoval text vzorce místo vypočtené hodnoty. |
| **Locale‑specifické desetinné oddělovače** | Upravit `txtOptions.DecimalSeparator` na `','` pro evropské lokály. |
| **Více listů** | Procházejte `workbook.Worksheets` a volajte `Save` pro každý, přičemž k názvu souboru připojíte jméno listu. |

## Často kladené otázky

**Q: Zaokrouhluje `SignificantDigits` nebo jen ořezává?**  
A: Zaokrouhluje na nejbližší hodnotu podle zadaného počtu významných číslic, čímž zajišťuje matematickou přesnost na tuto úroveň.

**Q: Můžu exportovat přímo do paměťového proudu?**  
A: Ano. Nahraďte cestu k souboru instancí `MemoryStream`: `workbook.Save(stream, txtOptions);`. To je užitečné pro webová API, která potřebují vrátit TXT obsah bez zápisu na disk.

**Q: Co když potřebuji zachovat původní formátování (např. datumy)?**  
A: Použijte `txtOptions.ExportFormattedValues = true`. Tím se Aspose.Cells přinutí zapisovat zobrazený text buňky místo surové hodnoty.

## Závěr

Nyní víte, jak **uložit Excel jako TXT** s plnou kontrolou nad přesností, formátováním a místem výstupu. Dodržením čtyř kroků – vytvoření sešitu, **write value to cell**, **set significant digits** a **export Excel to TXT** – můžete integrovat export prostého textu do jakékoli .NET aplikace.

Dále prozkoumejte související témata jako **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, nebo **use Aspose.Cells to generate JSON reports**. Každé z nich staví na stejných základních konceptech předvedených zde a poskytuje univerzální sadu nástrojů pro výměnu dat napříč platformami.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}