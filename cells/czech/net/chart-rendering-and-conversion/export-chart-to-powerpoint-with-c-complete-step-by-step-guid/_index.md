---
category: general
date: 2026-02-26
description: Exportujte graf do PowerPointu z Excelu pomocí C#. Naučte se, jak převést
  Excel na PowerPoint, uložit Excel jako PowerPoint a zachovat editovatelnost tvarů.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: cs
og_description: Exportujte graf do PowerPointu z Excelu pomocí C#. Tento návod ukazuje,
  jak převést Excel do PowerPointu, uložit sešit jako PPTX a zachovat editovatelnost
  tvarů.
og_title: Export grafu do PowerPointu pomocí C# – Kompletní programovací tutoriál
tags:
- Aspose.Cells
- C#
- Office Automation
title: Export grafu do PowerPointu pomocí C# – Kompletní průvodce krok za krokem
url: /cs/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export grafu do PowerPointu – Kompletní programovací tutoriál

Už jste se někdy zamýšleli, jak **exportovat graf do PowerPointu** bez ztráty editovatelnosti? V mnoha scénářích reportování potřebujete živý graf v prezentaci, ale ruční kopírování a vkládání je obtížné. Dobrou zprávou je, že to můžete provést programově pomocí několika řádků C#.

V tomto průvodci projdeme celý proces: od načtení sešitu Excel, který obsahuje graf s textovým polem, přes nastavení exportu tak, aby textová pole a tvary zůstaly editovatelné, až po uložení výsledku jako soubor **PowerPoint**. Na konci také budete vědět, jak **převést Excel do PowerPointu**, **uložit Excel jako PowerPoint**, a dokonce upravit možnosti pro okrajové scénáře.

## Co budete potřebovat

- **Aspose.Cells for .NET** (verze 23.10 nebo novější). Jedná se o knihovnu, která usnadňuje konverzi.
- **.NET 6+** runtime – funguje jakékoli recentní SDK.
- Jednoduchý soubor Excel (`ChartWithTextbox.xlsx`), který obsahuje alespoň jeden graf a textové pole.
- Visual Studio nebo vaše oblíbené IDE.

Kromě Aspose.Cells nejsou vyžadovány žádné další balíčky NuGet, ale základní znalost syntaxe C# určitě pomůže.

## Export grafu do PowerPointu – Krok za krokem

Níže rozdělíme řešení na jednotlivé, snadno sledovatelné kroky. Každý krok obsahuje přesný kód, který potřebujete, a krátký odstavec „proč“, který vysvětluje důvod.

### Krok 1: Načtení sešitu Excel, který obsahuje graf

Nejprve musíme načíst zdrojový soubor do paměti. Použití `Workbook` z Aspose.Cells načte celý sešit, včetně grafů, obrázků a vložených objektů.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Proč je to důležité:* Pokud je sešit otevřen bez správného určení cesty, získáte `FileNotFoundException`. Rychlá kontrola zabraňuje pozdějšímu exportu prázdného snímku.

### Krok 2: Připravte možnosti prezentace pro zachování editovatelnosti tvarů

Aspose.Cells vám umožňuje rozhodnout, zda textová pole, tvary a dokonce samotný graf zůstanou po exportu **editovatelné**. Nastavením `ExportTextBoxes` a `ExportShapes` na `true` zachováte tyto objekty jako nativní prvky PowerPointu místo jejich zploštění do statického obrázku.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Proč je to důležité:* Pokud ponecháte tyto příznaky v jejich výchozím nastavení (`false`), výsledný snímek bude obsahovat bitmapu grafu, což znemožní pozdější úpravu řad nebo změnu popisku. Povolením obou možností získáte skutečný PowerPoint graf, který se chová přesně jako ten, který byste vytvořili ručně.

### Krok 3: Převod Excelu do PowerPointu a uložení souboru

Nyní zavoláme metodu `Save`, předáme enum `SaveFormat.Pptx` a možnosti, které jsme právě nakonfigurovali. Knihovna se postará o převod objektu grafu z Excelu na tvar grafu v PowerPointu.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Proč je to důležité:* Volání `Save` provede veškerou těžkou práci – mapování řad z Excelu na řady v PowerPointu, zachování formátování os a kopírování všech propojených textových polí. Po provedení tohoto řádku budete mít plně editovatelný soubor `.pptx`, připravený k otevření v Microsoft PowerPoint.

### Ověření výsledku

Otevřete `Result.pptx` v PowerPointu. Měli byste vidět snímek, který obsahuje:

