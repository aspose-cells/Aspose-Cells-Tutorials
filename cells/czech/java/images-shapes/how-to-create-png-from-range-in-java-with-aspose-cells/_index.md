---
category: general
date: 2026-10-07
description: Naučte se, jak vytvořit PNG z rozsahu a exportovat data jako PNG v Javě.
  Tento průvodce vám ukáže, jak uložit obrázek rozsahu Excelu pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: cs
lastmod: 2026-10-07
og_description: Vytvořte PNG z oblasti v Javě a exportujte data jako PNG pomocí Aspose.Cells.
  Sledujte tento kompletní návod, jak okamžitě uložit obrázek oblasti Excelu.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Vytvořte PNG z rozsahu v Javě – podrobný návod Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak vytvořit PNG z rozsahu v Javě pomocí Aspose.Cells
url: /cs/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit PNG z rozsahu v Javě s Aspose.Cells

Pokud potřebujete **vytvořit PNG z rozsahu** v sešitu Excel, tento tutoriál vám přesně ukáže, jak na to. Na konci průvodce budete schopni **exportovat data jako PNG**, uložit obrázek rozsahu Excelu a znovu použít soubor v reportech nebo webových stránkách.

Uvidíte kompletní, spustitelný Java program, který načte sešit, vybere požadované buňky, vykreslí je jako PNG a uloží výsledek na disk. Žádné externí nástroje nejsou potřeba — Aspose.Cells vše zpracuje interně.

## Co tento tutoriál pokrývá

* Předpoklady a nastavení Maven pro Aspose.Cells
* Načtení sešitu, který obsahuje kontingenční tabulku nebo libovolný datový rozsah
* Definování přesného rozsahu buněk, který chcete převést
* Konfigurace možností obrázku pro výstup PNG
* Vykreslení rozsahu a uložení souboru PNG
* Běžné úskalí a tipy pro vysoce kvalitní obrázky

Po dokončení těchto kroků budete schopni **převést list na PNG** pro libovolný rozsah, ať už jde o jednoduchou tabulku nebo složitý kontingenční graf.

## Předpoklady

* Java 17 nebo novější (kód se kompiluje s JDK 11+)
* Maven 3.6+ (nebo Gradle, pokud dáváte přednost)
* Aspose.Cells pro Java 23.12 nebo novější — přidejte závislost uvedenou níže
* Existující soubor Excel (`PivotWithStyle.xlsx`), který obsahuje rozsah, který chcete zachytit

> **Tip:** Pokud nemáte licenci, můžete požádat o dočasný evaluační klíč od Aspose. Knihovna funguje v evaluačním režimu bez další konfigurace.

### Maven závislost

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Krok 1: Načtěte sešit, který obsahuje cílový rozsah

Prvním krokem je otevřít soubor Excel. Aspose.Cells načte soubor do paměti, aniž by vyžadoval Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Proč je to důležité*: Načtení sešitu vám poskytne přístup k listům, buňkám a vlastnostem nastavení stránky potřebným pro vykreslení.

## Krok 2: Přístup k listu, který obsahuje rozsah

Většina sešitů má výchozí list na indexu 0, ale můžete také použít název listu.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Pokud jsou vaše data na jiném listu, nahraďte `0` odpovídajícím indexem nebo použijte `workbook.getWorksheets().get("SheetName")`.

## Krok 3: Definujte rozsah buněk, který chcete převést

Můžete zadat libovolnou obdélníkovou oblast pomocí zápisu A1. V tomto příkladu zachytíme `A1:D15`, což může být kontingenční tabulka nebo běžný datový blok.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Hraniční případ*: Když rozsah zahrnuje sloučené buňky, Aspose.Cells automaticky rozšíří obrázek tak, aby zahrnoval sloučenou oblast.

## Krok 4: Připravte možnosti PNG obrázku

`ImageOrPrintOptions` vám umožňuje řídit formát, rozlišení a další podrobnosti vykreslování. Nastavením formátu uložení na PNG zajistíte bezztrátovou kvalitu.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Zvýšení DPI je užitečné, když zdrojové buňky obsahují malé písmo nebo detailní grafy.

## Krok 5: Omezte oblast vykreslování na vybraný rozsah

