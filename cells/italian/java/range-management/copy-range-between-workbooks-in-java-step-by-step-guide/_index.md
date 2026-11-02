---
category: general
date: 2026-08-14
description: Copia l’intervallo tra cartelle di lavoro con Java usando Aspose.Cells.
  Impara a copiare la cartella di lavoro della tabella pivot, esportare un’immagine
  in PowerPoint e rimuovere l’AutoFiltro da una tabella Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: it
lastmod: 2026-08-14
og_description: Copia intervallo tra cartelle di lavoro in Java. Questa guida mostra
  come copiare una cartella di lavoro con tabella pivot, esportare un'immagine in
  PowerPoint e rimuovere l'AutoFiltro da una tabella Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Copia intervallo tra cartelle di lavoro in Java – tutorial completo su Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Copia intervallo tra cartelle di lavoro in Java – guida passo‑passo
url: /it/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia intervallo tra cartelle di lavoro in Java – guida passo‑a‑passo

Se hai bisogno di **copiare un intervallo tra cartelle di lavoro** in Java, Aspose.Cells fornisce un'API pulita che gestisce oggetti complessi come tabelle pivot e immagini. Questo tutorial mostra come **copiare una cartella di lavoro con tabella pivot**, **esportare un'immagine in PowerPoint** e **rimuovere l'AutoFilter da una tabella Excel** mantenendo il codice facile da leggere e da mantenere.

Imparerai a:

* Caricare una cartella di lavoro di origine e definire l'intervallo di origine.  
* Creare una cartella di lavoro di destinazione e copiare l'intervallo in modo che la tabella pivot rimanga intatta.  
* Esportare la prima immagine sul foglio come oggetto PowerPoint modificabile.  
* Rimuovere un AutoFilter dalla prima tabella Excel.  
* Caricare una cartella di lavoro con `SmartMarkerOptions` per trattare gli array JSON come valore di una singola cella.

L'esempio utilizza Aspose.Cells 23.10 per Java, ma i concetti si applicano anche alle versioni precedenti.

---

## Prerequisiti

| Requisito | Perché è importante |
|-----------|----------------------|
| Java 17 o versioni successive | Richiesto dal runtime più recente di Aspose.Cells. |
| Aspose.Cells per Java (artifact Maven `com.aspose:aspose-cells`) | Fornisce le classi `Workbook`, `Worksheet`, `Range` e le classi correlate usate nel codice. |
| Un file Excel di origine (`src.xlsx`) che contiene una tabella pivot, un'immagine e una tabella con AutoFilter. | Il tutorial manipola questi oggetti per dimostrare ciascuna funzionalità. |

Aggiungi la dipendenza Maven al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copia intervallo tra cartelle di lavoro – carica sorgente e destinazione

Il primo passo è aprire la cartella di lavoro di origine, selezionare l'intervallo che contiene i dati da copiare e creare una cartella di lavoro di destinazione vuota.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Perché è importante:** Utilizzando `Range.copy`, Aspose.Cells copia non solo i valori grezzi delle celle ma anche la cache pivot sottostante, mantenendo la tabella pivot funzionale nella cartella di lavoro di destinazione.

---

## Copia la cartella di lavoro con tabella pivot durante la copia dell'intervallo

Ora copia l'intervallo definito dalla cartella di lavoro di origine a quella di destinazione. La tabella pivot viene preservata automaticamente perché l'intervallo include la cache pivot.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Risultato:** Aprendo `destination.xlsx` si vede lo stesso layout della tabella pivot di `src.xlsx`. Non è necessario alcun codice aggiuntivo per ricostruire la cache pivot.

---

## Esporta immagine in PowerPoint

Aspose.Cells può contrassegnare un'immagine per l'esportazione a un oggetto PowerPoint modificabile. Il codice seguente seleziona la prima immagine sul foglio di destinazione e imposta il flag di esportazione.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Ciò che vedi:** Aprendo `destination.pptx` in PowerPoint l'immagine appare come forma nativa che puoi modificare, ridimensionare o animare.

---

## Rimuovi AutoFilter da una tabella Excel

Se il foglio di origine contiene una tabella con AutoFilter, potresti volerlo eliminare dopo la copia. Il codice qui sotto accede alla prima tabella e ne rimuove il filtro.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effetto:** La tabella rimane nella cartella di lavoro, ma le frecce a discesa del filtro scompaiono, offrendoti una visualizzazione dei dati pulita.

---

## Carica cartella di lavoro con opzioni SmartMarker – trattare gli array JSON come una singola cella

Quando generi un report da JSON, Aspose.Cells può trattare un intero array come valore di una singola cella. Questo è utile per incorporare stringhe JSON in un modello senza espanderle in più celle.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Perché potresti usarlo:** Se il tuo payload JSON contiene un array che deve apparire come stringa JSON in una singola cella, `setArrayAsSingle(true)` impedisce ad Aspose.Cells di espandere l'array in righe o colonne separate.

---

![Copia intervallo tra cartelle di lavoro in Java – esempio di codice Aspose.Cells](copy-range-workbooks.png)

*Testo alternativo dell'immagine:* **Copia intervallo tra cartelle di lavoro in Java – esempio di codice Aspose.Cells** (corrisponde alla parola chiave principale).

---

## Output previsto

| Nome file                | Contiene |
|--------------------------|----------|
| `destination.xlsx`       | Intervallo copiato con tabella pivot funzionale. |
| `destination.pptx`       | Immagine esportata come forma PowerPoint modificabile. |
| `final_output.xlsx`      | Tabella senza frecce AutoFilter. |
| `template_filled.xlsx`   | Array JSON memorizzato come valore di una singola cella. |

Apri ciascun file nell'applicazione appropriata (Excel o PowerPoint) per verificare che le operazioni siano riuscite.

---

## Conclusione

Ora sai come **copiare un intervallo tra cartelle di lavoro** in Java usando Aspose.Cells, preservando una tabella pivot, esportando un'immagine in PowerPoint e rimuovendo un AutoFilter da una tabella Excel. Lo stesso schema può essere esteso per copiare qualsiasi intervallo Excel in una nuova cartella di lavoro, gestire gli array JSON di SmartMarker o concatenare trasformazioni aggiuntive.

Passi successivi che potresti esplorare:

* **Copia intervallo Excel in una nuova cartella di lavoro** con più fogli.  
* Usa **esporta immagine in PowerPoint** per l'estrazione batch di immagini.  
* Applica **rimuovi autofilter da tabella excel** in pipeline di reporting più ampie.  
* Combina queste tecniche con Aspose.Slides per un'automazione completa da Excel a PowerPoint.

Sentiti libero di sperimentare con diversi indirizzi di intervallo, più tabelle pivot o formati immagine personalizzati. L'API di Aspose.Cells è progettata per la flessibilità programmatica, così puoi adattare i pattern mostrati qui a qualsiasi scenario di automazione Excel aziendale.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑a‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Copia immagini tra fogli in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copia impostazioni di configurazione pagina tra fogli di lavoro in Excel usando Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Copia fogli di lavoro Excel tra cartelle di lavoro](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}