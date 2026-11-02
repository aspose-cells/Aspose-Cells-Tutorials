---
category: general
date: 2026-08-20
description: Scopri come impostare l'area di stampa in Excel, quindi esportare Excel
  in PPTX con Aspose.Cells. Questa guida ti accompagna nella conversione di un foglio
  di lavoro in PowerPoint e nel salvataggio come PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: it
lastmod: 2026-08-20
og_description: Imposta l'area di stampa in Excel e poi esporta Excel in PPTX usando
  Aspose.Cells. Segui questo tutorial passo‑passo per convertire un foglio di lavoro
  in PowerPoint e salvarlo come file PPTX.
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: Imposta l'area di stampa in Excel ed esporta in PowerPoint – guida completa
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: Come impostare l'area di stampa in Excel e esportare in PowerPoint
url: /it/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare l'area di stampa in Excel ed esportare in PowerPoint

Se hai bisogno di **set print area excel** prima di condividere i dati in una presentazione, questo tutorial ti mostra esattamente come fare. Vedrai come configurare l'area di stampa, poi **export excel to pptx** mantenendo le caselle di testo modificabili, così il PowerPoint risultante è pronto per ulteriori modifiche.

Utilizzeremo Aspose.Cells for Java per **convert worksheet to PowerPoint** e infine **save worksheet as PowerPoint** in formato PPTX. Non sono necessarie librerie aggiuntive oltre al JAR di Aspose.Cells. Alla fine di questa guida potrai eseguire il codice in qualsiasi ambiente compatibile con Java e produrre una presentazione che rispecchia l'intervallo Excel selezionato.

## Prerequisiti

- Java Development Kit 17 o versioni successive  
- Aspose.Cells for Java (scarica dal sito ufficiale di Aspose)  
- Un workbook Excel che contiene forme che desideri mantenere modificabili (ad es., `BookWithShapes.xlsx`)  

Assicurati che il JAR di Aspose.Cells sia nel tuo classpath:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## Passo 1: Set print area excel using Aspose.Cells

Il primo passo è definire l'intervallo che verrà esportato. Impostare l'area di stampa limita la conversione alle celle di interesse e migliora le prestazioni.

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**Why this matters** – Il metodo `setPrintArea` indica ad Aspose.Cells quali celle appartengono alla pagina stampabile. Quando successivamente **export excel to pptx**, solo quest'area viene renderizzata, così i dati superflui non compaiono nella diapositiva.

### Suggerimento Pro
Se ti serve un intervallo dinamico, puoi calcolare l'indirizzo programmaticamente:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## Passo 2: Export excel to pptx with editable text boxes

Dopo aver definito l'area di stampa, configura le opzioni di esportazione. Abilitare `setExportEditableTextBoxes` conserva il testo delle forme come campi modificabili in PowerPoint.

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**Why this matters** – Per impostazione predefinita Aspose.Cells rasterizza le caselle di testo, rendendole parte dell'immagine. Impostare `ExportEditableTextBoxes` su `true` mantiene gli oggetti forma originali, consentendo agli utenti di modificare il testo direttamente in PowerPoint.

## Passo 3: Convert worksheet to PowerPoint and save the file

Ora esegui la conversione effettiva. Il metodo `Workbook.save` accetta il nome del file di destinazione e le opzioni precedentemente preparate.

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

Quando il codice termina, `SheetWithEditableShapes.pptx` contiene una singola diapositiva che rispecchia l'area di stampa definita (`A1:G30`). Tutte le forme, incluse le caselle di testo, rimangono modificabili.

### Output previsto
Apri il PPTX generato in Microsoft PowerPoint:

- La diapositiva mostra le celle da **A1 a G30** esattamente come appaiono in Excel.  
- Qualsiasi forma presente nel foglio originale appare come forma PowerPoint.  
- Il testo all'interno di quelle forme può essere modificato direttamente in PowerPoint (senza rasterizzazione).

## Passo 4: Esempio completo e eseguibile

Di seguito il programma completo. Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella sul tuo computer.

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

Esegui il programma come descritto nella sezione *Prerequisiti*. Il file PowerPoint generato verrà collocato nella stessa directory specificata.

## Domande comuni e casi particolari

| Question | Answer |
|----------|--------|
| **Posso esportare più fogli di lavoro?** | Sì. Itera su `workbook.getWorksheets()` e chiama `save` per ogni foglio, modificando opzionalmente il nome del file di output. |
| **E se il mio workbook contiene grafici?** | I grafici vengono renderizzati come immagini per impostazione predefinita. Per mantenerli modificabili dovresti convertirli manualmente in forme PowerPoint, il che è al di fuori dello scopo di questa guida. |
| **L'area di stampa è obbligatoria?** | No. Se ometti `setPrintArea`, Aspose.Cells esporta l'intero intervallo utilizzato del foglio. Impostarla ti dà un controllo preciso. |
| **Funziona con file .xlsx creati da altri strumenti?** | Assolutamente. Aspose.Cells supporta qualsiasi workbook Office Open XML valido, indipendentemente dalla sua origine. |

## Prossimi passi

- **Save worksheet as PowerPoint** con layout di diapositiva personalizzati: esplora la classe `Presentation` di Aspose.Slides per unire la diapositiva esportata in un deck più ampio.  
- **Export excel to pptx** con diverse risoluzioni immagine: regola `exportOptions.setResolution(300)` per output ad alta DPI.  
- **Automate batch conversions**: combina questo codice con un file‑watcher per elaborare più file Excel in una cartella.

Padroneggiando **set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint** e **save worksheet as powerpoint**, puoi integrare i dati Excel in presentazioni programmaticamente, ottimizzando i flussi di reporting e riducendo il lavoro manuale di copia‑incolla.

---

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [Come impostare un'area di stampa in Excel usando Aspose.Cells per .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Imposta area di stampa Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Imposta area di stampa Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}