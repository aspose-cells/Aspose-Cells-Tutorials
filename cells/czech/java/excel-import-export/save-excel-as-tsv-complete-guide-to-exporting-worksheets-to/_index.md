---
category: general
date: 2026-06-27
description: Uložte Excel jako TSV rychle pomocí Javy. Naučte se, jak exportovat list
  do textu, exportovat list jako prostý text a exportovat řetězec dat z Excelu pomocí
  Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: cs
og_description: Uložte Excel jako TSV pomocí Javy. Tento tutoriál ukazuje, jak exportovat
  list do textu, exportovat list jako prostý text a efektivně exportovat řetězec dat
  z Excelu.
og_title: Uložte Excel jako TSV – Průvodce krok za krokem exportem
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Uložte Excel jako TSV – Kompletní průvodce exportem listů do textu
url: /cs/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Excel as TSV – Complete Guide to Exporting Worksheets to Text

Už jste někdy potřebovali **save Excel as TSV**, ale nebyli jste si jisti, kterou API volání použít? Nejste sami. Mnoho vývojářů narazí na problém, když se snaží převést tabulku na soubor s oddělovačem tabulátorů pro následné zpracování. Dobrá zpráva? S několika řádky Java a Aspose.Cells můžete exportovat list do textu, exportovat list jako čistý text a dokonce exportovat Excel data string bez potíží.

V tomto tutoriálu projdeme celým pracovním postupem – od načtení sešitu po nastavení možností exportu a nakonec zápis souboru TSV na disk. Na konci budete schopni **save Excel as TSV** v jakémkoli Java projektu, ať už pracujete s jedním listem nebo dávkujete desítky souborů.

## Co tento průvodce pokrývá

* Načtení Excel sešitu z disku  
* Výběr správného listu (nebo iterace přes více)  
* Nastavení `ExportTableOptions` pro vytvoření výstupu jako prostý text  
* Zapsání dat jako soubor s hodnotami oddělenými tabulátorem (TSV)  
* Tipy pro práci s velkými oblastmi, různými oddělovači a Unicode znaky  

Není potřeba žádné externí nástroje – stačí Aspose.Cells pro Java a runtime Java 8+.

## Krok 1: Nastavte svůj projekt a načtěte sešit

Než se ponoříme do kódu, ujistěte se, že jste přidali Aspose.Cells JAR do classpath vašeho projektu. Pokud používáte Maven, závislost vypadá takto:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Nyní můžeme načíst sešit:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Proč je to důležité:** Načtení souboru je první krok v jakémkoli workflow **export Excel data string**. Pokud soubor nelze otevřít, nic dalšího nebude fungovat.

### Pro tip
Pokud pracujete se soubory chráněnými heslem, zavolejte `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

## Krok 2: Vyberte list, který chcete exportovat

Můžete získat první list, list podle názvu nebo iterovat přes všechny. Zde je nejjednodušší případ – export prvního listu:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Pokud potřebujete **export worksheet to text** pro každý list, zabalte výše uvedené do `for` smyčky:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

## Krok 3: Vytvořte a nakonfigurujte možnosti exportu

Jádro **export sheet plain text** spočívá v `ExportTableOptions`. Přepnutím několika vlastností převádíme oblast na řetězec prostého textu s oddělovačem tabulátor:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Proč použít `setExportAsString(true)`?**  
> Říká Aspose.Cells, aby výstup považoval za surový text, což je přesně to, co potřebujete, když chcete **save Excel as TSV**. Alternativou by byl export do CSV nebo HTML, což neposkytuje čisté oddělení tabulátory.

### Okrajový případ: Vlastní oddělovače
Pokud váš následný systém očekává místo tabulátoru svislou čáru (`|`), stačí změnit oddělovač:

```java
exportOptions.setDelimiter('|');
```

## Krok 4: Exportujte požadovanou oblast do textového souboru

Nyní skutečně zapíšeme soubor TSV. Metoda `exportTable` přijímá tři argumenty: rozsah buněk, výstupní cestu a `ExportTableOptions`, které jsme právě nakonfigurovali.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Pokud chcete exportovat *celý* použitý rozsah, nahraďte `"A1:D20"` za `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Pro tip
Po exportu můžete také přímo zachytit řetězec:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

To vám poskytne surový **export Excel data string** bez zásahu do souborového systému.

## Krok 5: Práce s velkými soubory a tipy na výkon

Při práci s obrovskými tabulkami (stovky tisíc řádků) zvažte tyto optimalizace:

| Problém | Řešení |
|-------|----------|
| Tlak na paměť | Použijte `WorkbookFactory.create(InputStream)` pro streamování souboru místo úplného načtení. |
| Pomalejší I/O | Zapisujte do `BufferedWriter` nebo použijte NIO `Files.newBufferedWriter`. |
| Unicode znaky | Zajistěte, aby výstupní soubor byl zapisován v UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Níže je úryvek, který kombinuje streamování a kódování UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

## Časté úskalí a jak se jim vyhnout

1. **Zapomněli jste nastavit `setExportAsString(true)`.**  
   Bez tohoto příznaku Aspose vygeneruje binární Excel soubor, což naruší váš cíl **export worksheet to text**.

2. **Použití nesprávného oddělovače.**  
   Čárka místo tabulátoru vám poskytne CSV, ne TSV. Zkontrolujte `setDelimiter('\t')`.

3. **Nesprávná syntaxe rozsahu.**  
   `"A1:D20"` je v pořádku, ale `"A1:D20:"` (přebytečná dvojtečka) vyvolá `IllegalArgumentException`.

4. **Oprávnění k souborům.**  
   Ujistěte se, že cílový adresář je zapisovatelný. V Linuxu často pomůže `chmod 755`.

## Shrnutí – kompletní funkční příklad

Zde je kompletní, připravený ke spuštění program, který demonstruje **save Excel as TSV** od začátku do konce:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Spuštěním tohoto programu vznikne soubor s hodnotami oddělenými tabulátorem (`out.tsv`), který může využít jakýkoli následný systém – ať už jde o načítač databáze, Unixový skript `awk` nebo jednoduchý prohlížeč tabulek.

## Závěr

Probrali jsme vše, co potřebujete k **save Excel as TSV** pomocí Java a Aspose.Cells. Od načtení sešitu, výběru správného listu, nastavení `ExportTableOptions` až po zápis souboru – nyní máte pevný, připravený pro produkci vzor pro scénáře **export worksheet to text**, **export sheet plain text** a **export Excel data string**.

Co dál? Zkuste exportovat více oblastí, měnit oddělovače za běhu nebo streamovat výstup přímo do HTTP odpovědi pro webové stahování. Stejné principy platí a zjistíte, že práce s Excel daty v prostém textu je hračka, jakmile máte základy nastavené.

Máte otázky nebo narazíte na podivný okrajový případ? Zanechte komentář níže a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}