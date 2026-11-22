---
category: general
date: 2026-11-22
description: Scopri come convertire Excel in PowerPoint usando Aspose.Cells per Java,
  includendo i passaggi per esportare un grafico Excel in PowerPoint in un unico flusso
  di lavoro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: it
lastmod: 2026-11-22
og_description: Converti Excel in PowerPoint usando Aspose.Cells per Java. Segui questo
  tutorial completo passo‑passo per esportare anche i grafici di Excel in PowerPoint.
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: Converti Excel in PowerPoint con Aspose.Cells – Guida Java
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: Come convertire Excel in PowerPoint con Aspose.Cells per Java
url: /it/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come convertire Excel in PowerPoint con Aspose.Cells per Java

Se hai bisogno di **convertire Excel in PowerPoint**, questa guida ti mostra un modo semplice con Aspose.Cells per Java. Vedrai anche come **esportare un grafico Excel in PowerPoint** come parte dello stesso processo, così potrai incorporare i grafici direttamente in una presentazione senza copia‑incolla manuale.

Convertire fogli di calcolo in presentazioni è comune quando vuoi condividere insight basati sui dati con un pubblico non tecnico. Invece di ricreare i grafici in PowerPoint, puoi automatizzare l'intero flusso, mantenere intatta la formattazione e risparmiare ore di lavoro.

In questo tutorial tu:

* Configurare Aspose.Cells in un progetto Maven o Gradle.  
* Caricare una cartella di lavoro esistente che contiene dati e grafici.  
* Configurare `ImageOrPrintOptions` per puntare al formato PPTX.  
* Salvare la cartella di lavoro come presentazione PowerPoint.  
* Verificare il risultato e gestire i casi limite tipici.

> **Prerequisito** – È necessaria una licenza valida di Aspose.Cells per Java (oppure puoi lavorare con la versione di valutazione). Il codice funziona con Java 8+ e qualsiasi IDE che supporti Maven/Gradle.

![Diagramma che mostra la conversione di Excel in PowerPoint usando Aspose.Cells](convert_excel_to_powerpoint.png)

## Di cosa avrai bisogno

| Elemento | Motivo |
|------|--------|
| **Java Development Kit (JDK) 8 or newer** | Necessario per compilare ed eseguire l'esempio. |
| **Maven or Gradle** | Semplifica la gestione delle dipendenze per Aspose.Cells. |
| **Aspose.Cells for Java** | Fornisce le API `Workbook` e `ImageOrPrintOptions` utilizzate per la conversione. |
| **Un file Excel (`shapes.xlsx`) contenente almeno un grafico** | Dimostra lo scenario di *esportare un grafico Excel in PowerPoint*. |

## Passo 1: Aggiungere Aspose.Cells al tuo progetto

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **Perché questo passo è importante** – Aggiungere la libreria rende disponibili le classi `Workbook`, `ImageOrPrintOptions` e `SaveFormat`. Senza la dipendenza corretta il codice non compila.

## Passo 2: Caricare la cartella di lavoro che contiene il/i grafico/i

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**Spiegazione:**  
`Workbook` è il punto di ingresso per tutte le operazioni Excel. Caricando `shapes.xlsx` porti sia le tabelle dati sia i grafici incorporati in memoria, consentendo la successiva conversione.

## Passo 3: Creare le opzioni di conversione e impostare il formato di destinazione su PPTX

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**Perché usare `ImageOrPrintOptions`?**  
Queste opzioni controllano come ogni foglio di lavoro o grafico viene renderizzato. Impostare `SaveFormat.PPTX` indica alla libreria di posizionare ogni foglio (o grafico) su una propria diapositiva, preservando la fedeltà visiva.

## Passo 4: Salvare la cartella di lavoro come presentazione PowerPoint

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**Cosa succede qui?**  
Aspose.Cells itera sui fogli di lavoro e sui grafici della cartella, li rasterizza in grafica compatibile con le diapositive e scrive un pacchetto `.pptx` nella posizione specificata. Il file risultante può essere aperto in Microsoft PowerPoint, Google Slides o qualsiasi visualizzatore compatibile con PPTX.

## Passo 5: Verificare la conversione

