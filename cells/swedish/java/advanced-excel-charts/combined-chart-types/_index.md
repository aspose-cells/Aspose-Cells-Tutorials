---
date: 2026-02-14
description: Lär dig hur du exporterar diagram till PNG, lägger till dataserier, kombinerar
  linje‑ och stapeldiagram, sparar arbetsboken som XLSX och lägger till diagramförklaring
  med Aspose.Cells för Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Exportera diagram till PNG och lägg till dataserier för kombinerat diagram
url: /sv/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

Let's construct final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportera diagram till PNG och lägg till dataserier för kombinerat diagram

I den här handledningen kommer du att **lägga till dataserier** i en Excel-arbetsbok, **kombinera linje‑ och stapeldiagram**‑element och lära dig hur du **exporterar diagram till PNG** med Aspose.Cells for Java. Vi går igenom varje steg—från att skapa arbetsboken, lägga till diagrammet i ett kalkylblad, anpassa förklaringen, till att **spara arbetsboken som xlsx** och generera en PNG‑bild av diagrammet. I slutet har du ett färdigt kombinerat diagram som du kan bädda in i rapporter eller instrumentpaneler.

## Snabba svar
- **Vilket bibliotek skapar kombinerade diagram?** Aspose.Cells for Java  
- **Hur lägger jag till en dataserie?** Use `chart.getNSeries().add(...)`  
- **Hur kan jag exportera diagram till png?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **Vilket filformat kan jag spara arbetsboken som?** Standard `.xlsx` (save workbook as xlsx)  
- **Behöver jag en licens för produktion?** A valid Aspose.Cells license is required  

## Vad är **export chart to PNG** i Aspose.Cells?
Att exportera ett diagram till PNG skapar en rasterbild av Excel‑diagrammet som kan visas på webbsidor, i rapporter eller e‑post utan att kräva Excel‑applikationen.

## Varför skapa ett **kombinerat linje‑stapeldiagram**?
Ett kombinerat diagram låter dig visa olika dataset med olika visuella representationer (t.ex. en linjeserie ovanpå en stapelserie) i en enda vy. Detta är perfekt för att jämföra trender mot totalsummor, framhäva korrelationer eller leverera rikare insikter i ett kompakt format.

## Förutsättningar
- Java Development Kit (JDK) 8 eller högre  
- Aspose.Cells for Java‑biblioteket (ladda ner från länken nedan)  
- Grundläggande kunskap om Java‑syntax och Excel‑koncept  

## Komma igång

Först, ladda ner Aspose.Cells for Java‑biblioteket från den officiella webbplatsen:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

När JAR‑filen har lagts till i ditt projekts classpath kan du börja bygga diagrammet.

### Steg 1: Importera Aspose.Cells‑klasser
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

### Steg 4: Lägg till ett kombinerat diagramobjekt i kalkylbladet  
Vi börjar med ett linjediagram och lägger senare till en stapelserie för att uppnå en **kombinerad linje‑stapeldiagram**‑effekt.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Lägg till data i diagrammet

När diagrambehållaren finns, måste vi fylla den med data.

### Steg 5: Definiera dataområdena och **lägga till dataserier**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Proffstips:** Den första parametern (`"A1:A5"`) är området för den första serien, och den andra (`"B1:B5"`) skapar en andra serie som kommer att kombineras med den första.

### Steg 6: Ställ in kategori‑ (X‑axel) data
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Anpassa diagrammet

Ett bra diagram berättar en historia. Låt oss ge det titlar, axelrubriker och en tydlig förklaring.

### Steg 7: **Ställ in diagramaxelrubriker** och titel
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Steg 8: **Lägg till förklaringsdiagram** och justera dess position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Spara och exportera diagrammet

Efter anpassning vill du **spara arbetsboken som xlsx** och även generera en bild.

### Steg 9: Spara arbetsboken som en Excel‑fil (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Steg 10: **Exportera diagram till PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoden `chart.toImage` **genererar Excel‑diagram**‑bilder som kan användas på webbsidor, i rapporter eller e‑post.

## Vanliga problem & felsökning

| Problem | Lösning |
|-------|----------|
| **Ingen data visas** | Verifiera att cellområdena (`A1:A5`, `B1:B5`, `C1:C5`) faktiskt innehåller data innan diagrammet skapas. |
| **Förklaring överlappar diagram** | Ställ in `chart.getLegend().setOverlay(false)` eller flytta förklaringen till en annan position (t.ex. `RIGHT`). |
| **Bildfilen är tom** | Säkerställ att diagrammet har minst en serie och att `chart.toImage` anropas efter alla anpassningar. |
| **Sparande kastar ett undantag** | Kontrollera att du har skrivbehörighet till mål katalogen och att filen inte är öppen i Excel. |

## Vanliga frågor

**Q: Hur installerar jag Aspose.Cells for Java?**  
A: Ladda ner JAR‑filen från den officiella webbplatsen och lägg till den i ditt projekts classpath. Nedladdningslänken är: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kan jag skapa andra diagramtyper än linje och stapel?**  
A: Ja, Aspose.Cells stöder stapel, paj, spridnings-, yta‑ och många fler diagramtyper. Se API‑dokumentationen för hela listan.

**Q: Krävs en licens för produktionsanvändning?**  
A: En giltig Aspose.Cells‑licens krävs för produktionsdistributioner. En gratis provversion finns tillgänglig för utvärdering.

**Q: Hur kan jag ändra färgerna för varje serie?**  
A: Använd `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (eller liknande) efter att serien har lagts till.

**Q: Var kan jag hitta fler kodexempel?**  
A: Omfattande dokumentation och ytterligare exempel finns på Aspose‑referenssajten: [here](https://reference.aspose.com/cells/java/).

---

**Senast uppdaterad:** 2026-02-14  
**Testat med:** Aspose.Cells for Java senaste versionen  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}