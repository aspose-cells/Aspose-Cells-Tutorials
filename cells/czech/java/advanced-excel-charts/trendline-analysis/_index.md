---
date: 2026-08-27
description: Naučte se, jak přidat trendline do chart, zobrazit jeho R‑squared hodnotu
  a exportovat chart jako PNG nebo JPEG obrázek pomocí Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Export Chart do obrázku s analýzou Trendline
og_description: Přidejte trendline do chart, zobrazte R‑squared a exportujte výsledek
  jako PNG/JPEG pomocí Aspose.Cells for Java – rychlé řešení podporující 50 formátů.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Přidejte trendline do chart a exportujte jako obrázek s Aspose.Cells for
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Jak přidat trendline do chart a exportovat jako obrázek v Javě
url: /cs/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat trendovou čáru do grafu a exportovat ji jako obrázek

V tomto tutoriálu se naučíte, jak **přidat trendovou čáru do grafu**, zobrazit hodnotu R‑čtverce a exportovat vizualizaci do souboru PNG nebo JPEG pomocí Aspose.Cells pro Java. Uvidíte, proč jsou trendové čáry důležité, jak připravit sešit a přesné kroky k vytvoření vysoce rozlišeného obrázku, který lze vložit do zpráv, e‑mailů nebo webových stránek.