1. Apri `withShapes.pptx` in PowerPoint.  
2. Conferma che ogni foglio Excel appare come una diapositiva separata.  
3. Verifica che i grafici mantengano i loro colori, legende e etichette dei dati.  

Se un grafico appare distorto, potresti dover regolare i DPI di `ImageOrPrintOptions`:

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## Esportare un grafico Excel in PowerPoint – una variazione mirata

A volte è necessario spostare solo un singolo grafico invece dell'intera cartella di lavoro. Puoi farlo convertendo prima il grafico in un'immagine e poi inserendolo manualmente in una diapositiva PowerPoint, ma Aspose.Cells semplifica il processo:

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**Perché è importante:**  
Il frammento isola un singolo grafico, riduce le dimensioni del file e ti offre un controllo più fine su quali visualizzazioni diventano diapositive. È il modo più diretto per **esportare un grafico Excel in PowerPoint** quando non ti serve l'intera cartella di lavoro.

## Problemi comuni e come evitarli

| Problema | Causa | Soluzione |
|-------|-------|-----|
| **Blank slides** | Il foglio di lavoro non contiene dati visibili o il grafico è nascosto. | Assicurati che il grafico sia visibile e che il foglio di lavoro contenga dati prima di salvare. |
| **Low‑resolution images** | Il DPI predefinito è 96, potrebbe essere insufficiente per diapositive stampate. | Chiama `options.setResolution(200‑300)` prima di `workbook.save`. |
| **Unsupported chart types** | Tipi di grafico molto nuovi o personalizzati potrebbero non essere renderizzati perfettamente. | Esporta il grafico come immagine (`ImageFormat.PNG`) poi inseriscilo manualmente. |
| **File‑path errors** | Percorso relativo errato su diversi OS. | Usa `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` per percorsi indipendenti dalla piattaforma. |

## Consigli professionali per conversioni di livello produzione

* **Elaborazione batch:** Scorri una directory di file Excel e chiama la stessa logica di conversione.  
* **Gestione della memoria:** Per cartelle di lavoro grandi, invoca `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` per ridurre l'uso dell'heap.  
* **Attivazione licenza:** Posiziona il tuo file di licenza (`Aspose.Cells.lic`) nel classpath e chiama `License license = new License(); license.setLicense("Aspose.Cells.lic");` prima di qualsiasi utilizzo dell'API Aspose.  
* **Sicurezza dei thread:** Ogni thread dovrebbe lavorare con la propria istanza `Workbook`; gli oggetti Aspose.Cells non sono thread‑safe.

## Esempio completo funzionante

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**Output previsto:**  

Eseguendo il programma stampa `Conversion completed successfully.` e crea due file:

* `withShapes.pptx` – una presentazione in cui ogni foglio di lavoro (e i suoi grafici) appare su una diapositiva separata.  
* `singleChart.pptx` – una presentazione a singola diapositiva contenente solo il primo grafico della cartella di lavoro.

Apri questi file in PowerPoint per verificare che i grafici mantengano lo stile originale e le etichette dei dati.

## Conclusione

Ora sai come **convertire Excel in PowerPoint** usando Aspose.Cells per Java, e hai anche visto il modo più efficiente per **esportare un grafico Excel in PowerPoint** quando è necessario solo un visual specifico. Configurando `ImageOrPrintOptions` e impostando `SaveFormat` su `PPTX`, la libreria si occupa del lavoro pesante di renderizzare fogli di lavoro e grafici in grafiche compatibili con le diapositive.

Da qui puoi:

* Automatizzare conversioni batch per pipeline di reporting.  
* Combinare il PPTX generato con altri asset diapositive usando l'API Apache POI `XSLF`.  
* Esplorare formati di esportazione aggiuntivi come PDF o HTML per distribuzione multicanale.

Senti libero di sperimentare con le impostazioni DPI, layout diapositive personalizzati, o incorporare il PPTX generato nei flussi di lavoro email. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come esportare un foglio Excel in PowerPoint con Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [Come convertire Excel in PDF in Java usando Aspose.Cells: Guida passo‑passo](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Come esportare un grafico in docx da Excel usando Aspose.Cells per Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}