---
category: general
date: 2026-06-21
description: Copia programmaticamente un intervallo di foglio di lavoro in Java usando
  Aspose.Cells. Scopri come copiare un intervallo Excel in un altro workbook in modo
  efficiente.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: it
og_description: Copia programmaticamente l’intervallo di un foglio di lavoro in Java.
  Questa guida mostra come copiare un intervallo di Excel in un’altra cartella di
  lavoro con codice completo e suggerimenti.
og_title: Copia programmaticamente l’intervallo del foglio di lavoro – Java passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Copia programmatica dell’intervallo di foglio di lavoro – Guida completa a
  Java
url: /it/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia programmatica di un intervallo di foglio di lavoro – Guida completa Java

Ti sei mai chiesto come **copiare programmaticamente un intervallo di foglio di lavoro** senza aprire Excel manualmente? Non sei il solo. Che tu debba duplicare un report, clonare una dashboard basata su pivot o semplicemente spostare dati tra file, farlo via codice fa risparmiare tempo ed elimina gli errori umani.

In questo tutorial percorreremo una soluzione pulita, end‑to‑end, che mostra **come copiare un intervallo Excel in un altro workbook** usando Java e la libreria Aspose.Cells. Alla fine avrai un programma pronto all'uso, comprenderai il perché di ogni passaggio e conoscerai le insidie da tenere d'occhio.

---

## Cosa ti serve

- **Java Development Kit (JDK) 11+** – il codice si compila con qualsiasi JDK recente.  
- **Aspose.Cells for Java** (versione di prova gratuita o licenziata). Aggiungi la dipendenza Maven o scarica il JAR.  
- Due file Excel: un `input.xlsx` che contiene l'intervallo sorgente (inclusa una tabella pivot) e un `output.xlsx` vuoto dove l'intervallo verrà incollato.  
- Qualsiasi IDE ti piaccia – IntelliJ IDEA, Eclipse o anche un semplice editor di testo.

Tutto qui. Nessun servizio aggiuntivo, nessun COM interop, solo puro Java.

---

![Diagram illustrating programmatically copy worksheet range between two workbooks](image.png)

*Testo alternativo immagine: illustrazione della copia programmatica di un intervallo di foglio di lavoro*

---

## Passo 1: Configura il progetto e importa Aspose.Cells

Prima di tutto, dobbiamo avere la libreria nel classpath. Se usi Maven, aggiungi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Se preferisci un JAR manuale, copialo nella cartella `libs` e aggiungilo al percorso di compilazione.

Perché è importante: Aspose.Cells fornisce un modello di oggetti ricco (`Workbook`, `Worksheet`, `Range`) che consente di copiare dati **inclusi tabelle pivot, formule e formattazione** con una singola chiamata—qualcosa che la libreria Apache POI non riesce a fare altrettanto pulito.

---

## Passo 2: Carica il workbook sorgente

Apriremo il workbook che contiene i dati da clonare. Il costruttore `Workbook` accetta un percorso file, e Aspose leggerà l'intero file in memoria.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Consiglio professionale:* avvolgi il caricamento in un blocco try‑catch se il file potrebbe mancare; altrimenti il programma terminerà con un errore chiaro.

---

## Passo 3: Crea un workbook di destinazione vuoto

Un workbook nuovo ci offre una tela pulita. Non è necessario pre‑popolare fogli; Aspose ne aggiungerà uno per noi.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Perché non riutilizzare il sorgente? Tenerli separati evita sovrascritture accidentali e rende il codice riutilizzabile per operazioni batch.

---

## Passo 4: Definisci l'intervallo esatto da copiare

Qui inizia la magia della **copia programmatica di un intervallo di foglio di lavoro**. Selezioniamo le celle `A1:D20` dal primo foglio del file sorgente. Il metodo `createRange` restituisce un oggetto `Range` che rappresenta esattamente quelle celle, tabelle pivot incluse.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Se ti serve un intervallo dinamico (ad es. “ultima riga usata”), puoi sostituire l'indirizzo hard‑coded con `Cells.maxDisplayRange` o calcolarlo con `Cells.getMaxDataColumn()` e `Cells.getMaxDataRow()`.

---

## Passo 5: Aggiungi un foglio di destinazione nel workbook

Aspose crea un foglio predefinito chiamato “Sheet1” quando istanzi `Workbook`. Aggiungeremo un nuovo foglio per mantenere le cose ordinate, specialmente se prevedi di copiare più intervalli in seguito.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Puoi assegnare al foglio un nome più descrittivo:

