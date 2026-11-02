---
date: '2026-09-27'
description: Naučte se, jak vytvořit koláčový graf v Javě pomocí Aspose.Cells. Podrobný
  návod krok za krokem, jak přizpůsobit koláčový graf v Excelu, nastavit Maven závislost
  a generovat profesionální grafy.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Vytvořte koláčový graf v Javě pomocí Aspose.Cells pro Javu. Naučte
  se přizpůsobit koláčový graf v Excelu, přidat Maven závislost a během minut generovat
  profesionální grafy.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Vytvořte koláčový graf v Javě s Aspose.Cells – Kompletní průvodce Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Jak vytvořit koláčový graf v Javě s Aspose.Cells
url: /cs/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit koláčový graf v Javě pomocí Aspose.Cells

## Úvod
Vytváření **pie chart** programově často připomíná hádanku, zejména když potřebujete detailní kontrolu nad barvami, legendami a nadpisy. V tomto průvodci se naučíte, jak **create pie chart java** pomocí Aspose.Cells a poté přizpůsobit Excel **pie chart** tak, aby odpovídal vaší značce nebo stylu reportování. Provedeme vás nastavením prostředí, naplněním dat, generováním grafu a vizuálními úpravami – vše bez opuštění vašeho Java IDE.

**What you'll learn**
- Přidejte **Maven dependency Aspose.Cells** do svého projektu.
- Vytvořte sešit, naplňte buňky daty a vygenerujte **pie chart**.
- Použijte vlastní barvy, nadpisy a legendy v grafu.
- Exportujte sešit do souboru XLSX připraveného ke sdílení.

Před začátkem byste měli být obeznámeni se základní syntaxí Javy a mít nainstalovaný Maven nebo Gradle.

## Rychlé odpovědi
- **Which library creates pie charts in Java?** Aspose.Cells for Java.  
- **Do I need a license?** A free trial works for development; a paid license is required for production.  
- **What Maven coordinates are required?** `com.aspose:aspose-cells:24.10`.  
- **Can I change slice colors?** Yes, via the `setAreaColor` method on each series.  
- **Is the chart exportable to XLSX?** Absolutely—just call `workbook.save("output.xlsx")`.

## Co je pie chart v Excelu?
Pie chart vizualizuje jedinou datovou sérii jako poměrné výseče kruhu, což usnadňuje porovnání částí celku. Úhel každé výseče odpovídá její hodnotě vzhledem k celku, což umožňuje rychlý pohled na rozdělení napříč kategoriemi, jako je podíl na trhu, rozdělení rozpočtu nebo demografické procenta.

## Proč použít Aspose.Cells k vytvoření pie chart java?
Aspose.Cells podporuje více než 50 typů grafů a dokáže zpracovat listy s až jedním milionem řádků, aniž by načítal celý soubor do paměti. Tento výkonnostní náskok vám umožní generovat rozsáhlé reporty na skromném hardware, přičemž poskytuje detailní kontrolu nad vzhledem grafu, vazbou dat a exportními formáty, což z něj činí lepší volbu než mnoho open‑source knihoven.

## Požadavky
- **Java Development Kit (JDK)** 8 nebo novější.
- **IDE** jako IntelliJ IDEA nebo Eclipse.
- **Maven** nebo **Gradle** pro správu závislostí.
- Zkušební nebo zakoupená licence Aspose.Cells.

