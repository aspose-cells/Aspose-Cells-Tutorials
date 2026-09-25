---
date: 2026-02-09
description: Naučte se, jak přidat datové popisky do grafu v Excelu a změnit typ grafu
  pomocí Aspose.Cells pro Javu, plus tooltipy a interaktivitu drill‑down.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Přidat popisky dat do grafu v Excelu pomocí Aspose.Cells Java
url: /cs/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání popisků dat do grafu Excel a změna typu grafu – Aspose.Cells Java

Interaktivní grafy dodávají vašim Excelovým reportům novou úroveň přehledu a **přidání popisků dat do grafu Excel** umožňuje okamžité čtení informací. V tomto tutoriálu se naučíte, jak **přidat popisky dat do grafu Excel**, změnit typ grafu a vytvořit interaktivní Java řešení s Aspose.Cells. Také vám ukážeme, jak přidat tooltipy a jednoduchý drill‑down hypertextový odkaz, aby si vaše publikum mohlo data podrobně prozkoumat.

## Rychlé odpovědi
- **Jaká knihovna se používá?** Aspose.Cells for Java  
- **Mohu změnit typ grafu?** Ano – stačí upravit výčtový typ `ChartType` při vytváření grafu.  
- **Jak přidám tooltipy do grafu?** Použijte API pro popisky dat (`setHasDataLabels(true)`) a povolte zobrazování hodnot.  
- **Je podporován drill‑down?** Můžete připojit hypertextové odkazy k datovým bodům pro základní drill‑down chování.  
- **Požadavky?** Java IDE, Aspose.Cells JAR a Excel soubor se vzorovými daty.

## Požadavky

Než začnete, ujistěte se, že máte následující:

- Vývojové prostředí Java (doporučeno JDK 8+)  
- Knihovna Aspose.Cells for Java (stáhněte z [zde](https://releases.aspose.com/cells/java/))  
- Vzorková sešit (`data.xlsx`) obsahující data, která chcete vizualizovat  

## Krok 1: Nastavení Java projektu

1. Vytvořte nový Java projekt ve svém oblíbeném IDE (IntelliJ IDEA, Eclipse atd.).  
2. Přidejte Aspose.Cells JAR do cesty sestavení projektu nebo do Maven/Gradle závislostí.

## Krok 2: Načtení dat

Pro práci s grafy nejprve potřebujete načíst sešit do paměti.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Krok 3: Vytvoření grafu (a změna jeho typu)

Můžete zvolit jakýkoli typ grafu, který vyhovuje vaší analýze. Níže vytvoříme **sloupcový graf**, ale snadno můžete přepnout na čárový, koláčový nebo pruhový graf změnou výčtového typu `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Tip:** Pro **změnu typu grafu v Excelu** nahraďte `ChartType.COLUMN` za `ChartType.LINE`, `ChartType.PIE` atd.

## Krok 4: Přidání interaktivity

### 4.1. Přidání tooltipů (Add Tooltips to Chart)

Tooltipy se zobrazí, když uživatel najede kurzorem na datový bod. Následující kód povolí popisky dat a zobrazí hodnotu jako tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Přidání popisků dat – **add data labels to excel chart**

Popisky dat poskytují trvalý vizuální prvek přímo v grafu. Můžete je zobrazit jako bubliny pro lepší čitelnost.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Proč přidávat popisky dat?** Umístěním popisků přímo do grafu eliminuje potřebu, aby uživatelé najížděli nebo hádali hodnoty, čímž se zvyšuje srozumitelnost reportu.

### 4.3. Implementace drill‑down (hyperlink na datový bod)

Jednoduchý způsob, jak přidat drill‑down funkci, je připojit hypertextový odkaz ke konkrétnímu bodu. Kliknutím na bod se otevře webová stránka s podrobnými informacemi.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Krok 5: Uložení sešitu

Po nastavení grafu uložte sešit, aby byly interaktivní funkce uloženy v výstupním souboru.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Tooltipy se nezobrazují** | Ujistěte se, že je voláno `setHasDataLabels(true)` před konfigurací `setShowValue(true)`. |
| **Hyperlink není klikací** | Ověřte, že výstupní formát podporuje hypertextové odkazy (např. XLSX, ne CSV). |
| **Typ grafu se nezmění** | Zkontrolujte, že jste upravili správný výčtový typ `ChartType` při přidávání grafu. |

## Často kladené otázky

**Q: Jak mohu změnit typ grafu po jeho vytvoření?**  
A: Musíte vytvořit nový graf s požadovaným `ChartType`. Aspose.Cells nenabízí konverzi typu „na místě“, takže odeberte starý graf a přidejte nový.

**Q: Mohu upravit vzhled tooltipů?**  
A: Ano. Použijte vlastnosti `DataLabel`, jako jsou `setFontSize`, `setFontColor` a `setBackgroundColor`, pro stylizaci textu tooltipu.

**Q: Jak zvládnout uživatelské interakce ve webové aplikaci?**  
A: Exportujte sešit do HTML nebo XLSX souboru a použijte JavaScript na straně klienta k zachycení kliknutí na elementy grafu.

**Q: Kde najdu více příkladů a dokumentaci?**  
A: Navštivte [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pro kompletní seznam tříd a metod souvisejících s grafy.

## Závěr

Nyní víte, jak **přidat popisky dat do grafu Excel**, **změnit typ grafu v Excelu**, **vytvořit interaktivní Java řešení pro grafy** a obohatit je o tooltipy, popisky dat a drill‑down hypertextové odkazy pomocí Aspose.Cells for Java. Tyto vylepšení učiní vaše Excelové reporty mnohem poutavějšími a přínosnějšími pro koncové uživatele.

---

**Poslední aktualizace:** 2026-02-09  
**Testováno s:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}