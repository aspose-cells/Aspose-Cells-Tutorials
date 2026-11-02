---
date: '2026-04-08'
description: Lär dig hur du skapar ett linjediagram med markörer med Aspose.Cells
  för Java, lägger till diagrammet i kalkylbladet och anpassar Excel-diagram för automatiserad
  rapportering.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Skapa ett linjediagram med markörer med Aspose.Cells för Java
url: /sv/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa och formatera Excel-diagram med Aspose.Cells Java

## Introduktion

I dagens datadrivna värld är ett **line chart with markers** ett av de mest effektiva sätten att visualisera trender och avvikelser. Oavsett om du bygger automatiserade rapporter eller en instrumentpanel som uppdateras dagligen, sparar det att programatiskt lägga till ett line chart with markers i ett kalkylblad otal manuella steg. Denna handledning guidar dig genom att använda Aspose.Cells för Java för att skapa, formatera och exportera sådana diagram, så att du kan fokusera på insikter istället för tråkigt Excel‑arbete.

**Vad du kommer att lära dig**
- Initiera en arbetsbok och fylla den med data med hjälp av Aspose.Cells.  
- **Hur man lägger till ett line chart with markers i ett kalkylblad** och konfigurerar dess utseende.  
- Anpassa seriefärger, markörer och andra formateringsalternativ.  
- Spara arbetsboken som en Excel‑fil som inkluderar ditt formaterade diagram.

## Snabba svar
- **Vad är den primära klassen att börja med?** `Workbook` initierar en ny Excel‑fil.  
- **Vilken diagramtyp skapar ett line chart with markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Hur sätter jag anpassade färger för seriepunkter?** Använd `chart.getNSeries().setColorVaried(true)` och ange färger för markörområdet.  
- **Behöver jag en licens för full funktionalitet?** Ja, en betald eller tillfällig Aspose.Cells‑licens tar bort utvärderingsgränser.  
- **Kan jag exportera resultatet som XLSX?** Absolut—`workbook.save("StyledChart.xlsx")` skapar en XLSX‑fil.

## Förutsättningar

Innan du skapar och formaterar diagram med Aspose.Cells för Java, se till att du har följande konfiguration:

### Nödvändiga bibliotek
Inkludera Aspose.Cells som ett beroende i ditt projekt. Här är instruktioner för både Maven‑ och Gradle‑användare:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Krav för miljöinställning
- Java Development Kit (JDK) installerat på ditt system.  
- En Integrated Development Environment (IDE) såsom IntelliJ IDEA eller Eclipse för kodning och testning.

### Kunskapsförutsättningar
Grundläggande kunskap i Java‑programmering krävs, tillsammans med förtrogenhet med Excel‑arbetsböcker och diagramkoncept. 

### Licensanskaffning
Aspose.Cells är en kommersiell produkt som kräver en licens för full funktionalitet. Du kan få en gratis provversion för att utvärdera funktionerna, begära en tillfällig licens för utökad testning, eller köpa produkten för långsiktig användning.

- **Gratis provversion:** [Ladda ner gratis provversion](https://releases.aspose.com/cells/java/)  
- **Tillfällig licens:** [Begär tillfällig licens](https://purchase.aspose.com/temporary-license/)  
- **Köp:** [Köp Aspose.Cells](https://purchase.aspose.com/buy)

## Konfigurera Aspose.Cells för Java

När du har installerat de nödvändiga beroendena, konfigurera din utvecklingsmiljö för att använda Aspose.Cells. Börja med att importera biblioteket och initiera ett `Workbook`‑objekt i din Java‑applikation:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Implementeringsguide

I detta avsnitt kommer vi att dela upp implementeringen i separata funktioner: Initiering av arbetsbok och datainmatning, Diagramskapande och konfiguration, Serieanpassning och Sparande av arbetsbok.

### Funktion 1: Initiering av arbetsbok och datainmatning

**Översikt:** Denna funktion fokuserar på att skapa en ny arbetsbok, komma åt dess första kalkylblad och fylla det med data för diagramskapande.

#### Steg 1: Initiera arbetsboken
Börja med att instansiera ett `Workbook`‑objekt:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Steg 2: Ange kolumnrubriker och fyll i data
Definiera kolumnrubrikerna och fyll raderna med exempeldata:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funktion 2: Skapa diagram och konfigurera

**Översikt:** Denna funktion visar hur man lägger till ett diagram i arbetsbokens kalkylblad, ställer in dess stil och konfigurerar grundläggande egenskaper.

#### Steg 3: Lägg till ett diagram i kalkylbladet
Lägg till ett line chart with markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funktion 3: Seriekonfiguration och anpassning

**Översikt:** Förbättra det visuella intrycket av dina diagram genom att anpassa serieinställningar, såsom varierade färger och markörstilar.

#### Steg 4: Anpassa serieinställningar
Konfigurera seriedata, tillämpa anpassad formatering och justera markörer:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funktion 4: Spara arbetsbok

**Översikt:** Slutligen, spara arbetsboken för att bevara dina ändringar och säkerställa att diagrammet inkluderas i Excel‑filen.

#### Steg 5: Spara arbetsboken
Spara din arbetsbok med de nyss skapade diagrammen:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Vanliga problem och felsökning

- **Diagrammet visas tomt:** Verifiera att cellområdena som används i `setXValues` och `setValues` korrekt refererar till fyllda celler.  
- **Färger tillämpas inte:** Se till att `chart.getNSeries().setColorVaried(true)` anropas innan du anpassar enskilda serier.  
- **Licensfel:** En provlicens kan begränsa antalet diagram; installera en full licens för att ta bort begränsningarna.

## Vanliga frågor

**Q: Kan jag skapa andra diagramtyper (t.ex. stapel, cirkel) med Aspose.Cells?**  
A: Ja, Aspose.Cells stödjer ett brett utbud av diagramtyper; ersätt bara `ChartType.LINE_WITH_DATA_MARKERS` med önskat enum‑värde.

**Q: Behöver jag stänga arbetsboken eller frigöra resurser?**  
A: Klassen `Workbook` hanterar resurser automatiskt, men du kan anropa `workbook.dispose()` i långvariga applikationer för att frigöra minne.

**Q: Är det möjligt att lägga till flera diagram i samma kalkylblad?**  
A: Absolut—anropa `worksheet.getCharts().add(...)` för varje diagram du vill infoga.

**Q: Hur exporterar jag filen som ett äldre Excel‑format (XLS)?**  
A: Använd `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Q: Behåller diagrammet sin formatering när det öppnas i Microsoft Excel?**  
A: Ja, Aspose.Cells skriver inbyggda Excel‑diagramobjekt, så alla stilar, färger och markörer visas exakt som definierat.

---

**Senast uppdaterad:** 2026-04-08  
**Testat med:** Aspose.Cells 25.3 för Java  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}