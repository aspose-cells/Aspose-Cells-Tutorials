---
category: general
date: 2026-09-27
description: Nastavte oblast tisku v Excelu a naučte se exportovat PNG obrázky vybraných
  buněk. Tento průvodce také zahrnuje uložení rozsahu jako obrázku a přidání obrázku
  do listu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: cs
lastmod: 2026-09-27
og_description: Nastavte oblast tisku v Excelu a exportujte PNG pomocí Aspose.Cells.
  Postupujte podle tohoto krok‑za‑krokem návodu, jak uložit oblast jako obrázek a
  přidat obrázek do listu.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Nastavte oblast tisku v Excelu – export PNG v C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Jak nastavit tiskovou oblast v Excelu a exportovat PNG
url: /cs/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit oblast tisku v Excelu a exportovat PNG

Pokud potřebujete **set print area excel** před vytvořením obrázku, tento průvodce vám přesně ukáže, jak na to. Také se naučíte **how to export png** soubory z konkrétního rozsahu, **save range as image** a **add picture to worksheet** v jednom opakovatelném pracovním postupu.

Práce s Excelem programově často znamená, že chcete pouze podmnožinu buněk – například kontingenční tabulku nebo graf – převést na obrázek. Definováním oblasti tisku nejprve zajistíte, že exportovaný PNG obsahuje přesně buňky, které očekáváte, ani více, ani méně. Tento tutoriál vás provede každým krokem, od načtení sešitu až po uložení finálního PNG souboru, a vysvětlí, proč je každé nastavení důležité.

## Požadavky

* .NET 6.0 nebo novější nainstalováno  
* Visual Studio 2022 (nebo jakékoli C# IDE)  
* Balíček **Aspose.Cells for .NET** NuGet (`Install-Package Aspose.Cells`)  
* Excel soubor (`input.xlsx`) umístěný v známém adresáři  

Tyto požadavky zajišťují, že kód běží bez další konfigurace.

## Krok 1: Načtěte sešit, se kterým chcete pracovat

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Třída `Workbook` představuje celý Excel soubor. Načtením nejprve získáte přístup k listům, buňkám a možnostem nastavení stránky.

## Krok 2: **Set print area excel** pro cílový rozsah

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Nastavení **print area** říká Excelu (a Aspose.Cells), které buňky patří na tisknutelnou stránku. Když později exportujete list jako obrázek, bude vykreslena pouze tato oblast, což je nezbytné pro čistý **export selected cells image**.

## Krok 3: Nakonfigurujte možnosti exportu obrázku – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` řídí výstupní formát. Výběrem `ImageFormat.Png` zajistíte obrázek s vysokým rozlišením a průhledným pozadím, který dobře funguje ve webových i desktopových kontextech.

## Krok 4: Vytvořte obrázek z definovaného rozsahu a **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Metoda `Pictures.Add` vloží nový obrázek do listu. Předáním rozsahu vytvořeného v Kroku 2 **save range as image** přímo na list, což je užitečné, pokud později potřebujete odkazovat na obrázek v jiných částech sešitu.

## Krok 5: **Save the picture as an image file** – dokončení pracovního postupu **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Volání `Save` zapíše obrázek do souborového systému pomocí možností definovaných v Kroku 3. Výsledný soubor `selected_range.png` obsahuje přesně buňky definované příkazem **set print area excel**.

## Kompletní, spustitelný příklad

Složení všech částí dohromady vám poskytne kompaktní program, který můžete vložit do libovolné konzolové aplikace:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Očekávaný výstup

Running the program prints:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

A najdete soubor `selected_range.png`, který zobrazuje pouze buňky A1 až G20 z `input.xlsx`.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Exportovaný obrázek obsahuje celý list | Nebyla definována oblast tisku | Ujistěte se, že jste **set print area excel** před vytvořením obrázku |
| PNG je rozmazané | Výchozí DPI je nízké | Nastavte `imageOptions.DpiX` a `imageOptions.DpiY` na vyšší hodnotu (např. 300) |
| Chyba souboru nenalezen | Špatná cesta k adresáři | Použijte `Path.Combine` nebo dvojitě zkontrolujte, že složka existuje |
| Obrázek je posunut | Nesprávné indexy řádku/sloupce | První dva parametry `Pictures.Add` jsou buňka vlevo nahoře, kde je obrázek umístěn; ponechte je na `0,0` pro čistý export |

## Pro tip: Exportujte více rozsahů najednou

Pokud potřebujete **export selected cells image** pro několik oblastí, opakujte Kroky 2‑5 uvnitř smyčky a měňte `printArea` v každé iteraci. Nezapomeňte každému obrázku přiřadit jedinečný název souboru, jinak pozdější uložení přepíše předchozí soubor.

## Závěr

Nyní víte, jak **set print area excel**, nakonfigurovat **how to export png**, **save range as image** a **add picture to worksheet** pomocí Aspose.Cells. Toto komplexní řešení vám umožní převést jakýkoli blok buněk na vysoce kvalitní PNG pomocí několika řádků C# kódu.

Dále můžete zkoumat:

* Přidání okrajů nebo vodoznaků do exportovaného PNG (vyhledejte *add picture to worksheet* s formátováním)
* Přímý export do PDF pro tiskové zprávy (*export selected cells image* → PDF workflow)
* Automatizace procesu pro více sešitů v dávkovém úkolu

Neváhejte experimentovat s různými rozsahy, nastavením DPI nebo formáty obrázků, aby vyhovovaly potřebám vašeho projektu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Nastavit oblast tisku v Excelu a exportovat do PowerPointu – krok za krokem](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Exportovat oblast tisku Excelu do HTML pomocí Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Jak nastavit oblast tisku v Excelu pomocí Aspose.Cells pro .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}