---
category: general
date: 2026-08-11
description: Crea un nuovo workbook Aspose in Java, aggiungi una proprietà personalizzata
  Excel, quindi salva il workbook come XLSB con un esempio completo passo‑passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: it
lastmod: 2026-08-11
og_description: Crea un nuovo workbook Aspose in Java, aggiungi una proprietà personalizzata
  Excel e salva il workbook come XLSB con un esempio completo, pronto all'uso.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Crea nuova cartella di lavoro Aspose – aggiungi proprietà personalizzata
  Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Crea nuovo workbook Aspose – aggiungi proprietà personalizzata Excel e salva
  come XLSB
url: /it/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea nuovo workbook Aspose – aggiungi proprietà personalizzata Excel e salva come XLSB

Se devi **creare un nuovo workbook Aspose** in un'applicazione Java, questa guida ti mostra esattamente come farlo. Imparerai a **aggiungere una proprietà personalizzata Excel**, a recuperarne il valore e a **salvare il workbook come XLSB** senza perdere alcun metadato.

Il tutorial copre tutto, dalla configurazione del progetto alla verifica del file salvato. Non è necessaria alcuna documentazione esterna; basta seguire i passaggi e eseguire il codice.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Java Development Kit (JDK) 8 o superiore installato.  
- Maven o Gradle per gestire le dipendenze (l'esempio utilizza Maven).  
- Una licenza attiva di Aspose.Cells per Java (oppure usa la modalità di valutazione gratuita per i test).

## Passo 1: Aggiungi Aspose.Cells al tuo progetto

Aggiungi l'artifact Maven di Aspose.Cells al tuo `pom.xml`. Questa dipendenza fornisce le classi necessarie per **creare un nuovo workbook Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Suggerimento:** Se preferisci Gradle, sostituisci lo snippet Maven con la riga equivalente `implementation "com.aspose:aspose-cells:23.12"`.

## Passo 2: Crea un nuovo workbook Aspose

Il primo passo funzionale è istanziare un oggetto `Workbook`. Questo oggetto rappresenta un file Excel in memoria ed è il punto di ingresso per tutte le operazioni successive.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Creare un nuovo workbook Aspose ti fornisce un workbook vuoto con un foglio di lavoro predefinito, pronto per le personalizzazioni.

## Passo 3: Aggiungi proprietà personalizzata Excel

Le proprietà personalizzate ti consentono di memorizzare metadati arbitrari all'interno di un file Excel. Qui **aggiungiamo una proprietà personalizzata Excel** chiamata `ProjectId` con un valore numerico.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

Il metodo `add` accetta un nome di proprietà e un valore di qualsiasi tipo supportato (stringa, numero, data, ecc.). Questi metadati viaggiano con il file ovunque lo copi.

## Passo 4: Recupera e visualizza la proprietà personalizzata

Leggere nuovamente la proprietà verifica che sia stata memorizzata correttamente. Puoi anche utilizzare il valore recuperato nella tua logica di business.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Il cast a `int` funziona perché abbiamo memorizzato un valore numerico. Se memorizzi una stringa, usa `(String)` al suo posto.

## Passo 5: Salva il workbook come XLSB

Ora **salvi il workbook come XLSB**. Il formato XLSB memorizza il workbook in una rappresentazione binaria, più veloce da aprire e più piccola su disco. Tutte le proprietà personalizzate vengono preservate automaticamente.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Sostituisci `"WithCustomProps.xlsb"` con un percorso assoluto se devi salvare il file in una directory specifica. L'enum `SaveFormat.XLSB` indica ad Aspose.Cells di scrivere il formato binario.

## Passo 6: Verifica l'output

Esegui il programma dal tuo IDE o da riga di comando:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Dovresti vedere:

```
ProjectId = 12345
```

Apri `WithCustomProps.xlsb` in Excel. Vai su **File → Info → Proprietà → Proprietà avanzate → Personalizzate**. L'elemento `ProjectId` con valore `12345` sarà elencato, confermando che il passaggio **add custom property excel** è riuscito e che l'operazione **save workbook as xlsb** ha mantenuto i metadati.

## Domande comuni e casi particolari

### E se devo memorizzare una proprietà di tipo stringa?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Recuperala con:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Posso aggiungere più proprietà personalizzate contemporaneamente?

Sì. Chiama `add` ripetutamente per ogni coppia nome/valore. Aspose.Cells non limita il numero di proprietà personalizzate, ma mantieni la dimensione totale ragionevole per evitare di gonfiare il file.

### Come influisce il formato binario sulle prestazioni?

I file XLSB si caricano più rapidamente perché evitano il parsing XML. Questo è particolarmente evidente per workbook con molte righe, formule o immagini incorporate.

### E se devo lavorare con un file XLSX esistente?

Sostituisci il costruttore `new Workbook()` con `new Workbook("ExistingFile.xlsx")`. Il resto dei passaggi (aggiunta delle proprietà, salvataggio come XLSB) rimane identico.

## Codice sorgente completo

Di seguito trovi l'esempio completo, pronto per l'esecuzione. Copialo in un file chiamato `CustomPropertiesXlsb.java` nella cartella `src/main/java`.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Eseguendo questa classe otterrai un file XLSB che contiene la proprietà personalizzata e può essere aperto con qualsiasi versione moderna di Microsoft Excel.

## Conclusione

Ora sai come **creare un nuovo workbook Aspose**, **aggiungere una proprietà personalizzata Excel** e **salvare il workbook come XLSB** usando Java. L'esempio dimostra l'intero ciclo di vita: inizializzazione, iniezione di metadati, verifica e serializzazione binaria.

Successivamente, esplora argomenti correlati come **impostare le proprietà del documento**, **lavorare con le formule Excel** o **convertire tra XLSX e XLSB**. Ognuno di questi si basa sulla stessa API Aspose.Cells che hai appena utilizzato, così potrai estendere la soluzione senza dover apprendere nuove librerie.

Sentiti libero di sperimentare con diversi tipi di dati, più fogli di lavoro o protezione con password—Aspose.Cells supporta tutti questi scenari out of the box. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}