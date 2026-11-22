---
category: general
date: 2026-11-22
description: Converti Excel in PowerPoint in Java usando Aspose.Cells. Scopri come
  creare PowerPoint da un file Excel, esportare i fogli di lavoro come diapositive
  PPTX e automatizzare le presentazioni.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: it
lastmod: 2026-11-22
og_description: Converti Excel in PowerPoint in Java con Aspose.Cells. Questo tutorial
  ti mostra come creare PowerPoint da un file Excel ed esportare file .xlsx in diapositive
  .pptx.
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: Converti Excel in PowerPoint in Java – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: Converti Excel in PowerPoint con Java – guida passo passo
url: /it/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti Excel in PowerPoint in Java – guida passo‑passo

Se hai bisogno di **convertire Excel in PowerPoint in Java**, questa guida ti mostra come farlo con Aspose.Cells. Che tu stia costruendo un motore di reporting o automatizzando le presentazioni, imparerai a **creare PowerPoint da un file Excel** programmaticamente ed esportare ogni foglio di lavoro come slide PPTX modificabili.

Il tutorial copre tutto, dalla configurazione del progetto al salvataggio della presentazione finale. Alla fine avrai un programma Java eseguibile che converte una cartella di lavoro `.xlsx` in un file `.pptx` che puoi modificare in Microsoft PowerPoint. Non è necessario alcun copia‑incolla manuale.

## Prerequisiti

* Java 17 o versioni successive installato (il codice utilizza il moderno sistema di moduli).  
* Una licenza Aspose.Cells per Java o una chiave di valutazione temporanea.  
* Maven o Gradle per la gestione delle dipendenze (l'esempio utilizza Maven).  
* Un file Excel di esempio (`input.xlsx`) posizionato in una directory nota.

> **Consiglio professionale:** Aspose.Cells supporta sia `.xls` che `.xlsx`. Lo stesso codice funziona per entrambi i formati; basta cambiare l'estensione del file.

## Passo 1: Configura il progetto Java per **convertire Excel in PowerPoint**

Crea un nuovo progetto Maven (o aggiungilo a uno esistente) e includi la dipendenza Aspose.Cells:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

Esegui `mvn clean install` per scaricare la libreria. Se possiedi un file di licenza (`Aspose.Total.lic`), posizionalo nella cartella `src/main/resources`; il codice lo caricherà automaticamente.

## Passo 2: Carica la cartella di lavoro Excel

Il primo passo funzionale nel processo di **convertire la cartella di lavoro Excel in slide PPTX** è caricare il file sorgente. Aspose.Cells può aprire file dal file system, da uno stream o anche da un array di byte.

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**Perché è importante:** Caricare la cartella di lavoro valida il formato del file e prepara le strutture interne che Aspose.Cells tradurrà successivamente in oggetti PowerPoint.

## Passo 3: Configura le opzioni di salvataggio per **creare PowerPoint da un file Excel**

Aspose.Cells utilizza `ImageOrPrintOptions` per definire il formato di output durante la conversione in file di presentazione. Imposta `SaveFormat` su `SaveFormat.PPTX` per generare slide modificabili.

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**Perché è importante:** Il flag `setOnePagePerSheet(false)` indica ad Aspose.Cells di trattare ogni foglio di lavoro come una slide individuale, lo scenario più comune quando **converti Excel in PowerPoint** per le presentazioni.

## Passo 4: Salva la cartella di lavoro come slide PPTX

Ora puoi scrivere la presentazione su disco. Il metodo `Workbook.save` accetta il percorso di output e le opzioni configurate.

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

Quando apri `editable.pptx` in Microsoft PowerPoint, vedrai una slide per ogni foglio di lavoro, con tutte le celle renderizzate come caselle di testo e forme modificabili. Puoi modificare ulteriormente caratteri, colori o aggiungere animazioni direttamente in PowerPoint.

### Output previsto

Eseguendo il programma stampa:

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

E il file `editable.pptx` appare nella directory specificata, pronto per modifiche manuali o ulteriori automazioni.

## Passo 5: Varianti comuni e casi limite

### Convertire solo i fogli selezionati

Se vuoi **convertire la cartella di lavoro Excel in slide PPTX** ma escludere alcuni fogli, filtrali prima del salvataggio:

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### Gestire cartelle di lavoro di grandi dimensioni

Per cartelle di lavoro con molti fogli, il consumo di memoria può diventare significativo. Usa `WorkbookSettings` per abilitare lo streaming:

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### Conservare le formule

Aspose.Cells valuta le formule prima del rendering. Se hai bisogno del testo grezzo della formula sulla slide, imposta `opts.setExportFormulas(true)`.

## Passo 6: Verifica il risultato programmaticamente (opzionale)

Puoi caricare il PPTX generato con Aspose.Slides per confermare che il numero di slide corrisponda al numero di fogli di lavoro:

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

Questo controllo aggiuntivo è utile nelle pipeline CI dove vuoi verificare che la conversione sia avvenuta con successo.

## Conclusione

Ora hai una soluzione completa, pronta per la produzione, per **convertire Excel in PowerPoint in Java**. Il programma carica una cartella di lavoro `.xlsx`, configura `ImageOrPrintOptions` per **creare PowerPoint da un file Excel** e salva il risultato come slide PPTX modificabili. Regolando le opzioni puoi perfezionare la risoluzione, selezionare fogli specifici o streammare file di grandi dimensioni, rendendo l'approccio flessibile per molti scenari di automazione.

**Passi successivi**

* Approfondisci **java convert .xlsx to .pptx** aggiungendo layout di slide personalizzati con Aspose.Slides.  
* Automatizza l'elaborazione batch di più cartelle di lavoro usando un semplice watcher di directory.  
* Combina questa conversione con la generazione di grafici basati sui dati per produrre presentazioni dinamiche.

Sentiti libero di sperimentare con le impostazioni e condividere i tuoi risultati. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti Excel in PowerPoint con Aspose.Cells in Java](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [Come convertire Excel in PowerPoint usando Aspose.Cells per .NET: Guida completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Converti Excel in PowerPoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}