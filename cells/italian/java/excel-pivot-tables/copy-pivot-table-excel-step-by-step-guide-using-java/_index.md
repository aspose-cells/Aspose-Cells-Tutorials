---
category: general
date: 2026-06-27
description: Copia una tabella pivot di Excel con Java in pochi minuti – impara come
  copiare un intervallo in un'altra cartella di lavoro e scopri come copiare la tabella
  pivot in modo efficiente.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: it
og_description: Copia una tabella pivot di Excel usando Java. Questa guida mostra
  come copiare un intervallo in un'altra cartella di lavoro e spiega come copiare
  una tabella pivot con un esempio completo.
og_title: Copia Tabella Pivot Excel – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: Copia Tabella Pivot Excel – Guida Passo‑Passo Utilizzando Java
url: /it/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia Tabella Pivot Excel – Tutorial Java

Ti sei mai chiesto come **copy pivot table excel** file senza perdere le connessioni dati sottostanti? Non sei l'unico. Molti sviluppatori incontrano un ostacolo quando provano a spostare una tabella pivot da una cartella di lavoro a un'altra, per finire con un intervallo statico o un riferimento interrotto.  

La buona notizia? Con poche righe di Java e la libreria giusta, puoi **copy pivot table excel** cartelle di lavoro in modo pulito, preservando ogni campo, filtro e layout. In questa guida ti mostreremo anche **how to copy pivot table** usando l'API Aspose.Cells per Java, e aggiungeremo consigli su **copy range to another workbook** per quegli scenari particolari.

> **What you’ll walk away with:** un programma completamente eseguibile che carica una cartella di lavoro sorgente, copia l'intervallo contenente la tabella pivot e salva una nuova cartella di lavoro che appare esattamente come l'originale.

## Prerequisites

Prima di immergerci, assicurati di avere:

- Java 17 o versioni successive (il codice compila con qualsiasi JDK recente).
- Aspose.Cells per Java 23.10 o successivo – la versione di prova gratuita è sufficiente per i test.
- Un file Excel sorgente (`source.xlsx`) che contiene già una tabella pivot nel primo foglio.
- Un IDE o un semplice ambiente di compilazione da riga di comando (Maven/Gradle).

Nessun'altra dipendenza esterna è necessaria.

## Step 1: Set Up the Project and Import Classes

Per prima cosa, crea un progetto Maven (o Gradle, se preferisci) e aggiungi la dipendenza Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Ora importa le classi di cui avremo bisogno:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Mantieni ordinata la cartella `src/main/resources`; posiziona `source.xlsx` lì e riferiscila con un percorso relativo per evitare di codificare percorsi assoluti.

## Step 2: Load the Source Workbook that Contains the Pivot Table

La prima riga di qualsiasi operazione **copy pivot table excel** è caricare la cartella di lavoro che contiene la tabella pivot da duplicare.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

Perché carichiamo l'intera cartella di lavoro invece del solo foglio? Perché la cache della pivot vive a livello di cartella di lavoro; copiare solo il foglio romperebbe la cache e la tua tabella pivot si trasformerebbe in un semplice intervallo.

## Step 3: Grab the Worksheet and Define the Pivot‑Table Range

Successivamente, individuiamo il foglio di lavoro e il blocco di celle esatto che racchiude la tabella pivot. Nella maggior parte dei casi la tabella pivot inizia in `A1`, ma dovresti adeguare l'intervallo al tuo file.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

Se non sei sicuro dell'intervallo, puoi far calcolare ad Aspose.Cells le celle utilizzate:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

Quel piccolo snippet è utile quando devi **copy range to another workbook** senza codificare l'indirizzo.

## Step 4: Create the Destination Workbook

Ora creiamo una nuova cartella di lavoro che riceverà la tabella pivot copiata. Questo è il cuore di **how to copy pivot table**—crei una tela pulita e poi incolli l'intervallo.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

Se hai già un file modello che vuoi arricchire, sostituisci semplicemente il costruttore con `new Workbook("template.xlsx")`.

