---
category: general
date: 2026-08-20
description: Crea una cartella di lavoro Excel in Java usando Aspose.Cells, imposta
  il formato valuta, aggiungi il carattere in grassetto e importa l'array di stili
  per le celle formattate.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: it
lastmod: 2026-08-20
og_description: Crea una cartella di lavoro Excel in Java, imposta il formato valuta,
  aggiungi il carattere grassetto e scopri come importare lo stile utilizzando Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Crea una cartella di lavoro Excel con celle di valuta formattate in Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Come creare una cartella di lavoro Excel con formato valuta e carattere grassetto
  in Java
url: /it/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una cartella di lavoro Excel con formato valuta e carattere grassetto in Java

Se hai bisogno di **creare una cartella di lavoro Excel** programmaticamente, questa guida ti mostra esattamente come fare. Cammineremo attraverso la creazione di una cartella di lavoro, l'applicazione di un formato valuta, l'aggiunta di un carattere grassetto e l'uso della funzionalità **how to import style** di Aspose.Cells affinché ogni cella importata abbia un aspetto coerente.

Terminerai con un file `DataTableWithStyleArray.xlsx` pronto all'uso che visualizza i numeri in dollari e li evidenzia in grassetto. Non è necessario alcun formattazione manuale in Excel.

## Prerequisiti

- Java 17 o versioni successive installate.
- Una licenza Aspose.Cells per Java (o una chiave di valutazione gratuita).
- Maven o Gradle per gestire la dipendenza `aspose-cells`.
- Familiarità di base con le collezioni Java e `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Suggerimento:** Se incontri una `LicenseException`, posiziona il tuo file di licenza nel classpath e chiama `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` prima di creare la cartella di lavoro.

## Come creare una cartella di lavoro Excel con celle di valuta formattate

Questa sezione contiene i passaggi fondamentali. Ogni passaggio spiega **perché** è importante, non solo **cosa** digitare.

### Passo 1: Inizializzare la cartella di lavoro e il foglio di lavoro

Creare una nuova cartella di lavoro ti fornisce un contenitore pulito per tutta la formattazione successiva.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Perché:** L'oggetto `Workbook` rappresenta l'intero file Excel. Accedere al primo `Worksheet` ti permette di iniziare a popolare i dati immediatamente.

### Passo 2: Creare un DataTable con dati numerici

Un `DataTable` imita una tabella di database, facilitando l'importazione di righe in blocco.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Perché:** L'uso di `DOUBLE` garantisce che i valori mantengano la precisione decimale, fondamentale quando successivamente **format cells currency**.

### Passo 3: Definire uno stile – formato valuta e carattere grassetto

Qui **impostiamo il formato valuta** e **aggiungiamo il carattere grassetto** a un oggetto `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Perché:** La stringa di formato `Number` `$#,##0.00` indica a Excel di trattare la cella come valore monetario, mentre `setBold(true)` attira l'attenzione sui numeri. Inserire lo stile in un array ci prepara al passaggio **how to import style**.

### Passo 4: Configurare le opzioni di importazione per utilizzare l'array di stili

Aspose.Cells consente di passare un `Style[]` tramite `ImportTableOptions`. Questo è il metodo ufficiale **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Perché:** Senza `ImportTableOptions`, le celle importate erediteranno lo stile predefinito, perdendo la formattazione valuta e il grassetto che abbiamo definito.

### Passo 5: Importare il DataTable nel foglio di lavoro

Ora trasferiamo i dati nel foglio nella cella `A1`, applicando automaticamente l'array di stili.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` indica che la prima riga del `DataTable` contiene le intestazioni di colonna.
- `"A1"` è l'angolo in alto a sinistra dove inizia l'importazione.

> **Perché:** L'importazione con l'array di stili garantisce che ogni cella importata riceva lo stile **format cells currency** che abbiamo preparato in precedenza.

### Passo 6: Salvare la cartella di lavoro su disco

Infine, scrivi la cartella di lavoro in memoria su un file fisico.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Perché:** Il salvataggio conserva la formattazione, consentendo a te o ai processi successivi di aprire il file in Excel con l'aspetto desiderato.

## Codice sorgente completo

Di seguito trovi la classe Java completa, pronta per l'esecuzione. Copiala nel tuo IDE, sostituisci `YOUR_DIRECTORY` con una cartella esistente ed esegui.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Output previsto

Quando apri `DataTableWithStyleArray.xlsx` in Microsoft Excel, dovresti vedere:

| Importo |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- I numeri sono visualizzati con un **formato valuta** (simbolo `$`, due cifre decimali).
- Il carattere per entrambe le celle è **grassetto**, rendendole evidenti.

## Variazioni comuni e casi limite

| Scenario | Cosa cambiare | Motivo |
|----------|----------------|--------|
| **Valuta diversa** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Usa il simbolo Euro o qualsiasi formato specifico per la locale. |
| **Più colonne con stili diversi** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | Ogni colonna può avere il proprio formato numerico, carattere, sfondo, ecc. |
| **Grandi set di dati** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Migliora le prestazioni evitando le righe di intestazione o metadati non necessari. |
| **Applicare lo stile dopo l'importazione** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Utile quando solo un sottoinsieme di righe richiede una formattazione speciale. |

## Consigli per l'uso in produzione

- **License early**: Registra la tua licenza Aspose.Cells prima di creare la cartella di lavoro per evitare la filigrana di valutazione.
- **Thread safety**: Le istanze di `Workbook` **non** sono thread‑safe. Crea un'istanza separata per thread se generi molti file contemporaneamente.
- **Memory management**: Per fogli molto grandi, considera l'uso dell'API di streaming di `Workbook` (`Workbook` → `WorkbookDesigner`) per mantenere basso l'uso di memoria.
- **Testing**: Includi un test unitario che apre il file salvato con Apache POI e verifica che il formato numerico dello stile della cella corrisponda a `"$#,##0.00"`.

## Conclusione

Ora sai come **creare una cartella di lavoro Excel** in Java, **impostare il formato valuta**, **aggiungere il carattere grassetto**, e correttamente **how to import style** usando `ImportTableOptions` di Aspose.Cells. Questa soluzione end‑to‑end elimina i passaggi manuali in Excel e garantisce che ogni cella importata segua lo stesso stile **format cells currency**.

Pronto per la prossima sfida? Prova ad aggiungere formattazione condizionale, incorporare grafici o esportare la cartella di lavoro in PDF—tutto riutilizzando la stessa tecnica dell'array di stili. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea una cartella di lavoro Excel usando Aspose.Cells in Java: Guida passo‑passo](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Come creare e formattare celle Excel usando Aspose.Cells per Java: Guida passo‑passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Come stilizzare celle Excel e aggiungere collegamenti ipertestuali usando Aspose.Cells per Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}