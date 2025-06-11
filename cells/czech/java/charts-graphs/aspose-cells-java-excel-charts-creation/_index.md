---
"date": "2025-04-07"
"description": "Naučte se, jak vytvářet a upravovat grafy v Excelu pomocí Aspose.Cells pro Javu. Automatizujte vytváření grafů, vylepšete vizualizaci dat a ušetřete čas s tímto podrobným průvodcem."
"title": "Vytváření a stylování grafů v Excelu pomocí Aspose.Cells v Javě&#58; Komplexní průvodce"
"url": "/cs/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Vytváření a stylování grafů v Excelu pomocí Aspose.Cells v Javě

## Zavedení

dnešním světě založeném na datech je efektivní vizualizace informací klíčová pro analýzu a rozhodování. Často je potřeba programově vytvářet dynamické grafy v sešitech aplikace Excel – zejména při práci s velkými datovými sadami nebo automatizovanými systémy pro tvorbu sestav. Tento tutoriál ukazuje, jak používat Aspose.Cells pro Javu k bezproblémovému vytváření a úpravě grafů v Excelu. Integrací Aspose.Cells do vašich aplikací v Javě můžete automatizovat vytváření grafů, vylepšit prezentaci dat a ušetřit čas.

**Co se naučíte:**
- Inicializace sešitu a jeho naplnění daty pomocí Aspose.Cells.
- Vytváření a konfigurace spojnicových grafů s datovými značkami.
- Úprava vzhledu a barev série pro lepší vizualizaci.
- Uložení sešitu s nově vytvořeným grafem ve formátu Excel.

Začněme diskusí o předpokladech potřebných k zahájení.

## Předpoklady

Před vytvářením a stylováním grafů pomocí Aspose.Cells pro Javu se ujistěte, že máte následující nastavení:

### Požadované knihovny
Zahrňte Aspose.Cells jako závislost do svého projektu. Zde jsou pokyny pro uživatele Mavenu i Gradle:

**Znalec:**
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
- Na vašem systému nainstalovaná sada pro vývoj Java (JDK).
- Integrované vývojové prostředí (IDE), jako je IntelliJ IDEA nebo Eclipse, pro kódování a testování.

### Předpoklady znalostí
Vyžaduje se základní znalost programování v Javě a znalost sešitů aplikace Excel a konceptů tvorby grafů. 

### Získání licence
Aspose.Cells je komerční produkt, který pro plnou funkčnost vyžaduje licenci. Můžete získat bezplatnou zkušební verzi pro otestování jeho funkcí, požádat o dočasnou licenci pro delší testování nebo si produkt zakoupit pro dlouhodobé používání.

- **Bezplatná zkušební verze:** [Stáhnout bezplatnou zkušební verzi](https://releases.aspose.com/cells/java/)
- **Dočasná licence:** [Žádost o dočasnou licenci](https://purchase.aspose.com/temporary-license/)
- **Nákup:** [Koupit Aspose.Cells](https://purchase.aspose.com/buy)

## Nastavení Aspose.Cells pro Javu

Jakmile nainstalujete potřebné závislosti, nastavte vývojové prostředí pro použití Aspose.Cells. Začněte importem knihovny a inicializací objektu Workbook ve vaší aplikaci Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Inicializace nové instance sešitu
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Průvodce implementací

V této části rozdělíme implementaci na jednotlivé funkce: Inicializace sešitu a naplnění dat, Vytváření a konfigurace grafu, Přizpůsobení řad a Ukládání sešitu.

### Funkce 1: Inicializace sešitu a naplnění dat

**Přehled:** Tato funkce se zaměřuje na vytvoření nového sešitu, přístup k jeho prvnímu listu a jeho naplnění daty pro vytvoření grafu.

#### Krok 1: Inicializace sešitu
Začněte vytvořením instance `Workbook` objekt:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Vytvoření instance sešitu
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu listu
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Krok 2: Nastavení názvů sloupců a naplnění dat
Definujte záhlaví sloupců a naplňte řádky vzorovými daty:

```java
        // Nastavit název sloupců 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Vytvořte náhodná data pro sérii 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Vytvořte náhodná data pro sérii 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funkce 2: Vytvoření a konfigurace grafu

**Přehled:** Tato funkce ukazuje, jak přidat graf do listu sešitu, nastavit jeho styl a konfigurovat základní vlastnosti.

#### Krok 3: Přidání grafu do pracovního listu
Přidejte spojnicový graf s datovými značkami:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Vytvoření instance sešitu
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu listu
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Přidání grafu do listu
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Přístup k grafu a jeho konfigurace
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Nastavení předdefinovaného stylu
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funkce 3: Konfigurace a přizpůsobení řady

**Přehled:** Vylepšete vizuální atraktivitu svých grafů přizpůsobením nastavení řad, jako jsou různé barvy a styly značek.

#### Krok 4: Úprava nastavení série
Konfigurace dat řady, použití vlastního formátování a úprava značek:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Vytvoření instance sešitu
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu listu
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Přidání série do grafu
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Povolit různé barvy pro body série
        chart.getNSeries().setColorVaried(true);

        // Přizpůsobení stylů a barev značek první série
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Nastavení hodnot X a Y pro první sérii
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Přizpůsobení stylů a barev značek druhé série
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Nastavte hodnoty X a Y pro druhou sérii
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funkce 4: Ukládání sešitu

**Přehled:** Nakonec sešit uložte, aby se změny zachovaly, a ujistěte se, že je graf součástí souboru aplikace Excel.

#### Krok 5: Uložení sešitu
Uložte si sešit s nově vytvořenými grafy:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Vytvoření instance sešitu
        Workbook workbook = new Workbook();
        
        // Otevřete první pracovní list a přidejte data, konfiguraci grafu podle předchozích kroků...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementace přidávání dat a konfigurace grafu by byla zde)

        // Uložení sešitu do souboru aplikace Excel
        workbook.save("StyledChart.xlsx");
    }
}
```

**Doporučení klíčových slov:**
- „Aspose.Cells pro Javu“
- "Vytváření grafů v Excelu pomocí Javy"
- "Programování v Javě pro automatizaci Excelu"

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}