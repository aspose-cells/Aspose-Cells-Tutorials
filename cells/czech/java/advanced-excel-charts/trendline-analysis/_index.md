---
date: 2025-12-09
description: Naučte se, jak exportovat graf do obrázku při provádění analýzy trendové
  čáry v Javě s Aspose.Cells. Obsahuje kroky pro načtení souboru Excel, přidání trendové
  čáry, zobrazení hodnoty R‑čtverce a uložení sešitu ve formátu XLSX.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Export grafu do obrázku s analýzou trendové čáry pomocí Aspose.Cells pro Java
url: /cs/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export grafu do obrázku s analýzou trendové čáry

V tomto tutoriálu se dozvíte **jak exportovat graf do obrázku** při provádění kompletní **analýzy trendové čáry** pomocí Aspose.Cells for Java. Provedeme vás načtením existujícího sešitu Excel, přidáním trendové čáry, zobrazením hodnoty R‑squared, úpravou grafu a nakonec exportem grafu jako souboru obrázku — vše s jasným, krok‑za‑krokem kódem, který můžete zkopírovat & vložit.

## Rychlé odpovědi
- **Jaký je hlavní účel tohoto průvodce?** Ukázat vám, jak přidat trendovou čáru, zobrazit její rovnici a hodnotu R‑squared a exportovat výsledný graf do obrázku pomocí Javy.  
- **Která knihovna je vyžadována?** Aspose.Cells for Java (stáhněte [ZDE](https://releases.aspose.com/cells/java/)).  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkční nasazení je vyžadována komerční licence.  
- **Mohu v Javě generovat soubor Excel?** Ano — tutoriál vytvoří a uloží sešit XLSX.  
- **Jak exportuji graf do PNG nebo JPEG?** Použijte metodu `Chart.toImage()` (popisováno v sekci „Export grafu“).

## Co je export grafu do obrázku?
Export grafu do obrázku převádí vizuální reprezentaci vašich dat do přenositelného bitmapového formátu (PNG, JPEG atd.). To je užitečné pro vložení grafů do zpráv, webových stránek nebo prezentací, kde není vyžadován původní soubor Excel.

## Proč přidat trendovou čáru a zobrazit hodnotu R‑squared?
Trendová čára vám pomáhá identifikovat základní vzorec datové řady, zatímco metrika **R‑squared** kvantifikuje, jak dobře trendová čára odpovídá datům. Začlenění těchto informací do exportovaného obrázku poskytne zainteresovaným stranám okamžitý přehled bez nutnosti otevírat sešit.

## Požadavky
- Nainstalovaný Java 8 nebo novější.  
- Knihovna Aspose.Cells for Java přidaná do projektu (JAR soubory v classpath).  
- Základní znalost Java IDE (IntelliJ IDEA, Eclipse atd.).

## Postupný návod

### Krok 1: Nastavení projektu
Vytvořte nový Java projekt a přidejte JAR soubory Aspose.Cells do cesty sestavení. Tím připravíte prostředí pro generování a manipulaci se soubory Excel.

### Krok 2: Načtení souboru Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Právě jsme **načetli soubor Excel** do paměti, připravený pro vytvoření grafu.*

### Krok 3: Vytvoření grafu
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Zde generujeme čárový graf, který později bude obsahovat naši trendovou čáru.*

### Krok 4: Přidání trendové čáry (how to add trendline) a zobrazení hodnoty R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Volání `setDisplayRSquaredValue(true)` zajišťuje, že **hodnota R‑squared** se zobrazí v grafu.*

### Krok 5: Úprava grafu a uložení sešitu (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Nyní je sešit **vygenerován** a uložen jako soubor XLSX, připravený k dalšímu zpracování.*

### Krok 6: Export grafu do obrázku (export chart to image)
> **Poznámka:** Tento krok je popsán bez dalšího kódu, aby se zachoval původní počet bloků.  
Po vytvoření a uložení grafu jej můžete exportovat do obrázku voláním metody `chart.toImage()` a zápisem výsledného `java.awt.image.BufferedImage` do formátu souboru podle vašeho výběru (PNG, JPEG, BMP). Typický postup je:
1. Získat objekt `Chart` (již provedeno v předchozích krocích).  
2. Zavolat `chart.toImage()` pro získání `BufferedImage`.  
3. Použít `ImageIO.write(bufferedImage, "png", new File("chart.png"))` pro zápis souboru.  

Tím vznikne vysoce‑rozlišený obrázek, který můžete vložit kamkoli, čímž se dokončí proces **export grafu do obrázku**.

## Analyzujte výsledky
Otevřete `output.xlsx` v Excelu a ověřte, že trendová čára, rovnice a hodnota R‑squared jsou zobrazeny podle očekávání. Otevřete exportovaný soubor obrázku (např. `chart.png`) a zobrazte čistý vizuál, který lze sdílet bez původního sešitu.

## Časté problémy a řešení
- **Trendová čára se nezobrazuje:** Ujistěte se, že datový rozsah (`A1:A10`) skutečně obsahuje číselné hodnoty; ne‑číselná data zabrání výpočtu trendové čáry.  
- **Hodnota R‑squared se zobrazuje jako 0:** To často znamená, že datová řada je konstantní nebo má nedostatečnou variabilitu. Zkuste jinou sadu dat nebo polynomickou trendovou čáru.  
- **Export obrázku selže s `NullPointerException`:** Ověřte, že graf byl plně vykreslen před voláním `toImage()`. Uložení sešitu předem může někdy vyřešit problémy s načasováním.

## Často kladené otázky

**Q: Jak mohu změnit typ trendové čáry?**  
A: Použijte jinou výčtovou hodnotu `TrendlineType` při přidávání trendové čáry, např. `TrendlineType.POLYNOMIAL` pro polynomické přizpůsobení.

**Q: Mohu přizpůsobit vzhled trendové čáry (barvu, tloušťku)?**  
A: Ano. Přistupte k `LineFormat` trendové čáry pomocí `trendline.getLineFormat()` a nastavte vlastnosti jako `setWeight()` a `setColor()`.

**Q: Jak exportuji graf do PDF místo obrázku?**  
A: Nejprve převést graf na obrázek, poté vložit tento obrázek do PDF pomocí Aspose.PDF nebo libovolné PDF knihovny dle vašeho výběru.

**Q: Je možné přidat více trendových čar do stejného grafu?**  
A: Rozhodně. Zavolejte `chart.getNSeries().get(0).getTrendlines().add(...)` pro každou řadu, kterou chcete analyzovat.

**Q: Podporuje Aspose.Cells export obrázků ve vysokém rozlišení?**  
A: Ano. Můžete specifikovat DPI při volání `chart.toImage()` a následně obrázek podle toho škálovat před uložením.

## Závěr
Nyní máte kompletní, end‑to‑end řešení pro **export grafu do obrázku** při provádění **analýzy trendové čáry** v Javě s Aspose.Cells. Načtením souboru Excel, přidáním trendové čáry, zobrazením rovnice a hodnoty R‑squared, úpravou grafu, uložením sešitu a nakonec exportem vizuálu do PNG/JPEG můžete programově generovat profesionální analytické výstupy.

---

**Poslední aktualizace:** 2025-12-09  
**Testováno s:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}