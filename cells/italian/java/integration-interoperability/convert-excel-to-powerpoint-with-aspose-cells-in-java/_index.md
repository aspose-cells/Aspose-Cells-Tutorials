---
category: general
date: 2026-09-21
description: Converti Excel in PowerPoint con Aspose.Cells in Java – scopri come esportare
  il grafico in PPTX e salvare la cartella di lavoro come PPTX in poche righe di codice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: it
lastmod: 2026-09-21
og_description: Converti Excel in PowerPoint usando Aspose.Cells in Java. Questo tutorial
  mostra come esportare un grafico in PPTX e salvare la cartella di lavoro come PPTX
  con caselle di testo modificabili.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Converti Excel in PowerPoint con Aspose.Cells – Guida Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Converti Excel in PowerPoint con Aspose.Cells in Java
url: /it/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti Excel in PowerPoint con Aspose.Cells in Java

Se hai bisogno di **convertire Excel in PowerPoint**, questa guida ti mostra un modo conciso e pronto per la produzione. Vedrai come esportare un grafico in PPTX, mantenere le caselle di testo modificabili e **salvare la cartella di lavoro come PPTX** in sole tre righe di codice Java.

Molti sviluppatori esportano dati in PDF, ma PowerPoint è spesso più adatto per presentazioni che richiedono grafici dinamici ed elementi modificabili. Questo tutorial copre tutto ciò che ti serve — dall’impostazione del progetto alla gestione delle difficoltà più comuni — così potrai creare una presentazione PowerPoint da un grafico Excel senza uscire dal tuo IDE Java.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java 17 o versioni successive installate.  
* Maven (o Gradle) per gestire le dipendenze.  
* Una licenza Aspose.Cells per Java (la versione di prova gratuita è sufficiente per la valutazione).  
* Un file Excel (`ChartAndTextbox.xlsx`) che contenga almeno un grafico e una casella di testo.

## Passo 1: Aggiungi Aspose.Cells al tuo progetto

Il primo passo è includere la libreria Aspose.Cells. Usando Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Suggerimento:** Se usi Gradle, l’equivalente è:
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

L’inclusione della libreria ti dà accesso a `Workbook`, `PdfSaveOptions` e all’enum `SaveFormat` necessari per la conversione.

## Passo 2: Carica la cartella di lavoro che contiene il grafico e la casella di testo

Ora carica il file Excel. La classe `Workbook` legge l’intera cartella di lavoro in memoria, preservando grafici, formule e caselle di testo.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**Perché è importante:** Caricare prima la cartella di lavoro garantisce che tutti gli oggetti incorporati (grafici, immagini, caselle di testo) siano disponibili per il processo di esportazione. Se il file non viene trovato, Aspose.Cells genera una chiara `FileNotFoundException`, che puoi gestire per offrire un’esperienza utente migliore.

## Passo 3: Configura le opzioni di esportazione per mantenere le caselle di testo modificabili

Aspose.Cells utilizza `PdfSaveOptions` per controllare come gli oggetti vengono scritti quando il formato di destinazione è PowerPoint. Abilitando `setExportEditableTextBoxes(true)`, qualsiasi casella di testo nel foglio Excel rimane modificabile dopo la conversione.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **Perché usare `PdfSaveOptions` per PPTX?**  
> Internamente, Aspose.Cells riutilizza la pipeline di rendering PDF per l’output PowerPoint, consentendo un controllo fine sugli elementi modificabili. Impostare questa opzione è il modo consigliato per preservare la modificabilità delle caselle di testo.

## Passo 4: Salva la cartella di lavoro come presentazione PowerPoint

Infine, invoca `workbook.save` con `SaveFormat.PPTX`. Questo passaggio completa il flusso di lavoro **creare PowerPoint da grafico Excel**.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

Mettendo tutto insieme, il programma completo è il seguente:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Output previsto

Eseguendo il programma stampa:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

Quando apri `Result.pptx` in Microsoft PowerPoint, vedrai:

* Il grafico Excel originale renderizzato come un grafico PowerPoint nativo (modificabile nell’editor di grafici di PowerPoint).  
* La casella di testo di Excel appare come una forma modificabile, permettendoti di cambiare il testo direttamente nella diapositiva.

## Gestione dei casi limite più comuni

| Situazione | Approccio consigliato |
|-----------|----------------------|
| **File non trovato** | Avvolgi il costruttore `Workbook` in un blocco `try‑catch` e mostra un messaggio chiaro. |
| **La cartella di lavoro non contiene grafici** | Verifica che il foglio contenga un grafico (`worksheet.getCharts().getCount() > 0`) prima della conversione; altrimenti, salta il passaggio o aggiungi un segnaposto. |
| **File Excel di grandi dimensioni** | Aumenta la dimensione dell’heap JVM (`-Xmx2g`) per evitare `OutOfMemoryError` durante il rendering. |
| **Licenza non impostata** | Chiama `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` prima di caricare la cartella di lavoro per rimuovere la filigrana di valutazione. |

## Domande frequenti

**D: Posso convertire più fogli di lavoro in diapositive PowerPoint separate?**  
R: Sì. Scorri ogni foglio, esporta il suo grafico in una nuova diapositiva usando `PdfSaveOptions`, e poi salva la cartella di lavoro una sola volta al termine dell’elaborazione di tutti i fogli.

**D: Questo metodo preserva la formattazione delle celle?**  
R: Vengono trasferiti solo gli oggetti grafico e le caselle di testo su PowerPoint. La formattazione delle celle rimane nel file Excel; non appare nel PPTX.

**D: E se devo esportare in PDF invece di PPTX?**  
R: Usa `SaveFormat.PDF` e le stesse `PdfSaveOptions`. Il flag `setExportEditableTextBoxes` funziona anche per il PDF.

## Prossimi passi

Ora che sai come **salvare la cartella di lavoro come PPTX** e **esportare un grafico in PPTX**, potresti approfondire:

* Aggiungere più grafici a diapositive diverse (`create powerpoint from excel chart` con un ciclo).  
* Personalizzare i layout delle diapositive usando Aspose.Slides per Java per uno stile di presentazione più ricco.  
* Incorporare immagini dalle celle Excel in PowerPoint usando la classe `Picture`.

Queste estensioni ti permettono di costruire pipeline di reporting completamente automatizzate che generano presentazioni rifinite direttamente dai dati Excel.

---

**Riepilogo:** Questo tutorial ha mostrato un modo affidabile per **convertire Excel in PowerPoint** usando Aspose.Cells per Java. Caricando la cartella di lavoro, configurando `PdfSaveOptions` per mantenere le caselle di testo modificabili e salvando con `SaveFormat.PPTX`, ottieni un file PowerPoint che contiene grafici dinamici e forme modificabili — perfetto per presentazioni aziendali dinamiche. Sentiti libero di adattare il codice per l’elaborazione batch o integrarlo in soluzioni di reporting più ampie.


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}