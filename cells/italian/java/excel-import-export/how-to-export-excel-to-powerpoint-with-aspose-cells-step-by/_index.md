---
category: general
date: 2026-09-18
description: Scopri come esportare Excel in PowerPoint usando Aspose.Cells. Converti
  Excel in PPTX, crea PowerPoint da Excel e salva Excel come PowerPoint in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: it
lastmod: 2026-09-18
og_description: Come esportare Excel in PowerPoint usando Aspose.Cells. Segui questa
  guida per convertire Excel in PPTX, creare PowerPoint da Excel e salvare Excel come
  PowerPoint in modo efficiente.
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: Come esportare Excel in PowerPoint – tutorial completo di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: Come esportare Excel in PowerPoint con Aspose.Cells – guida passo‑passo
url: /it/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel in PowerPoint con Aspose.Cells – guida passo‑passo

Se hai bisogno di **come esportare Excel** in una presentazione PowerPoint, questo tutorial mostra una soluzione completa, pronta‑all'uso. Alla fine delle prime due frasi saprai esattamente quali chiamate API trasformano un file `.xlsx` in un `.pptx` modificabile. L'approccio funziona con qualsiasi cartella di lavoro che contiene grafici, immagini o altre forme, e richiede solo poche righe di codice Java.

In questa guida imparerai a **convertire Excel in PPTX**, **creare PowerPoint da Excel** e **salvare Excel come PowerPoint** mantenendo la modificabilità di grafici e immagini. Non è necessario alcuno strumento aggiuntivo oltre a Aspose.Cells, e il codice funziona su Java 8+ e su qualsiasi JDK recente.  

Prerequisiti:

* Java Development Kit (JDK) 8 o più recente installato  
* Maven o Gradle per la gestione delle dipendenze (o il JAR di Aspose.Cells nel classpath)  
* Una cartella di lavoro (`WithShapes.xlsx`) che contiene almeno un'immagine o un grafico  

---

