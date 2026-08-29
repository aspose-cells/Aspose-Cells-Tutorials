---
category: general
date: 2026-08-08
description: Come copiare un pivot in Aspose.Cells e copiare un intervallo in una
  cartella di lavoro usando Java. Scopri i passaggi esatti per duplicare una tabella
  pivot con CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: it
lastmod: 2026-08-08
og_description: Come copiare un pivot in Aspose.Cells e copiare un intervallo in una
  cartella di lavoro con Java. Segui questa guida completa per duplicare una tabella
  pivot usando CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Come copiare il pivot in Aspose.Cells – copiare l'intervallo nel workbook
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Come copiare il pivot in Aspose.Cells – copiare l'intervallo nella cartella
  di lavoro
url: /it/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare pivot in Aspose.Cells – copiare intervallo in cartella di lavoro

Se hai bisogno di **come copiare pivot** in un file Excel usando Aspose.Cells, questa guida ti mostra il processo esatto. Alla fine del tutorial sarai in grado di **copiare intervallo in cartella di lavoro** preservando la definizione della tabella pivot.

L'esempio utilizza Java, ma gli stessi concetti si applicano a qualsiasi linguaggio .NET che funziona con Aspose.Cells. Non sono richiesti strumenti esterni—basta la libreria Aspose.Cells per Java e un ambiente di sviluppo di base.

## Prerequisiti

* Java Development Kit (JDK) 8 o successivo.
* Maven o Gradle per gestire le dipendenze (l'esempio usa Maven).
* Aspose.Cells per Java 23.9 (o l'ultima versione) aggiunto al tuo progetto.
* Una cartella di lavoro di input (`input.xlsx`) che contiene almeno una tabella pivot nel primo foglio.

Avere questi elementi pronti previene errori di runtime quando il codice accede alla cartella di lavoro.

## Come copiare pivot con Aspose.Cells

Questa sezione illustra ogni passaggio necessario per **come copiare pivot** da una parte di un foglio a un'altra, usando la classe `CopyOptions`.

### Passo 1: Aggiungi Aspose.Cells al tuo progetto

Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Perché questo passaggio è importante*: La libreria fornisce le classi `Workbook`, `CopyOptions` e altre necessarie per le operazioni **aspose.cells copy range**. Senza la dipendenza il compilatore non può risolvere quei tipi.

### Passo 2: Carica la cartella di lavoro di origine

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Caricare il file crea una rappresentazione in memoria del foglio di calcolo. L'oggetto `Workbook` ti dà accesso ai fogli di lavoro, alle celle e alle tabelle pivot.

### Passo 3: Configura le opzioni di copia per includere la tabella pivot

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` indica ad Aspose.Cells che l'operazione deve preservare i metadati della tabella pivot. Se ometti questa opzione, la tabella pivot verrebbe ridotta a dati statici, perdendo la sua interattività.

### Passo 4: Copia l'intervallo desiderato con la tabella pivot

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Il metodo `copyRange` copia celle, formattazione e—grazie alle opzioni impostate nel passaggio precedente—tutte le tabelle pivot che intersecano l'intervallo. Questo è il nucleo della funzionalità **copy range to workbook**.

### Passo 5: Salva la cartella di lavoro modificata

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Il salvataggio scrive le modifiche in un nuovo file (`output.xlsx`). Ora puoi aprire questo file in Excel e vedere che la tabella pivot è stata duplicata esattamente dove l'intervallo è stato copiato.

## Esempio completo, eseguibile

Unendo tutti i pezzi, ecco il programma completo che puoi compilare ed eseguire:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Risultato atteso

* `output.xlsx` contiene gli stessi dati di `input.xlsx`.
* La tabella pivot che originariamente occupava l'intervallo di origine appare nelle celle di destinazione, pienamente funzionale (filtri, capacità di aggiornamento, ecc.).
* Tutta la formattazione delle celle, le formule e le larghezze delle colonne sono preservate perché `copyRange` copia l'intero blocco di celle.

## Domande comuni e casi limite

**Cosa succede se l'intervallo di destinazione si sovrappone a una tabella pivot esistente?**  
Aspose.Cells sovrascriverà le celle di destinazione. Per evitare perdite di dati, assicurati che l'area di destinazione sia vuota o sposta prima la tabella pivot esistente.

**Posso copiare una tabella pivot tra fogli di lavoro?**  
Sì. Usa `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` dove `targetSheetIndex` indica il foglio di destinazione.

**Il metodo `setCopyPivotTable(true)` copia la sorgente dati sottostante?**  
Il metodo copia solo il riferimento alla cache della pivot. Se i dati di origine risiedono nella stessa cartella di lavoro, la pivot di destinazione punterà alla stessa cache. Per duplicare la cache, devi crearne una nuova manualmente.

**Come copiare un intervallo grande in modo efficiente?**  
Quando copi intervalli molto grandi, considera di utilizzare `CopyOptions.setCopyFormula(true)` e `setCopyDataValidation(true)` solo se necessario. Ridurre il numero di opzioni può migliorare le prestazioni.

## Consigli per un utilizzo affidabile di **aspose.cells copy range**

* **Suggerimento professionale:** Chiama sempre `workbook.calculateFormula()` dopo la copia se l'intervallo contiene formule che dipendono dalla cache della pivot.
* **Attenzione a:** Fogli di lavoro nascosti. `copyRange` funziona solo su fogli visibili a meno che non si faccia riferimento esplicitamente al foglio nascosto per indice.
* **Controllo versione:** Il flag `setCopyPivotTable` è disponibile a partire da Aspose.Cells 20.9. Assicurati che la versione della tua libreria lo supporti.

## Conclusione

Ora sai **come copiare pivot** in Aspose.Cells e come **copiare intervallo in cartella di lavoro** preservando la piena funzionalità della pivot. I passaggi—aggiungere la libreria, caricare la cartella di lavoro, configurare `CopyOptions`, eseguire la copia e salvare—formano un modello ripetibile che puoi adattare ad altri scenari di copia‑incolla.

Successivamente, esplora argomenti correlati come **aspose.cells copy range** per grafici, formattazione condizionale e convalida dei dati. Sperimenta la copia tra diversi formati di file (XLSX → XLS) per ampliare le tue capacità di automazione. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare tabelle pivot in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Come aggiornare la sorgente della tabella pivot di Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Come implementare i filtri (Slicers) nelle tabelle pivot usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}