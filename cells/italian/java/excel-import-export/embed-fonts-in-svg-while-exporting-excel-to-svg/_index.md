---
category: general
date: 2026-08-14
description: Incorpora i font in SVG durante l'esportazione di Excel in SVG usando
  Aspose.Cells. Scopri come impostare l'area di stampa, impostare le opzioni di stampa
  e utilizzare la funzione WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: it
lastmod: 2026-08-14
og_description: Incorpora i font in SVG durante l'esportazione di Excel in SVG con
  Aspose.Cells. Questa guida ti mostra come impostare l'area di stampa, configurare
  le opzioni di stampa e applicare la funzione WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Incorpora i font in SVG durante l'esportazione di Excel in SVG – passo dopo
  passo
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Incorpora i font in SVG durante l'esportazione di Excel in SVG
url: /it/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporare i font in SVG durante l'esportazione di Excel in SVG

Se hai bisogno di **incorporare i font in SVG durante l'esportazione di Excel in SVG**, questo tutorial ti mostra esattamente come farlo con Aspose.Cells per Java. Tratteremo anche come **impostare l'area di stampa**, **configurare le opzioni di stampa** e **utilizzare la funzione WRAPCOLS** per formattare i dati senza perdere il layout.

Seguirai un esempio completo e eseguibile che carica una cartella di lavoro esistente, applica la formula `WRAPCOLS`, configura le opzioni immagine specifiche per SVG, definisce la regione di stampa e infine salva il file come SVG con i font incorporati. Non è necessaria alcuna documentazione esterna: copia il codice, eseguilo e ispeziona lo SVG risultante.

## Incorporare i font in SVG – configurazione di ImageOrPrintOptions

L'incorporamento dei font garantisce che lo SVG venga visualizzato esattamente come appare in Excel, anche su macchine che non hanno installato i caratteri originali.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Perché è importante*: quando `setEmbedFonts(true)` è abilitato, Aspose.Cells scrive i dati del font direttamente nella sezione `<defs>` dello SVG. Il risultato è un file autonomo che appare identico su tutti i browser e le piattaforme.

## Esportare Excel in SVG – flusso di lavoro completo

I passaggi seguenti illustrano il processo end‑to‑end, dal caricamento della cartella di lavoro al salvataggio del file SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Output previsto**: `output.svg` appare in `YOUR_DIRECTORY`. Aprendolo in un browser si vede il foglio di lavoro con tutti i font incorporati, i dati avvolti in tre colonne (grazie a `WRAPCOLS`) e solo le celle all'interno di `A1:H30` renderizzate.

## Impostare l'area di stampa per il foglio di lavoro

Definire un'area di stampa limita lo SVG esportato a un intervallo specifico, riducendo le dimensioni del file e focalizzando l'osservatore sui dati rilevanti.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Consiglio*: l'intervallo segue la notazione A1 di Excel. Se ti serve un intervallo dinamico, puoi calcolarlo programmaticamente con `ws.getCells().getMaxDisplayRange()`.

## Configurare le opzioni di stampa per l'output SVG

Le opzioni di stampa controllano come Aspose.Cells traduce il foglio di lavoro in un'immagine. Oltre a incorporare i font, puoi regolare risoluzione, scala e layout della pagina.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Perché impostare le opzioni di stampa*: senza opzioni esplicite, Aspose.Cells utilizza i valori predefiniti che potrebbero omettere l'incorporamento dei font o applicare un fattore di scala indesiderato, producendo SVG sfocati o con stile errato.

## Utilizzare la funzione WRAPCOLS per avvolgere i dati di colonna

`WRAPCOLS` è una formula di Excel che distribuisce un intervallo verticale in un numero specificato di colonne. È utile quando vuoi visualizzare un elenco lungo in una griglia compatta.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Quando la cartella di lavoro viene salvata, Aspose.Cells valuta la formula, producendo un layout a tre colonne all'interno dell'area di stampa definita. Questa tecnica funziona per qualsiasi intervallo di dimensioni: basta modificare il secondo argomento con il numero di colonne desiderato.

## Esempio completo e eseguibile

Di seguito trovi il programma Java completo che puoi incollare in qualsiasi IDE. Assicurati di avere la libreria Aspose.Cells per Java nel classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Passaggi di verifica**

1. Esegui il programma.  
2. Apri `output.svg` in un browser web.  
3. Conferma che il testo utilizzi lo stesso carattere del file Excel originale (i font sono incorporati).  
4. Verifica che compaiano solo le celle all'interno di `A1:H30` e che i dati da `A2:A10` siano visualizzati in tre colonne.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| I font mancano nello SVG | `setEmbedFonts(false)` o il file del font non è accessibile | Assicurati `setEmbedFonts(true)` e che il font sia installato sulla macchina che esegue il codice |
| WRAPCOLS non viene valutato | Motore di calcolo disabilitato | Chiama `workbook.calculateFormula()` prima dell'esportazione, oppure lascia che Aspose.Cells valuti durante il salvataggio |
| Lo SVG esportato è vuoto | L'area di stampa non include alcun dato | Controlla nuovamente l'intervallo passato a `setPrintArea` |
| Il file SVG è enorme | Nessuna scala applicata, alta risoluzione dell'immagine | Regola `imgOptions.setResolution(96)` o valore simile per controllare i DPI |

## Suggerimento professionale: riutilizzare ImageOrPrintOptions per più fogli di lavoro

Se la tua cartella di lavoro contiene diversi fogli che necessitano delle stesse impostazioni SVG, crea un'unica istanza di `ImageOrPrintOptions` e assegnala a ciascun `PageSetup` del foglio. Questo riduce il consumo di memoria e garantisce un'incorporazione coerente dei font in tutti i file esportati.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Prossimi passi

* **Esportare in altri formati vettoriali** – Cambia `ImageFormat.SVG` in `ImageFormat.PDF` per PDF di alta qualità.  
* **Elaborazione batch** – Scorri una cartella di file `.xlsx` e genera SVG automaticamente.  
* **Gestione personalizzata dei font** – Usa `FontSettings` per caricare i font da una directory specifica quando i font di sistema non sono sufficienti.  

Padroneggiando **incorporare i font in SVG**, **esportare excel in svg**, **impostare l'area di stampa**, **configurare le opzioni di stampa** e **utilizzare la funzione WRAPCOLS**, potrai automatizzare la generazione di SVG ad alta fedeltà per report, dashboard e visualizzazioni web direttamente dai dati di Excel. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche illustrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}