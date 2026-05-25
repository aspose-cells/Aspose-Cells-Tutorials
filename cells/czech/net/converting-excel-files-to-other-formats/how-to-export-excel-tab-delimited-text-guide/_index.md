---
category: general
date: 2026-02-26
description: jak exportovat Excel do textového souboru s tabulátorem pomocí C#. Naučte
  se exportovat Excel jako tabulátor, převést Excel na txt a exportovat Excel s oddělovačem
  ve třech snadných krocích.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: cs
og_description: Jak exportovat Excel do souboru txt odděleného tabulátory pomocí C#.
  Tento tutoriál ukazuje export Excelu jako tabulátor, převod Excelu na txt a export
  Excelu s oddělovačem.
og_title: jak exportovat excel – Průvodce textem odděleným tabulátory
tags:
- csharp
- excel
- file-conversion
title: Jak exportovat Excel – Průvodce textem odděleným tabulátory
url: /cs/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

Then closing shortcodes.

Now ensure we keep all placeholders and shortcodes exactly.

Also note there is a line "### Quick Verification" we translated to "### Rychlé ověření". Keep heading level.

Also ensure we keep the image markdown unchanged.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak exportovat excel – Kompletní C# tutoriál

Už jste se někdy zamysleli **jak exportovat excel** data do prostého textového souboru bez ztráty formátování? Možná potřebujete rychlý TSV (tabulkově oddělené hodnoty) pro datový pipeline, nebo napájíte starý systém, který čte jen `.txt`. V každém případě nejste sami — vývojáři často narazí na tuto překážku při přesunu dat z tabulek.

Dobrá zpráva? Za pouhé tři jednoduché kroky můžete **exportovat excel jako tab**‑oddělený text, **převést excel na txt**, a dokonce si vybrat vlastní oddělovač, pokud později změníte názor. Níže uvidíte plně spustitelný C# příklad, proč je každý řádek důležitý, a několik tipů, jak se vyhnout běžným úskalím.

> **Pro tip:** Tento přístup funguje s populární knihovnou Aspose.Cells, ale koncepty se dají použít s jakýmkoli .NET Excel API, které nabízí metodu ve stylu `ExportTable`.

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.6+). Kód se kompiluje na jakémkoli aktuálním runtime.
- **Aspose.Cells for .NET** (zdarma zkušební verze nebo licencovaná). Nainstalujte přes NuGet: `dotnet add package Aspose.Cells`.
- Vstupní sešit pojmenovaný `input.xlsx` umístěný ve složce, kterou ovládáte.
- Trochu zvědavosti — žádné hluboké znalosti interního fungování Excelu nejsou potřeba.

Pokud už to máte, pojďme rovnou přejít k řešení.

## Krok 1 – Načtěte sešit, který chcete exportovat

Nejprve vytvoříme objekt `Workbook`, který ukazuje na zdrojový soubor. Tento objekt představuje celý Excel soubor, včetně všech listů, pojmenovaných oblastí a formátování.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Proč je to důležité:*  
Načtení sešitu vám poskytne přístup ke kolekci listů (`workbook.Worksheets`). Bez tohoto objektu nemůžete adresovat buňky, oblasti ani nastavení exportu.  

> **Poznámka:** Pokud se váš soubor nachází na síťovém disku, přidejte `\\` nebo použijte UNC cestu — Aspose.Cells to zvládne bez problémů.

## Krok 2 – Nastavte možnosti exportu (řetězcové hodnoty a tabulátor jako oddělovač)

Nyní řekneme knihovně, jak mají být data zapsána. Nastavením `ExportAsString = true` vynutíme, aby každá buňka byla považována za prostý řetězec, což eliminuje lokálně specifické číselné formáty Excelu. Část `Delimiter = "\t"` je jádrem **exportovat excel jako tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Proč je to důležité:*  
Pokud vynecháte `ExportAsString`, buňka obsahující `12345` se v některých locale může změnit na `12,345`, což rozbije následné parsery. Oddělovač lze vyměnit za čárky, svislé čáry nebo jakýkoli jiný znak, pokud se později rozhodnete **exportovat excel s oddělovačem** jiným než tabulátorem.

