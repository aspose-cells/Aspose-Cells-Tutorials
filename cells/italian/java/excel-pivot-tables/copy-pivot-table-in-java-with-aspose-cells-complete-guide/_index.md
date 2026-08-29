---
category: general
date: 2026-07-20
description: Copia una tabella pivot in Java usando Aspose.Cells. Scopri come copiare
  la tabella pivot in un altro file, estrarre l’intervallo della tabella pivot e copiare
  l’intervallo in una nuova cartella di lavoro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy pivot table to another file
- copy range to new workbook
- how to copy pivot table
- extract pivot table range
language: it
lastmod: 2026-07-20
og_description: Copia tabella pivot in Java con Aspose.Cells. Segui questa guida per
  copiare la tabella pivot in un altro file, estrarne l’intervallo e copiare l’intervallo
  in una nuova cartella di lavoro.
og_image_alt: Diagram illustrating how to copy pivot table from one workbook to another
  using Java
og_title: Copia tabella pivot in Java – Tutorial passo‑passo Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  headline: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  type: TechArticle
- description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  name: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  steps:
  - name: Expected Output
    text: '- `CopyWithPivot.xlsx` contains a single worksheet. - The worksheet shows
      the same pivot layout as the source. - All pivot fields, filters, and calculated
      items are intact. - Refreshing the pivot updates totals based on the newly copied
      data.'
  - name: Copying Multiple Pivot Tables
    text: If your source sheet has more than one pivot, repeat the `createRange`/`copy`
      pair for each table, adjusting the address accordingly. You can also loop through
      `sourceWorksheet.getPivotTables()` to automate discovery.
  - name: Preserving Styles and Formatting
    text: The `Range.copy` method copies cell values, formulas, and formatting by
      default. However, if you only need the data without styles, use `sourceRange.copy(destinationRange,
      new CopyOptions());` and tweak the `CopyOptions` flags.
  - name: Working with Large Workbooks
    text: 'For workbooks exceeding a few hundred MB, consider enabling **memory‑efficient
      loading**:'
  - name: Quick Recap
    text: '- Loaded a source workbook containing a pivot table. - Identified the exact
      **extract pivot table range** (`A1:G20`). - Created a fresh workbook and **copied
      range to new workbook**, preserving the pivot. - Saved the result, effectively
      **copying pivot table to another file**.'
  type: HowTo
