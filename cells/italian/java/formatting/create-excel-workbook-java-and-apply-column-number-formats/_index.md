---
category: general
date: 2026-09-27
description: Crea una cartella di lavoro Excel in Java, importa dati SQL, imposta
  il formato numerico della colonna e salva la cartella di lavoro come XLSX usando
  Aspose.Cells in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: it
lastmod: 2026-09-27
og_description: Crea una cartella di lavoro Excel in Java, importa dati SQL, imposta
  il formato numerico della colonna e salva la cartella di lavoro come XLSX con un
  esempio Java completamente funzionante.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Crea cartella di lavoro Excel in Java – importa dati SQL e imposta i formati
  numerici delle colonne
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Crea una cartella di lavoro Excel in Java e applica formati numerici alle colonne
url: /it/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare una cartella di lavoro Excel in Java e applicare formati numerici alle colonne

Se hai bisogno di **creare una cartella di lavoro Excel in Java** e formattare le colonne numeriche, questa guida ti mostra esattamente come fare. Imparerai a importare dati SQL in Excel, impostare un formato numerico per ogni colonna e **salvare la cartella di lavoro come XLSX** usando la libreria Aspose.Cells.

Lavorare con i fogli di calcolo da Java spesso risulta frammentato: gli sviluppatori copiano‑incollano snippet, dimenticano di formattare i numeri o finiscono con file CSV invece di veri file Excel. Questo tutorial elimina tali frizioni fornendo una soluzione end‑to‑end unica che puoi inserire in qualsiasi progetto Java.

Al termine dell’articolo sarai in grado di:

* Connetterti a un database e recuperare un `DataTable` (o `ResultSet`)  
* Creare una nuova cartella di lavoro con Aspose.Cells  
* Applicare uno stile **add number format excel** coerente a ogni colonna  
* **Salvare la cartella di lavoro come XLSX** in una posizione a tua scelta  

L’unico prerequisito è un ambiente di sviluppo Java (JDK 8+ consigliato) e il JAR Aspose.Cells for Java presente nel classpath.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| JDK 8 o versioni successive | Fornisce le funzionalità del linguaggio usate nell’esempio. |
| Aspose.Cells for Java (ultima versione) | Gestisce la creazione, lo styling e il salvataggio di Excel senza necessità di Office installato. |
| Un database compatibile JDBC (es. MySQL, PostgreSQL) | Fornisce i dati SQL che importeremo. |
| Maven o Gradle (opzionale) | Semplifica la gestione delle dipendenze. |

Aggiungi Aspose.Cells al tuo `pom.xml` di Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Oppure scarica il JAR direttamente dal sito Aspose e aggiungilo al classpath del tuo progetto.

---

## Passo 1: Creare Excel workbook java

Il primo blocco logico è istanziare un nuovo `Workbook`. Questo oggetto rappresenta l’intero file Excel in memoria e ti dà accesso a fogli, celle e stili.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Creare la cartella di lavoro in anticipo ci fornisce anche una factory `Style` che ci servirà più tardi quando **set number format column**.

---

## Passo 2: Recuperare dati da SQL (import sql data excel)

Di seguito apriamo una connessione JDBC, eseguiamo una semplice istruzione `SELECT` e carichiamo il result set in un `DataTable` di Aspose. La classe `DataTable` imita la .NET `DataTable` e funziona senza problemi con il metodo `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Suggerimento:** Se hai già un `DataTable` da un’altra fonte (es. parsing CSV), puoi saltare il codice JDBC e restituire direttamente quella tabella.

---

## Passo 3: Preparare uno stile riutilizzabile (add number format excel)

Vogliamo che ogni colonna numerica mostri i numeri con due decimali e separatore delle migliaia. Invece di stilizzare ogni cella singolarmente, creiamo un oggetto `Style` una volta per colonna e lo riusiamo durante l’importazione. Questo è il modo più efficiente per **add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Puoi adattare la stringa di formato (`"#,##0.00"`) a qualsiasi formato numerico di Excel di cui hai bisogno. Per le date, usa `styles[i].setCustom("mm-dd-yyyy")`, ecc.

---

## Passo 4: Importare il DataTable e applicare gli stili di colonna

Ora uniamo tutto. La sovraccarico di `importDataTable` ci permette di passare il `DataTable`, specificare se la prima riga deve essere trattata come intestazione di colonna e fornire l’array di stili. Questo imposta automaticamente **set number format column** per ogni cella nella colonna corrispondente.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Poiché abbiamo passato `true` per il flag `importColumnNames`, la prima riga del foglio contiene i nomi delle colonne provenienti dal `DataTable`. Ogni riga successiva riceve i dati, già formattati secondo lo stile che abbiamo definito.

---

## Passo 5: Salvare la cartella di lavoro come xlsx

L’ultimo passo è persistere la cartella di lavoro in memoria su un file fisico. Aspose.Cells supporta molti formati; useremo il moderno formato XLSX, quello che la maggior parte delle applicazioni si aspetta oggi.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Puoi cambiare `filePath` con qualsiasi percorso valido sul tuo sistema. Il metodo lancia `IOException` se la directory non esiste o se non hai i permessi di scrittura.

---

## Esempio completo, eseguibile

Unendo tutti i pezzi otteniamo un programma autonomo che puoi compilare ed eseguire subito.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Risultato atteso

L’esecuzione del programma crea un file chiamato **DataTableWithNumberFormat.xlsx** nella directory di lavoro. Aprilo con Microsoft Excel, LibreOffice Calc o qualsiasi visualizzatore compatibile con XLSX e vedrai:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*La colonna **Amount** mostra i numeri con due decimali e separatore delle migliaia, grazie allo stile **add number format excel** che abbiamo applicato.*

---

## Domande comuni e gestione dei casi limite

| Domanda | Risposta |
|----------|--------|
| **E se la mia query non restituisce righe?** | Il `DataTable` sarà vuoto ma conterrà comunque le definizioni delle colonne. La cartella di lavoro conterrà solo la riga di intestazione, spesso sufficiente per i processi successivi. |
| **Come applicare formati diversi per colonna?** | Modifica `buildColumnStyles` per ispezionare il nome della colonna o il tipo di dato e assegnare un formato personalizzato (es. date, percentuali). |
| **Posso scrivere direttamente su un `ByteArrayOutputStream`?** | Sì. Sostituisci `workbook.save(filePath, SaveFormat.XLSX);` con


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}