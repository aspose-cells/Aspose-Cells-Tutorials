---
category: general
date: 2026-08-14
description: Jak nastavit oddělovač a uložit jako CSV pomocí Aspose.Cells, omezit
  počet číslic, exportovat CSV řetězce a přepočítat vzorce v Javě.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: cs
lastmod: 2026-08-14
og_description: Jak nastavit oddělovač a uložit jako CSV pomocí Aspose.Cells, omezit
  počet číslic, exportovat CSV řetězce a přepočítat vzorce v Javě.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Jak nastavit oddělovač a uložit jako CSV – průvodce Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Jak nastavit oddělovač a uložit jako CSV pomocí Aspose.Cells
url: /cs/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit oddělovač a uložit jako CSV pomocí Aspose.Cells

Pokud potřebujete **jak nastavit oddělovač** při exportu dat z Excel sešitu, tento průvodce vám ukáže kompletní řešení od začátku do konce pomocí Aspose.Cells pro Java. Naučíte se, jak nakonfigurovat oddělovač CSV, omezit počet významných číslic, exportovat CSV řetězec a obnovit dynamické pole vzorců po načtení sešitu.

Tutoriál pokrývá vše, co potřebujete ke spuštění kódu na vašem počítači, včetně práce se speciálními kalendáři, jako je japonský císařský režim. Na konci budete schopni generovat přesné CSV soubory, řídit číselnou přesnost a zajistit, aby byly vzorce aktuální.

## Prerequisites

- Java 17 nebo novější (kód se také kompiluje s JDK 11+)
- Aspose.Cells pro Java 23.9 nebo novější – stáhněte z [Aspose webu](https://products.aspose.com/cells/java/)
- Základní znalost Maven nebo Gradle pro správu závislostí
- IDE (IntelliJ IDEA, Eclipse, VS Code) nebo jednoduchý textový editor a příkazová řádka

> **Tip:** Použijte vyhrazený adresář `libs` nebo Maven Central k uložení Aspose.Cells JAR na classpath. Níže uvedené příklady předpokládají Maven projekt.

## Krok 1: Nastavení Maven projektu

Vytvořte `pom.xml` s Aspose.Cells závislostí:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Spusťte `mvn clean compile`, aby se stáhla knihovna a ověřilo se, že sestavení proběhne úspěšně.

## Krok 2: Jak nastavit oddělovač a uložit jako CSV

Hlavním cílem je změnit výchozí čárkový oddělovač na vlastní znak (např. středník) při ukládání Excel sešitu jako CSV. Aspose.Cells poskytuje k tomu třídu `CsvSaveOptions`.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Proč to funguje

- `CsvSaveOptions.setDelimiter(char)` určuje, který znak Aspose.Cells použije k oddělení polí. Ve výchozím nastavení je to čárka, ale funguje libovolný znak (tabulátor `'\t'`, svislá čára `'|'` atd.).
- `setSignificantDigits(int)` omezuje číselnou přesnost, čímž splňuje požadavek **jak omezit číslice** bez nutnosti ručního formátování každé buňky.

#### Očekávaný výstup

Soubor `output.csv` bude obsahovat řádky jako:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Všimněte si, že čísla jsou zaokrouhlena na pět významných číslic (např. `123.45678` → `123.46`).

## Krok 3: Jak omezit číslice při ukládání CSV

Pokud potřebujete přesnější kontrolu nad číselným formátováním, můžete také použít instanci `CsvSaveOptions` k zadání vlastního řetězce formátu čísla.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` používá vzory ve stylu .NET, které Aspose.Cells respektuje.
- Kombinace `setNumberFormat` a `setSignificantDigits` vám poskytne předvídatelné zaokrouhlování napříč různými locale.

## Krok 4: Jak exportovat CSV jako řetězec s vlastním oddělovačem

Někdy nechcete fyzický soubor; potřebujete CSV data v paměti (např. pro odeslání jako HTTP odpověď). Třída `ExportTableOptions` umožňuje exportovat oblast jako řetězec.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Kdy použít

- Vrácení CSV z REST endpointu (`@RestController` ve Springu)
- Vložení CSV dat jako přílohy e‑mailu bez zápisu na disk
- Provádění rychlých kontrol během unit testů

## Krok 5: Jak přepočítat vzorce po načtení sešitu

Pokud váš sešit obsahuje vzorce—zejména **dynamic‑array formulas** zavedené v novějších verzích Excelu—musíte je po načtení souboru přepočítat. Aspose.Cells automaticky obnovuje výsledky dynamických polí, ale pro běžné vzorce je stále nutné zavolat `calculateFormula()`.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Proč přepočítat?

- Vzorce mohou odkazovat na externí data nebo volatilní funkce (`NOW()`, `RAND()`), které potřebují čerstvé hodnoty.
- Dynamické pole vzorců (např. `=SORT(A1:A10)`) jsou vyhodnoceny automaticky, ale volání `calculateFormula()` zajišťuje konzistenci napříč všemi listy.

## Krok 6: Kompletní end‑to‑end příklad

Níže je jedna třída, která demonstruje **jak nastavit oddělovač**, **uložit jako CSV**, **omezit číslice**, **exportovat CSV řetězec**, **načíst sešit se speciálním kalendářem** a **přepočítat vzorce**. Kód je připravený ke zkopírování do vašeho projektu.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Ověření výsledku

1. Otevřete `output.csv` v textovém editoru – měli byste vidět středník (`;`) oddělující jednotlivé sloupce.
2. Ověřte, že číselné sloupce zobrazují nejvýše pět významných číslic.
3. Výstup v konzoli vytiskne CSV řetězec vygenerovaný ve kroku 4.
4. Otevřete `japan_updated.xlsx` v Excelu – všechny vzorce, které dříve zobrazovaly `#REF!` nebo zastaralé hodnoty, nyní ukážou správné výsledky.

## Časté úskalí a jak se jim vyhnout

| Problém | Příčina | Řešení |
|---------|---------|--------|
| CSV zobrazuje nadbytečné uvozovky | Buňky obsahují čárky, zatímco oddělovač je také čárka | Použijte jiný oddělovač (`;` nebo `\t`) pomocí `setDelimiter` |
| Čísla jsou zaokrouhlena nesprávně | `setSignificantDigits` aplikováno po vlastním formátu čísla | Použijte `setNumberFormat` **před** `setSignificantDigits` |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobným vysvětlením, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak načíst a uložit Excel jako CSV pomocí Aspose.Cells pro Java: Komplexní průvodce](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Jak načíst CSV soubor pomocí Aspose.Cells pro Java: Komplexní průvodce](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Jak načíst CSV soubory pomocí vlastních parserů v Javě s Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}