## Step 5: Add a Worksheet to the Destination Workbook

Anche se un nuovo `Workbook` contiene già un foglio predefinito, aggiungeremo un secondo foglio per dimostrare il processo di copia in una posizione specifica.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

Puoi rinominare il foglio per maggiore chiarezza:

```java
dstWs.setName("CopiedPivot");
```

## Step 6: Copy the Range – Pivot Table Is Preserved

Ecco la riga magica che effettivamente **copy range to another workbook** mantenendo intatta la tabella pivot. L'oggetto `CopyOptions` indica ad Aspose.Cells di preservare tutto, inclusa la cache della pivot.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

Perché impostiamo `PasteType.PASTE_ALL`? Perché l'operazione di incolla predefinita copia solo valori e formattazione, scartando la cache della pivot. Richiedendo esplicitamente `PASTE_ALL`, garantiamo che la cartella di lavoro di destinazione riceva una tabella pivot pienamente funzionale.

## Step 7: Save the Destination Workbook

Infine, scrivi il nuovo file su disco. Dopo questo passaggio potrai aprire `destination.xlsx` in Excel e vedere la tabella pivot esattamente come appariva nel file sorgente.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### Expected Result

- Aprendo `destination.xlsx` si visualizza un foglio chiamato **CopiedPivot**.
- Il foglio contiene una tabella pivot che può essere aggiornata, filtrata e riorganizzata proprio come l'originale.
- Nessun messaggio di errore appare nella console, confermando che **copy pivot table excel** è riuscito.

## Common Questions & Edge Cases

### What if the source workbook has multiple pivot tables?

Puoi ripetere la logica di selezione dell'intervallo per ogni tabella pivot, oppure copiare l'intero foglio:

```java
srcWs.getCells().copy(dstWs.getCells());
```

Copiare l'intero foglio sposta anche tutte le cache delle pivot, rendendolo un modo rapido per **copy range to another workbook** quando hai molte tabelle.

### How to handle external data connections?

Se la tua tabella pivot estrae dati da un database esterno, la cartella di lavoro di destinazione manterrà la stringa di connessione. Per evitare collegamenti interrotti, aggiorna la connessione dopo la copia:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### Does this work with .xls files?

Sì. Aspose.Cells astrae il formato del file, quindi lo stesso codice funziona per `.xls`, `.xlsx`, `.xlsb` e anche per `.ods`. Basta cambiare l'estensione del file nei costruttori `Workbook`.

## Full Working Example

Mettendo tutto insieme, ecco una classe Java pronta per l'esecuzione che dimostra **how to copy pivot table** da una cartella di lavoro all'altra:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

Esegui la classe, apri `destination.xlsx` e vedrai la replica esatta della tabella pivot originale. 🎉

## Conclusion

Abbiamo appena attraversato un flusso di lavoro completo per **copy pivot table excel** usando Java. Caricando la cartella di lavoro sorgente, individuando l'intervallo della tabella pivot e utilizzando `CopyOptions` con `PASTE_ALL`, puoi copiare in modo affidabile **copy range to another workbook** preservando ogni funzionalità della pivot.  

Se sei curioso di sapere **how to copy pivot table** in altri linguaggi, gli stessi concetti si applicano—basta sostituire l'SDK Aspose.Cells con la piattaforma appropriata. Successivamente potresti esplorare l'aggiornamento programmatico della tabella pivot copiata, o l'esportazione in PDF per scopi di reporting.  

Hai una variante di questo scenario? Forse devi copiare un grafico collegato a una tabella pivot, o vuoi elaborare in batch decine di file. Questi argomenti sono estensioni naturali di quanto trattato oggi.  

Metti alla prova il codice, modifica l'intervallo e lascia che le tue avventure di automazione Excel abbiano inizio. Buona programmazione!

## What Should You Learn Next?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiornare la fonte della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatizzare lo stile e il salvataggio della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Manipolazione della tabella pivot Excel con Aspose.Cells Java: Guida completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}