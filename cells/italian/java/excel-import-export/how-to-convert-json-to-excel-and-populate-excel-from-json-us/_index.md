---
category: general
date: 2026-09-27
description: Converti JSON in Excel con Aspose.Cells – scopri come popolare Excel
  da JSON e come elaborare JSON in Excel in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to excel
- populate excel from json
- how to process json in excel
- Aspose.Cells Java
- smart marker JSON
- excel automation Java
language: it
lastmod: 2026-09-27
og_description: Converti JSON in Excel usando Aspose.Cells. Questo tutorial mostra
  come popolare Excel da JSON e spiega come elaborare JSON in Excel con i marker intelligenti.
og_image_alt: Excel sheet after JSON data is merged into a single cell using Aspose.Cells
  Smart Marker
og_title: Converti JSON in Excel con Aspose.Cells – guida completa
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Convert JSON to Excel with Aspose.Cells – learn how to populate Excel
    from JSON and how to process JSON in Excel efficiently.
  headline: How to convert JSON to Excel and populate Excel from JSON using Aspose.Cells
  type: TechArticle
- description: Convert JSON to Excel with Aspose.Cells – learn how to populate Excel
    from JSON and how to process JSON in Excel efficiently.
  name: How to convert JSON to Excel and populate Excel from JSON using Aspose.Cells
  steps:
  - name: Why each step matters
    text: '* **Step 1** – The JSON string is the source data. Because we set `ArrayAsSingle`,
      the processor will not try to create rows for each object; instead it will write
      the raw JSON text into the cell. * **Step 2** – Loading the template separates
      presentation (the Excel layout) from data (the JSON). Thi'
  - name: 4.1 Converting a large JSON payload
    text: 'If the JSON text exceeds the default cell length limit, increase the column
      width or set the cell’s `Style` to wrap text:'
  - name: 4.2 Using a named range instead of a fixed cell
    text: You can place the smart‑marker inside a named range (e.g., `JsonCell`) and
      refer to it by name in the template. The processing code remains unchanged;
      Aspose.Cells resolves the marker wherever it appears.
  - name: 4.3 Merging multiple JSON objects into separate cells
    text: If you later decide to expand the array into rows, simply remove `options.setArrayAsSingle(true)`.
      The processor will generate a table where each object occupies a row, and you
      can customize column headings with additional markers.
  - name: 4.4 Handling nested JSON structures
    text: For nested objects, use dot notation in the marker, e.g., `${person.name}`.
      The processor will traverse the hierarchy automatically, allowing you to **populate
      Excel from JSON** with complex data models.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come convertire JSON in Excel e popolare Excel da JSON usando Aspose.Cells
url: /it/java/excel-import-export/how-to-convert-json-to-excel-and-populate-excel-from-json-us/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come convertire JSON in Excel e popolare Excel da JSON usando Aspose.Cells

Se hai bisogno di **convertire JSON in Excel**, questa guida ti mostra una soluzione completa, pronta all'uso. Entro la fine delle prime due frasi capirai come **popolare Excel da JSON** con una singola espressione smart‑marker e perché la chiamata `SmartMarkerOptions.setArrayAsSingle(true)` è fondamentale per il layout desiderato.

Passeremo in rassegna ogni passaggio necessario per **elaborare JSON in Excel**: caricare un modello, configurare il motore smart‑marker, unire i dati e salvare il risultato. Il tutorial presuppone che tu abbia conoscenze di base di Java e una licenza Aspose.Cells funzionante. Non sono necessari strumenti esterni, e il codice si compila ed esegue su Java 8+.

## Prerequisiti

