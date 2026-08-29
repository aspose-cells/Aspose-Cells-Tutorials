---
category: general
date: 2026-08-17
description: Esporta Excel in TXT limitando le cifre significative – scopri come impostare
  le cifre e convertire Excel in testo in Java con un esempio completo di Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: it
lastmod: 2026-08-17
og_description: Esporta Excel in TXT limitando le cifre significative. Questo tutorial
  mostra come impostare le cifre significative e convertire Excel in testo utilizzando
  Aspose.Cells per Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Esporta Excel in TXT con cifre significative limitate – Guida Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Come esportare Excel in TXT con cifre significative limitate usando Java
url: /it/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Excel in TXT con cifre significative limitate usando Java

Se hai bisogno di **esportare Excel in TXT** controllando il numero di cifre significative, questa guida fornisce una soluzione pronta all'uso. Vedrai come impostare le cifre, convertire Excel in testo e mantenere l'output ordinato con una singola modifica di configurazione.

L'esempio utilizza Aspose.Cells per Java 25.10, che introduce l'opzione `setSignificantDigits`. Alla fine del tutorial potrai generare un file TXT che contiene solo le cifre desiderate, senza codice di arrotondamento aggiuntivo.

## Cosa otterrai

- Creare una cartella di lavoro programmaticamente.
- Inserire un valore numerico in una cella.
- Configurare le opzioni di salvataggio TXT per limitare le cifre significative.
- Salvare la cartella di lavoro come file di testo semplice.
- Comprendere come funziona l'impostazione `significantDigits` e come adattarla ad altri scenari.

### Prerequisiti

- Java 17 o successiva (il codice si compila anche con Java 8).
- Aspose.Cells per Java 25.10 o più recente. Scarica il JAR dal [sito Aspose](https://products.aspose.com/cells/java) e aggiungilo al classpath del tuo progetto.
- Un IDE o un semplice editor di testo e uno strumento di build da riga di comando (Maven/Gradle).

## Passo 1: Configura il progetto e importa Aspose.Cells

Crea un nuovo progetto Java e aggiungi il JAR di Aspose.Cells al percorso di compilazione. Se usi Maven, aggiungi la seguente dipendenza a `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Suggerimento:** Usa il classificatore `jdk17` per l'ultima runtime Java; riduce il rischio di avvisi di compatibilità.

## Passo 2: Crea una cartella di lavoro e scrivi un valore

La cartella di lavoro rappresenta un file Excel in memoria. Puoi aggiungere dati a qualsiasi cella usando il metodo `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Il numero `123.456789` sarà la sorgente per la nostra esportazione TXT. Per impostazione predefinita Aspose.Cells scriverebbe tutte le cifre decimali, il che spesso produce file di testo rumorosi.

## Passo 3: Configura le opzioni di salvataggio TXT per limitare le cifre significative

Aspose.Cells fornisce `TxtSaveOptions` per un controllo dettagliato sull'output di testo semplice. Il metodo `setSignificantDigits` indica all'esportatore quante cifre mantenere **in totale**, non solo dopo il punto decimale.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Quando `significantDigits` è impostato a `4`, l'esportatore arrotonda il valore `123.456789` a `123.5`. Questo comportamento corrisponde alla definizione matematica di cifre significative: le prime quattro cifre non zero vengono conservate.

### Come l'impostazione differisce da “limit decimals”

- **limit decimals** (`setDecimalPlaces`) taglia le cifre *dopo* il punto decimale, indipendentemente dalla parte intera.
- **significant digits** (`setSignificantDigits`) conta le cifre a partire dalla prima cifra non zero, utile quando i numeri variano di ordine di grandezza.

Se invece hai bisogno di un numero fisso di cifre decimali, sostituisci la riga sopra con:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Passo 4: Salva la cartella di lavoro come file TXT

Ora scrivi la cartella di lavoro su disco usando le opzioni configurate.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Eseguendo il programma viene creato `significant_digits.txt` nella directory di lavoro. Il file contiene una singola riga:

```
123.5
```

### Output previsto

| Cella | Valore originale | Esportato (4 cifre significative) |
|-------|-------------------|-----------------------------------|
| A1    | 123.456789        | 123.5                             |

Se cambi `setSignificantDigits(4)` in `6`, l'output diventa `123.457`. Sperimenta con valori diversi per vedere come l'arrotondamento si adatta.

## Passo 5: Varianti comuni e casi limite

### Esportare un intervallo intero

Se vuoi esportare più di una cella, basta riempire l'intervallo prima di salvare:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

La stessa impostazione `significantDigits` si applica a ogni cella numerica, garantendo una precisione coerente in tutto il file.

### Gestione dei separatori decimali specifici della locale

Aspose.Cells rispetta la locale di sistema quando scrive il testo. Per forzare un punto (`.`) come separatore decimale, imposta la cultura di `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Questo è utile quando l'applicazione di destinazione si aspetta un formato specifico, ad esempio parser CSV che accettano solo `.`.

### Sovrascrivere file esistenti

Il metodo `save` sovrascrive il file di destinazione per impostazione predefinita. Se devi evitare perdite accidentali di dati, controlla prima l'esistenza del file:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Cartelle di lavoro grandi e utilizzo della memoria

Quando esporti fogli di lavoro molto grandi, considera lo streaming dell'output:

```java
saveOptions.setEnableMemorySaving(true);
```

Questa opzione riduce il consumo di heap scrivendo le righe in modo incrementale.

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire immediatamente:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Eseguendo questo codice si produce `significant_digits.txt` con il seguente contenuto (colonne separate da tabulazione):

```
123.5	0.001235	98770
```

Ogni numero rispetta la regola delle **4 cifre significative**, dimostrando che l'impostazione funziona su diverse magnitudini.

## Conclusione

Ora sai come **esportare Excel in TXT** controllando il numero di cifre significative. Usando `TxtSaveOptions.setSignificantDigits`, puoi **impostare le cifre**, **limitare i decimali** e **limitare le cifre significative** in una singola riga di codice mantenibile. L'approccio funziona per celle singole, intervalli completi e cartelle di lavoro grandi allo stesso modo.

### Prossimi passi

- Esplora altre proprietà di `TxtSaveOptions` come `setDelimiter('\t')` per personalizzare i separatori di colonna.
- Combina l'esportatore con `CsvSaveOptions` se ti servono valori separati da virgola invece di testo semplice.
- Integra la routine in un servizio web che accetta file Excel caricati e restituisce l'output TXT ridotto al volo.

Sentiti libero di sperimentare con diversi limiti di cifre e locale. Se incontri uno scenario in cui le opzioni integrate non soddisfano un requisito speciale, puoi sempre post‑processare il file TXT generato con le utility standard di I/O Java.

Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire testo in numeri in Excel usando Aspose.Cells per Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java | Guida alle operazioni del workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Come esportare proprietà Excel personalizzate in PDF usando Aspose.Cells per Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}