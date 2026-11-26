---
category: general
date: 2026-11-25
description: Export Excel do SVG pomocí Aspose.Cells v Javě – krok za krokem průvodce,
  jak uložit Excel jako SVG a vytvořit vektorový obrázek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: cs
lastmod: 2026-11-25
og_description: Exportujte Excel do SVG pomocí Aspose.Cells v Javě. Zjistěte, jak
  uložit Excel jako SVG a vytvořit vysoce kvalitní vektorové obrázky pomocí několika
  řádků kódu.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Export Excel do SVG v Javě – kompletní tutoriál Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Jak exportovat Excel do SVG pomocí Aspose.Cells v Javě
url: /cs/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat Excel do SVG pomocí Aspose.Cells v Javě

Pokud potřebujete **exportovat Excel do SVG**, tento průvodce vám ukáže, jak to provést pomocí Aspose.Cells pro Java. Naučíte se, jak **uložit Excel jako SVG** a vygenerovat vysoce kvalitní **vektorový obrázek** během několika řádků kódu.

Exportování sešitu Excel do souboru SVG vám umožní vložit list do webových stránek, reportů nebo jakéhokoli prostředí, které preferuje škálovatelnou grafiku. Formát SVG zachovává písma, barvy a okraje buněk bez pixelace, kterou získáte u rastrových obrázků.

## Požadavky

Než začnete, ujistěte se, že máte:

* Java 17 nebo novější nainstalovanou.
* Aktivní licenci Aspose.Cells pro Java (nebo dočasný evaluační klíč).
* Projekt Maven nebo Gradle, do kterého můžete přidat závislost Aspose.Cells.

Přidejte knihovnu Aspose.Cells do svého projektu:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Export Excel do SVG – krok za krokem

Proces se skládá ze tří jednoduchých kroků: načíst sešit, nakonfigurovat možnosti exportu SVG a uložit výsledek. Každý krok je vysvětlen níže.

### Krok 1: Načtěte sešit obsahující data

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Proč je to důležité:**  
`Workbook` je centrální objekt v Aspose.Cells. Načtení souboru jednou vám poskytne přístup ke všem listům, stylům a vloženým objektům, které později SVG exportér vykreslí.

### Krok 2: Nastavte možnosti exportu obrázku pro SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Proč je to důležité:**  
`ImageOrPrintOptions` vám umožňuje řídit výstupní formát. Výběrem `ImageFormat.SVG` zajistíte, že výsledek bude **vektorový obrázek** místo bitmapy. Povolení `OnePagePerSheet` zabraňuje zalomení stránek uvnitř listu, což je obvykle žádoucí, když bude SVG zobrazováno ve webovém prohlížeči.

### Krok 3: Uložte sešit jako soubor SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Proč je to důležité:**  
Metoda `save` kombinuje načtený sešit s nakonfigurovanými `exportOptions`. Volání zapíše plně kompatibilní SVG soubor, který lze otevřít v prohlížečích, Inkscape nebo jakémkoli editoru podporujícím vektorovou grafiku.

## Kompletní spustitelný příklad

Spojením tří kroků získáte samostatný program, který můžete okamžitě zkompilovat a spustit:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Očekávaný výstup**

Po spuštění programu se vypíše:

```
Export complete: Excel saved as SVG.
```

V adresáři `C:/Output` najdete soubor `WithVariationSelectors.svg`. Otevření souboru v prohlížeči zobrazí list jako škálovatelnou grafiku, přičemž text, okraje a barvy buněk zůstanou zachovány.

## Běžné varianty a okrajové případy

| Situace | Doporučená úprava |
|-----------|------------------------|
| **Více listů** | Procházejte `workbook.getWorksheets()` a pro každý list zavolejte `save`, případně připojte název listu k názvu souboru. |
| **Velké sešity** | Zvyšte `exportOptions.setRenderThreadCount(int)`, aby se použilo paralelní vykreslování a zkrátila se doba konverze. |
| **Vlastní DPI** | Zavolejte `exportOptions.setHorizontalResolution(int)` a `exportOptions.setVerticalResolution(int)` pro řízení měřítka viewBoxu SVG. |
| **Vkládání písem** | Nastavte `exportOptions.setExportFontAsSVG(true)`, aby se definice písem vložily přímo do SVG, což zajistí vizuální věrnost i na počítačích bez původních písem. |
| **Soubor chráněný heslem** | Při načítání poskytněte heslo: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Profesionální tipy

* **Vyhněte se rastrovému fallbacku** – Pokud list obsahuje složité grafy, ověřte, že se v SVG zobrazují jako vektorové elementy. Pokud ne, povolte `exportOptions.setExportChartAsSVG(true)`.
* **Výkon** – Pro hromadné konverze znovu použijte jednu instanci `ImageOrPrintOptions` místo vytváření nové pro každý soubor.
* **Testování** – Ověřte vygenerované SVG pomocí online validátoru (např. W3C SVG Validator), abyste včas zachytili případné chyby v markupu.

## Ověření konverze

Můžete programově potvrdit, že výstupní soubor je skutečně SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

Přítomnost kořenového elementu `<svg>` naznačuje úspěšnou **konverzi Excel do SVG**.

## Závěr

Tento tutoriál ukázal, jak **exportovat Excel do SVG** pomocí Aspose.Cells pro Java. Načtením sešitu, nastavením `ImageOrPrintOptions` pro SVG a voláním `save` můžete **uložit Excel jako SVG** a získat čistou **konverzi Excel do vektorového obrázku**. Nyní můžete SVG vložit do webových stránek, zahrnout jej do dokumentace nebo dále zpracovávat libovolným nástrojem pro vektorovou grafiku.

### Co zkoumat dál

* **Exportovat Excel jako PNG nebo JPEG** – změňte na `exportOptions.setImageFormat(ImageFormat.PNG)` pro rastrový výstup.
* **Převést Excel do PDF** – použijte `PdfSaveOptions` pro tisknutelné dokumenty.
* **Dávkové zpracování** – spojte výše uvedený kód s monitorováním souborového systému, aby se automaticky **konvertoval Excel do SVG** pro každý nový sešit ve složce.

Neváhejte experimentovat s možnostmi a nechte flexibilitu Aspose.Cells proměnit vaše data v Excelu na jakýkoli vizuální formát, který potřebujete. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak exportovat grafy Excelu jako SVG pomocí Aspose.Cells Java pro škálovatelnou vektorovou grafiku](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Jak vytvořit a uložit sešit Excel jako SVG pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Jak exportovat Excel do SVG – krok‑za‑krokem Java průvodce](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}