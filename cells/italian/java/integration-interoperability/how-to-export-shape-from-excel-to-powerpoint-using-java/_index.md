---
category: general
date: 2026-11-16
description: Scopri come esportare una forma da Excel a PowerPoint in Java, convertire
  un grafico di Excel in un file PPTX e salvare la forma PPTX con Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: it
lastmod: 2026-11-16
og_description: Come esportare una forma da Excel a PowerPoint in Java. Segui questo
  tutorial completo per convertire un grafico Excel, salvare la forma in PPTX e incorporare
  una forma in un file PowerPoint.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: Come esportare una forma da Excel a PowerPoint in Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: Come esportare una forma da Excel a PowerPoint usando Java
url: /it/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare una forma da Excel a PowerPoint usando Java

Se hai bisogno di **come esportare una forma** da una cartella di lavoro Excel a una diapositiva PowerPoint, questa guida ti mostra i passaggi esatti. Vedrai come **convertire oggetti di grafico Excel**, trasformarli in una **forma per PowerPoint**, e infine **salvare la forma PPTX** con le opzioni di esportazione corrette.

Esportare una forma è una necessità comune quando generi report in modo programmatico. Alla fine di questo tutorial avrai un programma Java autonomo che crea un file `shape.pptx` pronto per la presentazione. Non sono richiesti script esterni e il codice funziona con Aspose.Cells 2024‑R2 o versioni successive.

## Prerequisiti

* Java 17 o versioni successive (il codice si compila con qualsiasi JDK 8+)
* Libreria Aspose.Cells per Java (scarica dal sito Aspose o aggiungi la dipendenza Maven)
* Un file Excel (`chart.xls`) che contiene almeno una forma (un grafico, una casella di testo o SmartArt)
* Familiarità di base con la gestione delle eccezioni in Java

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## Come esportare una forma da Excel a PowerPoint (flusso generale)

Il processo è composto da quattro sezioni logiche:

1. **Carica la cartella di lavoro** che contiene la forma.  
2. **Individua la forma** sul primo foglio di lavoro.  
3. **Configura le opzioni di esportazione** affinché la forma diventi un oggetto PowerPoint modificabile.  
4. **Salva la forma come file PPTX**.

Ogni sezione è spiegata in dettaglio di seguito, e il programma completo e eseguibile segue le spiegazioni.

## Passo 1: Carica la cartella di lavoro che contiene la forma

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*Perché questo passo?*  
`Workbook` è il punto di ingresso per tutte le operazioni di Aspose.Cells. Caricare il file ti dà accesso ai fogli di lavoro, alle celle e alla collezione di forme. Se il file non viene trovato, Aspose.Cells genera una `FileNotFoundException`, che catturiamo più tardi.

## Passo 2: Accedi al primo foglio di lavoro e recupera la forma target

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*Perché questo passo?*  
I fogli di lavoro sono memorizzati in una collezione indicizzata a partire da zero, quindi `get(0)` restituisce il primo foglio. Anche le forme sono indicizzate; `get(0)` recupera la prima forma, che è tipicamente il grafico che desideri esportare. Se la tua cartella di lavoro contiene più forme, puoi iterare la collezione o usare `shape.getName()` per selezionarne una specifica.

## Passo 3: Prepara le opzioni di esportazione – vogliamo la forma come oggetto PPTX modificabile

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*Perché questo passo?*  
`ImageOrPrintOptions` controlla come la forma viene renderizzata. Scegliendo `SaveFormat.PPTX`, la libreria converte la grafica Excel in una forma PowerPoint basata su vettori che rimane modificabile dopo l'importazione. Questo è essenziale per una vera conversione **forma a PowerPoint**; usare PNG o JPEG bloccherebbe la grafica.

## Passo 4: Esporta la forma in un file PowerPoint

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*Perché questo passo?*  
Il metodo `save` scrive la forma usando le opzioni definite in precedenza. Il risultato `shape.pptx` contiene una singola diapositiva in cui la forma appare esattamente come in Excel, ma ora puoi modificarla in PowerPoint (cambiare colori, ridimensionare, aggiungere animazioni, ecc.). Questo soddisfa il requisito **save shape PPTX**.

