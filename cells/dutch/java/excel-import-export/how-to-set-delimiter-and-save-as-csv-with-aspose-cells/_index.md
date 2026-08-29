---
category: general
date: 2026-08-14
description: Hoe delimiter instellen en opslaan als CSV met Aspose.Cells, cijfers
  beperken, CSV‑strings exporteren en formules opnieuw berekenen in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: nl
lastmod: 2026-08-14
og_description: Hoe delimiter instellen en opslaan als CSV met Aspose.Cells, cijfers
  beperken, CSV-strings exporteren en formules opnieuw berekenen in Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Hoe een scheidingsteken instellen en opslaan als CSV – Aspose.Cells-gids
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
title: Hoe een scheidingsteken instellen en opslaan als CSV met Aspose.Cells
url: /nl/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een scheidingsteken instellen en opslaan als CSV met Aspose.Cells

Als je **hoe je een scheidingsteken instelt** tijdens het exporteren van gegevens uit een Excel-werkmap, laat deze gids je een complete, end‑to‑end oplossing zien met Aspose.Cells voor Java. Je leert hoe je het CSV‑scheidingsteken configureert, het aantal significante cijfers beperkt, een CSV‑string exporteert en dynamische‑array‑formules vernieuwt na het laden van een werkmap.

De tutorial behandelt alles wat je nodig hebt om de code op je machine uit te voeren, inclusief het omgaan met speciale kalenders zoals de Japanse keizerlijke regeerperiode. Aan het einde kun je nauwkeurige CSV‑bestanden genereren, numerieke precisie beheersen en ervoor zorgen dat formules up‑to‑date zijn.

## Vereisten

- Java 17 of later (de code compileert ook met JDK 11+)
- Aspose.Cells for Java 23.9 of nieuwer – download van de [Aspose website](https://products.aspose.com/cells/java/)
- Basiskennis van Maven of Gradle voor afhankelijkheidsbeheer
- Een IDE (IntelliJ IDEA, Eclipse, VS Code) of een eenvoudige teksteditor en de opdrachtregel

> **Pro tip:** Gebruik een speciale `libs` map of Maven Central om de Aspose.Cells JAR op je classpath te houden. De onderstaande voorbeelden gaan uit van een Maven‑project.

## Stap 1: Het Maven‑project opzetten

Maak een `pom.xml` met de Aspose.Cells‑dependency:

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

Voer `mvn clean compile` uit om de bibliotheek te downloaden en te verifiëren dat de build slaagt.

## Stap 2: Hoe een scheidingsteken instellen en opslaan als CSV

Het primaire doel is om het standaard komma‑scheidingsteken te wijzigen in een aangepast teken (bijv. puntkomma) bij het opslaan van een Excel‑werkmap als CSV. Aspose.Cells biedt `CsvSaveOptions` hiervoor.

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

### Waarom dit werkt

- `CsvSaveOptions.setDelimiter(char)` vertelt Aspose.Cells welk teken velden scheidt. Standaard is dit een komma, maar elk teken (tab `'\t'`, pipe `'|'`, etc.) werkt.
- `setSignificantDigits(int)` beperkt de numerieke precisie, waardoor aan de **hoe je cijfers beperkt**‑vereiste wordt voldaan zonder elke cel handmatig te formatteren.

#### Verwachte output

Het bestand `output.csv` zal rijen bevatten zoals:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Merk op dat getallen worden afgerond op vijf significante cijfers (bijv. `123.45678` → `123.46`).

## Stap 3: Hoe cijfers beperken bij het opslaan van CSV

Als je strakkere controle over numerieke opmaak nodig hebt, kun je ook een `CsvSaveOptions`‑instantie gebruiken om een aangepast getalopmaak‑string op te geven.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` volgt .NET‑stijlpatronen, die Aspose.Cells respecteert.
- Het combineren van zowel `setNumberFormat` als `setSignificantDigits` geeft je voorspelbare afronding over verschillende locales.

## Stap 4: Hoe CSV exporteren als een string met een aangepast scheidingsteken

Soms wil je geen fysiek bestand; je hebt de CSV‑gegevens in het geheugen nodig (bijv. om als HTTP‑respons te sturen). De `ExportTableOptions`‑klasse laat je een bereik als string exporteren.

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

### Wanneer dit te gebruiken

- CSV teruggeven vanaf een REST‑endpoint (`@RestController` in Spring)
- CSV‑gegevens in een e‑mailbijlage insluiten zonder naar schijf te schrijven
- Snelle sanity‑checks uitvoeren tijdens unit‑tests

## Stap 5: Hoe formules opnieuw berekenen na het laden van een werkmap

Als je werkmap formules bevat—vooral **dynamic‑array formulas** geïntroduceerd in recente Excel‑versies—moet je ze opnieuw berekenen na het laden van het bestand. Aspose.Cells ververst automatisch dynamische‑array‑resultaten, maar je moet nog steeds `calculateFormula()` aanroepen voor reguliere formules.

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

### Waarom opnieuw berekenen?

- Formules kunnen verwijzen naar externe data of vluchtige functies (`NOW()`, `RAND()`) die verse waarden nodig hebben.
- Dynamische‑array‑formules (bijv. `=SORT(A1:A10)`) worden automatisch geëvalueerd, maar het aanroepen van `calculateFormula()` garandeert consistentie over alle bladen.

## Stap 6: Volledig end‑to‑end voorbeeld

Hieronder staat een enkele klasse die **hoe je een scheidingsteken instelt**, **opslaat als CSV**, **cijfers beperkt**, **een CSV‑string exporteert**, **een werkmap laadt met een speciale kalender**, en **formules opnieuw berekent** demonstreert. De code is klaar om te copy‑pasten in je project.

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

### Het resultaat verifiëren

1. Open `output.csv` in een teksteditor – je zou een puntkomma (`;`) moeten zien die elke kolom scheidt.
2. Bevestig dat numerieke kolommen maximaal vijf significante cijfers weergeven.
3. De console‑output zal de in stap 4 gegenereerde CSV‑string afdrukken.
4. Open `japan_updated.xlsx` in Excel – formules die eerder `#REF!` of verouderde waarden lieten zien, zullen nu de juiste resultaten tonen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| CSV toont extra aanhalingstekens | Cellen bevatten komma's terwijl het scheidingsteken ook een komma is | Gebruik een ander scheidingsteken (`;` of `\t`) via `setDelimiter` |
| Getallen worden onjuist afgerond | `setSignificantDigits` toegepast na aangepaste getalopmaak | Pas `setNumberFormat` **voor** `setSignificantDigits` toe |

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel te laden en op te slaan als CSV met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Hoe een CSV‑bestand te laden met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Hoe CSV‑bestanden te laden met aangepaste parsers in Java met Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}