---
category: general
date: 2026-09-08
description: Come copiare un intervallo in Java usando Aspose.Cells – impara a copiare
  una tabella pivot, duplicare una tabella pivot e esportare una tabella pivot mantenendo
  la formattazione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: it
lastmod: 2026-09-08
og_description: Come copiare un intervallo in Java con Aspose.Cells. Questo tutorial
  ti mostra come copiare una tabella pivot, duplicare una tabella pivot e esportare
  una tabella pivot mantenendo la formattazione.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Come copiare un intervallo in Java – guida completa ad Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come copiare un intervallo in Java con Aspose.Cells
url: /it/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare un intervallo in Java con Aspose.Cells

Se hai bisogno di **come copiare un intervallo** in Java, Aspose.Cells rende il compito semplice. Che tu stia spostando un blocco di celle normale o una tabella pivot completa, la libreria gestisce l'operazione di copia mantenendo intatti formule, stili e cache della pivot. In questa guida imparerai a **copiare la tabella pivot**, **duplicare la tabella pivot**, e persino **esportare la tabella pivot** in una nuova cartella di lavoro con formattazione completa.

Il tutorial copre tutto, dalla configurazione del progetto fino al passaggio finale di verifica, così potrai eseguire il codice subito dopo aver letto. Non sono necessari strumenti esterni oltre al JAR di Aspose.Cells per Java.

## Prerequisiti

- Java 17 (o qualsiasi JDK supportato) installato e configurato nel tuo IDE.
- Maven o Gradle per la gestione delle dipendenze (gli esempi usano Maven).
- Un file Excel di origine (`source.xlsx`) che contiene una tabella pivot nell'intervallo `A1:H20`.
- Familiarità di base con la programmazione Java.

## Passo 1: Aggiungi Aspose.Cells al tuo progetto

Aspose.Cells è una libreria commerciale, ma è disponibile una versione di valutazione gratuita. Aggiungi la dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Se preferisci Gradle, l'entry equivalente è:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Aggiungere il JAR ti dà accesso alle classi `Workbook`, `Worksheet`, `Range` e `CopyOptions` utilizzate in tutto questo tutorial.

## Passo 2: Carica la cartella di lavoro di origine e seleziona il primo foglio di lavoro

La prima parte di **come copiare un intervallo** è aprire la cartella di lavoro che contiene i dati che desideri spostare.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Perché è importante:** aprire la cartella di lavoro crea una rappresentazione in memoria che l'API può manipolare senza toccare il file originale su disco.

## Passo 3: Definisci l'intervallo che contiene la tabella pivot

Una tabella pivot vive all'interno di un blocco rettangolare. Devi specificare quel blocco affinché Aspose.Cells sappia cosa copiare.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Nota:** il metodo `createRange` **non** copia ancora nulla; crea solo un oggetto `Range` che punta alle celle che intendi duplicare.

## Passo 4: Crea una nuova cartella di lavoro e ottieni il suo primo foglio

Ora crea la cartella di lavoro di destinazione dove risiederà l'intervallo copiato.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Perché una nuova cartella di lavoro?** Usare un file nuovo garantisce che nessuno stile nascosto o intervallo denominato interferisca con l'operazione di copia, il che è particolarmente importante quando **esporti la tabella pivot** in un file separato.

## Passo 5: Copia l'intervallo (inclusa la tabella pivot) nel foglio di destinazione

Questo è il fulcro di **come copiare un intervallo con formattazione**. L'oggetto `CopyOptions` indica ad Aspose.Cells di preservare tutto: valori, formule, stili e cache della pivot.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copia della tabella pivot:** Poiché l'intervallo di origine include la tabella pivot, l'API duplica automaticamente la cache della pivot, così il nuovo foglio contiene una tabella pivot pienamente funzionale che si comporta esattamente come l'originale.

## Passo 6: Salva la cartella di lavoro di destinazione

Infine, scrivi il risultato su disco.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Quando apri `dest.xlsx`, vedrai una replica esatta della tabella pivot originale, completa della sua formattazione, dei filtri (slicers) e dei campi calcolati.

## Output previsto

- `dest.xlsx` contiene un foglio di lavoro chiamato **Sheet1**.
- Le celle `A1:H20` contengono gli stessi dati e la stessa tabella pivot dell'origine.
- Tutti gli stili delle celle (font, colori, bordi) sono preservati.
- La tabella pivot è completamente interattiva; aggiornandola si riflettono i dati sottostanti nell'intervallo copiato.

## Come copiare un intervallo con formattazione – approfondimento

L'esempio precedente mostra lo scenario più semplice, ma potresti incontrare variazioni che richiedono un approccio leggermente diverso.

### Copia la tabella pivot in una cartella di lavoro esistente

Se hai bisogno di **duplicare la tabella pivot** all'interno di una cartella di lavoro che contiene già dati, usa la stessa chiamata `copyRange` ma punta a un indirizzo di destinazione diverso:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Esporta solo la tabella pivot (senza i dati circostanti)

A volte vuoi solo la tabella pivot, non i dati di origine. Identifica l'intervallo di visualizzazione della tabella pivot tramite il suo metodo `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Conserva la formattazione condizionale

Le regole di formattazione condizionale fanno parte della collezione di stili. Il flag `PasteType.ALL` le copia già, ma puoi essere esplicito:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Casi limite e risoluzione dei problemi

| Situazione | Cosa controllare | Correzione consigliata |
|------------|------------------|------------------------|
| Le cartelle di lavoro di origine e destinazione usano versioni di Excel diverse | Alcune funzionalità pivot più recenti (ad es., modello dati) potrebbero non essere visualizzate correttamente | Usa l'ultima versione di Aspose.Cells e imposta `Workbook.setFileFormatType(FileFormatType.XLSX)` per entrambe le cartelle di lavoro |
| Tabelle pivot molto grandi ( > 10 000 righe) causano pressione sulla memoria | Errori di out‑of‑memory durante la copia | Abilita `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` prima del caricamento |
| Il foglio di destinazione contiene già un intervallo denominato con lo stesso nome dell'origine | La collisione di nomi porta a un fallimento di `CopyOptions` | Chiama `copyOptions.setIgnoreNameConflicts(true)` |

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in una classe Java. Include tutti gli import, la gestione degli errori e i commenti.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Esegui il programma, poi apri `dest.xlsx` per verificare che la tabella pivot funzioni esattamente come l'originale.

## Conclusione

Ora sai **come copiare un intervallo** in Java usando Aspose.Cells, inclusi come **copiare la tabella pivot**, **duplicare la tabella pivot** e **esportare la tabella pivot** mantenendo tutta la formattazione. La libreria astrae i dettagli a basso livello della struttura XML di Excel, permettendoti di concentrarti sulla logica di business.

### Prossimi passi

- Esplora **copy range with formatting** per grafici e immagini (usa `PasteType.PICTURES`).
- Automatizza l'elaborazione batch: cicla su più file di origine e consolida le loro tabelle pivot in una cartella di lavoro riepilogativa.
- Combina questa tecnica con Aspose.Slides per generare report PowerPoint che incorporano la pivot copiata

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiornare la fonte della tabella pivot di Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Ottimizzare il caricamento della tabella pivot in Java usando Aspose.Cells – Guida completa](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Come copiare la tabella pivot in C# – Convertire Excel in PPTX, Copiare intervallo e creare casella di testo](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}