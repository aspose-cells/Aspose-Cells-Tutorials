---
date: 2026-08-21
description: Naučte se, jak přidat tooltipy, datové popisky a změnit typ grafu v grafech
  Excel pomocí Aspose.Cells for Java – krok za krokem průvodce s interaktivními příklady.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Změna typu grafu v Excelu
og_description: Naučte se, jak přidat tooltipy, datové popisky a změnit typ grafu
  v grafech Excel pomocí Aspose.Cells for Java – krok za krokem průvodce s interaktivními
  příklady.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Jak přidat tooltipy a datové popisky do grafů Excel v jazyce Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Jak přidat tooltipy a datové popisky do grafů Excel v jazyce Java
url: /cs/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání popisků dat do grafu Excel a změna typu grafu – Aspose.Cells Java

Interaktivní grafy dávají vašim Excelovým reportům novou úroveň přehledu a **jak přidat tooltipy** umožňují okamžité čtení informací. V tomto tutoriálu se naučíte, jak **přidat popisky dat do grafu Excel**, **změnit typ grafu** a vytvořit interaktivní Java řešení s Aspose.Cells. Také vám ukážeme, jak přidat tooltipy a jednoduchý drill‑down hypertextový odkaz, aby si vaše publikum mohlo data podrobně prozkoumat.

## Rychlé odpovědi
- **Jaká knihovna se používá?** Aspose.Cells for Java  
- **Mohu změnit typ grafu?** Ano – stačí upravit výčtový typ `ChartType` při vytváření grafu.  
- **Jak přidám tooltipy do grafu?** Použijte API pro popisky dat (`setHasDataLabels(true)`) a povolte zobrazování hodnot.  
- **Je podporován drill‑down?** Můžete připojit hypertextové odkazy k datovým bodům pro základní drill‑down chování.  
- **Požadavky?** Java IDE, Aspose.Cells JAR a soubor Excel se vzorovými daty.

## Co je „jak přidat tooltipy“?
**Jak přidat tooltipy** označuje proces povolení textu při najetí myší, který zobrazuje hodnotu datového bodu nebo vlastní informace na grafu Excel. V Aspose.Cells se to dosahuje nastavením popisků dat grafu. Tooltipy pomáhají uživatelům rychle pochopit data, aniž by graf zahlcovaly, a lze je přizpůsobit fontu, barvě a formátu.

## Proč používat interaktivní grafy s Aspose.Cells?
Aspose.Cells podporuje **více než 50 vstupních a výstupních formátů** – včetně XLSX, CSV, PDF a HTML – a může zpracovávat sešity s **více než 1 000 listy** bez načítání celého souboru do paměti, což poskytuje rychlé generování grafů na serveru pro podnikovou tvorbu reportů. Interaktivní grafy také umožňují vkládání hypertextových odkazů, dynamické aktualizace dat a export do webových formátů, což je ideální pro dashboardy a portály reportování.

## Požadavky

