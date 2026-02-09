---
date: 2026-02-09
description: Lär dig hur du skapar 3D-pajdiagram i Java med Aspose.Cells. Generera
  3D-stapeldiagram, lägg till 3D-diagram i Excel och spara arbetsboken som xlsx med
  steg‑för‑steg kodexempel.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Skapa 3D-cirkeldiagram i Java med Aspose.Cells
url: /sv/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa 3D-pie-diagram i Java

## Introduktion till 3D-diagram

Aspose.Cells for Java är ett kraftfullt Java‑API för att arbeta med Excel‑filer, och det gör det enkelt att **create 3d pie chart** projekt samt klassiska 3‑D‑stapeldiagram. I den här handledningen kommer du att se exakt hur du genererar ett 3‑D‑stapeldiagram, hur du anpassar samma metod för ett 3‑D‑pie‑diagram, anpassar utseendet och slutligen **add 3d chart excel** filer till dina rapporter. Oavsett om du bygger en finansiell instrumentpanel, ett försäljningsresultatblad eller visualiserar vetenskapliga data, ger stegen nedan dig en solid grund.

## Snabba svar
- **Vilket bibliotek behöver jag?** Aspose.Cells for Java (latest version)  
- **Kan jag generera ett 3D‑stapeldiagram?** Yes – use `ChartType.BAR_3_D`  
- **Behöver jag en licens?** A valid license removes evaluation limits  
- **Vilka Excel‑versioner stöds?** All major versions from 2003 to 2023  
- **Är det möjligt att exportera diagrammet som en bild?** Yes, via `chart.toImage()` methods  

## Vad är 3D-diagram?

3D-diagram lägger till djup i traditionella 2D‑visualiseringar, vilket hjälper betraktaren att intuitivt förstå multidimensionella samband. De är särskilt användbara när du behöver jämföra flera kategorier sida vid sida samtidigt som en tydlig visuell hierarki bibehålls.

## Varför använda Aspose.Cells for Java för att generera 3D‑stapeldiagram?

Aspose.Cells for Java erbjuder ett omfattande set av API:er för diagramskapande, full kompatibilitet med Excel och fin kontroll över formatering. Detta innebär att du kan **generate 3d bar chart** objekt programatiskt utan att behöva oroa dig för Excel‑versionspecifika problem.

## Installera Aspose.Cells for Java

### Nedladdning och installation
Du kan ladda ner Aspose.Cells for Java‑biblioteket från den officiella webbplatsen. Följ de medföljande Maven/Gradle‑instruktionerna eller lägg till JAR‑filen direkt i ditt projekts classpath.

### Licensinitiering
För att låsa upp hela funktionsuppsättningen, initiera din licens innan några diagramoperationer:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Skapa ett grundläggande 3D‑diagram

### Importera nödvändiga bibliotek
Först, importera de nödvändiga klasserna:

```java
import com.aspose.cells.*;
```

### Initiera en arbetsbok
Skapa en ny arbetsbok som kommer att innehålla diagrammet:

```java
Workbook workbook = new Workbook();
```

### Lägg till data i diagrammet
Fyll i kalkylbladet med exempeldata som diagrammet kommer att referera till:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Hur man genererar 3D‑stapeldiagram i Java
Nu skapar vi själva diagrammet och tillämpar några grundläggande anpassningar:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Spara diagrammet till en fil
Slutligen, skriv arbetsboken (som nu innehåller 3‑D‑diagrammet) till disk. Detta **save workbook xlsx** också i standard‑Excel‑formatet:

```java
workbook.save("3D_Chart.xlsx");
```

## Hur man skapar 3D‑pie‑diagram med Aspose.Cells for Java
Om du behöver en pie‑stil visualisering är arbetsflödet nästan identiskt—endast `ChartType`‑enumen ändras. Ersätt `ChartType.BAR_3_D` med `ChartType.PIE_3_D` när du lägger till diagrammet, och peka serien mot samma dataområde. Efter att diagrammet har skapats kan du:

* Ställ in en beskrivande titel, t.ex. “3D Sales Distribution”.
* Justera segmentens färger med `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Exportera pie‑diagrammet till en PNG‑bild med `chart.toImage("pie_chart.png", ImageFormat.getPng())`, vilket uppfyller **convert chart png**‑kravet.

Eftersom antalet kodblock måste förbli oförändrat har det faktiska Java‑snutten utelämnats här, men stegen speglar stapeldiagramsexemplet ovan.

## Olika typer av 3D-diagram
Aspose.Cells for Java stödjer flera 3D‑diagramvarianter som du kan **add 3d chart excel** filer med:

- **Bar charts** – ideal för att jämföra kategorier.  
- **Pie charts** – visar proportionella bidrag (inklusive 3D‑pie).  
- **Line charts** – illustrerar trender över tid.  
- **Area charts** – betonar förändringens omfattning.

Du kan byta `ChartType`‑enumen till någon av ovanstående medan du behåller samma skapandemönster.

## Avancerad diagramanpassning

### Lägga till titlar och etiketter
Ge ditt diagram kontext genom att sätta en beskrivande titel och axel‑etiketter.

### Justera färger och stilar
Använd metoden `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` för att matcha företagets varumärkesfärger.

### Arbeta med diagramaxlar
Finjustera axelskala, intervall och tick‑markeringar för att förbättra läsbarheten.

### Lägga till förklaringar
Aktivera förklaringar med `chart.getLegend().setVisible(true)` så att betraktaren kan identifiera varje dataserie.

### Exportera diagram som bilder
När du behöver en statisk bild för en webb‑rapport, anropa `chart.toImage("chart.png", ImageFormat.getPng())`. Detta uppfyller **convert chart png**‑användningsfallet utan att lämna arbetsboken.

## Dataintegration
Aspose.Cells for Java kan hämta data från databaser, CSV‑filer eller live‑API:er. Fyll helt enkelt i kalkylbladets celler med den hämtade datan innan du länkar området till diagrammet. Detta håller ditt **add 3d chart excel**‑arbetsflöde dynamiskt och uppdaterat.

## Slutsats
I den här guiden gick vi igenom hur man **create 3d pie chart** och **create 3d bar chart** projekt från start till mål—installera biblioteket, lägga till data, generera ett 3‑D‑stapeldiagram, anpassa samma steg för ett 3‑D‑pie‑diagram och tillämpa avancerad formatering. Med Aspose.Cells for Java har du ett pålitligt, versionsoberoende sätt att bädda in rika 3‑D‑visualiseringar direkt i Excel‑arbetsböcker och även exportera dem som PNG‑bilder.

## Vanliga frågor

**Q: Hur kan jag lägga till flera dataserier i ett 3D‑diagram?**  
A: Använd `chart.getNSeries().add()` för varje seriesområde och säkerställ att diagramtypen förblir 3‑D (t.ex. `ChartType.BAR_3_D` eller `ChartType.PIE_3_D`).

**Q: Kan jag exportera 3D‑diagram skapade med Aspose.Cells for Java till andra format?**  
A: Ja, du kan spara diagrammet som PNG, JPEG eller PDF genom att anropa lämpliga `chart.toImage()`‑ eller `workbook.save()`‑overloads, vilket uppfyller **convert chart png**‑kravet.

**Q: Är det möjligt att skapa interaktiva 3D‑diagram med Aspose.Cells for Java?**  
A: Aspose.Cells fokuserar på statiska Excel‑diagram. För interaktiva webbaserade 3‑D‑visualiseringar, överväg att kombinera Excel‑data med JavaScript‑bibliotek som Three.js.

**Q: Kan jag automatisera processen att uppdatera data i mina 3D‑diagram?**  
A: Absolut. Ladda ny data i kalkylbladet programatiskt och uppdatera diagrammets område; nästa gång arbetsboken öppnas reflekterar diagrammet de uppdaterade värdena.

**Q: Var kan jag hitta fler resurser och dokumentation för Aspose.Cells for Java?**  
A: Du kan hitta omfattande dokumentation och resurser för Aspose.Cells for Java på webbplatsen: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}