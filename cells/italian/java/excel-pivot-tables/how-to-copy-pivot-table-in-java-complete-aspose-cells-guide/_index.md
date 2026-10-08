---
category: general
date: 2026-06-08
description: Come copiare una tabella pivot usando Aspose.Cells in Java. Impara a
  copiare l’intervallo tra cartelle di lavoro e a preservare le tabelle pivot senza
  sforzo.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: it
og_description: Come copiare una tabella pivot in Java con Aspose.Cells. Questo tutorial
  mostra come copiare un intervallo tra cartelle di lavoro mantenendo intatta la pivot.
og_title: Come copiare una tabella pivot in Java – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: Come copiare una tabella pivot in Java – Guida completa ad Aspose.Cells
url: /it/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Copiare una Tabella Pivot in Java – Guida Completa a Aspose.Cells

Ti sei mai chiesto **come copiare una tabella pivot** da una cartella di lavoro Excel a un'altra usando Java? La buona notizia è che Aspose.Cells rende semplice **copiare intervalli tra cartelle di lavoro** preservando ogni dettaglio della pivot.  

In questo tutorial percorreremo un esempio reale che non solo copia la pivot stessa, ma mantiene intatti i dati sottostanti, la formattazione e le formule. Alla fine saprai esattamente **come preservare le strutture della pivot**, come spostare una pivot in una cartella di lavoro nuova di zecca e come evitare le insidie comuni che ostacolano molti sviluppatori.

Copriamo:

* I prerequisiti minimi (Java 17+, Aspose.Cells for Java 23.9+).  
* Una suddivisione passo‑per‑passo del codice, con spiegazioni del **perché** di ogni riga.  
* Gestione dei casi limite per intervalli pivot di grandi dimensioni e sorgenti dati esterne.  
* Un programma completo, eseguibile, che puoi inserire nel tuo IDE e far girare subito.

> **Pro tip:** Se usi già Maven o Gradle, aggiungere Aspose.Cells come dipendenza è una singola riga—nessuna gestione manuale di JAR necessaria.

---

## Come Copiare una Tabella Pivot – Panoramica Passo‑per‑Passo

Di seguito una vista ad alto livello di ciò che realizzeremo:

1. Caricare la cartella di lavoro di origine che contiene la tabella pivot.  
2. Identificare l’intervallo di celle esatto che racchiude la pivot.  
3. Creare una nuova cartella di lavoro di destinazione.  
4. **Copiare l’intervallo** nel nuovo foglio, lasciando che Aspose.Cells preservi automaticamente la pivot.  
5. Salvare il risultato come nuovo file.

Ogni passo è illustrato con snippet di codice e una breve motivazione, così comprenderai la meccanica—non solo la meccanica.

![Diagramma che illustra come una tabella pivot viene copiata da una cartella di lavoro di origine a una cartella di lavoro di destinazione preservandone la struttura](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="diagramma come copiare tabella pivot"}

---

### Passo 1: Configurare Aspose.Cells nel tuo progetto

Prima di poter manipolare file Excel, devi avere la libreria Aspose.Cells nel classpath. Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

Per Gradle, è altrettanto una riga unica:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*Perché è importante:* Aspose.Cells astrae i dettagli low‑level di OpenXML, fornendoti un’API semplice per **copiare la tabella pivot in una nuova cartella di lavoro** senza perdere alcun metadato.

---

### Passo 2: Caricare la Cartella di Lavoro di Origine

Abbiamo bisogno di un’istanza `Workbook` che punti al file che contiene la pivot. Sostituisci `YOUR_DIRECTORY/src.xlsx` con il percorso reale sulla tua macchina.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Nota:** Aspose.Cells rileva automaticamente il formato del file (XLSX, XLS, CSV, ecc.), quindi non devi preoccuparti della conversione di formato.

---

### Passo 3: Definire l’Intervallo Che Racchiude la Pivot

Una tabella pivot vive all’interno di un blocco rettangolare di celle. Puoi individuarla manualmente (es. `A1:G20`) o programmaticamente ispezionando la collezione `PivotTables` del foglio di lavoro. Per questo tutorial codificheremo l’intervallo in modo statico per chiarezza.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*Perché usiamo `createRange`*: crea un oggetto `Range` leggero che può essere passato a `copyRange`. Questo è il modo più affidabile per **copiare intervalli tra cartelle di lavoro** assicurando che le strutture interne della pivot siano incluse.

