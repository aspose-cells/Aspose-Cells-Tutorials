---
category: general
date: 2026-11-22
description: Impara come esportare Excel come testo e creare un file delimitato da
  tabulazioni. Questa guida mostra come impostare la citazione di tutti i campi e
  salvare il testo del foglio di calcolo in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: it
lastmod: 2026-11-22
og_description: Esporta Excel come testo e crea un file delimitato da tabulazioni.
  Segui questo tutorial passo‑passo per racchiudere tutti i campi tra virgolette e
  salvare il testo del foglio di calcolo con Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Esporta Excel come testo – guida ai file delimitati da tabulazione
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Come esportare Excel in formato testo con delimitazione a tabulazione
url: /it/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel come testo con output delimitato da tabulazioni

Se hai bisogno di **esportare Excel come testo**, questo tutorial ti guida attraverso l’intero processo di creazione di un file delimitato da tabulazioni da una cartella di lavoro. Che tu stia costruendo una pipeline di migrazione dati o abbia bisogno di un rapido dump in stile CSV per l’elaborazione successiva, i passaggi seguenti ti permettono di **salvare il testo del foglio di calcolo** con pieno controllo su delimitatori e quotature.

Esportare i dati del foglio di calcolo come testo semplice è spesso più portabile rispetto al mantenimento del formato nativo `.xlsx`. In questa guida imparerai anche a **quotare tutti i campi**, garantendo che i valori contenenti tabulazioni, virgole o interruzioni di riga siano correttamente incapsulati.

## Cosa ti servirà

Prima di iniziare, assicurati di avere:

* Java 17 o versioni successive installate.  
* La libreria Aspose.Cells per Java (il codice utilizza `ExportOptions` e `ExportTableOptions` di questa libreria). Puoi aggiungerla via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Un IDE o un semplice editor di testo per compilare ed eseguire il programma Java.

## Esporta Excel come testo – passo‑a‑passo

Le sezioni seguenti suddividono il compito in tre passaggi logici. Ogni passaggio spiega **perché** è importante, non solo **cosa** digitare.

### Passo 1: Prepara la cartella di lavoro e i dati di esempio

Creare una cartella di lavoro ti fornisce qualcosa da esportare. In un progetto reale caricheresti un file esistente con `new Workbook("input.xlsx")`; qui generiamo un foglio piccolo in modo che l’esempio funzioni subito.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Perché questo passaggio?*  
Una cartella di lavoro è l’oggetto sorgente per qualsiasi operazione di esportazione. Aggiungendo qualche riga puoi verificare che l’opzione **quotare tutti i campi** protegga davvero virgole e altri caratteri speciali.

### Passo 2: Configura le opzioni di esportazione – delimitatore, quotatura e modalità di output

Il cuore dell’**esportazione del foglio di calcolo delimitato da tabulazioni** risiede in `ExportTableOptions`. Imposti il delimitatore a una tabulazione (`'\t'`) e abiliti `setQuoteAllFields(true)` così ogni cella è avvolta da virgolette doppie. Questo elimina ambiguità quando una cella contiene già una tabulazione o un ritorno a capo.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Perché questo passaggio?*  
- **Delimitatore** determina come le colonne sono separate. Una tabulazione (`\t`) crea un **file delimitato da tabulazioni** accettato da molti strumenti di elaborazione dati.  
- **Quote all fields** garantisce che anche se una cella contiene un delimitatore, il testo risultante rimanga analizzabile.  
- Impostare `ExportAsString` dice ad Aspose.Cells di generare una stringa anziché un workbook binario, esattamente ciò di cui hai bisogno per **salvare il testo del foglio di calcolo**.

### Passo 3: Salva la cartella di lavoro come file di testo delimitato da tabulazioni

Ora esegui effettivamente **l’esportazione di Excel come testo**. Il metodo `save` prende il percorso di destinazione e le `ExportOptions` configurate.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

Al termine del programma troverai `output/table.txt` contenente:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Perché questo passaggio?*  
La chiamata `save` scrive il **file delimitato da tabulazioni** su disco, effettuando di fatto **il salvataggio del testo del foglio di calcolo** in un formato apribile da Excel, Notepad o qualsiasi strumento di importazione dati che riconosca le tabulazioni.

## Come quotare tutti i campi quando si esporta Excel come testo

Se ometti `setQuoteAllFields(true)`, le celle che contengono tabulazioni, virgole o interruzioni di riga romperanno la struttura del file di output. Per esempio, la riga `Bob, Jr.` verrebbe divisa in due colonne, corrompendo il dataset. Abilita sempre la quotatura quando:

* I dati di origine possono contenere virgole, tabulazioni o interruzioni di riga.  
* I parser a valle si aspettano file CSV/TSV quotati.  
* Hai bisogno di un’esportazione deterministica indipendentemente dal contenuto delle celle.

## Creare un file delimitato da tabulazioni senza Aspose.Cells (opzionale)

Se preferisci una soluzione puramente Java senza librerie di terze parti, puoi iterare sulle righe e scriverle manualmente:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Questo snippet dimostra la stessa logica di **esportazione del foglio di calcolo delimitato da tabulazioni**: un delimitatore tab, quotatura di ogni campo e scrittura del risultato come testo semplice. Tuttavia, l’uso di Aspose.Cells semplifica la gestione di cartelle di lavoro grandi, preserva la formattazione e riduce il boilerplate.

## Problemi comuni e consigli professionali

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Tab mancanti nell'output** | Delimitatore lasciato al valore predefinito della virgola. | Chiamare esplicitamente `setDelimiter('\t')`. |
| **Le virgole non quotate rompono le colonne** | `quoteAllFields` non abilitato. | Usare `setQuoteAllFields(true)` o quotare manualmente. |
| **File non creato** | La cartella di output non esiste. | Assicurarsi che la cartella `output/` esista o usare `Files.createDirectories`. |
| **Problemi di codifica** | La codifica predefinita della piattaforma può corrompere i caratteri non ASCII. | Passare `ExportOptions.setEncoding(Encoding.getUTF8())` se necessario. |

## Testare il risultato

Dopo aver eseguito il programma:

1. Apri `output/table.txt` in un editor di testo semplice. Dovresti vedere ogni valore avvolto da virgolette doppie e le colonne separate da un singolo carattere di tabulazione.  
2. Importa il file in Excel (`Data → From Text/CSV`). Scegli **Tab** come delimitatore; Excel posizionerà correttamente ogni valore quotato nella propria cella.  
3. Verifica che i caratteri speciali (virgole, interruzioni di riga...

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [come esportare excel – Guida al testo delimitato da tabulazioni](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Salva Excel come file di testo con separatore personalizzato usando Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Come salvare Excel come testo con Aspose.Cells – guida passo‑passo](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}