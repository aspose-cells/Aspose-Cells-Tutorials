---
category: general
date: 2026-08-20
description: Naučte se, jak exportovat graf do formátu docx a převést sešit Excel
  do formátu docx pomocí Aspose.Cells v Javě. Podrobný návod krok za krokem s kompletním
  kódem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: cs
lastmod: 2026-08-20
og_description: Exportujte graf do formátu docx a převádějte sešit Excel do formátu
  docx pomocí Aspose.Cells pro Javu. Sledujte tento kompletní, spustitelný tutoriál.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Export grafu do docx pomocí Aspose.Cells – Java průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Jak exportovat graf do formátu docx z Excelu pomocí Aspose.Cells pro Java
url: /cs/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export grafu do docx z Excel sešitu pomocí Javy

Pokud potřebujete **export chart to docx** přímo ze souboru Excel, tento tutoriál vám ukáže připravené řešení. Na konci průvodce také zjistíte, jak **convert Excel workbook to docx** při zachování editovatelného grafu, takže výsledný dokument Word lze upravovat bez ztráty věrnosti.

Export grafů je běžný, když vytváříte zprávy, které kombinují výpočty v tabulkách s bohatým rozvržením Wordu. Aspose.Cells for Java usnadňuje konverzi a API vám umožní zachovat graf editovatelný – není potřeba statický obrázek.

## Co tento tutoriál pokrývá

* Načtení existujícího sešitu, který obsahuje graf.  
* Konfigurace `ImageOrPrintOptions` pro cílový formát DOCX.  
* Povolení příznaku `ExportEditableCharts` (k dispozici od verze 25.10).  
* Uložení sešitu jako soubor DOCX, který zachovává editovatelný graf.  

Kromě JAR souboru Aspose.Cells nejsou potřeba žádné externí nástroje. Kód funguje s Java 8+ a libovolnou aktuální verzí Aspose.Cells.

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 nebo novější) | Funkce `setExportEditableCharts` byla představena v tomto vydání. |
| **Java Development Kit (JDK) 8 nebo novější** | Poskytuje runtime pro kompilaci a spuštění příkladu. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | Graf je objekt, který bude exportován do DOCX. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Zjednodušuje správu závislostí a spouštění. |

