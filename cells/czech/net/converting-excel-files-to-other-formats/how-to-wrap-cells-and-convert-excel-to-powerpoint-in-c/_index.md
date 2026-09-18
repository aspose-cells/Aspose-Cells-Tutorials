---
category: general
date: 2026-09-18
description: Jak zalamovat text v buňkách v sešitu Excel a uložit jej jako soubor
  PowerPoint. Naučte se používat WRAPCOLS, vytvořit list sešitu a exportovat do PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: cs
lastmod: 2026-09-18
og_description: Jak zalamovat buňky v Excelu a exportovat sešit jako editovatelný
  soubor PowerPoint pomocí C#. Postupujte podle krok‑za‑krokem návodu a ovládněte
  WRAPCOLS a tvorbu listů sešitu.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: Jak zalomit buňky a převést Excel do PowerPointu v C#
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Jak zalamovat buňky a převést Excel do PowerPointu v C#
url: /cs/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zalomit buňky a převést Excel do PowerPointu v C#

Pokud potřebujete **how to wrap cells** v listu Excel a poté tento list převést na prezentaci PowerPoint, tento průvodce vám ukáže kompletní, připravené řešení. Na konci prvních dvou vět budete přesně vědět, které volání API provádí zalomení a která metoda uloží soubor jako PPTX.

Použijeme Aspose.Cells for .NET, knihovnu, která vám umožní manipulovat s sešity Excel bez nainstalovaného Microsoft Office. Tutoriál pokrývá **convert Excel to PowerPoint**, ukazuje **how to use WRAPCOLS** a vysvětluje osvědčené postupy **create workbook worksheet**. Žádné externí nástroje nejsou potřeba – pouze vývojové prostředí .NET.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.6+)
- NuGet balíček Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Základní znalost C# a konceptu listů (worksheets)
- IDE jako Visual Studio nebo VS Code

> **Tip:** Používejte bezplatnou zkušební licenci Aspose.Cells během experimentování; před nasazením ji nahraďte plnou licencí.

## Krok 1: Vytvořit sešit a přidat list

Prvním krokem, který musíte **create workbook worksheet**, je vytvořit objekt `Workbook`. Ve výchozím nastavení Aspose.Cells vytvoří jeden list (index 0), který použijeme pro ukázku.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**Proč je to důležité:** Inicializace sešitu vám poskytne čisté plátno. Výchozí list je již součástí kolekce `Worksheets`, takže není potřeba volat `Add()`, pokud nechcete další listy.

## Krok 2: Naplnit zdrojový rozsah (A2:A10)

Než budeme moci **how to wrap cells**, potřebujeme nějaká data k zalomení. Tento krok vyplní buňky A2 až A10 ukázkovým textem.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**Hraniční případ:** Pokud je zdrojový rozsah prázdný, `WRAPCOLS` vrátí `#VALUE!`. Vždy se ujistěte, že rozsah obsahuje alespoň jednu neprázdnou buňku.

## Krok 3: Použít vzorec WRAPCOLS

Nyní odpovídáme na hlavní otázku **how to use WRAPCOLS**. Vzorec vezme svislý rozsah a rozloží jej do zadaného počtu sloupců. Zapíšeme vzorec do buňky `A1`; výsledné pole se automaticky rozšíří do sousedních buněk.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**Co se děje pod kapotou:** `WRAPCOLS` vyhodnotí zdrojový rozsah, rozdělí položky rovnoměrně (nebo co nejblíže) mezi cílové sloupce a zapíše hodnoty do obdélníkového bloku. Velikost bloku je dynamická, takže není nutné předem definovat cílový rozsah.

## Krok 4: Uložit sešit jako editovatelný soubor PowerPoint

Nakonec se zabýváme **convert Excel to PowerPoint** a **save Excel as PowerPoint**. Aspose.Cells může exportovat list přímo do PPTX, přičemž zachová rozvržení jako editovatelný tvar.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**Proč PPTX?** Vygenerovaný PowerPoint obsahuje jediný snímek s zalomenými buňkami zobrazenými jako tabulka. Soubor můžete otevřít v Microsoft PowerPoint, upravit text, změnit styly nebo přidat další snímky – vše zůstane plně editovatelné.

### Očekávaný výstup

- **Excel:** Buňka `A1` zobrazuje 3‑sloupcové pole původních dlouhých řetězců, přičemž každý sloupec obsahuje přibližně stejný počet řádků.
- **PowerPoint:** Po otevření `ChartEditable.pptx` se zobrazí snímek s tabulkou, která odráží zalomené rozvržení. Tabulku lze vybrat, změnit její velikost nebo upravit stejně jako jakýkoli nativní objekt PowerPointu.

## Běžné varianty a na co si dát pozor

| Scénář | Úprava |
|----------|------------|
| **Wrap into more columns** | Změňte druhý argument funkce `WRAPCOLS`, např. `=WRAPCOLS(A2:A10,5)`. |
| **Wrap a different range** | Aktualizujte odkaz ve vzorci, např. `=WRAPCOLS(B2:B15,2)`. |
| **Export only a portion of the sheet** | Použijte `Worksheet.ExportDataTable` k získání `DataTable` a poté API `Presentation` pro vytvoření vlastního PPTX. |
| **Large worksheets ( > 10 000 rows )** | Zvažte rozdělení exportu do více snímků, aby nedošlo k výkonovým úzkým hrdlům. |

> **Pozor:** Výchozí export do PPTX vykreslí list jako jediný obrázek, pokud sešit obsahuje grafy. Použití `WRAPCOLS` zajistí, že data zůstanou jako tabulka, která je editovatelná.

## Kompletní zdrojový kód pro rychlé zkopírování

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

Uložte soubor jako `Program.cs`, obnovte NuGet balíček a spusťte:

```bash
dotnet run
```

Měli byste vidět zprávu v konzoli potvrzující export a soubor PPTX se objeví ve specifikovaném adresáři.

## Závěr

Nyní víte **how to wrap cells** v listu Excel, **how to use WRAPCOLS** a přesné kroky k **convert Excel to PowerPoint** pomocí **save excel as powerpoint** s Aspose.Cells. Kompletní řešení ukazuje **create workbook worksheet**, aplikuje vzorec pro zalomení a vytváří editovatelný soubor PPTX připravený k úpravám prezentace.

### Další kroky

- Prozkoumejte další funkce Excelu (např. `TRANSPOSE`, `FILTER`) před exportem.
- Kombinujte více listů do vícesnímkové prezentace PowerPoint pomocí smyčky.
- Přidejte vlastní názvy snímků nebo branding integrací Aspose.Slides po exportu.

Neváhejte experimentovat s různým počtem sloupců, zdrojovými rozsahy nebo dokonce kombinovat grafy a tabulky ve stejném PPTX. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak převést Excel do PowerPointu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Jak zalomit text v Excelu pomocí Aspose.Cells pro .NET \| Formátovací tutoriál](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Export vlastností sešitu a listu Excel do HTML pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}