## Krok 3 – Exportujte konkrétní oblast do textového souboru

Nakonec vybereme oblast, která nás zajímá (`A1:D10` v tomto příkladu) a zapíšeme ji do `out.txt`. Metoda `ExportTable` provede veškerou těžkou práci: načte buňky, použije nastavení a výsledek uloží na disk.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Po spuštění najdete `out.txt` s obsahem, který vypadá takto:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Každý sloupec je oddělen **tabulátorem**, což jej připraví pro `awk`, `PowerShell` nebo jakýkoli nástroj kompatibilní s CSV, který respektuje tabulátory.

### Rychlé ověření

Otevřete vygenerovaný soubor v prostém textovém editoru (Notepad, VS Code) a ověřte:

1. Sloupce jsou zarovnané, když zapnete „Zobrazit mezery“.
2. Neobjeví se žádné další uvozovky ani čárky.
3. Všechny číselné buňky jsou přesně takové, jaké byly v Excelu (díky `ExportAsString`).

Pokud něco vypadá špatně, dvojitě zkontrolujte, že zdrojový sešit neskrývá řádky/sloupce, a ujistěte se, že odkazujete na správný index listu.

## Běžné varianty a okrajové případy

### Export celého listu

Pokud chcete **exportovat excel oblast**, která pokrývá celý list, můžete použít `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Použití jiného oddělovače

Přepnutí z tabulátoru na svislou čáru (`|`) je tak jednoduché jako změna jedné řádky:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Tím se vyhoví scénáři **exportovat excel s oddělovačem** bez přepisování dalšího kódu.

### Zpracování velkých souborů (> 100 MB)

Pro obrovské sešity streamujte export, aby se předešlo načítání všeho do paměti:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Převod více listů najednou

Pokud potřebujete **převést excel na txt** pro několik listů, projděte je ve smyčce:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Každý list získá vlastní TSV soubor — praktické pro dávkové úlohy.

## Úplný funkční příklad (připravený ke zkopírování)

Níže je celý program, připravený ke kompilaci. Stačí nahradit cesty k souborům vlastními.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Očekávaný výstup:** Soubor pojmenovaný `out.txt`, kde je každý sloupec oddělen znakem tabulátoru a každá hodnota buňky je přesně taková, jaká je v Excelu.

## Často kladené otázky

- **Funguje to i s .xls soubory?**  
  Ano. Aspose.Cells automaticky detekuje formát, takže můžete ukázat `Workbook` na starší `.xls` a stejný kód platí.

- **Co když moje data obsahují tabulátory?**  
  Tabulátory uvnitř buňky budou zachovány, což může rozbít TSV parsery. V takovém případě zvažte přepnutí na svislou čáru (`|`) jako oddělovač úpravou `exportOptions.Delimiter`.

- **Mohu exportovat místo hodnot i vzorce?**  
  Nastavte `exportOptions.ExportAsString = false` a použijte přetížení `ExportTableOptions`, které zahrnuje `ExportFormula = true`. Výstup bude obsahovat surový text vzorce.

- **Existuje způsob, jak přeskočit skryté řádky?**  
  Ano. Nastavte `exportOptions.ExportHiddenRows = false` (výchozí je `true`). Skryté řádky budou vynechány ve finálním textovém souboru.

## Závěr

Nyní máte solidní, produkčně připravený recept na **jak exportovat excel** data jako tabulátorově oddělený textový soubor, jak **exportovat excel jako tab**, a jak **převést excel na txt** s plnou kontrolou nad oddělovači a výběrem oblastí. Využitím metody `ExportTable` z Aspose.Cells se vyhnete ručnímu sestavování CSV, zachováte věrnost dat a udržíte kód čistý.

Připraveni na další výzvu? Vyzkoušejte:

- Export přímo do `MemoryStream` pro webová API.  
- Dynamické přidání řádku záhlaví na základě obsahu prvního řádku.  
- Integraci tohoto postupu do Azure Function, která sleduje úložiště pro nové nahrané Excel soubory.

Vyzkoušejte to, upravte oddělovač a nechte data proudit kamkoli potřebujete. Šťastné programování!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}