---
date: '2026-09-27'
description: Lär dig hur du skapar pie chart java med Aspose.Cells. Steg‑för‑steg
  guide för att anpassa Excel pie chart, konfigurera Maven dependency och generera
  professionella diagram.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Skapa pie chart java med Aspose.Cells för Java. Lär dig att anpassa
  Excel pie chart, lägga till Maven dependency och generera professionella diagram
  på några minuter.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Skapa pie chart java med Aspose.Cells – Fullständig Java-guide
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
title: Hur man skapar pie chart java med Aspose.Cells
url: /sv/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar cirkeldiagram java med Aspose.Cells

## Introduktion
Att skapa ett **pie chart** programatiskt känns ofta som ett pussel, särskilt när du behöver fin‑granulär kontroll över färger, förklaringar och titlar. I den här guiden kommer du att lära dig hur du **create pie chart java** med Aspose.Cells, och sedan anpassa Excel‑cirkeldiagrammet så att det matchar ditt varumärke eller rapporteringsstil. Vi går igenom miljöinställning, datainmatning, diagramgenerering och visuella justeringar — allt utan att lämna ditt Java‑IDE.

**Vad du kommer att lära dig**
- Lägg till **Maven dependency Aspose.Cells** i ditt projekt.
- Skapa en arbetsbok, fyll celler med data och generera ett cirkeldiagram.
- Applicera anpassade färger, titlar och förklaringar på diagrammet.
- Exportera arbetsboken till en XLSX‑fil klar för delning.

Innan du börjar bör du vara bekväm med grundläggande Java‑syntax och ha Maven eller Gradle installerat.

## Snabba svar
- **Vilket bibliotek skapar cirkeldiagram i Java?** Aspose.Cells for Java.
- **Behöver jag en licens?** A free trial works for development; a paid license is required for production.
- **Vilka Maven‑koordinater krävs?** `com.aspose:aspose-cells:24.10`.
- **Kan jag ändra segmentfärger?** Yes, via the `setAreaColor` method on each series.
- **Kan diagrammet exporteras till XLSX?** Absolutely—just call `workbook.save("output.xlsx")`.

## Vad är ett cirkeldiagram i Excel?
Ett cirkeldiagram visualiserar en enda dataserie som proportionella segment av en cirkel, vilket gör det enkelt att jämföra delar av ett helt. Varje segments vinkel motsvarar dess värde i förhållande till totalen, vilket ger snabb insikt i fördelning över kategorier såsom marknadsandel, budgetfördelning eller demografiska procentsatser.

## Varför använda Aspose.Cells för att skapa ett cirkeldiagram java?
Aspose.Cells stöder över 50 diagramtyper och kan hantera kalkylblad med upp till en miljon rader utan att ladda hela filen i minnet. Denna prestandafördel låter dig generera stora rapporter på modest hårdvara, samtidigt som du får fin‑granulär kontroll över diagrammets utseende, databindning och exportformat, vilket gör det till ett överlägset val jämfört med många open‑source‑bibliotek.

## Förutsättningar
- **Java Development Kit (JDK)** 8 eller nyare.
- **IDE** såsom IntelliJ IDEA eller Eclipse.
- **Maven** eller **Gradle** för beroendehantering.
- En **trial or purchased Aspose.Cells license**.

