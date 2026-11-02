---
category: general
date: 2026-10-07
description: Scopri come caricare JSON in Excel e generare XLSX da JSON usando Aspose.Cells.
  Questa guida passo‑passo mostra anche come popolare Excel da JSON e salvare la cartella
  di lavoro come XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: it
lastmod: 2026-10-07
og_description: Carica JSON in Excel e genera XLSX da JSON usando Aspose.Cells per
  Java. Segui questa guida per popolare Excel da JSON e salvare la cartella di lavoro
  come XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Carica JSON in Excel con Aspose.Cells – guida completa Java
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come caricare JSON in Excel con Aspose.Cells per Java
url: /it/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carica JSON in Excel con Aspose.Cells per Java

Se hai bisogno di **caricare JSON in Excel**, questo tutorial ti mostra un modo affidabile per farlo con Aspose.Cells per Java. Vedrai come generare XLSX da JSON, popolare Excel da JSON e infine **salvare la cartella di lavoro come XLSX** — tutto in un unico programma autonomo.

Lavorare con JSON nei fogli di calcolo è comune quando esporti dati da servizi web, API o archivi NoSQL. Alla fine di questa guida avrai una classe Java pronta all'uso che crea una cartella di lavoro da JSON e scrive il risultato in un file su disco.

## Prerequisiti

* Java 8 o versioni successive installato (il codice utilizza funzionalità Java standard).
* Libreria Aspose.Cells per Java (versione 23.10 o successiva). Puoi ottenerla dal [sito Aspose](https://downloads.aspose.com/cells/java) o tramite Maven Central.
* Un IDE o un semplice editor di testo e un terminale per compilare ed eseguire il codice Java.
* Familiarità di base con la sintassi JSON e i concetti di Excel.

> **Consiglio professionale:** Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml` per evitare la gestione manuale dei JAR:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Passo 1: Configura il progetto e importa le classi necessarie

Crea una nuova classe Java chiamata `JsonToExcelDemo`. Importa le classi Aspose.Cells di cui avrai bisogno per la creazione della cartella di lavoro, la gestione dei fogli di lavoro e l'elaborazione dei Smart Marker.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Perché questo passo è importante:* Importare le classi corrette garantisce che il compilatore possa trovare le API di Aspose.Cells. La classe `Workbook` rappresenta il file Excel, mentre `SmartMarkerProcessor` gestisce la conversione da JSON a Excel.

## Passo 2: Definisci la sorgente JSON che sarà caricata in Excel

Per questo esempio utilizziamo un piccolo array JSON contenente due oggetti. In uno scenario reale potresti leggere il JSON da un file, da un endpoint REST o da un database.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Perché questo passo è importante:* La stringa JSON è la fonte dei dati per l'operazione **popola Excel da JSON**. Tenere il JSON in una variabile `String` lo rende facile da passare al `SmartMarkerProcessor`.

## Passo 3: Crea una nuova cartella di lavoro e ottieni il primo foglio di lavoro

Una nuova cartella di lavoro ti offre una tela pulita. Il primo foglio di lavoro (indice 0) è dove inseriremo lo Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Perché questo passo è importante:* Aspose.Cells lavora con un oggetto `Workbook` che può essere salvato successivamente come file XLSX. Accedere al primo `Worksheet` ci consente di posizionare il marker in un indirizzo di cella noto.

## Passo 4: Inserisci uno Smart Marker che indica ad Aspose.Cells come trattare il JSON

Gli Smart Marker sono segnaposti che Aspose.Cells sostituisce con dati provenienti da una sorgente. Il marker `&=JSONData.ArrayAsSingle` indica alla libreria di trattare l'intero array JSON come valore di una singola cella.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Perché questo passo è importante:* L'uso di `ArrayAsSingle` evita il comportamento predefinito di espandere ogni elemento dell'array in righe separate. Questo è utile quando vuoi che il testo JSON appaia letteralmente in una cella, o quando prevedi di dividerlo successivamente con formule.

## Passo 5: Configura lo SmartMarkerProcessor con la sorgente dati JSON

Ora associa la stringa JSON al nome logico `JSONData`. Il processor sostituirà il marker con i dati effettivi.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Perché questo passo è importante:* `setDataSource` collega il nome usato nel marker (`JSONData`) con il payload JSON effettivo. `process()` esegue il lavoro pesante: analizza il JSON, applica la logica del marker e scrive il risultato nel foglio di lavoro.

## Passo 6: Salva la cartella di lavoro risultante come file XLSX

Infine, scrivi la cartella di lavoro su disco. La costante `SaveFormat.XLSX` garantisce il corretto formato Office Open XML.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Perché questo passo è importante:* Il salvataggio del file completa il flusso di lavoro **genera XLSX da JSON**. Il file prodotto può essere aperto in Excel, LibreOffice o qualsiasi altro programma di fogli di calcolo che supporta XLSX.

### Codice sorgente completo

Mettendo insieme tutti i pezzi, ecco il programma completo e eseguibile che **crea una cartella di lavoro da JSON**, **popola Excel da JSON** e **salva la cartella di lavoro come XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Risultato atteso

Quando apri `JsonSingleCell.xlsx` vedrai l'array JSON visualizzato nella cella **A1** esattamente come la stringa originale:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Se preferisci ogni oggetto su una riga separata, sostituisci il marker con `&=JSONData` (senza `.ArrayAsSingle`). Il processor espanderà quindi l'array in righe individuali, dimostrando una diversa tecnica **popola Excel da JSON**.

## Variazioni comuni e casi limite

| Situazione | Adeguamento |
|------------|-------------|
| **Grande payload JSON ( > 10 MB )** | Aumenta la dimensione dell'heap JVM (`-Xmx2g`) e considera lo streaming del JSON per evitare `OutOfMemoryError`. |
| **Oggetti annidati** | Usa marker gerarchici come `&=JSONData.Name` e `&=JSONData.Age` all'interno di una tabella per mappare ogni proprietà a una colonna. |
| **File JSON invece di una stringa** | Leggi il file in una `String` con `java.nio.file.Files.readString(Path.of("data.json"))` e passalo a `setDataSource`. |
| **Necessità di mantenere il formato JSON originale** | Mantieni il suffisso `.ArrayAsSingle`, oppure avvolgi il JSON in CDATA se prevedi di usare formule Excel che analizzano JSON in seguito. |
| **Fogli di lavoro multipli** | Crea fogli di lavoro aggiuntivi (`workbook.getWorksheets().add("Sheet2")`) e ripeti l'inserimento del marker su ciascun foglio. |

> **Attenzione:** Gli Smart Marker sono sensibili al maiuscolo/minuscolo. Assicurati che il nome logico (`JSONData`) corrisponda esattamente tra il marker e `setDataSource`.

## Testare la soluzione

1. Compila il programma:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Eseguilo:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Verifica che `JsonSingleCell.xlsx` compaia nella directory di lavoro e si apra senza errori.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea cartella di lavoro Excel da JSON – Guida completa Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Crea cartella di lavoro Excel C# – Inserisci JSON e salva come XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Salva cartella di lavoro Excel da JSON – Guida completa](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}