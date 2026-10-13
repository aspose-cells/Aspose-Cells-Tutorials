---
date: '2026-04-08'
description: Naučte se, jak v Javě pomocí Aspose.Cells vytvořit sloupcový graf, včetně
  vytvoření grafu v Javě, přidání listu s grafem a exportu sešitu do Excelu.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Vytvořte sloupcový graf pomocí tutoriálu Aspose.Cells Java
url: /cs/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Generování sloupcového grafu pomocí Aspose.Cells Java

V dnešních aplikacích řízených daty může **generování sloupcového grafu** rychle a programově proměnit surová čísla v jasné vizuální poznatky. Ať už vytváříte reportingový dashboard, analytický nástroj nebo jednoduchou exportní funkci, Aspose.Cells pro Java vám poskytuje plynulé API pro **create chart java** projekty, aniž byste museli pracovat s uživatelským rozhraním Excelu. V tomto tutoriálu se naučíte, jak nastavit knihovnu, **populate Excel cells**, přidat **chart sheet**, přizpůsobit **chart title** a nakonec **export workbook excel** do souboru.

## Rychlé odpovědi
- **Co znamená „generate column chart“?** Vytváří svislou sloupcovou vizualizaci z tabulkových dat.  
- **Která knihovna je vyžadována?** Aspose.Cells for Java (k dispozici bezplatná zkušební verze).  
- **Potřebuji instalaci Excelu?** Ne, knihovna funguje nezávisle na Microsoft Excel.  
- **Mohu exportovat do formátů jiných než XLS?** Ano – PDF, PNG, SVG atd., pomocí `workbook.save()`.  
- **Je licence povinná pro produkci?** Ano, je vyžadována zakoupená nebo dočasná licence.

## Co je generate column chart?
Sloupcový graf zobrazuje datové řady jako svislé pruhy, což usnadňuje porovnání hodnot napříč kategoriemi, jako jsou regiony, měsíce nebo produktové řady. Aspose.Cells vám umožňuje vytvořit tento graf kompletně v kódu, což vám dává plnou kontrolu nad daty, stylováním a výstupním formátem.

## Proč použít Aspose.Cells k vytvoření chart java?
- **Žádná COM interop** – funguje na jakémkoli OS s JVM.  
- **Bohaté možnosti stylování** – obrázky, přechody, legendy a vlastní písma.  
- **Vysoký výkon** – vhodné pro velké datové sady.  
- **Více exportních formátů** – XLS, XLSX, PDF, PNG a další.

## Předpoklady
- **Java Development Kit (JDK) 8+** nainstalován.  
- Základní znalost Javy a povědomí o konceptech Excelu.  

### Požadované knihovny
Přidejte Aspose.Cells do svého projektu pomocí jednoho ze snippetů níže.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Získání licence
Aspose nabízí bezplatnou zkušební verzi a dočasnou licenci pro rozsáhlé testování.

- **Bezplatná zkušební verze**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Dočasná licence**: [Request Here](https://purchase.aspose.com/temporary-license/)

## Nastavení Aspose.Cells pro Java

Nejprve vytvořte instanci `Workbook` – bude to plátno pro naše data a graf.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Průvodce krok za krokem

### 1. Vytvořte a pojmenujte list
Uložíme surová data do listu nazvaného **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Naplňte buňky Excelu
Vložte názvy regionů a prodejní údaje, které sloupcový graf zobrazí.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Přidejte list s grafem
Oddělení grafu od surových dat udržuje sešit přehledný.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Vytvořte sloupcový graf
Nyní skutečně **generate column chart** objekty.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Nastavte obrázek jako výplň pozadí v oblasti vykreslování
Obrázek na pozadí může graf zvýraznit.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Nastavte název grafu
Přizpůsobení **set chart title** zlepšuje čitelnost.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Nakonfigurujte data řady a legendu
Propojte rozsah dat s grafem a umístěte legendu.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Exportujte sešit Excel
Nakonec **export workbook excel** do souboru XLS (nebo jakéhokoli podporovaného formátu).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Praktické aplikace
- **Business Reports** – Automaticky generujte prodejní grafy pro měsíční PDF.  
- **Data Analysis Tools** – Vložte dynamické grafy do vlastních analytických dashboardů.  
- **Enterprise Dashboards** – Aktualizujte obrázky grafů za běhu pro monitorování v reálném čase.

## Úvahy o výkonu
- Hromadně aktualizujte buňky při práci s velkými datovými sadami, aby se snížila režie.  
- Uvolněte prostředky (`workbook.dispose()`), pokud ve smyčce zpracováváte mnoho sešitů.

## Časté problémy a řešení
- **Image not showing** – Ověřte cestu k souboru a že formát obrázku (PNG, JPEG) je podporován.  
- **Chart appears blank** – Ujistěte se, že odkazy na datové rozsahy (`Data!B2:B8`) odpovídají naplněným buňkám.  
- **Out‑of‑memory errors** – Zpracovávejte data po částech a po velkých uloženích zavolejte `System.gc()`.

## Často kladené otázky

**Q: Jak přidat více řad do sloupcového grafu?**  
A: Volajte `chart.getNSeries().add()` opakovaně s různými datovými rozsahy, např. `"Data!C2:C8"` pro druhou řadu.

**Q: Mohu změnit popisky os?**  
A: Ano. Použijte `chart.getCategoryAxis().setTitle("Regions")` a `chart.getValueAxis().setTitle("Sales")`.

**Q: Do jakých formátů mohu exportovat kromě XLS?**  
A: Použijte `workbook.save("chart.pdf")`, `workbook.save("chart.png")` nebo `workbook.save("chart.xlsx")` pro PDF, PNG a XLSX.

**Q: Je licence vyžadována pro vývojové sestavy?**  
A: Bezplatná zkušební verze funguje pro hodnocení, ale pro produkční nasazení je potřeba trvalá nebo dočasná licence.

**Q: Jak mohu zlepšit rychlost vykreslování pro tisíce řádků?**  
A: Naplněte buňky pomocí `cells.importArray()` a minimalizujte překreslování grafu tím, že graf vytvoříte až po načtení všech dat.

---

**Poslední aktualizace:** 2026-04-08  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

## Zdroje

- [Dokumentace Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Stáhnout Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Koupit licenci](https://purchase.aspose.com/buy)
- [Bezplatná zkušební verze](https://releases.aspose.com/cells/java/)
- [Požadavek na dočasnou licenci](https://purchase.aspose.com/temporary-license/)
- [Fórum podpory](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}