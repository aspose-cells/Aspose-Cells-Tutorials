---
category: general
date: 2026-09-24
description: Exportujte oblast Excelu jako obrázek v C# pomocí Aspose.Cells – krok
  za krokem průvodce pro uložení oblasti listu jako PNG nebo JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: cs
lastmod: 2026-09-24
og_description: Exportujte oblast Excelu jako obrázek v C# s Aspose.Cells. Naučte
  se, jak během několika minut převést libovolnou oblast listu, včetně kontingenčních
  tabulek, na PNG nebo JPEG.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Exportovat oblast Excelu jako obrázek pomocí C# – kompletní průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Jak exportovat oblast Excelu jako obrázek pomocí C# a Aspose.Cells
url: /cs/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat oblast Excelu jako obrázek pomocí C# a Aspose.Cells

Pokud potřebujete **exportovat oblast Excelu jako obrázek** v .NET aplikaci, tento návod vám ukáže kompletní, připravené řešení. Ať už publikujete dashboard, vkládáte kontingenční tabulku na webovou stránku nebo generujete miniaturu reportu, můžete libovolnou oblast listu převést na PNG (nebo JPEG) pomocí několika řádků C# kódu.

V tomto tutoriálu se naučíte:

* Načíst existující sešit (`Workbook` class)  
* Definovat přesnou oblast buněk, kterou chcete zachytit (`PrintArea`)  
* Nakonfigurovat možnosti exportu obrázku (`ImageOrPrintOptions`)  
* Uložit výsledný obrázek na disk  

Všechny předpoklady, okrajové případy a běžné úskalí jsou zde popsány, takže můžete kód přizpůsobit svým projektům bez překvapení.

## Požadavky

Než začnete, ujistěte se, že máte:

| Požadavek | Důvod |
|-----------|-------|
| **Aspose.Cells for .NET** (nejnovější verze) | Poskytuje API `Workbook`, `Worksheet` a `ImageOrPrintOptions` použité v příkladu. |
| **.NET 6.0 nebo novější** | Vzorový kód cílí na .NET 6, ale funguje s libovolnou verzí .NET Core/Framework, která podporuje Aspose.Cells. |
| **Platný Excel soubor** (např. `input.xlsx`) | Sešit, který chcete převést. |
| **Oprávnění k zápisu do výstupní složky** | Nutné pro úspěšné provedení `Save`. |

Aspose.Cells můžete nainstalovat přes NuGet:

```bash
dotnet add package Aspose.Cells
```

## Export oblasti Excelu jako obrázek – přehled procesu

Operace se skládá ze tří logických fází:

1. **Načíst** sešit z disku.  
2. **Definovat** oblast buněk, která se stane obrázkem (tzv. *print area*).  
3. **Exportovat** oblast pomocí `ImageOrPrintOptions` a zapsat soubor.

Každá fáze je dále rozebrána v samostatném kroku s úplným zdrojovým kódem a vysvětlením.

## Krok 1: Načíst sešit

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Proč je to důležité:**  
`Workbook` je vstupní bod pro všechny operace s Excelem. Načtení souboru jednou snižuje spotřebu paměti a umožňuje pozdější přístup k libovolnému listu.

## Krok 2: Přistoupit k cílovému listu

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Tip:** Pokud potřebujete konkrétní list podle názvu, nahraďte index výrazem `workbook.Worksheets["SheetName"]`. Tím se vyhnete chybám při změně rozložení sešitu.

## Krok 3: Definovat oblast, kterou chcete exportovat

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Proč nastavit `PrintArea`?**  
Aspose.Cells při vytváření obrázku vykresluje *print area*. Omezením na přesnou oblast se vyhnete nadbytečnému bílému prostoru a zlepšíte výkon.

### Alternativa: Exportovat celý list

Pokud chcete exportovat celý list, jednoduše vynechte přiřazení `PrintArea`. Aspose.Cells použije výchozí použité rozmezí listu.

## Krok 4: Nakonfigurovat možnosti exportu obrázku

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Vysvětlení klíčových vlastností:**

