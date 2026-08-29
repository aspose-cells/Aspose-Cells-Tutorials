---
date: '2026-04-11'
description: Naučte se automatizaci Excelu v Javě s Aspose.Cells. Tento tutoriál ukazuje,
  jak vytvořit Excel sešit v Javě, naplnit data v Excelu v Javě a uložit Excel soubor
  v Javě s grafy.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Automatizace Excelu v Javě: Vytvářejte sešity a grafy pomocí Aspose'
url: /cs/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatizace Excelu v Javě: Vytváření sešitů a grafů pomocí Aspose

## Úvod

Automatizace úkolů v Excelu pomocí Javy může ušetřit hodiny ruční práce, zejména když potřebujete za běhu generovat zprávy, dashboardy nebo datově řízené grafy. **Excel automation java** s Aspose.Cells vám poskytuje čisté, výkonné API, které zvládne vše od vytváření sešitu až po sofistikované formátování grafů. V tomto tutoriálu se naučíte, jak nastavit Aspose.Cells, **create an Excel workbook java**, naplnit jej daty, přidat graf, aplikovat 3‑D formátování a nakonec **save the Excel file java**.

### Rychlé odpovědi
- **Which library simplifies Excel automation in Java?** Která knihovna zjednodušuje automatizaci Excelu v Javě? Aspose.Cells for Java.  
- **Can I add 3‑D charts programmatically?** Mohu programově přidat 3‑D grafy? Ano – API podporuje 3‑D formátování a osvětlení.  
- **Do I need a license for development?** Potřebuji licenci pro vývoj? K dispozici je bezplatná zkušební licence; pro produkci je vyžadována komerční licence.  
- **What Java build tools are supported?** Jaké nástroje pro sestavování Java jsou podporovány? Maven a Gradle jsou plně podporovány.  
- **What file formats can I export?** Jaké formáty souborů mohu exportovat? XLS, XLSX, CSV, PDF a mnoho dalších.

## Co je Excel automation java?

Excel automation java odkazuje na proces generování, úpravy a ukládání Excel sešitů programově pomocí Java kódu. Eliminují se ruční úpravy tabulek, zajišťuje se konzistence a umožňuje integrace s dalšími systémy, jako jsou databáze nebo webové služby.

## Proč používat Aspose.Cells pro Java?

- **Rich feature set** – od jednoduchých hodnot buněk po složité grafy, kontingenční tabulky a podmíněné formátování.  
- **No Microsoft Office dependency** – funguje v jakémkoli serverovém prostředí.  
- **High performance** – optimalizováno pro velké datové sady a vícevláknové scénáře.  
- **Broad format support** – čtení/zápis XLS, XLSX, ODS, CSV, PDF, HTML a dalších.

## Prerequisites

- **Java Development Kit (JDK) 8+**  
- **Maven nebo Gradle** for dependency management  
- **Aspose.Cells pro Java 25.3 nebo novější** (trial or licensed)  

## Nastavení Aspose.Cells pro Java

Add the library to your project using one of the following configurations.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Získání licence

Request a free trial license from the Aspose website, or purchase a full license for production use. Place the license file in your project and load it at runtime.

## Základní inicializace a nastavení

Once the dependency is resolved, you can start coding.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Průvodce krok za krokem

### Krok 1: Jak vytvořit excel workbook java

Create a fresh workbook instance that will hold all your worksheets.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Krok 2: Přidat listy (včetně listu s grafem)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Krok 3: Jak naplnit excel data java

Insert sample data that the chart will reference.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Krok 4: Přidat sloupcový graf do sešitu

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Krok 5: Použít barevné formátování na oblast grafu

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Krok 6: Nastavit legendu a datové řady

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Krok 7: Použít 3D formátování na řady

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Krok 8: Nastavit barvy řad pro lepší vizuální odlišení

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Krok 9: Jak uložit excel file java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Praktické aplikace

- **Financial Reporting** – Generovat čtvrtletní výkazy s dynamickými grafy.  
- **Data‑Analysis Dashboards** – Vytvářet interaktivní dashboardy, které se automaticky obnovují.  
- **Inventory Management** – Exportovat úrovně zásob a trendy do Excelu pro přezkum zainteresovaných stran.  
- **Project Planning** – Vytvářet Ganttovy diagramy přímo z plánovacích systémů založených na Javě.

## Tipy pro výkon při automatizaci Excelu v Javě

- **Reuse Workbook Objects** when processing multiple sheets to reduce memory churn.  
- **Batch Cell Updates** using `Cells.importArray` for large data sets instead of individual `putValue` calls.  
- **Dispose Resources** by calling `book.dispose()` after saving large files.

## Často kladené otázky

**Q: Can I generate XLSX instead of XLS?**  
A: Yes – simply change the file extension in `book.save("output.xlsx")`; Aspose automatically selects the correct format.

**Q: Is a license required for development?**  
A: A free trial license works for development and testing. Production deployments require a purchased license.

**Q: How do I add more chart types?**  
A: Use `ChartType` enum (e.g., `ChartType.PIE`, `ChartType.LINE`) when calling `charts.add(...)`.

**Q: What if I need to protect the workbook?**  
A: Call `book.getSettings().setPassword("yourPassword")` before saving.

**Q: Does Aspose.Cells support macro‑enabled files?**  
A: Yes – you can create or preserve VBA macros in XLSM workbooks.

**Poslední aktualizace:** 2026-04-11  
**Testováno s:** Aspose.Cells 25.3 (Java)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}