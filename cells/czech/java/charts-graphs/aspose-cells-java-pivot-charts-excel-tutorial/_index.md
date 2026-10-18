---
date: '2026-07-07'
description: Naučte se pomocí příkladu Aspose Cells chart example vytvořit dynamické
  kontingenční grafy v Excelu pomocí Java. Postupujte podle krok‑za‑krokem návodu
  pro plynulou analýzu dat.
keywords:
- aspose cells chart example
- how to create pivot chart
- dynamic pivot chart excel
- export pivot chart excel
- add pivot chart workbook
og_description: Naučte se pomocí příkladu Aspose Cells chart example vytvořit dynamické
  kontingenční grafy v Excelu pomocí Java. Postupujte podle krok‑za‑krokem návodu
  pro plynulou analýzu dat.
og_title: 'Aspose Cells Chart Example: Ovládání kontingenčních grafů v Java'
schemas:
- author: Aspose
  dateModified: '2026-07-07'
  description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  headline: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  type: TechArticle
- description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  name: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  steps:
  - name: Load the Source Workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory.
  - name: Add a Worksheet for the Pivot Chart
    text: Create a dedicated chart sheet to keep the visual separate from raw data.
  - name: Insert a Pivot Table
    text: First, define the data range for the pivot table, then add it to the chart
      sheet. The `PivotTable` class represents a pivot table in a worksheet and provides
      methods to define its data source, layout, and calculations.
  - name: Create and Configure the Pivot Chart
    text: The `Chart` class represents any Excel chart. Here we create a column chart
      linked to the pivot table.
  - name: Export the Workbook
    text: Save the workbook with the new pivot chart to an `.xlsx` file, or directly
      to PDF if you need a static report.
  type: HowTo
- questions:
  - answer: Yes, call `chart.toImage("chart.png", ImageFormat.PNG)` after configuring
      the chart.
    question: Can I export a pivot chart directly to an image file?
  - answer: The library can preserve existing VBA macros, but it does not create or
      modify them programmatically.
    question: Does Aspose.Cells support Excel macros in pivot charts?
  - answer: Absolutely—invoke `pivotTable.refreshData()` and then `chart.refresh()`
      to reflect the latest values.
    question: Is it possible to update the pivot chart after changing the source data?
  - answer: Over 40 types, including column, line, area, pie, radar, and stacked bar,
      all fully supported for pivot data.
    question: Which chart types are available for pivot charts?
  - answer: Yes, a purchased license removes evaluation limits and enables full feature
      set.
    question: Do I need a license to use the Maven/Gradle setup in production?
  type: FAQPage
title: 'Aspose Cells Chart Example: Ovládání kontingenčních grafů v Java'
url: /cs/java/charts-graphs/aspose-cells-java-pivot-charts-excel-tutorial/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Příklad grafu Aspose Cells: Ovládání kontingenčních grafů v Javě

V dnešním světě řízeném daty je převod surových čísel na jasné vizuální poznatky nezbytný. Tento tutoriál vám ukáže **aspose cells chart example**, který potřebujete k vytvoření dynamických kontingenčních grafů v Excelu pomocí Javy. Na konci tohoto průvodce budete schopni načíst sešit, přidat samostatný list s grafem, svázat kontingenční tabulku a exportovat výsledek – vše jen s několika řádky kódu.

## Rychlé odpovědi
- **Jaká je hlavní třída pro práci se soubory Excel?** `Workbook` představuje celý soubor Excel v paměti.  
- **Který Maven artefakt přidá Aspose.Cells do projektu?** `com.aspose:aspose-cells` (verze 25.3 nebo novější).  
- **Mohu vytvořit kontingenční graf bez licence?** Ano, bezplatná zkušební verze funguje pro vývoj, ale licence odstraňuje omezení hodnocení.  
- **Kolik typů grafů Aspose.Cells podporuje?** Více než 40 typů grafů, včetně čárových, sloupcových, koláčových a radarových.  
- **Jaký je nejrychlejší způsob exportu kontingenčního grafu do PDF?** Zavolejte `chart.toPdf("output.pdf")` po nastavení zdroje dat grafu.

## Co je kontingenční graf v Excelu?
**Kontingenční graf** je interaktivní vizuální reprezentace kontingenční tabulky, která uživatelům umožňuje dynamicky zkoumat agregovaná data. Pomocí Aspose.Cells můžete tyto grafy generovat programově bez otevření Excelu. Automaticky se aktualizuje, když se změní podkladová kontingenční tabulka, podporuje filtrování a lze jej přizpůsobit různými typy grafů, názvy a legendami, což z něj činí výkonný nástroj pro analýzu dat.

