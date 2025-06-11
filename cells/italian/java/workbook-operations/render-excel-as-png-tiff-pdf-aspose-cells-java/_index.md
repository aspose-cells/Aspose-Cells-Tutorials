---
"date": "2025-04-07"
"description": "Scopri come convertire file Excel in immagini (PNG, TIFF) o PDF con Aspose.Cells per Java. Segui questa guida passo passo per migliorare la condivisione dei report."
"title": "Converti Excel in PNG, TIFF e PDF in Java utilizzando Aspose.Cells"
"url": "/it/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Convertire file Excel in PNG, TIFF e PDF utilizzando Aspose.Cells per Java

Nell'attuale contesto aziendale basato sui dati, convertire i file Excel in diversi formati, come immagini o PDF, è essenziale per migliorare la qualità dei report condivisi con gli stakeholder. Questo tutorial completo ti guiderà nella trasformazione fluida dei tuoi fogli di calcolo Excel in formati immagine come PNG e TIFF o nel loro salvataggio in PDF utilizzando Aspose.Cells per Java.

## Cosa imparerai
- Come convertire un file Excel in un'immagine PNG.
- Conversione di intere cartelle di lavoro Excel in file TIFF.
- Salvataggio dei dati Excel come PDF con impostazioni di carattere personalizzate.
- L'importanza di impostare font predefiniti per i caratteri mancanti nei documenti.
- Tecniche per ottimizzare le prestazioni quando si utilizza Aspose.Cells.

Cominciamo subito col procedimento!

## Prerequisiti
Prima di iniziare, assicurati di avere:
- **Kit di sviluppo Java (JDK):** Versione 8 o successiva installata sul sistema.
- **Maven o Gradle:** Per gestire le dipendenze. Scegli in base alla configurazione del tuo progetto.
- **IDE:** Qualsiasi IDE Java come IntelliJ IDEA, Eclipse o NetBeans.

### Librerie e dipendenze richieste
Includi Aspose.Cells per Java nel tuo progetto:

**Utilizzo di Maven:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Utilizzo di Gradle:**

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisizione della licenza
- **Prova gratuita:** Inizia con una prova gratuita per esplorare le funzionalità di Aspose.Cells.
- **Licenza temporanea:** Richiedi una licenza temporanea se hai bisogno di più tempo per valutare il prodotto.
- **Acquistare:** Si consiglia di acquistare una licenza per un utilizzo a lungo termine.

