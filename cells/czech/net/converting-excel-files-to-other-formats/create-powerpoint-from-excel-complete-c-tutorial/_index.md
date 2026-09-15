---
category: general
date: 2026-02-21
description: Rychle vytvořte PowerPoint z Excelu. Naučte se, jak exportovat Excel
  do PowerPointu s editovatelným textem a grafy pomocí Aspose.Cells během několika
  řádků C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: cs
og_description: Vytvořte PowerPoint z Excelu s editovatelným textem a grafy. Postupujte
  podle tohoto podrobného návodu k exportu Excelu do PowerPointu pomocí Aspose.Cells.
og_title: Vytvořte PowerPoint z Excelu – krok za krokem C# průvodce
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Vytvořte PowerPoint z Excelu – kompletní C# tutoriál
url: /cs/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PowerPointu z Excelu – Kompletní C# tutoriál

Už jste někdy potřebovali **vytvořit PowerPoint z Excelu**, ale nebyli jste si jisti, kterou API použít? Nejste v tom sami. Mnoho vývojářů narazí na problém, když chtějí převést tabulku bohatou na data do vylepšené prezentace, zejména když potřebují, aby textová pole zůstala po konverzi editovatelná.  

V tomto průvodci vám ukážeme, jak **exportovat Excel do PowerPointu** se zachováním editovatelného textu, věrnosti grafů a rozvržení – vše pomocí několika řádků C#. Na konci budete mít připravený soubor PPTX, který můžete v PowerPointu upravovat stejně jako jakýkoli ručně vytvořený snímek.

## Co se naučíte

- Jak načíst sešit Excelu, který obsahuje grafy a tvary.  
- Jak nakonfigurovat `PresentationExportOptions`, aby textová pole zůstala editovatelná (`export editable text`).  
- Jak skutečně **exportovat Excel graf PowerPoint** a získat čistou sadu snímků.  
- Menší variace, které můžete použít, když potřebujete **převést Excel graf PowerPoint** pro různé nastavení stránky nebo více listů.  

### Požadavky

- Vývojové prostředí .NET (Visual Studio 2022 nebo novější).  
- Aspose.Cells pro .NET (zkušební verze nebo licencovaná verze).  
- Soubor Excel (`ChartWithShape.xlsx`) obsahující alespoň jeden graf a tvar, který chcete ponechat editovatelný.  

Pokud máte vše připravené, pojďme na to – žádné zbytečnosti, jen praktické a spustitelné řešení.

## Vytvoření PowerPointu z Excelu – krok za krokem

Pod každým krokem uvedeme stručný úryvek kódu, vysvětlíme **proč** to děláme, a upozorníme na časté úskalí. Klidně si celý příklad zkopírujte ze spodní části stránky.

### Krok 1: Načtení sešitu Excel

Nejprve musíme načíst zdrojový sešit do paměti. Aspose.Cells soubor přečte a vytvoří bohatý objektový model, se kterým můžeme pracovat.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Proč je to důležité:**  
Načtení sešitu je základem. Pokud je cesta k souboru špatná nebo je sešit poškozený, všechny následující kroky `export excel to powerpoint` selžou. Kontrola integrity vám poskytne včasnou zpětnou vazbu místo nejasné chyby „soubor nenalezen“ později.

### Krok 2: Příprava možností exportu

Aspose.Cells poskytuje objekt `PresentationExportOptions`, který řídí vzhled výsledného PPTX. Zde rozhodujete, zda má text zůstat editovatelný.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Proč je to důležité:**  
Bez nastavení `PresentationExportOptions` knihovna použije výchozí hodnoty, které nemusí odpovídat vaší firemní šabloně prezentace. Nastavení velikosti snímku předem zabraňuje nutnosti ručního přizpůsobení později.

### Krok 3: Povolení editovatelných textových polí