![Diagramma che illustra come esportare Excel in PowerPoint](https://example.com/diagram.png "illustrazione di come esportare excel in powerpoint")

## Come esportare Excel in PowerPoint usando Aspose.Cells

Il cuore della conversione si articola in quattro passaggi concisi. Ogni passaggio è racchiuso in un metodo così da poter riutilizzare la logica in applicazioni più grandi.

### Passo 1: Carica la cartella di lavoro che contiene le forme

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**Perché è importante:**  
Caricare la cartella di lavoro ti dà accesso a fogli di lavoro, immagini e grafici. Aspose.Cells legge il file senza invocare Microsoft Office, quindi l'operazione funziona su server senza interfaccia grafica.

### Passo 2: Configura le opzioni di esportazione per la conversione in PowerPoint

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**Perché è importante:**  
`setExportChartAsEditable(true)` indica ad Aspose.Cells di generare forme vettoriali invece di immagini raster. Questo rende l'output PowerPoint **creare PowerPoint da Excel** con grafici completamente modificabili, soddisfacendo la maggior parte dei flussi di lavoro di creazione di presentazioni.

### Passo 3: Contrassegna le immagini (o i grafici) come modificabili

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**Perché è importante:**  
Quando un'immagine è contrassegnata come modificabile, Aspose.Cells la emette come forma EMF/WMF nel file PPTX. Questo è essenziale per il caso d'uso **esportare excel in powerpoint** in cui il destinatario deve modificare l'immagine in seguito.

### Passo 4: Salva la cartella di lavoro come presentazione PowerPoint modificabile

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**Perché è importante:**  
La chiamata `save` raggruppa tutte le modifiche precedenti (immagini modificabili, impostazioni dei grafici) in un unico archivio `.pptx`. Il file risultante può essere aperto in Microsoft PowerPoint, Google Slides o qualsiasi visualizzatore compatibile con PPTX.

### Esempio completo eseguibile

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**Risultato atteso:**  
Aprendo `Result.pptx` in PowerPoint si visualizza una diapositiva che rispecchia il primo foglio di lavoro di `WithShapes.xlsx`. I grafici appaiono come forme vettoriali su cui è possibile fare doppio clic per modificare i dati, e la prima immagine è un oggetto modificabile (puoi ridimensionarlo, cambiarne il colore o sostituirlo direttamente in PowerPoint).

---

## Convertire Excel in PPTX – personalizzazione avanzata

Mentre il flusso di base è sufficiente per la maggior parte degli scenari, potresti aver bisogno di:

* **Esporta più fogli di lavoro** – esegui un ciclo su `workbook.getWorksheets()` e chiama `workbook.save` per ciascuno, passando un indice di diapositiva diverso tramite `ImageOrPrintOptions.setSlideNumber(int)`.
* **Controlla le dimensioni della diapositiva** – usa `exportOptions.setImageHeight(int)` e `setImageWidth(int)` per corrispondere a una dimensione specifica della diapositiva PowerPoint (ad es., 1024 × 768).
* **Preserva le formule** – imposta `exportOptions.setExportFormulasAsValues(false)` se desideri che le formule originali di Excel siano incorporate come dati nascosti.

Queste modifiche ti consentono di **creare PowerPoint da Excel** che si allinea al branding aziendale o agli standard di presentazione.

---

## Salva Excel come PowerPoint – problemi comuni e come evitarli

| Sintomo | Causa probabile | Correzione |
|---------|-----------------|------------|
| I grafici appaiono come immagini raster | `setExportChartAsEditable(false)` (default) | Abilita i grafici modificabili con `setExportChartAsEditable(true)` |
| Nessuna immagine appare sulla diapositiva | Immagine non contrassegnata come modificabile o indice immagine fuori intervallo | Verifica che `sheet.getPictures().size() > 0` prima di chiamare `setEditable(true)` |
| Fogli di lavoro nascosti compaiono nel PPTX | `setExportHiddenWorksheet(true)` | Mantieni il valore predefinito `false` o impostalo esplicitamente a `false` |
| Il file di output è corrotto | Uso di una versione obsoleta di Aspose.Cells (pre‑20.10) | Aggiorna all'ultima versione di Aspose.Cells per Java (ad es., 23.12) |

---

## Esportare Excel in PowerPoint: consigli sulle prestazioni

* **Riutilizza lo stesso oggetto `ImageOrPrintOptions`** per più salvataggi – evita allocazioni ripetute.
* **Trasmetti in streaming la cartella di lavoro di origine** (`new Workbook(InputStream)`) quando lavori con file di grandi dimensioni su server con memoria limitata.
* **Parallelizza la conversione per foglio di lavoro** se devi generare una presentazione con centinaia di diapositive; ogni foglio può essere elaborato nel proprio thread perché gli oggetti Aspose.Cells sono thread‑safe dopo la costruzione.

---

## Prossimi passi

Ora sai **come esportare Excel** in un deck PowerPoint, **convertire Excel in PPTX** e **salvare Excel come PowerPoint** con contenuti modificabili. Per ampliare queste conoscenze potresti:

* Esplorare **Aspose.Slides** per aggiungere animazioni o layout di master‑slide dopo la conversione.
* Automatizzare il flusso di lavoro in una pipeline CI/CD in modo che ogni nuovo report Excel diventi automaticamente un deck di diapositive PPTX.
* Combinare questo approccio con **Apache POI** per pre‑elaborare i file Excel prima di passarli ad Aspose.Cells.

---

## Conclusione

Questo tutorial ha dimostrato **come esportare Excel** in PowerPoint usando Aspose.Cells, coprendo ogni passaggio dal caricamento della cartella di lavoro al salvataggio di un `.pptx` modificabile. Ora puoi **convertire Excel in PPTX**, **creare PowerPoint da Excel** e **salvare Excel come PowerPoint** nelle tue applicazioni Java con sicurezza. Sperimenta le impostazioni opzionali per personalizzare l'output secondo le tue precise esigenze di presentazione. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire Excel in PowerPoint usando Aspose.Cells per .NET: Guida completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Come esportare Excel in PowerPoint – Guida passo‑passo](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Come esportare Excel in PowerPoint con C# – Guida completa](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}