---
date: '2026-04-08'
description: Naučte se, jak pomocí Aspose.Cells pro Javu vytvořit čárový graf se značkami,
  přidat graf do listu a přizpůsobit grafy v Excelu pro automatizované reportování.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Vytvořte čárový graf se značkami pomocí Aspose.Cells pro Javu
url: /cs/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytváření a stylování grafů Excel pomocí Aspose.Cells Java

## Úvod

V dnešním datově řízeném světě je **line chart with markers** jedním z nejúčinnějších způsobů vizualizace trendů a odlehlých hodnot. Ať už vytváříte automatizované zprávy nebo dashboard, který se aktualizuje denně, schopnost programově přidat line chart with markers do listu šetří nespočet ručních kroků. Tento tutoriál vás provede používáním Aspose.Cells pro Java k vytvoření, stylování a exportu takových grafů, abyste se mohli soustředit na poznatky místo únavného manipulování s Excelem.

**Co se naučíte**
- Inicializace sešitu a naplnění daty pomocí Aspose.Cells.  
- **Jak přidat line chart with markers do listu** a nakonfigurovat jeho vzhled.  
- Přizpůsobení barev řad, značek a dalších možností stylování.  
- Uložení sešitu jako soubor Excel, který obsahuje váš stylovaný graf.

## Rychlé odpovědi
- **Jaká je hlavní třída pro zahájení?** `Workbook` inicializuje nový soubor Excel.  
- **Který typ grafu vytváří line chart with markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Jak nastavit vlastní barvy pro body řady?** Použijte `chart.getNSeries().setColorVaried(true)` a nastavte barvy oblastí značek.  
- **Potřebuji licenci pro plnou funkčnost?** Ano, placená nebo dočasná licence Aspose.Cells odstraňuje omezení zkušební verze.  
- **Mohu výsledek exportovat jako XLSX?** Rozhodně—`workbook.save("StyledChart.xlsx")` vytvoří soubor XLSX.

## Předpoklady

Před vytvořením a stylováním grafů pomocí Aspose.Cells pro Java se ujistěte, že máte následující nastavení:

### Požadované knihovny
Zahrňte Aspose.Cells jako závislost ve vašem projektu. Zde jsou instrukce pro uživatele Maven i Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Požadavky na nastavení prostředí
- Nainstalovaný Java Development Kit (JDK) ve vašem systému.  
- Integrované vývojové prostředí (IDE) jako IntelliJ IDEA nebo Eclipse pro kódování a testování.

### Předpoklady znalostí
Základní znalost programování v Javě je vyžadována, spolu se znalostí sešitů Excel a konceptů grafů.

### Získání licence
Aspose.Cells je komerční produkt, který vyžaduje licenci pro plnou funkčnost. Můžete získat bezplatnou zkušební verzi k vyzkoušení funkcí, požádat o dočasnou licenci pro rozšířené testování nebo zakoupit produkt pro dlouhodobé používání.

- **Bezplatná zkušební verze:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Dočasná licence:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Koupit:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Nastavení Aspose.Cells pro Java

Jakmile nainstalujete potřebné závislosti, nastavte vývojové prostředí pro použití Aspose.Cells. Začněte importováním knihovny a inicializací objektu `Workbook` ve vaší Java aplikaci:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Průvodce implementací

V této sekci rozdělíme implementaci na jednotlivé funkce: Inicializace sešitu a naplnění daty, Vytvoření a konfigurace grafu, Přizpůsobení řad a Uložení sešitu.

### Funkce 1: Inicializace sešitu a naplnění daty

**Přehled:** Tato funkce se zaměřuje na vytvoření nového sešitu, přístup k prvnímu listu a naplnění daty pro vytvoření grafu.

#### Krok 1: Inicializace sešitu
Začněte vytvořením instance objektu `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Krok 2: Nastavení názvů sloupců a naplnění daty
Definujte záhlaví sloupců a naplňte řádky ukázkovými daty:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funkce 2: Vytvoření a konfigurace grafu

**Přehled:** Tato funkce ukazuje, jak přidat graf do listu sešitu, nastavit jeho styl a konfigurovat základní vlastnosti.

#### Krok 3: Přidání grafu do listu
Přidejte line chart with data markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funkce 3: Konfigurace a přizpůsobení řad

**Přehled:** Zlepšete vizuální vzhled vašich grafů přizpůsobením nastavení řad, jako jsou různé barvy a styly značek.

#### Krok 4: Přizpůsobení nastavení řad
Konfigurujte data řad, aplikujte vlastní formátování a upravte značky:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funkce 4: Uložení sešitu

**Přehled:** Nakonec uložte sešit, aby se změny zachovaly a graf byl zahrnut v souboru Excel.

#### Krok 5: Uložení sešitu
Uložte svůj sešit s nově vytvořenými grafy:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Časté problémy a řešení
- **Graf je prázdný:** Ověřte, že rozsahy buněk použité v `setXValues` a `setValues` správně odkazují na naplněné buňky.  
- **Barvy nejsou aplikovány:** Ujistěte se, že `chart.getNSeries().setColorVaried(true)` je zavoláno před přizpůsobením jednotlivých řad.  
- **Chyby licence:** Zkušební licence může omezovat počet grafů; nainstalujte plnou licenci pro odstranění omezení.

## Často kladené otázky

**Q: Mohu vytvořit jiné typy grafů (např. sloupcový, koláčový) pomocí Aspose.Cells?**  
A: Ano, Aspose.Cells podporuje širokou škálu typů grafů; stačí nahradit `ChartType.LINE_WITH_DATA_MARKERS` požadovanou hodnotou enumu.

**Q: Musím zavřít sešit nebo uvolnit prostředky?**  
A: Třída `Workbook` spravuje prostředky automaticky, ale můžete zavolat `workbook.dispose()` v dlouhodobých aplikacích pro uvolnění paměti.

**Q: Je možné přidat více grafů do stejného listu?**  
A: Rozhodně—voláním `worksheet.getCharts().add(...)` pro každý graf, který chcete vložit.

**Q: Jak exportovat soubor do staršího formátu Excel (XLS)?**  
A: Použijte `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Q: Zachová graf své stylování při otevření v Microsoft Excel?**  
A: Ano, Aspose.Cells zapisuje nativní objekty grafu Excel, takže všechny styly, barvy a značky se zobrazí přesně tak, jak jsou definovány.

---

**Poslední aktualizace:** 2026-04-08  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}