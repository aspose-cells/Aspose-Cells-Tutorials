---
date: '2026-10-17'
description: Lär dig hur du anger formen på Excel-diagrammets datamärkning i Java
  med Aspose.Cells. Denna guide visar dig hur du snabbt och effektivt ändrar Excel-diagrametiketter.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Lär dig hur du anger formen på Excel-diagrammets datamärkning i Java
  med Aspose.Cells. Denna steg‑för‑steg‑guide hjälper dig att snabbt ändra Excel-diagrametiketter.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Hur du anger formen på Excel-diagrammets datamärkning i Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Hur du anger formen på Excel-diagrammets datamärkning i Java
url: /sv/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Behärska anpassning av diagram i Java med Aspose.Cells: ändra datalabels former

## Introduktion

Att förbättra det visuella intrycket av Excel-diagram är avgörande när man förbereder rapporter eller instrumentpaneler, särskilt om du använder Java. Med Aspose.Cells—ett kraftfullt bibliotek för kalkylblads‑hantering och manipulation—kan du **hur man ställer in form** för diagrammets datalabels på bara några rader kod. Denna handledning guidar dig genom att ändra formen på datalabels i ett Excel‑diagram med Aspose.Cells för Java. I slutet kommer du att kunna:

- Kom åt och ändra diagrammets datalabels
- Ställ in anpassade former för datalabels
- Spara ändringarna i din arbetsbok

## Snabba svar
- **Vilken är den primära klassen för att arbeta med Excel‑filer?** `Workbook` representerar en hel Excel‑fil i minnet.  
- **Vilken metod sätter label‑formen?** `setShapeType(DataLabelShapeType shape)` på ett `DataLabel`‑objekt.  
- **Behöver jag en licens för utveckling?** En gratis temporär licens fungerar för utvärdering; en full licens krävs för produktion.  
- **Kan jag tillämpa formen på flera serier?** Ja—iterera över varje serie och anropa `setShapeType`.  
- **Är detta tillvägagångssätt kompatibelt med stora arbetsböcker?** Aspose.Cells bearbetar arbetsböcker med flera hundra sidor utan att ladda hela filen i minnet.

## Vad är hur man ställer in form?
Frasen **how to set shape** avser konfiguration av den visuella konturen för ett diagrammets datalabel, till exempel att förvandla en enkel rektangel till en pratbubbla eller ellips. Att ändra formen förbättrar läsbarheten och framhäver viktiga datapunkter. Genom att välja en lämplig form kan du få etiketten att sticka ut, gruppera relaterade punkter eller matcha företagets varumärkesriktlinjer, vilket förbättrar diagrammets övergripande läsbarhet.

## Varför använda Aspose.Cells för anpassning av diagrametiketter?
Aspose.Cells stödjer **50+ in‑ och utdataformat**—inklusive XLSX, CSV, ODS och PDF—och kan manipulera arbetsböcker som innehåller **upp till 1 miljon rader** utan att tömma minnet. Dess API låter dig modifiera diagram programatiskt, vilket eliminerar behovet av manuella Excel‑ändringar och säkerställer konsekvent styling i automatiserade rapporter.

## Förutsättningar

- **Aspose.Cells för Java‑biblioteket**: Version 25.3 eller senare krävs.  
- **Java‑utvecklingsmiljö**: JDK installerat på din maskin.  
- **IDE‑uppsättning**: Använd en IDE som IntelliJ IDEA eller Eclipse för att skriva och köra din kod.

### Nödvändiga bibliotek och beroenden

För Maven‑användare, inkludera följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Gradle‑användare bör lägga till detta i sin `build.gradle`‑fil:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Licensanskaffning

