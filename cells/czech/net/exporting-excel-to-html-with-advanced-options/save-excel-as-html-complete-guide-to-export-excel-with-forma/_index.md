---
category: general
date: 2026-07-14
description: Uložte Excel jako HTML rychle a naučte se, jak převést Excel do HTML
  s plným formátováním. Exportujte Excel s formátováním pomocí Aspose.Cells během
  několika minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: cs
lastmod: 2026-07-14
og_description: Uložte Excel jako HTML okamžitě. Tento průvodce ukazuje, jak převést
  Excel do HTML při zachování stylů a povolení formátování čísel v Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Uložte Excel jako HTML – krok za krokem export s plným formátováním
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Uložte Excel jako HTML – Kompletní průvodce exportem Excelu s formátováním
url: /cs/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložte Excel jako HTML – Kompletní průvodce exportem Excelu s formátováním

Už jste se někdy ptali, jak **uložit Excel jako HTML** bez ztráty barev, okrajů nebo formátů čísel? Nejste v tom sami. V mnoha scénářích reportování potřebujete web‑připravený pohled na sešit a nejrychlejší způsob je exportovat soubor přímo do HTML.  

V tomto tutoriálu projdeme přesně kroky, jak **převést Excel do HTML** pomocí Aspose.Cells, povolit formátování čísel v Grid.js a zajistit, aby výstup vypadal přesně jako původní tabulka. Na konci budete mít připravený HTML soubor, který můžete nasadit na libovolný webový server.

## Co se naučíte

- Předpoklady a instalace balíčku  
- Načtení existujícího sešitu (nebo vytvoření nového za běhu)  
- Konfigurace `HtmlSaveOptions` pro dokonalou vizuální věrnost  
- Povolení `GridJsOptions.EnableNumberFormat` pro zachování číselného stylu  
- Uložení souboru a ověření výsledku  

Pokud jste někdy zkoušeli **exportovat Excel s formátováním** pomocí obecného CSV výpisu, víte, jak frustrující může být, když se čísla změní na prostý text. Tento průvodce tomuto úskalí předchází.

---

## Předpoklady – Nastavení vývojového prostředí

Než se pustíme do kódu, ujistěte se, že máte:

