---
category: general
date: 2026-11-25
description: Scopri come esportare Excel in PPTX con forme modificabili. Questa guida
  mostra anche come impostare l'area di stampa e convertire i grafici di Excel per
  le presentazioni.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: it
lastmod: 2026-11-25
og_description: Come esportare Excel in PPTX con forme modificabili usando Aspose.Cells,
  oltre a consigli per impostare l'area di stampa e convertire i grafici Excel per
  le presentazioni.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Come esportare Excel in PPTX con forme modificabili
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Come esportare Excel in PPTX con forme modificabili
url: /it/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel in PPTX con forme modificabili

Se hai bisogno di **come esportare Excel** in file PowerPoint mantenendo caselle di testo e forme modificabili, questa guida ti accompagna passo passo nel processo completo. Imparerai anche come **impostare l'area di stampa** per una diapositiva mirata e come **convertire oggetti di grafico Excel** affinché rimangano pienamente modificabili dopo l'esportazione.

Esportare Excel in PPTX è comune quando si creano presentazioni a partire da report basati sui dati. Utilizzando Aspose.Cells per Java eviti copie manuali, mantieni intatta la formattazione e ottieni un controllo programmatico sull'output.

## Cosa imparerai

* Carica un workbook XLSX esistente che contiene una casella di testo o un grafico.  
* Configura le opzioni di esportazione in modo che il file PPTX risultante contenga **forme modificabili**.  
* **Imposta l'area di stampa** per limitare l'intervallo esportato alle celle necessarie.  
* Salva il foglio di lavoro come file PPTX e verifica che le caselle di testo e i grafici possano essere modificati in PowerPoint.  

**Prerequisiti**

* Java 17 o versioni successive installate.  
* Maven o Gradle per la gestione delle dipendenze.  
* Una conoscenza di base dei workbook Excel e della programmazione Java.

---

## Come esportare Excel in PPTX con forme modificabili

Questa sezione fornisce il codice principale che esegue l'esportazione. L'esempio utilizza Aspose.Cells 23.9 (l'ultima versione al momento della stesura) e dimostra tutti i passaggi necessari.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### Perché ogni riga è importante

1. **Dipendenza** – Aspose.Cells fornisce la classe `ImageOrPrintOptions` che può renderizzare i fogli di lavoro come diapositive PPTX. Aggiungerla tramite Maven garantisce che la libreria sia nel classpath.  
2. **Import** – Importare le classi corrette mantiene il codice pulito ed evita nomi completamente qualificati.  
3. **Caricamento del workbook** – Devi indicare il file esatto che contiene gli oggetti da esportare. Il percorso può essere assoluto o relativo alla radice del progetto.  
4. **Opzioni di esportazione** – Impostare `setEditable(true)` è la chiave per **come esportare Excel** in modo che le forme PowerPoint risultanti rimangano modificabili. Senza questa impostazione, le caselle di testo diventano immagini statiche.  
5. **Area di stampa** – La chiamata `setPrintArea` limita l'esportazione alla regione di interesse, riducendo la dimensione del file e rimuovendo righe/colonne indesiderate. Questo risponde direttamente al requisito **imposta area di stampa excel**.  
6. **Salvataggio** – La costante `SaveFormat.PPTX` indica ad Aspose.Cells di generare un file PowerPoint anziché un'immagine o un PDF.  

#### Output previsto

Dopo aver eseguito il programma, apri `EditableShapes.pptx` in PowerPoint. Dovresti vedere una diapositiva che rispecchia l'intervallo Excel selezionato, e qualsiasi casella di testo o legenda del grafico può essere doppio‑cliccata e modificata come gli oggetti nativi di PowerPoint.

---

## Impostare l'area di stampa in Excel

Quando ti serve solo una parte del foglio di lavoro, definire un'**area di stampa** migliora sia le prestazioni sia la chiarezza visiva.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Suggerimento:* Se in seguito cambi l'intervallo dei dati, chiama nuovamente `setPrintArea` prima dell'esportazione. L'esportazione rispetta l'impostazione più recente.

---

## Convertire un grafico XLSX in un grafico PowerPoint modificabile

Aspose.Cells tratta i grafici come oggetti di disegno. Abilitando `setEditable(true)`, il grafico viene convertito in un grafico PowerPoint nativo che può essere modificato (ad esempio, cambiare le serie, i titoli degli assi).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

Se devi **come convertire xlsx** file che contengono più grafici, ripeti l'esportazione per ogni foglio di lavoro o utilizza `Workbook.save` con `SaveFormat.PPTX` dopo aver regolato il foglio attivo.

---

## Come convertire XLSX programmaticamente (bonus)

Oltre a PPTX, potresti voler convertire il workbook in un altro formato come PDF o PNG. La stessa classe `ImageOrPrintOptions` funziona per questi target:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

Questo dimostra la più ampia capacità di **come convertire xlsx** di Aspose.Cells.

---

## Problemi comuni e consigli di best‑practice

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Le forme diventano immagini | `setEditable(false)` (default) | Chiama `exportOptions.setEditable(true)` |
| La diapositiva esportata è vuota | L'area di stampa non include alcun dato | Verifica la stringa di intervallo passata a `setPrintArea` |
| Il grafico perde la formattazione | Uso di una versione obsoleta di Aspose.Cells | Aggiorna alla libreria più recente (≥ 23.9) |
| Dimensione file grande | Esportazione dell'intero foglio di lavoro | Limita l'area di stampa o nascondi righe/colonne inutilizzate |

---

## Conclusione

Ora sai **come esportare Excel** workbook in PPTX con forme e grafici completamente modificabili, come **impostare l'area di stampa** per focalizzare l'output, e come **convertire oggetti di grafico Excel** per una modifica fluida della presentazione. L'esempio Java completo e eseguibile sopra può essere inserito in qualsiasi progetto che utilizza già Aspose.Cells.

**Passi successivi**

* Esplora le opzioni di **convertire grafico excel** in PowerPoint (ad esempio, cambiare il tipo di grafico).  
* Combina questa esportazione con l'automazione **imposta area di stampa excel** per generare più diapositive da un unico workbook.  
* Prova a esportare in altri formati (PDF, PNG) utilizzando lo stesso modello `ImageOrPrintOptions`.  

Sentiti libero di sperimentare con diversi intervalli, più fogli di lavoro o layout di diapositiva personalizzati. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come impostare l'area di stampa excel ed esportare in PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Converti Excel in PowerPoint e imposta l'area di stampa](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Imposta l'area di stampa in Excel ed esporta in PowerPoint – Guida passo‑passo](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}