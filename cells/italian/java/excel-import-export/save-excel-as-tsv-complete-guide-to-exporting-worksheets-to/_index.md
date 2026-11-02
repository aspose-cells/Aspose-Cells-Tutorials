---
category: general
date: 2026-06-27
description: Salva Excel come TSV rapidamente usando Java. Scopri come esportare il
  foglio di lavoro in testo, esportare il foglio in testo semplice e esportare la
  stringa dei dati di Excel con Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: it
og_description: Salva Excel come TSV usando Java. Questo tutorial mostra come esportare
  il foglio di lavoro in testo, esportare il foglio in testo semplice e esportare
  la stringa dei dati di Excel in modo efficiente.
og_title: Salva Excel come TSV – Guida passo‑passo all'esportazione
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Salva Excel come TSV – Guida completa all'esportazione dei fogli di lavoro
  in testo
url: /it/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Excel as TSV – Guida completa all'esportazione dei fogli di lavoro in testo

Hai mai avuto bisogno di **save Excel as TSV** ma non sapevi quale chiamata API usare? Non sei solo. Molti sviluppatori si trovano in difficoltà quando cercano di trasformare un foglio di calcolo in un file delimitato da tabulazioni per l'elaborazione a valle. La buona notizia? Con poche righe di Java e Aspose.Cells puoi esportare un foglio di lavoro in testo, esportare il foglio come testo semplice e persino esportare la stringa dei dati di Excel senza sforzo.

In questo tutorial percorreremo l'intero flusso di lavoro—dalla lettura di una cartella di lavoro alla configurazione delle opzioni di esportazione e infine alla scrittura di un file TSV su disco. Alla fine sarai in grado di **save Excel as TSV** in qualsiasi progetto Java, sia che tu stia gestendo un singolo foglio sia che tu stia elaborando decine di file.

## Cosa copre questa guida

* Caricamento di una cartella di lavoro Excel dal disco  
* Selezione del foglio di lavoro corretto (o iterazione su molti)  
* Configurazione di `ExportTableOptions` per produrre output di testo semplice  
* Scrittura dei dati come file di valori separati da tabulazioni (TSV)  
* Suggerimenti per gestire intervalli grandi, delimitatori diversi e caratteri Unicode  

Nessuno strumento esterno richiesto—solo Aspose.Cells per Java e un runtime Java 8+.

## Passo 1: Configura il tuo progetto e carica la cartella di lavoro

Prima di immergerci nel codice, assicurati di aver aggiunto il JAR di Aspose.Cells al classpath del tuo progetto. Se usi Maven, la dipendenza è così:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Ora possiamo caricare la cartella di lavoro:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Perché è importante:** Caricare il file è il primo passo in qualsiasi flusso di lavoro **export Excel data string**. Se il file non può essere aperto, nulla funzionerà.

### Consiglio professionale
Se stai gestendo file protetti da password, chiama `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

## Passo 2: Scegli il foglio di lavoro da esportare

Puoi prendere il primo foglio, un foglio per nome, o iterare su tutti. Ecco il caso più semplice—esportare il primo foglio di lavoro:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Se hai bisogno di **export worksheet to text** per ogni foglio, avvolgi quanto sopra in un ciclo `for`:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

## Passo 3: Crea e configura le opzioni di esportazione

Il cuore di **export sheet plain text** risiede in `ExportTableOptions`. Attivando un paio di proprietà trasformiamo l'intervallo in una stringa di testo semplice con delimitatore tabulazione:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Perché usare `setExportAsString(true)`?**  
> Indica ad Aspose.Cells di trattare l'output come testo grezzo, che è esattamente ciò di cui hai bisogno quando vuoi **save Excel as TSV**. L'alternativa sarebbe un'esportazione CSV o HTML, nessuna delle quali fornisce una separazione tabulata pulita.

### Caso limite: delimitatori personalizzati
Se il tuo sistema a valle si aspetta una pipe (`|`) invece di una tabulazione, basta cambiare il delimitatore:

```java
exportOptions.setDelimiter('|');
```

## Passo 4: Esporta l'intervallo desiderato in un file di testo

Ora scriviamo effettivamente il file TSV. Il metodo `exportTable` accetta tre argomenti: l'intervallo di celle, il percorso di output e le `ExportTableOptions` appena configurate.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Se vuoi esportare l'intero intervallo utilizzato, sostituisci `"A1:D20"` con `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Consiglio professionale
Dopo l'esportazione, puoi anche catturare direttamente la stringa:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Questo ti fornisce la **export Excel data string** grezza senza toccare il file system.

## Passo 5: Gestione di file di grandi dimensioni e consigli sulle prestazioni

Quando si gestiscono fogli di calcolo massivi (centinaia di migliaia di righe), considera queste ottimizzazioni:

| Problema | Soluzione |
|----------|-----------|
| Pressione di memoria | Usa `WorkbookFactory.create(InputStream)` per streammare il file invece di caricarlo completamente. |
| I/O lento | Scrivi su un `BufferedWriter` o usa NIO `Files.newBufferedWriter`. |
| Caratteri Unicode | Assicurati che il file di output sia scritto con UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Di seguito un frammento che combina streaming e codifica UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

## Errori comuni e come evitarli

1. **Dimenticato di impostare `setExportAsString(true)`.**  
   Senza questo flag Aspose genererà un file Excel binario, compromettendo il tuo obiettivo **export worksheet to text**.  

2. **Uso del delimitatore sbagliato.**  
   Una virgola invece di una tabulazione produrrà un CSV, non TSV. Controlla `setDelimiter('\t')`.  

3. **Sintassi dell'intervallo errata.**  
   `"A1:D20"` va bene, ma `"A1:D20:"` (due punti extra) genererà un `IllegalArgumentException`.  

4. **Permessi del file.**  
   Assicurati che la directory di destinazione sia scrivibile. Su Linux, `chmod 755` spesso risolve il problema.  

## Conclusione – Esempio completo funzionante

Ecco il programma completo, pronto per l'esecuzione, che dimostra **save Excel as TSV** dall'inizio alla fine:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Eseguendo questo programma si ottiene un file separato da tabulazioni (`out.tsv`) che qualsiasi sistema a valle—sia un caricatore di database, uno script Unix `awk` o un semplice visualizzatore di fogli di calcolo—può consumare.

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **save Excel as TSV** usando Java e Aspose.Cells. Partendo dal caricamento della cartella di lavoro, selezionando il foglio corretto, configurando `ExportTableOptions` e infine scrivendo il file, ora disponi di un modello solido e pronto per la produzione per gli scenari **export worksheet to text**, **export sheet plain text** e **export Excel data string**.

Cosa c'è dopo? Prova a esportare più intervalli, cambiare i delimitatori al volo, o streammare l'output direttamente in una risposta HTTP per download basati sul web. Gli stessi principi si applicano, e scoprirai che gestire i dati Excel in testo semplice è un gioco da ragazzi una volta che le basi sono in ordine.

Hai domande o incontri un caso limite strano? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}