## Proč použít Aspose.Cells pro Javu k vytvoření kontingenčních grafů?
Aspose.Cells zpracovává **více než 50 vstupních a výstupních formátů** a dokáže pracovat se sešity obsahujícími **stovky listů**, přičemž spotřeba paměti zůstává pod 200 MB. Jeho API vytváří, upravuje a vykresluje grafy **za méně než 2 sekundy** pro typické datové sady o velikosti 10 KB, což jej činí ideálním pro server‑side reportování.

## Požadavky

- **Aspose.Cells for Java** verze 25.3 nebo novější.  
- Maven nebo Gradle build systém.  
- JDK 8 nebo novější a IDE jako IntelliJ IDEA, Eclipse nebo NetBeans.  
- Základní znalost Javy; znalost Excelu je výhodou, ale není povinná.

### Požadované knihovny a závislosti
- **Maven:** přidejte závislost Aspose.Cells (viz sekce *aspose cells maven setup* níže).  
- **Gradle:** zahrňte stejný artefakt ve vašem `build.gradle`.

### Kroky pro získání licence
- **Bezplatná zkušební verze:** začněte s bezplatnou zkušební verzou a prozkoumejte aspose cells chart example.  
- **Dočasná licence:** získejte dočasný klíč pro rozšířené testování.  
- **Nákup:** zakupte plnou licenci na [oficiálních stránkách Aspose](https://purchase.aspose.com/buy).

## Jak nastavit Aspose.Cells pro Javu

### Maven závislost (aspose cells maven nastavení)

Přidejte následující úryvek do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```

### Gradle závislost

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Základní inicializace
Po přidání závislosti inicializujte knihovnu, jak je ukázáno níže:

```java
// Initialize license (optional for trial)
License license = new License();
license.setLicense("Aspose.Cells.lic");

// Create a Workbook object – this loads or creates an Excel file.
Workbook workbook = new Workbook();
```

## Jak vytvořit kontingenční graf pomocí Aspose.Cells pro Javu?

Načtěte svá zdrojová data, vygenerujte kontingenční tabulku a svázete ji s grafem – vše během několika jednoduchých kroků. Proces zahrnuje načtení sešitu obsahujícího zdrojová data, vytvoření kontingenční tabulky pro jejich souhrn, přidání samostatného listu s grafem, svázání kontingenční tabulky s grafem, úpravu vzhledu grafu a nakonec uložení sešitu v požadovaném formátu.

### Krok 1: Načtení zdrojového sešitu
Třída `Workbook` je nejvyšší objekt Aspose.Cells, který představuje jeden soubor Excel v paměti.

```java
Workbook workbook = new Workbook("data.xlsx");
```

### Krok 2: Přidání listu pro kontingenční graf
Vytvořte samostatný list s grafem, aby byl vizuál oddělený od surových dat.

```java
int chartSheetIndex = workbook.getWorksheets().addChart("PivotChartSheet");
Worksheet chartSheet = workbook.getWorksheets().get(chartSheetIndex);
```

### Krok 3: Vložení kontingenční tabulky
Nejprve definujte rozsah dat pro kontingenční tabulku, poté ji přidejte na list s grafem.

Třída `PivotTable` představuje kontingenční tabulku v listu a poskytuje metody pro definování zdroje dat, rozvržení a výpočtů.

```java
int pivotTableIndex = chartSheet.getPivotTables().add("A1:D100", "PivotTable1", 0, 0);
PivotTable pivotTable = chartSheet.getPivotTables().get(pivotTableIndex);
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);   // Category
pivotTable.addFieldToArea(PivotFieldType.DATA, 1);  // Values
```

### Krok 4: Vytvoření a konfigurace kontingenčního grafu
Třída `Chart` představuje libovolný graf v Excelu. Zde vytvoříme sloupcový graf propojený s kontingenční tabulkou.

```java
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 5, 0, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
chart.getNSeries().add("=PivotTable1!$B$2:$B$5", true);
chart.setTitle("Sales by Region");
```

### Krok 5: Export sešitu
Uložte sešit s novým kontingenčním grafem do souboru `.xlsx`, nebo přímo do PDF, pokud potřebujete statickou zprávu.

```java
workbook.save("PivotChartResult.xlsx", SaveFormat.XLSX);
// Optional PDF export
workbook.save("PivotChartResult.pdf", SaveFormat.PDF);
```

## Praktické aplikace dynamických kontingenčních grafů

- **Finanční reportování:** Automatické generování čtvrtletních dashboardů, které se aktualizují při importu nových dat.  
- **Analýza prodeje:** Vizualizace regionálních trendů prodeje jedním API voláním.  
- **Řízení zásob:** Sledování úrovní zásob a objednávkových bodů v reálném čase.  
- **Zákaznické poznatky:** Kombinace demografických dat s historií nákupů pro interaktivní grafy.  
- **Projektové řízení:** Zobrazení alokace zdrojů a odchylek časového plánu pomocí kontingenčních grafů.

## Tipy pro výkon při velkých datových sadách

- **Správa paměti:** Po uložení zavolejte `workbook.dispose()` pro uvolnění nativních zdrojů.  
- **Dávkové operace:** Použijte `CellsHelper.copyRange` pro přesun velkých bloků dat místo smyček po jednotlivých buňkách.  
- **Líné načítání:** Při zpracování souborů větších než 100 MB povolte `LoadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby byla spotřeba paměti nízká.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Kontingenční tabulka neodráží nová data** | Obnovte kontingenční tabulku pomocí `pivotTable.refreshData()` před vytvořením grafu. |
| **Graf se zobrazuje prázdný** | Ujistěte se, že rozsah datového zdroje grafu odpovídá rozsahu výsledků kontingenční tabulky. |
| **Chyby nedostatku paměti u obrovských souborů** | Použijte `LoadOptions` s `MemorySetting.MEMORY_PREFERENCE` a zavřete listy, které již nepotřebujete. |

