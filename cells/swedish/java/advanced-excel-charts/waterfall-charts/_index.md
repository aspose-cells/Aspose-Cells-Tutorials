---
date: 2025-12-10
description: Lär dig hur du skapar ett waterfall‑diagram i Java med Aspose.Cells.
  Steg‑för‑steg‑guide för att lägga till diagram i ett kalkylblad, anpassa det och
  spara arbetsboken som XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Hur man skapar ett vattenfallsdiagram med Aspose.Cells för Java
url: /sv/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Waterfall Charts

## Introduction to Waterfall Charts using Aspose.Cells for Java

In this tutorial you’ll learn how to **create waterfall chart** with Aspose.Cells for Java. Waterfall charts are an essential tool in data visualization because they let you see the cumulative effect of a series of positive and negative values. Whether you’re preparing a financial statement, a sales performance report, or any other data‑driven analysis, a waterfall chart can turn raw numbers into clear, actionable insights.

## Quick Answers
- **What is a waterfall chart?** En visualisering som visar hur ett startvärde ökas och minskas av en serie mellanliggande värden, och avslutas med ett slutligt totalvärde.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Can I save the file as XLSX?** Ja – använd `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Absolut; Aspose.Cells provides rich charting features without Office installed.

## What is a Waterfall Chart?
Ett waterfall-diagram visar sekventiella positiva och negativa bidrag till ett startvärde, vilket hjälper dig att förstå hur varje komponent påverkar det totala resultatet.

## Why Use Aspose.Cells for Java to Add a Waterfall Chart?
- **No Microsoft Excel required** – generera diagram på vilken server eller CI-pipeline som helst.  
- **Full control over formatting** – färger, datamärkningar och axlar kan anpassas programmässigt.  
- **Supports multiple output formats** – XLSX, PDF, HTML och mer.  
- **High performance** – idealiskt för stora arbetsböcker och automatiserad rapportering.

## Prerequisites

Innan vi dyker ner i koden, se till att du har följande förutsättningar på plats:

- Aspose.Cells for Java: Du behöver ha Aspose.Cells for Java installerat. Du kan ladda ner det från [here](https://releases.aspose.com/cells/java/).

- Java Development Environment: Se till att du har Java installerat på ditt system.

Låt oss nu komma igång med att skapa waterfall-diagrammet steg för steg.

## How to Create Waterfall Chart in Java

### Step 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

Först måste du importera Aspose.Cells-biblioteket till ditt Java‑projekt. Detta bibliotek erbjuder omfattande funktionalitet för att arbeta med Excel‑filer, inklusive diagramskapande.

### Step 2: Initialize Workbook and Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Skapa en ny arbetsbok och lägg till ett kalkylblad i den. Vi kommer att använda detta kalkylblad för att ange våra data och **add chart to worksheet**.

### Step 3: Enter Data

Nu ska vi fylla kalkylbladet med data som vi vill representera i waterfall-diagrammet.

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

I det här exemplet har vi kategorier i kolumn A och motsvarande värden i kolumn B. Du kan ersätta dessa data med ditt eget dataset.

### Step 4: Create the Waterfall Chart

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Vi har lagt till ett waterfall-diagram i vårt kalkylblad, specificerat dataserierna och kategoridata. Detta är huvudsteget som **adds waterfall chart** till ditt blad. Du kan ytterligare anpassa diagrammets utseende (färger, datamärkningar osv.) med hjälp av `Chart`‑objektets egenskaper.

### Step 5: Save the Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Spara arbetsboken till en fil. Exemplet använder XLSX‑formatet, men Aspose.Cells låter dig också exportera till PDF, CSV och många andra format. Detta uppfyller kravet **save workbook xlsx**.

## Common Issues and Solutions

- **Chart appears blank** – Verifiera att dataområdesreferenserna (`B2:B6` och `A2:A6`) matchar de faktiska cellerna som innehåller dina värden och kategorier.  
- **Negative values not displayed correctly** – Säkerställ att serietypen är satt till `ChartType.WATERFALL`; andra diagramtyper hanterar negativa värden annorlunda.  
- **File not opening in Excel** – Se till att du använder en aktuell version av Aspose.Cells (senaste releasen) och att filändelsen matchar formatet (`.xlsx` för Excel).

## Frequently Asked Questions

### How can I customize the appearance of my waterfall chart?

Hur kan jag anpassa utseendet på mitt waterfall-diagram?

Du kan anpassa utseendet på ditt waterfall-diagram genom att ändra egenskaper som färger, datamärkningar och axelrubriker. Se Aspose.Cells‑dokumentationen för detaljerad vägledning.

### Can I create multiple waterfall charts in the same worksheet?

Kan jag skapa flera waterfall-diagram i samma kalkylblad?

Ja, du kan skapa flera waterfall-diagram i samma kalkylblad genom att följa samma steg med olika dataområden.

### Is Aspose.Cells compatible with different Java development environments?

Är Aspose.Cells kompatibelt med olika Java‑utvecklingsmiljöer?

Ja, Aspose.Cells for Java är kompatibelt med olika Java‑utvecklingsmiljöer, inklusive Eclipse, IntelliJ IDEA och NetBeans.

### Can I add additional data series to my waterfall chart?

Kan jag lägga till ytterligare dataserier i mitt waterfall-diagram?

Självklart, du kan lägga till fler dataserier i ditt waterfall-diagram för att effektivt representera komplexa datascenarier.

### Where can I find more resources and examples for Aspose.Cells for Java?

Var kan jag hitta fler resurser och exempel för Aspose.Cells for Java?

Du kan utforska dokumentationen för Aspose.Cells for Java på [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) för djupgående information och kodexempel.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}