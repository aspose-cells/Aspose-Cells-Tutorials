---
category: general
date: 2026-10-20
description: Uložte sešit jako CSV s přesnými desetinnými číslicemi, uvozovkami u
  hodnot a formátem data japonské éry pomocí Aspose.Cells pro .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set excel number format
- export excel to csv
- quote csv values
language: cs
lastmod: 2026-10-20
og_description: Uložte sešit jako CSV s plnou kontrolou nad desetinnými čísly, uvozovkami
  a japonskými daty podle japonské éry. Postupujte podle tohoto krok‑za‑krokem tutoriálu
  v C# s využitím Aspose.Cells.
og_image_alt: Screenshot illustrating how to save workbook as CSV with custom options
  in C#
og_title: Uložte sešit jako CSV – kompletní průvodce pro vývojáře C#
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Save workbook as CSV with precise decimal digits, quoted values and
    Japanese era date format using Aspose.Cells for .NET.
  headline: How to save workbook as CSV with custom formatting in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
- Excel formatting
title: Jak uložit sešit jako CSV s vlastním formátováním v C#
url: /cs/net/csv-file-handling/how-to-save-workbook-as-csv-with-custom-formatting-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit sešit jako CSV s vlastním formátováním v C#

Pokud potřebujete **uložit sešit jako CSV** a zároveň kontrolovat přesnost desetinných míst, uvozovat hodnoty a pracovat s daty v japonském kalendáři, tento tutoriál vám ukáže, jak na to s Aspose.Cells pro .NET. Naučíte se **exportovat Excel do CSV**, **nastavit číselný formát v Excelu** a **uvozovat hodnoty v CSV**, aby výstup odpovídal běžným požadavkům na výměnu dat.

Průvodce předpokládá, že máte vývojové prostředí .NET (Visual Studio 2022 nebo novější) a platnou licenci Aspose.Cells. Kromě `Aspose.Cells` nejsou vyžadovány žádné další balíčky NuGet.

## Předpoklady

- .NET 6.0 SDK nebo novější  
- Aspose.Cells pro .NET (nainstalováno přes NuGet: `Install-Package Aspose.Cells`)  
- Ukázkový soubor Excel (`Data.xlsx`) umístěný ve složce, na kterou můžete odkazovat z kódu  

## Krok 1: Načtení zdrojového sešitu – základ pro uložení sešitu jako CSV

Nejprve vytvoříte instanci `Workbook`, která ukazuje na Excel soubor, který chcete převést.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\Data.xlsx");
```

*Proč je tento krok důležitý*: Objekt `Workbook` obsahuje všechny listy, styly a vzorce. Všechny následující operace s CSV pracují s touto reprezentací v paměti.

## Krok 2: Omezení přesnosti desetinných míst při ukládání sešitu jako CSV

Když potřebujete přesně čtyři číslice za desetinnou čárkou, nakonfigurujte `CsvSaveOptions`.

```csharp
// Configure CSV saving options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep 4 digits after the decimal point
    SignificantDigits = 4
};

// Save the workbook as CSV with the defined precision
workbook.Save(@"YOUR_DIRECTORY\Data_Sig4.csv", csvOptions);
```

*Klíčový bod*: `SignificantDigits` zaokrouhluje každou číselnou buňku na zadaný počet desetinných míst před zápisem do CSV souboru. Tím se zabrání šumu z plovoucí desetinné čárky v následných systémech.

## Krok 3: Export Excel do CSV s uvozenými hodnotami

Některé následné parsovací nástroje vyžadují, aby každé pole bylo obklopeno dvojitými uvozovkami, zejména když hodnoty obsahují čárky nebo zalomení řádku. Třída `ExportTableOptions` vám umožní zacházet s každou buňkou jako s řetězcem a použít vlastní uvozování.

```csharp
// Prepare export options that treat every cell as a string
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // Force string export for all cells
    // Custom delegate to wrap each value in double quotes
    CustomExport = (cell, writer) =>
    {
        writer.Write('"' + cell.StringValue + '"');
    }
};

// Export the first worksheet as a CSV file with quoted values
workbook.Save(@"YOUR_DIRECTORY\TableExport.csv", tableOptions);
```

*Proč byste měli hodnoty uvozovat*: Uvozování chrání čárky, nové řádky a úvodní/koncové mezery před tím, aby byly interpretovány jako oddělovače, což je nezbytné pro spolehlivý import dat.

## Krok 4: Nastavení číselného formátu v Excelu pro japonské datumy (era)

Excel může ukládat data pomocí kalendářů specifických pro éry. Pro demonstraci vložte řetězec s japonským datumem (era) a použijte odpovídající číselný formát.

```csharp
// Create a new workbook for the era‑date example
Workbook eraWorkbook = new Workbook();
Worksheet sheet = eraWorkbook.Worksheets[0];

