---
category: general
date: 2026-06-18
description: Crea tutorial Java per file Excel che mostra come impostare il colore
  di sfondo delle righe, generare Excel da DataTable e salvare la cartella di lavoro
  come XLSX con alternanza di colore delle righe.
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: it
og_description: Crea file Excel in Java passo dopo passo. Impara a impostare il colore
  di sfondo delle righe, applicare l'ombreggiatura alternata delle righe, generare
  Excel da DataTable e salvare la cartella di lavoro come XLSX.
og_title: Crea file Excel in Java – Guida completa a formattazione ed esportazione
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: Creare un file Excel in Java – Guida completa con stile delle righe ed esportazione
  XLSX
url: /it/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare un file Excel con Java – Guida completa con stile delle righe ed esportazione XLSX

Ti sei mai chiesto come **creare excel file java** dall’aspetto professionale senza dover aprire Excel manualmente? Non sei solo: gli sviluppatori hanno spesso bisogno di un modo rapido per trasformare dati tabulari in un foglio di calcolo ben formattato. In questo tutorial percorreremo una soluzione completa: estrarre dati da un `DataTable`, applicare **alternating row shading excel**, e infine **save workbook as xlsx**. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto Java.

Copriamo tutto ciò di cui hai bisogno: la libreria necessaria (Aspose.Cells per Java), il codice esatto per impostare **row background color**, come **generate excel from datatable**, e alcuni consigli pratici per evitare le insidie più comuni. Niente superflui, solo un esempio solido, pronto‑da‑eseguire, che puoi adattare subito.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Java 17 o successiva (il codice funziona con qualsiasi JDK recente)
- Maven o Gradle per gestire le dipendenze
- Una conoscenza di base delle collezioni Java
- Accesso alla libreria Aspose.Cells per Java (versione di prova gratuita o licenza)

Se preferisci un’alternativa open‑source, la logica si traduce facilmente in Apache POI—basta sostituire le chiamate API. Per brevità rimarremo su Aspose.Cells perché il suo metodo `importDataTable` rende il passaggio **generate excel from datatable** una singola riga.

## Passo 1: Configurare il progetto e aggiungere Aspose.Cells

Aggiungi la seguente dipendenza al tuo `pom.xml` (Maven) o `build.gradle` (Gradle). Questo includerà la libreria core che ci permette di manipolare workbook, stili e colori.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

Dopo aver aggiornato il progetto, sei pronto a scrivere codice Java in stile **create excel file java**.

## Passo 2: Creare il Workbook e caricare i dati

Per prima cosa istanziamo un nuovo `Workbook`. Poi otteniamo un `DataTable`—può essere il risultato di una query JDBC, di un parser CSV o di qualsiasi tabella in memoria che già possiedi.

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

A questo punto abbiamo un workbook pulito e un `DataTable` popolato. Il passo successivo è dove avviene la magia visiva.

## Passo 3: Definire gli stili delle righe – Impostare il colore di sfondo della riga

Vogliamo che ogni riga abbia uno sfondo distinto, alternando tra azzurro chiaro e grigio chiaro. Questo migliora la leggibilità, soprattutto per report di grandi dimensioni. Il codice qui sotto crea un array di `Style`—una voce per ogni riga di dati—e assegna un **set row background color** in base all’indice della riga.

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

Nota come utilizziamo `Color.getLightBlue()` e `Color.getLightGray()`. Aspose.Cells offre una palette ricca, ma puoi sostituire queste chiamate con qualsiasi `Color` desideri—magari i colori del tuo brand aziendale.

## Passo 4: Importare il DataTable con lo stile

Ora uniamo i dati e l’array di stili. Il metodo `importDataTable` si occupa di copiare le righe, applicare lo stile corrispondente e aggiungere le intestazioni di colonna se passi `true` al parametro `importColumnNames`.

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

L’ancora `"A1"` indica ad Aspose dove iniziare a scrivere—l’angolo in alto a sinistra del foglio. Poiché abbiamo fornito l’array `rowStyles`, ogni riga eredita il colore di sfondo impostato in precedenza, ottenendo **alternating row shading excel** senza un ciclo aggiuntivo dopo l’importazione.