### Nödvändiga bibliotek och beroenden
Lägg till Aspose.Cells Maven‑artefaktet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Eller motsvarande för Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Steg för att skaffa licens
Aspose.Cells för Java är kommersiell, men du kan börja med en gratis provperiod. Besök [purchase page](https://purchase.aspose.com/buy) för att få en temporär licensnyckel.

## Konfigurera Aspose.Cells för Java
Först, se till att biblioteket finns på din classpath. Efter att ha lagt till beroendet kan du initiera API:t som visas nedan.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Implementeringsguide

### Skapa och konfigurera en arbetsbok
`Workbook`‑klassen representerar en hel Excel‑fil i minnet.

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

#### Steg 1: instansiera en arbetsbok
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Detta skapar en ny, tom arbetsbok som du omedelbart kan börja fylla.

### Åtkomst till eller ändra kalkylbladsceller
`Worksheet` representerar ett enskilt blad i arbetsboken, innehållande celler, rader och kolumner.  
Du kommer att skriva data som driver cirkeldiagrammet till ett kalkylblad.

#### Steg 2: hämta det första kalkylbladet och dess celler
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
Fyll cellerna med kategorinamn och värden som diagrammet kommer att använda.

### Skapa ett cirkeldiagram
`Chart`‑objekt visualiserar data i ett kalkylblad och stödjer olika typer såsom cirkel, stapel och linje.

#### Steg 3: lägg till ett cirkeldiagram i kalkylbladet
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Konfigurera cirkeldiagramserie och data
`Series` definierar dataintervallet och formateringen för ett diagram, och länkar kalkylbladceller till visuella element.

#### Steg 4: ange serien för diagrammet
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Konfigurera diagramlegend och titelutseende
En diagram‑`Legend` visar serienamnen och färgerna, vilket hjälper läsarna att identifiera varje segment.

#### Steg 5: anpassa diagramlegend och titel
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Anpassa diagramseriens färger
`setAreaColor` sätter fyllningsfärgen för ett diagramseriens segment med ett RGB‑värde.

#### Steg 6: ändra färger på cirkelsegment
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

### Autofit kolumner och spara arbetsbok
`autoFitColumns` justerar automatiskt kolumnbredderna så att de passar cellinnehållet.

#### Steg 7: justera kolumnbredder och spara filen
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Vanliga användningsfall
- **Demographic analysis:** Visa befolkningsfördelning över regioner.
- **Market‑share reporting:** Visualisera varje konkurrents andel i ett ögonkast.
- **Budget allocation:** Markera hur medel fördelas mellan avdelningar.

## Prestandaöverväganden
- Frigör objekt (`workbook.dispose()`) när de inte längre behövs för att frigöra native‑minne.
- För massiva datamängder, använd `WorkbookDesigner` för att strömma data istället för att ladda allt på en gång.
- Profilera med Java Flight Recorder för att upptäcka eventuella flaskhalsar i diagramgenereringen.

## Vanliga frågor

**Q: Kan jag generera flera cirkeldiagram i samma arbetsbok?**  
A: Yes, repeat the chart‑creation steps for each data range; each chart is independent.

**Q: Stöder Aspose.Cells 3‑D‑cirkeldiagram?**  
A: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.

**Q: Hur applicerar jag ett anpassat tema på alla diagram?**  
A: Use the `Workbook.setDefaultTheme` method before creating any charts.

**Q: Vilka filformat kan jag exportera arbetsboken till?**  
A: Over 30 formats, including XLSX, CSV, PDF, and HTML.

**Q: Krävs en licens för kommersiell distribution?**  
A: Yes, a valid license removes evaluation watermarks and unlocks full functionality.

## Slutsats
Du har nu ett komplett, end‑to‑end‑recept för **create pie chart java** med Aspose.Cells. Genom att följa stegen ovan kan du generera polerade Excel‑cirkeldiagram, anpassa färger och titlar, och bädda in dem i vilken rapporteringspipeline som helst. Utforska andra diagramtyper — stapel, linje, radar — för att bredda ditt verktyg för datavisualisering.

---

**Senast uppdaterad:** 2026-09-27  
**Testad med:** Aspose.Cells 24.10 for Java  
**Författare:** Aspose

## Relaterade handledningar

- [Anpassa Excel-diagramdatamärkningar med Aspose.Cells för Java&#58; En steg‑för‑steg‑guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Skapa dynamiska Excel‑diagram med Aspose.Cells Java&#58; En omfattande guide för utvecklare](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Skapa och anpassa Excel‑arbetsböcker med Aspose.Cells Java&#58; En steg‑för‑steg‑guide](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}