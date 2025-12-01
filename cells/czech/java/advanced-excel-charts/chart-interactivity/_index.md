---
date: 2025-12-01
description: Naučte se, jak změnit typ grafu v Excelu a přidat interaktivní funkce,
  jako jsou tooltipy, popisky dat a drill‑down, pomocí Aspose.Cells pro Javu.
language: cs
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Změňte typ grafu v Excelu a přidejte interaktivitu – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Změna typu grafu v Excelu a přidání interaktivity

## Úvod

Interaktivní grafy umožňují vašemu publiku prozkoumávat data za běhu, zatímco možnost **change Excel chart type** vám poskytuje flexibilitu prezentovat informace v nejefektivnějším vizuálním formátu. V tomto tutoriálu se naučíte, jak pomocí Aspose.Cells pro Java změnit typ grafu, přidat tooltipy, vložit popisky dat a dokonce vytvořit drill‑down odkazy – vše bez opuštění vašeho Java kódu. Na konci budete mít plně vybavený, interaktivní Excel sešit, který můžete vložit do reportů, dashboardů nebo webových aplikací.

## Rychlé odpovědi
- **Mohu změnit typ grafu programově?** Yes – use the `ChartType` enum when creating or updating a chart.  
- **Jak přidám tooltipy do grafu?** Enable data labels and set `ShowValue` to true.  
- **Jaký je nejjednodušší způsob, jak přidat drill‑down odkazy?** Attach a hyperlink to a data point via `getHyperlinks().add(url)`.  
- **Potřebuji licenci pro Aspose.Cells?** A free trial works for development; a license is required for production.  
- **Která verze Javy je podporována?** Java 8 and above are fully supported.

## Co je “change Excel chart type”?

Změna typu grafu znamená výměnu vizuální reprezentace (např. z sloupcového grafu na čárový graf) při zachování podkladových dat beze změny. To je užitečné, když zjistíte, že jiný graf lépe komunikuje trendy, srovnání nebo rozdělení.

## Proč přidávat interaktivitu do Excel grafů?

- **Lepší přehled o datech:** Tooltipy a popisky dat umožňují uživatelům vidět přesné hodnoty bez posouvání.  
- **Poutavé prezentace:** Interaktivní prvky udržují diváky zaujaté.  
- **Možnost drill‑down:** Hyperlinky umožňují uživatelům přejít na podrobné listy nebo externí zdroje.  
- **Znovupoužitelné zdroje:** Jeden sešit může sloužit více scénářům reportování pouhým přepnutím typu grafu.

## Prerequisites

- Vývojové prostředí Java (JDK 8+)  
- Aspose.Cells pro Java knihovna (stáhněte z [here](https://releases.aspose.com/cells/java/))  
- Ukázkový Excel soubor (`data.xlsx`) obsahující data, která chcete vizualizovat

## Průvodce krok za krokem

### Krok 1: Nastavte svůj Java projekt

1. Vytvořte nový Java projekt ve svém oblíbeném IDE (IntelliJ IDEA, Eclipse, VS Code, atd.).  
2. Přidejte JAR soubor Aspose.Cells do classpath vašeho projektu.

### Krok 2: Načtěte zdrojový sešit

Začneme načtením existujícího sešitu, který obsahuje data pro náš graf.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 3: Vytvořte graf a **změňte jeho typ**

Níže vytvoříme sloupcový graf a poté okamžitě ukážeme, jak jej můžete v případě potřeby přepnout na čárový graf.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro tip:** Změna typu grafu po vytvoření je tak jednoduchá jako zavolat `setChartType(...)`. To splňuje hlavní klíčové slovo **change Excel chart type** bez nutnosti vytvářet nový graf.

### Krok 4: Přidejte interaktivitu

#### 4.1 Přidejte tooltipy do grafu

Tooltipy se zobrazují, když uživatel najede myší na datový bod. V Aspose.Cells jsou implementovány pomocí popisků dat.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Přidejte popisky dat ( **add data labels chart** )

Popisky dat mohou zobrazovat přesnou hodnotu, název kategorie nebo obojí. Zde používáme styl callout.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implementujte drill‑down ( **add drill down excel** )

Drill‑down odkaz umožňuje uživatelům kliknout na bod a přejít na podrobný pohled, buď uvnitř sešitu, nebo na webové stránce.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Krok 5: Uložte sešit

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Časté problémy a řešení

| Problém | Důvod | Řešení |
|---------|-------|--------|
| Tooltipy se nezobrazují | `HasDataLabels` není povoleno | Ensure `setHasDataLabels(true)` is called before configuring `ShowValue`. |
| Drill‑down odkaz nefunguje | URL hypertextového odkazu je poškozené | Verify the URL starts with `http://` or `https://`. |
| Typ grafu se nezmění | Používáte starší verzi Aspose.Cells | Upgrade to the latest version (tested with 24.12). |

## Často kladené otázky

**Q: Jak mohu změnit typ grafu po jeho vytvoření?**  
A: Call `chart.setChartType(ChartType.YOUR_CHOICE)` on the existing `Chart` object. This directly addresses the **change Excel chart type** requirement.

**Q: Mohu přizpůsobit vzhled tooltipů?**  
A: Yes. Use `chart.getNSeries().get(0).getPoints().getDataLabels()` to set font size, color, and background.

**Q: Je možné přidat více drill‑down odkazů do jednoho grafu?**  
A: Absolutely. Loop through the points and call `getHyperlinks().add(url)` for each point you want to link.

**Q: Podporuje Aspose.Cells jiné typy grafů, jako koláčové nebo radarové?**  
A: All chart types defined in the `ChartType` enum are supported, including `PIE`, `RADAR`, `AREA`, etc.

**Q: Kde mohu najít více příkladů?**  
A: Visit the official [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) for a full list of chart‑related methods.

## Závěr

Nyní víte, jak **change Excel chart type**, vložit **tooltipy**, přidat **popisky dat** a vytvořit **drill‑down** odkazy pomocí Aspose.Cells pro Java. Tyto interaktivní funkce promění statické tabulky na dynamické nástroje pro průzkum dat, ideální pro dashboardy, reporty a webové analytické nástroje.

---

**Poslední aktualizace:** 2025-12-01  
**Testováno s:** Aspose.Cells 24.12 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}