| Požadavek | Proč je důležité |
|-------------|----------------|
| .NET 6.0 nebo novější (tutorial používá .NET 6) | Moderní API a lepší výkon |
| Visual Studio 2022 (nebo VS Code s rozšířením C#) | Pohodlné editování a ladění |
| Aspose.Cells for .NET NuGet package | Knihovna, která poskytuje `HtmlSaveOptions` a `GridJsOptions` |
| Vzorek Excel souboru (`sample.xlsx`) nebo sešit, který vygenerujete v kódu | Zdroj, který budete převádět |

Instalujte Aspose.Cells pomocí následujícího příkazu v Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

> **Tip:** Pokud používáte CI pipeline, přidejte stejný řádek `dotnet add package` do svého build skriptu, aby byla závislost vždy přítomna.

---

## Krok 1: Načíst nebo vytvořit sešit

Můžete buď načíst existující soubor, nebo jej vytvořit programově. Zde je minimální příklad, který vytváří sešit s několika stylovanými buňkami, abyste viděli, že formátování přežije export.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Proč je to důležité:** Explicitním nastavením formátů čísel později uvidíte, jak `GridJsOptions.EnableNumberFormat` udržuje tyto formáty v HTML výstupu.

---

## Krok 2: Nakonfigurujte možnosti uložení HTML

Nyní vytvoříme instanci `HtmlSaveOptions`. Tento objekt říká Aspose.Cells přesně, jak má být HTML vykresleno.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Povolení formátování čísel v Grid.js

Pokud plánujete vložit HTML do stránky, která používá **Grid.js** pro interaktivní tabulky, budete chtít, aby čísla zůstala naformátovaná (např. měnové symboly, oddělovače tisíců). Následující řádek to přesně provede:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Co se děje pod kapotou?** `EnableNumberFormat` vloží malý JavaScriptový úryvek, který říká Grid.js, aby interpretoval atribut buňky `data-format`, čímž zachová Excel‑stylové formátování v prohlížeči.

---

## Krok 3: Uložte sešit jako soubor HTML

Sešitem připraveným a volbami vyladěnými, poslední řádek zapíše HTML soubor na disk.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Spuštěním programu vznikne soubor `gridjs.html`, který vypadá takto (zjednodušený pohled):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Otevřete soubor v libovolném prohlížeči a uvidíte pěkně stylovanou tabulku, kompletní s světle šedým pozadím hlavičky a formátováním měny. Pokud stránku vložíte do webu, který již načítá Grid.js, čísla se automaticky zobrazí se správnými čárkami a symboly.

---

## Časté úskalí při **konverzi Excelu do HTML**

| Problém | Proč k tomu dochází | Jak tomu předejít |
|-------|---------------|-----------------|
| **Ztracené vzorce** | HTML je statické; vzorce se změní na prosté hodnoty. | Pokud potřebujete živé výpočty, uchovejte sešit na serveru a použijte JavaScriptové knihovny jako SheetJS. |
| **Chybějící obrázky** | Obrázky jsou uloženy jako samostatné zdroje. | Nastavte `HtmlSaveOptions.ExportImagesAsBase64 = true`, aby se vložily přímo. |
| **Obrovské soubory** | Velké sešity generují obrovské HTML + JS. | Použijte `ExportOnlyVisibleSheets` nebo rozdělte do více stránek pomocí `HtmlSaveOptions.OnePagePerSheet`. |
| **Nesprávná lokalizace čísel** | Excel ukládá čísla v invariantní kultuře, prohlížeče mohou použít místní nastavení. | Explicitně nastavte `htmlOptions.Encoding = Encoding.UTF8` a použijte `GridJsOptions.EnableNumberFormat`. |

---

## Pokročilé: Export více listů s jednotlivými instancemi Grid.js

Pokud váš sešit obsahuje několik listů a chcete, aby se každý stal vlastní tabulkou Grid.js, můžete projít listy a uložit každý zvlášť:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Každý soubor bude obsahovat vlastní element `<table class="gridjs-table">`, připravený pro nezávislou manipulaci.

---

## Ověření výstupu – Rychlý kontrolní seznam

1. **Je styl zachován?** Porovnejte barvy pozadí buněk a okraje s původním zobrazením v Excelu.  
2. **Jsou formáty čísel zachovány?** Hledejte atribut `data-format` na elementech `<td>`.  
3. **Jsou obrázky zobrazeny?** Pokud jste exportovali obrázky jako Base64, měly by se zobrazit inline.  
4. **Je konzole prohlížeče čistá?** Žádné JavaScriptové chyby související s Grid.js.  

Pokud některá z těchto kontrol selže, vraťte se k odpovídající vlastnosti `HtmlSaveOptions` – většina problémů pramení z chybějícího příznaku.

---

## Závěr

Nyní máte solidní, produkčně připravenou metodu, jak **uložit Excel jako HTML** a zachovat každý styl, okraj i číselnou reprezentaci. Konfigurací `HtmlSaveOptions` a zapnutím `GridJsOptions.EnableNumberFormat` jste proměnili statický sešit na web‑přátelskou tabulku, která funguje bez problémů s Grid.js.

Stručně řečeno, tento tutoriál vám ukazuje, jak **převést Excel do HTML** a **exportovat Excel s formátováním** pomocí Aspose.Cells. Nebojte se experimentovat: vyzkoušejte různé motivy, vložte grafy nebo dokonce servírujte HTML přes ASP.NET endpoint pro konverzi za běhu.

---

## Co bude dál?

- **Prozkoumejte další exportní formáty**: PDF, PNG nebo CSV pomocí `Workbook.Save`.  
- **Integrujte s ASP.NET Core**: Vraťte HTML řetězec přímo z akce kontroleru.  
- **Kombinujte se SheetJS**: Načtěte vygenerované HTML zpět do JavaScriptového sešitu pro úpravy na klientovi.  

Pokud narazíte na problémy, zanechte komentář níže nebo si projděte dokumentaci Aspose.Cells pro podrobnější možnosti konfigurace. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak exportovat Excel do HTML s mřížkovými čarami pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Export Excel do HTML se zachováním stylů okrajů pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Převod HTML do Excelu pomocí Aspose.Cells .NET: Kompletní průvodce](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}