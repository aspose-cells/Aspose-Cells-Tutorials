---
category: general
date: 2026-08-20
description: Impara a scrivere JSON in Excel e a popolare una cartella di lavoro Excel
  da JSON usando i marker intelligenti di Aspose e Java – guida passo‑passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose smart markers
- convert json to excel
- write json to excel
- populate excel from json
- create excel workbook java
language: it
lastmod: 2026-08-20
og_description: aspose smart markers ti consentono di scrivere JSON in Excel e creare
  un esempio di codice Java per un workbook Excel. Segui questo tutorial per popolare
  Excel da JSON rapidamente.
og_image_alt: Screenshot of an Excel file generated from a JSON array using Aspose.Cells
og_title: 'aspose smart markers: converti JSON in Excel con Java – guida completa'
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  headline: How to use aspose smart markers to convert JSON to Excel in Java
  type: TechArticle
- description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  name: How to use aspose smart markers to convert JSON to Excel in Java
  steps:
  - name: Expected output
    text: 'When you open `JsonArraySingleCell.xlsx`, cell **A1** contains:'
  - name: 1. Populating multiple cells with different JSON objects
    text: 'If you need to fill a table rather than a single cell, omit `ArrayAsSingle`
      and use the default array handling:'
  - name: 2. Using a JSON file instead of a hard‑coded string
    text: '```java String jsonPath = "data/people.json"; String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)),
      StandardCharsets.UTF_8); ```'
  - name: 3. Handling nested JSON structures
    text: 'For nested objects, reference sub‑properties in the smart marker:'
  - name: 4. License activation
    text: 'To avoid the evaluation watermark, activate your license before creating
      the workbook:'
  type: HowTo
tags:
- Aspose
- Java
- Excel
- JSON
title: Come utilizzare i marker intelligenti di Aspose per convertire JSON in Excel
  in Java
url: /it/java/excel-import-export/how-to-use-aspose-smart-markers-to-convert-json-to-excel-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare aspose smart markers per convertire JSON in Excel in Java

Se hai bisogno di **aspose smart markers** per convertire JSON in Excel, questo tutorial mostra una soluzione pronta all'uso. Vedrai come scrivere JSON in Excel, popolare una cartella di lavoro Excel da JSON e generare un file con una sola riga di codice.

L'esempio utilizza Aspose.Cells for Java, una libreria che elimina la necessità di Microsoft Office sul server. Alla fine della guida avrai un programma Java completo che crea una cartella di lavoro Excel, inserisce un array JSON in una singola cella e salva il risultato come `JsonArraySingleCell.xlsx`.

## Prerequisiti

* Java Development Kit 17 o versioni successive installato.
* Maven o Gradle per gestire le dipendenze (l'esempio utilizza Maven).
* Una licenza Aspose.Cells for Java (la valutazione gratuita funziona per i test).
* Familiarità di base con la sintassi Java e il formato JSON.

> **Consiglio professionale:** Se esegui il codice senza una licenza, la cartella di lavoro generata conterrà una piccola filigrana di valutazione sul primo foglio.

## Aggiungi Aspose.Cells al tuo progetto

Aggiungi la seguente dipendenza al tuo `pom.xml` (Maven) o l'equivalente in Gradle:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

La libreria fornisce le classi `Workbook`, `Worksheet`, `JsonDataSource` e `SmartMarker` utilizzate in tutto questo tutorial.

## Passo 1: Crea una cartella di lavoro Excel in Java

Per prima cosa, istanzia un nuovo oggetto `Workbook`. Rappresenta un file Excel vuoto in memoria.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // Creates a blank .xlsx file
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();
```

`Workbook` è il punto di ingresso per tutte le operazioni Excel. Per impostazione predefinita contiene un foglio di lavoro, che recuperiamo per ulteriori manipolazioni.

## Passo 2: Prepara l'array JSON che desideri scrivere in Excel

La stringa JSON può provenire da un file, da un servizio web o essere costruita programmaticamente. Per questo tutorial utilizziamo un semplice array inline:

```java
// Step 2: Define the JSON array that will be used as the data source
String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";
```

La struttura JSON corrisponde al formato previsto dai smart markers di Aspose.Cells: un array di oggetti in cui ogni oggetto contiene una proprietà `Name`.

## Passo 3: Inserisci uno smart marker che tratta l'array come una singola cella

Gli smart markers di Aspose ti consentono di inserire segnaposti direttamente nelle celle. L'opzione `ArrayAsSingle` indica al motore di posizionare l'intero array JSON in una singola cella anziché espanderlo in una tabella.

```java
// Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
cells.putValue("A1", "${jsonArray,ArrayAsSingle}");
```

Quando la cartella di lavoro viene elaborata, `${jsonArray,ArrayAsSingle}` verrà sostituito con il testo JSON grezzo.

## Passo 4: Registra la fonte dati JSON con il nome dello smart marker

