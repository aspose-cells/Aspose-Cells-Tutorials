---
date: 2025-12-05
description: Naučte se, jak přidat popisky dat do grafu a vytvořit interaktivní graf
  v Javě pomocí Aspose.Cells. Přidejte tooltipy, popisky dat a funkci drill‑down.
language: cs
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Přidání popisků dat do grafu s interaktivitou v Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání popisků dat do grafu s interaktivitou v Aspose.Cells Java

Interaktivní grafy umožňují uživatelům prozkoumávat data za běhu. V tomto tutoriálu **přidáte funkce popisků dat do grafu** — tooltipy, popisky dat a akce drill‑down — pomocí Aspose.Cells pro Java. Na konci budete mít vyladěný, interaktivní graf, který okamžitě zpřehlední složitá data.

## Rychlé odpovědi
- **Jaká knihovna je potřeba?** Aspose.Cells for Java  
- **Mohu přidat tooltipy do grafu v Excelu?** Ano — použijte nastavení popisků dat v API.  
- **Které typy grafů podporují interaktivitu?** Většina vestavěných typů (sloupcový, čárový, koláčový atd.).  
- **Potřebuji licenci pro produkci?** Vyžaduje se platná licence Aspose.Cells.  
- **Jak dlouho trvá implementace?** Přibližně 10–15 minut pro základní graf.

## Co je „add data labels chart“?
*Add data labels chart* je graf, ve kterém každý datový bod zobrazuje popisek (hodnotu, název nebo vlastní text) přímo na vizualizaci. To usnadňuje čtení přesných hodnot bez nutnosti najíždění myší nebo porovnávání s oddělenou legendou.

## Proč vytvářet interaktivní řešení grafů v Javě?
Vložení interaktivity — tooltipy, klikatelné body, odkazy drill‑down — promění statické tabulky na průzkumné dashboardy. Uživatelé mohou:
- Rychle identifikovat odlehlé hodnoty.  
- Přistupovat k podrobnějším úrovním dat jedním kliknutím.  
- Zrychlit rozhodování snížením potřeby samostatných reportů.

## Požadavky

Než začneme, ujistěte se, že máte:

- Vývojové prostředí Java (doporučeno JDK 8+).  
- Knihovnu Aspose.Cells for Java (stáhněte z [zde](https://releases.aspose.com/cells/java/)).  

## Krok 1: Nastavení Java projektu

1. Vytvořte nový Java projekt ve svém oblíbeném IDE (IntelliJ, Eclipse, VS Code atd.).  
2. Přidejte JAR Aspose.Cells for Java do classpath projektu.

## Krok 2: Načtení dat

Pro vytvoření interaktivního grafu nejprve potřebujete data v listu. Níže uvedený úryvek načte existující sešit nazvaný **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Krok 3: Vytvoření grafu

Nyní vytvoříme sloupcový graf a umístíme jej do listu. Klidně můžete `ChartType.COLUMN` nahradit jiným typem, pokud chcete.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Krok 4: Přidání interaktivity — Jádro „add data labels chart“

### 4.1. Přidání tooltipů (add tooltips excel chart)

Tooltipy se zobrazí, když uživatel najede myší na datový bod. Následující kód je povolí zapnutím popisků dat a zobraím hodnoty.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Přidání popisků dat (add data labels chart)

Popisky dat jsou vizuální text umístěný vedle každého bodu. Tento úryvek nastaví graf tak, aby zobrazoval popisky typu callout místo prostých hodnot.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implementace drill‑down (create interactive chart java)

Drill‑down umožňuje uživatelům kliknout na bod a přejít na podrobný pohled. Zde připojujeme hypertextový odkaz k prvnímu datovému bodu; můžete to zopakovat pro libovolný bod, který potřebujete.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Krok 5: Uložení sešitu

Po nastavení grafu uložte sešit do nového souboru, abyste jej mohli otevřít v Excelu a otestovat interaktivitu.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Časté problémy a tipy

| Problém | Řešení |
|---------|--------|
| **Tooltipy se nezobrazují** | Ujistěte se, že je volána `setHasDataLabels(true)` před nastavením `ShowValue`. |
| **Hyperlink není klikací** | Ověřte, že URL je správně vytvořena a že nastavení zabezpečení v Excelu povoluje externí odkazy. |
| **Nesoulad typu grafu** | Některé typy grafů (např. radar) mají omezenou podporu popisků — zvolte kompatibilní typ, jako je sloupcový nebo čárový. |
| **Zpomalení při velkých datech** | Omezte počet bodů s popisky; zvažte `setShowValue(false)` pro méně kritické řady. |

## Často kladené otázky

**Q: Jak mohu změnit typ grafu?**  
A: Upravit enum `ChartType` v řádku tvorby grafu (např. `ChartType.LINE` pro čárový graf).

**Q: Mohu přizpůsobit vzhled tooltipů?**  
A: Ano — použijte vlastnosti písma, barvy pozadí a okraje objektu `DataLabel` k úpravě tooltipů.

**Q: Jak zvládnout uživatelské interakce ve webové aplikaci?**  
A: Exportujte sešit do HTML nebo použijte Aspose.Cells Cloud k vykreslení grafu a zachyťte klikací události pomocí JavaScriptu.

**Q: Kde najdu více příkladů a dokumentaci?**  
A: Navštivte [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pro úplný seznam tříd a metod souvisejících s grafy.

## Závěr

V tomto průvodci jsme ukázali, jak **přidat popisky dat do grafu** a vytvořit **interaktivní graf v Javě** pomocí Aspose.Cells. Přidáním tooltipů, popisků a hypertextových odkazů drill‑down proměníte statický Excel graf na dynamický nástroj pro průzkum dat, který zvyšuje přehlednost i použitelnost.

---

**Poslední aktualizace:** 2025-12-05  
**Testováno s:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}