---
category: general
date: 2026-08-14
description: Jak ustawić separator i zapisać jako CSV przy użyciu Aspose.Cells, ograniczyć
  liczbę cyfr, eksportować ciągi CSV oraz przeliczyć formuły w Javie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: pl
lastmod: 2026-08-14
og_description: Jak ustawić separator i zapisać jako CSV przy użyciu Aspose.Cells,
  ograniczyć liczbę cyfr, wyeksportować ciągi CSV oraz przeliczyć formuły w Javie.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Jak ustawić separator i zapisać jako CSV – przewodnik Aspose.Cells
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
title: Jak ustawić separator i zapisać jako CSV przy użyciu Aspose.Cells
url: /pl/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić separator i zapisać jako CSV przy użyciu Aspose.Cells

Jeśli potrzebujesz **how to set delimiter** podczas eksportowania danych z skoroszytu Excel, ten przewodnik pokazuje kompletną, end‑to‑end rozwiązanie przy użyciu Aspose.Cells for Java. Nauczysz się, jak skonfigurować separator CSV, ograniczyć liczbę istotnych cyfr, wyeksportować ciąg CSV oraz odświeżyć formuły dynamic‑array po załadowaniu skoroszytu.

Tutorial obejmuje wszystko, co potrzebne, aby uruchomić kod na własnym komputerze, w tym obsługę specjalnych kalendarzy, takich jak panowanie japońskich cesarzy. Po zakończeniu będziesz w stanie generować dokładne pliki CSV, kontrolować precyzję liczb i zapewnić aktualność formuł.

## Prerequisites

- Java 17 lub nowszy (kod kompiluje się również z JDK 11+)
- Aspose.Cells for Java 23.9 lub nowszy – pobierz ze [Aspose website](https://products.aspose.com/cells/java/)
- Podstawowa znajomość Maven lub Gradle do zarządzania zależnościami
- IDE (IntelliJ IDEA, Eclipse, VS Code) lub prosty edytor tekstu i wiersz poleceń

> **Pro tip:** Użyj dedykowanego folderu `libs` lub Maven Central, aby trzymać plik JAR Aspose.Cells na classpathie. Przykłady poniżej zakładają projekt Maven.

## Step 1: Set up the Maven project

Utwórz plik `pom.xml` z zależnością Aspose.Cells:

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

Uruchom `mvn clean compile`, aby pobrać bibliotekę i zweryfikować, że kompilacja zakończyła się sukcesem.

## Step 2: How to set delimiter and save as CSV

Głównym celem jest zmiana domyślnego separatora przecinka na własny znak (np. średnik) podczas zapisywania skoroszytu Excel jako CSV. Aspose.Cells udostępnia do tego klasę `CsvSaveOptions`.

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

### Why this works

- `CsvSaveOptions.setDelimiter(char)` określa, który znak Aspose.Cells ma używać do oddzielania pól. Domyślnie jest to przecinek, ale działa każdy znak (tabulacja `'\t'`, pionowa kreska `'|'` itp.).
- `setSignificantDigits(int)` ogranicza precyzję liczb, spełniając wymaganie **how to limit digits** bez ręcznego formatowania każdej komórki.

#### Expected output

Plik `output.csv` będzie zawierał wiersze takie jak:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Zauważ, że liczby są zaokrąglane do pięciu istotnych cyfr (np. `123.45678` → `123.46`).

## Step 3: How to limit digits when saving CSV

Jeśli potrzebujesz ściślejszej kontroli nad formatowaniem liczb, możesz również użyć instancji `CsvSaveOptions`, aby określić własny ciąg formatu liczbowego.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` przyjmuje wzorce w stylu .NET, które Aspose.Cells respektuje.
- Połączenie `setNumberFormat` i `setSignificantDigits` zapewnia przewidywalne zaokrąglanie w różnych ustawieniach regionalnych.

## Step 4: How to export CSV as a string with a custom delimiter

Czasami nie chcesz fizycznego pliku; potrzebujesz danych CSV w pamięci (np. aby wysłać jako odpowiedź HTTP). Klasa `ExportTableOptions` umożliwia wyeksportowanie zakresu jako ciąg znaków.

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

### When to use this

- Zwracanie CSV z endpointu REST (`@RestController` w Spring)
- Osadzanie danych CSV w załączniku e‑mail bez zapisywania na dysku
- Szybkie sprawdzanie poprawności podczas testów jednostkowych

## Step 5: How to recalculate formulas after loading a workbook

Jeśli Twój skoroszyt zawiera formuły — szczególnie **dynamic‑array formulas** wprowadzone w nowszych wersjach Excel — musisz je przeliczyć po załadowaniu pliku. Aspose.Cells automatycznie odświeża wyniki dynamic‑array, ale nadal trzeba wywołać `calculateFormula()` dla zwykłych formuł.

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

### Why recalculate?

- Formuły mogą odwoływać się do danych zewnętrznych lub funkcji zmiennych (`NOW()`, `RAND()`), które wymagają aktualnych wartości.
- Formuły dynamic‑array (np. `=SORT(A1:A10)`) są oceniane automatycznie, ale wywołanie `calculateFormula()` zapewnia spójność we wszystkich arkuszach.

## Step 6: Full end‑to‑end example

Poniżej znajduje się pojedyncza klasa, która demonstruje **how to set delimiter**, **save as CSV**, **limit digits**, **export a CSV string**, **load a workbook with a special calendar** oraz **recalculate formulas**. Kod jest gotowy do skopiowania i wklejenia do Twojego projektu.

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

### Verifying the result

1. Otwórz `output.csv` w edytorze tekstu – powinieneś zobaczyć średnik (`;`) oddzielający każdą kolumnę.  
2. Potwierdź, że kolumny liczbowe wyświetlają maksymalnie pięć istotnych cyfr.  
3. Wyjście konsoli wydrukuje ciąg CSV wygenerowany w kroku 4.  
4. Otwórz `japan_updated.xlsx` w Excel – wszystkie formuły, które wcześniej wyświetlały `#REF!` lub przestarzałe wartości, teraz pokażą prawidłowe wyniki.

## Common pitfalls and how to avoid them

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| CSV shows extra quotes | Cells contain commas while delimiter is also a comma | Use a different delimiter (`;` or `\t`) via `setDelimiter` |
| Numbers are rounded incorrectly | `setSignificantDigits` applied after custom number format | Apply `setNumberFormat` **before** `setSignificantDigits` |

## What Should You Learn Next?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Load a CSV File Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [How to Load CSV Files Using Custom Parsers in Java with Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}