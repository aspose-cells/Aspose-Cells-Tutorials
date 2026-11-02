---
category: general
date: 2026-07-13
description: Jak exportovat oblast buněk jako tabulku pomocí C# a ExportTableOptions.
  Naučte se krok za krokem nastavení sešitu, formátování a export tabulky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: cs
lastmod: 2026-07-13
og_description: Jak exportovat oblast buněk jako tabulku v C# pomocí ExportTableOptions.
  Postupujte podle tohoto návodu, abyste formátovali buňky, vytvořili sešit a snadno
  exportovali tabulku.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Jak exportovat oblast buněk jako tabulku – Kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Jak exportovat oblast buněk jako tabulku – Kompletní průvodce C#
url: /cs/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat oblast buněk jako tabulku – Kompletní průvodce C#  

Už jste se někdy zamýšleli **jak exportovat oblast buněk jako tabulku** bez toho, abyste si trhali vlasy kvůli podivnostem formátování? Nejste v tom sami. Ať už posíláte data do reportovacího kanálu nebo jen potřebujete rychlý výpis ve stylu CSV, zvládnutí exportního procesu vám může ušetřit hodiny ručního kopírování a vkládání.

V tomto tutoriálu projdeme přesně kroky, jak vzít číselnou buňku, použít vědecký zápis a exportovat ji jako tabulku pomocí **ExportTableOptions**. Na konci budete mít spustitelný úryvek, pochopíte *proč* každého volání a budete vědět, jak upravit kód pro větší oblasti nebo jiné formáty.

## Požadavky

- .NET 6 nebo novější (API funguje stejně i na .NET Framework 4.7+)
- Aspose.Cells pro .NET nainstalován (`Install-Package Aspose.Cells`)
- Základní znalost syntaxe C#; není potřeba hluboké znalosti interního fungování Excelu

Máte to? Skvělé – pojďme na to.

## Krok 1: Nastavení možností exportu – Jak exportovat oblast buněk jako tabulku

První, co potřebujete, je instance **ExportTableOptions**, která knihovně říká, jak má zacházet s obsahem buněk. Bez ní export standardně používá surové číselné hodnoty, což může rozbít následné spotřebitele očekávající text.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Proč je to důležité:**  
- `ExportAsString = true` nutí knihovnu zapsat zobrazený text buňky, nikoli její podkladové číslo typu double.  
- `CustomFormat` vám umožní vynutit **export ve vědeckém zápisu**, užitečné při práci s velmi velkými nebo velmi malými čísly.

> **Tip:** Pokud potřebujete formát data nebo měny, nahraďte `"0.00E+00"` řetězcem `"yyyy‑MM‑dd"` nebo `"$#,##0.00"`.

## Krok 2: Vytvoření sešitu a získání první listu – Práce se sešitem a listem

**Workbook** představuje celý soubor Excel, zatímco **Worksheet** je jediná karta. Pro jednoduchý export použijeme první list, který je vždy přítomen na indexu 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Proč je to důležité:**  
Vytvoření nového `Workbook` zajišťuje čistý start – žádné skryté styly ani zbylé data, která by vás mohla překvapit. Přístup k `Worksheets[0]` je nejrychlejší cesta, jak získat odkaz na aktivní list, aniž byste se museli starat o názvy listů.

## Krok 3: Naplnění cílové buňky – Formátování hodnoty buňky v C#

Nyní vložíme číselnou hodnotu do buňky **A1** (řádek 0, sloupec 0). Hodnota je záměrně dlouhá desetinná, aby bylo vidět, jak funguje vědecký zápis.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Proč je to důležité:**  
Volání `PutValue` automaticky určuje datový typ buňky. Protože později exportujeme jako řetězec, surový double bude převeden pomocí formátu, který jsme nastavili dříve, a získáme tak úhledný výstup `"1.23E+04"`.

## Krok 4: Export definované oblasti buněk jako tabulky – Export oblasti buněk jako tabulky

S nastavenými možnostmi a daty je posledním krokem říct Aspose.Cells, aby oblast zapsal. Metoda `ExportTable` očekává počáteční řádek/sloupec, velikost oblasti a objekt možností, který jsme vytvořili.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Proč je to důležité:**  
- `totalRows = 1` a `totalColumns = 1` omezují export na jedinou buňku, ale můžete tato čísla rozšířit pro větší bloky (např. `5, 3` pro oblast 5 řádků × 3 sloupců).  
- Metoda zapisuje data do interní struktury tabulky, kterou lze uložit jako CSV, HTML nebo dokonce přímo streamovat klientovi.

### Uložení výsledku (volitelné)

Pokud chcete exportovanou tabulku uložit na disk, můžete ji zapsat do CSV souboru:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Po spuštění výše uvedeného kódu se vygeneruje soubor obsahující:

```
1.23E+04
```

## Okrajové případy a běžné varianty

| Situace | Co změnit | Důvod |
|-----------|----------------|--------|
| **Export více řádků** | Upravit `totalRows` a případně přidat smyčku přes řádky | Umožňuje hromadný export bez opakovaného volání `ExportTable` |
| **Zachování vzorců** | Nastavit `ExportAsString = false` | Zachová původní vzorec místo zobrazené hodnoty |
| **Různé oddělovače** | Použít přetížení `ExportTableToCSV(..., ',', ...)` | Přepne z čárkou oddělených hodnot na tabulátorem nebo svislítkem oddělené hodnoty |
| **Velké listy** | Streamovat export, aby nedošlo k `OutOfMemoryException` | Funguje dobře pro >10 000 řádků |

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Kompiluje se v jakémkoli .NET konzolovém projektu, který odkazuje na Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Očekávaný výstup:**  
Soubor pojmenovaný `ExportedTable.csv` obsahující jediný řádek:

```
1.23E+04
```

Pokud otevřete CSV v textovém editoru, uvidíte přesně definovaný vědecký zápis.

## Závěr

Probrali jsme **jak exportovat oblast buněk jako tabulku** od začátku do konce: nastavení `ExportTableOptions`, vytvoření `Workbook`, vložení dat a nakonec volání `ExportTable`. Porozuměním každému kroku můžete nyní rozšířit přístup na větší oblasti, jiné formáty nebo jej dokonce integrovat do webového API, které poskytuje data odvozená z Excelu na vyžádání.

Do budoucna můžete zkusit:

- **ExportTableToHTML** pro náhledy připravené na web  
- **ExportTableToDataTable** pro přímé napojení na ADO.NET pipeline  
- Pokročilé **vlastní formáty** pro data, měny nebo procenta  

Vyzkoušejte to a proměňte jednoduchý export buňky v univerzální nástroj pro doručování dat. Máte otázky nebo netradiční případ použití? Zanechte komentář níže – šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak exportovat viditelné řádky Excelu pomocí Aspose.Cells pro .NET: Průvodce krok za krokem](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Jak exportovat soubory Excel v .NET pomocí Aspose.Cells: Kompletní průvodce](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Jak přistupovat k buňce Excelu podle názvu pomocí Aspose.Cells pro .NET: Průvodce krok za krokem](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}