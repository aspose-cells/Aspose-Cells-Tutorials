---
category: general
date: 2026-08-14
description: Hur man anger avgränsare och sparar som CSV med Aspose.Cells, begränsar
  siffror, exporterar CSV‑strängar och beräknar om formler i Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: sv
lastmod: 2026-08-14
og_description: Hur man ställer in avgränsare och sparar som CSV med Aspose.Cells,
  begränsar siffror, exporterar CSV‑strängar och beräknar om formler i Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Hur man ställer in avgränsare och sparar som CSV – Aspose.Cells‑guide
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
title: Hur man anger avgränsare och sparar som CSV med Aspose.Cells
url: /sv/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så ställer du in avgränsare och sparar som CSV med Aspose.Cells

Om du behöver **hur man ställer in avgränsare** när du exporterar data från en Excel‑arbetsbok, visar den här guiden en komplett, end‑to‑end‑lösning med Aspose.Cells för Java. Du kommer att lära dig hur du konfigurerar CSV‑avgränsaren, begränsar antalet signifikanta siffror, exporterar en CSV‑sträng och uppdaterar dynamiska‑array‑formler efter att ha laddat en arbetsbok.

Guiden täcker allt du behöver för att köra koden på din maskin, inklusive hantering av speciella kalendrar som den japanska kejsarens regeringstid. När du är klar kan du generera korrekta CSV‑filer, kontrollera numerisk precision och säkerställa att formler är uppdaterade.

## Förutsättningar

- Java 17 eller senare (koden kompileras även med JDK 11+)
- Aspose.Cells för Java 23.9 eller nyare – ladda ner från [Aspose website](https://products.aspose.com/cells/java/)
- Grundläggande kunskap om Maven eller Gradle för beroendehantering
- En IDE (IntelliJ IDEA, Eclipse, VS Code) eller en enkel textredigerare och kommandorad

> **Proffstips:** Använd en dedikerad `libs`‑mapp eller Maven Central för att hålla Aspose.Cells‑JAR‑filen på din classpath. Exemplen nedan förutsätter ett Maven‑projekt.

## Steg 1: Ställ in Maven‑projektet

Skapa en `pom.xml` med Aspose.Cells‑beroendet:

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

Kör `mvn clean compile` för att ladda ner biblioteket och verifiera att bygget lyckas.

## Steg 2: Hur man ställer in avgränsare och sparar som CSV

Det primära målet är att ändra standardkomma‑avgränsaren till ett eget tecken (t.ex. semikolon) när du sparar en Excel‑arbetsbok som CSV. Aspose.Cells tillhandahåller `CsvSaveOptions` för detta ändamål.

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

### Varför detta fungerar

- `CsvSaveOptions.setDelimiter(char)` talar om för Aspose.Cells vilket tecken som separerar fält. Som standard är det ett kommatecken, men vilket tecken som helst (tab `'\t'`, pipe `'|'` osv.) fungerar.
- `setSignificantDigits(int)` begränsar numerisk precision, vilket uppfyller kravet **hur man begränsar siffror** utan att manuellt formatera varje cell.

#### Förväntat resultat

Filen `output.csv` kommer att innehålla rader som:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Observera att tal avrundas till fem signifikanta siffror (t.ex. `123.45678` → `123.46`).

## Steg 3: Hur man begränsar siffror vid sparande av CSV

Om du behöver striktare kontroll över numerisk formatering kan du också använda en `CsvSaveOptions`‑instans för att ange en anpassad talformatsträng.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` följer .NET‑stilens mönster, vilket Aspose.Cells respekterar.
- Att kombinera både `setNumberFormat` och `setSignificantDigits` ger dig förutsägbar avrundning över olika språkregioner.

## Steg 4: Hur man exporterar CSV som en sträng med en anpassad avgränsare

Ibland vill du inte ha en fysisk fil; du behöver CSV‑data i minnet (t.ex. för att skicka som ett HTTP‑svar). Klassen `ExportTableOptions` låter dig exportera ett område som en sträng.

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

### När man använder detta

- Returnera CSV från en REST‑endpoint (`@RestController` i Spring)
- Bädda in CSV‑data i en e‑postbilaga utan att skriva till disk
- Utföra snabba kontrolltester under enhetstester

## Steg 5: Hur man räknar om formler efter att ha laddat en arbetsbok

Om din arbetsbok innehåller formler—särskilt **dynamic‑array formulas** som introducerats i de senaste Excel‑versionerna—måste du räkna om dem efter att filen har laddats. Aspose.Cells uppdaterar automatiskt dynamiska‑array‑resultat, men du måste fortfarande anropa `calculateFormula()` för vanliga formler.

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

### Varför räkna om?

- Formler kan referera till extern data eller flyktiga funktioner (`NOW()`, `RAND()`) som behöver nya värden.
- Dynamiska‑array‑formler (t.ex. `=SORT(A1:A10)`) utvärderas automatiskt, men att anropa `calculateFormula()` garanterar konsistens i alla blad.

## Steg 6: Fullständig end‑to‑end‑exempel

Nedan finns en enda klass som demonstrerar **hur man ställer in avgränsare**, **sparar som CSV**, **begränsar siffror**, **exporterar en CSV‑sträng**, **laddar en arbetsbok med en speciell kalender** och **räknar om formler**. Koden är klar att kopiera‑klistra in i ditt projekt.

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

### Verifiera resultatet

1. Öppna `output.csv` i en textredigerare – du bör se ett semikolon (`;`) som separerar varje kolumn.
2. Bekräfta att numeriska kolumner visar högst fem signifikanta siffror.
3. Konsolutdata kommer att skriva ut CSV‑strängen som genererades i steg 4.
4. Öppna `japan_updated.xlsx` i Excel – eventuella formler som tidigare visade `#REF!` eller föråldrade värden kommer nu att visa de korrekta resultaten.

## Vanliga fallgropar och hur man undviker dem

| Problem | Orsak | Lösning |
|---------|-------|---------|
| CSV visar extra citattecken | Celler innehåller kommatecken medan avgränsaren också är ett kommatecken | Använd en annan avgränsare (`;` eller `\t`) via `setDelimiter` |
| Tal avrundas felaktigt | `setSignificantDigits` tillämpas efter anpassat talformat | Tillämpa `setNumberFormat` **före** `setSignificantDigits` |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man laddar och sparar Excel som CSV med Aspose.Cells för Java: En omfattande guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Hur man laddar en CSV‑fil med Aspose.Cells för Java: En omfattande guide](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Hur man laddar CSV‑filer med anpassade parsers i Java med Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}