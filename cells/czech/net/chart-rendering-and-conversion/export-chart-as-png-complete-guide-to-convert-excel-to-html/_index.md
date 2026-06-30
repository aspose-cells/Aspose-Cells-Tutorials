---
category: general
date: 2026-06-30
description: Exportujte graf jako PNG při převodu Excelu na HTML pomocí Aspose.Cells.
  Naučte se vkládat obrázky jako Base64 a uložit sešit jako HTML během několika minut.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: cs
og_description: Exportujte graf jako PNG a vložte obrázky jako Base64 při převodu
  Excelu do HTML. Postupujte podle tohoto krok‑za‑krokem C# tutoriálu a snadno uložte
  sešit jako HTML.
og_title: Exportovat graf jako PNG – Převést Excel do HTML pomocí Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Export grafu jako PNG – Kompletní průvodce převodem Excelu do HTML pomocí Aspose.Cells
url: /cs/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Chart as PNG – Kompletní průvodce převodem Excel do HTML pomocí Aspose.Cells

Už jste se někdy zamýšleli, jak **export chart as PNG** přímo z Excel sešitu a zároveň převést celý list na čisté, responzivní HTML? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují web‑připravenou zprávu, která zobrazuje grafy bez manipulace s oddělenými soubory obrázků. Dobrou zprávou je, že Aspose.Cells to umožňuje snadno.

V tomto tutoriálu projdeme přesně kroky k **convert Excel to HTML**, **embed images as Base64** a nakonec **save workbook as HTML** — při tom zajistíme, že každý graf bude uložen jako PNG obrázek. Na konci budete mít jediný HTML soubor, který můžete vložit na jakoukoli webovou stránku, a všechny grafy se zobrazí okamžitě, bez nutnosti dalších souborů.

## Co se naučíte

- Jak načíst existující sešit, který již obsahuje grafy.  
- Které příznaky `HtmlSaveOptions` řídí export obrázků, formát grafu a responzivitu.  
- Přesný kód potřebný k **export chart as PNG** a vložení těchto PNG jako Base64 řetězců.  
- Jak **save workbook as HTML** jedním voláním metody.  
- Tipy pro řešení běžných problémů, jako chybějící obrázky grafů nebo příliš velké Base64 řetězce.  

**Požadavky:**  
- .NET 6+ (nebo .NET Framework 4.6+) nainstalovaný.  
- Platná licence Aspose.Cells (nebo dočasný evaluační klíč).  
- Základní znalost C# a Visual Studio (nebo vašeho oblíbeného IDE).  

Pokud vám některá z těchto věcí není známá, zastavte se na chvíli a připravte si je; zbytek průvodce předpokládá, že jsou připravené.

---

## Krok 1: Nastavte projekt a nainstalujte Aspose.Cells

Než budeme moci **export chart as PNG**, potřebujeme C# projekt, který odkazuje na knihovnu Aspose.Cells.

1. Otevřete Visual Studio a vytvořte novou **Console App** (`dotnet new console`).  
2. Přidejte NuGet balíček Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (Volitelné) Pokud máte licenční soubor, umístěte jej do kořenového adresáře projektu a aktivujte jej za běhu:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Pro tip:** Uchovávejte licenční soubor mimo zdrojový kontrolní systém. Používejte proměnné prostředí nebo zabezpečené úložiště tajemství pro produkci.

---

## Krok 2: Načtěte sešit, který obsahuje graf

Nyní načteme Excel soubor, který již má graf, který chceme **export chart as PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Proč je to důležité:** Načtení sešitu včas nám poskytne přístup ke všem listům, grafům a vloženým objektům. Pokud sešit selže při načítání, následující krok **export chart to PNG** se nikdy neprovede.

---

## Krok 3: Nakonfigurujte HTML Save Options

Srdcem řešení jsou `HtmlSaveOptions`. Přepnutím několika vlastností můžeme:

- **ExportChartImageFormat = ImageFormat.Png** → zajistí, že každý graf bude PNG.  
- **ExportImagesAsBase64 = true** → vloží PNG data přímo do HTML, eliminuje externí soubory.  
- **IsResponsive = true** → umožní generovaným tabulkám přizpůsobit se mobilním obrazovkám.  
- **ExportPrintingHeadersFooters = false** → odstraní zbytečná metadata pro tisk.  

Zde je kompletní konfigurace:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Proč tato nastavení?