### Požadované knihovny a závislosti
Přidejte Maven artefakt Aspose.Cells do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Nebo ekvivalent pro Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Kroky získání licence
Aspose.Cells pro Java je komerční, ale můžete začít s bezplatnou zkušební verzí. Navštivte [stránku nákupu](https://purchase.aspose.com/buy) a získejte dočasný licenční klíč.

## Nastavení Aspose.Cells pro Java
Nejprve se ujistěte, že knihovna je ve vašem classpath. Po přidání závislosti můžete inicializovat API, jak je ukázáno níže.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Průvodce implementací

### Vytvoření a konfigurace sešitu
Třída `Workbook` představuje celý Excel soubor v paměti.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Krok 1: vytvořit instanci sešitu
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Tím se vytvoří nový, prázdný sešit, který můžete okamžitě začít naplňovat.

### Přístup nebo úprava buněk listu
Třída `Worksheet` představuje jeden list v sešitu, obsahující buňky, řádky a sloupce.  
Do listu zapíšete data, která napájejí **pie chart**.

#### Krok 2: získat první list a jeho buňky
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Naplněte buňky názvy kategorií a hodnotami, které graf použije.

### Vytvořit **pie chart**
`Chart` objekty vizualizují data v listu a podporují různé typy, jako jsou **pie**, sloupcové a čárové grafy.

#### Krok 3: přidat **pie chart** do listu
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Konfigurace sérií a dat **pie chart**
`Series` definuje rozsah dat a formátování pro graf, propojující buňky listu s vizuálními prvky.

#### Krok 4: nastavit sérii pro graf
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Nastavení vzhledu legendy a názvu grafu
Legenda grafu `Legend` zobrazuje názvy sérií a barvy, což pomáhá čtenářům identifikovat jednotlivé výseče.

#### Krok 5: přizpůsobit legendu a název grafu
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Přizpůsobení barev sérií grafu
`setAreaColor` nastavuje barvu výplně výseče série grafu pomocí RGB hodnoty.

#### Krok 6: změnit barvy segmentů **pie**
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Automatické přizpůsobení sloupců a uložení sešitu
`autoFitColumns` automaticky upravuje šířky sloupců tak, aby odpovídaly obsahu buněk.

#### Krok 7: upravit šířky sloupců a uložit soubor
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Běžné případy použití
- **Demographic analysis:** Zobrazit rozdělení populace napříč regiony.
- **Market‑share reporting:** Vizualizovat podíl každého konkurenta na první pohled.
- **Budget allocation:** Zvýraznit, jak jsou prostředky rozděleny mezi oddělení.

## Úvahy o výkonu
- Uvolněte objekty (`workbook.dispose()`), když již nejsou potřeba, aby se uvolnila nativní paměť.
- Pro obrovské datové sady použijte `WorkbookDesigner` ke streamování dat místo načítání všeho najednou.
- Profilujte pomocí Java Flight Recorder k odhalení případných úzkých míst při generování grafu.

## Často kladené otázky

**Q: Mohu v jednom sešitu vytvořit více **pie chart**?**  
A: Ano, opakujte kroky vytvoření grafu pro každý datový rozsah; každý graf je nezávislý.

**Q: Podporuje Aspose.Cells 3‑D **pie chart**?**  
A: Ano; při přidávání grafu nastavte typ grafu na `ChartType.PIE_3D`.

**Q: Jak použít vlastní téma na všechny grafy?**  
A: Použijte metodu `Workbook.setDefaultTheme` před vytvořením jakýchkoli grafů.

**Q: Do jakých formátů mohu exportovat sešit?**  
A: Do více než 30 formátů, včetně XLSX, CSV, PDF a HTML.

**Q: Je licence vyžadována pro komerční nasazení?**  
A: Ano, platná licence odstraňuje vodotisky z hodnocení a odemyká plnou funkčnost.

## Závěr
Nyní máte kompletní, end‑to‑end návod pro **create pie chart java** s Aspose.Cells. Dodržením výše uvedených kroků můžete generovat vylepšené Excel **pie chart**, přizpůsobit barvy a nadpisy a vložit je do jakéhokoli reportovacího řetězce. Prozkoumejte další typy grafů – sloupcové, čárové, radarové – a rozšiřte tak svou sadu nástrojů pro vizualizaci dat.

---

**Poslední aktualizace:** 2026-09-27  
**Testováno s:** Aspose.Cells 24.10 for Java  
**Autor:** Aspose

## Související tutoriály

- [Přizpůsobení popisků dat v Excel grafu pomocí Aspose.Cells pro Java&#58; Průvodce krok za krokem](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Vytvoření dynamických Excel grafů s Aspose.Cells Java&#58; Kompletní průvodce pro vývojáře](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Vytvoření a přizpůsobení Excel sešitů pomocí Aspose.Cells Java&#58; Průvodce krok za krokem](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}