---
category: general
date: 2026-10-10
description: Naučte se, jak exportovat oblast Excelu jako obrázek v Javě pomocí Aspose.Cells.
  Průvodce také zahrnuje export vybraných buněk jako obrázek a uložení listu Excelu
  jako obrázku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: cs
lastmod: 2026-10-10
og_description: Exportujte oblast Excelu jako obrázek v Javě s řešením krok za krokem.
  Obsahuje export vybraných buněk jako obrázek a uložení listu Excelu jako obrázek.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Exportovat oblast Excelu jako obrázek v Javě – kompletní průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Jak exportovat oblast Excelu jako obrázek v Javě pomocí Aspose.Cells
url: /cs/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat oblast Excelu jako obrázek v Javě s Aspose.Cells

Pokud potřebujete **exportovat oblast Excelu jako obrázek**, tento tutoriál vás provede kompletním řešením v Javě pomocí knihovny Aspose.Cells. Také se naučíte, jak **exportovat vybrané buňky jako obrázek** a jak **uložit list Excelu jako obrázek** pro účely reportování nebo dokumentace.

Exportování části sešitu do obrázku eliminuje potřebu nástrojů třetích stran pro snímání obrazovky a zaručuje pixel‑dokonalé výsledky. Na konci tohoto průvodce budete mít znovupoužitelnou metodu, která zapíše PNG (nebo jakýkoli podporovaný formát) přímo na disk, připravený k vložení do PDF, e‑mailů nebo webových stránek.

## Požadavky

Před zahájením se ujistěte, že máte:

* Java 17 nebo novější nainstalována.
* Maven 3.8+ (nebo jiný build nástroj, který dokáže zpracovat Maven závislosti).
* Licence Aspose.Cells pro Java (bezplatná zkušební verze funguje, ale přidává vodoznak).
* Ukázkový soubor Excel (`input.xlsx`) umístěný v známém adresáři.

Následující sekce předpokládají, že jste obeznámeni se základním vývojem v Javě a nastavením Maven projektu.

## Krok 1: Přidejte Aspose.Cells do svého projektu

Přidejte Maven závislost Aspose.Cells do svého `pom.xml`. Tato knihovna poskytuje třídy `Workbook`, `Worksheet` a `ImageOrPrintOptions`, které jsou použity v ukázkovém kódu.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Tip:** Udržujte číslo verze aktuální; novější vydání přidávají podporu formátů a vylepšení výkonu.

## Krok 2: Vytvořte pomocnou metodu pro export oblasti

Zabalení logiky exportu do metody usnadňuje opakované použití napříč projekty a řešení okrajových případů, jako jsou sloučené buňky nebo skryté řádky.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Proč je tato metoda důležitá

* **Oddělení odpovědností:** Načítání, konfigurace možností a export jsou jasně odděleny.
* **Flexibilita:** Můžete změnit formát obrázku nebo DPI, aniž byste zasahovali do hlavní logiky.
* **Zpracování chyb:** Vyhození `Exception` umožňuje volajícímu rozhodnout, zda logovat, opakovat nebo ukončit.

## Krok 3: Zavolejte metodu s reálnými parametry

Níže je minimální metoda `main`, která ukazuje, jak **exportovat vybrané buňky jako obrázek** a také jak **uložit list Excelu jako obrázek** pomocí celé oblasti listu.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Očekávaný výstup

Spuštěním programu se vytvoří dva PNG soubory:

* `range.png` – obrázek, který obsahuje pouze buňky **A1:G20**.
* `full_sheet.png` – obrázek celé použité oblasti prvního listu, efektivně **ukládá list Excelu jako obrázek**.

Soubory můžete otevřít v libovolném prohlížeči obrázků a ověřit, že vizuální rozložení odpovídá zobrazení v Excelu, včetně okrajů buněk, barev a sloučených buněk.

## Krok 4: Řešte běžné okrajové případy

### 1. Sloučené buňky

Aspose.Cells automaticky zachovává vzhled sloučených buněk, ale pokud potřebujete řídit vykreslování, nastavte `options.setOnePagePerSheet(true)`, aby se celý list před exportem vynutil na jednu stránku.

### 2. Skryté řádky nebo sloupce

Ve výchozím nastavení nejsou skryté řádky/sloupce vykresleny. Pro jejich zahrnutí povolte:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Velké oblasti a spotřeba paměti

Exportování velmi velkých oblastí může spotřebovat značnou paměť. Pokud narazíte na `OutOfMemoryError`, zvažte:

* Snížení DPI (`options.setHorizontalResolution(150)`).
* Exportování oblasti po menších částech a následné spojení obrázků pomocí grafické knihovny.

## Krok 5: Ověřte výsledek programově (volitelné)

Pokud váš následný proces potřebuje potvrdit, že obrázek byl vygenerován správně, můžete načíst PNG pomocí `javax.imageio.ImageIO` a zkontrolovat jeho rozměry:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Nenulová šířka a výška indikují úspěšný export.

## Závěr

Nyní víte, jak **exportovat oblast Excelu jako obrázek** v Javě, jak **exportovat vybrané buňky jako obrázek** a jak **uložit list Excelu jako obrázek** pomocí Aspose.Cells. Znovupoužitelná metoda `exportRangeAsImage` abstrahuje složitost, umožňuje kontrolovat kvalitu obrázku a funguje s libovolným indexem listu nebo oblastí buněk.

Další kroky, které můžete prozkoumat:

* Převést PNG do PDF pomocí Aspose.PDF pro reportování.
* Hromadně zpracovat více sešitů v adresáři.
* Integrovat export obrázku do Spring Boot REST endpointu, aby klienti mohli požadovat obrázky na vyžádání.

Neváhejte experimentovat s různými formáty obrázků (`ImageFormat.JPEG`, `ImageFormat.BMP`) a nastavením DPI, abyste splnili vizuální požadavky svého projektu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Exportovat sešit Excel jako obrázek pomocí Aspose.Cells pro Java: krok za krokem](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Jak vytvořit graf Excel s trendovou čarou a exportovat jej jako obrázek pomocí Aspose.Cells pro Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Exportovat buňky Excelu do obrázku pomocí Aspose.Cells .NET: krok za krokem](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}