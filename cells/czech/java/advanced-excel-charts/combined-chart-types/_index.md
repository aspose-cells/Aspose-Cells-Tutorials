---
date: 2026-02-14
description: Naučte se, jak exportovat graf do PNG, přidat datové řady, kombinovat
  sloupcový a čárový graf, uložit sešit jako XLSX a přidat legendu grafu pomocí Aspose.Cells
  pro Javu.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Exportovat graf do PNG a přidat datové řady pro kombinovaný graf
url: /cs/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export grafu do PNG a přidání datových sérií pro kombinovaný graf

V tomto tutoriálu **přidáte datové série** do sešitu Excel, **zkombinujete prvky čárového a sloupcového grafu** a naučíte se, jak **exportovat graf do PNG** pomocí Aspose.Cells pro Java. Provedeme vás každým krokem – od nastavení sešitu, přidání grafu do listu, úpravy legendy, až po **uložení sešitu jako xlsx** a vytvoření PNG obrázku grafu. Na konci budete mít připravený kombinovaný graf, který můžete vložit do zpráv nebo dashboardů.

## Rychlé odpovědi
- **Která knihovna vytváří kombinované grafy?** Aspose.Cells for Java  
- **Jak přidám datovou sérii?** Použijte `chart.getNSeries().add(...)`  
- **Jak mohu exportovat graf do png?** Zavolejte `chart.toImage("file.png", ImageFormat.getPng())`  
- **Do jakého formátu mohu uložit sešit?** Standardní `.xlsx` (uložit sešit jako xlsx)  
- **Potřebuji licenci pro produkci?** Je vyžadována platná licence Aspose.Cells  

## Co je **export grafu do PNG** v Aspose.Cells?
Export grafu do PNG vytvoří rastrový obrázek grafu z Excelu, který lze zobrazit na webových stránkách, v reportech nebo e‑mailech bez nutnosti aplikace Excel.

## Proč vytvořit **kombinovaný čárový a sloupcový graf**?
Kombinovaný graf vám umožní zobrazit různé datové sady s odlišnými vizuálními reprezentacemi (např. čárovou sérii nad sloupcovou sérií) v jednom zobrazení. To je ideální pro porovnání trendů s celkovými hodnotami, zvýraznění korelací nebo poskytování bohatších poznatků v kompaktním formátu.

## Prerequisites
- Java Development Kit (JDK) 8 nebo vyšší  
- Knihovna Aspose.Cells pro Java (stáhněte z odkazu níže)  
- Základní znalost syntaxe Java a konceptů Excelu  

## Getting Started

Nejprve stáhněte knihovnu Aspose.Cells pro Java z oficiálního webu:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Jakmile je JAR přidán do classpath vašeho projektu, můžete začít vytvářet graf.

### Krok 1: Importujte třídy Aspose.Cells
```java
import com.aspose.cells.*;
```

### Krok 2: Vytvořte nový sešit
```java
Workbook workbook = new Workbook();
```

### Krok 3: Získejte první list
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 4: Přidejte objekt kombinovaného grafu do listu  
Začneme s čárovým grafem a později přidáme sloupcovou sérii, abychom dosáhli efektu **kombinovaného čárového a sloupcového grafu**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Přidání dat do grafu

Jakmile existuje kontejner grafu, musíme ho naplnit daty.

### Krok 5: Definujte datové rozsahy a **přidejte datovou sérii**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Tip:** První parametr (`"A1:A5"`) je rozsah pro první sérii a druhý (`"B1:B5"`) vytváří druhou sérii, která bude kombinována s první.

### Krok 6: Nastavte data kategorie (osa X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Přizpůsobení grafu

Dobrý graf vypráví příběh. Přidejme mu názvy, popisky os a přehlednou legendu.

### Krok 7: **Nastavte popisky os grafu** a název
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Krok 8: **Přidejte legendu grafu** a upravte její umístění
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Ukládání a export grafu

Po úpravách budete chtít **uložit sešit jako xlsx** a také vygenerovat obrázek.

### Krok 9: Uložte sešit jako soubor Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Krok 10: **Exportujte graf do PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoda `chart.toImage` **generuje obrázky grafu z Excelu**, které lze použít na webových stránkách, v reportech nebo e‑mailech.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Žádná data se nezobrazují** | Ověřte, že rozsahy buněk (`A1:A5`, `B1:B5`, `C1:C5`) skutečně obsahují data před vytvořením grafu. |
| **Legenda překrývá graf** | Nastavte `chart.getLegend().setOverlay(false)` nebo legendu přesuňte na jiné místo (např. `RIGHT`). |
| **Obrázkový soubor je prázdný** | Ujistěte se, že graf má alespoň jednu sérii a že `chart.toImage` je voláno po všech úpravách. |
| **Ukládání vyvolá výjimku** | Zkontrolujte, že máte oprávnění k zápisu do cílového adresáře a že soubor není otevřen v Excelu. |

## Často kladené otázky

**Q: Jak nainstaluji Aspose.Cells pro Java?**  
A: Stáhněte JAR z oficiálního webu a přidejte jej do classpath vašeho projektu. Odkaz ke stažení je: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Mohu vytvořit jiné typy grafů než čárový a sloupcový?**  
A: Ano, Aspose.Cells podporuje pruhové, koláčové, rozptylové, plošné a mnoho dalších typů grafů. Viz dokumentace API pro úplný seznam.

**Q: Je licence vyžadována pro produkční použití?**  
A: Pro produkční nasazení je vyžadována platná licence Aspose.Cells. K dispozici je bezplatná zkušební verze pro vyhodnocení.

**Q: Jak mohu změnit barvy jednotlivých sérií?**  
A: Použijte `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (nebo podobně) po přidání sérií.

**Q: Kde najdu více ukázek kódu?**  
A: Kompletní dokumentace a další příklady jsou k dispozici na referenční stránce Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Poslední aktualizace:** 2026-02-14  
**Testováno s:** Aspose.Cells for Java nejnovější verze  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}