## Esempio completo e eseguibile

Copia l'intera classe in un file chiamato `ExportShapeDemo.java`, sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo, ed esegui `javac ExportShapeDemo.java && java ExportShapeDemo`. Dopo l'esecuzione troverai `shape.pptx` nella cartella di destinazione.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### Output previsto

```
Export completed. File saved as shape.pptx
```

Apri `shape.pptx` in Microsoft PowerPoint. Vedrai una singola diapositiva contenente il grafico Excel originale (o la casella di testo) come una forma PowerPoint completamente modificabile.

## Varianti comuni e casi limite

| Situazione | Regolazione consigliata |
|------------|--------------------------|
| **Forme multiple** | Itera `worksheet.getShapes()` e chiama `save` per ogni forma, oppure seleziona tramite `shape.getName()`. |
| **La forma è un grafico con serie di dati** | Usa `exportOptions.setExportChartAsEditable(true)` per mantenere le serie modificabili. |
| **Necessità di un layout di diapositiva specifico** | Dopo il salvataggio, apri il PPTX con Aspose.Slides e inserisci la forma in un layout personalizzato. |
| **Cartella di lavoro grande** | Carica solo il foglio di lavoro necessario usando `Workbook(String, LoadOptions)` per ridurre il consumo di memoria. |
| **Formato di output diverso (PDF, PNG)** | Modifica `exportOptions.setSaveFormat(SaveFormat.PDF)` o `SaveFormat.PNG`. Questo è utile quando **converti un grafico Excel** in un'immagine statica invece di una forma PowerPoint. |

**Consiglio professionale:** Verifica sempre che l'indice della forma (`get(0)`) corrisponda all'elemento visivo che intendi esportare. L'ordine della collezione di forme rispecchia l'ordine di inserimento in Excel, che può differire dall'ordine di sovrapposizione visiva.

## Come esportare una forma da Excel a PowerPoint – lista di controllo per la risoluzione dei problemi

* **File not found** – Assicurati che il percorso in `new Workbook()` punti a un file `.xls` o `.xlsx` esistente.  
* **No shapes returned** – Conferma che il foglio di lavoro contenga effettivamente una forma; puoi chiamare `worksheet.getShapes().getCount()` per il debug.  
* **Exported file is empty** – Verifica che `exportOptions.setSaveFormat(SaveFormat.PPTX)` sia impostato; usare un formato immagine produrrà un'immagine invece di una forma.  
* **Compatibility issues** – Aspose.Cells 24.9+ supporta l'esportazione PPTX su tutte le principali piattaforme. Aggiorna se incontri `UnsupportedOperationException`.

## Conclusione

Ora sai **come esportare una forma** da una cartella di lavoro Excel e incorporarla in una presentazione PowerPoint usando Java. Il tutorial ha coperto il caricamento della cartella di lavoro, l'individuazione della forma, la configurazione delle opzioni **export shape from Excel**, e infine **save shape PPTX**. Con questa base puoi automatizzare la generazione di report, creare dashboard o integrare visualizzazioni Excel in presentazioni senza copia‑incolla manuale.

### Prossimi passi

* Esplora **converti un grafico Excel** in altri formati Office come PDF o DOCX.  
* Combina questa tecnica con Aspose.Slides per posizionare più forme su una singola diapositiva.  
* Sperimenta le proprietà di `ImageOrPrintOptions` (ad es., `setResolution`, `setTransparent`) per perfezionare la qualità visiva della forma esportata.

Sentiti libero di adattare il codice per l'elaborazione batch o per integrarlo in un servizio di reporting più ampio. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come esportare una forma con ShapeExportOptions in Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [Come esportare un foglio Excel in PowerPoint con Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [Come esportare grafici da Excel a PowerPoint – Guida completa Java](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}