- Java vývojové prostředí (doporučeno JDK 8+)  
- Aspose.Cells pro Java knihovna (stáhněte z [stránky ke stažení Aspose.Cells pro Java](https://releases.aspose.com/cells/java/))  
- Ukázkový sešit (`data.xlsx`) obsahující data, která chcete vizualizovat  

## Krok 1: nastavení vašeho Java projektu

1. Vytvořte nový Java projekt ve vašem oblíbeném IDE (IntelliJ IDEA, Eclipse atd.).  
2. Přidejte Aspose.Cells JAR do cesty sestavení vašeho projektu nebo do Maven/Gradle závislostí.

## Krok 2: načítání dat

Pro práci s grafy nejprve potřebujete načíst sešit do paměti.

Třída `Workbook` představuje soubor Excel a `Worksheet` představuje jednotlivý list v tomto souboru.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Jak změnit typ grafu v Aspose.Cells?

Vytvořte nový graf s požadovaným výčtem `ChartType`; Aspose.Cells nemění typ existujícího grafu přímo, takže musíte přidat nový graf požadovaného typu a případně odstranit ten starý. Tento přístup zajišťuje, že všechny řady a osy jsou správně přestavěny pro novou vizuální reprezentaci.

## Krok 3: vytvoření grafu (a změna jeho typu)

Můžete zvolit jakýkoli typ grafu, který vyhovuje vaší analýze. Níže vytvoříme **sloupcový graf**, ale můžete snadno přepnout na čárový, koláčový nebo pruhový graf změnou výčtu `ChartType`.

Objekt `Chart` poskytuje metody pro konfiguraci vizuální reprezentace dat v listu.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Tip:** Pro **změnu typu grafu v Excelu** nahraďte `ChartType.COLUMN` za `ChartType.LINE`, `ChartType.PIE` atd.

## Jak přidat tooltipy do grafu Excel?

Načtěte svůj graf, povolte popisky dat a nastavte příznak `showValue`. Tooltip pak zobrazí podkladovou hodnotu buňky, kdykoli uživatel najede myší na datový bod v renderovaném souboru Excel nebo HTML zobrazení. Můžete také přizpůsobit font, barvu a pozadí tooltipu tak, aby odpovídaly stylu vašeho reportu.

Třída `DataLabel` řídí vzhled a obsah popisků dat, které zároveň slouží jako tooltipy.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Krok 4: přidání interaktivity

### 4.1. Přidání tooltipů (přidat tooltipy do grafu)

Tooltipy se zobrazí, když uživatel najede myší na datový bod. Následující kód povoluje popisky dat a zobrazuje hodnotu jako tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Přidání popisků dat – **přidat popisky dat do grafu Excel**

Popisky dat poskytují trvalý vizuální prvek přímo na grafu. Můžete je zobrazit jako bubliny pro lepší čitelnost.

Třída `DataLabel` řídí vzhled popisků na každé řadě. Voláním `setHasDataLabels(true)` a konfigurací vlastností jako `setShowValue(true)` vložíte číselnou hodnotu přímo do grafu, což ji okamžitě zpřístupní bez jakékoli interakce. Další možnosti vám umožní zobrazit názvy řad, procenta nebo vlastní text pro bohatší kontext.

> **Proč přidávat popisky dat?** Zahrnutí popisků dat přímo do grafu eliminuje potřebu, aby uživatelé najížděli myší nebo hádali hodnoty, čímž se zvyšuje přehlednost reportu.

### 4.3. Implementace drill‑down (hyperlink na datovém bodu)

Jednoduchý způsob, jak přidat funkci drill‑down, je připojit hypertextový odkaz k určitému bodu. Kliknutím na bod se otevře webová stránka s podrobnými informacemi.

Třída `Hyperlink` připojuje klikací odkaz k elementu grafu, což umožňuje navigaci drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Jak přidat popisky dat do grafu Excel?

Třída `DataLabel` řídí vzhled popisků na každé řadě. Voláním `setHasDataLabels(true)` a konfigurací vlastností jako `setShowValue(true)` vložíte číselnou hodnotu přímo do grafu, což ji okamžitě zpřístupní bez jakékoli interakce. Další možnosti vám umožní zobrazit názvy řad, procenta nebo vlastní text pro bohatší kontext.

## Krok 5: uložení sešitu

Po nakonfigurování grafu uložte sešit, aby byly interaktivní funkce uloženy v výstupním souboru.

Volání `workbook.save` zapíše upravený sešit do souboru ve zvoleném formátu.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Časté problémy a řešení

| Problém | Řešení |
|---------|--------|
| **Tooltipy se nezobrazují** | Ujistěte se, že `setHasDataLabels(true)` je voláno před konfigurací `setShowValue(true)`. |
| **Hyperlink není klikací** | Ověřte, že výstupní formát podporuje hypertextové odkazy (např. XLSX, ne CSV). |
| **Typ grafu se nezmění** | Zkontrolujte, že jste upravili správný výčet `ChartType` při přidávání grafu. |

## Často kladené otázky

**Q: Jak mohu změnit typ grafu po jeho vytvoření?**  
A: Musíte vytvořit nový graf s požadovaným `ChartType`. Aspose.Cells nenabízí konverzi typu přímo, takže odstraňte starý graf a přidejte nový.

**Q: Mohu přizpůsobit vzhled tooltipů?**  
A: Ano. Použijte vlastnosti `DataLabel`, jako jsou `setFontSize`, `setFontColor` a `setBackgroundColor`, k úpravě stylu textu tooltipu.

**Q: Jak zvládnu uživatelské interakce ve webové aplikaci?**  
A: Exportujte sešit do HTML nebo XLSX souboru a použijte JavaScript na straně klienta k zachycení kliknutí na elementy grafu.

**Q: Kde najdu více příkladů a dokumentaci?**  
A: Navštivte [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pro kompletní seznam tříd a metod souvisejících s grafy.

## Závěr

Nyní víte, jak **přidat popisky dat do grafu Excel**, **změnit typ grafu Excel**, **vytvořit interaktivní Java** řešení a obohatit je o tooltipy, popisky dat a drill‑down hypertextové odkazy pomocí Aspose.Cells pro Java. Tato vylepšení učiní vaše Excelové reporty mnohem poutavějšími a přínosnějšími pro koncové uživatele.

---

**Poslední aktualizace:** 2026-08-21  
**Testováno s:** Aspose.Cells for Java 24.12  
**Autor:** Aspose

## Související tutoriály

- [Jak upravit grafy Excel a popisky dat pomocí Aspose.Cells pro Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extrahování popisků os grafu Excel pomocí Aspose.Cells Java: Kompletní průvodce](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Vytvoření bublinových grafů v Excelu pomocí Aspose.Cells pro Java: krok za krokem](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}