## Passo 5: Salvare il Workbook stilizzato come XLSX

Infine, persi­stiamo il workbook su disco. Il metodo `save` determina automaticamente il formato dall’estensione del file, quindi usando `.xlsx` otteniamo un workbook Office Open XML moderno, apribile in Excel, Google Sheets o LibreOffice.

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

Eseguendo il metodo `main` verrà creato un file chiamato `styledTable.xlsx` nella directory radice del tuo progetto. Aprilo e vedrai una tabella ordinatamente formattata con colori di riga alternati—esattamente ciò che uno stakeholder aziendale si aspetta da un report.

![Screenshot del file Excel stilizzato creato con Java](images/styled_excel_java.png "esempio di creazione di file excel java")

*Testo alternativo dell’immagine:* **create excel file java** screenshot che mostra l’alternanza di colore delle righe

## Perché questo approccio funziona meglio rispetto allo styling manuale cella‑per‑cella

Ti starai chiedendo perché usare un array di stili invece di ciclare su ogni riga dopo l’importazione. La risposta è duplice:

1. **Performance** – Applicare lo stile durante l’importazione evita un passaggio extra sul foglio, che può risultare costoso per migliaia di righe.
2. **Manutenibilità** – La logica di stile vive in un unico punto (`rowStyles`), rendendo semplice cambiare colori, aggiungere bordi o modificare il pattern senza toccare il codice di importazione.

Se in seguito dovessi aggiungere altri indicatori visivi (ad esempio evidenziare le righe con un punteggio inferiore a una soglia), basta estendere il blocco `if` all’interno del ciclo—nessun altro cambiamento necessario.

## Varianti comuni e casi limite

### Esportare un DataTable di grandi dimensioni

Quando si gestiscono più di 100 000 righe, potresti raggiungere i limiti di memoria. Aspose.Cells supporta la modalità **streaming**:

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

Imposta la preferenza di memoria prima di creare gli stili e la libreria scriverà i dati su file temporanei invece di mantenerli tutti in RAM.

### Usare Apache POI al posto di Aspose.Cells

Se la licenza è un problema, puoi sostituire la logica di importazione con gli oggetti `CellStyle` di POI. Il concetto rimane lo stesso: crea due `CellStyle`, cicla sulle righe e applica `setFillForegroundColor` con `IndexedColors`. L’unico svantaggio è che il codice diventa un po’ più verboso.

### Aggiungere formattazione condizionale

Supponiamo di voler evidenziare in verde qualsiasi punteggio superiore a 90. Aggiungi questo dopo l’importazione:

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

Ora il foglio di lavoro non solo ha l’alternanza di colore, ma anche evidenziazioni dinamiche.

## Riepilogo: cosa abbiamo realizzato

- **Create excel file java** da un `DataTable` usando Aspose.Cells.
- **Set row background color** programmaticamente, ottenendo **alternating row shading excel**.
- **Save workbook as xlsx**, garantendo compatibilità con gli strumenti di foglio di calcolo moderni.
- Dimostrato come **generate excel from datatable** in modo efficiente ed estensibile.

Il tutto è contenuto in una classe Java compatta e di facile lettura, pronta da copiare‑incollare nel tuo codice.

## Prossimi passi e argomenti correlati

Se ti è piaciuto questo walkthrough, potresti anche approfondire:

- **Esportare grafici** da Java a Excel (API grafici di Aspose.Cells).
- **Proteggere con password** il workbook generato (`workbook.protect(...)`).
- **Scrivere grandi dataset** con lo streaming per mantenere basso l’utilizzo di memoria.
- **Integrare con Spring Boot** per servire il file generato come risposta scaricabile.

Ognuno di questi argomenti si basa sulla stessa base che abbiamo mostrato qui—quindi sentiti libero di sperimentare e ampliare.

---

*Buona programmazione! Se incontri difficoltà o hai idee per ulteriori miglioramenti, lascia un commento qui sotto. Continuiamo la conversazione.*

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API ed esplorare approcci alternativi nei tuoi progetti.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Set Excel Row Heights Using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}