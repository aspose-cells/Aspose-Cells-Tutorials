---
category: general
date: 2026-11-25
description: Crea un esempio di codice Java per creare una cartella di lavoro Excel
  utilizzando i smart marker di Aspose.Cells per associare gli array JSON a valori
  singoli.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: it
lastmod: 2026-11-25
og_description: Crea una cartella di lavoro Excel in Java con Aspose.Cells per esportare
  facilmente gli array JSON come singole celle. Segui la guida passo passo.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Crea cartella di lavoro Excel in Java – Guida ai marker intelligenti di
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come creare un workbook Excel in Java con i marker di Aspose.Cells
url: /it/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una cartella di lavoro Excel in Java con i marker di Aspose.Cells

Se hai bisogno di **creare una cartella di lavoro Excel in Java** che scriva un array JSON in una singola cella, questo tutorial ti mostra esattamente come fare. Utilizzando i marker intelligenti di Aspose.Cells puoi trattare un intero array come un unico valore, evitando loop manuali e scritture cella‑per‑cella.

Imparerai come configurare una cartella di lavoro, definire un marker intelligente, collegare una fonte dati `Map` che contiene un array in stile JSON e infine salvare il file. L'esempio funziona con Java 17+, Maven e la libreria di prova gratuita Aspose.Cells per Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Screenshot di una cartella di lavoro Excel creata in Java usando i marker intelligenti di Aspose.Cells"}

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Java 17 or later | Le ultime funzionalità del linguaggio e gli aggiornamenti di sicurezza |
| Maven 3.6+ | Semplifica la gestione delle dipendenze |
| Aspose.Cells for Java (v23.12 or newer) | Fornisce le API `Workbook`, `Worksheet` e smart‑marker utilizzate nell'esempio |
| Basic knowledge of Java collections | Creerai una `Map<String, Object>` che funge da fonte dati |

Aggiungi la dipendenza Aspose.Cells al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Creare una cartella di lavoro Excel in Java – esempio completo

Il programma seguente è una soluzione **completa e eseguibile**. Copialo in un file chiamato `ExcelSmartMarkerDemo.java`, compila ed esegui.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Cosa fa il codice

1. **Crea una nuova cartella di lavoro** – `new Workbook()` ti fornisce un file Excel in memoria con un foglio predefinito.  
2. **Inserisce un marker intelligente nella cella A1** – `{{jsonArray:ArrayAsSingle}}` indica ad Aspose.Cells di sostituire il marker con l'*intero* array, unito da virgole.  
3. **Costruisce una fonte dati `Map`** – La chiave `"jsonArray"` corrisponde al nome del marker; il valore è un `String[]`.  
4. **Chiama `setSmartMarkerData`** – Questo collega la mappa al marker ed esegue la sostituzione.  
5. **Salva il file** – `workbook.save(...)` scrive `JsonSingleValue.xlsx` su disco.

Quando apri il file Excel generato, la cella **A1** contiene:

```
One, Two, Three
```

L'array viene visualizzato come una singola stringa separata da virgole grazie all'opzione `ArrayAsSingle`.

---

## Utilizzare i marker intelligenti di Aspose.Cells per collegare dati JSON

I marker intelligenti di Aspose.Cells sono un modo potente per mappare oggetti complessi (incluse strutture simili a JSON) direttamente sui fogli di lavoro. La sintassi `{{fieldName:Option}}` funziona in modo simile a un motore di template:

* **fieldName** – la chiave nella tua fonte dati (`Map`, POJO o `DataTable`).  
* **Option** – controlla come vengono gestite le collezioni. `ArrayAsSingle` tratta l'intera collezione come un unico valore; altre opzioni come `Array` espanderebbero l'array su più righe.

**Perché usare un marker intelligente invece di un ciclo?**  
Un ciclo richiede calcoli manuali degli indirizzi delle celle, indicizzazioni soggette a errori e codice aggiuntivo per lo stile. I marker intelligenti ti permettono di scrivere segnaposti dichiarativi, mantenere il tuo codice Java breve e lasciare che la libreria gestisca i dettagli del layout.

---

## Configurare la fonte dati Java Map

`Map<String, Object>` è il contenitore dati più semplice per Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*La chiave (`jsonArray`) deve corrispondere esattamente al nome del marker.*

Puoi anche usare un `List<String>`, un POJO personalizzato o anche una `Map` annidata per strutture JSON più complesse. Aspose.Cells attraverserà automaticamente il grafo degli oggetti.

**Suggerimento:** Se hai bisogno di formattare la stringa concatenata in modo diverso (ad esempio usando punti e virgola), preelabora l'array in Java prima di assegnarlo alla mappa:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Salvare la cartella di lavoro e verificare l'output

```java
workbook.save("JsonSingleValue.xlsx");
```

Il metodo `save` supporta molti formati (`.xlsx`, `.xls`, `.csv`, `.pdf`). Per questo tutorial manteniamo il formato predefinito Excel Open XML.

**Passaggi di verifica**

1. Apri `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc o Google Sheets.  
2. Conferma che la cella **A1** contenga `One, Two, Three`.  
3. Verifica che non siano state aggiunte righe o colonne extra – il marker intelligente ha eseguito una sostituzione in‑place.

Se la cella mostra il testo grezzo del marker (`{{jsonArray:ArrayAsSingle}}`), ricontrolla che:

* Il nome del marker corrisponda esattamente alla chiave della mappa (case‑sensitive).  
* `setSmartMarkerData` sia chiamato **dopo** che il marker è stato inserito.  
* La versione di Aspose.Cells supporti l'opzione `ArrayAsSingle` (disponibile dalla v20.3).

---

## Variazioni comuni e casi limite

| Scenario | Adjustamento |
|----------|--------------|
| **Delimitatore diverso** | Usa `ArrayAsSingle` insieme a una concatenazione personalizzata in Java (vedi il suggerimento sopra). |
| **Array multipli in un foglio** | Inserisci marker aggiuntivi come `{{anotherArray:ArrayAsSingle}}` in altre celle e aggiungi le voci corrispondenti alla mappa. |
| **Oggetti JSON annidati** | Fornisci una `Map<String, Object>` annidata; fai riferimento ai campi con notazione a punti (`{{parent.child}}`). |
| **Grandi set di dati** | Per migliaia di righe, preferisci l'opzione `Array` per consentire ad Aspose.Cells di espandere le righe automaticamente, che |

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java \| Guida alle operazioni del workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Esporta la cartella di lavoro Excel come immagine usando Aspose.Cells per Java: Guida passo‑passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Come creare e salvare una cartella di lavoro Excel come SVG usando Aspose.Cells per Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}