// Insert a Japanese‑era date string (Reiwa 3‑04‑01)
sheet.Cells["A1"].PutValue("R3-04-01");

// Apply the Japanese locale number format
sheet.Cells["A1"].SetNumberFormat("[$-ja-JP]yyyy-mm-dd");

// Retrieve the parsed DateTime value
DateTime parsedDate = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(parsedDate); // Outputs: 2021-04-01
```

*Vysvětlení*: Volání `SetNumberFormat` říká Aspose.Cells, aby interpretovalo řetězec pomocí japonského kalendáře. Když zavoláte `GetDateTime()`, knihovna automaticky převede notaci era na gregoriánské datum.

## Krok 5: Ověření vygenerovaných CSV souborů

Po spuštění kódu byste měli ve složce `YOUR_DIRECTORY` vidět tři soubory:

| Název souboru            | Poznámky |
|--------------------------|----------|
| `Data_Sig4.csv`          | Čísla zaokrouhlena na 4 desetinná místa |
| `TableExport.csv`        | Každá buňka obklopena dvojitými uvozovkami |
| `Data.xlsx` (unchanged) | Ukazuje zpracování japonských datumů (zobrazitelné v Excelu) |

Otevřete `Data_Sig4.csv` v editoru prostého textu a ověřte přesnost, a otevřete `TableExport.csv`, abyste viděli uvozené hodnoty, např.:

```
"Name","Score","Comment"
"Alice","95.1234","Excellent"
"Bob","88.0000","Good"
```

Výstup v konzoli pro datum era bude:

```
2021-04-01 00:00:00
```

## Časté úskalí a jak se jim vyhnout

- **Místně závislé desetinné oddělovače**: `CsvSaveOptions` respektuje aktuální kulturu. Pokud potřebujete tečku (`.`) jako oddělovač bez ohledu na locale, nastavte `csvOptions.Separator = ',';`.
- **Velké listy**: Export sešitu s miliony řádků může spotřebovat značné množství paměti. Použijte `ExportTableOptions.StartRow` a `EndRow` k omezení rozsahu exportu.
- **Speciální znaky v řetězcích**: Vlastní zapisovač v kroku 3 pouze přidává okolní uvozovky. Pokud buňka již obsahuje uvozovku, zdvojnásobte ji (`""`), aby CSV zůstalo platné.

## Profesionální tip: Kombinace možností pro maximální kontrolu

Můžete řetězit `CsvSaveOptions` a `ExportTableOptions` tak, že nejprve převedete sešit na `MemoryStream` s jednou sadou možností a poté zapíšete stream na disk s dalšími. Tento přístup vám například umožní použít jak zaokrouhlování desetinných míst **tak** i uvozování v jednom průchodu:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    // Apply rounding
    workbook.Save(ms, csvOptions);
    ms.Position = 0; // Reset stream

    // Load the intermediate CSV into a new workbook for quoting
    Workbook temp = new Workbook(ms, new LoadOptions(LoadFormat.Csv));
    temp.Save(@"YOUR_DIRECTORY\RoundedAndQuoted.csv", tableOptions);
}
```

## Závěr

Nyní víte, jak **uložit sešit jako CSV** s přesným zpracováním desetinných míst, uvozenými hodnotami a vlastním formátováním dat. Kompletní řešení zahrnuje načtení sešitu, konfiguraci `CsvSaveOptions`, použití `ExportTableOptions` k **uvození hodnot v CSV** a aplikaci **číslicového formátu v Excelu** pro japonské datumy (era). Odtud můžete prozkoumat další možnosti, jako jsou vlastní oddělovače, různé kódování nebo selektivní export listů.

---

*Další kroky*  
- Prozkoumejte `CsvSaveOptions.Encoding` pro zápis souborů s UTF‑8 BOM nebo UTF‑16.  
- Použijte `ExportTableOptions.StartColumn` / `EndColumn` k exportu pouze podmnožiny sloupců.  
- Kombinujte tyto techniky s `DataFormatter` z Aspose.Cells pro formátování čísel podle locale.  

Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Uložit sešit jako CSV – Kompletní průvodce exportem Excel do CSV s kontrolou](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-w/)
- [Uložit sešit jako CSV v C# – Export Excel do CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)
- [Vytvořit a uložit Excel sešit jako PDF v ASP.NET pomocí Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}