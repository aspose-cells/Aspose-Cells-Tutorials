---
category: general
date: 2026-11-19
description: Scopri come copiare una tabella pivot in Java preservandone i dati e
  il layout. Questa guida passo‑passo mostra anche come copiare le tabelle pivot di
  Excel in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: it
lastmod: 2026-11-19
og_description: Copia tabella pivot in Java con Aspose.Cells. Segui questa guida per
  imparare come preservare le tabelle pivot e copiare accuratamente i dati pivot di
  Excel.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Copia tabella pivot in Java – guida completa di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Come copiare una tabella pivot in Java con Aspose.Cells
url: /it/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in Java con Aspose.Cells

Se hai bisogno di **copiare una tabella pivot** da una cartella di lavoro a un'altra, questa guida ti mostra esattamente come farlo in Java. Che tu stia costruendo un motore di reporting o migrando dati, vedrai un modo affidabile per preservare la cache, i campi e la formattazione della pivot.

Copiare una tabella pivot può essere complicato perché una semplice copia di intervallo spesso perde la fonte dati sottostante. In questo tutorial useremo Aspose.Cells per **come copiare una pivot** mantenendo intatti tutti i calcoli, e tratteremo anche **come preservare le pivot** quando la cartella di lavoro di destinazione è vuota.

## Prerequisiti

* Java 17 o versioni successive installate.  
* Aspose.Cells per Java (versione 23.9 o successiva) aggiunto al classpath del tuo progetto.  
* Due file Excel: una cartella di lavoro sorgente che contiene la tabella pivot e una cartella di lavoro di destinazione vuota (o una cartella di lavoro in cui vuoi unire).

Non è necessaria alcuna licenza speciale per l'esempio di codice, ma una licenza valida di Aspose.Cells rimuove le filigrane di valutazione.

## Passo 1: Carica la cartella di lavoro sorgente che contiene la tabella pivot

Il primo passo è aprire la cartella di lavoro che contiene la pivot originale. Caricare il file ti dà accesso al foglio di lavoro, alle celle e alla cache della pivot.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Perché è importante*: Aspose.Cells legge l'intera cartella di lavoro, inclusi i dati di cache nascosti che alimentano la pivot. Senza caricare il file completo, l'operazione di copia perderebbe la definizione della pivot.

## Passo 2: Prepara la cartella di lavoro di destinazione

Crea una nuova cartella di lavoro (o aprine una esistente) e prendi il suo primo foglio di lavoro. Qui verrà inserita la pivot.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Suggerimento*: Se hai già una cartella di lavoro di destinazione, sostituisci la chiamata `new Workbook()` con `new Workbook("target.xlsx")`. Questo ti permette di **copiare una pivot Excel** in una cartella di lavoro pre‑popolata.

## Passo 3: Definisci l'area di celle che racchiude la tabella pivot

Devi specificare l'intervallo esatto che copre la pivot. L'intervallo include la tabella della pivot, l'elenco dei campi e tutti i dati circostanti che desideri conservare.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Perché è importante*: Il `CellArea` indica ad Aspose.Cells cosa copiare. Se l'area è troppo piccola, la pivot verrà troncata; se è troppo grande, copierai dati non necessari. Regola le coordinate in base alle dimensioni reali della tua pivot.

## Passo 4: Esegui l'operazione di copia con CopyOptions

Usa il metodo `copy` sulla collezione di celle del foglio di lavoro sorgente. Passare un nuovo oggetto `CopyOptions()` garantisce che tutta la formattazione, le formule e la cache della pivot vengano trasferite.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Perché `CopyOptions` preserva la pivot

`CopyOptions` indica ad Aspose.Cells di trattare l'intervallo come un *intero* oggetto anziché come un semplice insieme di valori. Questa è la chiave per **come preservare le pivot**: la cache della pivot sottostante viene duplicata, così la cartella di lavoro di destinazione può ricalcolare la pivot senza intervento manuale.

## Passo 5: Salva la cartella di lavoro di destinazione

