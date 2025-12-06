---
date: 2025-12-06
description: Naučte se, jak změnit typ grafu v Excelu a vytvářet interaktivní grafy
  v Javě pomocí Aspose.Cells. Přidejte do grafu tooltipy, popisky dat a drill‑down
  pro bohatší vizualizaci dat.
language: cs
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Změňte typ grafu v Excelu pomocí Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Změna typu grafu v Excelu a přidání interaktivity

## Úvod

Interaktivní grafy dodají vašim Excelovým reportům novou úroveň přehledu, umožní uživatelům najíždět, kliknout a přímo prozkoumávat datové body. V tomto tutoriálu **změníte typ grafu v Excelu** a **vytvoříte interaktivní grafová řešení v Javě** pomocí Aspose.Cells for Java. Provedeme vás přidáním tooltipů do grafu, datových popisků a jednoduchého drill‑down hypertextového odkazu, aby vaše publikum mohlo hlouběji proniknout do čísel.

## Rychlé odpovědi
- **Jaká knihovna se používá?** Aspose.Cells for Java  
- **Mohu změnit typ grafu?** Ano – stačí upravit výčtový typ `ChartType` při vytváření grafu.  
- **Jak přidám tooltipy do grafu?** Použijte API datových popisků (`setHasDataLabels(true)`) a povolte zobrazení hodnot.  
- **Je podporováno drill‑down?** Můžete připojit hypertextové odkazy k datovým bodům pro základní chování drill‑down.  
- **Požadavky?** Java IDE, Aspose.Cells JAR a Excel soubor se vzorovými daty.

## Požadavky

Než začneme, ujistěte se, že máte následující:

- Java vývojové prostředí (doporučeno JDK 8+)  
- Knihovna Aspose.Cells for Java (stáhněte z [here](https://releases.aspose.com/cells/java/))  
- Vzorek sešitu (`data.xlsx`) obsahující data, která chcete vizualizovat  

## Krok 1: Nastavení Java projektu

1. Vytvořte nový Java projekt ve svém oblíbeném IDE (IntelliJ IDEA, Eclipse, atd.).  
2. Přidejte Aspose.Cells JAR do cesty sestavení projektu nebo do Maven/Gradle závislostí.

## Krok 2: Načtení dat

Pro práci s grafy potřebujete nejprve načíst sešit do paměti.

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

Tooltipy se zobrazí, když uživatel najede myší na datový bod. Následující kód povolí datové popisky a zobrazí hodnotu jako tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Přidání datových popisků

Datové popisky poskytují trvalou vizuální nápovědu přímo v grafu. Můžete je zobrazit jako bubliny pro lepší čitelnost.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implementace drill‑down (Hyperlink na datovém bodu)

Jednoduchý způsob, jak přidat funkci drill‑down, je připojit hypertextový odkaz k určitému bodu. Kliknutím na bod se otevře webová stránka s podrobnými informacemi.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Krok 5: Uložení sešitu

Po nakonfigurování grafu uložte sešit, aby se interaktivní funkce uložily do výstupního souboru.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Tooltipy se nezobrazují** | Ujistěte se, že `setHasDataLabels(true)` je voláno před nastavením `setShowValue(true)`. |
| **Hyperlink není klikací** | Ověřte, že výstupní formát podporuje hypertextové odkazy (např. XLSX, ne CSV). |
| **Typ grafu se nezmění** | Zkontrolujte, že jste upravili správný výčtový typ `ChartType` při přidávání grafu. |

## Často kladené otázky

**Q: Jak mohu změnit typ grafu po jeho vytvoření?**  
A: Musíte vytvořit nový graf s požadovaným `ChartType`. Aspose.Cells nenabízí konverzi typu přímo, takže odstraňte starý graf a přidejte nový.

**Q: Mohu přizpůsobit vzhled tooltipů?**  
A: Ano. Použijte vlastnosti `DataLabel`, jako jsou `setFontSize`, `setFontColor` a `setBackgroundColor`, k úpravě stylu textu tooltipu.

**Q: Jak mohu zpracovat uživatelské interakce ve webové aplikaci?**  
A: Exportujte sešit do HTML nebo XLSX souboru a použijte JavaScript na straně klienta k zachycení kliknutí na elementy grafu.

**Q: Kde najdu více příkladů a dokumentaci?**  
A: Navštivte [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pro kompletní seznam tříd a metod souvisejících s grafy.

## Závěr

Nyní víte, jak **změnit typ grafu v Excelu**, **vytvořit interaktivní grafová řešení v Javě** a obohatit je o tooltipy, datové popisky a drill‑down hypertextové odkazy pomocí Aspose.Cells for Java. Tyto vylepšení učiní vaše Excelové reporty mnohem poutavějšími a přínosnějšími pro koncové uživatele.

---

**Poslední aktualizace:** 2025-12-06  
**Testováno s:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}