## Často kladené otázky

**Q: Mohu exportovat kontingenční graf přímo do souboru obrázku?**  
A: Ano, zavolejte `chart.toImage("chart.png", ImageFormat.PNG)` po nastavení grafu.

**Q: Podporuje Aspose.Cells makra Excelu v kontingenčních grafech?**  
A: Knihovna může zachovat existující VBA makra, ale nevytváří ani nemění je programově.

**Q: Je možné aktualizovat kontingenční graf po změně zdrojových dat?**  
A: Ano—vyvolejte `pivotTable.refreshData()` a poté `chart.refresh()`, aby se projevily nejnovější hodnoty.

**Q: Které typy grafů jsou k dispozici pro kontingenční grafy?**  
A: Více než 40 typů, včetně sloupcových, čárových, plošných, koláčových, radarových a skládaných pruhových, všechny plně podporované pro kontingenční data.

**Q: Potřebuji licenci pro použití Maven/Gradle nastavení v produkci?**  
A: Ano, zakoupená licence odstraňuje omezení hodnocení a umožňuje plnou sadu funkcí.

---

**Poslední aktualizace:** 2026-07-07  
**Testováno s:** Aspose.Cells 25.3 pro Javu  
**Autor:** Aspose  

## Zdroje

- [Dokumentace Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Stáhnout Aspose.Cells pro Javu](https://releases.aspose.com/cells/java/)
- [Zakoupit licenci](https://purchase.aspose.com/buy)
- [Bezplatná zkušební verze a dočasné licence](https://releases.aspose.com/cells/java/)
- [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

```java
import com.aspose.cells.Workbook;

// Load an existing workbook
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
```

```java
   import com.aspose.cells.Workbook;
   ```

```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
   ```

```java
   import com.aspose.cells.SheetType;
   import com.aspose.cells.Worksheet;
   ```

```java
   int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
   Worksheet sheet3 = workbook.getWorksheets().get(sheetIndex);
   sheet3.setName("PivotChart");
   ```

```java
   import com.aspose.cells.Chart;
   import com.aspose.cells.ChartType;
   ```

```java
   int chartIndex = sheet3.getCharts().add(ChartType.COLUMN, 0, 5, 28, 16);
   Chart chart = sheet3.getCharts().get(chartIndex);
   ```

```java
   chart.setPivotSource("PivotTable!PivotTable1");
   chart.setHidePivotFieldButtons(false);
   ```

```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   workbook.save(outDir + "/CPCBasedOnPTable_out.xls");
   ```

## Související tutoriály

- [Ovládání kontingenčních tabulek v Excelu pomocí Aspose.Cells pro Javu: Kompletní průvodce analýzou dat](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [Vytvoření sešitu a přidání grafů s Aspose.Cells pro Javu: Kompletní průvodce](/cells/java/charts-graphs/create-workbook-add-charts-aspose-cells-java/)
- [Přizpůsobení grafů v Excelu v Javě: Ovládání Aspose.Cells pro plynulou vizualizaci dat](/cells/java/charts-graphs/excel-chart-customization-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}