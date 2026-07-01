---
category: general
date: 2026-06-30
description: Exportujte graf jako obrázek a zjistěte, jak exportovat graf, uložit
  Excel jako Word, převést Excel do Wordu a převést XLSX na DOCX během několika jednoduchých
  kroků.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: cs
og_description: Exportujte graf jako obrázek a rychle převádějte Excel do Wordu. Postupujte
  podle tohoto návodu, jak uložit Excel jako Word, exportovat grafy a převést XLSX
  na DOCX.
og_title: Exportovat graf jako obrázek – krok za krokem převod z Excelu do Wordu
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Export grafu jako obrázek – Kompletní průvodce převodem Excelu do Wordu
url: /cs/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export grafu jako obrázek – Kompletní průvodce převodem Excelu do Wordu

Už jste se někdy zamýšleli, jak exportovat graf jako obrázek z sešitu Excel a vložit jej přímo do dokumentu Word? Nejste jediní – vývojáři se neustále ptají: „Jak exportovat graf z XLSX a vložit jej do DOCX bez ztráty kvality?“

Dobrou zprávou je, že s několika řádky Java kódu můžete **export chart as image**, pak **save Excel as Word** v jednom plynulém procesu. V tomto tutoriálu projdeme celý postup, od načtení sešitu až po nastavení možností ukládání, které vaše grafy převedou na ostré PNG obrázky uvnitř souboru DOCX.

Také se dotkneme souvisejících úkolů, jako **convert Excel to Word**, **save Excel as Word** a **convert XLSX to DOCX** – vše při zachování přehledného a spustitelného kódu. Žádné zbytečnosti, jen praktické řešení, které můžete dnes zkopírovat a vložit.

## Co budete potřebovat

- **Java Development Kit (JDK) 8+** – kód běží na jakémkoli moderním JDK.
- **Aspose.Cells for Java** knihovna (verze 23.10 nebo novější). Můžete ji získat z Maven Central nebo stáhnout JAR přímo.
- **Excel soubor** (`charts.xlsx`), který obsahuje alespoň jeden graf, který chcete exportovat.
- **Java IDE** (IntelliJ IDEA, Eclipse nebo VS Code) – jakýkoli bude stačit.
- Základní znalost Javy a Maven/Gradle (volitelné, ale užitečné).

A to je vše. Žádné extra pluginy, žádná COM interop, jen čistá Java.

## Krok 1: Načtení Excel sešitu a nalezení grafu

Prvním krokem je otevřít sešit, který obsahuje graf. Aspose.Cells to usnadňuje – stačí nasměrovat na cestu k souboru.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Proč je to důležité:** Načtení sešitu nám poskytuje přístup k objektu grafu, který později řekneme Aspose, aby jej vykreslil jako obrázek. Pokud sešit obsahuje více listů nebo grafů, můžete upravit indexy nebo je projít ve smyčce.

## Krok 2: Nastavení možností uložení DOCX pro export grafů jako obrázků

Aspose.Cells poskytuje třídu `DocxSaveOptions`, která vám umožní řídit chování konverze. Nastavení `setExportChartAsImage(true)` řekne knihovně, aby rasterizovala každý graf do obrázku před jeho vložením do souboru Word.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Tip:** Pokud dáváte přednost vektorové grafice (EMF/WMF), můžete tento příznak vypnout, ale rastrové obrázky se obvykle zobrazují konzistentněji napříč verzemi Wordu.

## Krok 3: Uložení sešitu jako soubor DOCX

Jakmile jsou možnosti nastaveny, jednoduše uložíme sešit. Knihovna se postará o konverzi všech listů, tabulek a – díky nastavenému příznaku – grafů jako obrázků.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Co získáte:** Soubor `charts.docx`, kde se původní Excel graf zobrazuje jako vysoce rozlišený PNG (nebo JPEG, podle nastavení) uvnitř dokumentu Word. Otevřete jej v Microsoft Word a uvidíte výsledek.