- Původní graf, stále propojený s jeho daty (můžete dvojklikem upravit řady).
- Jakékoli textové pole, které bylo v listu Excel, nyní jako nativní textové pole PowerPointu.
- Rozložení snímku je automaticky vybráno (obvykle prázdný snímek).

Pokud si všimnete chybějících prvků, zkontrolujte, že zdrojový sešit skutečně obsahoval viditelné objekty a že `ExportTextBoxes` / `ExportShapes` byly nastaveny na `true`.

### Převod Excelu do PowerPointu: Práce s více listy

Často sešit obsahuje více než jeden list, každý s vlastním grafem. Ve výchozím nastavení Aspose.Cells exportuje **všechny** grafy ze **všech** listů do samostatných snímků. Pokud potřebujete jen podmnožinu, můžete je před uložením filtrovat:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Tip:* Nastavení `chart.IsVisible = false` je levnější než úplné odstranění grafu a umožňuje vám přepínat zahrnutí bez úpravy zdrojového souboru.

### Uložení Excelu jako PowerPoint – Přizpůsobení velikosti snímku

PowerPoint ve výchozím nastavení používá snímek o rozměrech 10 palců × 5,63 palce. Pokud se vám graf zdá stísněný, můžete změnit rozměry snímku pomocí objektu `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Nyní bude mít exportovaný graf více místa a všechna textová pole si zachovají původní rozložení.

### Jak převést Excel do PPT: Práce se skrytými objekty

Skryté řádky, sloupce nebo tvary se mohou někdy nechtěně dostat do exportu. Pro jejich odstranění proveďte rychlé vyčištění před uložením:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Tento krok není vždy nutný, ale zabraňuje nečekaným mezerám ve finální prezentaci.

### Uložení sešitu jako PPTX – Kompletní funkční příklad

Spojením všech částí zde máte připravený konzolový program, který demonstruje celý proces:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Spuštěním tohoto programu vytvoříte `Result.pptx` s editovatelným grafem a textovým polem, přesně to, co byste očekávali při ručním **uložení sešitu jako pptx**.

![Příklad exportu grafu do PowerPointu](/images/export-chart-to-powerpoint.png "Export grafu do PowerPointu – editovatelný snímek")

## Časté otázky a okrajové případy

**Co když soubor Excel obsahuje graf s propojeným externím zdrojem dat?**  
Aspose.Cells zkopíruje *aktuální* hodnoty dat do grafu v PowerPointu. **Ne**zachová externí odkaz, protože PowerPoint nemůže odkazovat na datové spojení Excelu stejným způsobem. Pokud potřebujete živé aktualizace, zvažte vložení původního souboru Excel do PPTX jako OLE objekt.

**Mohu exportovat graf, který používá vlastní motiv?**  
Ano. Knihovna se snaží mapovat barvy motivu z Excelu do slotů motivu v PowerPointu. Pro velmi vlastní palety může být nutné po exportu upravit barvy pomocí API PowerPointu (např. Aspose.Slides).

**Existuje limit na počet grafů?**  
Prakticky žádný – Aspose.Cells streamuje data, takže i sešit s desítkami grafů bude exportován, i když velikost výsledného PPTX roste lineárně.

**Potřebuji licenci pro Aspose.Cells?**  
Bezplatná zkušební verze funguje, ale přidá vodoznak na první snímek. Pro produkční použití získejte řádnou licenci, která odstraní vodoznak a odemkne plný výkon.

## Shrnutí

Probrali jsme, jak **exportovat graf do PowerPointu** pomocí C#, ukázali přesný kód pro načtení sešitu Excel, nastavení `PresentationOptions` pro zachování editovatelnosti textových polí a tvarů a nakonec uložení výsledku jako `.pptx`. Také jste se naučili, jak **převést Excel do PowerPointu**, **uložit Excel jako PowerPoint**, a odpověděli na otázku „**jak převést Excel do ppt**“ pomocí kompletního, spustitelného příkladu.

## Co dál?

- **Uložit sešit jako PPTX** s více snímky: projít každý list a zavolat `Save` s `PresentationOptions` pro každý.
- Prozkoumejte **Aspose.Slides**, pokud potřebujete programově dále upravovat vygenerovaný PPTX (přidat přechody, poznámky řečníka atd.).
- Vyzkoušejte export **pivot grafů** nebo **3‑D grafů** – stejné možnosti platí, ale může být potřeba po exportu upravit formátování os.

Pokud narazíte na nějaké potíže, zanechte komentář níže nebo si prohlédněte oficiální dokumentaci Aspose.Cells pro nejnovější změny API. Šťastné programování a užívejte si převod těchto Excel grafů do elegantních PowerPoint prezentací pomocí několika řádků C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}