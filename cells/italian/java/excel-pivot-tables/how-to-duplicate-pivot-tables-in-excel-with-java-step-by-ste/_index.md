---
category: general
date: 2026-10-07
description: Impara come duplicare le tabelle pivot in Excel usando Java e Aspose.Cells.
  Copia una tabella pivot copiando il suo intervallo tra le cartelle di lavoro rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: it
lastmod: 2026-10-07
og_description: Come duplicare le tabelle pivot in Excel usando Java e Aspose.Cells.
  Segui questa guida per copiare una tabella pivot copiandone l’intervallo tra cartelle
  di lavoro.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Come duplicare le tabelle pivot in Excel con Java – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Come duplicare le tabelle pivot in Excel con Java – guida passo passo
url: /it/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come duplicare le tabelle pivot in Excel con Java – guida passo‑passo

Se hai bisogno di **come duplicare pivot** tabelle in una cartella di lavoro Excel, questo tutorial ti mostra una soluzione completa, pronta‑all'uso. Utilizzando Aspose.Cells per Java puoi copiare una tabella pivot insieme ai suoi dati di origine copiando l'intervallo sottostante, quindi salvare il risultato come una nuova cartella di lavoro.

Duplicare una tabella pivot spesso sembra complicato perché la cache della pivot è nascosta all'interno del foglio. Copiando l'intero intervallo che contiene la pivot, Aspose.Cells ricrea automaticamente la cache nella cartella di lavoro di destinazione, così ottieni una copia pienamente funzionale senza dover intervenire manualmente sul XML.

In questa guida imparerai a:

* Caricare una cartella di lavoro di origine che contiene una tabella pivot.  
* Definire l'intervallo esatto che contiene la pivot.  
* Copiare quell'intervallo in una nuova cartella di lavoro, preservando la definizione della pivot.  
* Salvare il nuovo file e verificare che la pivot funzioni.  

I passaggi funzionano con qualsiasi versione di Excel supportata da Aspose.Cells (2007‑2024) e richiedono solo poche righe di codice Java.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| **Java 8 or newer** | Aspose.Cells is built for Java 8+. |
| **Aspose.Cells for Java** (latest version) | Provides the `Workbook`, `Range`, and `CopyRange` APIs used in the example. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | The pivot you want to duplicate. |
| **Write permission** to the target directory | Needed to save `CopyWithPivot.xlsx`. |

Aggiungi la dipendenza Maven di Aspose.Cells al tuo `pom.xml` (o scarica il JAR manualmente):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Come duplicare le tabelle pivot – implementazione completa

Di seguito trovi un programma Java autonomo che dimostra **come duplicare pivot** tabelle copiando l'intervallo che contiene la pivot. Il codice include gestione degli errori, commenti e un passaggio di verifica.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Spiegazione di ogni passaggio

| Passo | Cosa fa il codice | Perché è importante per **copia tabella pivot** |
|------|-------------------|----------------------------------------|
| **1️⃣ Carica cartella di lavoro di origine** | `new Workbook(srcPath)` reads `Source.xlsx`. | The source file is the only place where the original pivot exists. |
| **2️⃣ Definisci l'intervallo** | `createRange("A1:G20")` creates a `Range` object that covers the pivot and its data. | A pivot table is stored together with its cache; copying the whole range ensures the cache is moved as well. |
| **3️⃣ Copia l'intervallo** | `copyRange(srcRange, "A1")` writes the range into the destination sheet. | This is the core of **copy range between workbooks** – the API handles hidden objects automatically. |
| **4️⃣ Aggiorna la pivot** | `pivotTable.refresh()` forces the pivot to recalculate. | Guarantees the duplicated pivot shows the same values as the original, especially after modifications. |
| **5️⃣ Salva la cartella di lavoro** | `destWb.save(destPath)` writes the file to disk. | Produces the final **copy excel range** result that you can open in Excel. |

#### Output previsto

Dopo aver eseguito il programma, apri `CopyWithPivot.xlsx`. Vedrai un foglio di lavoro identico a quello di origine, e la tabella pivot funziona esattamente come l'originale – puoi espandere le righe, filtrare i campi e aggiornare i dati senza errori.

## Varianti comuni e casi limite

### 1️⃣ Copiare una pivot che si estende su più fogli

Se i dati di origine della pivot si trovano su un foglio diverso da quello della pivot stessa, includi entrambi i fogli nell'operazione di copia. L'approccio più semplice è copiare prima l'intero foglio di origine, poi copiare il foglio della pivot:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Gestire gli intervalli denominati

Aspose.Cells preserves named ranges when you copy a range. However, if the destination workbook already contains a name with the same identifier, a `CellsException` is thrown. Resolve this by renaming the conflicting name before the copy:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Cartelle di lavoro molto grandi e prestazioni

Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive. Enable **memory optimization**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Mantenere intatte le formule

If the source range contains formulas that reference cells outside the copied area, those references become broken after the copy. To avoid this, expand the range to include all dependent cells, or use `copyRange` with the `CopyOptions` flag `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Consigli professionali per una **copia intervallo tra cartelle di lavoro** affidabile

* **Usa sempre indirizzi assoluti** (`$A$1:$G$20`) quando il foglio di origine potrebbe essere rinominato.  
* **Aggiorna dopo la copia** – anche se Aspose.Cells ricostruisce la cache, chiamare `refresh()` elimina occasionali avvisi di cache obsoleta in Excel.  
* **Convalida la pivot**: dopo il salvataggio, apri il file programmaticamente e chiama `pivotTable.validate()` per assicurarti che non vi siano riferimenti interrotti.  
* **Compatibilità di versione**: il codice funziona con file Excel 2007‑2024 (`.xlsx`, `.xlsm`). Per file legacy `.xls`, imposta `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Elenco completo del codice sorgente (pronto per la compilazione)



## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come copiare una tabella pivot in Java – Guida completa Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Come creare tabelle pivot in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Come aggiornare l'origine della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}