Nejnovější JAR soubor Aspose.Cells můžete stáhnout z [Aspose website](https://products.aspose.com/cells/java/).

## Krok 1: Nastavte projekt a přidejte závislost Aspose.Cells

Pokud používáte Maven, přidejte následující závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Pro Gradle přidejte:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Tip:** Použijte přesnou verzi, která zavedla `ExportEditableCharts` (25.10) nebo jakoukoli novější verzi. Starší verze příznak ignorují a místo toho vytvoří statický obrázek.

## Krok 2: Načtěte sešit, který obsahuje graf

`Workbook` třída představuje celý soubor Excel. Načtení je jednorázová operace:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Proč je to důležité:** Sešit musí být plně načten, než můžete použít jakékoli možnosti exportu. Pokud je cesta k souboru nesprávná, Aspose.Cells vyhodí `FileNotFoundException`.

## Krok 3: Nakonfigurujte možnosti obrázku/tisku pro výstup DOCX

`ImageOrPrintOptions` řídí, jak je sešit vykreslen. Nastavením formátu uložení na `DOCX` říkáte Aspose.Cells, aby vytvořil dokument Word místo obrázku.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Zde můžete také upravit velikost stránky, DPI nebo kvalitu obrázku, ale jsou volitelné pro export grafu.

## Krok 4: Povolit export editovatelných grafů

Od verze 25.10 může Aspose.Cells vkládat grafy jako nativní objekty grafu ve Wordu. To je činí plně editovatelnými v Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Okrajový případ:** Pokud nastavíte tento příznak na `false` (nebo jej vynecháte), graf bude vykreslen jako statický obrázek. Použijte `true` pouze tehdy, když cílové publikum potřebuje po konverzi graf upravovat.

## Krok 5: Uložte sešit jako soubor DOCX

Nakonec zavolejte `Workbook.save` s nakonfigurovanými možnostmi:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Po dokončení programu otevřete `ChartEditable.docx` v Microsoft Word. Měli byste vidět původní graf a po kliknutí pravým tlačítkem se zobrazí možnost **Edit Data**, což potvrzuje, že graf je skutečně editovatelný.

## Kompletní, spustitelný příklad

Níže je kompletní zdrojový soubor. Zkopírujte jej do svého IDE, nahraďte `YOUR_DIRECTORY` absolutní nebo relativní cestou a spusťte.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Očekávaný výstup**

* Soubor s názvem `ChartEditable.docx` ve zadaném adresáři.  
* Po otevření souboru ve Wordu se zobrazí graf přesně tak, jak byl v Excelu, a můžete dvojklikem na graf upravit jeho datové řady.

## Časté úskalí a jak se jim vyhnout

| Projev | Příčina | Řešení |
|---------|-------|-----|
| Word zobrazuje **statický obrázek** místo editovatelného grafu | `setExportEditableCharts` nebyl zavolán nebo je použita verze < 25.10 | Ujistěte se, že je příznak nastaven na `true` a používáte Aspose.Cells 25.10 nebo novější. |
| Vygenerovaný DOCX je **prázdný** | Nesprávná cesta k souboru zdrojového sešitu nebo nedostatečná oprávnění | Zkontrolujte cestu k sešitu a že aplikace má práva pro čtení/zápis. |
| Rozložení grafu vypadá **zkresleně** | Nastavení stránky v Excelu (např. skryté řádky/sloupce) se liší od výchozích nastavení Wordu | Upravte `ImageOrPrintOptions` (např. `setOnePagePerSheet(true)`) pro kontrolu měřítka. |
| **Výkon** se snižuje u velkých sešitů | Exportování mnoha grafů nebo velkých datových sad | Exportujte pouze potřebné listy nebo použijte `setSheetIndex` k omezení zpracování. |

## Rozšíření řešení

* **Více grafů:** Procházejte všechny listy a volajte `worksheet.getCharts()` pro export každého grafu zvlášť.  
* **Vlastní stylování DOCX:** Po uložení použijte Aspose.Words k aplikaci záhlaví, zápatí nebo stylů na vygenerovaný dokument.  
* **Dávková konverze:** Zabalte kód do smyčky, která zpracuje adresář souborů `.xlsx` a pro každý vytvoří DOCX.

## Závěr

Nyní máte spolehlivou metodu pro **export chart to docx** a **convert Excel workbook to docx** při zachování plné editovatelnosti grafu. Klíčové kroky jsou načtení sešitu, konfigurace `ImageOrPrintOptions` pro DOCX, povolení `ExportEditableCharts` a uložení výsledku.

Experimentujte s dalšími možnostmi – například nastavením okrajů stránky nebo vložením vzorců sešitu – aby výstup odpovídal vašemu workflow reportování. Když potřebujete programově generovat Wordové zprávy z dat v Excelu, tento přístup poskytuje čisté, udržitelné řešení.

--- 

*Připraveni to vyzkoušet? Klonujte příklad, aktualizujte cesty k souborům a spusťte program. Pokud narazíte na problémy, konzultujte dokumentaci Aspose.Cells for Java nebo prozkoumejte související témata níže.*  

### Související témata, která můžete dále zkoumat

* **convert excel workbook to pdf** – generujte PDF zprávy ze stejného sešitu.  
* **Aspose.Cells chart formatting** – přizpůsobte barvy, značky a osy před exportem.  
* **Embedding images in DOCX with Aspose.Words** – kombinujte grafy s dalším obsahem Wordu.  

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit graf v Excelu s trendovou čárou a exportovat jej jako obrázek pomocí Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automatizace přístupu ke grafům v Excelu pomocí Aspose.Cells Java: krok za krokem](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Přizpůsobení popisků dat v grafu Excelu pomocí Aspose.Cells for Java: krok za krokem](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}