- **ExportChartImageFormat = ImageFormat.Png** je jediný způsob, jak garantovat bezztrátový, web‑bezpečný obrázek grafu.  
- **ExportImagesAsBase64 = true** znamená, že můžete **embed images as Base64**, což je ideální pro e‑mailové zprávy nebo nasazení v jediném souboru.  
- **IsResponsive = true** řeší častou stížnost: tabulky, které přetéčou na smartphonech.  
- **ExportPrintingHeadersFooters = false** udržuje HTML lehké — žádné skryté tiskové informace, které se na webu nikdy nepoužijí.  

---

## Krok 4: Uložte sešit jako HTML

Po nastavení možností je poslední řádek jediným voláním, které **convert excel to html** a **export chart as PNG** provede na pozadí.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

Až tento řádek dokončí, budete mít soubor nazvaný `Report.html`. Otevřete jej v libovolném prohlížeči a uvidíte:

- Všechna data listu vykreslená jako čisté HTML tabulky.  
- Každý graf zobrazený jako vložený PNG obrázek (díky Base64).  
- Žádné extra soubory obrázků vedle HTML.  

### Očekávaný výstup

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Všimněte si atributu `src="data:image/png;base64,..."` — to je magie **embed images as base64** v akci. Žádné samostatné `.png` soubory nejsou vytvořeny na disku.

---

## Krok 5: Ověřte export PNG a upravte podle potřeby

Někdy může graf po konverzi vypadat mírně rozmazaně, zejména pokud používá vlastní fonty nebo složité gradienty. Zde je postup, jak to zkontrolovat:

1. Otevřete vygenerované HTML v Chrome. Klikněte pravým tlačítkem na obrázek grafu a zvolte **Open image in new tab**. URL stále začne `data:image/png;base64,`.  
2. Pokud je obrázek rozmazaný, zvažte zvýšení rozlišení grafu před uložením:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Pro grafy, které závisí na externích zdrojích dat, se ujistěte, že je sešit plně obnoven před uložením:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Tyto úpravy zajistí, že krok **export excel chart to png** poskytne ostrou, produkčně připravenou grafiku.

---

## Krok 6: Nasazení HTML kdekoliv

Protože jsou všechny obrázky vloženy, můžete nyní:

- Poslat HTML jako jedinou přílohu e‑mailu.  
- Vložit HTML do CMS, který akceptuje čistý kód.  
- Hostovat jej na statické stránce bez obav o chybějící PNG soubory.  

Pokud někdy budete potřebovat PNG soubory jako samostatná aktiva (např. pro PDF), můžete přepnout `ExportImagesAsBase64` na `false` a nastavit `HtmlSaveOptions` na výstupní složku pro obrázky.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Nyní bude HTML odkazovat na externí PNG soubory, stále zajišťuje **export chart as png**, ale poskytne vám jednotlivé soubory pro další použití.

---

## Běžné problémy a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| Graf chybí v HTML | `ExportChartImageFormat` zůstalo na výchozím (`Jpeg`) a prohlížeč blokuje smíšený obsah. | Nastavte `ExportChartImageFormat = ImageFormat.Png`. |
| HTML soubor je obrovský (několik MB) | Velké grafy nebo mnoho vysoce rozlišených obrázků vložených jako Base64. | Snižte `htmlOptions.ImageResolution` nebo komprimujte graf v Excelu před konverzí. |
| Tabulky přetéčou na mobilu | `IsResponsive` není povoleno. | Ujistěte se, že `IsResponsive = true` v `HtmlSaveOptions`. |
| Base64 řetězce obsahují znaky nových řádků | Starší verze .NET mohou dlouhé řetězce zalamovat. | Upgradujte na .NET 6+ nebo nastavte `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bonus: Zabalte vše do znovupoužitelné metody

Pokud budete tuto konverzi provádět opakovaně, zabalte logiku:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Nyní můžete volat `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` odkudkoli ve vašem kódu.

---

## Závěr

Právě jste se naučili, jak **export chart as PNG** při **convert Excel to HTML**, **embed images as Base64** a **save workbook as HTML** pomocí Aspose.Cells. Hlavní výsledek je, že několik dobře zvolených nastavení `HtmlSaveOptions` vám poskytne jediný, samostatný HTML soubor, který funguje na jakémkoli zařízení — žádné extra PNG soubory, žádné nepořádné složky.

Jste připraveni na další výzvu? Zkuste kombinovat tento přístup s **export excel chart to PNG** pro generování PDF, nebo experimentujte s vlastním CSS pro další úpravu tabulek. Možnosti jsou neomezené, když ovládáte jak data, tak prezentaci programově.

Neváhejte zanechat komentář, pokud narazíte na potíže, nebo podělit se o to, jak jste tento vzor přizpůsobili ve svých projektech. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}