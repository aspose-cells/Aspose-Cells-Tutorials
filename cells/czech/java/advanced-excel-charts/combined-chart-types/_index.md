---
date: 2025-12-06
description: Naučte se, jak přidat datové řady, vytvořit kombinované typy grafů, uložit
  sešit Excel a exportovat graf do PNG pomocí Aspose.Cells pro Javu.
language: cs
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Přidejte datové řady k vytvoření kombinovaného grafu pomocí Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání datových řad pro vytvoření kombinovaného grafu pomocí Aspose.Cells

V tomto tutoriálu **přidáte datové řady** do sešitu Excel a naučíte se, jak **vytvořit kombinované typy grafů** pomocí Aspose.Cells pro Java. Provedeme vás každým krokem – od nastavení sešitu, přidání řad, úpravy legendy, až po **uložení sešitu Excel** a export **grafu do PNG**. Na konci budete mít připravený kombinovaný graf, který můžete vložit do zpráv nebo dashboardů.

## Rychlé odpovědi
- **Která knihovna vytváří kombinované grafy?** Aspose.Cells pro Java  
- **Jak přidám datovou řadu?** Použijte `chart.getNSeries().add(...)`  
- **Mohu exportovat graf jako obrázek?** Ano, pomocí `chart.toImage(...)` (PNG)  
- **Do jakého formátu mohu sešit uložit?** Standardní `.xlsx` (Excel)  
- **Potřebuji licenci pro produkci?** Vyžaduje se platná licence Aspose.Cells  

## Co je **add data series** v Aspose.Cells?
Přidání datové řady říká grafu, které buňky obsahují hodnoty, které chcete vykreslit. Každá řada může představovat čáru, sloupec nebo jiný typ grafu a můžete je kombinovat pro vytvoření **kombinovaného grafu**.

## Proč vytvářet **combined chart**?
Kombinovaný graf vám umožní zobrazit různé datové sady s odlišnými vizuálními reprezentacemi (např. čárovou řadou nad sloupcovým grafem) v jedné zobrazení. To je ideální pro porovnání trendů s celky, zvýraznění korelací nebo poskytování bohatších informací v kompaktním formátu.

## Předpoklady
- Java Development Kit (JDK) 8 nebo vyšší  
- Knihovna Aspose.Cells pro Java (stáhněte z odkazu níže)  
- Základní znalost syntaxe Javy a konceptů Excelu  

## Začínáme

Nejprve si stáhněte knihovnu Aspose.Cells pro Java z oficiálního webu:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Jakmile přidáte JAR do classpath vašeho projektu, můžete začít vytvářet graf.

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

### Krok 4: Přidejte objekt kombinovaného grafu  
Začneme s čárovým grafem a později přidáme další řady, abychom dosáhli efektu **kombinovaného grafu**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Přidání dat do grafu

Nyní, když existuje kontejner grafu, musíme jej naplnit daty.

### Krok 5: Definujte datové rozsahy a **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Tip:** První parametr (`"A1:A5"`) je rozsah pro první řadu a druhý (`"B1:B5"`) vytváří druhou řadu, která bude kombinována s první.

### Krok 6: Nastavte data kategorií (osa X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Úprava grafu

Dobrý graf vypráví příběh. Přidáme mu názvy, popisky os a přehlednou legendu.

### Krok 7: Nastavte název grafu a popisky os
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Krok 8: **Add legend chart** a upravte její umístění
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Ukládání a export grafu

Po úpravách budete chtít **uložit sešit Excel** a také vygenerovat obrázek.

### Krok 9: Uložte sešit jako soubor Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Krok 10: Exportujte **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoda `chart.toImage` **generuje obrázky excelových grafů**, které lze použít na webových stránkách, v reportech nebo e‑mailech.

## Časté problémy a řešení

| Problém | Řešení |
|-------|----------|
| **Neobjevují se žádná data** | Ověřte, že rozsahy buněk (`A1:A5`, `B1:B5`, `C1:C5`) skutečně obsahují data před vytvořením grafu. |
| **Legenda překrývá graf** | Nastavte `chart.getLegend().setOverlay(false)` nebo přesuňte legendu na jiné místo (např. `RIGHT`). |
| **Soubor obrázku je prázdný** | Ujistěte se, že graf má alespoň jednu řadu a že `chart.toImage` je voláno po všech úpravách. |
| **Ukládání vyvolá výjimku** | Zkontrolujte, že máte oprávnění zapisovat do cílového adresáře a že soubor není otevřen v Excelu. |

## Často kladené otázky

**Q: Jak nainstaluji Aspose.Cells pro Java?**  
A: Stáhněte JAR z oficiálního webu a přidejte jej do classpath projektu. Odkaz ke stažení: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Mohu vytvořit jiné typy grafů než čáru a sloupec?**  
A: Ano, Aspose.Cells podporuje sloupcové, koláčové, rozptylové, plošné a mnoho dalších typů grafů. Podívejte se do API dokumentace pro úplný seznam.

**Q: Je licence vyžadována pro produkční použití?**  
A: Pro nasazení do produkce je nutná platná licence Aspose.Cells. K dispozici je také bezplatná zkušební verze pro hodnocení.

**Q: Jak mohu změnit barvy jednotlivých řad?**  
A: Použijte `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (nebo podobně) po přidání řady.

**Q: Kde najdu další ukázky kódu?**  
A: Rozsáhlá dokumentace a další příklady jsou k dispozici na referenčním webu Aspose: [here](https://reference.aspose.com/cells/java/).

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**Poslední aktualizace:** 2025-12-06  
**Testováno s:** Aspose.Cells pro Java 24.12  
**Autor:** Aspose  

---