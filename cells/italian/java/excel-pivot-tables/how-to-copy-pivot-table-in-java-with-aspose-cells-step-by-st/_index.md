---
category: general
date: 2026-10-20
description: Scopri come copiare una tabella pivot usando Aspose.Cells in Java. Questo
  tutorial mostra come copiare un intervallo in un nuovo foglio e duplicare in modo
  sicuro il foglio della tabella pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: it
lastmod: 2026-10-20
og_description: Come copiare una tabella pivot con Aspose.Cells in Java. Segui questa
  guida per copiare l'intervallo in un nuovo foglio e duplicare il foglio della tabella
  pivot senza perdere dati.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Come copiare una tabella pivot in Java – tutorial completo di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come copiare una tabella pivot in Java con Aspose.Cells – guida passo passo
url: /it/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in Java con Aspose.Cells – guida passo‑passo

Se hai bisogno di **come copiare una tabella pivot** in un'applicazione Java, questa guida ti accompagna passo passo. Che tu stia costruendo un motore di reporting o automatizzando la migrazione dei dati, vedrai come copiare un intervallo in un nuovo foglio mantenendo intatta la definizione e i dati della tabella pivot.

Copiare una tabella pivot può sembrare rischioso perché la cache sottostante e le impostazioni dei campi spesso vanno perse. Questo tutorial dimostra un approccio affidabile usando Aspose.Cells, mostra il codice completo eseguibile e spiega perché ogni riga è importante. Alla fine, sarai in grado di duplicare il foglio della tabella pivot in pochi secondi.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java 8 o versioni successive installate.  
* Aspose.Cells per Java (versione 23.10 o successiva) aggiunto al classpath del tuo progetto.  
* Un workbook di origine (`source.xlsx`) che contiene una tabella pivot nell'intervallo `A1:G20`.  
* Familiarità di base con Java e i concetti di Excel.

Non sono richieste librerie aggiuntive; Aspose.Cells gestisce tutte le operazioni di Excel internamente.

## Come copiare una tabella pivot – strategia generale

L'idea di base è semplice:

1. Carica il workbook che contiene la tabella pivot originale.  
2. Identifica l'intervallo esatto che include la tabella pivot.  
3. Crea un nuovo foglio di lavoro che riceverà i dati copiati.  
4. Usa il metodo `Range.copy` per trasferire l'intervallo nel nuovo foglio.  
   Questo metodo copia automaticamente la cache della pivot, quindi la tabella pivot rimane funzionale.  
5. Salva il workbook in un nuovo file.

Poiché l'operazione di copia avviene a livello di intervallo, il **foglio della tabella pivot duplicato** conserva tutte le configurazioni dei campi, i filtri e gli elementi calcolati.

## Passo 1: Carica il workbook di origine

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Perché è importante*: Caricare il workbook ti dà accesso ai suoi fogli, celle e alla cache della pivot. Aspose.Cells legge l'intero file in memoria, così le operazioni successive sono rapide e thread‑safe.

## Passo 2: Definisci l'intervallo di origine che contiene la tabella pivot

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Perché è importante*: La chiamata `createRange` indica ad Aspose.Cells esattamente quali celle copiare. Includere l'intera area della tabella pivot assicura che anche le righe nascoste della cache vengano trasferite. Se ometti una parte della cache, la tabella pivot copiata apparirà vuota.

## Passo 3: Aggiungi un foglio di destinazione per i dati copiati

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Perché è importante*: Aggiungere un foglio dedicato isola la tabella pivot copiata dall'originale, rendendo più semplice confrontare i risultati o usare il foglio come modello per ulteriori elaborazioni.

## Passo 4: Copia l'intervallo nel foglio di destinazione (la tabella pivot è preservata)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Perché è importante*: Il metodo `copy` non solo copia i valori e la formattazione delle celle, ma replica anche la cache della pivot. Questo è il passaggio chiave che ti consente di **duplicare il foglio della tabella pivot** senza perdere alcuna funzionalità.

