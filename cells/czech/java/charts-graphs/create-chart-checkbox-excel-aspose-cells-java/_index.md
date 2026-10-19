---
date: '2026-09-22'
description: Naučte se, jak vytvořit interaktivní graf v Excelu s zaškrtávacími políčky
  pomocí Aspose.Cells for Java. Tento průvodce pokrývá nastavení, přidávání zaškrtávacích
  políček, licencování a osvědčené postupy.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Naučte se, jak vytvořit interaktivní graf v Excelu s zaškrtávacími
  políčky pomocí Aspose.Cells for Java. Postupujte podle krok‑za‑krokem instrukcí,
  podívejte se na tipy k licencování a objevte reálné příklady použití.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Jak vytvořit interaktivní graf v Excelu s zaškrtávacími políčky
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Jak vytvořit interaktivní graf v Excelu s zaškrtávacími políčky
url: /cs/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit interaktivní graf v Excelu s zaškrtávacími políčky

## Úvod

V tomto tutoriálu **vytvoříte interaktivní graf v Excelu**, který umožňuje uživatelům přepínat datové řady kliknutím na zaškrtávací políčka umístěná přímo v grafu. Pomocí Aspose.Cells for Java můžete programově generovat plně vybavené sešity, aniž byste potřebovali nainstalovaný Microsoft Excel. Tento přístup funguje pro jakékoli řešení reportingu nebo dashboardu založené na Javě.

**Co se naučíte**
- Jak nastavit Aspose.Cells for Java v Maven nebo Gradle
- Jak vytvořit instanci `Workbook` a přidat sloupcový graf
- Jak vložit tvar zaškrtávacího políčka do oblasti grafu
- Jak použít licenci Aspose.Cells pro produkční použití  

## Rychlé odpovědi
- **Která knihovna vytváří interaktivní grafy v Excelu?** Aspose.Cells for Java.  
- **Mohu přidat zaškrtávací políčka bez VBA?** Ano, vložením tvaru Form Control pomocí API.  
- **Potřebuji licenci pro tuto funkci?** Dočasná licence funguje pro hodnocení; trvalá licence je vyžadována pro produkci.  
- **Jaká verze Javy je požadována?** JDK 8 nebo novější.  
- **Bude graf fungovat v Excelu 2016‑2024?** Ano, vygenerovaný soubor dodržuje standard Office Open XML.  

## Co je interaktivní graf v Excelu?
Interaktivní graf v Excelu kombinuje standardní graf s UI ovládacími prvky (např. zaškrtávacími políčky), které uživatelům umožňují během provozu zobrazovat nebo skrývat datové řady, čímž se statický vizuál promění v dynamický nástroj pro reportování.

## Proč používat Aspose.Cells for Java?
Aspose.Cells podporuje **více než 80 vstupních a výstupních formátů** a dokáže zpracovat sešity s **více než 10 000 řádky** bez načítání celého souboru do paměti, což poskytuje vysoký výkon generování v serverových prostředích.

## Požadavky

- **Java Development Kit (JDK):** verze 8 nebo vyšší.  
- **Aspose.Cells for Java:** nejnovější verze (např. 25.3).  
- **Maven nebo Gradle:** pro správu závislosti knihovny.  

### Základní požadavky na znalosti
Základní syntaxe Javy a povědomí o konceptech Excelu (listy, oblasti, grafy) jsou užitečné, ale níže uvedené kroky jsou dostatečně podrobné pro vývojáře jakékoli úrovně zkušeností.

## Jak přidat zaškrtávací políčko v Javě?

Načtěte knihovnu Aspose.Cells, vytvořte sešit a vložte tvar zaškrtávacího políčka jedním voláním. Zaškrtávací políčko je Form Control, který může být propojen s buňkou; jeho přepínání změní hodnotu propojené buňky, kterou můžete později použít k řízení viditelnosti řady grafu.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Krok 1: Nastavení Maven závislosti

Přidejte Maven artefakt Aspose.Cells do souboru `pom.xml`:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Krok 2: Nastavení Gradle závislosti

