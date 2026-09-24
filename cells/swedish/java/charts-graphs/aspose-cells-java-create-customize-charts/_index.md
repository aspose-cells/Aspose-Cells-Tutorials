---
date: '2026-04-08'
description: Lär dig hur du genererar stapeldiagram i Java med Aspose.Cells, inklusive
  skapa diagram i Java, lägga till diagramblad och exportera arbetsbok till Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Skapa stapeldiagram med Aspose.Cells Java-handledning
url: /sv/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa stapeldiagram med Aspose.Cells Java

I dagens datadrivna applikationer kan **generera ett stapeldiagram** snabbt och programatiskt omvandla råa siffror till tydliga visuella insikter. Oavsett om du bygger en rapporteringsdashboard, ett analysverktyg eller en enkel exportfunktion, ger Aspose.Cells för Java dig ett flytande API för att **skapa diagram java** projekt utan att behöva hantera Excel‑gränssnittet. I den här handledningen lär du dig hur du installerar biblioteket, **fyller i Excel‑celler**, lägger till ett **diagramark**, anpassar **diagramtitel** och slutligen **exporterar arbetsbok excel** till en fil.

## Snabba svar
- **Vad betyder “generate column chart”?** Det skapar en vertikal stapel‑typ visualisering från tabulära data.  
- **Vilket bibliotek krävs?** Aspose.Cells för Java (gratis provversion tillgänglig).  
- **Behöver jag en Excel‑installation?** Nej, biblioteket fungerar oberoende av Microsoft Excel.  
- **Kan jag exportera till andra format än XLS?** Ja – PDF, PNG, SVG osv., via `workbook.save()`.  
- **Är en licens obligatorisk för produktion?** Ja, en köpt eller tillfällig licens krävs.

## Vad är ett genererat stapeldiagram?
Ett stapeldiagram visar dataserier som vertikala staplar, vilket gör det enkelt att jämföra värden över kategorier såsom regioner, månader eller produktlinjer. Aspose.Cells låter dig bygga detta diagram helt i kod, vilket ger dig full kontroll över data, stil och utdataformat.

## Varför använda Aspose.Cells för att skapa chart java?
- **Ingen COM‑interop** – fungerar på alla OS med en JVM.  
- **Rika stilalternativ** – bilder, gradienter, förklaringar och anpassade typsnitt.  
- **Hög prestanda** – lämplig för stora datamängder.  
- **Flera exportformat** – XLS, XLSX, PDF, PNG och mer.

## Förutsättningar
- **Java Development Kit (JDK) 8+** installerat.  
- Grundläggande Java‑kunskaper och bekantskap med Excel‑koncept.

### Nödvändiga bibliotek
Lägg till Aspose.Cells i ditt projekt med någon av kodsnuttarna nedan.

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

### Licensanskaffning
Aspose erbjuder en gratis provversion och en tillfällig licens för omfattande testning.

- **Gratis provversion**: [Ladda ner gratis](https://releases.aspose.com/cells/java/)  
- **Tillfällig licens**: [Begär här](https://purchase.aspose.com/temporary-license/)

## Konfigurera Aspose.Cells för Java

Först, skapa en `Workbook`‑instans – detta blir duken för våra data och diagram.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Steg‑för‑steg‑guide

### 1. Skapa och namnge ett arbetsblad
Vi kommer att lagra rådata i ett blad som heter **Data**.

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

### 2. Fyll i Excel‑celler
Infoga regionsnamn och försäljningssiffror som stapeldiagrammet kommer att visualisera.

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

### 3. Lägg till diagramark
Att separera diagrammet från rådata håller arbetsboken prydlig.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Skapa ett stapeldiagram
Nu skapar vi faktiskt **generera stapeldiagram** objekt.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Ställ in bild som bakgrundsfyllning i plot‑området
En bakgrundsbild kan få diagrammet att sticka ut.

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

### 6. Ställ in diagramtitel
Att anpassa **set chart title** förbättrar läsbarheten.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Konfigurera seriedata och förklaring
Länka dataområdet till diagrammet och placera förklaringen.

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

### 8. Exportera arbetsbok Excel
Slutligen **export workbook excel** till en XLS‑fil (eller något annat stödd format).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Praktiska tillämpningar
- **Affärsrapporter** – Auto‑generera försäljningsdiagram för månatliga PDF‑filer.  
- **Dataanalysverktyg** – Bädda in dynamiska diagram i anpassade analysdashboards.  
- **Företagsdashboards** – Uppdatera diagrambilder i realtid för övervakning.

## Prestandaöverväganden
- Batch‑uppdatera celler när du arbetar med stora datamängder för att minska overhead.  
- Frigör resurser (`workbook.dispose()`) om du bearbetar många arbetsböcker i en loop.  

## Vanliga problem och lösningar
- **Bild visas inte** – Verifiera filvägen och att bildformatet (PNG, JPEG) stöds.  
- **Diagrammet är tomt** – Säkerställ att dataområdesreferenserna (`Data!B2:B8`) matchar de ifyllda cellerna.  
- **Out‑of‑memory‑fel** – Bearbeta data i delar och anropa `System.gc()` efter stora sparningar.  

## Vanliga frågor

**Q: Hur lägger jag till flera serier i ett stapeldiagram?**  
A: Anropa `chart.getNSeries().add()` upprepade gånger med olika dataområden, t.ex. `"Data!C2:C8"` för en andra serie.

**Q: Kan jag ändra axelrubrikerna?**  
A: Ja. Använd `chart.getCategoryAxis().setTitle("Regions")` och `chart.getValueAxis().setTitle("Sales")`.

**Q: Vilka format kan jag exportera till förutom XLS?**  
A: Använd `workbook.save("chart.pdf")`, `workbook.save("chart.png")` eller `workbook.save("chart.xlsx")` för PDF, PNG respektive XLSX.

**Q: Krävs en licens för utvecklingsbyggen?**  
A: En gratis provversion fungerar för utvärdering, men en permanent eller tillfällig licens behövs för produktionsdistributioner.

**Q: Hur kan jag förbättra renderingshastigheten för tusentals rader?**  
A: Fyll i celler med `cells.importArray()` och minimera diagramomritningar genom att skapa diagrammet efter att all data har laddats.

---

**Senast uppdaterad:** 2026-04-08  
**Testad med:** Aspose.Cells 25.3 för Java  
**Författare:** Aspose  

## Resurser

- [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/java/)
- [Ladda ner Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Köp en licens](https://purchase.aspose.com/buy)
- [Gratis provversion](https://releases.aspose.com/cells/java/)
- [Begär tillfällig licens](https://purchase.aspose.com/temporary-license/)
- [Supportforum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}