## Passo 5: Salva il workbook con l'intervallo copiato

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Perché è importante*: Il salvataggio crea un nuovo file Excel (`result.xlsx`) che contiene sia l'originale sia il foglio della tabella pivot duplicato. Ora puoi aprire il file in Excel per verificare che la tabella pivot funzioni esattamente come prima.

## Esempio completo, eseguibile

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare nel tuo IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Output previsto

* Aprendo `result.xlsx` si vedono due fogli di lavoro:  
  * **Sheet1** – i dati originali e la tabella pivot.  
  * **CopyResult** – una copia esatta della tabella pivot, pienamente funzionale.  
* Tutti i campi pivot, i filtri e gli elementi calcolati si comportano identicamente alla sorgente.

Se modifichi la tabella pivot di origine dopo la copia, il foglio duplicato **non** rifletterà tali modifiche perché la cache è stata duplicata al momento della copia. Questa isolazione è spesso desiderabile quando ti serve uno snapshot del report.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| **La tabella pivot appare vuota** | L'intervallo copiato ha omesso le righe nascoste della cache. | Assicurati che l'intervallo includa l'intera cache (di solito qualche riga sotto la tabella visibile). |
| **Il nome del foglio di destinazione esiste già** | `add("CopyResult")` genera un'eccezione se il nome è già occupato. | Usa `workbook.getWorksheets().addUniqueName("CopyResult")` o verifica `contains` prima di aggiungere. |
| **Errori di percorso file** | Un `YOUR_DIRECTORY` errato porta a `FileNotFoundException`. | Usa percorsi assoluti o `Paths.get(...).toAbsolutePath()` di Java per risolvere le posizioni. |
| **Rallentamento delle prestazioni su workbook grandi** | Copiare intervalli massivi trasferisce celle non necessarie. | Limita l'intervallo all'area esatta della pivot, oppure usa `Range.copy` con `CopyOptions` per saltare la formattazione se non necessaria. |

## Consiglio esperto: usare `CopyOptions` per un controllo più fine

Se ti serve solo i dati della tabella pivot e vuoi saltare la formattazione delle celle, puoi passare un oggetto `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Questo riduce la dimensione del file del foglio duplicato e velocizza l'operazione di copia, specialmente per workbook di grandi dimensioni.

## Come copiare un intervallo in un nuovo foglio senza perdere le formule

L'esempio sopra copia già le formule perché `Range.copy` le preserva per impostazione predefinita. Se desideri solo i valori (ad esempio per congelare lo stato attuale), imposta `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Ora il foglio di destinazione contiene valori statici, ma la tabella pivot continuerà a funzionare perché la sua cache fa parte dell'intervallo.

## Riepilogo della soluzione

* **Come copiare una tabella pivot** – carica il workbook, definisci l'intervallo esatto, aggiungi un nuovo foglio, copia l'intervallo e salva.  
* Il processo dimostra anche **copiare un intervallo in un nuovo foglio** e come **duplicare il foglio della tabella pivot** in modo sicuro.  
* Puoi affinare la copia con `CopyOptions` per migliorare le prestazioni o ottenere scenari solo‑valore.

## Prossimi passi e argomenti correlati

* **Aggiornare la cache della pivot programmaticamente** – usa `PivotTable.refreshData()` dopo aver aggiornato i dati di origine.  
* **Esportare la tabella pivot in PDF** – combina questa tecnica di copia con `PdfSaveOptions` per creare report snapshot.  
* **Automatizzare la duplicazione di più fogli** – itera su tutti i fogli di lavoro e applica la stessa logica di copia.

Sperimenta con queste varianti per adattare il modello al tuo specifico flusso di reporting. Se incontri casi particolari, come fonti dati esterne o pivot guidate da VBA, lo stesso approccio di copia dell'intervallo funziona, ma potresti dover copiare anche gli oggetti di connessione sottostanti.

---

*Buona programmazione! Se questo tutorial ti ha aiutato a imparare **come copiare una tabella pivot**, sentiti libero di condividerlo con i colleghi o contribuire con miglioramenti.*

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}