---
date: 2026-09-02
description: Lär dig hur du skapar ett Excel‑vattenfallsdiagram i Java med Aspose.Cells,
  ställer in diagrammets dataområde, anpassar etiketter och exporterar till XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Vattenfallsdiagram
og_description: Skapa ett Excel‑vattenfallsdiagram med Aspose.Cells för Java – ställ
  in diagrammets dataområde, lägg till dataetiketter och exportera till XLSX i några
  enkla steg.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Skapa Excel‑vattenfallsdiagram med Aspose.Cells för Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Skapa Excel‑vattenfallsdiagram med Aspose.Cells för Java
url: /sv/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vattenfallsdiagram

## Introduktion till vattenfallsdiagram med Aspose.Cells för Java

I den här handledningen kommer du att lära dig hur du **skapar excel vattenfallsdiagram** och **anger diagrammets dataområde** med Aspose.Cells för Java. Vattenfallsdiagram omvandlar en serie av positiva och negativa tal till en tydlig visuell berättelse, vilket gör dem idealiska för finansiella rapporter, försäljningsprestandaöversikter och alla scenarier där du behöver se hur enskilda poster bidrar till ett totalvärde.

## Snabba svar
- **Vad är ett vattenfallsdiagram?** En visualisering som visar hur ett startvärde ökas och minskas av en serie mellanliggande värden, och slutar med ett slutligt totalvärde.  
- **Vilket bibliotek används?** Aspose.Cells för Java.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Kan jag spara filen som XLSX?** Ja – använd `workbook.save("FileName.xlsx")`.  
- **Är det lämpligt för Java-datavisuellisering?** Absolut; Aspose.Cells erbjuder rika diagramfunktioner utan att Office är installerat.

## Vad är ett vattenfallsdiagram?
Ett vattenfallsdiagram visar sekventiella positiva och negativa bidrag till ett startvärde, vilket hjälper dig att förstå hur varje komponent påverkar det totala resultatet. Genom att visualisera vinster och förluster sida‑vid‑sida blir komplexa finansiella flöden omedelbart läsbara.

## Varför använda Aspose.Cells för Java för att lägga till ett vattenfallsdiagram?
Aspose.Cells låter dig generera Excel‑diagram på vilken server, CI‑pipeline eller skrivbord som helst utan att behöva Microsoft Excel. Det stöder **15+ utdataformat** (XLSX, PDF, HTML, CSV och mer), bearbetar arbetsböcker med **500+ rader** på under en sekund och ger programmatisk kontroll över varje diagramdel – från färger till datamärkningar.

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande förutsättningar på plats:

- Aspose.Cells för Java: Du måste ha Aspose.Cells för Java installerat. Du kan ladda ner det från Aspose.Cells för Java‑utgivningssidan: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Java‑utvecklingsmiljö: Säkerställ att du har Java installerat på ditt system och ett byggverktyg (Maven/Gradle) redo.

Nu, låt oss komma igång med att skapa vattenfallsdiagrammet steg för steg.

## Hur man anger diagrammets dataområde för ett vattenfallsdiagram i Java
Läs in en ny arbetsbok, fyll den med data, lägg till ett `Chart`‑objekt, definiera seriernas område och spara slutligen filen. Denna process är enkel: du skapar en arbetsbok, fyller celler med kategorier och värden, skapar ett diagram, binder dataområdena och exporterar sedan arbetsboken. Resultatet blir ett fullt funktionellt vattenfallsdiagram redo för användning i rapporter eller instrumentpaneler.

### Steg 1: importera Aspose.Cells
`com.aspose.cells`‑paketet innehåller alla klasser som krävs för Excel‑manipulation, inklusive skapande av arbetsböcker, hantering av kalkylblad och generering av diagram.

### Steg 2: initiera arbetsbok och kalkylblad
En **Workbook** representerar en Excel‑fil, och ett **Worksheet** är ett enskilt blad i den filen. Att skapa dessa objekt ger en yta för både rådata och diagrammet.

### Steg 3: ange data
Kolumn A innehåller kategorietiketter, medan kolumn B innehåller de numeriska värdena för vattenfallet. Denna layout motsvarar det typiska resultat‑och‑förlust‑flödet som används i finansiell analys.