- questions:
  - answer: Yes. Aspose handles format conversion automatically during `save()`. Just
      specify the desired extension in the output path.
    question: Can I copy a pivot table across different Excel formats (XLSX → XLS)?
  - answer: The copy will overwrite existing cells. To avoid data loss, either clear
      the area first (`destinationSheet.getCells().clearRange("A1:G20")`) or choose
      a different start cell.
    question: What if the destination workbook already contains data in the target
      range?
  - answer: 'The source workbook is opened in read‑write mode by default. If you only
      need to read, pass `LoadOptions` with `setReadOnly(true)`. ## Next Steps & Related
      Topics Now that you know **how to copy pivot table** programmatically, you might
      explore: - **Refreshing pivot caches** after copying (`pivotTab'
    question: Does this work with read‑only source files?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot Table
title: Copia della tabella pivot in Java con Aspose.Cells – Guida completa
url: /it/java/excel-pivot-tables/copy-pivot-table-in-java-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia Tabella Pivot in Java con Aspose.Cells – Guida Completa

Hai mai avuto bisogno di **copiare una tabella pivot** da un file Excel a un altro ma non sapevi da dove cominciare? Non sei solo. In molti flussi di reporting dobbiamo spostare un riepilogo basato su pivot da una cartella di lavoro master a un file leggero per la distribuzione, e farlo manualmente è una seccatura.  

In questo tutorial illustreremo una soluzione pulita e programmatica che ti permette di **copiare la tabella pivot in un altro file**, estrarre il suo intervallo esatto e persino **copiare l'intervallo in una nuova cartella di lavoro** in un unico passaggio. Alla fine avrai uno snippet riutilizzabile che funziona con qualsiasi progetto Java abilitato a Aspose.Cells.

## Cosa Copre Questa Guida

- Caricamento di una cartella di lavoro sorgente che contiene già una tabella pivot  
- Determinazione dell'esatto **intervallo da estrarre della tabella pivot** necessario  
- Creazione di una nuova cartella di lavoro e incollaggio dell'intervallo preservando la logica della pivot  
- Salvataggio del risultato come nuovo file, pronto per l'elaborazione successiva  

Nessuno strumento esterno, nessuna acrobazia con macro—solo puro codice Java e una manciata di chiamate a Aspose.Cells. Se hai già lavorato con Excel, i concetti ti saranno familiari; se sei nuovo a Aspose, la libreria astrae la gestione XML a basso livello, permettendoti di concentrarti sulla logica di business.

> **Prerequisiti**  
> - Java 8 or newer  
> - Aspose.Cells for Java (latest version as of July 2026)  
> - Basic familiarity with Excel pivot tables  

Ora, immergiamoci.

## Passo 1: Configura il tuo progetto e importa Aspose.Cells

Prima di toccare qualsiasi cartella di lavoro, assicurati che il JAR di Aspose.Cells sia nel tuo classpath. Se usi Maven, aggiungi la dipendenza:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of 2026 -->
</dependency>
```

Se preferisci una configurazione manuale, inserisci `aspose-cells-24.10.jar` nella tua cartella `libs` e riferiscilo nel tuo IDE.

> **Suggerimento Pro:** Mantieni la versione della libreria allineata con il tuo runtime Java per evitare `UnsupportedClassVersionError`.

## Passo 2: Carica la cartella di lavoro sorgente contenente la tabella pivot

La prima cosa di cui abbiamo bisogno è un oggetto `Workbook` che punti al file dove risiede la pivot. È qui che inizia l'operazione di **copia della tabella pivot**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that already has the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Perché lo carichiamo in questo modo? Aspose legge l'intero file in memoria, fornendoci pieno accesso ai fogli di lavoro, alle celle e alla cache della pivot sottostante. Ciò garantisce che la definizione della pivot (campi, filtri, origine dati) rimanga intatta quando la copieremo in seguito.

## Passo 3: Identifica l'intervallo esatto che contiene la tabella pivot

Una tabella pivot non è solo un blocco di celle; è supportata da una cache nascosta. Tuttavia, quando copi l'intervallo visivo, Aspose trasporta automaticamente la cache. Per sicurezza, definiremo l'intervallo esplicitamente—questo è il passo **estrazione dell'intervallo della tabella pivot**.

```java
        // Define the range covering the pivot table (adjust as needed)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                // first worksheet
                                          .getCells()
                                          .createRange("A1:G20"); // typical size; change if larger
```

Se non sei sicuro delle dimensioni, puoi individuare programmaticamente la tabella pivot usando `Worksheet.getPivotTables()`. Per brevità assumiamo un rettangolo noto, ma la stessa logica funziona per la scoperta dinamica.

## Passo 4: Crea una nuova cartella di lavoro per ricevere l'intervallo copiato

Ora creiamo una nuova cartella di lavoro che diventerà il file di destinazione. È qui che avviene **copia dell'intervallo in una nuova cartella di lavoro**.

```java
        // Create an empty workbook that will receive the copy
        Workbook destinationWorkbook = new Workbook(); // starts with a default sheet
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Perché una cartella di lavoro completamente nuova? Partire da zero garantisce che nessuna formattazione errante o foglio nascosto interferisca con i riferimenti interni della pivot. Se devi unire in un file esistente, carica semplicemente quel file invece di `new Workbook()`.

## Passo 5: Esegui la copia – la tabella pivot è preservata

Ecco il cuore del tutorial: copiare l'intervallo mantenendo la pivot funzionale. Il metodo `Range.copy` di Aspose fa il lavoro pesante.

```java
        // Copy the source range (including the pivot) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Quando questa riga viene eseguita, Aspose clona le celle visive **e** clona la cache della pivot sottostante nella nuova cartella di lavoro. Il risultato è una tabella pivot pienamente operativa che puoi aggiornare, filtrare o esportare proprio come l'originale.

> **Domanda comune:** *Cosa succede se la destinazione ha già una pivot con lo stesso nome?*  
> Aspose rinomina automaticamente la pivot copiata per evitare collisioni (ad esempio, “PivotTable1_1”).

## Passo 6: Salva la cartella di lavoro di destinazione

Infine, salviamo il nuovo file. Questo è il passo che effettivamente **copia la tabella pivot in un altro file** su disco.

```java
        // Save the workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

Dopo aver eseguito il programma, apri `CopyWithPivot.xlsx` in Excel. Vedrai lo stesso layout della pivot, i filtri e l'origine dati (che ora punta all'intervallo copiato). Aggiornare la pivot ricalcolerà i totali in base al nuovo blocco di dati.

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco la classe completa, pronta per l'esecuzione:

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Define the range that includes the pivot table (e.g., A1:G20)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:G20");

        // 3️⃣ Create a new workbook to receive the copied range
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range to the destination worksheet; the pivot table is preserved
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Output Atteso

- `CopyWithPivot.xlsx` contiene un unico foglio di lavoro.  
- Il foglio di lavoro mostra lo stesso layout della pivot della sorgente.  
- Tutti i campi, i filtri e gli elementi calcolati della pivot sono intatti.  
- Aggiornare la pivot aggiorna i totali basati sui dati appena copiati.

## Gestione di Casi Limite e Varianti

### Copiare più tabelle pivot

Se il tuo foglio sorgente ha più di una pivot, ripeti la coppia `createRange`/`copy` per ogni tabella, adeguando l'indirizzo di conseguenza. Puoi anche iterare su `sourceWorksheet.getPivotTables()` per automatizzare la scoperta.

### Preservare Stili e Formattazione

Il metodo `Range.copy` copia per impostazione predefinita i valori delle celle, le formule e la formattazione. Tuttavia, se ti servono solo i dati senza stili, usa `sourceRange.copy(destinationRange, new CopyOptions());` e modifica i flag di `CopyOptions`.

### Lavorare con Cartelle di Lavoro di grandi dimensioni

Per cartelle di lavoro che superano qualche centinaio di MB, considera l'abilitazione del **caricamento a basso consumo di memoria**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook sourceWorkbook = new Workbook("bigfile.xlsx", loadOptions);
```

Ciò riduce il consumo di heap mantenendo comunque la possibilità di copiare gli intervalli.

## Domande Frequenti

**Q: Posso copiare una tabella pivot tra diversi formati Excel (XLSX → XLS)?**  
A: Sì. Aspose gestisce automaticamente la conversione del formato durante `save()`. Basta specificare l'estensione desiderata nel percorso di output.

**Q: Cosa succede se la cartella di lavoro di destinazione contiene già dati nell'intervallo target?**  
A: La copia sovrascriverà le celle esistenti. Per evitare perdite di dati, cancella prima l'area (`destinationSheet.getCells().clearRange("A1:G20")`) o scegli una cella di partenza diversa.

**Q: Funziona con file sorgente in sola lettura?**  
A: La cartella di lavoro sorgente è aperta in modalità lettura‑scrittura per impostazione predefinita. Se hai solo bisogno di leggere, passa `LoadOptions` con `setReadOnly(true)`.

## Prossimi Passi e Argomenti Correlati

Ora che sai **come copiare una tabella pivot** programmaticamente, potresti esplorare:

- **Aggiornare le cache della pivot** dopo la copia (`pivotTable.refresh();`)  
- **Esportare i dati della pivot in CSV** per analisi successive  
- **Aggiungere slicer programmaticamente** alla pivot copiata (`PivotTable.addSlicer(...)`)  
- **Copiare grafici collegati a tabelle pivot** usando `Chart.copy()`  

Each of these builds on the foundation we just laid, letting you build end‑to‑end Excel automation pipelines in Java.

---

### Riepilogo Rapido

- Caricata una cartella di lavoro sorgente contenente una tabella pivot.  
- Identificato l'esatto **intervallo da estrarre della tabella pivot** (`A1:G20`).  
- Creata una nuova cartella di lavoro e **copiato l'intervallo in una nuova cartella di lavoro**, preservando la pivot.  
- Salvato il risultato, copiando efficacemente la **tabella pivot in un altro file**.  

Provalo con i tuoi file, modifica l'intervallo e guarda la pivot migrare senza problemi. Se incontri difficoltà, lascia un commento qui sotto—buona programmazione!

![Copy pivot table diagram showing source and destination workbooks](https://example.com/images/copy-pivot-table-diagram.png)


## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiornare l'origine della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Ottimizzare il caricamento della tabella pivot in Java usando Aspose.Cells: Guida completa](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Manipolazione della tabella pivot Excel con Aspose.Cells Java: Guida completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}