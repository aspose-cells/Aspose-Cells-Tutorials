---
date: 2026-09-02
description: Naučte se, jak vytvořit vodopádový graf v Excelu v jazyce Java pomocí
  Aspose.Cells, nastavit rozsah dat grafu, přizpůsobit popisky a exportovat do formátu
  XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Vodopádové grafy
og_description: Vytvořte vodopádový graf v Excelu pomocí Aspose.Cells pro Java – nastavte
  rozsah dat grafu, přidejte popisky dat a exportujte do formátu XLSX během několika
  kroků.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Vytvořte vodopádový graf v Excelu pomocí Aspose.Cells pro Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Vytvořte vodopádový graf v Excelu pomocí Aspose.Cells pro Java
url: /cs/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vodopádové grafy

## Úvod do vodopádových grafů pomocí Aspose.Cells pro Java

V tomto tutoriálu se naučíte, jak **vytvořit vodopádový graf v Excelu** a **nastavit rozsah dat grafu** pomocí Aspose.Cells pro Java. Vodopádové grafy převádějí sérii kladných a záporných čísel na přehledný vizuální příběh, což je činí ideálními pro finanční výkazy, přehledy prodeje a jakýkoli scénář, kde potřebujete vidět, jak jednotlivé položky přispívají k celku.

## Rychlé odpovědi
- **Co je vodopádový graf?** Vizuál, který ukazuje, jak je počáteční hodnota zvýšena a snížena sérií mezihodnot, končící konečným součtem.  
- **Která knihovna se používá?** Aspose.Cells pro Java.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována komerční licence.  
- **Mohu soubor uložit jako XLSX?** Ano – použijte `workbook.save("FileName.xlsx")`.  
- **Je vhodný pro vizualizaci dat v Javě?** Rozhodně; Aspose.Cells poskytuje bohaté funkce pro tvorbu grafů bez nutnosti instalace Office.

## Co je vodopádový graf?
Vodopádový graf zobrazuje sekvenční kladné a záporné příspěvky k počáteční hodnotě, což vám pomáhá pochopit, jak každý komponent ovlivňuje celkový výsledek. Vizualizací zisků a ztrát vedle sebe činí složité finanční toky okamžitě čitelné.

## Proč použít Aspose.Cells pro Java k přidání vodopádového grafu?
Aspose.Cells vám umožňuje generovat Excel grafy na jakémkoli serveru, v CI pipeline nebo na desktopu bez potřeby Microsoft Excel. Podporuje **15+ výstupních formátů** (XLSX, PDF, HTML, CSV a další), zpracovává sešity s **500+ řádky** za méně než sekundu a poskytuje programový přístup ke každému prvku grafu – od barev po popisky dat.

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte následující předpoklady:

- Aspose.Cells pro Java: Budete potřebovat nainstalovaný Aspose.Cells pro Java. Můžete jej stáhnout ze stránky vydání Aspose.Cells pro Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Vývojové prostředí Java: Ujistěte se, že máte na svém systému nainstalovanou Javu a připravený nástroj pro sestavení (Maven/Gradle).

Nyní začněme krok za krokem vytvářet vodopádový graf.

## Jak nastavit rozsah dat grafu pro vodopádový graf v Javě
Načtěte nový sešit, naplňte jej daty, přidejte objekt `Chart`, definujte rozsah řady a nakonec soubor uložte. Tento proces je jednoduchý: vytvoříte sešit, vyplníte buňky kategoriemi a hodnotami, vytvoříte graf, svázete datové rozsahy a poté sešit exportujete. Výsledkem je plně funkční vodopádový graf připravený k použití v reportech nebo řídicích panelech.

### Krok 1: import Aspose.Cells
Balíček `com.aspose.cells` obsahuje všechny třídy potřebné pro manipulaci s Excelem, včetně vytváření sešitů, práce s listy a generování grafů.

### Krok 2: inicializace sešitu a listu
**Workbook** představuje soubor Excel a **Worksheet** je jediný list v tomto souboru. Vytvoření těchto objektů poskytuje plátno jak pro surová data, tak pro graf.

### Krok 3: zadání dat
Sloupec A obsahuje štítky kategorií, zatímco sloupec B obsahuje číselné hodnoty pro vodopád. Toto uspořádání odpovídá typickému toku zisk‑a‑ztráta používanému ve finanční analýze.