```java
        targetWorksheet.setName("CopiedData");
```

---

## Passo 6: Esegui la copia – incluse le tabelle pivot

Ora l'operazione centrale: `copyRange`. Questo metodo copia **valori, formule, formattazione e oggetti incorporati** (come le tabelle pivot) dall'intervallo sorgente a una cella di destinazione (`A1` nel nostro nuovo foglio). È il modo più semplice per realizzare **come copiare un intervallo Excel in un altro workbook** senza dover gestire cicli di celle a basso livello.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Dietro le quinte Aspose serializza l'intervallo sorgente in un formato intermedio, poi lo deserializza nel foglio di destinazione—così tutto rimane intatto.

---

## Passo 7: Salva il workbook di destinazione e verifica

Infine, scriviamo il workbook di destinazione su disco. Apri `output.xlsx` in Excel per vedere l'intervallo copiato, la tabella pivot e tutta la formattazione preservata.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

Quando apri `output.xlsx`, dovresti vedere un foglio chiamato “CopiedData” con lo stesso layout di `A1:D20` del sorgente, inclusa la tabella pivot che ora punta ai dati copiati.

---

## Gestione dei casi d'uso più comuni

### 1. Copia tra versioni diverse di Excel
Aspose.Cells funziona con `.xls`, `.xlsx`, `.xlsb` e anche `.csv`. Se sorgente e destinazione usano formati diversi, la libreria li converte automaticamente. Basta assicurarsi che le estensioni dei file corrispondano al risultato desiderato.

### 2. Conservare le fonti dati esterne nelle tabelle pivot
Se la tabella pivot nel sorgente fa riferimento a una fonte dati esterna (ad es. una connessione a database), la copia manterrà la stringa di connessione ma **non si aggiornerà automaticamente**. Chiama `pivotTable.refreshData()` dopo la copia se ti servono risultati aggiornati.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Intervalli molto grandi e consumo di memoria
Copiare intervalli enormi (centinaia di migliaia di righe) può aumentare l'uso di memoria. Usa `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` prima di caricare file di grandi dimensioni per ridurre l'impronta.

### 4. Più fogli o intervalli
Se devi copiare diversi intervalli non contigui, ripeti i passi 4‑6 per ciascun intervallo, oppure usa `copyRange` con un intervallo unito (`Cells.createRange("A1:B10,C1:D10")`).

---

## Consigli professionali per un'automazione robusta

- **Valida l'intervallo sorgente** prima di copiare. Usa `sourceRange.isValid()` per evitare errori a runtime.  
- **Sblocca il file di destinazione** con `FileInfo.setReadOnly(false)` se stai sovrascrivendo un workbook esistente.  
- **Registra le azioni** con un logger leggero (SLF4J) – particolarmente utile quando si elaborano batch.  
- **Rilascia i workbook** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) in servizi a lunga esecuzione per liberare risorse native.

---

## Riepilogo dell'esempio completo

Di seguito trovi la classe Java completa, autonoma, che puoi incollare nel tuo IDE e farla girare. Ricorda di sostituire `YOUR_DIRECTORY` con il percorso reale sul tuo computer.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Output atteso:** Un file `output.xlsx` con un foglio chiamato “CopiedData”. Le celle `A1:D20` rispecchieranno il sorgente, e qualsiasi tabella pivot all'interno di quel blocco sarà pienamente funzionante, puntando ai dati copiati.

---

## Conclusione

Abbiamo appena dimostrato una soluzione pulita per **copiare programmaticamente un intervallo di foglio di lavoro** in Java, rispondendo alla domanda comune **come copiare un intervallo Excel in un altro workbook**. Sfruttando l'API di alto livello di Aspose.Cells abbiamo evitato cicli di celle a basso livello, preservato le tabelle pivot e mantenuto il codice leggibile.

Qual è il prossimo passo? Prova a estendere questo schema per:

- Copiare interi fogli invece di un singolo intervallo.  
- Elaborare in batch decine di workbook in una cartella.  
- Esportare l'intervallo copiato in CSV o PDF per pipeline di reporting.

Sentiti libero di sperimentare e, se incontri difficoltà, lascia un commento. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Come copiare più colonne in Excel usando Aspose.Cells Java: Guida completa](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copiare colonne Excel in modo efficiente usando Aspose.Cells per Java: Guida completa](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Copiare immagini tra fogli in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}