* `ImageFormat` – Určuje typ souboru (`Png`, `Jpeg`, `Bmp`, atd.). PNG je ideální pro grafy a text, protože zachovává ostré hrany.  
* `HorizontalResolution` / `VerticalResolution` – Řídí hustotu pixelů. Pro webové miniatury stačí 96 DPI; pro tiskové grafiky se doporučuje 300 DPI.  
* `PageOrientation` – Pomáhá, když je vybraná oblast širší než vysoká.

## Krok 5: Exportovat oblast do souboru obrázku

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Co se děje uvnitř:**  
Když je nastaveno `PrintArea`, Aspose.Cells vytvoří dočasný obrázek představující tuto oblast. Objekt `Pictures[0]` je následně uložen s použitím vámi zadaných možností.

### Zpracování listů bez obrázků

Pokud list ještě neobsahuje žádný obrázek (např. zcela nový soubor), můžete jej vytvořit za běhu:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Úplný, spustitelný příklad

Sestavením všech částí získáte samostatnou konzolovou aplikaci, kterou můžete zkopírovat, vložit a spustit:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Očekávaný výstup:**  
Soubor s názvem `range.png` se objeví v `YOUR_DIRECTORY`. Po otevření zobrazí přesně buňky od **A1 do G20** jako ostrý PNG obrázek.

## Běžné varianty a řešení okrajových případů

| Scénář | Úprava |
|--------|--------|
| **Export do JPEG** | Změňte `ImageFormat = ImageFormat.Jpeg` a volitelně nastavte `Quality = 90` (rozsah 0‑100). |
| **Více oblastí** | Zavolejte `sheet.Pictures.Add` pro každou oblast a uložte každý obrázek pod jiným názvem souboru. |
| **Velké listy** | Zvyšte `HorizontalResolution`/`VerticalResolution` jen pro potřebnou oblast, aby nedošlo k výkyvům paměti. |
| **Nebyl vygenerován žádný obrázek** | Ověřte, že `PrintArea` je správně naformátována (`"A1:G20"`). Neplatná adresa vede k prázdné kolekci `Pictures`. |
| **Ukládání do proudu** | Použijte `pic.Save(Stream, imgOptions)`, pokud potřebujete obrázek v paměti (např. pro odpověď v ASP.NET). |

## Profesionální tipy pro spolehlivý export obrázků

* **Ověřte oblast tisku** – Použijte parsování `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) pro programové vytváření oblastí a vyhněte se překlepům.  
* **Uvolňujte prostředky** – Zabalte `Workbook` do `using` bloku, pokud zpracováváte mnoho souborů, aby se nativní zdroje uvolnily co nejdříve.  
* **Dávkové zpracování** – Při exportu desítek oblastí opakovaně používejte jedinou instanci `ImageOrPrintOptions`, čímž snížíte režii alokace objektů.  
* **Bezpečnost vláken** – Objektům Aspose.Cells **není** thread‑safe. Vytvořte samostatný `Workbook` pro každé vlákno nebo synchronizujte přístup.

## Závěr

Nyní máte kompletní, připravenou metodu pro **export oblasti Excelu jako obrázek** pomocí C# a Aspose.Cells. Kroky – načtení sešitu, nastavení tiskové oblasti, konfigurace `ImageOrPrintOptions` a uložení obrázku – pokrývají jak „jak“, tak „proč“, což vám umožní přizpůsobit kód pro kontingenční tabulky, grafy nebo libovolný vlastní blok buněk.

Dále můžete zkusit:

* **Export oblasti Excelu jako obrázek** v jiných formátech (SVG, BMP) – další sekundární klíčové slovo k vyzkoušení.  
* **Vložení PNG do PDF** pomocí Aspose.PDF pro kompletní generování reportu.  
* **Automatizaci dávkových exportů** napříč více sešity pomocí jednoduché smyčky v konzoli.

Nebojte se experimentovat s různými rozlišeními, orientacemi a výstupními složkami. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}