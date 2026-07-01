---
category: general
date: 2026-06-30
description: Imposta il carattere in grassetto durante l'importazione di una DataTable
  in Excel usando Java. Impara il codice di formattazione condizionale, importa la
  DataTable in Excel e stila le tabelle senza sforzo.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: it
og_description: Imposta il testo in grassetto in Java durante l'esportazione di una
  DataTable in Excel. Questa guida copre il codice di formattazione condizionale,
  l'importazione della DataTable in Excel e lo styling della tabella.
og_title: Imposta il carattere in grassetto nell'esportazione Excel Java – Tutorial
  passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Imposta il carattere in grassetto nell'esportazione Excel con Java – Guida
  completa
url: /it/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il Grassetto del Font in Java Excel Export – Guida Completa

Ti sei mai chiesto **come impostare il grassetto del font** per colonne specifiche mentre **importi file excel datatable**? Non sei il solo. Molti sviluppatori si trovano in difficoltà quando hanno bisogno di un foglio di calcolo ben formattato senza dover modificare manualmente ogni cella. La buona notizia? Con poche righe di Java puoi importare un `DataTable`, applicare font in grassetto e persino aggiungere del **codice di formattazione condizionale**—tutto in modo programmatico.

In questo tutorial percorreremo un esempio completo e eseguibile che mostra **come importare datatable** in una cartella di lavoro Excel, applicare **set font bold** su ogni colonna con indice pari e, facoltativamente, aggiungere una semplice formattazione condizionale. Alla fine avrai uno snippet pronto da eseguire e una chiara comprensione di **import table with styles** per qualsiasi progetto.

## Prerequisiti

- Java 8 o versioni successive (il codice funziona anche su Java 17)  
- Aspose.Cells per Java (va bene la versione di prova) – aggiungi la dipendenza Maven o il JAR al tuo classpath.  
- Familiarità di base con la conversione `java.sql` `ResultSet` → `DataTable` (simuleremo una tabella per semplicità).  
- Un IDE o uno strumento di build come Maven/Gradle.

> **Pro tip:** Se stai usando Maven, aggiungi questo al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Panoramica della Soluzione

1. **Crea un mock `DataTable`** che imita i dati che normalmente estrarresti da un database.  
2. **Genera un array di `CellStyle`** dove ogni colonna pari ottiene un font in grassetto – è il cuore di **set font bold**.  
3. **Recupera il primo foglio di lavoro** dalla cartella di lavoro.  
4. **Importa il `DataTable`** con le intestazioni di colonna, a partire dalla cella `A1`, e applica gli stili preparati.  
5. (Facoltativo) **Aggiungi una regola di formattazione condizionale** per illustrare la parola chiave **conditional formatting code**.

Ogni passaggio è spiegato in inglese semplice, e i blocchi di codice sono completamente autonomi così puoi copiare‑incollare ed eseguire immediatamente.

---

## Passo 1: Recupera o Costruisci il DataTable da Importare

Nelle applicazioni reali probabilmente chiameresti le utility di conversione `ResultSet` → `DataTable`. Per questa guida costruiremo manualmente un semplice `DataTable` così potrai concentrarti sulla parte Excel.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Perché è importante:** Avere un `DataTable` pronto ci permette di concentrarci sull'API **import datatable excel** e sulla logica di stile. Il metodo sopra è riutilizzabile—basta sostituire le righe hard‑coded con una query al database quando passi in produzione.

## Passo 2: Prepara gli Stili – Qui è Dove **Set Font Bold**

Ora costruiremo un array di oggetti `CellStyle`, uno per colonna. La regola è semplice: **set font bold** per ogni colonna con indice pari (0, 2, 4,…). Le colonne dispari rimangono normali.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Perché Usare un Array di Stili?

- **Performance:** Applicare uno stile per colonna è più veloce che formattare ogni cella individualmente.  
- **Consistency:** Ogni cella in una colonna eredita la stessa formattazione, garantendo un aspetto uniforme.  
- **Scalability:** Aggiungere altre colonne in seguito richiede solo l'estensione dell'array—nessuna riscrittura del codice.

## Passo 3: Accedi al Primo Foglio di Lavoro nella Cartella di Lavoro

Aspose.Cells crea un foglio di lavoro predefinito per noi, ma è buona pratica recuperarlo esplicitamente. Questo dimostra anche **how to import datatable** in un foglio specifico.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

## Passo 4: Importa il DataTable con Stili – L'Operazione Centrale **Import Table With Styles**

Il metodo `importDataTable` fa il lavoro pesante. Copia i dati, aggiunge le intestazioni di colonna e applica l'array di stili che abbiamo creato in precedenza.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Quando esegui l'esempio, vedrai **set font bold** applicato alle colonne `ID` e `Score`, mentre `Name` rimane normale.

## Passo 5 (Facoltativo): Aggiungi Formattazione Condizionale – Un Rapido Esempio di **Conditional Formatting Code**

Se vuoi evidenziare le righe in cui il punteggio supera 90, qualche riga extra farà al caso tuo. Questo mostra la parola chiave **conditional formatting code** senza deviare dal flusso principale.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Nota:** Lo snippet sopra è facoltativo ma dimostra come puoi sovrapporre **conditional formatting code** alla tabella già formattata.

## Mettere Tutto Insieme – Esempio Completo e Eseguibile

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Automatizza la Formattazione Condizionale di Excel con Aspose.Cells per Java: Guida Completa](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Come Implementare Impostazioni di Font Personalizzate in Aspose.Cells Java per la Formattazione di Excel](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Imposta la Dimensione del Font in Excel con Aspose.Cells Java - Guida Completa](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}