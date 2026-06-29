---
category: general
date: 2026-06-27
description: Esporta la tabella pivot come immagine pivot di Excel in Java. Scopri
  come impostare il formato PNG, configurare le opzioni e salvare il file in pochi
  passaggi.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: it
og_description: Esporta la tabella pivot come immagine pivot di Excel usando Java.
  Questa guida mostra come impostare il formato PNG e salvare l'immagine con sicurezza.
og_title: Esporta tabella pivot in PNG in Java – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Esporta tabella pivot in PNG in Java – Guida completa di programmazione
url: /it/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta tabella pivot in PNG con Java – Guida completa alla programmazione

Hai mai avuto bisogno di **esportare una tabella pivot** da una cartella di lavoro Excel ma non sapevi come ottenere un file immagine pulito? Non sei l'unico—molti sviluppatori incontrano questo ostacolo quando costruiscono dashboard di reporting. La buona notizia è che con poche righe di codice Java puoi trasformare qualsiasi tabella pivot in una nitida **immagine pivot di Excel** salvata come PNG.  

In questo tutorial percorreremo l’intero processo: lettura della cartella di lavoro, individuazione della prima tabella pivot, configurazione dell’esportazione per **impostare il formato PNG**, e infine scrittura dell’immagine su disco. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto.

## Cosa imparerai

- Come caricare un file Excel con Aspose.Cells (o Apache POI se preferisci).  
- Le chiamate API esatte necessarie per **esportare la tabella pivot** come PNG.  
- Perché impostare il formato immagine è importante e come **impostare correttamente il formato PNG**.  
- Problemi comuni—come gestire più tabelle pivot o fogli di lavoro mancanti—e come evitarli.  
- Un esempio Java completo, pronto‑da‑eseguire, che puoi copiare‑incollare.

> **Prerequisiti**  
> • Java 17 o versione più recente (il codice funziona anche con versioni precedenti, ma 17 è consigliata).  
> • Libreria Aspose.Cells per Java (la versione di prova gratuita è sufficiente).  
> • Familiarità di base con i file Excel e con Java I/O.

---

## Passo 1: Aggiungi la dipendenza Aspose.Cells

Se usi Maven, inserisci la seguente dipendenza nel tuo `pom.xml`. In alternativa, scarica il JAR dal sito Aspose e aggiungilo al classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Suggerimento:* Mantieni le versioni delle librerie sincronizzate con le note di rilascio ufficiali per evitare bug inaspettati.

## Passo 2: Carica la cartella di lavoro e individua la tabella pivot

Prima apriamo il file Excel, poi recuperiamo la prima tabella pivot sul primo foglio di lavoro. Se la cartella di lavoro non contiene tabelle pivot, usciamo in modo pulito.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Perché questo passo è importante** – L’oggetto `PivotTable` è il punto di ingresso per qualsiasi esportazione di immagine. Tentare di chiamare `toImage` su una pivot inesistente genererà una `NullPointerException`, per questo controlliamo prima il conteggio.

## Passo 3: Configura le opzioni di esportazione immagine (Imposta formato PNG)

Ora creiamo un’istanza di `ImageOrPrintOptions` e impostiamo esplicitamente **il formato PNG**. PNG è loss‑less, il che preserva la nitidezza delle linee della griglia e dei caratteri.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Nota:* Se ti serve invece un JPEG, basta sostituire `ImageFormat.PNG` con `ImageFormat.JPEG`. Lo stesso oggetto opzioni funziona per entrambi i formati.

## Passo 4: Esporta la tabella pivot come file immagine

Con le opzioni pronte, chiamiamo `toImage`. Il metodo scrive direttamente il file, quindi non sono necessari stream aggiuntivi.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

L’esecuzione del programma produce un file chiamato `pivot.png` che appare esattamente come la pivot che vedi in Excel. Aprilo con qualsiasi visualizzatore di immagini per verificare.

### Output previsto

```
Pivot table exported successfully to: C:/exports/pivot.png
```

L’immagine risultante corrisponderà al layout sullo schermo, includendo larghezze delle colonne, altezze delle righe e qualsiasi formattazione condizionale applicata.

## Gestione di più tabelle pivot (Avanzato)

E se il tuo foglio contiene diverse tabelle pivot e ne vuoi esportare una specifica? Puoi iterare su `ws.getPivotTables()` e selezionare per nome:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Perché è utile*: Nei report reali spesso hai una pivot di riepilogo più una dettagliata. Selezionare per nome evita sovrascritture accidentali.

## Problemi comuni e come evitarli

| Problema | Sintomo | Soluzione |
|------|----------|-----|
| **Foglio mancante** | `IndexOutOfBoundsException` durante l’accesso a `ws` | Verifica `workbook.getWorksheets().getCount() > 0` prima di indicizzare. |
| **Nessuna tabella pivot** | Fallimento silenzioso o immagine vuota | Usa il controllo `ws.getPivotTables().getCount()` (vedi Passo 2). |
| **Formato immagine errato** | L’output appare sfocato o con artefatti | Imposta sempre `setImageFormat(ImageFormat.PNG)` per un output lossless; evita JPEG per tabelle ricche di testo. |
| **Percorso file non scrivibile** | `IOException` in `toImage` | Assicurati che la directory esista (`new File(outputPath).getParentFile().mkdirs()`). |

## Suggerimento: Esporta in un array di byte per le app web

Se stai costruendo un servizio web che restituisce il PNG direttamente al browser, puoi scrivere su un `ByteArrayOutputStream` invece che su un file:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Questo elimina la necessità di file temporanei e velocizza la risposta.

---

## Esempio completo funzionante (tutti i passi combinati)

Di seguito trovi il programma completo, pronto‑da‑copiare‑incollare, che include tutte le migliori pratiche discusse.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

L’esecuzione di questa classe genererà `pivot.png` all’interno di `C:/exports`. Apri il file e vedrai una replica visiva esatta della tabella pivot originale—perfetta per incorporarla in report, email o pagine web.

![Tabella pivot esportata salvata come PNG – esempio di immagine pivot di Excel](https://example.com/images/pivot-export.png "esempio di esportazione della tabella pivot")

*Testo alternativo dell'immagine:* **esempio di esportazione della tabella pivot che mostra un'immagine PNG di una pivot Excel**

## Conclusione

Ti abbiamo appena mostrato come **esportare una tabella pivot** da Excel in un PNG di alta qualità usando Java. I passaggi chiave sono caricare la cartella di lavoro, individuare la pivot, configurare `ImageOrPrintOptions` per **impostare il formato PNG**, e infine chiamare `toImage`.  

Con queste conoscenze puoi ora automatizzare la generazione di report, incorporare snapshot di pivot nei dashboard, o servirli direttamente da un’API web. Prossimamente potresti esplorare le opzioni di scaling dell’**immagine pivot di Excel**, aggiungere filigrane, o persino convertire il PNG in PDF per report stampabili.  

Hai domande sulla gestione di cartelle di lavoro più grandi o sull’integrazione con Spring Boot? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiornare l'origine della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatizzare lo stile e il salvataggio della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Manipolazione della tabella pivot Excel con Aspose.Cells Java: Guida completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}