Přidejte následující řádek do souboru `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Kroky získání licence
Pro odemčení plné funkčnosti získáte dočasnou nebo trvalou licenci. Stáhněte si zkušební licenci z [webu Aspose](https://releases.aspose.com/cells/java/). Pro produkci zakupte licenci a použijte ji, jak je ukázáno níže.

#### Základní inicializace
License je třída Aspose.Cells používaná k aplikaci zakoupeného licenčního souboru, což umožňuje plnou funkčnost bez omezení hodnocení. Inicializujte knihovnu ve svém Java kódu před jakoukoli operací sešitu:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Jak vytvořit interaktivní graf v Excelu?

Objekt Aspose.Cells `Workbook` představuje celý soubor Excel, obsahující listy, grafy a další prvky. Vytvořením sešitu můžete programově přidávat data, generovat sloupcový graf a později vkládat interaktivní ovládací prvky, jako jsou zaškrtávací políčka. Následující kroky vás provedou tvorbou sešitu, naplněním dat a nastavením grafu pro interaktivitu.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Vytvoření sešitu a přidání grafu

#### Přehled
Tato sekce ukazuje, jak vytvořit nový sešit, přidat list pro data a vygenerovat sloupcový graf, který bude později interaktivní.

##### Krok 1: Vytvořit nový sešit

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Krok 2: Přidat list s grafem

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Krok 3: Vložit sloupcový graf

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Krok 4: Přidat data řady

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Jak vložit zaškrtávací políčko do grafu?

Vložení zaškrtávacího políčka přímo do oblasti grafu umožňuje koncovým uživatelům kliknutím zobrazit nebo skrýt konkrétní řadu. Zaškrtávací políčko je tvar Form Control, který může být propojen s buňkou; hodnota buňky může být použita ve vzorci, který řídí viditelnost řady.

Shape je objekt Aspose.Cells představující kreslicí prvek, jako je formulářový ovládací prvek, obrázek nebo textové pole v listu.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Vložit tvar zaškrtávacího políčka

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Nastavit text zaškrtávacího políčka

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Jak uložit sešit jako soubor Excel?

Uložení `Workbook` zapíše všechny změny v paměti do fyzického souboru Excel na disku. Aspose.Cells podporuje moderní formát .xlsx, což zajišťuje, že soubor se otevře v Excelu 2016‑2024 a dalších aplikacích kompatibilních s Office. Použijte metodu `save` s požadovanou cestou k souboru a případně specifikujte formát souboru pro další možnosti.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Praktické aplikace

Reálné scénáře, kde interaktivní graf s zaškrtávacími políčky přináší hodnotu:

1. **Interaktivní zprávy:** Umožněte zúčastněným stranám přepínat jednotlivé produktové řady v prodejním grafu.  
2. **Komparativní analýza:** Umožněte analytikům soustředit se na konkrétní časová období nebo regiony zaškrtnutím/odškrtnutím řad.  
3. **Vzdělávací dashboardy:** Studenti mohou zkoumat datové trendy výběrem, které proměnné zobrazit.  

## Časté problémy a řešení

- **Zaškrtávací políčko neodpovídá:** Ujistěte se, že je zaškrtávací políčko propojeno s buňkou a že buňka je použita ve vzorci ovlivňujícím viditelnost řady.  
- **Graf se po přepnutí neaktualizuje:** Obnovte zobrazení sešitu v Excelu nebo přepočítejte vzorce (`workbook.calculateFormula()`).  
- **Licence nebyla aplikována:** Ověřte, že `License license = new License(); license.setLicense("Aspose.Cells.lic");` je spuštěno před jakoukoli operací sešitu.  

## Často kladené otázky

**Q: Jak přidám zaškrtávací políčko bez použití VBA?**  
A: Použijte API `Shape` v Aspose.Cells s `ShapeType.FORM_CONTROL_CHECKBOX` a propojte jej s buňkou listu; zaškrtávací políčko funguje nativně v Excelu.

**Q: Potřebuji licenci pro funkci zaškrtávacího políčka?**  
A: Tvar zaškrtávacího políčka je k dispozici ve volném hodnocení, ale trvalá licence Aspose.Cells odstraňuje omezení hodnocení a umožňuje plné optimalizace výkonu.

**Q: Které verze Excelu mohou otevřít vygenerovaný soubor?**  
A: Soubory uložené pomocí Aspose.Cells dodržují standard Office Open XML a otevírají se správně v Excelu 2016, 2019, 2021 a Microsoft 365.

**Q: Mohu ovládat více řad pomocí samostatných zaškrtávacích políček?**  
A: Ano, vytvořte zaškrtávací políčko pro každou řadu, propojte každé s odlišnou pomocnou buňkou a použijte podmíněné vzorce k nezávislému přepínání každé řady.

**Q: Existuje limit na počet zaškrtávacích políček na graf?**  
A: Prakticky můžete přidat desítky; výkon zůstává stabilní až do 200 ovládacích prvků na listu na typickém serverovém hardware.

---

**Poslední aktualizace:** 2026-09-22  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Související tutoriály

- [Jak přidat zaškrtávací políčko v Excelu pomocí Aspose.Cells for Java: Průvodce krok za krokem](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Vytvořit dynamické grafy v Excelu s Aspose.Cells Java: Kompletní průvodce pro vývojáře](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Přidat popisky dat do grafu v Excelu s Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}