---
category: general
date: 2026-11-22
description: Scopri come utilizzare un formato numerico personalizzato per formattare
  una colonna come valuta in Excel usando Java. Imposta rapidamente il formato numerico
  di Excel con uno stile semplice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: it
lastmod: 2026-11-22
og_description: Applica un formato numerico personalizzato in Excel con Java. Questo
  tutorial mostra come impostare il formato numerico di Excel e formattare la prima
  colonna come valuta.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Applica un formato numerico personalizzato in Excel con Java – guida passo
  passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Come applicare un formato numerico personalizzato in Excel con Java
url: /it/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come applicare un formato numerico personalizzato in Excel con Java

Se hai bisogno di **formato numerico personalizzato** per una colonna in un foglio di lavoro Excel, questa guida ti mostra esattamente come farlo usando Java. Che tu stia generando report finanziari o esportando dati contabili, formattare la prima colonna come valuta rende l'output immediatamente leggibile.

Nell'esempio seguente **formatteremo la colonna come valuta**, applicheremo lo stile alla prima colonna e poi importeremo un `DataTable` nel foglio di lavoro. Lo stesso approccio funziona per qualsiasi formato numerico che desideri visualizzare.

## Cosa imparerai

* Come creare un **formato numerico personalizzato** con l'oggetto `Style` di Apache POI.  
* Come **impostare il formato numerico di Excel** per una colonna specifica, incluso il caso **impostazione del formato valuta**.  
* Come **formattare la prima colonna** durante l'importazione di un `DataTable`.  
* Come salvare la cartella di lavoro e verificare che la formattazione appaia correttamente.

### Prerequisiti

* Java 17 o versioni successive.  
* Apache POI 5.x (la libreria che fornisce `Workbook`, `Worksheet` e `Style`).  
* Un'implementazione di `DataTable` che può essere iterata come quella nell'esempio di codice.  
* Familiarità di base con i concetti di Java ed Excel.

---

## Passo 1: Configurare il progetto e importare i dati

Per prima cosa, aggiungi Apache POI al tuo progetto. Se usi Maven, includi la seguente dipendenza:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Successivamente, ottieni i dati di origine come `DataTable`. In uno scenario reale, questi potrebbero provenire da una query al database, da un file CSV o da una risposta API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Suggerimento:** Assicurati che le colonne del `DataTable` abbiano i tipi Java corretti (`Integer`, `Double`, ecc.) perché il formato numerico influisce solo sulle celle numeriche.

---

## Passo 2: Creare un **formato numerico personalizzato** per la prima colonna

Un **formato numerico personalizzato** indica a Excel come visualizzare i valori numerici. Per mostrare i valori come valuta utilizziamo il formato predefinito `CURRENCY`, ma è anche possibile definire pattern come `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Perché funziona:**  
* `createCellStyle()` restituisce un oggetto stile riutilizzabile.  
* `setDataFormat()` collega il **formato valuta** allo stile, che Excel applica a ogni cella che utilizza questo stile.  
* Memorizzando lo stile in `columnStyles[0]` garantiamo che solo la prima colonna riceva la formattazione valuta.

---

## Passo 3: Importare il `DataTable` applicando gli stili di colonna

Ora importiamo i dati nel foglio di lavoro. Il metodo `importDataTable` accetta l'array di stili, permettendoci di **formattare la prima colonna** e lasciare le colonne rimanenti con la formattazione predefinita.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

La chiamata sopra **imposta il formato numerico di Excel** solo per la prima colonna. Tutte le altre colonne ereditano lo stile predefinito della cartella di lavoro, il che mantiene il codice semplice ed efficiente.

---

## Passo 4: Salvare la cartella di lavoro e verificare il risultato

Infine, scrivi la cartella di lavoro su un file e aprila in Excel per confermare che la prima colonna mostri i simboli di valuta.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Output previsto:**  
Quando apri *FormattedReport.xlsx*, i valori nella colonna A appaiono con il simbolo di valuta appropriato (ad esempio, `$1,234.00`). Tutte le altre colonne mantengono la loro rappresentazione numerica originale.

---

## Variazioni comuni e casi limite

| Situazione | Adeguamento |
|-----------|------------|
| **Valuta diversa** (ad es. Euro) | Sostituire `Style.CustomNumberFormat.CURRENCY` con un pattern personalizzato: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Più di una colonna formattata** | Popolare voci aggiuntive in `columnStyles[]` con i propri oggetti `CellStyle`. |
| **Set di dati di grandi dimensioni** | Usare `importDataTable` in batch o streammare le righe per evitare `OutOfMemoryError`. |
| **Separatori specifici per locale** | Usare `java.text.NumberFormat` per generare un pattern sensibile al locale e passarlo a `setDataFormat`. |

> **Attenzione:** Riutilizzare un unico oggetto `CellStyle` su molte colonne può causare formattazioni inattese perché Excel limita il numero di stili distinti per cartella di lavoro. Crea uno stile separato per ogni formato unico di cui hai bisogno.

---

## Esempio completo eseguibile

Di seguito è riportato un programma autonomo che dimostra l'intero flusso di lavoro, dalla creazione dei dati al salvataggio della cartella di lavoro formattata.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Eseguendo il programma si crea **FormattedReport.xlsx** dove la colonna A (la colonna “Amount”) viene visualizzata con un **formato numerico personalizzato** che mostra il simbolo del dollaro e due cifre decimali.

---

## Conclusione

Ora sai come **formattare numericamente in modo personalizzato** un foglio di lavoro Excel da Java, **formattare la colonna come valuta**, e **formattare la prima colonna** durante l'importazione dei dati. Creando un `CellStyle` riutilizzabile e passandolo a `importDataTable`, puoi **impostare il formato numerico di Excel** per qualsiasi colonna senza dover iterare manualmente su ogni cella.

Next, try:

* Usare `setDataFormat` con pattern specifici per locale per **impostare il formato valuta**

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Imposta Formato Numerico Excel in Java – Guida Completa](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Applica Formato Numerico Excel in Java – Guida Completa Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Come creare una cartella di lavoro Excel con formato valuta e carattere grassetto in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}