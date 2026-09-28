---
category: general
date: 2026-09-27
description: Come esportare un foglio Excel in PowerPoint con Aspose.Cells in Java
  – una guida passo passo che mostra anche come convertire una cartella di lavoro
  Excel in una presentazione PowerPoint.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: it
lastmod: 2026-09-27
og_description: Come esportare un foglio Excel in PowerPoint usando Aspose.Cells in
  Java. Impara a convertire una cartella di lavoro Excel in una presentazione PowerPoint
  con il codice completo.
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: Come esportare un foglio Excel in PowerPoint – Guida Java con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: Come esportare un foglio Excel in PowerPoint con Aspose.Cells in Java
url: /it/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare un foglio Excel in PowerPoint con Aspose.Cells in Java

Se hai bisogno di **come esportare un foglio Excel in PowerPoint**, questo tutorial ti fornisce una soluzione completa, pronta all'uso. Vedrai esattamente come **convertire una cartella di lavoro Excel in una presentazione PowerPoint** preservando le caselle di testo modificabili e la formattazione di base.

La guida presuppone che tu abbia un ambiente di sviluppo Java funzionante e una licenza valida di Aspose.Cells per Java. Alla fine dell'articolo avrai un programma Java che carica una cartella di lavoro Excel, esporta il primo foglio di lavoro e scrive un file `.pptx` che può essere aperto e modificato in Microsoft PowerPoint.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------------|
| Java 17 o successivo | Aspose.Cells supporta runtime Java moderni e offre migliori prestazioni. |
| Aspose.Cells per Java (versione 23.10 o successiva) | La libreria contiene il sovraccarico `Workbook.save(..., SaveFormat.PPTX)` usato per la conversione. |
| Una copia con licenza di Aspose.Cells | Senza licenza la libreria funziona in modalità di valutazione e aggiunge filigrane. |
| Un file Excel che contiene almeno una casella di testo modificabile | La conversione preserva la casella di testo come forma modificabile in PowerPoint. |
| IDE o strumento di build (es., Maven, Gradle) | Per compilare ed eseguire il codice di esempio. |

## Passo 1: Aggiungere Aspose.Cells al tuo progetto

Se usi Maven, aggiungi la seguente dipendenza a `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Per Gradle, inserisci questo snippet in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Suggerimento:** Dichiarare la dipendenza nello scope `provided` se hai bisogno della libreria solo a runtime su un server.

## Passo 2: Preparare la cartella di lavoro Excel

Crea un file Excel (`WorkbookWithTextbox.xlsx`) che contenga una casella di testo modificabile nel primo foglio di lavoro. La casella di testo può essere inserita in Excel tramite **Insert → Text Box**. Salva il file in una directory a cui puoi fare riferimento da Java, ad esempio `src/main/resources`.

## Passo 3: Scrivere il codice di conversione

Crea una classe Java chiamata `ExportEditableTextbox`. Il codice qui sotto include tutti gli import, la gestione degli errori e commenti che spiegano ogni operazione.

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### Perché funziona

* `Workbook` rappresenta l'intero file Excel. Il suo caricamento analizza tutti i fogli di lavoro, i grafici e le forme.  
* `workbook.save(..., SaveFormat.PPTX)` attiva il motore di conversione integrato di Aspose.Cells. Il motore mappa celle, righe e forme di Excel su diapositive PowerPoint, preservando le caselle di testo modificabili come forme PowerPoint.  
* Il metodo scrive una singola diapositiva per foglio di lavoro. In questo esempio il primo foglio di lavoro diventa l'unica diapositiva.

## Passo 4: Eseguire il programma

Compila ed esegui la classe con il tuo strumento di build:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

oppure, se usi Gradle:

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

Dopo che il programma termina, apri `Worksheet.pptx` in Microsoft PowerPoint. Dovresti vedere una diapositiva che rispecchia il foglio Excel, e la casella di testo creata in Excel appare come una forma modificabile su cui puoi fare doppio clic e modificarla.

## Passo 5: Gestire più fogli di lavoro (opzionale)

Se hai bisogno di esportare **tutti** i fogli di lavoro nella cartella, sostituisci la chiamata a singolo foglio con un ciclo:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

Ogni iterazione crea un file PowerPoint separato (`Worksheet_0.pptx`, `Worksheet_1.pptx`, …). Per una singola presentazione contenente più diapositive, Aspose.Cells aggiunge automaticamente una diapositiva per foglio di lavoro quando chiami `save` una volta; non è necessario alcun codice aggiuntivo.

## Casi limite e migliori pratiche

| Situazione | Approccio consigliato |
|-----------|----------------------|
| Cartella di lavoro grande (centinaia di MB) | Aumentare l'heap JVM (`-Xmx4g`) e considerare l'esportazione dei fogli singolarmente per evitare errori di out‑of‑memory. |
| Cartella di lavoro protetta da password | Usare `LoadOptions` per fornire la password prima del caricamento: `new LoadOptions(LoadFormat.XLSX, "pwd")`. |
| Necessità di mantenere le formule Excel | PowerPoint non supporta le formule; vengono renderizzate come valori statici durante la conversione. |
| È richiesto un layout di diapositiva personalizzato | Dopo la conversione, manipolare il `.pptx` generato con Aspose.Slides per Java per regolare i master delle diapositive o aggiungere animazioni. |
| Esecuzione in un servizio web | Trasmettere l'output direttamente alla risposta HTTP invece di scrivere un file: `workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## Output previsto

Eseguendo l'esempio si produce un file chiamato `Worksheet.pptx`. Aprendolo in PowerPoint si vede:

* Una diapositiva che corrisponde visivamente al primo foglio Excel.  
* Una casella di testo modificabile posizionata esattamente dove era in Excel.  
* Formattazione di base delle celle (dimensione carattere, colore, bordi) preservata.

La console stampa:

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## Conclusione

Ora sai **come esportare un foglio Excel in PowerPoint** usando Aspose.Cells per Java, e comprendi anche come **convertire una cartella di lavoro Excel in una presentazione PowerPoint** in scenari reali. La soluzione funziona per esportazioni di singolo foglio, cartelle di lavoro con più fogli, e può essere estesa con Aspose.Slides per ulteriori personalizzazioni delle diapositive.

---

### Prossimi passi

* Esplora **Aspose.Slides per Java** per aggiungere animazioni, grafici o master diapositive personalizzati dopo la conversione.  
* Prova a convertire cartelle di lavoro che contengono grafici; Aspose.Cells renderizza i grafici come oggetti grafico nativi di PowerPoint.  
* Indaga l'elaborazione batch leggendo una directory di file Excel e generando un PowerPoint per ciascun file.

Sentiti libero di sperimentare con il codice, adattare i percorsi dei file e integrare la conversione in applicazioni Java più grandi, come servizi di reporting o pipeline di documenti automatizzate. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come esportare Excel in PowerPoint – Guida passo‑passo](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Come convertire Excel in PDF in Java usando Aspose.Cells: Guida passo‑passo](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Come esportare un foglio di lavoro Excel in PNG usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}