### Steg 4: skapa vattenfallsdiagrammet
**Chart**‑objektet skapar en visuell representation; genom att sätta dess typ till `ChartType.WATERFALL` konfigureras det som ett vattenfallsdiagram. Använd `add`‑metoden för att ange diagrammets dataområde för serien (`"B2:B6"`), och länka kategori‑axeln till `"A2:A6"`.

### Steg 5: spara arbetsboken
Att spara arbetsboken skriver diagrammet och datan till det angivna filformatet. Anropa `workbook.save("WaterfallChart.xlsx")` för att generera en XLSX‑fil, eller ändra formatparametern för att exportera till PDF, CSV eller HTML.

## Vanliga problem och lösningar

- **Diagrammet visas tomt** – Kontrollera att dataområdesreferenserna (`B2:B6` och `A2:A6`) matchar de faktiska cellerna som innehåller dina värden och kategorier.  
- **Negativa värden visas inte korrekt** – Säkerställ att serietypen är satt till `ChartType.WATERFALL`; andra diagramtyper hanterar negativa värden annorlunda.  
- **Filen öppnas inte i Excel** – Använd den senaste Aspose.Cells‑utgåvan och bekräfta att filändelsen matchar formatet (`.xlsx` för Excel).

## Vanliga frågor

### Hur kan jag anpassa utseendet på mitt vattenfallsdiagram?
Du kan modifiera egenskaper som `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` för att ändra stapelfärger, aktivera datamärkningar med `setShowDataLabels(true)` och justera axelrubriker via `getCategoryAxis().setTitle("Stage")`. Aspose.Cells API‑referensen ger en komplett lista över anpassningsbara alternativ.

### Kan jag skapa flera vattenfallsdiagram i samma kalkylblad?
Ja. Efter att du lagt till det första diagrammet, upprepa stegen för diagramskapande med ett annat dataområde och ett nytt `Chart`‑objekt. Varje diagram är oberoende och kan placeras var som helst på bladet.

### Är Aspose.Cells kompatibel med olika Java‑utvecklingsmiljöer?
Absolut. Biblioteket fungerar med Eclipse, IntelliJ IDEA, NetBeans och alla byggsystem som stödjer Maven eller Gradle. Inga extra plugins krävs.

### Kan jag lägga till ytterligare dataserier i mitt vattenfallsdiagram?
Du kan lägga till fler serier genom att anropa `chart.getNSeries().add("C2:C6", true)` och konfigurera varje serie separat. Detta låter dig jämföra flera scenarier sida‑vid‑sida.

### Var kan jag hitta fler resurser och exempel för Aspose.Cells för Java?
Utforska den fullständiga dokumentationen i Aspose.Cells Java API‑referensen: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## Vanliga frågor

**Q: Hur anger jag diagrammets dataområde för ett finansiellt vattenfallsdiagram?**  
A: Använd `add`‑metoden på diagrammets serie och ange cellområdet som innehåller dina värden, t.ex. `"B2:B6"`.

**Q: Kan jag exportera arbetsboken till PDF istället för XLSX?**  
A: Ja, anropa `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` för att generera en PDF‑version.

**Q: Vad händer om jag behöver skapa ett vattenfallsdiagram med fler kategorier?**  
A: Utöka dataområdet både i värde‑kolumnen och i kategori‑kolumnen, och uppdatera sedan anropen till `add` och `setCategoryData` därefter.

**Q: Finns det ett sätt att automatiskt formatera positiva och negativa staplar?**  
A: Iterera genom `Series`‑samlingen och sätt `FillFormat`‑färgen baserat på varje värdes tecken; Aspose.Cells låter dig tillämpa villkorlig formatering programatiskt.

**Q: Stöder Aspose.Cells dynamiska datauppdateringar för diagram?**  
A: Ja. Efter att du har ändrat cellvärden, spara bara arbetsboken igen – diagrammet kommer automatiskt att återspegla de nya data.

---

**Senast uppdaterad:** 2026-09-02  
**Testat med:** Aspose.Cells för Java (senaste)  
**Författare:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Relaterade handledningar

- [Anpassa Excel-diagrammets datamärkningar med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Lägg till datamärkningar i Excel-diagram med Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Hur man skapar och exporterar diagram i Java med Aspose.Cells: En komplett guide](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}