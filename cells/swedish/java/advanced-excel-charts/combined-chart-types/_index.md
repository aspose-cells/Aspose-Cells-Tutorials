---
date: 2025-12-06
description: Lär dig hur du lägger till dataserier, skapar kombinerade diagramtyper,
  sparar Excel‑arbetsboken och exporterar diagrammet till PNG med Aspose.Cells för
  Java.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Lägg till dataserier för att skapa ett kombinerat diagram med Aspose.Cells
url: /sv/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till dataserier för att skapa kombinerat diagram med Aspose.Cells

I den här handledningen kommer du att **lägga till dataserier** i en Excel-arbetsbok och lära dig hur du **skapar kombinerade diagram** med Aspose.Cells för Java. Vi går igenom varje steg—från att skapa arbetsboken, lägga till serier, anpassa legenden, till att **spara Excel‑arbetsbok**-filer och exportera **diagrammet till PNG**. I slutet har du ett färdigt kombinerat diagram som du kan bädda in i rapporter eller instrumentpaneler.

## Snabba svar
- **Vilket bibliotek skapar kombinerade diagram?** Aspose.Cells for Java  
- **Hur lägger jag till en dataserie?** Använd `chart.getNSeries().add(...)`  
- **Kan jag exportera diagrammet som en bild?** Ja, med `chart.toImage(...)` (PNG)  
- **Vilket filformat kan jag spara arbetsboken som?** Standard `.xlsx` (Excel)  
- **Behöver jag en licens för produktion?** En giltig Aspose.Cells-licens krävs  

## Vad är **add data series** i Aspose.Cells?
Att lägga till en dataserie talar om för diagrammet vilka celler som innehåller de värden du vill plotta. Varje serie kan representera en linje, kolumn eller någon annan diagramtyp, och du kan blanda dem för att bygga ett **combined chart**.

## Varför skapa ett **combined chart**?
Ett combined chart låter dig visa olika datamängder med distinkta visuella representationer (t.ex. en linjeserie över en kolumnserie) i en enda vy. Detta är perfekt för att jämföra trender mot totalsummor, framhäva korrelationer eller leverera rikare insikter i ett kompakt format.

## Förutsättningar
- Java Development Kit (JDK) 8 eller högre  
- Aspose.Cells for Java-biblioteket (ladda ner från länken nedan)  
- Grundläggande kunskap om Java-syntax och Excel-koncept  

## Komma igång

Först, ladda ner Aspose.Cells for Java-biblioteket från den officiella webbplatsen:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

När JAR-filen har lagts till i ditt projekts classpath kan du börja bygga diagrammet.

### Steg 1: Importera Aspose.Cells-klasser
```java
import com.aspose.cells.*;
```

### Steg 2: Skapa en ny arbetsbok
```java
Workbook workbook = new Workbook();
```

### Steg 3: Åtkomst till det första kalkylbladet
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Steg 4: Lägg till ett combined chart-objekt  
Vi börjar med ett linjediagram och lägger senare till andra serier för att uppnå en **combined chart**-effekt.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Lägg till data i diagrammet

Nu när diagrambehållaren finns, måste vi fylla den med data.

### Steg 5: Definiera dataområdena och **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Den första parametern (`"A1:A5"`) är intervallet för den första serien, och den andra (`"B1:B5"`) skapar en andra serie som kommer att kombineras med den första.

### Steg 6: Ställ in kategori‑data (X‑axel)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Anpassa diagrammet

Ett bra diagram berättar en historia. Låt oss ge det titlar, axelrubriker och en tydlig legend.

### Steg 7: Ställ in diagramtitel och axelrubriker
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Steg 8: **Add legend chart** och justera dess position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Spara och exportera diagrammet

Efter anpassning vill du **spara Excel‑arbetsbok** och även generera en bild.

### Steg 9: Spara arbetsboken som en Excel‑fil
```java
workbook.save("CombinedChart.xlsx");
```

### Steg 10: Exportera **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoden `chart.toImage` **genererar excel chart**-bilder som kan användas i webbsidor, rapporter eller e‑post.

## Vanliga problem & felsökning

| Issue | Solution |
|-------|----------|
| **Ingen data visas** | Verifiera att cellområdena (`A1:A5`, `B1:B5`, `C1:C5`) faktiskt innehåller data innan diagrammet skapas. |
| **Legend överlappar diagram** | Ställ in `chart.getLegend().setOverlay(false)` eller flytta legenden till en annan position (t.ex. `RIGHT`). |
| **Bildfil är tom** | Se till att diagrammet har minst en serie och att `chart.toImage` anropas efter alla anpassningar. |
| **Sparande ger ett undantag** | Kontrollera att du har skrivbehörighet till mål katalogen och att filen inte är öppen i Excel. |

## Vanliga frågor

**Q: Hur installerar jag Aspose.Cells för Java?**  
A: Ladda ner JAR-filen från den officiella webbplatsen och lägg till den i ditt projekts classpath. Nedladdningslänken är: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kan jag skapa andra diagramtyper förutom linje och kolumn?**  
A: Ja, Aspose.Cells stödjer stapel, cirkel, spridning, område och många fler diagramtyper. Se API-dokumentationen för den fullständiga listan.

**Q: Krävs en licens för produktionsanvändning?**  
A: En giltig Aspose.Cells-licens krävs för produktionsdistributioner. En gratis provperiod finns tillgänglig för utvärdering.

**Q: Hur kan jag ändra färgerna på varje serie?**  
A: Använd `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (eller liknande) efter att ha lagt till serierna.

**Q: Var kan jag hitta fler kodexempel?**  
A: Omfattande dokumentation och ytterligare exempel finns på Aspose referenswebbplatsen: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