## Impostazione di Aspose.Cells per Java
Per impostare Aspose.Cells, segui questi passaggi:
1. Assicurati che il tuo ambiente di sviluppo sia pronto con JDK e il tuo IDE preferito.
2. Aggiungere la dipendenza Aspose.Cells utilizzando Maven o Gradle come mostrato sopra.
3. Scarica una licenza temporanea o completa da [Pagina di acquisto di Aspose](https://purchase.aspose.com/buy) per rimuovere le limitazioni di valutazione.

**Inizializzazione di base:**
Inizia creando un `Workbook` oggetto nella tua applicazione Java:

```java
import com.aspose.cells.Workbook;

// Inizializza la cartella di lavoro con un percorso di file Excel
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/sample.xlsx");
```

## Guida all'implementazione
In questa sezione esploreremo come convertire i file Excel nei formati PNG, TIFF e PDF utilizzando Aspose.Cells per Java.

### Rendi Excel in PNG con il carattere predefinito
**Panoramica:** Converti un foglio Excel in un'immagine PNG impostando i font predefiniti per eventuali caratteri mancanti nella cartella di lavoro.

#### Guida passo passo:
1. **Crea ImageOrPrintOptions:**
   Questo oggetto consente di specificare impostazioni quali il tipo di immagine e le opzioni del carattere.

   ```java
   import com.aspose.cells.ImageOrPrintOptions;
   import com.aspose.cells.ImageType;

   ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
   imgOpt.setImageType(ImageType.PNG);
   imgOpt.setCheckWorkbookDefaultFont(false); // Ignora i caratteri predefiniti della cartella di lavoro
   imgOpt.setDefaultFont("Times New Roman"); // Font predefinito per i caratteri mancanti
   ```

2. **Rendi il primo foglio di lavoro:**
   Utilizzo `SheetRender` per convertire il primo foglio di lavoro del file Excel in un'immagine PNG.

   ```java
   import com.aspose.cells.SheetRender;
   import com.aspose.cells.Workbook;

   Workbook workbook = new Workbook(dataDir + "/sample.xlsx");
   SheetRender sr = new SheetRender(workbook.getWorksheets().get(0), imgOpt);
   sr.toImage(0, "YOUR_OUTPUT_DIRECTORY/output.png"); // Salva il file PNG
   ```

### Rendi Excel in TIFF con il carattere predefinito
**Panoramica:** Converti un'intera cartella di lavoro di Excel in un'immagine TIFF multipagina, assicurandoti che tutti i caratteri vengano visualizzati utilizzando un font predefinito.

#### Guida passo passo:
1. **Configurare ImageOrPrintOptions per TIFF:**

   ```java
   ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
   imgOpt.setImageType(ImageType.TIFF);
   imgOpt.setCheckWorkbookDefaultFont(false); // Ignora i caratteri predefiniti della cartella di lavoro
   imgOpt.setDefaultFont("Times New Roman"); // Font predefinito per i caratteri mancanti
   ```

2. **Esegui il rendering dell'intera cartella di lavoro:**
   Utilizzo `WorkbookRender` per convertire l'intera cartella di lavoro di Excel in un'immagine TIFF.

   ```java
   import com.aspose.cells.WorkbookRender;

   Workbook workbook = new Workbook(dataDir + "/sample.xlsx");
   WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
   wr.toImage("YOUR_OUTPUT_DIRECTORY/output.tiff"); // Salva il file TIFF
   ```

### Salva Excel come PDF con il carattere predefinito
**Panoramica:** Salva la cartella di lavoro di Excel come documento PDF specificando un font predefinito per eventuali font mancanti.

#### Guida passo passo:
1. **Configura PdfSaveOptions:**

   ```java
   import com.aspose.cells.PdfSaveOptions;

   PdfSaveOptions saveOptions = new PdfSaveOptions();
   saveOptions.setDefaultFont("Times New Roman"); // Font predefinito per i caratteri mancanti
   saveOptions.setCheckWorkbookDefaultFont(false); // Ignora i caratteri predefiniti della cartella di lavoro
   ```

2. **Salva la cartella di lavoro in formato PDF:**
   Utilizzare il `save` metodo per convertire il tuo file Excel in un PDF.

   ```java
   Workbook workbook = new Workbook(dataDir + "/sample.xlsx");
   workbook.save("YOUR_OUTPUT_DIRECTORY/output.pdf", saveOptions); // Salva il documento PDF
   ```

## Applicazioni pratiche
1. **Generazione automatica di report:** Converti i report finanziari mensili da Excel in PNG per una facile distribuzione.
2. **Archiviazione:** Salvare fogli di calcolo multipagina come immagini TIFF per scopi di archiviazione.
3. **Condivisione documenti:** Esporta i modelli di contratto in formato Excel in PDF con uno stile di carattere coerente.

## Considerazioni sulle prestazioni
- **Ottimizza la qualità dell'immagine:** Regola le impostazioni DPI in `ImageOrPrintOptions` per bilanciare qualità e dimensione del file.
- **Gestione della memoria:** Utilizzare strutture dati efficienti e smaltire tempestivamente le risorse inutilizzate per gestire efficacemente la memoria.
- **Elaborazione batch:** Per set di dati di grandi dimensioni, valutare l'elaborazione dei file in batch per evitare un sovraccarico di memoria.

## Conclusione
Ora hai imparato a convertire file Excel nei formati PNG, TIFF e PDF utilizzando Aspose.Cells per Java. Queste competenze miglioreranno significativamente le tue capacità di presentazione dei dati. Per esplorare ulteriori funzionalità di Aspose.Cells, consulta la relativa guida. [documentazione](https://reference.aspose.com/cells/java/) oppure prova la versione di prova gratuita.

## Sezione FAQ
1. **Come gestire file Excel di grandi dimensioni?**
   - Per aumentare l'efficienza dell'elaborazione, si consiglia di suddividere le cartelle di lavoro di grandi dimensioni in cartelle più piccole.
2. **Posso personalizzare la risoluzione dell'immagine durante il rendering?**
   - Sì, regola le impostazioni DPI in `ImageOrPrintOptions`.
3. **Cosa succede se il mio font predefinito non è disponibile su tutti i sistemi?**
   - Assicurarsi che il font predefinito scelto sia installato su tutti i sistemi di destinazione.
4. **Come posso richiedere una licenza temporanea?**
   - Visita [Pagina della licenza temporanea di Aspose](https://purchase.aspose.com/temporary-license/) per istruzioni.
5. **Dove posso trovare supporto se riscontro problemi?**
   - Utilizzare il [Forum di Aspose](https://forum.aspose.com/c/cells/9) per cercare assistenza dalla comunità e dagli esperti di Aspose.

## Risorse
- **Documentazione:** [Documentazione Java di Aspose.Cells](https://reference.aspose.com/cells/java/)
- **Scarica la libreria:** [Download di Aspose.Cells per Java](https://releases.aspose.com/cells/java/)
- **Acquista licenza:** [Acquista Aspose.Cells](https://purchase.aspose.com/buy)
- **Prova gratuita:** [Inizia una prova gratuita](https://releases.aspose.com/cells/java/)
- **Licenza temporanea:** [Ottieni una licenza temporanea](https://purchase.aspose.com/temporary-license/)
- **Forum di supporto:** [Supporto per le celle Aspose](https://forum.aspose.com/c/cells/9)

Con questa guida, ora sei pronto a convertire file Excel in formati PNG, TIFF e PDF utilizzando Aspose.Cells per Java. Migliora le tue capacità di condivisione dei dati con queste versatili tecniche di conversione.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}