Infine, scrivi il file di destinazione su disco. Il file salvato conterrà una copia pienamente funzionante della pivot originale.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Risultato atteso*: Aprendo `copied_with_pivot.xlsx` in Excel si visualizza la stessa tabella pivot, completa di slicer, filtri e campi calcolati. Puoi aggiornarla e la fonte dati punterà all'intervallo copiato all'interno della stessa cartella di lavoro.

---

![Diagram showing copy pivot table process](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagramma che illustra il flusso di lavoro della copia della tabella pivot dalla cartella di lavoro sorgente a quella di destinazione"}

## Come copiare le tabelle pivot su più fogli di lavoro

Se hai bisogno di **copiare pivot Excel** da diversi fogli, ripeti i Passi 3‑4 per ogni foglio sorgente. Puoi anche iterare su `srcWb.getWorksheets()` e copiare ogni pivot in un foglio corrispondente in `destWb`. Ecco un esempio di ciclo conciso:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Consiglio professionale*: Usa `srcWs.getPivotTables().getCount()` per verificare se un foglio contiene effettivamente una pivot prima di copiarla. Questo evita di copiare dati irrilevanti.

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **La pivot perde la sua cache** | L'uso di `Worksheet.copy()` senza `CopyOptions` copia solo i valori delle celle. | Usa sempre `srcWs.getCells().copy(..., new CopyOptions())`. |
| **La destinazione mostra errori #REF!** | La pivot copiata fa ancora riferimento alla fonte dati esterna della cartella di lavoro originale. | Dopo la copia, chiama `destWs.getPivotTables().get(0).refresh();` per ricollegare la cache al nuovo intervallo. |
| **I slicer scompaiono** | I slicer sono memorizzati al di fuori dell'area principale delle celle. | Espandi `CellArea` per includere gli intervalli dei slicer, oppure copia l'intero foglio (`srcWs.copy(destWs, new CopyOptions())`). |
| **Rallentamento delle prestazioni su pivot grandi** | Copiare grandi intervalli con formattazione può essere lento. | Usa `CopyOptions.setOnlyData(true)` se non ti serve la formattazione, poi riapplica gli stili manualmente. |

## Come preservare la formattazione della tabella pivot durante l'aggiornamento dei dati

A volte è necessario **come preservare la pivot** dopo che i dati sorgente cambiano. Dopo la copia, puoi bloccare lo stile della pivot:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Impostare `PreserveFormatting` garantisce che tutti gli stili personalizzati applicati nella sorgente sopravvivano alla copia.

## Verifica della copia

Un modo rapido per confermare che la copia sia riuscita è confrontare le definizioni della pivot:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Se i conteggi corrispondono e la destinazione si apre senza errori, hai copiato con successo la **tabella pivot**.

## Conclusione

Ora sai come **copiare una tabella pivot** da una cartella di lavoro Excel a un'altra usando Aspose.Cells per Java, e hai visto i passaggi esatti per **come copiare una pivot** garantendo che la cache, la formattazione e i slicer della pivot rimangano intatti. Lo stesso schema funziona per scenari di **copia di pivot Excel** su più fogli, e puoi adattare il codice per gestire casi particolari come preservare la formattazione della pivot o gestire grandi set di dati.

### Prossimi passi

* Esplora le opzioni **preserve pivot table** come `setPreserveFormatting` e `refresh` per fonti dati dinamiche.  
* Prova a copiare le tabelle pivot tra cartelle di lavoro con ordini di colonna diversi—adatta il `CellArea` di conseguenza.  
* Combina questa tecnica con Aspose.Slides per inserire snapshot della pivot nelle presentazioni PowerPoint.

Buona programmazione, e sentiti libero di sperimentare variazioni per adattarle al tuo specifico flusso di automazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come copiare un intervallo e preservare una tabella pivot in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Come copiare una tabella pivot tra fogli di lavoro in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Come copiare una tabella pivot in una nuova cartella di lavoro in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}