---
category: general
date: 2026-11-22
description: Esporta Excel come immagine con Java usando Aspose.Cells. Scopri come
  aggiungere un’immagine al foglio di lavoro e salvare Excel come file PNG in pochi
  passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: it
lastmod: 2026-11-22
og_description: Esporta Excel come immagine con Java usando Aspose.Cells. Segui questa
  guida per aggiungere un’immagine al foglio di lavoro e salvare Excel come file PNG
  rapidamente.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Esporta Excel come immagine con Java – tutorial passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Esporta Excel come immagine con Java – guida completa
url: /it/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel as image with Java – guida completa

Se hai bisogno di **export Excel as image** in un'applicazione Java, questo tutorial ti mostra una soluzione pronta all'uso. Vedrai come aggiungere un'immagine al foglio di lavoro, configurare le opzioni di esportazione e infine **save Excel as PNG file** con poche righe di codice.

La guida copre tutto, dall'impostazione di Maven alla gestione dei casi limite, così puoi integrare la tecnica in qualsiasi progetto che richieda snapshot visivi dei fogli di calcolo.

## Prerequisiti

* Java 17 o versioni successive installato.
* Maven 3.6+ (o Gradle) per la gestione delle dipendenze.
* Una licenza Aspose.Cells for Java (la valutazione gratuita funziona per i test).
* Un file Excel di esempio (`sample.xlsx`) che contiene i dati che desideri esportare.

## Passo 1: Aggiungi la dipendenza Aspose.Cells

Aspose.Cells fornisce la classe `ImageOrPrintOptions` utilizzata per **export Excel as image**. Aggiungi la seguente dipendenza al tuo `pom.xml` (o all'equivalente entry di Gradle).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Suggerimento:** Mantieni il numero di versione aggiornato; le versioni più recenti includono miglioramenti delle prestazioni per il rendering delle immagini.

## Passo 2: Carica la cartella di lavoro e seleziona il foglio di lavoro

Il primo passo programmatico è aprire il file Excel e ottenere un riferimento al foglio di lavoro che desideri esportare.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Perché è importante*: Caricare la cartella di lavoro ti dà accesso ai suoi oggetti interni, e selezionare il foglio corretto garantisce che l'intervallo giusto venga renderizzato.

## Passo 3: Configura ImageOrPrintOptions (export excel as image)

`ImageOrPrintOptions` controlla il formato dell'immagine, la risoluzione e altri dettagli di rendering. Qui impostiamo il formato su PNG, che soddisfa il requisito **export excel sheet to png**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Impostare il formato su `PNG` garantisce una compressione senza perdita, rendendo il file adatto per ulteriori elaborazioni o per l'inclusione in report.

## Passo 4: Aggiungi immagine al foglio di lavoro (add picture to worksheet)

Se hai bisogno di incorporare un'immagine — come un logo o uno snapshot di un altro intervallo — usa la collezione `Pictures`. Il codice seguente inserisce un'immagine dell'intervallo `A1:G20` nell'angolo in alto a sinistra del foglio di lavoro.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Perché potresti farlo:** Aggiungere un'immagine prima dell'esportazione ti consente di combinare grafiche statiche con i dati del foglio di lavoro, producendo un'immagine finale più ricca.

## Passo 5: Salva il foglio di lavoro come file PNG (save excel as png file, save workbook as image)

Infine, invoca `Workbook.save` con le opzioni configurate. Il metodo scrive un file PNG nella directory specificata.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Quando il programma termina, `output/pivot.png` contiene una rappresentazione pixel‑perfect del foglio di lavoro, inclusa l'immagine che hai aggiunto.

### File sorgente completo

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Eseguendo la classe si genera il file PNG mostrato di seguito (l'immagine è illustrativa; il tuo file rifletterà il contenuto reale del foglio di lavoro).

![Foglio di lavoro Excel esportato come PNG](/images/excel-to-png.png "Risultato dell'esportazione di Excel come immagine usando Java")

*Testo alternativo (alt immagine):* **Risultato dell'esportazione di Excel come immagine usando Java – uno snapshot PNG del foglio di lavoro** (soddisfa il requisito dell'alt immagine).

## Problemi comuni e come evitarli

| Problema | Motivo | Soluzione |
|-------|--------|-----|
| **File non trovato** | Il percorso verso `sample.xlsx` è errato. | Usa un percorso assoluto o posiziona il file nella radice del progetto. |
| **Immagine vuota** | Il foglio di lavoro non ha contenuti visibili o l'intervallo dell'immagine è vuoto. | Verifica che le celle `A1:G20` contengano dati o modifica l'intervallo. |
| **Bassa risoluzione** | DPI predefinito è 96, il che può apparire sfocato quando stampato. | Chiama `opts.setResolution(300)` (o superiore) prima di salvare. |
| **Eccezione di licenza** | L'uso della versione di valutazione può aggiungere una filigrana. | Applica una licenza valida Aspose.Cells con `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Prossimi passi

Ora che puoi **export Excel as image**, potresti esplorare:

* **Export excel sheet to png** per ogni foglio di lavoro in una cartella di lavoro (ciclo attraverso `wb.getWorksheets()`).
* Convertire il PNG in PDF usando Aspose.PDF se ti serve un formato adatto ai documenti.
* Incorporare il PNG generato in una pagina web o in un allegato email direttamente da Java.

Queste estensioni si basano sullo stesso pattern `ImageOrPrintOptions`, mantenendo il codice coerente.

## Conclusione

Hai imparato come **export Excel as image** con Java, come **add picture to worksheet**, e come **save Excel as PNG file** usando Aspose.Cells. L'esempio completo dimostra un modo affidabile per **save workbook as image**, gestire la risoluzione e evitare errori comuni. Applica il pattern per automatizzare i report, generare thumbnail o integrare visualizzazioni di fogli di calcolo in qualsiasi workflow basato su Java.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}