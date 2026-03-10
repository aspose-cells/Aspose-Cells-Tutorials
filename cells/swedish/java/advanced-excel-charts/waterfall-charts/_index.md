---
date: 2026-02-16
description: Lär dig hur du ställer in diagrammets dataområde och skapar ett waterfall‑diagram
  i Java med Aspose.Cells. Steg‑för‑steg‑guide för att lägga till ett dataseriediagram,
  anpassa det och exportera till XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Ange diagrammets dataområde – Aspose.Cells för Java vattenfallsdiagram
url: /sv/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vattenfallsdiagram

## Introduktion till vattenfallsdiagram med Aspose.Cells för Java

I den här handledningen kommer du att lära dig hur du **set chart data range** och skapar ett **waterfall chart** med Aspose.Cells för Java. Vattenfallsdiagram är ett viktigt verktyg inom datavisualisering eftersom de låter dig se den kumulativa effekten av en serie positiva och negativa värden. Oavsett om du förbereder en finansiell rapport, en försäljningsprestandarapport eller någon annan datadriven analys, kan ett vattenfallsdiagram omvandla råa siffror till tydliga, handlingsbara insikter.

## Snabba svar
- **What is a waterfall chart?** En visualisering som visar hur ett startvärde ökas och minskas av en serie mellanliggande värden, och slutar med ett slutligt totalvärde.  
- **Which library is used?** Aspose.Cells för Java.  
- **Do I need a license?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Can I save the file as XLSX?** Ja – använd `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Absolut; Aspose.Cells erbjuder rika diagramfunktioner utan att Office är installerat.

## Vad är ett vattenfallsdiagram?

Ett vattenfallsdiagram visar sekventiella positiva och negativa bidrag till ett startvärde, vilket hjälper dig att förstå hur varje komponent påverkar det totala resultatet.

## Varför använda Aspose.Cells för Java för att lägga till ett vattenfallsdiagram?
- **No Microsoft Excel required** – generera diagram på vilken server eller CI-pipeline som helst.  
- **Full control over formatting** – färger, datalabels och axlar kan anpassas programatiskt.  
- **Supports multiple output formats** – XLSX, PDF, HTML och mer.  
- **High performance** – ideal för stora arbetsböcker och automatiserad rapportering.

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande förutsättningar på plats:

- Aspose.Cells för Java: Du behöver ha Aspose.Cells för Java installerat. Du kan ladda ner det från [here](https://releases.aspose.com/cells/java/).

- Java-utvecklingsmiljö: Se till att du har Java installerat på ditt system.

Nu, låt oss komma igång med att skapa vattenfallsdiagrammet steg för steg.

## Hur man anger diagrammets dataintervall för ett vattenfallsdiagram i Java

### Steg 1: Importera Aspose.Cells

```java
import com.aspose.cells.*;
```

Först måste du importera Aspose.Cells‑biblioteket till ditt Java‑projekt. Detta bibliotek erbjuder omfattande funktionalitet för att arbeta med Excel‑filer, inklusive skapande av diagram.

### Steg 2: Initiera arbetsbok och kalkylblad

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Skapa en ny arbetsbok och lägg till ett kalkylblad i den. Vi kommer att använda detta kalkylblad för att ange våra data och **add chart to worksheet**.

### Steg 3: Ange data

Nu ska vi fylla kalkylbladet med data som vi vill representera i vattenfallsdiagrammet.

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

I detta exempel har vi kategorier i kolumn A och motsvarande värden i kolumn B. Du kan ersätta dessa data med ditt eget dataset.

### Steg 4: Skapa vattenfallsdiagrammet

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Vi har lagt till ett vattenfallsdiagram i vårt kalkylblad, specificerat dataserierna och kategoridata. Detta är kärnsteg som **adds waterfall chart** till ditt blad. Lägg märke till hur `add`‑metoden använder intervallet `"B2:B6"` – det är här vi **set chart data range** för serien. Du kan ytterligare anpassa diagrammets utseende (färger, datalabels osv.) via `Chart`‑objektets egenskaper.

### Steg 5: Spara arbetsboken

```java
workbook.save("WaterfallChart.xlsx");
```

Spara arbetsboken till en fil. Exemplet använder XLSX‑formatet, men Aspose.Cells låter dig också **export excel pdf java**‑kompatibla filer såsom PDF, CSV och många andra format. Detta uppfyller kravet **save workbook xlsx**.

## Vanliga problem och lösningar

- **Chart appears blank** – Verifiera att dataintervallreferenserna (`B2:B6` och `A2:A6`) matchar de faktiska cellerna som innehåller dina värden och kategorier.  
- **Negative values not displayed correctly** – Säkerställ att serietypen är satt till `ChartType.WATERFALL`; andra diagramtyper behandlar negativa värden annorlunda.  
- **File not opening in Excel** – Se till att du använder en recent version of Aspose.Cells (the latest release) och att filändelsen matchar formatet (`.xlsx` för Excel).

## Vanliga frågor

### Hur kan jag anpassa utseendet på mitt vattenfallsdiagram?

Du kan anpassa utseendet på ditt vattenfallsdiagram genom att ändra egenskaper såsom färger, datalabels och axelrubriker. Se Aspose.Cells‑dokumentationen för detaljerad vägledning.

### Kan jag skapa flera vattenfallsdiagram i samma kalkylblad?

Ja, du kan skapa flera vattenfallsdiagram i samma kalkylblad genom att följa samma steg med olika dataintervall.

### Är Aspose.Cells kompatibel med olika Java‑utvecklingsmiljöer?

Ja, Aspose.Cells för Java är kompatibel med olika Java‑utvecklingsmiljöer, inklusive Eclipse, IntelliJ IDEA och NetBeans.

### Kan jag lägga till ytterligare dataserier i mitt vattenfallsdiagram?

Självklart, du kan lägga till fler dataserier i ditt vattenfallsdiagram för att effektivt representera komplexa datascenarier. Detta är ett exempel på hur du kan **add data series chart** programatiskt.

### Var kan jag hitta fler resurser och exempel för Aspose.Cells för Java?

Du kan utforska dokumentationen för Aspose.Cells för Java på [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) för djupgående information och kodexempel.

## FAQ

**Q: Hur anger jag diagrammets dataintervall för ett finansiellt vattenfallsdiagram?**  
A: Använd `add`‑metoden på diagrammets serier och skicka cellintervallet som innehåller dina värden, t.ex. `"B2:B6"`.

**Q: Kan jag exportera arbetsboken till PDF istället för XLSX?**  
A: Ja, anropa `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` för att **export excel pdf java**‑kompatibel output.

**Q: Vad händer om jag behöver skapa ett finansiellt vattenfallsdiagram med fler kategorier?**  
A: Utöka dataintervallet i både värdekolumnen och kategori‑kolumnen, och uppdatera sedan anropen till `add` och `setCategoryData` därefter.

**Q: Finns det ett sätt att automatiskt formatera positiva och negativa staplar?**  
A: Du kan iterera genom `Series`‑samlingen och sätta `FillFormat`‑färgen baserat på tecknet för varje värde.

**Q: Stöder Aspose.Cells dynamiska datauppdateringar för diagram?**  
A: Ja, du kan ändra cellvärden efter att diagrammet har skapats; diagrammet kommer att återspegla förändringarna när arbetsboken sparas.

---

**Senast uppdaterad:** 2026-02-16  
**Testad med:** Aspose.Cells för Java (senaste)  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}