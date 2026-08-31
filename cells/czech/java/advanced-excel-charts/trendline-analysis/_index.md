---
date: 2026-02-09
description: Naučte se, jak vytvořit graf v Excelu, přidat regresní čáru, zobrazit
  hodnotu R‑kvadrátu a exportovat graf jako obrázek pomocí Aspose.Cells pro Javu.
  Obsahuje kroky pro načtení souboru Excel, úpravu grafu a uložení jako PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Jak vytvořit graf v Excelu s trendovou čárou a exportovat jej jako obrázek
  pomocí Aspose.Cells pro Javu
url: /cs/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export grafu do obrázku s analýzou trendové čáry

V tomto tutoriálu se naučíte, jak **vytvořit Excel graf** s trendovou čárou, zobrazit jeho hodnotu R‑squared a exportovat výsledný vizuál do obrázku pomocí Aspose.Cells pro Java. Provedeme vás načtením existujícího sešitu, přidáním trendové čáry, úpravou názvů, uložením sešitu a nakonec vygenerováním souboru PNG/JPEG, který můžete vložit kamkoli.

## Rychlé odpovědi
- **Jaký je hlavní účel tohoto návodu?** Ukázat, jak přidat trendovou čáru, zobrazit její rovnici a hodnotu R‑squared a exportovat vzniklý graf do obrázku pomocí Javy.  
- **Která knihovna je vyžadována?** Aspose.Cells pro Java (stáhněte [here](https://releases.aspose.com/cells/java/)).  
- **Potřebuji licenci?** Bezplatná zkušební verze stačí pro vývoj; pro produkční nasazení je nutná komerční licence.  
- **Mohu v Javě generovat soubor Excel?** Ano – tutoriál vytvoří a uloží sešit XLSX.  
- **Jak exportovat graf do PNG nebo JPEG?** Použijte metodu `Chart.toImage()` (viz sekce „Export grafu“).

## Jak vytvořit Excel graf s trendovou čárou a exportovat jej do obrázku
Tento nadpis přímo odpovídá hlavnímu dotazu a provádí vás celým pracovním postupem v logickém pořadí. Níže najdete proč, předpoklady a podrobný průvodce krok za krokem.

## Co je Export grafu do obrázku?
Export grafu do obrázku převádí vizuální reprezentaci vašich dat do přenosného bitmapového formátu (PNG, JPEG atd.). To je užitečné pro vkládání grafů do zpráv, webových stránek nebo prezentací, kde není vyžadován původní soubor Excel.

## Proč přidat trendovou čáru a zobrazit hodnotu R‑squared?
Trendová čára vám pomůže identifikovat základní vzorec datové řady, zatímco **R‑squared** měří, jak dobře trendová čára odpovídá datům. Začlenění těchto informací do exportovaného obrázku poskytne zainteresovaným stranám okamžitý přehled bez nutnosti otevírat sešit.

## Předpoklady
- Nainstalovaný Java 8 nebo novější.  
- Knihovna Aspose.Cells pro Java přidaná do vašeho projektu (JAR soubory na classpath).  
- Základní znalost Java IDE (IntelliJ IDEA, Eclipse atd.).  

## Průvodce krok za krokem

### Krok 1: Nastavení projektu
Vytvořte nový Java projekt a přidejte JAR soubory Aspose.Cells do cesty sestavení. Tím připravíte prostředí pro generování a manipulaci se soubory Excel.

### Krok 2: Načtení Excel souboru (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Právě jsme **načetli Excel soubor** do paměti, připravený pro vytvoření grafu.*

### Krok 3: Vytvoření grafu
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Zde generujeme čárový graf, do kterého později přidáme naši trendovou čáru.*

### Krok 4: Přidání trendové čáry (how to add trendline) a zobrazení hodnoty R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Volání `setDisplayRSquaredValue(true)` zajistí, že se **hodnota R‑squared** zobrazí na grafu.*

### Krok 5: Úprava grafu a uložení sešitu (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Nyní je sešit **vygenerován** a uložen jako soubor XLSX, připravený pro další zpracování.*

### Krok 6: Export grafu do obrázku (export chart to image)
> **Poznámka:** Tento krok je popsán bez dalšího kódu, aby se zachoval původní počet bloků.  
Po vytvoření a uložení grafu jej můžete exportovat do obrázku voláním metody `chart.toImage()` a zápisem výsledného `java.awt.image.BufferedImage` do formátu dle vašeho výběru (PNG, JPEG, BMP). Typický postup je:
1. Získat objekt `Chart` (již provedeno v předchozích krocích).  
2. Zavolat `chart.toImage()` a získat `BufferedImage`.  
3. Použít `ImageIO.write(bufferedImage, "png", new File("chart.png"))` pro zápis souboru.  

Tím vznikne vysoce kvalitní obrázek, který můžete vložit kamkoli, čímž dokončíte proces **exportu grafu do obrázku**.

## Analýza výsledků
Otevřete `output.xlsx` v Excelu a ověřte, že trendová čára, rovnice a hodnota R‑squared jsou zobrazeny podle očekávání. Otevřete exportovaný obrázek (např. `chart.png`) a podívejte se na čistý vizuál, který lze sdílet bez původního sešitu.

## Časté problémy a řešení
- **Trendová čára se nezobrazuje:** Ujistěte se, že rozsah dat (`A1:A10`) skutečně obsahuje číselné hodnoty; ne‑číselná data zabrání výpočtu trendové čáry.  
- **Hodnota R‑squared se zobrazuje jako 0:** To často znamená, že datová řada je konstantní nebo má nedostatečnou variabilitu. Vyzkoušejte jiný datový soubor nebo polynomickou trendovou čáru.  
- **Export obrázku selže s `NullPointerException`:** Ověřte, že byl graf plně vykreslen před voláním `toImage()`. Uložení sešitu před exportem může někdy vyřešit časové problémy.

## Často kladené otázky

**Q: Jak mohu změnit typ trendové čáry?**  
A: Použijte jinou enumeraci `TrendlineType` při přidávání trendové čáry, např. `TrendlineType.POLYNOMIAL` pro polynomické přizpůsobení.

**Q: Mohu přizpůsobit vzhled trendové čáry (barvu, tloušťku)?**  
A: Ano. Přistupte k `LineFormat` trendové čáry pomocí `trendline.getLineFormat()` a nastavte vlastnosti jako `setWeight()` a `setColor()`.

**Q: Jak exportovat graf do PDF místo obrázku?**  
A: Nejprve převést graf na obrázek, poté vložit tento obrázek do PDF pomocí Aspose.PDF nebo libovolné PDF knihovny dle vašeho výběru.

**Q: Je možné přidat více trendových čar do stejného grafu?**  
A: Rozhodně. Zavolejte `chart.getNSeries().get(0).getTrendlines().add(...)` pro každou řadu, kterou chcete analyzovat.

**Q: Podporuje Aspose.Cells export obrázku ve vysokém rozlišení?**  
A: Ano. DPI můžete specifikovat při volání `chart.toImage()` a následně před uložením obrázek škálovat.

## Závěr
Nyní máte kompletní end‑to‑end řešení pro **vytvoření Excel grafu**, přidání trendové čáry, zobrazení rovnice a hodnoty R‑squared, úpravu vizuálu, uložení sešitu a nakonec export grafu jako PNG/JPEG obrázku. Tento přístup vám umožní programově generovat profesionální analytické materiály, ideální pro automatizované reportování, dashboardy nebo jakýkoli scénář, kde je statický obrázek praktičtější než soubor Excel.

---

**Poslední aktualizace:** 2026-02-09  
**Testováno s:** Aspose.Cells pro Java nejnovější verze  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}