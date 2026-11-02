---
category: general
date: 2026-09-21
description: Scopri come copiare un intervallo in Java mantenendo intatta la tabella
  pivot. Questa guida passo passo ti mostra come esportare una tabella pivot in modo
  sicuro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: it
lastmod: 2026-09-21
og_description: Come copiare un intervallo in Java mantenendo la tabella pivot. Segui
  questa guida completa per esportare le tabelle pivot in modo sicuro.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Come copiare un intervallo e preservare una tabella pivot in Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Come copiare un intervallo e preservare una tabella pivot in Java
url: /it/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare un intervallo e preservare una tabella pivot in Java

Se hai bisogno di **come copiare intervallo** che contiene una tabella pivot, questa guida ti mostra un metodo affidabile per mantenere intatta la pivot. Molti sviluppatori hanno problemi a perdere la pivot quando esportano i dati, ma l'approccio qui sotto ti consente di **copiare tabella pivot** senza romperne la funzionalità. Alla fine di questo tutorial sarai in grado di **preservare la struttura della tabella pivot**, **esportare file della tabella pivot** e capire **come preservare la pivot** in diversi scenari.

L'esempio utilizza Aspose.Cells per Java, una libreria popolare per l'automazione di Excel. Non è necessario alcuno strumento aggiuntivo oltre a un ambiente di sviluppo Java standard.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java 17 (o successiva) installata.  
* Maven o Gradle per gestire le dipendenze.  
* Aspose.Cells per Java (versione 23.9 o più recente). Aggiungi la seguente dipendenza Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Un workbook di origine (`Source.xlsx`) che contiene la tabella pivot che desideri copiare.

## Come copiare un intervallo e mantenere intatta la tabella pivot

L'idea principale è copiare il **range** che racchiude l'intera pivot—compresa la sua origine dati—utilizzando `copyRange`. Questo metodo copia sia i dati grezzi sia la definizione della pivot, garantendo che il workbook di destinazione riceva una pivot pienamente funzionale.

### Passo 1: Caricare il workbook di origine

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Perché questo passo?*  
Caricare il workbook ti dà accesso al foglio di lavoro che ospita la pivot. La classe `Workbook` astrae l'intero file Excel, mentre `Worksheet` fornisce operazioni a livello di cella.

### Passo 2: Definire l'intervallo che copre la tabella pivot

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Perché questo passo?*  
Una tabella pivot non è una singola cella; si estende su un blocco che include intestazioni, righe di dati e la cache della pivot. Specificando un intervallo che contiene completamente la pivot, garantisci che `copyRange` copierà anche la cache sottostante, fondamentale per il comportamento di **preservare la tabella pivot**.

### Passo 3: Creare un workbook di destinazione vuoto

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Perché questo passo?*  
Partire da un workbook pulito evita conflitti accidentali con fogli o intervalli denominati esistenti. Il workbook di destinazione riceverà l'intervallo copiato, esportando efficacemente il contenuto della **tabella pivot**.

### Passo 4: Copiare l'intervallo – la tabella pivot è preservata

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Perché questo passo?*  
`copyRange` esegue una copia profonda: valori delle celle, formattazione e metadati della pivot vengono trasferiti. Questa è l'operazione critica che consente di **copiare la tabella pivot** senza perderne la funzionalità. L'oggetto `CellArea` definisce dove l'intervallo atterra nel foglio di destinazione.

### Passo 5: Salvare il workbook di destinazione

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Perché questo passo?*  
Il salvataggio finalizza il processo di **esportazione della tabella pivot**. Il file risultante (`DestWithPivot.xlsx`) contiene una pivot pienamente operativa che puoi aprire in Excel, Google Sheets o qualsiasi altro visualizzatore di fogli di calcolo.

## Verifica che la tabella pivot sia stata preservata

Apri `DestWithPivot.xlsx` in Excel e controlla quanto segue:

1. La tabella pivot appare nella stessa posizione (A1:G20) della sorgente.  
2. Aggiornare la pivot aggiorna correttamente i dati, dimostrando che la cache è stata copiata.  
3. Tutta la formattazione (larghezze colonne, formati numerici) corrisponde a quella originale.

Se uno di questi controlli fallisce, verifica che l'intervallo di origine racchiuda completamente la pivot e la sua origine dati. Un errore comune è selezionare un intervallo che non include la cache dei dati, il che porta a una pivot rotta.

## Considerazioni aggiuntive

### Copiare la tabella pivot tra versioni di workbook diverse

Aspose.Cells supporta sia i file `.xls` più vecchi sia il formato più recente `.xlsx`. Lo stesso codice funziona indipendentemente dall'estensione del file, rendendolo una soluzione universale per **come preservare la pivot** tra versioni.

### Preservare la tabella pivot quando si utilizza una sorgente filtrata

Se la pivot di origine è filtrata, lo stato del filtro viene copiato anch'esso. Se devi reimpostare i filtri nella destinazione, chiama `PivotTable.refreshData()` dopo la copia:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Esportare la tabella pivot come snapshot statico

A volte potresti volere una copia statica (solo valori) anziché una pivot attiva. Sostituisci `copyRange` con `copyRange` seguito da `pt.setEnableRefresh(false)` per disabilitare ulteriori calcoli.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Gestire workbook di grandi dimensioni

Per workbook con molti fogli, limita l'operazione di copia al foglio specifico per ridurre l'uso di memoria. Usa `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` per ottimizzare le prestazioni.

## Esempio completo eseguibile

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire. Adatta i percorsi dei file al tuo ambiente.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Output previsto**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Quando apri `DestWithPivot.xlsx`, dovresti vedere la tabella pivot originale pienamente funzionale, confermando che hai eseguito con successo **come copiare intervallo** preservando la **tabella pivot**.

## Problemi comuni e consigli professionali

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| La pivot appare ma mostra errori `#REF!` | L'intervallo copiato ha omesso il foglio cache nascosto | Estendi l'intervallo di origine per includere l'intera cache (di solito le righe sotto la pivot) |
| Il workbook di destinazione è più grande del previsto | `copyRange` copia anche la formattazione | Usa `CopyOptions` per escludere la formattazione se le dimensioni sono un problema |
| L'aggiornamento fallisce con “Data source not found” | Il workbook di origine utilizza connessioni dati esterne | Replicare la connessione nella destinazione o copiare prima il foglio di origine dei dati |

**Consiglio pro:** Esegui sempre un rapido controllo `destWs.getPivotTables().size()` dopo la copia. Se il conteggio è zero, l'intervallo non includeva la definizione della pivot e devi ampliarlo.

## Conclusione

In questo tutorial abbiamo dimostrato **come copiare un intervallo** che contiene una tabella pivot e garantire che il comportamento di **preservare la tabella pivot** rimanga intatto. Caricando il workbook di origine, definendo un intervallo completo, usando `copyRange` e salvando il file di destinazione, puoi esportare in modo affidabile i dati della **tabella pivot** e rispondere alla domanda **come preservare la pivot** nei progetti Java.

Passi successivi che potresti esplorare includono:

* Automatizzare la copia per più fogli (usa la keyword secondaria **copy pivot table** in un ciclo).  
* Convertire il workbook esportato in CSV mantenendo i dati grezzi (mantieni comunque la logica **preservare la tabella pivot** per la sorgente).

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}