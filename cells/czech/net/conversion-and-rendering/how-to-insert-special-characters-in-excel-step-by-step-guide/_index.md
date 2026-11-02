---
category: general
date: 2026-06-21
description: Naučte se vkládat speciální znaky do Excelu a exportovat list Excelu
  do SVG pomocí C#. Obsahuje Unicode symboly, XPS a export do SVG.
draft: false
keywords:
- how to insert special characters in excel
- export excel sheet to svg
- insert unicode symbol into excel
- use unicode characters in excel cells
language: cs
og_description: Objevte, jak vložit speciální znaky v Excelu, používat Unicode symboly
  v buňkách a exportovat svůj list do SVG s kompletním příkladem kódu.
og_title: Jak vložit speciální znaky v Excelu – kompletní C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to insert special characters in Excel and export Excel sheet
    to SVG using C#. Includes Unicode symbols, XPS, and SVG export.
  headline: How to Insert Special Characters in Excel – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to insert special characters in Excel and export Excel sheet
    to SVG using C#. Includes Unicode symbols, XPS, and SVG export.
  name: How to Insert Special Characters in Excel – Step‑by‑Step Guide
  steps:
  - name: You’ll see the three symbols side by side.
    text: You’ll see the three symbols side by side.
  - name: Zoom in—no fuzziness, because SVG is vector‑based.
    text: Zoom in—no fuzziness, because SVG is vector‑based.
  - name: If a symbol looks like a box, double‑check the font you set in Step 3.
    text: If a symbol looks like a box, double‑check the font you set in Step 3.
  type: HowTo
tags:
- excel
- unicode
- aspnet
- aspocells
title: Jak vložit speciální znaky v Excelu – průvodce krok za krokem
url: /cs/net/conversion-and-rendering/how-to-insert-special-characters-in-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit speciální znaky v Excelu – kompletní C# tutoriál

Už jste se někdy zamysleli **jak vložit speciální znaky v Excelu** bez kopírování a vkládání z webové stránky? Nejste v tom sami. V mnoha reportovacích scénářích potřebujete hudební notu, znak ochranné známky nebo dokonce selektor variant přímo v buňce a pak chcete tento list sdílet jako vektorovou grafiku.  

V tomto průvodci vás provedeme praktickým řešením, které zahrnuje **jak vložit speciální znaky v Excelu**, ukáže vám, jak **exportovat list Excelu do SVG**, a vysvětlí nuance **používání Unicode znaků v buňkách Excelu**. Na konci budete mít připravený C# projekt, který vše zvládne během několika řádků kódu.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Core 3.1+)  
- Visual Studio 2022 (nebo jakékoli jiné IDE)  
- **Aspose.Cells for .NET** – komerční knihovna, která pracuje s Excel soubory bez nutnosti mít nainstalovaný Excel. Zkuste zdarma zkušební verzi na webu Aspose.  
- Základní znalost C# – nic složitého, jen dost na vytvoření konzolové aplikace.

> **Pro tip:** Pokud ještě nemáte licenci, vynechte volání `License`; knihovna bude i nadále fungovat v režimu hodnocení, ale na uložených souborech se objeví vodoznak.

## Krok 1: Vytvořte projekt a přidejte Aspose.Cells

Nejprve vytvořte nový konzolový projekt:

```bash
dotnet new console -n ExcelUnicodeDemo
cd ExcelUnicodeDemo
dotnet add package Aspose.Cells
```

Pak otevřete `Program.cs`. Na začátek přidejte potřebné `using` direktivy:

```csharp
using System;
using Aspose.Cells;
```

Pokud máte licenční soubor (`Aspose.Cells.lic`), načtěte jej hned po `using` příkazech:

```csharp
// Uncomment and adjust the path if you have a license
// var license = new License();
// license.SetLicense("Aspose.Cells.lic");
```

## Krok 2: Vytvořte sešit a získejte první list

Nyní vytvoříme nový sešit a získáme první list. Toto odpovídá prvním dvěma řádkům původního úryvku.

