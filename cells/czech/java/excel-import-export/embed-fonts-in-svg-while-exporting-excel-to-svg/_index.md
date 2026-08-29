---
category: general
date: 2026-08-14
description: Vkládejte písma do SVG při exportu Excelu do SVG pomocí Aspose.Cells.
  Naučte se, jak nastavit tiskovou oblast, nastavit tiskové možnosti a použít funkci
  WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: cs
lastmod: 2026-08-14
og_description: Vkládejte písma do SVG při exportu Excelu do SVG pomocí Aspose.Cells.
  Tento průvodce vám ukáže, jak nastavit oblast tisku, nakonfigurovat možnosti tisku
  a použít funkci WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Vložení fontů do SVG při exportu Excelu do SVG – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Vložit písma do SVG při exportu Excelu do SVG
url: /cs/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vkládání fontů do SVG při exportu Excelu do SVG

Pokud potřebujete **embed fonts in SVG while exporting Excel to SVG**, tento tutoriál vám přesně ukáže, jak to provést pomocí Aspose.Cells pro Java. Také se podíváme na to, jak **set print area**, **set print options**, a **use WRAPCOLS function** pro formátování dat bez ztráty rozvržení.

Provedete kompletní, spustitelný příklad, který načte existující sešit, použije vzorec `WRAPCOLS`, nakonfiguruje specifické možnosti obrázku pro SVG, určí oblast tisku a nakonec uloží soubor jako SVG s vloženými fonty. Není potřeba žádná externí dokumentace – stačí zkopírovat kód, spustit jej a prozkoumat vzniklé SVG.

## Vkládání fontů do SVG – konfigurace ImageOrPrintOptions

Vkládání fontů zajišťuje, že SVG se vykreslí přesně tak, jak vypadá v Excelu, i na počítačích, kde nejsou nainstalovány původní typy písma.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Proč je to důležité*: Když je povoleno `setEmbedFonts(true)`, Aspose.Cells zapíše data fontu přímo do sekce `<defs>` SVG. Výsledkem je samostatný soubor, který vypadá identicky ve všech prohlížečích a platformách.

## Export Excel do SVG – kompletní workflow

Následující kroky ilustrují celý proces od načtení sešitu až po uložení SVG souboru.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Očekávaný výstup**: `output.svg` se objeví v `YOUR_DIRECTORY`. Po otevření v prohlížeči zobrazí list se všemi vloženými fonty, data zabalená do tří sloupců (díky `WRAPCOLS`) a vykreslené jsou pouze buňky v rozsahu `A1:H30`.

## Nastavení oblasti tisku pro list

Definování oblasti tisku omezuje exportované SVG na konkrétní rozsah, což snižuje velikost souboru a zaměřuje prohlížeč na relevantní data.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tip*: Rozsah používá Excelovou notaci A1. Pokud potřebujete dynamický rozsah, můžete jej vypočítat programově pomocí `ws.getCells().getMaxDisplayRange()`.

## Nastavení možností tisku pro výstup SVG

Možnosti tisku řídí, jak Aspose.Cells převádí list na obrázek. Kromě vkládání fontů můžete upravit rozlišení, měřítko a rozvržení stránky.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Proč byste měli nastavit možnosti tisku*: Bez explicitních nastavení Aspose.Cells používá výchozí hodnoty, které mohou vynechat vkládání fontů nebo aplikovat nechtěný faktor měřítka, což vede k rozmazaným nebo nesprávně stylovaným SVG.

## Použití funkce WRAPCOLS pro zalamování dat ve sloupcích

`WRAPCOLS` je Excelový vzorec, který rozděluje vertikální rozsah do určeného počtu sloupců. Je užitečný, když chcete zobrazit dlouhý seznam v kompaktní mřížce.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Když je sešit uložen, Aspose.Cells vyhodnotí vzorec a vytvoří rozvržení ve třech sloupcích v definované oblasti tisku. Tato technika funguje pro libovolný rozsah – stačí upravit druhý argument na požadovaný počet sloupců.

## Kompletní spustitelný příklad

Níže je kompletní Java program, který můžete vložit do libovolného IDE. Ujistěte se, že máte knihovnu Aspose.Cells pro Java ve své classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Kroky ověření**

1. Spusťte program.  
2. Otevřete `output.svg` ve webovém prohlížeči.  
3. Potvrďte, že text používá stejný typ písma jako původní Excel soubor (fonty jsou vloženy).  
4. Ověřte, že se zobrazují pouze buňky v rozsahu `A1:H30` a že data z `A2:A10` jsou zobrazena ve třech sloupcích.

## Časté úskalí a jak se jim vyhnout

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Fonts are missing in the SVG | `setEmbedFonts(false)` or the font file is not accessible | Ensure `setEmbedFonts(true)` and that the font is installed on the machine running the code |
| WRAPCOLS does not evaluate | Calculation engine disabled | Call `workbook.calculateFormula()` before exporting, or let Aspose.Cells evaluate during save |
| Exported SVG is blank | Print area does not include any data | Double‑check the range passed to `setPrintArea` |
| SVG file is huge | No scaling applied, large image resolution | Adjust `imgOptions.setResolution(96)` or similar to control DPI |

## Pro tip: znovupoužití ImageOrPrintOptions pro více listů

Pokud váš sešit obsahuje několik listů, které potřebují identické nastavení SVG, vytvořte jedinou instanci `ImageOrPrintOptions` a přiřaďte ji každému listu v `PageSetup`. Tím snížíte spotřebu paměti a zajistíte konzistentní vkládání fontů ve všech exportovaných souborech.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Další kroky

* **Export do jiných vektorových formátů** – Změňte `ImageFormat.SVG` na `ImageFormat.PDF` pro PDF vysoké kvality.  
* **Dávkové zpracování** – Procházejte složku s `.xlsx` soubory a automaticky generujte SVG.  
* **Vlastní správa fontů** – Použijte `FontSettings` k načtení fontů z konkrétního adresáře, pokud systémové fonty nejsou dostačující.  

Ovládnutím **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options** a **use WRAPCOLS function** můžete automatizovat tvorbu vysoce kvalitních SVG pro reporty, dashboardy a webové vizualizace přímo z Excel dat. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}