---
date: 2026-09-02
description: Naučte se, jak exportovat graf do PNG, přidat datové řady, kombinovat
  line column chart, uložit sešit jako XLSX a přidat legend chart pomocí Aspose.Cells
  for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Exportovat graf do PNG a přidat datové řady pro kombinovaný graf
og_description: Exportovat graf do PNG pomocí Aspose.Cells for Java, kombinovat line
  and column chart, přidat datové řady a uložit sešit jako XLSX v jednom tutoriálu.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Exportovat graf do PNG a přidat datové řady pro kombinovaný graf
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Exportovat graf do PNG a přidat datové řady pro kombinovaný graf
url: /cs/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportovat graf do PNG a přidat datové řady pro kombinovaný graf

V tomto tutoriálu **přidáte datové řady** do sešitu Excel, **zkombinujete prvky čárového a sloupcového grafu** a naučíte se, jak **exportovat graf do PNG** pomocí Aspose.Cells pro Java. Provedeme vás každým krokem – od nastavení sešitu, přidání grafu do listu, úpravy legendy, až po **uložení sešitu jako XLSX** a vytvoření PNG obrázku grafu. Na konci budete mít připravený kombinovaný graf, který můžete vložit do zpráv nebo dashboardů.

## Rychlé odpovědi
- **Která knihovna vytváří kombinované grafy?** Aspose.Cells for Java.  
- **Jak přidám datovou řadu?** Call `chart.getNSeries().add(...)` with the appropriate range.  
- **Jak mohu exportovat graf do PNG?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Do jakého formátu souboru mohu sešit uložit?** Standard `.xlsx` (save workbook as XLSX).  
- **Potřebuji licenci pro produkci?** Yes – a valid Aspose.Cells license is required for production deployments.

## Co je export grafu do PNG v Aspose.Cells?
Exportování grafu do PNG vytvoří rastrový obrázek grafu Excel, který lze zobrazit na webových stránkách, v reportech nebo e‑mailech, aniž by bylo nutné mít aplikaci Excel. Tato metoda zachytí přesné vizuální rozložení, barvy a datové značky a vytvoří přenosný soubor obrázku.

## Proč vytvořit kombinovaný čárový a sloupcový graf?
Kombinovaný čárový‑sloupcový graf vám umožní zobrazit různé datové sady s odlišnými vizuálními reprezentacemi (např. čárovou řadu nad sloupcovou řadou) v jednom zobrazení. Tento přístup je ideální pro porovnání trendů s celky, zvýraznění korelací nebo poskytování podrobnějších poznatků při zachování malého vizuálního prostoru.

## Požadavky
- Java Development Kit (JDK) 8 nebo vyšší  
- Aspose.Cells pro Java knihovna (stáhněte z níže uvedeného odkazu)  
- Základní znalost syntaxe Java a konceptů Excelu  

## Začínáme

Nejprve stáhněte knihovnu Aspose.Cells pro Java z oficiálního webu:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Jakmile je JAR přidán do classpath vašeho projektu, můžete začít vytvářet graf.

### Krok 1: importovat třídy aspose.cells
`Workbook` je jádrový objekt Aspose.Cells, který představuje celý soubor Excel v paměti.  
```java
import com.aspose.cells.*;
```

### Krok 2: vytvořit nový sešit
`Worksheet` představuje jednotlivý list uvnitř `Workbook` a poskytuje přístup k buňkám, řádkům a grafům.  
```java
Workbook workbook = new Workbook();
```

### Krok 3: přístup k prvnímu listu
`Chart` je objekt, který obsahuje všechna nastavení související s grafem, řady a možnosti vykreslování.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 4: přidat kombinovaný grafový objekt do listu  
Začneme s čárovým grafem a později přidáme sloupcovou řadu, abychom dosáhli efektu **kombinovaného čárového a sloupcového grafu**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Přidání dat do grafu

Nyní, když existuje kontejner grafu, musíme ho naplnit daty.

### Krok 5: definovat datové rozsahy a přidat datové řady
`NSeries` je kolekce, která ukládá každou datovou řadu pro graf. Přidání řady propojí rozsah buněk s grafem.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Tip:** První parametr (`"A1:A5"`) je rozsah pro první řadu a druhý (`"B1:B5"`) vytváří druhou řadu, která bude kombinována s první.

### Krok 6: nastavit data kategorie (X‑osa)
`CategoryAxis` představuje vodorovnou osu grafu, která řídí popisky zobrazované podél X‑osy.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Přizpůsobení grafu

Dobrý graf vypráví příběh. Přidejme mu názvy, popisky os a přehlednou legendu.

### Krok 7: nastavit popisky os grafu a název
`Title` nastavuje hlavní název grafu a objekty `Axis` představují osy X a Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Krok 8: přidat legendu grafu a upravit její pozici
`Legend` řídí umístění a vzhled legendy řad v grafu.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Ukládání a export grafu

Po přizpůsobení budete chtít **uložit sešit jako XLSX** a také vygenerovat obrázek.

### Krok 9: uložit sešit jako soubor Excel (XLSX)
`Workbook.save` zapíše sešit v paměti do souboru ve zvoleném formátu.  
```java
workbook.save("CombinedChart.xlsx");
```

### Krok 10: exportovat graf do PNG
`Chart.toImage` vykreslí graf jako soubor obrázku ve zvoleném formátu.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoda `chart.toImage` **generuje obrázky grafu Excel**, které lze použít na webových stránkách, v reportech nebo e‑mailech.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Nejsou zobrazeny žádná data** | Ověřte, že rozsahy buněk (`A1:A5`, `B1:B5`, `C1:C5`) skutečně obsahují data před vytvořením grafu. |
| **Legenda překrývá graf** | Nastavte `chart.getLegend().setOverlay(false)` nebo přesuňte legendu na jinou pozici (např. `RIGHT`). |
| **Soubor obrázku je prázdný** | Ujistěte se, že graf má alespoň jednu řadu a že `chart.toImage` je voláno po všech úpravách. |
| **Ukládání vyvolá výjimku** | Zkontrolujte, že máte oprávnění k zápisu do cílového adresáře a že soubor není otevřen v Excelu. |

## Často kladené otázky

**Q: Jak nainstaluji Aspose.Cells pro Java?**  
A: Stáhněte JAR z oficiálního webu a přidejte jej do classpath vašeho projektu. Odkaz ke stažení je: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Mohu vytvořit jiné typy grafů než čárový a sloupcový?**  
A: Ano, Aspose.Cells podporuje pruhové, koláčové, rozptylové, plošné a mnoho dalších typů grafů. Viz dokumentace API pro úplný seznam.

**Q: Je licence vyžadována pro produkční použití?**  
A: Platná licence Aspose.Cells je vyžadována pro produkční nasazení. K dispozici je bezplatná zkušební verze pro vyhodnocení.

**Q: Jak mohu změnit barvy jednotlivých řad?**  
A: Použijte `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (nebo podobně) po přidání řady.

**Q: Kde najdu více příkladů kódu?**  
A: Kompletní dokumentace a další ukázky jsou k dispozici na referenčním webu Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Poslední aktualizace:** 2026-09-02  
**Testováno s:** Aspose.Cells pro Java nejnovější verze  
**Autor:** Aspose

## Související tutoriály

- [Jak přidat popisky do grafů Excel pomocí Aspose.Cells pro Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Jak vytvořit graf Excel s trendovou čárou a exportovat do obrázku pomocí Aspose.Cells pro Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Exportovat grafy Excel do PDF pomocí Aspose.Cells pro Java: Průvodce vlastními velikostmi stránek](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}