```csharp
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Step 3: Grab the default worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

Proč to děláme? Objekt `Workbook` představuje celý Excel soubor, zatímco `Worksheet` je plátno, kde žijí buňky. Začátek s čistým sešitem zaručuje, že naše Unicode znaky nebudou kolidovat s existujícím formátováním.

## Krok 3: Vložte Unicode symbol (nebo jakýkoli speciální znak) do buňky

Zde se děje kouzlo. Unicode znaky jsou vyjádřeny buď jako jediný kódový bod (např. `\u00AE` pro ®) nebo jako *surrogate pair* pro symboly mimo Basic Multilingual Plane (BMP). Hudební symbol G‑Clef (`𝄞`) je takový případ a potřebuje dva 16‑bitové jednotky: `\uD834\uDD1E`. Přidání selektoru variant (`\uFE00`) říká rendereru, aby použil alternativní glyfu.

```csharp
// Insert a musical symbol with a variation selector into cell A1
// \uD834\uDD1E = 𝄞 (musical G clef), \uFE00 = variation selector-1
sheet.Cells["A1"].PutValue("\uD834\uDD1E\uFE00");

// You can also insert simpler Unicode like the registered trademark sign:
sheet.Cells["B1"].PutValue("\u00AE"); // ®

// Or a heart symbol (U+2764) directly:
sheet.Cells["C1"].PutValue("\u2764"); // ❤
```

**Proč použít `PutValue`?** Automaticky detekuje datový typ a zapíše řetězec jako hodnotu buňky, přičemž Unicode znaky zůstávají nedotčeny. Kdybyste zkusili `PutValue((int)0x1D11E)`, Excel by to interpretoval jako číslo, ne jako glyfu.

### Okrajové případy a tipy

- **Podpora fontu:** Excel zobrazí znak jen tehdy, pokud vybraný font obsahuje požadovanou glyfu. Arial Unicode MS, Segoe UI Symbol nebo jakýkoli OpenType font s hudebními symboly funguje dobře. Font můžete nastavit programově:

  ```csharp
  var style = sheet.Cells["A1"].GetStyle();
  style.Font.Name = "Segoe UI Symbol";
  sheet.Cells["A1"].SetStyle(style);
  ```

- **Surrogate páry:** Vždy používejte syntaxi `\uXXXX\uXXXX` pro kódové body > U+FFFF. Jediný literál `\U0001D11E` funguje v C# 8.0+, ale může zmást starší kompilátory.

- **Selektory variant:** Ne všechny prohlížeče je respektují. Pokud se vám zobrazí chybějící glyfa, zkuste selektor vynechat nebo změnit font.

## Krok 4: Uložte sešit jako XPS (volitelné)

Uložení do XPS vám poskytne stránkovanou, připravenou k tisku reprezentaci, která zachová vektorovou kvalitu. Tento krok není nutný pro export do SVG, ale ukazuje všestrannost knihovny.

```csharp
// Save as XPS – useful for printing or PDF conversion later
string xpsPath = @"C:\Temp\Variations.xps";
workbook.Save(xpsPath, SaveFormat.Xps);
Console.WriteLine($"Workbook saved as XPS to {xpsPath}");
```

## Krok 5: Exportujte stejný sešit do SVG

A teď hvězda večera: **export excel sheet to SVG**. Každý list se stane samostatným SVG souborem, který zachová tvary, text i vložené obrázky jako vektorové elementy.

```csharp
// Export the first worksheet to SVG
string svgPath = @"C:\Temp\Variations.svg";
workbook.Save(svgPath, SaveFormat.Svg);
Console.WriteLine($"Worksheet exported as SVG to {svgPath}");
```

### Co SVG obsahuje

- **Textové uzly** s Unicode znaky (např. `<text>𝄞︎</text>`).  
- **Atributy stylu**, které mapují Excel fonty na CSS `font-family`.  
- **Škálovatelná geometrie**, takže můžete přibližovat bez pixelace.

Pokud otevřete výsledné SVG v prohlížeči, měli byste vidět hudební klíč, znak ® a srdce vykreslené ostře.

## Krok 6: Ověřte výstup

Spusťte program (`dotnet run`). Po dokončení přejděte do `C:\Temp`. Otevřete `Variations.svg` v Chrome nebo Edge:

1. Uvidíte tři symboly vedle sebe.  
2. Přibližte – žádná rozmazanost, protože SVG je vektorové.  
3. Pokud se některý symbol zobrazí jako čtvereček, zkontrolujte font nastavený v Kroku 3.

Pro XPS soubor můžete použít vestavěný Windows XPS Viewer. Stejné znaky by se měly objevit na stránce.

## Často kladené otázky a řešení problémů

| Otázka | Odpověď |
|----------|--------|
| *Mohu vložit emoji?* | Ano, emoji jsou jen Unicode kódové body (např. `\U0001F600` pro 😀). Ujistěte se, že font je podporuje, např. Segoe UI Emoji. |
| *Proč se symbol zobrazuje jako čtvereček?* | Výchozí font pravděpodobně neobsahuje požadovanou glyfu. Nastavte buňce font, který ji má (viz Krok 3). |
| *Musím mít nainstalovaný Excel na serveru?* | Ne. Aspose.Cells funguje zcela v řízeném kódu, což je důvod, proč je ideální pro automatizované pipeline. |
| *Mohu exportovat jen určitý rozsah jako SVG?* | Přímý export rozsahu není podporován, ale můžete rozsah zkopírovat do nového dočasného listu a ten exportovat. |
| *Existuje způsob, jak hromadně exportovat všechny listy?* | Projděte `workbook.Worksheets` a zavolejte `Save` s odlišným názvem souboru pro každý list. |

## Kompletní funkční příklad

Níže je celý, připravený ke zkopírování a vložení program. Uložte jej jako `Program.cs` v projektu, který jsme vytvořili dříve.

```csharp
using System;
using Aspose.Cells;

