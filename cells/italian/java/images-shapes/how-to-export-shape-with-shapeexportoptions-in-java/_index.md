---
category: general
date: 2026-10-01
description: Scopri come esportare una forma con ShapeExportOptions in Java, mantenendo
  la forma modificabile durante la conversione in PPTX utilizzando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: it
lastmod: 2026-10-01
og_description: Esporta una forma con ShapeExportOptions in Java per creare file PPTX
  modificabili. Questo tutorial ti guida attraverso l’intero processo usando Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Esporta forma con ShapeExportOptions in Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Come esportare una forma con ShapeExportOptions in Java
url: /it/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare una forma con ShapeExportOptions in Java

Se hai bisogno di **esportare una forma con ShapeExportOptions** da una cartella di lavoro Excel, questa guida ti mostra i passaggi esatti. Vedrai come mantenere la forma modificabile quando la converti in un file PPTX, il che è essenziale per la modifica successiva in PowerPoint.

Esportare forme è un'operazione comune quando generi presentazioni da fogli di calcolo—che tu stia creando deck di vendita, dashboard di reportistica o presentazioni automatizzate. Questo tutorial copre tutto ciò di cui hai bisogno, dalla configurazione del progetto alla verifica del file esportato, e utilizza la libreria **Aspose.Cells for Java**.

## Cosa ti servirà

- Java 17 o versioni successive (il codice si compila con qualsiasi JDK recente)
- Maven o Gradle per la gestione delle dipendenze
- Un file Excel (`Shapes.xlsx`) che contiene almeno una casella di testo o un'altra forma
- Familiarità di base con le API di Aspose.Cells

## Passo 1: Aggiungi Aspose.Cells al tuo progetto (Aspose Cells export shape)

Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Per Gradle, inserisci questo in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Consiglio:** Registra la tua licenza subito per evitare filigrane di valutazione.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Passo 2: Carica la cartella di lavoro che contiene la forma

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

L'oggetto `Workbook` rappresenta l'intero file Excel. Caricarlo è il primo requisito per qualsiasi manipolazione di forme.

## Passo 3: Accedi al foglio di lavoro e recupera la forma desiderata (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Perché è importante:** Le forme sono memorizzate per foglio, quindi devi navigare al foglio corretto prima di poter esportare una forma specifica.

## Passo 4: Configura **ShapeExportOptions** per mantenere la forma modificabile (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

Impostare `ExportAsEditable` a `true` indica ad Aspose.Cells di preservare i dati vettoriali della forma, consentendo agli utenti di PowerPoint di modificare la forma dopo l'importazione.

## Passo 5: Esporta la forma direttamente in un file PPTX (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

Il metodo `exportToImage` funziona per diversi formati immagine; quando il nome del file di destinazione termina con `.pptx`, Aspose.Cells scrive una diapositiva PowerPoint che contiene la forma.

### Risultato atteso

- `textbox.pptx` appare nella directory specificata.
- Aprendo il file in PowerPoint viene mostrata una singola diapositiva con la casella di testo originale.
- La casella di testo è completamente modificabile (puoi cambiare testo, carattere, dimensione, ecc.).

## Passo 6: Verifica l'output e gestisci i casi limite comuni

### Verifica programmaticamente

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

Se `slideCount` è uguale a `1`, l'esportazione è riuscita.

### Caso limite: più forme

Se il foglio contiene diverse forme e ne vuoi una specifica, individuala per nome:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Caso limite: forma non trovata

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Caso limite: esportare in altri formati

`ShapeExportOptions` supporta anche PNG, JPEG, SVG e EMF. Cambia l'estensione del file e opzionalmente imposta `exportOptions.setImageFormat(ImageFormat.PNG)`.

## Esempio completo, eseguibile

Mettere insieme tutti i pezzi ti fornisce un programma autonomo che puoi copiare‑incollare nel tuo IDE:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

Eseguendo il programma si crea `textbox.pptx`. Aprilo in PowerPoint, fai clic destro sulla casella di testo e vedrai le consuete maniglie di modifica—confermando che **export shape with ShapeExportOptions** ha preservato la modificabilità.

## Domande frequenti

| Domanda | Risposta |
|----------|--------|
| *Posso esportare una forma di grafico?* | Sì. La stessa chiamata `exportToImage` funziona per grafici, immagini e SmartArt. |
| *E se ho bisogno di un PNG a risoluzione più alta?* | Imposta `options.setImageFormat(ImageFormat.PNG)` e regola `options.setResolution(300)` prima dell'esportazione. |
| *Il PPTX esportato è compatibile con versioni più vecchie di PowerPoint?* | La libreria scrive Office Open XML (PPTX) che è supportato da PowerPoint 2007 e versioni successive. |
| *È necessaria una licenza per far funzionare tutto?* | Una valutazione gratuita funziona ma aggiunge una filigrana. Registra una licenza per rimuoverla. |

## Prossimi passi

- Esplora **Aspose.Slides for Java** se devi combinare più forme esportate in un unico deck di diapositive.
- Usa **ShapeExportOptions.setExportAsEditable(false)** quando preferisci un'immagine raster (PNG/JPEG) per un rendering più veloce.
- Automatizza l'elaborazione batch: cicla attraverso tutti i fogli di lavoro ed esporta ogni forma in file PPTX separati.

---

### Conclusione

Ora sai come **export shape with ShapeExportOptions** in Java, preservando la modificabilità quando converti una casella di testo (o qualsiasi altra forma) in un file PPTX. Seguendo i passaggi sopra—configurando la libreria, caricando la cartella di lavoro, configurando `ShapeExportOptions` e invocando `exportToImage`—puoi integrare l'esportazione di forme in qualsiasi pipeline di reportistica automatizzata.

Sentiti libero di sperimentare con forme diverse, formati di output e impostazioni di risoluzione. Se hai trovato utile questa guida, condividila con i colleghi o aggiungila ai preferiti per riferimento futuro. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come regolare i margini delle forme in Excel usando Aspose.Cells per Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [Come applicare la formattazione 3D alle forme in Excel usando Aspose.Cells per Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Guida alla copia di forme del workbook Aspose Cells Java](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}