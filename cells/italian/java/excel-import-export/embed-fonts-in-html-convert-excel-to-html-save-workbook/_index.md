---
category: general
date: 2026-06-27
description: Incorpora i font in HTML quando converti Excel in HTML. Scopri come salvare
  la cartella di lavoro come HTML con i font incorporati usando un semplice codice
  Java.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: it
og_description: Incorpora i font in HTML durante la conversione di Excel in HTML.
  Questa guida mostra come salvare la cartella di lavoro come HTML con i font incorporati
  usando Java.
og_title: Incorpora i font in HTML – Converti Excel in HTML e salva la cartella di
  lavoro
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Incorpora i font in HTML – Converti Excel in HTML e salva la cartella di lavoro
url: /it/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporare i Font in HTML – Convertire Excel in HTML e Salvare la Cartella di Lavoro

Ti è mai capitato di dover **incorporare i font in HTML** quando *converti Excel in HTML*? Forse stai costruendo un portale di reporting e i font web predefiniti non sono sufficienti. La buona notizia è che non devi accontentarti di un aspetto generico e piatto: Aspose.Cells ti permette di inserire i caratteri esatti usati nel foglio di calcolo direttamente nel file HTML generato.

In questo tutorial percorreremo un esempio Java completo, pronto‑da‑eseguire, che **salva la cartella di lavoro come HTML** con i font incorporati, spiegheremo perché potresti volerlo fare e indicheremo alcune insidie comuni. Alla fine avrai una pagina HTML autonoma che appare esattamente come il foglio Excel originale, senza glifi mancanti, senza problemi di CSS esterno.

## Cosa Imparerai

- Come caricare una cartella di lavoro Excel esistente (o crearne una da zero) in Java.  
- Come configurare `HtmlSaveOptions` per incorporare i font della cartella di lavoro direttamente nell'output HTML.  
- Come invocare `Workbook.save` affinché il file venga scritto come **HTML con font incorporati**.  
- Suggerimenti per gestire file di font di grandi dimensioni, directory di font personalizzate e la risoluzione dei problemi comuni.

> **Prerequisito:** Hai bisogno di Aspose.Cells per Java (ultima versione) nel tuo classpath e di un runtime Java 8+. Non sono richieste altre librerie di terze parti.

---

## Passo 1: Configurare il Progetto e Importare le Classi Necessarie

Prima di immergerci nel codice, assicuriamoci che l'ambiente di sviluppo sia pronto. Se usi Maven, aggiungi la dipendenza Aspose.Cells al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Se preferisci Gradle, l'equivalente è:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Pro tip:** Mantieni la libreria aggiornata. Le nuove versioni migliorano spesso la gestione dei font e riducono la dimensione dei dati incorporati.

Ora, importa le classi di cui avremo bisogno:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Queste importazioni ci danno accesso al modello della cartella di lavoro, alle opzioni di esportazione HTML e a qualche classe di utilità.

---

## Passo 2: Caricare (o Creare) la Cartella di Lavoro Excel

Puoi caricare un file `.xlsx` esistente o creare una cartella di lavoro al volo. Per illustrare, supponiamo di avere un file chiamato `Sample.xlsx` nella cartella `resources` del progetto.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Se non hai un file di origine, puoi generare rapidamente una cartella di lavoro:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Perché è importante:** Quando incorpori i font, Aspose.Cells estrae le definizioni esatte dei caratteri usati nella cartella di lavoro. Se la cartella contiene font personalizzati, questi viaggeranno con l'HTML, garantendo fedeltà visiva.

---

## Passo 3: Configurare HtmlSaveOptions per Incorporare i Font