Magický příznak `ExportEditableTextBoxes` říká Aspose.Cells, aby zachoval všechny textové tvary jako textová pole v PowerPointu, nikoli jako statické obrázky.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Proč je to důležité:**  
Pokud tento řádek vynecháte, výsledný PPTX bude obsahovat rasterizovaný text – což znamená, že v PowerPointu nebudete moci upravit popisek nebo titulek. Nastavení `export editable text` je klíčem k opravdu znovupoužitelnému balíčku snímků.

### Krok 4: Export listu do PPTX

Nyní skutečně zapíšeme soubor PPTX. Můžete zvolit libovolný list; zde používáme první (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Proč je to důležité:**  
`SaveToPptx` respektuje nastavení stránky (okraje, orientaci), které jste definovali v Excelu, takže snímek odráží rozvržení, které jste již navrhli. To je jádro **export excel chart powerpoint**.

### Krok 5: Ověření výstupu (volitelné, ale doporučené)

Po konverzi otevřete vygenerovaný `Result.pptx` v PowerPointu a zkontrolujte:

1. Grafy jsou ostré a zachovávají datové řady.  
2. Textová pole jsou vybratelná a editovatelná.  
3. Velikost snímku odpovídá vašim očekáváním.

Pokud něco vypadá špatně, vraťte se k `exportOptions` – například můžete nastavit `exportOptions.IncludePrintArea = true`, aby se respektovala pojmenovaná oblast tisku.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Krok 6: Pokročilé variace (export více listů)

Často budete chtít **převést excel chart powerpoint** pro několik listů najednou. Projděte kolekci a každému snímku přiřaďte jedinečný název:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Tip:** Pokud potřebujete všechny listy v *jednom* PPTX, vytvořte nový objekt `Presentation`, importujte každý snímek a pak soubor uložte jednou. Je to o něco složitější, ale ušetří vám to práci s mnoha soubory.

## Kompletní funkční příklad

Zde je celý program, který můžete vložit do konzolové aplikace a okamžitě spustit.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Očekávaný výsledek:**  
Po otevření `Result.pptx` uvidíte snímek, který odráží rozvržení listu v Excelu. Každý graf, který jste v Excelu umístili, se objeví jako nativní PowerPoint graf a popisek, který jste přidali jako tvar, se nyní stane plně editovatelným textovým polem.

## Často kladené otázky a okrajové případy

- **Funguje to s makry povolenými sešity (`.xlsm`)?**  
  Ano. Aspose.Cells načte makra, ale nespouští je. Proces konverze ignoruje VBA, takže vizuální obsah získáte i tak.

- **Co když můj list obsahuje více grafů?**  
  Všechny viditelné grafy jsou převedeny na stejný snímek. Pokud potřebujete každý graf na samostatném snímku, rozdělte list nebo použijte smyčku uvedenou v kroku 6.

- **Mohu zachovat vlastní PowerPoint témata?**  
  Přímo během exportu ne. Po konverzi můžete v PowerPointu aplikovat téma nebo to provést programově pomocí Aspose.Slides.

- **Existuje způsob, jak exportovat jen vybraný rozsah?**  
  Nastavte pojmenovanou oblast tisku v Excelu (`Rozložení stránky → Oblast tisku`) a povolte `exportOptions.IncludePrintArea = true`.

## Závěr

Nyní víte, jak **vytvořit PowerPoint z Excelu** pomocí Aspose.Cells, s plnou kontrolou nad editovatelným textem, věrností grafů a velikostí snímků. Krátký úryvek kódu, který jsme poskytli, řeší nejčastější scénář a další tipy vám dávají flexibilitu, když potřebujete **export excel to powerpoint** pro více listů nebo vlastní rozvržení.  

Jste připraveni na další výzvu? Zkuste kombinovat tento přístup s **Aspose.Slides** a programově přidávat přechody, poznámky přednášejícího nebo dokonce vložit vygenerované snímky do větší prezentace. Nebo experimentujte s převodem celého sešitu na více‑snímkovou prezentaci – ideální pro automatizované reportovací pipeline.

Máte otázky nebo jste objevili chytrý trik? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}