namespace ExcelUnicodeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Uncomment if you have a license file
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            // 1️⃣ Create a new workbook and get the first sheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Insert Unicode symbols
            // Musical G clef with variation selector
            sheet.Cells["A1"].PutValue("\uD834\uDD1E\uFE00");
            // Registered trademark sign
            sheet.Cells["B1"].PutValue("\u00AE");
            // Heart symbol
            sheet.Cells["C1"].PutValue("\u2764");

            // Optional: set a font that supports these glyphs
            var style = sheet.Cells["A1"].GetStyle();
            style.Font.Name = "Segoe UI Symbol";
            sheet.Cells["A1"].SetStyle(style);
            sheet.Cells["B1"].SetStyle(style);
            sheet.Cells["C1"].SetStyle(style);

            // 3️⃣ Save as XPS (optional)
            string xpsPath = @"C:\Temp\Variations.xps";
            workbook.Save(xpsPath, SaveFormat.Xps);
            Console.WriteLine($"Saved XPS: {xpsPath}");

            // 4️⃣ Export the worksheet to SVG
            string svgPath = @"C:\Temp\Variations.svg";
            workbook.Save(svgPath, SaveFormat.Svg);
            Console.WriteLine($"Exported SVG: {svgPath}");
        }
    }
}
```

**Očekávaný výstup** po spuštění programu:

```
Saved XPS: C:\Temp\Variations.xps
Exported SVG: C:\Temp\Variations.svg
```

Otevřete SVG soubor a uvidíte tři znaky zobrazené čistě.

## Závěr

Právě jsme probrali **jak vložit speciální znaky v Excelu**, ukázali **vložení Unicode symbolu do buněk Excelu** a představili spolehlivý způsob **exportu listu Excelu do SVG**. Hlavní body jsou:

- Používejte `PutValue` s správnými Unicode escape sekvencemi.  
- Nastavte font, který skutečně obsahuje požadované glyfy.  
- Aspose.Cells vám umožní ukládat přímo do XPS nebo SVG bez nutnosti Microsoft Office.  

Odtud můžete experimentovat s většími rozsahy, aplikovat podmíněné formátování na Unicode buňky nebo dokonce generovat grafy, které zahrnují speciální symboly. Možnosti jsou neomezené, když spojíte Unicode s vektorovými exporty.

Máte další otázky ohledně **using Unicode characters in Excel cells** nebo potřebujete pomoc s hromadným zpracováním? Zanechte komentář a šťastné programování!  

![příklad jak vložit speciální znaky v excelu](https://example.com/images/unicode-excel.png "příklad jak vložit speciální znaky v excelu")


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}