Questo è il cuore del tutorial. Per impostazione predefinita, `HtmlSaveOptions` scrive CSS che fa riferimento ai font di sistema. Per cambiare questo comportamento, abilitiamo il flag `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Cosa Fanno le Opzioni

| Opzione | Predefinito | Effetto quando modificato |
|--------|-------------|---------------------------|
| `setEmbedFonts(true)` | `false` | Incorpora i file di font completi (di solito come URI dati Base64) all'interno dell'HTML generato. |
| `setSubsetFonts(true)` | `false` | Riduce il font incorporato solo ai caratteri effettivamente usati, diminuendo drasticamente la dimensione del file. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Puoi scegliere di incorporare solo font specifici se hai vincoli di licenza. |

> **Caso limite:** Se la cartella di lavoro usa un font non installato sul server, Aspose.Cells ricade su un font di sistema predefinito. Per evitare sorprese, assicurati che tutti i font personalizzati siano disponibili nella directory dei font del runtime Java o registrali manualmente tramite `FontConfig`.

---

## Passo 4: Salvare la Cartella di Lavoro come HTML con Font Incorporati

Ora che le opzioni sono impostate, chiamiamo semplicemente `save`. L'output sarà un unico file `.html` che contiene i dati della cartella di lavoro **e** i file dei font codificati direttamente nel markup.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Quando apri `page.html` in qualsiasi browser moderno, la pagina viene renderizzata con la stessa tipografia vista in Excel—nessun file di font esterno, nessun carattere mancante.

---

## Passo 5: Verificare il Risultato e Comprendere l'Output

Apri il file HTML generato in un browser (Chrome, Firefox, Edge—qualsiasi vada bene). Dovresti vedere il foglio di lavoro renderizzato fedelmente. Per ricontrollare che i font siano davvero incorporati:

1. Fai clic destro sulla pagina → “Visualizza sorgente pagina”.  
2. Cerca `@font-face`. Troverai una regola CSS che contiene una riga `src: url(data:font/ttf;base64,…)`—questi sono i dati del font codificati in Base64.  

Se vedi questo, il passo **incorporare i font in HTML** è riuscito.

### Domande Frequenti

- **“Perché il file HTML è più grande del previsto?”**  
  L'incorporamento dei font completi può aggiungere diverse centinaia di kilobyte. Usa `setSubsetFonts(true)` per ridurlo, o considera di convertire solo i fogli necessari.

- **“Posso incorporare solo un font specifico?”**  
  Sì. Imposta `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` e poi specifica i nomi dei font tramite `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **“E se il font è con licenza e non posso incorporarlo?”**  
  Disattiva il flag (`setEmbedFonts(false)`) e fornisci un fallback web‑safe tramite CSS, oppure ospita il font su un CDN dove hai i permessi.

---

## Passo 6: Gestire Cartelle di Lavoro Grandi e Suggerimenti sulle Prestazioni

Incorporare i font funziona bene per fogli di calcolo modesti, ma una cartella con decine di font personalizzati può gonfiare la dimensione dell'HTML. Ecco alcune raccomandazioni orientate alle prestazioni:

- **Subset dei font** (già mostrato) per mantenere solo i glifi usati.  
- **Esporta solo i fogli necessari** usando `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Comprimi l'HTML** dopo la generazione (ad es., gzip sul server) per ridurre la latenza di rete.  
- **Cachea l'HTML generato** se lo stesso file Excel viene richiesto frequentemente.

---

## Passo 7: Prossimi Passi – Oltre l'Esportazione Base

Ora che hai padroneggiato **incorporare i font in HTML**, potresti voler esplorare funzionalità correlate:

- **Converti Excel in HTML con immagini** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Genera PDF invece di HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Crea HTML responsive** modificando `htmlOpts.setExportActiveWorksheetOnly` e `htmlOpts.setExportGridLines`.  

Tutte queste funzionalità seguono lo stesso schema: configura un oggetto `*SaveOptions`, attiva i flag appropriati e chiama `Workbook.save`.

---

## Conclusione

Hai appena imparato come **incorporare i font in HTML** mentre **converti Excel in HTML** e **salvi la cartella di lavoro come HTML** usando Aspose.Cells per Java. I passaggi chiave sono:

1. Carica o crea la cartella di lavoro.  
2. Crea `HtmlSaveOptions` e abilita `setEmbedFonts(true)`.  
3. Chiama `Workbook.save` con quelle opzioni.

Il risultato è un unico file HTML portabile che appare esattamente come il tuo foglio di calcolo originale—nessun carattere mancante, nessun file CSS aggiuntivo e nessuna dipendenza dai font installati sul client.

Sentiti libero di sperimentare con il subset dei font, l'incorporamento selettivo o persino combinare questa tecnica con la cache lato server per scenari ad alto traffico. Se incontri stranezze (come file insolitamente grandi o glifi mancanti), rivedi le impostazioni opzionali di cui abbiamo parlato e aggiusta di conseguenza.

Buon coding e goditi l'HTML pixel‑perfect che ora puoi servire direttamente dalle tue applicazioni Java!

## Cosa Dovresti Imparare Dopo

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti Excel in HTML in Java usando Aspose.Cells: Guida passo‑passo](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Esporta Excel in HTML usando Aspose.Cells per Java: Guida completa](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Esporta Excel in HTML usando IStreamProvider e Aspose.Cells per Java: Guida completa](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}