### Krok 4: vytvoření vodopádového grafu
Objekt **Chart** vytváří vizuální reprezentaci; nastavením jeho typu na `ChartType.WATERFALL` jej konfiguruje jako vodopádový graf. Použijte metodu `add` k nastavení rozsahu dat grafu pro řadu (`"B2:B6"`) a propojte osu kategorií s `"A2:A6"`.

### Krok 5: uložení sešitu
Uložení sešitu zapíše graf a data do zvoleného formátu souboru. Zavolejte `workbook.save("WaterfallChart.xlsx")` pro vytvoření souboru XLSX, nebo změňte parametr formátu pro export do PDF, CSV nebo HTML.

## Časté problémy a řešení

- **Graf se zobrazuje prázdně** – Ověřte, že odkazy na datové rozsahy (`B2:B6` a `A2:A6`) odpovídají skutečným buňkám obsahujícím vaše hodnoty a kategorie.  
- **Záporné hodnoty se nezobrazují správně** – Ujistěte se, že typ řady je nastaven na `ChartType.WATERFALL`; jiné typy grafů zacházejí se zápornými hodnotami odlišně.  
- **Soubor se neotevírá v Excelu** – Použijte nejnovější verzi Aspose.Cells a potvrďte, že přípona souboru odpovídá formátu (`.xlsx` pro Excel).

## Často kladené otázky

### Jak mohu přizpůsobit vzhled mého vodopádového grafu?
Můžete upravit vlastnosti jako `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` pro změnu barev sloupců, povolit popisky dat pomocí `setShowDataLabels(true)` a upravit názvy os pomocí `getCategoryAxis().setTitle("Stage")`. Referenční příručka Aspose.Cells API poskytuje úplný seznam přizpůsobitelných možností.

### Mohu vytvořit více vodopádových grafů ve stejném listu?
Ano. Po přidání prvního grafu opakujte kroky tvorby grafu s jiným datovým rozsahem a novým objektem `Chart`. Každý graf je nezávislý a může být umístěn kdekoli na listu.

### Je Aspose.Cells kompatibilní s různými vývojovými prostředími Java?
Rozhodně. Knihovna funguje s Eclipse, IntelliJ IDEA, NetBeans a jakýmkoli systémem sestavení, který podporuje Maven nebo Gradle. Žádné další pluginy nejsou vyžadovány.

### Mohu přidat další datové řady do mého vodopádového grafu?
Můžete přidat více řad voláním `chart.getNSeries().add("C2:C6", true)` a samostatným nastavením každé řady. To vám umožní porovnat více scénářů vedle sebe.

### Kde najdu další zdroje a příklady pro Aspose.Cells pro Java?
Prozkoumejte úplnou dokumentaci v referenci Aspose.Cells Java API: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: Jak nastavit rozsah dat grafu pro finanční vodopádový graf?**  
A: Použijte metodu `add` na sérii grafu a předávejte rozsah buněk, který obsahuje vaše hodnoty, např. `"B2:B6"`.

**Q: Mohu exportovat sešit do PDF místo XLSX?**  
A: Ano, zavolejte `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` pro vytvoření verze PDF.

**Q: Co když potřebuji vytvořit vodopádový graf s více kategoriemi?**  
A: Rozšiřte datový rozsah jak ve sloupci hodnot, tak ve sloupci kategorií a poté podle toho aktualizujte volání `add` a `setCategoryData`.

**Q: Existuje způsob, jak automaticky formátovat kladné a záporné sloupce?**  
A: Procházejte kolekci `Series` a nastavte barvu `FillFormat` podle znaménka každé hodnoty; Aspose.Cells vám umožní aplikovat podmíněné formátování programově.

**Q: Podporuje Aspose.Cells dynamické aktualizace dat pro grafy?**  
A: Ano. Po úpravě hodnot v buňkách stačí znovu uložit sešit – graf automaticky zobrazí nová data.

---

**Poslední aktualizace:** 2026-09-02  
**Testováno s:** Aspose.Cells pro Java (nejnovější)  
**Autor:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

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

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Související tutoriály

- [Přizpůsobení popisků dat v Excel grafu pomocí Aspose.Cells pro Java: Průvodce krok za krokem](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Přidání popisků dat do Excel grafu s Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Jak vytvořit a exportovat grafy v Javě pomocí Aspose.Cells: Kompletní průvodce](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}