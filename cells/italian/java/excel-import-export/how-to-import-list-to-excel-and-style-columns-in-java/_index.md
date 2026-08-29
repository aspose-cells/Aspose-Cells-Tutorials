---
category: general
date: 2026-08-17
description: Importa una lista in Excel in Java usando Aspose.Cells, impara a formattare
  le colonne, esporta i dati in xlsx e crea un workbook Excel programmaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import list to excel
- how to style column
- export data to xlsx
- import data with header
- create excel workbook java
language: it
lastmod: 2026-08-17
og_description: Importa un elenco in Excel in Java con Aspose.Cells, formatta le intestazioni
  delle colonne, esporta i dati in xlsx e crea un workbook Excel in modo efficiente.
og_image_alt: Screenshot of a Java‑generated Excel file showing bold column headers
og_title: Importa una lista in Excel con Java – guida completa con formattazione delle
  colonne
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  headline: How to import list to Excel and style columns in Java
  type: TechArticle
- description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  name: How to import list to Excel and style columns in Java
  steps:
  - name: Why this works
    text: '* **`importDataTable`** reads the keys of each map (`"Name"` and `"Score"`)
      as column headers when the `true` flag is set. This satisfies the **import data
      with header** requirement. * The **style array** aligns with the column order.
      By setting `columnStyles[1].getFont().setBold(true)`, we answer t'
  - name: Null values and type safety
    text: 'If a map contains `null` or mixed‑type values, Aspose.Cells automatically
      writes an empty cell. To guarantee consistent typing, you can pre‑process the
      list:'
  - name: Mismatched column counts
    text: '`importDataTable` expects the style array length to match the number of
      columns. If you add a new column later, remember to expand `columnStyles` accordingly,
      otherwise Aspose.Cells throws `IndexOutOfBoundsException`.'
  - name: Large data sets
    text: For more than 10 000 rows, consider using the **`importArray`** overload,
      which streams data directly to the worksheet and reduces memory consumption.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Data export
title: Come importare una lista in Excel e formattare le colonne in Java
url: /it/java/excel-import-export/how-to-import-list-to-excel-and-style-columns-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come importare una lista in Excel e formattare le colonne in Java

Se hai bisogno di **importare una lista in Excel** da un'applicazione Java, questa guida ti mostra una soluzione completa, pronta all'uso. Vedrai come creare una cartella di lavoro Excel, importare una lista di mappe come tabella di dati, applicare uno stile grassetto a una colonna specifica e salvare il risultato come file **xlsx**.

Lavorare con i fogli di calcolo è una necessità comune per report, scambio di dati o automazione. Alla fine di questo tutorial sarai in grado di **esportare dati in xlsx** con formattazione personalizzata delle colonne senza uscire dal tuo codice Java.

## Di cosa avrai bisogno

* Java 17 o superiore (il codice funziona anche con Java 8+)
* Libreria Aspose.Cells per Java – versione 23.10 (o l'ultima release)
* Un ambiente di sviluppo come IntelliJ IDEA o Eclipse
* Familiarità di base con le collezioni Java (`List`, `Map`)

> **Suggerimento:** Aggiungi la dipendenza Maven di Aspose.Cells per mantenere la libreria sempre aggiornata:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Importare una lista in Excel con Aspose.Cells

Il primo passo importante è trasformare una `List<Map<String,Object>>` Java in un foglio di lavoro Excel. Aspose.Cells fornisce il metodo `importDataTable`, che accetta una collezione, un flag per l'intestazione, riga/colonna di partenza e un array di stile opzionale.

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcel {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Prepare the source data (simulating a DataTable)
        List<Map<String, Object>> dataRows = new ArrayList<>();
        dataRows.add(Map.of("Name", "Alice", "Score", 95));
        dataRows.add(Map.of("Name", "Bob",   "Score", 82));
        dataRows.add(Map.of("Name", "Charlie", "Score", 78));

        // 2️⃣ Create style objects – make the "Score" column bold
        Style[] columnStyles = new Style[2];               // two columns: Name, Score
        Workbook styleWorkbook = new Workbook();           // temporary workbook for style creation
        columnStyles[0] = styleWorkbook.createStyle();    // default style for "Name"
        columnStyles[1] = styleWorkbook.createStyle();    // custom style for "Score"
        columnStyles[1].getFont().setBold(true);          // **how to style column** – bold font

        // 3️⃣ Import the list into a worksheet using the style array
        Workbook workbook = new Workbook();                // **create excel workbook java**
        Worksheet sheet = workbook.getWorksheets().get(0);
        // true → include column headers from the map keys
        sheet.getCells().importDataTable(dataRows, true, 0, 0, columnStyles);

        // 4️⃣ Save the workbook to an .xlsx file
        String outputPath = "output/datatable_with_style.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved to: " + outputPath);
    }
}
```

### Perché funziona

* **`importDataTable`** legge le chiavi di ogni mappa (`"Name"` e `"Score"`) come intestazioni di colonna quando il flag `true` è impostato. Questo soddisfa il requisito di **importare dati con intestazione**.
* L'**array di stile** è allineato all'ordine delle colonne. Impostando `columnStyles[1].getFont().setBold(true)`, rispondi alla domanda **come formattare una colonna** senza influenzare le altre colonne.
* L'uso di un `Workbook` temporaneo solo per la creazione dello stile evita di inquinare la cartella di lavoro finale con celle non necessarie.

## Esportare dati in xlsx – gestione dei casi limite più comuni

### Valori null e sicurezza dei tipi
Se una mappa contiene `null` o valori di tipo misto, Aspose.Cells scrive automaticamente una cella vuota. Per garantire una tipizzazione coerente, puoi pre‑elaborare la lista:

```java
for (Map<String, Object> row : dataRows) {
    row.replaceAll((k, v) -> v == null ? "" : v);
}
```

### Conteggi di colonne non corrispondenti
`importDataTable` si aspetta che la lunghezza dell'array di stile corrisponda al numero di colonne. Se aggiungi una nuova colonna in seguito, ricorda di ampliare `columnStyles` di conseguenza; altrimenti Aspose.Cells solleverà `IndexOutOfBoundsException`.

### Set di dati di grandi dimensioni
Per più di 10 000 righe, considera l'uso della sovraccarico **`importArray`**, che trasmette i dati direttamente al foglio di lavoro riducendo il consumo di memoria.

## Come formattare colonne aggiuntive

Puoi formattare qualsiasi colonna estendendo l'array `columnStyles`. Di seguito un esempio che rende sia “Name” che “Score” in grassetto e aggiunge un colore di sfondo alla colonna “Score”.

```java
// Extend to three columns (Name, Score, Date)
Style[] extendedStyles = new Style[3];
Workbook tmp = new Workbook();
extendedStyles[0] = tmp.createStyle(); // Name – bold
extendedStyles[0].getFont().setBold(true);