Collega il nome del segnaposto (`jsonArray`) a un'istanza `JsonDataSource`. Questo passaggio associa la stringa JSON al marker.

```java
// Step 4: Register the JSON data source with the smart marker name
JsonDataSource dataSource = new JsonDataSource(jsonArray);
worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);
```

`JsonDataSource` analizza il JSON e lo rende disponibile al motore degli smart marker. La chiamata `setDataSource` lo registra con il nome utilizzato nella cella (`jsonArray`).

## Passo 5: Salva la cartella di lavoro su disco

Infine, scrivi la cartella di lavoro in un file fisico. Puoi scegliere qualsiasi directory desideri.

```java
// Step 5: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Eseguendo il programma si genera un file Excel che contiene l'array JSON nella cella **A1**. Apri il file con Excel, LibreOffice o qualsiasi visualizzatore che supporti `.xlsx` per verificare il risultato.

![Cartella di lavoro Excel creata con Aspose.Cells che mostra i dati JSON](/images/json-to-excel.png)

*Testo alternativo dell'immagine: Screenshot di un file Excel generato da un array JSON utilizzando Aspose.Cells.*

## Codice sorgente completo

Mettendo insieme tutti i pezzi, ecco la classe Java completa e eseguibile:

```java
import com.aspose.cells.*;

public class JsonArraySmartMarker {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                       // Empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Define the JSON array that will be used as the data source
        String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";

        // Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
        cells.putValue("A1", "${jsonArray,ArrayAsSingle}");

        // Step 4: Register the JSON data source with the smart marker name
        JsonDataSource dataSource = new JsonDataSource(jsonArray);
        worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);

        // Step 5: Save the workbook to a file
        String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Output previsto

Quando apri `JsonArraySingleCell.xlsx`, la cella **A1** contiene:

```
[{"Name":"John"},{"Name":"Jane"}]
```

Non vengono aggiunte righe o colonne aggiuntive—questo dimostra come **aspose smart markers** ti consentano di **scrivere JSON in Excel** mantenendo intatto il payload JSON.

## Varianti comuni e casi limite

### 1. Popolare più celle con diversi oggetti JSON

Se hai bisogno di riempire una tabella anziché una singola cella, ometti `ArrayAsSingle` e utilizza la gestione predefinita dell'array:

```java
cells.putValue("A1", "${jsonArray}");
```

Aspose.Cells espanderà l'array in righe, creando una colonna per ogni proprietà (`Name` in questo caso). Questo è utile quando desideri una visualizzazione tabellare tradizionale.

### 2. Utilizzare un file JSON invece di una stringa hard‑coded

```java
String jsonPath = "data/people.json";
String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)), StandardCharsets.UTF_8);
```

Leggi il contenuto del file in una stringa, quindi segui i Passi 3‑5 invariati. Questo approccio funziona per payload di grandi dimensioni o dati ricevuti da API esterne.

### 3. Gestire strutture JSON annidate

Per oggetti annidati, fai riferimento alle sotto‑proprietà nello smart marker:

```java
cells.putValue("B2", "${jsonArray.Address.City}");
```

Aspose.Cells attraversa automaticamente la gerarchia, consentendoti di popolare report complessi senza parsing manuale.

### 4. Attivazione della licenza

Per evitare la filigrana di valutazione, attiva la tua licenza prima di creare la cartella di lavoro:

```java
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

Inserisci questo codice all'inizio di `main`. Il file di licenza può essere incorporato come risorsa o caricato da una posizione sicura.

## Consigli per l'uso in produzione

* **Riutilizza l'oggetto workbook** – Se generi molti report in un'unica esecuzione, crea un unico `Workbook` e clona i fogli di lavoro invece di istanziare un nuovo workbook ogni volta.
* **Trasmetti l'output** – Per file di grandi dimensioni, usa `workbook.save(OutputStream, SaveFormat.XLSX)` per scrivere direttamente su uno stream di risposta nelle applicazioni web.
* **Valida il JSON** – Prima di passare i dati a `JsonDataSource`, valida il formato JSON per evitare errori a runtime.
* **Prestazioni** – Gli smart markers sono ottimizzati per operazioni in blocco; evita di mescolare scritture cella‑per‑cella con l'elaborazione degli smart marker nello stesso foglio.

## Conclusione

Ora sai come utilizzare **aspose smart markers** per **convertire JSON in Excel**, **scrivere JSON in Excel** e **popolare Excel da JSON** usando Java. L'esempio completo crea una cartella di lavoro Excel, inserisce un array JSON in una singola cella e salva il file—tutto in soli cinque passaggi concisi.

Successivamente, potresti esplorare:

- [Crea una cartella di lavoro Excel usando Aspose.Cells in Java: Guida passo‑passo](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Creare report Excel dinamici usando Aspose.Cells Java e Smart Markers](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java-smart-markers/)
- [Padroneggiare Aspose.Cells Java: Implementare Smart Markers e Formule per l'automazione di Excel](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}