---

### Passo 4: Creare una Cartella di Lavoro di Destinazione Vuota

Ora avviamo una cartella di lavoro vuota che riceverà i dati copiati.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Il workbook predefinito contiene già un foglio di lavoro, perfetto per il nostro scopo. Se ti serve un nome di foglio specifico, puoi rinominarlo:

```java
destinationSheet.setName("PivotCopy");
```

---

### Passo 5: Copiare l’Intervallo e Preservare la Pivot

Ecco dove avviene la magia. Il metodo `copyRange` accetta un oggetto `CopyOptions`, ma non è necessario modificarlo—la preservazione della pivot è attiva di default.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*Perché funziona:* Aspose.Cells tratta la pivot come parte della collezione di celle. Quando invochi `copyRange`, replica la cache della pivot sottostante, i campi dati e il layout, realizzando **come preservare la pivot** senza codice aggiuntivo.

---

### Passo 6: Salvare la Cartella di Lavoro di Destinazione

Infine, scrivi il nuovo file su disco.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Apri il file risultante `copied-with-pivot.xlsx` in Excel e vedrai una replica esatta della pivot originale, pronta per ulteriori analisi.

---

## Esempio Completo Funzionante

Di seguito il programma completo che puoi compilare ed eseguire direttamente. Unisce tutti gli snippet sopra, aggiunge alcuni controlli difensivi e stampa un messaggio di conferma amichevole.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Output previsto quando esegui il programma**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Apri il file di destinazione—la tua pivot dovrebbe apparire identica all’originale, completa di slicer, filtri e campi calcolati.

---

## Gestione dei casi edge comuni

| Situazione | Cosa Controllare | Correzione Suggerita |
|------------|------------------|----------------------|
| **La pivot utilizza una sorgente dati esterna** (es. un database) | La connessione esterna non è incorporata nella cartella di lavoro, quindi la copia potrebbe rompere il collegamento. | Esporta i dati in un foglio prima, quindi crea una pivot su quel foglio prima di copiarla. |
| **Pivot molto grande (migliaia di righe)** | `copyRange` può consumare molta memoria. | Aumenta l’heap JVM (`-Xmx2g`) o copia la pivot in blocchi più piccoli usando `copyRows`/`copyColumns`. |
| **Più pivot nello stesso foglio** | Codificare manualmente `A1:G20` copia solo la prima pivot. | Itera su `sourceWorksheet.getPivotTables()` e copia ogni `PivotTable.getDataRange()`. |
| **La cartella di lavoro di destinazione contiene già un foglio con lo stesso nome** | `setName` lancerà un’eccezione. | Usa `Workbook.getWorksheets().add("PivotCopy")` per creare un foglio con nome univoco. |

Questi consigli assicurano che **come copiare una tabella pivot** funzioni in modo affidabile, anche in scenari di produzione.

---

## Domande Frequenti

**D: Questo metodo copia anche la formattazione della pivot?**  
R: Sì. Poiché copiamo l’intero intervallo di celle, stili, formattazione condizionale e formati numerici viaggiano insieme ai dati.

**D: E se devo copiare la pivot in una cella specifica diversa da `A1`?**  
R: Basta cambiare il terzo argomento di `copyRange` con l’indirizzo in alto‑a‑sinistra desiderato, ad esempio `"B5"`.

**D: Posso copiare una pivot senza i dati di origine?**  
R: Non direttamente. La cache della pivot vive all’interno della cartella di lavoro; rimuovere i dati di origine renderebbe la pivot inutilizzabile. Esporta i dati di origine in un foglio nascosto se desideri una copia più leggera.

---

## Conclusione

Ora hai una risposta chiara, end‑to‑end, a **come copiare una tabella pivot** in Java usando Aspose.Cells. Caricando la cartella di lavoro di origine, definendo l’intervallo della pivot e sfruttando `copyRange`, puoi facilmente **copiare intervalli tra cartelle di lavoro** garantendo che la pivot rimanga

---

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑per‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}