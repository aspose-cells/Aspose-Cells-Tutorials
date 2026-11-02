---
category: general
date: 2026-06-30
description: Come copiare un intervallo in Java usando Aspose.Cells – duplicare l’intervallo
  Excel, copiare la tabella pivot e caricare il workbook Excel in modo efficiente.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: it
og_description: Come copiare un intervallo in Java con Aspose.Cells. Impara a duplicare
  un intervallo Excel, copiare una tabella pivot e caricare una cartella di lavoro
  Excel in pochi minuti.
og_title: Come copiare un intervallo in Java – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Come copiare un intervallo in Java – Copia tabella pivot con Aspose.Cells
url: /it/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare un intervallo in Java – Copia tabella pivot con Aspose.Cells

Ti sei mai chiesto **come copiare un intervallo** da una cartella di lavoro Excel a un'altra senza perdere l'integrità della tabella pivot? Non sei l'unico. In molti flussi di reporting è necessario *duplicare un intervallo Excel* mantenendo la logica della pivot, un vero grattacapo quotidiano. Fortunatamente, Aspose.Cells per Java rende tutto questo un gioco da ragazzi, e in questo tutorial percorreremo un esempio completo e eseguibile che ti mostrerà anche come **caricare una cartella di lavoro Excel**, copiare una tabella pivot e salvare il risultato.

Al termine di questa guida avrai un programma Java autonomo che:

* Carica una cartella di lavoro esistente (`load excel workbook`);
* Definisce le celle esatte che contengono una tabella pivot;
* Copia quella **tabella pivot in un foglio** in una nuova cartella di lavoro;
* Salva il nuovo file, pronto per l'elaborazione successiva.

Nessuno script esterno, nessun passaggio manuale—solo puro codice.

## Cosa ti servirà

Prima di immergerci, assicurati di avere:

* Java 8 o versioni successive (il codice funziona anche con Java 11+);
* Libreria Aspose.Cells per Java (puoi scaricarla da Maven Central);
* Due file Excel di esempio – uno sorgente con una tabella pivot (`source.xlsx`) e una cartella di destinazione dove scrivere `copy-pivot.xlsx`.

Tutto qui. Nessun trucco da IDE sofisticato; qualsiasi editor di testo più `javac` andrà bene.

## Passo 1: Configura il progetto e importa Aspose.Cells

Prima di tutto—mettiamo la libreria a disposizione. Se usi Maven, aggiungi questa dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Se non usi Maven, scarica il JAR dal sito di Aspose e aggiungilo al classpath. Una volta sistemato, crea una nuova classe Java chiamata `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Mantieni la cartella `src/main/java` pulita e dai alla classe un nome significativo; così la manutenzione futura sarà più semplice.

## Passo 2: Carica la cartella di lavoro sorgente (`load excel workbook`)

Ora **carichiamo la cartella di lavoro Excel** che contiene la tabella pivot da copiare. Il costruttore `Workbook` accetta un percorso file, quindi assicurati che il percorso sia corretto.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Perché scegliamo il primo foglio? Nella maggior parte dei casi semplici la pivot si trova sul primo foglio, ma puoi cambiare l'indice o usare il nome del foglio se necessario. Questa flessibilità è uno dei motivi per cui Aspose.Cells brilla.

## Passo 3: Definisci l'intervallo che contiene la tabella pivot

Una tabella pivot di solito occupa un blocco di celle. Supponiamo che copra `A1:G20`. Puoi modificare l'indirizzo per adattarlo ai tuoi dati reali.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Se non sei sicuro dell'indirizzo esatto, apri la cartella di lavoro in Excel, seleziona l'intera pivot e guarda la casella del nome. Ricorda, **duplicare un intervallo Excel** funziona al meglio quando punti all'area esatta—nessuna riga extra, nessuna colonna mancante.

## Passo 4: Crea una nuova cartella di lavoro per la destinazione

Ci serve una cartella di lavoro fresca che riceverà l'intervallo copiato. Qui è dove **copiare la tabella pivot** in un nuovo foglio.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

A questo punto la cartella di lavoro di destinazione è vuota, ma Aspose.Cells aggiunge automaticamente un foglio predefinito, che useremo come destinazione.

## Passo 5: Copia l'intervallo – la tabella pivot rimane intatta

Ecco la riga magica che **copia la tabella pivot** mantenendo vive tutte le sue connessioni interne.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

Il metodo `copy` accetta due argomenti: l'`Range` di origine e l'`Range` di destinazione. Iniziando la destinazione in `A1`, posizioniamo la pivot esattamente dove era nella sorgente. Aspose.Cells copia la cache pivot sottostante, così la nuova cartella di lavoro sa ancora come aggiornare la pivot.

## Passo 6: Salva la cartella di lavoro risultante

Infine, scrivi il nuovo file su disco. Puoi scegliere qualsiasi formato supportato da Aspose (`.xlsx`, `.xls`, `.csv`, ecc.). Restiamo su `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Esegui il programma e dovresti vedere una nuova cartella di lavoro con lo stesso layout della pivot. Aprila in Excel—se tutto è andato bene, potrai aggiornare la pivot senza errori.