Aspose.Cells erbjuder en gratis provlicens, som du kan hämta från [Aspose temporary license page](https://purchase.aspose.com/temporary-license/). Detta ger full åtkomst till alla funktioner utan begränsningar under en begränsad tid.

## Konfigurera Aspose.Cells för Java

När din miljö är klar, låt oss konfigurera Aspose.Cells. Så här kommer du igång:

### Installationssteg

1. **Ladda ner biblioteket**: Använd Maven eller Gradle som visas ovan.  
2. **Licenskonfiguration**:  
   - `License` är en klass som applicerar din Aspose.Cells‑licensfil för att möjliggöra full funktionalitet.  
   - Ladda ner och applicera en temporär licens med detta kodexempel efter att du initierat `Workbook`‑objektet:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Grundläggande initiering**: Skapa en `Workbook`‑instans för att börja arbeta med Excel‑filer.

## Hur man ställer in form för datalabels i ett diagram?

Läs in din arbetsbok, lokalisera mål‑diagrammet och applicera önskad form på dess datalabels. Följande direkta steg utför detta på under en minut.

### Steg‑för‑steg‑genomgång

#### Steg 1: ladda din arbetsbok

`Workbook`‑klassen är Aspose.Cells översta objekt som representerar en enda Excel‑fil i minnet. Använd `new Workbook("input.xlsx")` för att ladda filen du vill modifiera.

#### Steg 2: åtkomst till diagrammet

`Worksheet` representerar ett enskilt blad i en arbetsbok.  
`Worksheet ws = workbook.getWorksheets().get(0);` hämtar det första bladet.  
`Chart` är ett objekt som representerar ett diagram inbäddat i ett blad.  
`Chart chart = ws.getCharts().get(0);` får det första diagrammet på det bladet.

#### Steg 3: hämta serier och ändra datalabels

`Series` representerar en dataserie som plottas i ett diagram.  
Varje `Series`‑objekt innehåller en `DataLabel`‑samling.  
`DataLabel` styr utseendet på en datalabel för en serie.  
`DataLabelShapeType` är en uppräkning av möjliga former för datalabels.  
Anropa `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` för att sätta formen. Uppräkningen erbjuder dussintals alternativ, såsom `RECTANGLE`, `CLOUD` och `WEDGE_ELLIPSE_CALLOUT`.

#### Steg 4: spara din arbetsbok

Efter att ha applicerat formen, anropa `workbook.save("output.xlsx");` för att skriva tillbaka ändringarna till disk.

## Felsökningstips

- **Filvägsproblem**: Verifiera att filvägen är absolut eller korrekt relativ till ditt projekts arbetskatalog.  
- **Version mismatch för biblioteket**: Säkerställ att du använder Aspose.Cells version 25.3 eller senare; äldre versioner saknar metoden `setShapeType`.  
- **Ej stödda diagramtyper**: Vissa äldre diagramtyper (t.ex. radar) kanske inte exponerar egenskaper för datalabels form; byt till en stödd diagramtyp som kolumn eller linje.

## Praktiska tillämpningar

1. **Finansiell rapportering** – Markera viktiga vinstmarginaler med etiketter i samtalsstil.  
2. **Utbildningsinnehåll** – Använd molnformade etiketter för att dra uppmärksamhet till viktiga datapunkter i undervisningsmaterial.  
3. **Marknadsanalys** – Använd anpassade former för att särskilja kampanjprestandamått i instrumentpaneler.

Att integrera Aspose.Cells med datapipelines eller CRM‑system låter dig automatiskt generera fullt stylade rapporter, vilket minskar manuellt arbete och säkerställer varumärkes‑konsekventa visualiseringar.

## Prestandaöverväganden

När du arbetar med stora Excel‑filer:

- **Optimera minnesanvändning**: Anropa `workbook.dispose();` efter sparning för att snabbt frigöra inhemska resurser.  
- **Batch‑bearbetning**: Bearbeta diagram i grupper snarare än en åt gången för att minimera overhead för objekt‑skapande.  
- **Effektiv datahantering**: Undvik tunga beräkningar i loopar som itererar över tusentals rader; beräkna värden i förväg.

## Slutsats

Du vet nu **hur man ställer in form** för Excel‑diagramdatapetiketter i Java med Aspose.Cells. Denna funktion förbättrar inte bara diagrammets estetik utan också dataförståelsen för slutanvändare. Utforska ytterligare anpassningsalternativ—såsom etikettfärger, typsnitt och ledarlinjer—för att ytterligare förfina dina visualiseringar.

För frågor eller hjälp, se [Aspose support forum](https://forum.aspose.com/c/cells/9).

## Vanliga frågor

**Q: Hur ändrar jag formen på flera datalabels samtidigt?**  
A: Loopa igenom varje serie i diagrammet och anropa `setShapeType` på seriens `DataLabel`‑objekt.

**Q: Kan Aspose.Cells för Java hantera stora Excel‑filer effektivt?**  
A: Ja. Med korrekt minneshantering bearbetar det arbetsböcker med hundratusentals rader utan att ladda hela filen i minnet.

**Q: Vilka är vanliga problem när man konfigurerar Aspose.Cells?**  
A: Saknade Maven‑beroenden, användning av en föråldrad biblioteksversion eller en ogiltig licensfil är typiska fallgropar.

**Q: Finns det ett sätt att återställa datalabels former till standard?**  
A: Sätt formtypen till `DataLabelShapeType.DEFAULT` för att återställa ursprungligt utseende.

**Q: Hur kan jag tillämpa denna anpassning på flera diagram i en arbetsbok?**  
A: Iterera över `ws.getCharts()` och applicera samma `setShapeType`‑logik på varje diagrams seriekollektion.

## Resurser

- [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/java/)
- [Ladda ner Aspose.Cells för Java](https://releases.aspose.com/cells/java/)
- [Köp en licens](https://purchase.aspose.com/buy)
- [Gratis provlicens](https://releases.aspose.com/cells/java/)
- [Tillfällig licens](https://purchase.aspose.com/temporary-license/)

---  

**Last Updated:** 2026-10-17  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Relaterade handledningar

- [Ändra Excel-diagramdatapetiketter med Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Hur man ändrar storlek på etiketter i Excel-diagram med Aspose.Cells för Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Lägg till etiketter i Excel-diagram med Aspose Cells för Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}