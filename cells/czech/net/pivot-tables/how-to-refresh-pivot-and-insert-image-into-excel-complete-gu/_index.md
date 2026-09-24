---
category: general
date: 2026-04-07
description: Naučte se, jak během několika kroků obnovit kontingenční tabulku, vložit
  obrázek do Excelu a uložit sešit Excelu s místem pro obrázek.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: cs
og_description: Jak obnovit kontingenční tabulku v Excelu, vložit obrázek do Excelu
  a uložit sešit Excelu pomocí C# s placeholderem obrázku. Krok‑za‑krokem ukázkový
  kód.
og_title: Jak aktualizovat kontingenční tabulku a vložit obrázek do Excelu – kompletní
  průvodce
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak aktualizovat kontingenční tabulku a vložit obrázek do Excelu – kompletní
  průvodce
url: /cs/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak obnovit kontingenční tabulku a vložit obrázek do Excelu – Kompletní průvodce

Už jste se někdy zamysleli **jak obnovit kontingenční tabulku**, když se změní zdrojová data, a pak vložit čerstvý graf nebo obrázek tabulky přímo do stejného listu? Nejste v tom sami. V mnoha reportovacích řetězcích data žijí v databázi, kontingenční tabulka je načte a finální soubor Excelu musí zobrazovat nejnovější čísla jako obrázek – aby koncoví uživatelé nemohli omylem upravit zdroj.

V tomto tutoriálu projdeme přesně to: **jak obnovit kontingenční tabulku**, **vložit obrázek do Excelu** a nakonec **uložit sešit Excel** s použitím **zástupného obrázku**. Na konci budete mít jediný spustitelný C# program, který vše zvládne, a pochopíte, proč je každý řádek důležitý.

> **Pro tip:** Tento přístup funguje s Aspose.Cells 2024 nebo novějším, což znamená, že na serveru nemusíte mít nainstalovaný Excel.

---

## Co budete potřebovat

- **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`).  
- .NET 6.0 SDK nebo novější (kód se také kompiluje s .NET 8).  
- Základní soubor Excel (`input.xlsx`), který již obsahuje kontingenční tabulku a zástupný obrázek (první objekt obrázku na listu).  
- Trochu zvědavosti ohledně modelů objektů Excelu.

Žádné extra COM interop, žádná instalace Office, jen čisté C#.

---

## Jak obnovit kontingenční tabulku a zachytit nejnovější data

První věc, kterou musíte udělat, je říct Excelu (nebo spíše Aspose.Cells), že kontingenční tabulka má přepočítat na základě nejnovějšího zdrojového rozsahu. Přeskočení tohoto kroku vás nechá s zastaralými čísly, což podkopává celý smysl automatizace.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Proč je to důležité:**  
Když zavoláte `Refresh()`, engine kontingenční tabulky znovu spustí svou agregační logiku. Pokud později exportujete kontingenční tabulku jako obrázek, obrázek zobrazí *aktuální* součty, ne ty z posledního uložení souboru.

---

## Vložení obrázku do Excelu pomocí zástupného obrázku

Nyní, když je kontingenční tabulka čerstvá, musíme ji převést na statický obrázek. To je užitečné, když chcete zamknout vizuál pro distribuci nebo jej později vložit do snímku PowerPointu.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

Objekt `ImageOrPrintOptions` vám umožňuje řídit rozlišení, pozadí a formát. PNG je bezztrátový a skvěle funguje pro většinu obchodních reportů.

---

## Přidání zástupného obrázku do listu

Většina šablon Excelu již obsahuje tvar nebo obrázek, který funguje jako „slot“ pro dynamické grafiky. Pokud žádný nemáte, stačí vložit prázdný obrázek v Excelu a uložit šablonu – Aspose.Cells jej zpřístupní jako `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**Co když máte více zástupných obrázků?**  
Stačí změnit index (`Pictures[1]`, `Pictures[2]`, …) nebo projít `worksheet.Pictures` a najít ten podle názvu.

---

## Uložení sešitu Excel po úpravách

Nakonec změny uložíme. Sešit nyní obsahuje obnovenou kontingenční tabulku, čerstvě vygenerovaný PNG a zástupný obrázek aktualizovaný tímto obrázkem.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Když otevřete `output.xlsx`, uvidíte, že slot obrázku je vyplněn nejnovějším snímkem kontingenční tabulky. Žádné ruční kroky nejsou potřeba.

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní program připravený ke zkopírování a vložení. Obsahuje potřebné `using` direktivy, ošetření chyb a komentáře, které vysvětlují každý ne‑zřejmý řádek.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Očekávaný výsledek:**  
Otevřete `output.xlsx`. První objekt obrázku nyní ukazuje PNG obnovené kontingenční tabulky. Pokud změníte zdrojová data v `input.xlsx` a program spustíte znovu, obrázek se automaticky aktualizuje – žádné ruční kopírování‑vkládání není potřeba.

---

## Běžné varianty a okrajové případy

| Situace | Co změnit |
|-----------|----------------|
| **Multiple pivot tables** | Loop through `sheet.PivotTables` and refresh each, then pick the one you need for the image. |
| **Different image format** | Set `ImageFormat = ImageFormat.Jpeg` (or `Bmp`) in `ImageOrPrintOptions`. |
| **Dynamic placeholder selection** | Use `sheet.Pictures["MyPlaceholderName"]` instead of an index. |
| **Large workbooks** | Increase `Workbook.Settings.CalculateFormulaEngine` to `EngineType.Fast` for quicker refreshes. |
| **Running on a headless server** | Aspose.Cells works fully without UI, so no extra configuration is required. |

---

## Často kladené otázky

**Q: Funguje to s makry podporovanými sešity (`.xlsm`)?**  
A: Ano. Aspose.Cells s nimi zachází jako s jakýmkoli jiným sešitem; makra jsou zachována, ale během obnovy nejsou spouštěna.

**Q: Co když kontingenční tabulka používá externí zdroj dat?**  
A: Musíte zajistit, aby připojovací řetězec byl na stroji, kde kód běží, platný. Voláním `pivotTable.CacheDefinition.ConnectionInfo` jej můžete programově upravit.

**Q: Můžu obrázek umístit do konkrétního rozsahu buněk místo zástupného obrázku?**  
A: Rozhodně. Použijte `sheet.Pictures.Add(row, column, pivotImg)`, kde `row` a `column` jsou indexy začínající nulou.

---

## Závěr

Probrali jsme **jak obnovit kontingenční tabulku**, **vložit obrázek do Excelu**, **přidat zástupný obrázek** a nakonec **uložit sešit Excel** – vše v přehledném C# úryvku. Obnovením kontingenční tabulky jako první zajistíte, že obrázek odráží nejnovější čísla, a použitím zástupného obrázku udržíte šablony čisté a znovupoužitelné.

Dále můžete zkoumat:

- Export stejného obrázku do PDF reportu (`PdfSaveOptions`).  
- Automatizaci dávky souborů s různými zdrojovými daty.  
- Použití Aspose.Slides k vložení PNG přímo do snímku PowerPointu.

Klidně experimentujte – vyměňte PNG za JPEG, změňte DPI nebo přidejte více obrázků. Hlavní myšlenka zůstává stejná: udržujte data čerstvá, zachyťte je jako obrázek a vložte tam, kde je potřebujete.

Šťastné programování! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}