Při přiřazení rozsahu jako tiskové oblasti Aspose.Cells vykreslí pouze tyto buňky a ostatní list ignoruje.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Pokud tento krok přeskočíte, celý list bude rasterizován, což může plýtvat pamětí a vytvořit větší obrázek.

## Krok 6: Vykreslete rozsah a přidejte obrázek do listu (volitelné)

Pokud chcete vložit vygenerované PNG zpět do sešitu (pro účely náhledu), můžete jej přidat jako obrázek. Tento krok je volitelný pro čisté exportní scénáře.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Proč byste to mohli udělat*: Některé pracovní postupy vyžadují, aby byl obrázek součástí sešitu před distribucí, například vytvoření tisknutelné zprávy, která kombinuje nativní buňky a obrázky.

## Krok 7: Uložte PNG soubor na disk

Nakonec zapište obrázek do souboru. Metoda `save` respektuje formát specifikovaný v `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Po dokončení programu bude `PivotImage.png` obsahovat pixel‑dokonalý snímek buněk `A1:D15`.

### Očekávaný výstup

* Soubor pojmenovaný `PivotImage.png` umístěný v `YOUR_DIRECTORY`.
* Obrázek zobrazuje přesné rozložení, písma, barvy a okraje z vybraného rozsahu.
* Pokud zdrojový rozsah obsahuje kontingenční tabulku, vykreslený obrázek zahrnuje stejné stylování a vypočtené hodnoty, jak jsou zobrazeny v Excelu.

## Řešení běžných scénářů

### Export nespojitých rozsahů

Aspose.Cells nevykresluje nespojené rozsahy v jednom obrázku. Pro export více oblastí vytvořte samostatné obrázky pro každý rozsah a později je spojte pomocí knihovny pro zpracování obrázků (např. ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Ukládání velkého listu jako PNG

Vykreslení celého listu, který zahrnuje tisíce řádků, může spotřebovat značnou paměť. Omezte to tím, že:

* Snížíte DPI (`imageOptions.setResolution(72)`) pro menší soubor.
* Použijete `setPageCount` k omezení počtu vykreslených stránek.
* Exportujete jednu tiskovou stránku najednou pomocí `worksheet.getPageSetup().setPrintArea(...)`.

### Zachování vzorců buněk

PNG obrázek je rastrový formát; vzorce nejsou zachovány. Pokud následní uživatelé potřebují surová data, také exportujte rozsah jako CSV nebo JSON pomocí `Range.exportDataTable()`.

## Kompletní, spustitelný příklad

Níže je kompletní třída Java, kterou můžete zkopírovat a vložit do svého IDE. Nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou na vašem počítači.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Spusťte program pomocí `mvn compile exec:java` (nebo vašeho preferovaného nástroje). Po provedení otevřete `PivotImage.png` a ověřte výsledek.

## Závěr

Nyní víte, jak **vytvořit PNG z rozsahu** v Javě pomocí Aspose.Cells, efektivně **exportovat data jako PNG** a **uložit obrázek rozsahu Excelu** pro jakýkoli scénář reportování nebo sdílení. Kroky — načtení sešitu, definování rozsahu, konfigurace možností obrázku, nastavení tiskové oblasti a uložení souboru — pokrývají celý pracovní postup pro **převod listu na PNG** a **uložení buněk jako PNG**.

### Další kroky

* Experimentujte s různými hodnotami `Resolution` pro vyvážení kvality a velikosti souboru.
* Použijte `ImageOrPrintOptions.setTransparent(true)`, pokud potřebujete PNG s průhledným pozadím.
* Spojte více obrázků rozsahů do jednoho PDF pomocí `PdfSaveOptions` pro vícestránkové reporty.
* Prozkoumejte export do dalších rastrových formátů (JPEG, BMP) změnou `setSaveFormat`.

Neváhejte tento vzor přizpůsobit grafům, tabulkám nebo dokonce celým listům. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak exportovat list Excelu do PNG pomocí Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Převod Excelu na PNG pomocí Aspose.Cells pro Java: krok za krokem průvodce](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Vytvoření sjednoceného rozsahu v Excelu pomocí Aspose.Cells Java: komplexní průvodce](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}