## Krok 4: Ověření výstupu (volitelné, ale doporučené)

Vždy je dobré programově ověřit, že konverze proběhla úspěšně, zejména při automatizaci dávkových procesů.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Pokud spustíte úryvek a uvidíte zprávu o úspěchu, úspěšně jste **convert XLSX to DOCX** a zachovali vizuály grafu jako obrázky.

## Kompletní funkční příklad

Níže je kompletní, připravený Java program, který spojuje všechny kroky. Stačí nahradit `YOUR_DIRECTORY` skutečnou cestou na vašem počítači.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Očekávaný výstup po spuštění programu:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Otevřete `charts.docx` v Microsoft Word a uvidíte graf vykreslený jako čistý obrázek, perfektně umístěný tam, kde byl původní Excel graf.

## Časté otázky a okrajové případy

### Co když má můj sešit více grafů?

Nemusíte nic měnit – nastavení `setExportChartAsImage(true)` se vztahuje na **všechny** grafy v sešitu. Pokud chcete konkrétní grafy jako obrázky, budete je muset exportovat ručně pomocí `chart.toImage()` a poté je sami vložit do souboru Word.

### Můžu ovládat formát obrázku (PNG vs JPEG)?

Aspose.Cells používá jako výchozí formát PNG pro export grafu jako obrázku. Pro přepnutí na JPEG můžete před uložením upravit `ImageOrPrintOptions`:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Funguje to i se staršími soubory Excel (.xls)?

Ano. Stejný kód funguje jak pro `.xls`, tak pro `.xlsx`. Aspose.Cells automaticky detekuje formát, takže můžete **save Excel as Word** bez ohledu na verzi zdroje.

### Jak se liší od „convert Excel to Word“ pomocí nativního Office interopu?

Nativní interop často vyžaduje Windows stroj s nainstalovaným Office a grafy mohou ztratit kvalitu. Použití Aspose.Cells je platformově nezávislé, funguje na Linuxu/macOS a zachovává kvalitu grafů rasterizací.

## Tipy pro produkčně připravené implementace

- **Dávkové zpracování:** Procházejte adresář souborů XLSX a aplikujte stejné `DocxSaveOptions`. Zabalte konverzi do try‑catch bloku, aby se poškozené soubory ošetřily elegantně.
- **Správa paměti:** Pro velmi velké sešity zavolejte po uložení `workbook.dispose()`, aby se uvolnily nativní zdroje.
- **Přizpůsobení:** Můžete také nastavit `saveOptions.setPreserveCellFormatting(true)`, pokud potřebujete zachovat formátování buněk při konverzi.
- **Logování:** Integrujte logovací framework (SLF4J, Log4j) pro zachycení statistik konverze – užitečné pro auditní záznamy.

## Závěr

Nyní máte robustní, end‑to‑end řešení, které **export chart as image**, **save Excel as Word** a **convert XLSX to DOCX** pomocí několika Java příkazů. Hlavní výsledek je, že `DocxSaveOptions` od Aspose.Cells usnadňuje práci s grafy – žádná ruční extrakce obrázků, žádný COM interop a plná podpora napříč platformami.

Nebojte se experimentovat: zkuste exportovat více listů, upravit rozlišení obrázků nebo kombinovat tento přístup s dalšími knihovnami Aspose (např. Aspose.Words) pro ještě bohatší dokumenty Word. Možnosti jsou neomezené, pokud víte, jak správně exportovat graf.

Máte další otázky ohledně převodu Excel souborů, vkládání obrázků nebo optimalizace výkonu? Zanechte komentář níže a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převod Excel grafu na obrázek pomocí Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [Jak vytvořit Excel graf s trendovou čarou a exportovat jej jako obrázek pomocí Aspose.Cells pro Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Převod Excel koláčového grafu na obrázek pomocí Aspose.Cells .NET: krok za krokem](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}