* Java Development Kit (JDK) 8 o più recente installato.  
* Aspose.Cells for Java (l'ultima versione al momento della stesura, 23.9) aggiunto al classpath del tuo progetto.  
* Un modello Excel chiamato `SmartMarkerTemplate.xlsx` che contiene lo smart‑marker `${jsonArray:ArrayAsSingle}` nella cella dove vuoi che appaiano i dati JSON.  
* Una directory in cui puoi scrivere il file di output `JsonSingleCell.xlsx`.

Se uno di questi elementi manca, installa il JDK, scarica il JAR di Aspose.Cells e crea il modello come descritto nella sezione successiva.

## Passo 1: Creare un modello Excel con uno smart‑marker

Uno smart‑marker indica ad Aspose.Cells dove inserire i dati. In questo caso vogliamo che l'intero array JSON sia trattato come un valore unico, quindi inseriamo il seguente marker nella cella di destinazione (ad esempio, **A1**):

```
${jsonArray:ArrayAsSingle}
```

> **Suggerimento:** Il modificatore `ArrayAsSingle` indica al processore di visualizzare l'intero array in una singola cella anziché espanderlo in una tabella. Questa è l'opzione chiave per lo scenario di **convertire JSON in Excel** mostrato più avanti.

Salva la cartella di lavoro come `SmartMarkerTemplate.xlsx` in una cartella a cui farai riferimento dal tuo codice Java.

## Passo 2: Scrivere il programma Java che **convertire JSON in Excel**

Di seguito trovi il file sorgente completo `JsonSmartMarker.java`. Ogni riga è commentata così puoi vedere come il programma **popola Excel da JSON** e **elabora JSON in Excel**.

```java
import com.aspose.cells.*;

public class JsonSmartMarker {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Define the JSON data that will be merged into the workbook.
        // The array contains two simple objects – you can replace it with any valid JSON.
        String json = "[{\"name\":\"John\",\"age\":30},{\"name\":\"Anna\",\"age\":25}]";

        // 2️⃣ Load the Excel template that already contains the smart‑marker.
        // Adjust the path to match your environment.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 3️⃣ Configure SmartMarker to treat the JSON array as a single value.
        // This option is what makes the **convert JSON to Excel** operation produce one cell.
        SmartMarkerOptions options = new SmartMarkerOptions();
        options.setArrayAsSingle(true);   // key option for single‑cell output

        // 4️⃣ Process the JSON data using the configured options.
        // The SmartMarkerProcessor reads the JSON string, matches the marker,
        // and writes the resulting representation into the workbook.
        workbook.getSmartMarkerProcessor().process(json, options);

        // 5️⃣ Save the resulting workbook. The file now contains the JSON text in the target cell.
        workbook.save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

### Perché ogni passaggio è importante

* **Passo 1** – La stringa JSON è il dato di origine. Poiché impostiamo `ArrayAsSingle`, il processore non cercherà di creare righe per ogni oggetto; invece scriverà il testo JSON grezzo nella cella.  
* **Passo 2** – Caricare il modello separa la presentazione (il layout Excel) dai dati (il JSON). Questa pratica mantiene la logica di **popolare Excel da JSON** pulita e riutilizzabile.  
* **Passo 3** – `SmartMarkerOptions.setArrayAsSingle(true)` è l'unico interruttore necessario per modificare il comportamento predefinito di espansione degli array. Senza di esso, il processore genererebbe una tabella, cosa che non vogliamo quando **convertiamo JSON in Excel** in una singola cella.  
* **Passo 4** – Il metodo `process` esegue il lavoro pesante di **come elaborare JSON in Excel**. Analizza il JSON, corrisponde al marker e scrive l'output secondo le opzioni.  
* **Passo 5** – Salvare la cartella di lavoro finalizza la conversione. Il file di output `JsonSingleCell.xlsx` può essere aperto in qualsiasi applicazione di fogli di calcolo.

## Passo 3: Verificare il risultato

Apri `JsonSingleCell.xlsx`. La cella **A1** (o la cella dove hai inserito `${jsonArray:ArrayAsSingle}`) dovrebbe contenere la stringa JSON esatta:

```
[{"name":"John","age":30},{"name":"Anna","age":25}]
```

La cartella di lavoro ora contiene i dati JSON in una singola cella, dimostrando che il programma ha convertito correttamente **JSON in Excel** e **popolato Excel da JSON**.

![Excel sheet after JSON data is merged into a single cell using Aspose.Cells](excel-output.png){: .center-image alt="Foglio Excel dopo che i dati JSON sono stati uniti in una singola cella usando Aspose.Cells Smart Marker"}

## Passo 4: Varianti comuni e casi limite

### 4.1 Conversione di un payload JSON di grandi dimensioni

Se il testo JSON supera il limite di lunghezza predefinito della cella, aumenta la larghezza della colonna o imposta lo `Style` della cella per avvolgere il testo:

```java
Cell target = workbook.getWorksheets().get(0).getCells().get("A1");
target.getStyle().setWrapText(true);
workbook.getWorksheets().get(0).autoFitColumns();
```

### 4.2 Utilizzare un intervallo denominato invece di una cella fissa

Puoi inserire lo smart‑marker all'interno di un intervallo denominato (ad esempio, `JsonCell`) e fare riferimento ad esso per nome nel modello. Il codice di elaborazione rimane invariato; Aspose.Cells risolve il marker ovunque appaia.

### 4.3 Unire più oggetti JSON in celle separate

Se in seguito decidi di espandere l'array in righe, rimuovi semplicemente `options.setArrayAsSingle(true)`. Il processore genererà una tabella in cui ogni oggetto occupa una riga, e potrai personalizzare le intestazioni di colonna con marker aggiuntivi.

### 4.4 Gestione di strutture JSON nidificate

Per oggetti nidificati, usa la notazione a punti nel marker, ad esempio `${person.name}`. Il processore attraverserà automaticamente la gerarchia, consentendoti di **popolare Excel da JSON** con modelli di dati complessi.

## Passo 5: Consigli per l'uso in produzione

* **Applicazione della licenza:** Aspose.Cells funziona in modalità valutazione con una filigrana. Applica la tua licenza prima di chiamare `new Workbook(...)` per evitare la filigrana in produzione.  
* **Prestazioni:** Per file JSON di grandi dimensioni, trasmetti i dati in streaming invece di caricare l'intera stringa in memoria. Aspose.Cells supporta overload del metodo `process` che accettano `InputStream`.  
* **Gestione degli errori:** Avvolgi la chiamata `process` in un blocco try‑catch per `Exception`. Registra il messaggio dell'eccezione per aiutare a diagnosticare JSON malformato o marker non corrispondenti.  
* **Test:** Includi test unitari che confrontino il valore della cella generata con la stringa JSON attesa. Questo garantisce che la tua logica di **convertire JSON in Excel** rimanga affidabile dopo le modifiche al codice.

## Conclusione

Ora disponi di un esempio completo e eseguibile che **convertisce JSON in Excel**, dimostra come **popolare Excel da JSON** e spiega **come elaborare JSON in Excel** con gli smart marker di Aspose.Cells. Regolando il modello e le `SmartMarkerOptions`, puoi passare da un output a cella singola a tabelle espanse, gestire strutture nidificate e integrare la soluzione in pipeline di elaborazione dati più ampie.

**Passi successivi**

* Esplora altri modificatori smart‑marker come `:Repeat` e `:If` per creare report più dinamici.  
* Combina questo approccio con sorgenti CSV o database per creare flussi di dati ibridi.  
* Rivedi la documentazione di Aspose.Cells sulla [sintassi Smart Marker](https://docs.aspose.com/cells/java/smart-markers/) per personalizzazioni più approfondite.

Buon coding e divertiti ad automatizzare i tuoi flussi di lavoro Excel con Java!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Importare JSON in Excel in modo efficiente usando Aspose.Cells per Java: Guida completa](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Importare dati JSON in Excel usando Aspose.Cells Java: Guida completa](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importare Json in Excel Aspose Cells Java](/cells/spanish/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}