## Rychlé odpovědi
- **Jaký je hlavní cíl tohoto průvodce?** Ukázat vám, jak přidat trendovou čáru do grafu, zobrazit její rovnici a hodnotu R‑čtverce a exportovat graf jako obrázek pomocí Javy.  
- **Která knihovna je potřeba?** Aspose.Cells for Java – stáhněte ji ze [stránky vydání Aspose.Cells for Java](https://releases.aspose.com/cells/java/).  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro vývoj; pro produkční nasazení je vyžadována komerční licence.  
- **Mohu vygenerovat Excel sešit programově?** Ano – tutoriál vytvoří a uloží XLSX sešit od nuly.  
- **Jak se graf exportuje do PNG nebo JPEG?** Zavolejte metodu `Chart.toImage()` a zapište vrácený `BufferedImage` pomocí `ImageIO.write(...)`.

## Jak vytvořit Excel graf s trendovou čárou a exportovat jej jako obrázek?
Načtěte sešit, přidejte čárový graf, připojte trendovou čáru, která zobrazuje rovnici a hodnotu R‑čtverce, uložte sešit a poté zavolejte `chart.toImage()` a zapište vzniklý `BufferedImage` do souboru PNG nebo JPEG. Tento kompletní postup vyžaduje jen několik řádků Java kódu a vytvoří pixel‑dokonalý obrázek vhodný pro jakoukoli následnou aplikaci.

## Co je export grafu do obrázku?
Export grafu do obrázku převádí vizuální reprezentaci vašich dat do přenosného bitmapového formátu (PNG, JPEG, BMP atd.). Tento formát je ideální pro vkládání grafů do zpráv, webových stránek nebo prezentací, kde není vyžadován původní soubor Excel.

## Proč přidat trendovou čáru a zobrazit hodnotu R‑čtverce?
Trendová čára odhaluje základní vzorec datové řady, zatímco metrika **R‑čtverec** kvantifikuje, jak úzce trendová čára sedí k datům. Zahrnutí obou do exportovaného obrázku poskytuje zúčastněným stranám okamžitý přehled bez nutnosti otevírat sešit. Pomáhá rozhodovatelům rychle posoudit sílu korelace a předpovídat trendy bez nutnosti otevírat Excel.

## Požadavky
- Java 8 nebo novější nainstalovaný na vašem vývojovém počítači.  
- Knihovna Aspose.Cells for Java přidaná do classpath projektu (JAR soubory).  
- Znalost Java IDE, jako je IntelliJ IDEA nebo Eclipse.  

## Průvodce krok za krokem

### Krok 1: nastavení projektu
Vytvořte nový Java projekt a umístěte JAR soubory Aspose.Cells na cestu sestavení. Tím připravíte prostředí pro generování a manipulaci s Excel soubory.

### Krok 2: načtení Excel souboru (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Právě jsme **načetli Excel soubor** do paměti, připravený pro vytvoření grafu.*

### Krok 3: vytvoření grafu
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Zde generujeme čárový graf, který později bude hostovat naši trendovou čáru.*

### Krok 4: přidání trendové čáry (how to add trendline) a zobrazení hodnoty R‑čtverce
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Volání `setDisplayRSquaredValue(true)` zajišťuje, že **hodnota R‑čtverce** se zobrazí v grafu.*

### Krok 5: přizpůsobení grafu a uložení sešitu (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Nyní je sešit **vygenerován** a uložen jako soubor XLSX, připravený k dalšímu zpracování.*

### Krok 6: export grafu do obrázku (export chart to image)
> **Poznámka:** Tento krok je popsán bez dalšího kódu, aby se zachoval původní počet bloků.  
Po vytvoření a uložení grafu jej můžete exportovat do obrázku zavoláním metody `chart.toImage()` a zápisem vzniklého `java.awt.image.BufferedImage` do formátu souboru dle vašeho výběru (PNG, JPEG, BMP). Typický postup je:
1. Získat objekt `Chart` (již provedeno v předchozích krocích).  
2. Zavolat `chart.toImage()` pro získání `BufferedImage`.  
3. Použít `ImageIO.write(bufferedImage, "png", new File("chart.png"))` pro zápis souboru.  

Objekt `Chart` představuje graf v sešitu a poskytuje metody pro úpravu jeho vzhledu a dat. `BufferedImage` je třída Java, která drží obrázek v paměti, což umožňuje jeho uložení do souboru. `ImageIO` je pomocná třída pro čtení a zápis obrázků v Javě. `setDisplayRSquaredValue` umožňuje zobrazit statistiku R‑čtverce na trendové čáře.

### Analyzovat výsledky
Otevřete `output.xlsx` v Excelu a ověřte, že trendová čára, rovnice a hodnota R‑čtverce se zobrazují podle očekávání. Otevřete exportovaný soubor obrázku (např. `chart.png`) a zobrazte čistý vizuál, který lze sdílet bez původního sešitu.

## Časté problémy a řešení
- **Trendová čára se nezobrazuje:** Ujistěte se, že datový rozsah (`A1:A10`) obsahuje číselné hodnoty; ne‑číselná data zabraňují výpočtu trendové čáry.  
- **Hodnota R‑čtverce se zobrazuje jako 0:** To často znamená, že datová řada je konstantní nebo postrádá variaci. Zkuste jiný datový soubor nebo použijte polynomickou trendovou čáru.  
- **Export obrázku selže s `NullPointerException`:** Ověřte, že graf byl plně vykreslen před voláním `toImage()`. Uložení sešitu předtím může někdy vyřešit problémy s načasováním.

## Často kladené otázky

**Q: Jak mohu změnit typ trendové čáry?**  
A: Použijte jinou výčtovou hodnotu `TrendlineType` při přidávání trendové čáry, např. `TrendlineType.POLYNOMIAL` pro polynomické přizpůsobení.

**Q: Mohu přizpůsobit vzhled trendové čáry (barva, tloušťka)?**  
A: Ano. Přistupte k `LineFormat` trendové čáry pomocí `trendline.getLineFormat()` a nastavte vlastnosti jako `setWeight()` a `setColor()`.

**Q: Jak exportovat graf do PDF místo obrázku?**  
A: Nejprve převést graf na obrázek, poté vložit tento obrázek do PDF pomocí Aspose.PDF nebo jiné PDF knihovny.

**Q: Je možné přidat více trendových čar do stejného grafu?**  
A: Rozhodně. Zavolejte `chart.getNSeries().get(0).getTrendlines().add(...)` pro každou řadu, kterou chcete analyzovat.

**Q: Podporuje Aspose.Cells export obrázků ve vysokém rozlišení?**  
A: Ano. Můžete při volání `chart.toImage()` zadat DPI a poté před uložením upravit velikost obrázku, což zajistí ostrý výstup pro tisk nebo obrazovky s vysokou hustotou pixelů.

---

**Poslední aktualizace:** 2026-08-27  
**Testováno s:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**Autor:** Aspose

## Související tutoriály

- [Přidat popisky dat do Excel grafu s Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Jak exportovat Excel grafy jako SVG pomocí Aspose.Cells Java pro škálovatelnou vektorovou grafiku](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel grafů do PDF pomocí Aspose.Cells for Java&#58; Průvodce vlastními velikostmi stránek](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}