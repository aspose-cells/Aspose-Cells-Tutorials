---
category: general
date: 2026-07-23
description: Crea una nuova cartella di lavoro in Java e impara come copiare una tabella
  pivot, copiare un intervallo Excel e esportare la tabella pivot con Aspose.Cells
  in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: it
lastmod: 2026-07-23
og_description: Crea una nuova cartella di lavoro in Java e copia istantaneamente
  la tabella pivot, copia l’intervallo Excel, quindi esporta la tabella pivot usando
  Aspose.Cells. Segui questo tutorial completo.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Crea una nuova cartella di lavoro in Java – Copia la tabella pivot passo
  passo
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Crea una nuova cartella di lavoro in Java – Guida completa per copiare la tabella
  pivot
url: /it/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un nuovo Workbook in Java – Guida completa per copiare la tabella pivot

Ti sei mai chiesto come **create new workbook** in Java mantenendo intatta una tabella pivot complessa? Non sei l'unico a grattarsi la testa per questo. In molte applicazioni di reporting è necessario spostare una pivot da un file di origine a un nuovo workbook, magari per inviarla a un cliente o per eseguire ulteriori calcoli. La buona notizia? Con poche righe di codice puoi fare esattamente questo—senza dover copiare e incollare manualmente.

In questo tutorial percorreremo l'intero processo: caricare il file di origine, definire l'intervallo che contiene la pivot, **copying the Excel range**, creare un **new workbook**, e infine **exporting the pivot table** in un nuovo file. Alla fine avrai un programma Java autonomo e eseguibile che risponde alla domanda “**how to copy pivot**” senza alcuna congettura.

## Prerequisiti

- Java 17 o successivo (il codice funziona con qualsiasi JDK recente)
- Libreria Aspose.Cells per Java (versione di prova gratuita o licenziata)
- Un file di esempio `source.xlsx` che contiene una tabella pivot nell'intervallo `A1:G20`
- Un IDE o uno strumento di build (Maven/Gradle) per gestire il JAR di Aspose.Cells

Li hai? Ottimo—iniziamo.

## Passo 1: Configura il progetto e importa Aspose.Cells

Prima di tutto, devi aggiungere Aspose.Cells al tuo progetto. Se usi Maven, inserisci questa dipendenza nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Se preferisci Gradle, l'equivalente è:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Una volta che la libreria è nel classpath, importa le classi di cui avrai bisogno:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Consiglio professionale:** Aspose.Cells è una libreria commerciale, ma offre una valutazione completa di 30 giorni che aggiunge una filigrana all'output—perfetta per provare.

## Passo 2: Carica il Workbook di origine

Ora **create new workbook** oggetti, ma prima abbiamo bisogno della sorgente che contiene la pivot. Questo passo è la base per qualsiasi operazione **copy excel range** perché l'oggetto range conosce esattamente quali celle (inclusa la cache della pivot) trasferire.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Perché non leggere direttamente il range? Perché i metadati della tabella pivot risiedono nella cache pivot del foglio di lavoro, e Aspose.Cells li raggruppa automaticamente quando copi il range.

## Passo 3: Definisci il range che contiene la tabella pivot

In molti file reali la pivot occupa un blocco rettangolare. Per questo esempio assumiamo che si trovi in `A1:G20`. Puoi, naturalmente, regolare l'indirizzo per adattarlo al tuo layout reale.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Se non sei sicuro dell'indirizzo esatto, puoi usare `sourceSheet.getCells().getMaxDataRow()` e `getMaxDataColumn()` per calcolare dinamicamente i limiti. È un trucco utile quando le dimensioni della pivot cambiano nel tempo.

## Passo 4: **Create New Workbook** e foglio di destinazione

Ecco il momento in cui effettivamente **create new workbook** che riceverà il contenuto copiato. Pensalo come una tela vuota su cui incollerai la pivot.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Perché iniziare con un workbook vuoto? Garantisce che nessuno stile nascosto o pivot precedente interferisca con la copia, fornendoti un risultato pulito pronto per **export pivot table**.

## Passo 5: Copia la tabella pivot (e il suo range sottostante)

Ora il cuore del tutorial: **copy pivot table**. Aspose.Cells tratta la copia di un range come una copia profonda, il che significa che la cache della pivot viaggia con le celle. Ecco perché questa singola riga fa il lavoro pesante.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Se ti sei mai chiesto **how to copy pivot** senza perdere la sua funzionalità, questa è la risposta. Il foglio di destinazione ora contiene una pivot completamente funzionante che puoi aggiornare, modificare o semplicemente esportare.

### Caso limite: preservare le impostazioni di aggiornamento

A volte la pivot di origine è impostata per aggiornarsi all'apertura. Per mantenere quel comportamento, puoi copiare esplicitamente le opzioni della pivot:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Questa porzione di codice garantisce che la pivot copiata si comporti esattamente come l'originale.

## Passo 6: Salva il Workbook di destinazione – **Export Pivot Table**

Infine, **export pivot table** salvando il nuovo workbook su disco. Puoi scegliere qualsiasi formato supportato da Aspose: XLSX, XLS, CSV, PDF, ecc. Per questa guida useremo XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Se devi inviare il file tramite un servizio web, puoi scriverlo in un `ByteArrayOutputStream` invece di un percorso file—Aspose rende questo banale.

## Esempio completo funzionante

Mettendo tutto insieme, ecco un programma completo, pronto per l'esecuzione. Sentiti libero di copiare, incollare ed eseguirlo nel tuo IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Output previsto

Quando esegui il programma, la console stampa:

```
Pivot table copied successfully!
```

E il file `copied_with_pivot.xlsx` appare in `YOUR_DIRECTORY`. Aprilo in Excel e vedrai la tabella pivot intatta, pronta per essere aggiornata o modificata.

## Domande comuni e risoluzione dei problemi

- **What if the source pivot spans more than one worksheet?**  
  Se la pivot di origine si estende su più di un foglio di lavoro, dovrai copiare ogni range rilevante separatamente, quindi ricreare la pivot sul foglio di destinazione usando le API `PivotTable`.

- **Can I copy only the pivot layout without the data?**  
  Imposta `sourceRange.setCopyDataOnly(false)` prima della copia. Questo dice ad Aspose di mantenere la cache ma non i dati sottostanti.

- **Is there a way to copy the pivot to a CSV file?**  
  Il CSV non supporta le pivot, ma puoi esportare il *risultato* della pivot chiamando `pivotTable.calculate()` e poi salvando il foglio come CSV.

- **Why does the copied pivot lose its formatting?**  
  La formattazione vive nella collezione di stili. Dopo la copia, puoi chiamare `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` per trasferire gli stili.

## Conclusione

Ti abbiamo appena mostrato come **create new workbook** in Java, **copy pivot table**, e **export pivot table**—tutto con un esempio di codice pulito e riproducibile. Definendo l'esatto **copy excel range**, sfruttando le semantiche di deep‑copy di Aspose.Cells e preservando le impostazioni opzionali, puoi automatizzare praticamente qualsiasi operazione di migrazione di pivot.

Pronto per il passo successivo? Prova a cambiare il formato di output in PDF, o a iterare su più file di origine per elaborare in batch decine di pivot. Lo stesso schema si applica—basta regolare i percorsi dei file e gli indirizzi dei range.

Se incontri un problema, lascia un commento qui sotto o consulta la documentazione di Aspose.Cells per la manipolazione avanzata delle pivot. Buon coding, e goditi il tempo risparmiato automatizzando quelle noiose operazioni di copia‑incolla!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare tabelle pivot in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Come aggiornare l'origine della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java | Guida alle operazioni del Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}