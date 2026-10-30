---
category: general
date: 2026-07-03
description: Exportujte obrázek kontingenční tabulky Excelu pomocí Javy. Naučte se
  krok za krokem, jak nastavit formát obrázku PNG pomocí Aspose.Cells.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: cs
og_description: Export obrázku kontingenční tabulky Excel v Javě vysvětlen. Postupujte
  podle tohoto tutoriálu a rychle a spolehlivě nastavte formát obrázku PNG.
og_title: obrázek kontingenční tabulky v Excelu – Java průvodce exportem do PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'Obrázek kontingenční tabulky v Excelu: Export do PNG pomocí Javy'
url: /cs/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – Exportovat kontingenční tabulku jako PNG v Javě

Už jste někdy potřebovali převést **excel pivot table image** na sdíletelný PNG, ale nevedeli jste, kde začít? Nejste v tom sami. V mnoha reportingových řetězcích je kontingenční tabulka hvězdou, ale zbytek týmu chce jen statický obrázek. Dobrá zpráva? Několik řádků Java a Aspose.Cells vám umožní **set image format png** a získat přesně to, co potřebujete.

V tomto průvodci projdeme kompletní proces: načtení sešitu, získání první kontingenční tabulky, nastavení možností exportu a nakonec zápis ostrého PNG souboru na disk. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného Java projektu.

## Co se naučíte

- Jak načíst Excel sešit ze souborového systému.
- Jak najít konkrétní kontingenční tabulku na listu.
- Přesné kroky k **set image format png** pro exportovaný obrázek.
- Časté úskalí (více kontingenčních tabulek, velké datové sady) a jak se jim vyhnout.
- Připravenou Java třídu, kterou můžete zkopírovat‑vložit.

### Požadavky

- Java 8 nebo novější nainstalovaná.
- Aspose.Cells for Java knihovna (nejnovější verze k 03.07.2026).
- Excel soubor (`input.xlsx`) obsahující alespoň jednu kontingenční tabulku.
- Základní znalost Maven nebo Gradle pro správu závislostí.

---

## Krok 1: Přidejte Aspose.Cells do svého projektu

Nejprve se ujistěte, že je JAR Aspose.Cells na vašem classpathu. Pokud používáte Maven, vložte následující do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Pro Gradle je to podobně jednoduché:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Tip:** Aspose nabízí bezplatný 30‑denní evaluační klíč. Zaregistrujte se na jejich webu a poté přidejte `License.setLicense("Aspose.Cells.lic");` na začátek programu, abyste odemkli všechny funkce.

## Krok 2: Načtěte sešit a přistupte ke kontingenční tabulce

Nyní otevřeme Excel soubor a získáme první kontingenční tabulku. Níže uvedený kód dělá právě to a je záměrně obranný – pokud sešit neobsahuje listy nebo list neobsahuje kontingenční tabulku, vyhodí jasnou výjimku.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Proč jsou tyto kroky důležité

- **Načtení sešitu** nám poskytuje přístup k podkladovým datovým strukturám; Aspose.Cells abstrahuje nízko‑úrovňové OpenXML parsování.
- **Přístup k listu** je nutný, protože kontingenční tabulky jsou svázány s konkrétním listem. Pokud máte více listů, můžete projít `wb.getWorksheets()` a vybrat ten, který obsahuje požadovanou kontingu.
- **Získání kontingenční tabulky** je jádrem operace. `ws.getPivotTables().get(0)` načte první, ale můžete také hledat podle jména pomocí `ws.getPivotTables().get("MyPivot")`.
- **Setting image format png** (sekundární klíčové slovo) říká Aspose.Cells, aby výstup vykreslil jako bezztrátový PNG. Tento formát zachovává ostré linie a text, ideální pro reporty.
- **Export pomocí `toImage`** zapíše soubor jedním voláním, automaticky řeší stránkování a škálování.

## Krok 3: Ověřte výstup

Po spuštění programu přejděte do `YOUR_DIRECTORY` a měli byste vidět `pivot.png`. Otevřete jej v libovolném prohlížeči obrázků – všimněte si ostrých mřížek a přesného rozložení, jaké vidíte v Excelu. Pokud je obrázek rozmazaný, zvyšte DPI v `imgOpt.setResolution()`; 300‑600 funguje dobře pro tiskové kvality.

![excel pivot table image exportováno jako PNG](excel-pivot-table-image.png "excel pivot table image exportováno jako PNG")

*Alt text obrázku:* **excel pivot table image exportováno jako PNG**

## Práce s více kontingenčními tabulkami

Co když váš list obsahuje více než jednu kontingenční tabulku? Výše uvedený úryvek získá první, ale můžete iterovat:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Tato smyčka vytvoří `pivot_0.png`, `pivot_1.png` atd., přičemž každý představuje jinou kontingenční tabulku. Nezapomeňte **set image format png** jednou před smyčkou; stejnou instanci `ImageOrPrintOptions` můžete znovu použít.

## Okrajové případy a tipy

| Situace | Na co si dát pozor | Doporučené řešení |
|-----------|-------------------|---------------|
| **Velká kontingenční tabulka (mnoho řádků/sloupců)** | PNG může být obrovské a zatížit paměť. | Použijte `imgOpt.setOnePagePerSheet(false)`, aby se výstup rozdělil na více stránek, nebo snižte DPI. |
| **Skryté řádky/sloupce** | Aspose respektuje viditelnost; skrytá data se neobjeví. | Odhalte programově pomocí `ws.showRows(start, count, true)`. |
| **Vlastní styly (písma, barvy)** | Některá firemní písma se nemusí vykreslit, pokud nejsou nainstalována na serveru. | Vložte písmo do JVM nebo použijte záložní systémová písma pomocí `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **Později je potřeba jiný výstupní formát** | Možná budete chtít JPEG nebo BMP. | Změňte `imgOpt.setImageFormat(ImageFormat.JPEG)` – stejný kód funguje, jen s jinou hodnotou enumu. |

## Kompletní funkční příklad (kopírujte‑vložte)

Níže je celá třída, připravená ke kompilaci. Vložte ji do `PivotTableToPng.java`, upravte cesty a spusťte `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Spusťte ji a získáte **excel pivot table image** uložený jako PNG soubor – právě to, co tutorial sliboval.

---

## Závěr

Právě jsme prošli vším, co potřebujete k **exportu excel pivot table image** pomocí Javy, a ukázali jsme vám, jak přesně **set image format png** s Aspose.Cells. Od načtení sešitu po řešení okrajových případů je řešení kompaktní, spolehlivé a připravené do produkce.

Co dál? Zkuste exportovat více kontingenčních tabulek najednou, poexperimentujte s různými DPI nastaveními pro tiskové materiály, nebo přepněte formát na JPEG pro web‑optimalizované obrázky. Můžete také prozkoumat vložení PNG do PDF reportu – Aspose.PDF to udělá během chvilky.

Máte v pracovním postupu odchylku nebo blokující problém? Zanechte komentář a společně to vyřešíme. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další API funkce a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}