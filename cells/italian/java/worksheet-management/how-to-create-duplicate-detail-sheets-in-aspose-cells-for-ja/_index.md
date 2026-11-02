---
category: general
date: 2026-08-17
description: Scopri come creare fogli di dettaglio duplicati con Aspose.Cells per
  Java e consentire nomi di foglio duplicati usando SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: it
lastmod: 2026-08-17
og_description: Crea fogli di dettaglio duplicati in Aspose.Cells per Java e consenti
  nomi di foglio duplicati. Segui questo tutorial completo per risultati immediati.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Crea fogli di dettaglio duplicati in Aspose.Cells per Java – guida passo
  passo
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come creare fogli di dettaglio duplicati in Aspose.Cells per Java
url: /it/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare fogli di dettaglio duplicati in Aspose.Cells per Java

Se hai bisogno di **creare fogli di dettaglio duplicati** in una cartella di lavoro Excel, Aspose.Cells per Java lo rende semplice. Questo tutorial mostra esattamente come consentire nomi di foglio duplicati durante la generazione dei fogli di dettaglio con SmartMarkerProcessor, così puoi produrre una cartella di lavoro che contiene diversi fogli con lo stesso nome.

Vedrai un esempio completo e eseguibile, una suddivisione di ogni opzione di configurazione e consigli per gestire casi limite comuni come collisioni di nomi e set di dati di grandi dimensioni. Non sono necessari riferimenti esterni: tutto il necessario è incluso nel codice qui sotto.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java Development Kit (JDK) 8 o versioni successive.
* Maven o Gradle per gestire le dipendenze.
* Libreria Aspose.Cells per Java (versione 23.9 o successiva). Aggiungi la seguente dipendenza Maven al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Una cartella di lavoro modello (`master_template.xlsx`) che contiene una regione Smart Marker per i dati di dettaglio.

## Panoramica della soluzione

La soluzione segue quattro passaggi logici:

1. Caricare la cartella di lavoro modello.
2. Configurare `SmartMarkerProcessor` per **consentire nomi di foglio duplicati**.
3. Elaborare la cartella di lavoro in modo che venga creato un nuovo foglio di dettaglio per ogni gruppo di dati.
4. Salvare la cartella di lavoro risultante che ora contiene fogli di dettaglio duplicati.

Ogni passaggio è spiegato in dettaglio di seguito, e il file sorgente completo è fornito alla fine della guida.

## Passo 1: Caricare la cartella di lavoro modello

La prima operazione crea un'istanza `Workbook` che rappresenta il file modello. Il modello deve contenere un segnaposto Smart Marker (ad es., `&=DetailData`) che indica al processore dove inserire i dati.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Perché è importante:** Caricare il modello isola il layout e la formattazione dalla logica di generazione dei dati, mantenendo il codice pulito e facilitando il riutilizzo dello stesso modello per diversi set di dati.

## Passo 2: Configurare SmartMarkerProcessor per consentire nomi di foglio duplicati

Per impostazione predefinita, Aspose.Cells genera nomi di foglio univoci quando crea i fogli di dettaglio. Per **consentire nomi di foglio duplicati**, imposta l'opzione `DetailSheetNewName` su un valore costante. Il processore riutilizzerà questo nome per ogni foglio generato.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Perché è importante:** Impostare `DetailSheetNewName` indica al motore di riutilizzare lo stesso nome per ogni foglio di dettaglio, soddisfacendo direttamente il requisito di **consentire nomi di foglio duplicati**. Questo approccio è utile quando gli strumenti a valle identificano i fogli per posizione anziché per nome.

## Passo 3: Elaborare la cartella di lavoro per generare i fogli di dettaglio

Dopo la configurazione, invoca `process` sul workbook. Il processore legge la regione Smart Marker, crea un nuovo foglio per ogni gruppo di dati e lo popola con le righe corrispondenti.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Perché è importante:** La chiamata `process` esegue il lavoro pesante—analisi dei Smart Marker, clonazione del foglio modello e inserimento dei dati. Poiché l'opzione `DetailSheetNewName` è già impostata, ogni nuovo foglio riceve lo stesso nome, producendo nomi di foglio duplicati nel file finale.

## Passo 4: Salvare la cartella di lavoro risultante

Infine, scrivi la cartella di lavoro modificata in un nuovo file. Il file di output conterrà tante schede “DetailSheet” quanti sono i gruppi di dati.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Perché è importante:** Il salvataggio del file finalizza le modifiche apportate dal processore. La cartella di lavoro risultante può essere aperta in Microsoft Excel, LibreOffice o qualsiasi altra applicazione di fogli di calcolo che supporti il formato XLSX.

## Codice sorgente completo

Mettendo insieme tutti i pezzi, ecco il programma completo che puoi copiare, incollare ed eseguire:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Output previsto

Quando apri `duplicate_detail.xlsx`, vedrai più schede chiamate **DetailSheet**. Ogni scheda contiene il set di dati corrispondente a un gruppo specifico di Smart Marker nel modello. Layout, formattazione e formule del modello master sono preservati su ogni foglio duplicato.

## Gestione delle difficoltà comuni

| Problema | Spiegazione | Rimedio |
|----------|-------------|---------|
| Excel mostra un avviso sui nomi di foglio duplicati | Excel consente nomi duplicati ma può visualizzare un avviso all'apertura del file. | L'avviso è innocuo; la cartella di lavoro funziona correttamente. Se preferisci sopprimere l'avviso, rinomina i fogli dopo l'elaborazione usando `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Set di dati di grandi dimensioni causano alto utilizzo di memoria | Ogni foglio duplicato crea una copia completa del modello, il che può consumare RAM. | Abilita la modalità streaming con `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` prima di caricare il modello. |
| Regione Smart Marker non trovata | Il processore non riesce a individuare `&=DetailData` nel modello. | Verifica che la sintassi del segnaposto corrisponda alla fonte dati e che il foglio modello non sia nascosto. |

## Consiglio professionale: personalizzare lo schema di denominazione duplicato

Se ti serve uno schema di denominazione prevedibile mantenendo comunque i duplicati, combina un nome base con un indice:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Il segnaposto `{0}` viene sostituito dall'indice del foglio, producendo nomi come `DetailSheet_1`, `DetailSheet_2`, ecc. Questo soddisfa ancora il requisito di **consentire nomi di foglio duplicati** perché il nome base rimane costante.

## Prossimi passi

Ora che puoi **creare fogli di dettaglio duplicati**, potresti approfondire i seguenti argomenti:

* **Popolare i fogli di dettaglio con immagini** – usa gli oggetti `Picture` per inserire loghi o grafici.
* **Applicare la formattazione condizionale** – aggiungi regole `FormatCondition` per evidenziare le righe in base ai valori.
* **Esportare in PDF** – chiama `workbook.save("output.pdf", SaveFormat.PDF);` per generare una versione PDF dei fogli duplicati.

Ognuna di queste estensioni si basa sullo stesso flusso di lavoro Smart Marker mostrato qui, permettendoti di automatizzare compiti di reporting Excel complessi con sicurezza.

---

*Hai imparato come creare fogli di dettaglio duplicati in Aspose.Cells per Java e come consentire nomi di foglio duplicati usando SmartMarkerProcessor. Applica il codice, adatta il modello e integra la tecnica nei tuoi flussi di reporting.*

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea e accedi ai fogli Excel, aggiungi segnalibri PDF usando Aspose.Cells per Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Crea e accedi ai fogli Excel, aggiungi segnalibri PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Crea e accedi ai fogli Excel, aggiungi segnalibri PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}