extendedStyles[1] = tmp.createStyle(); // Score – bold + yellow background
extendedStyles[1].getFont().setBold(true);
extendedStyles[1].getPattern().setBackgroundColor(Color.getYellow());

extendedStyles[2] = tmp.createStyle(); // Date – default
```

Sostituisci il `columnStyles` originale con `extendedStyles` e adegua la fonte dei dati di conseguenza. Questo dimostra **come formattare una colonna** per più scenari.

## Verifica del risultato

Apri `output/datatable_with_style.xlsx` in Microsoft Excel, Google Sheets o LibreOffice Calc. Dovresti vedere:

| **Name**   | **Score** |
|------------|----------|
| Alice      | **95**   |
| Bob        | **82**   |
| Charlie    | **78**   |

L'intestazione **Score** e le sue celle appaiono in grassetto, confermando che lo stile è stato applicato correttamente.

## Esempio completo end‑to‑end (pronto da copiare e incollare)

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcelFull {
    public static void main(String[] args) throws Exception {
        // ----- Prepare sample data -----
        List<Map<String, Object>> rows = new ArrayList<>();
        rows.add(Map.of("Name", "Alice",   "Score", 95));
        rows.add(Map.of("Name", "Bob",     "Score", 82));
        rows.add(Map.of("Name", "Charlie", "Score", 78));

        // ----- Create column styles (Score column bold) -----
        Style[] styles = new Style[2];
        Workbook styleWB = new Workbook();                // temporary workbook for style objects
        styles[0] = styleWB.createStyle();                // Name – default
        styles[1] = styleWB.createStyle();                // Score – custom
        styles[1].getFont().setBold(true);                // apply bold font

        // ----- Build the workbook and import the list -----
        Workbook wb = new Workbook();                     // **create excel workbook java**
        Worksheet ws = wb.getWorksheets().get(0);
        ws.getCells().importDataTable(rows, true, 0, 0, styles); // true = import header row

        // ----- Save as XLSX -----
        String outFile = "output/datatable_with_style.xlsx";
        wb.save(outFile, SaveFormat.XLSX);

        System.out.println("Excel file created at: " + outFile);
    }
}
```

Eseguendo questo programma otterrai esattamente la cartella di lavoro mostrata in precedenza.

## Conclusione

Ora sai come **importare una lista in Excel**, applicare una formattazione personalizzata a una colonna specifica e **esportare dati in xlsx** usando Aspose.Cells per Java. Il tutorial ha coperto:

* Creazione di una cartella di lavoro Excel in Java (`create excel workbook java`)
* Importazione di una lista di mappe con intestazioni di colonna (`import data with header`)
* Formattazione di una colonna (`how to style column`) tramite un array di stile
* Salvataggio del risultato come file XLSX

Da qui puoi esplorare formattazioni più avanzate (bordi, formati numerici), aggiungere grafici o generare più fogli nello stesso workbook. Sperimenta con diverse fonti di dati—file CSV, database o risposte API REST—per estendere il modello dimostrato in questa guida.

Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)
- [Excel Data Import and Export Tutorials for Aspose.Cells Java](/cells/english/java/import-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}