### Output previsto

Quando esegui `CopyPivotDemo`, la console stampa:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Aprendo `copy-pivot.xlsx` si scopre un foglio identico all'area pivot della sorgente, e la **tabella pivot in foglio** funziona esattamente come l'originale.

## Esempio completo funzionante

Di seguito trovi la classe Java completa, pronta per l'esecuzione, che unisce tutti i passaggi. Copiala e incollala nel tuo IDE, aggiusta i percorsi dei file e avvia l'esecuzione.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Nota:** Se la tua tabella pivot si estende su più fogli, ripeti il passaggio di copia per ciascun foglio rilevante, oppure usa `Workbook.copy` per clonare interi fogli di lavoro.

## Domande frequenti e casi particolari

### E se la cartella di lavoro sorgente ha più fogli?

Puoi iterare su `sourceWorkbook.getWorksheets()` e copiare ogni intervallo rilevante. Fai solo attenzione a mantenere gli stessi nomi dei fogli nella destinazione se devi preservare i riferimenti.

### La pivot copiata mantiene la sua origine dati?

Sì. Aspose.Cells copia la cache pivot insieme all'intervallo, così la cartella di lavoro di destinazione punta ancora alla stessa origine dati all'interno dello stesso file. Se in seguito sposti i dati in un foglio diverso, potresti dover aggiornare manualmente la pivot.

### Come copiare una pivot che usa una fonte dati esterna?

Quando la fonte dati della pivot è un file esterno, devi prima incorporare quei dati nella cartella di lavoro di destinazione (ad esempio, copiando l'intervallo di dati sorgente) prima di copiare la pivot. Altrimenti la pivot mostrerà errori “#REF!”.

### Posso copiare la pivot senza i dati circostanti?

Assolutamente. Basta regolare `pivotRange` per coprire solo le celle della pivot (di solito l'angolo in alto a sinistra più l'area dati). Puoi anche usare `sourceSheet.getPivotTables().get(0).getPivotTableArea()` per ottenere programmaticamente l'intervallo esatto.

## Consigli per progetti reali

* **Elaborazione batch:** Se devi duplicare decine di cartelle di lavoro, avvolgi il codice sopra in un metodo e chiamalo all'interno di un ciclo che itera su una directory.
* **Performance:** Per file di grandi dimensioni, riutilizza una singola istanza `Workbook` e chiama `Workbook.calculateFormula()` solo dopo aver completato tutte le copie.
* **Gestione errori:** Avvolgi la logica di copia in blocchi try‑catch e registra `Exception.getMessage()`; Aspose lancia `CellsException` per intervalli non validi.

## Conclusione

Abbiamo appena coperto **come copiare un intervallo** in Java usando Aspose.Cells, mostrandoti come **duplicare un intervallo Excel**, **copiare una tabella pivot** e **caricare una cartella di lavoro Excel** tutto in un unico programma ordinato. I passaggi sono semplici, il codice è pienamente eseguibile e l'approccio scala da una demo a foglio singolo a lavori batch di livello enterprise.

Pronto per la prossima sfida? Prova a esportare la pivot copiata in PDF, o a rinfrescarla programmaticamente dopo aver aggiunto nuovi dati. Entrambe le attività si basano sulla stessa fondazione che abbiamo costruito qui, così sarai ben equipaggiato per affrontarle.

Hai domande o vuoi condividere le tue personalizzazioni? Lascia un commento qui sotto—buona programmazione! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "diagramma di come copiare l'intervallo")

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}