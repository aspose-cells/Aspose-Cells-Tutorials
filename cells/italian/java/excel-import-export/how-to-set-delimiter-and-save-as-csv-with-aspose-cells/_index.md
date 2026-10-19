---
category: general
date: 2026-08-14
description: Come impostare il delimitatore e salvare come CSV usando Aspose.Cells,
  limitare le cifre, esportare stringhe CSV e ricalcolare le formule in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: it
lastmod: 2026-08-14
og_description: Come impostare il delimitatore e salvare come CSV con Aspose.Cells,
  limitare le cifre, esportare stringhe CSV e ricalcolare le formule in Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Come impostare il delimitatore e salvare come CSV – Guida Aspose.Cells
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
title: Come impostare il delimitatore e salvare come CSV con Aspose.Cells
url: /it/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare il delimitatore e salvare come CSV con Aspose.Cells

Se hai bisogno di **impostare il delimitatore** durante l'esportazione dei dati da una cartella di lavoro Excel, questa guida ti mostra una soluzione completa, end‑to‑end, usando Aspose.Cells per Java. Imparerai come configurare il delimitatore CSV, limitare il numero di cifre significative, esportare una stringa CSV e aggiornare le formule dynamic‑array dopo aver caricato una cartella di lavoro.

Il tutorial copre tutto ciò di cui hai bisogno per eseguire il codice sulla tua macchina, inclusa la gestione di calendari speciali come il regno dell'Imperatore giapponese. Alla fine, sarai in grado di generare file CSV accurati, controllare la precisione numerica e garantire che le formule siano aggiornate.

## Prerequisiti

- Java 17 o versioni successive (il codice si compila anche con JDK 11+)
- Aspose.Cells per Java 23.9 o più recente – scarica dal [sito web di Aspose](https://products.aspose.com/cells/java/)
- Familiarità di base con Maven o Gradle per la gestione delle dipendenze
- Un IDE (IntelliJ IDEA, Eclipse, VS Code) o un semplice editor di testo e la riga di comando

> **Suggerimento professionale:** Usa una cartella `libs` dedicata o Maven Central per mantenere il JAR di Aspose.Cells nel tuo classpath. Gli esempi seguenti presumono un progetto Maven.

## Passo 1: Configurare il progetto Maven

Crea un `pom.xml` con la dipendenza di Aspose.Cells:

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

Esegui `mvn clean compile` per scaricare la libreria e verificare che la compilazione abbia successo.

## Passo 2: Come impostare il delimitatore e salvare come CSV

L'obiettivo principale è cambiare il delimitatore predefinito della virgola con un carattere personalizzato (ad esempio, punto e virgola) quando si salva una cartella di lavoro Excel come CSV. Aspose.Cells fornisce `CsvSaveOptions` a questo scopo.

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

### Perché funziona

- `CsvSaveOptions.setDelimiter(char)` indica ad Aspose.Cells quale carattere separa i campi. Per impostazione predefinita è una virgola, ma funziona qualsiasi carattere (tab `'\t'`, pipe `'|'`, ecc.).
- `setSignificantDigits(int)` limita la precisione numerica, soddisfacendo il requisito **come limitare le cifre** senza formattare manualmente ogni cella.

#### Output previsto

Il file `output.csv` conterrà righe simili a:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Nota che i numeri sono arrotondati a cinque cifre significative (ad esempio, `123.45678` → `123.46`).

## Passo 3: Come limitare le cifre quando si salva CSV

Se hai bisogno di un controllo più preciso sulla formattazione numerica, puoi anche utilizzare un'istanza `CsvSaveOptions` per specificare una stringa di formato numerico personalizzata.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` segue i pattern in stile .NET, che Aspose.Cells rispetta.
- Combinando sia `setNumberFormat` sia `setSignificantDigits` ottieni arrotondamenti prevedibili su diverse locale.

## Passo 4: Come esportare CSV come stringa con un delimitatore personalizzato

A volte non vuoi un file fisico; hai bisogno dei dati CSV in memoria (ad esempio, per inviarli come risposta HTTP). La classe `ExportTableOptions` ti consente di esportare un intervallo come stringa.

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

### Quando usarlo

- Restituire CSV da un endpoint REST (`@RestController` in Spring)
- Incorporare dati CSV in un allegato email senza scrivere su disco
- Eseguire rapidi controlli di coerenza durante i test unitari

## Passo 5: Come ricalcolare le formule dopo aver caricato una cartella di lavoro

Se la tua cartella di lavoro contiene formule—specialmente **formule dynamic‑array** introdotte nelle versioni recenti di Excel—devi ricalcolarle dopo aver caricato il file. Aspose.Cells aggiorna automaticamente i risultati delle dynamic‑array, ma è comunque necessario invocare `calculateFormula()` per le formule regolari.

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

### Perché ricalcolare?

- Le formule possono fare riferimento a dati esterni o a funzioni volatili (`NOW()`, `RAND()`) che necessitano di valori aggiornati.
- Le formule dynamic‑array (ad esempio, `=SORT(A1:A10)`) vengono valutate automaticamente, ma chiamare `calculateFormula()` garantisce la coerenza su tutti i fogli.

## Passo 6: Esempio completo end‑to‑end

Di seguito è presente una singola classe che dimostra **come impostare il delimitatore**, **salvare come CSV**, **limitare le cifre**, **esportare una stringa CSV**, **caricare una cartella di lavoro con un calendario speciale** e **ricalcolare le formule**. Il codice è pronto per essere copiato e incollato nel tuo progetto.

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

### Verifica del risultato

1. Apri `output.csv` in un editor di testo – dovresti vedere un punto e virgola (`;`) che separa ogni colonna.
2. Conferma che le colonne numeriche mostrino al massimo cinque cifre significative.
3. L'output della console stamperà la stringa CSV generata nel passo 4.
4. Apri `japan_updated.xlsx` in Excel – qualsiasi formula che mostrava precedentemente `#REF!` o valori obsoleti ora mostrerà i risultati corretti.

## Problemi comuni e come evitarli

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| Il CSV mostra virgolette extra | Le celle contengono virgole mentre il delimitatore è anche una virgola | Usa un delimitatore diverso (`;` o `\t`) tramite `setDelimiter` |
| I numeri sono arrotondati in modo errato | `setSignificantDigits` applicato dopo il formato numerico personalizzato | Applica `setNumberFormat` **prima** di `setSignificantDigits` |

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come caricare e salvare Excel come CSV usando Aspose.Cells per Java: Guida completa](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Come caricare un file CSV usando Aspose.Cells per Java: Guida completa](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Come caricare file CSV usando parser personalizzati in Java con Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}