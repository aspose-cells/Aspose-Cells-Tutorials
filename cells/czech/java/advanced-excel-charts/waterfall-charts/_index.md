---
date: 2026-02-16
description: Naučte se nastavit rozsah dat grafu a vytvořit vodopádový graf v Javě
  pomocí Aspose.Cells. Podrobný návod krok za krokem, jak přidat graf s datovými řadami,
  přizpůsobit jej a exportovat do formátu XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Nastavit rozsah dat grafu – Aspose.Cells pro Java vodopádový graf
url: /cs/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Waterfall Charts

## Introduction to Waterfall Charts using Aspose.Cells for Java

V tomto tutoriálu se naučíte, jak **nastavit rozsah dat grafu** a vytvořit **vodopádový graf** pomocí Aspose.Cells for Java. Vodopádové grafy jsou nezbytným nástrojem pro vizualizaci dat, protože umožňují vidět kumulativní efekt řady kladných i záporných hodnot. Ať už připravujete finanční výkaz, zprávu o prodeji nebo jakoukoli jinou analýzu založenou na datech, vodopádový graf může převést surová čísla na jasné, akční poznatky.

## Quick Answers
- **What is a waterfall chart?** Vizuální zobrazení, které ukazuje, jak je počáteční hodnota zvýšena a snížena řadou mezihodnot, a končí konečným součtem.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Bezplatná zkušební verze stačí pro vývoj; pro produkci je vyžadována komerční licence.  
- **Can I save the file as XLSX?** Ano – použijte `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Rozhodně; Aspose.Cells poskytuje bohaté funkce pro tvorbu grafů bez nutnosti instalace Office.

## What is a Waterfall Chart?
Vodopádový graf zobrazuje sekvenční kladné a záporné příspěvky k počáteční hodnotě, což vám pomáhá pochopit, jak každý komponent ovlivňuje celkový výsledek.

## Why Use Aspose.Cells for Java to Add a Waterfall Chart?
- **No Microsoft Excel required** – generujte grafy na jakémkoli serveru nebo v CI pipeline.  
- **Full control over formatting** – barvy, datové popisky a osy lze programově přizpůsobit.  
- **Supports multiple output formats** – XLSX, PDF, HTML a další.  
- **High performance** – ideální pro velké sešity a automatizované reportování.

## Prerequisites

Než se pustíme do kódu, ujistěte se, že máte splněny následující předpoklady:

- Aspose.Cells for Java: Musíte mít nainstalovaný Aspose.Cells for Java. Stáhnout jej můžete [zde](https://releases.aspose.com/cells/java/).

- Java Development Environment: Ujistěte se, že máte na svém systému nainstalovanou Javu.

Nyní můžeme krok za krokem vytvořit vodopádový graf.

## How to Set Chart Data Range for a Waterfall Chart in Java

### Step 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

Nejprve musíte do svého Java projektu importovat knihovnu Aspose.Cells. Tato knihovna poskytuje rozsáhlé funkce pro práci se soubory Excel, včetně tvorby grafů.

### Step 2: Initialize Workbook and Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Vytvořte nový sešit a přidejte do něj list. Tento list použijeme k zadání dat a **add chart to worksheet**.

### Step 3: Enter Data

Nyní naplňte list daty, která chcete zobrazit ve vodopádovém grafu.

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

V tomto příkladu máme kategorie ve sloupci A a odpovídající hodnoty ve sloupci B. Můžete nahradit tato data svým vlastním datasetem.

### Step 4: Create the Waterfall Chart

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Přidali jsme vodopádový graf do našeho listu, určili datovou sérii a data kategorií. Toto je klíčový krok, který **adds waterfall chart** do listu. Všimněte si, že metoda `add` používá rozsah `"B2:B6"` – zde **set chart data range** pro sérii. Další úpravy vzhledu grafu (barvy, datové popisky atd.) můžete provést pomocí vlastností objektu `Chart`.

### Step 5: Save the Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Uložte sešit do souboru. Příklad používá formát XLSX, ale Aspose.Cells vám také umožní **export excel pdf java**‑kompatibilní soubory, jako jsou PDF, CSV a mnoho dalších formátů. Tím splňujete požadavek **save workbook xlsx**.

## Common Issues and Solutions

- **Chart appears blank** – Ověřte, že odkazy na rozsahy dat (`B2:B6` a `A2:A6`) odpovídají skutečným buňkám obsahujícím vaše hodnoty a kategorie.  
- **Negative values not displayed correctly** – Ujistěte se, že typ série je nastaven na `ChartType.WATERFALL`; jiné typy grafů zacházejí se zápornými hodnotami odlišně.  
- **File not opening in Excel** – Používejte aktuální verzi Aspose.Cells (nejnovější vydání) a ujistěte se, že přípona souboru odpovídá formátu (`.xlsx` pro Excel).

## Frequently Asked Questions

### How can I customize the appearance of my waterfall chart?

Můžete upravit vzhled vodopádového grafu změnou vlastností, jako jsou barvy, datové popisky a popisky os. Podívejte se do dokumentace Aspose.Cells pro podrobné instrukce.

### Can I create multiple waterfall charts in the same worksheet?

Ano, můžete vytvořit více vodopádových grafů ve stejném listu podle stejných kroků s různými rozsahy dat.

### Is Aspose.Cells compatible with different Java development environments?

Ano, Aspose.Cells for Java je kompatibilní s různými vývojovými prostředími Java, včetně Eclipse, IntelliJ IDEA a NetBeans.

### Can I add additional data series to my waterfall chart?

Samozřejmě, můžete přidat další datové série do vašeho vodopádového grafu, abyste efektivně zobrazili složitější scénáře. Toto je příklad, jak **add data series chart** programově.

### Where can I find more resources and examples for Aspose.Cells for Java?

Další informace a příklady najdete v dokumentaci Aspose.Cells for Java na adrese [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/).

## FAQ

**Q: How do I set the chart data range for a financial waterfall chart?**  
A: Použijte metodu `add` na sérii grafu a jako argument zadejte rozsah buněk obsahujících vaše hodnoty, např. `"B2:B6"`.

**Q: Can I export the workbook to PDF instead of XLSX?**  
A: Ano, zavolejte `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` pro **export excel pdf java**‑kompatibilní výstup.

**Q: What if I need to create a financial waterfall chart with more categories?**  
A: Rozšiřte rozsah dat jak ve sloupci hodnot, tak ve sloupci kategorií a poté aktualizujte volání `add` a `setCategoryData`.

**Q: Is there a way to automatically format positive and negative bars?**  
A: Můžete iterovat přes kolekci `Series` a nastavit barvu `FillFormat` podle znaménka každé hodnoty.

**Q: Does Aspose.Cells support dynamic data updates for charts?**  
A: Ano, můžete po vytvoření grafu měnit hodnoty buněk; graf tyto změny při uložení sešitu odrazí.

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}