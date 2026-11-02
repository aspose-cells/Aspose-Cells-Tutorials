---
category: general
date: 2026-08-20
description: Scopri come esportare un grafico in docx e convertire una cartella di
  lavoro Excel in docx con Aspose.Cells in Java. Guida passo‑passo con codice completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: it
lastmod: 2026-08-20
og_description: Esporta il grafico in docx e converti la cartella di lavoro Excel
  in docx usando Aspose.Cells per Java. Segui questo tutorial completo e eseguibile.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Esporta grafico in docx con Aspose.Cells – Guida Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Come esportare un grafico in docx da Excel usando Aspose.Cells per Java
url: /it/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta grafico in docx da una cartella di lavoro Excel usando Java

Se hai bisogno di **export chart to docx** direttamente da un file Excel, questo tutorial ti mostra una soluzione pronta all'uso. Alla fine della guida saprai anche come **convert Excel workbook to docx** mantenendo un grafico modificabile, così il documento Word risultante può essere modificato senza perdere fedeltà.

Esportare grafici è comune quando generi report che combinano calcoli su fogli di calcolo con layout Word ricchi. Aspose.Cells for Java rende la conversione semplice, e l'API ti consente di mantenere il grafico modificabile—non è necessaria un'immagine statica.

## Cosa copre questo tutorial

* Caricamento di una cartella di lavoro esistente che contiene un grafico.  
* Configurazione di `ImageOrPrintOptions` per il formato DOCX.  
* Abilitazione del flag `ExportEditableCharts` (disponibile dalla versione 25.10).  
* Salvataggio della cartella di lavoro come file DOCX che conserva un grafico modificabile.  

Non sono necessari strumenti esterni oltre al JAR di Aspose.Cells. Il codice funziona con Java 8+ e qualsiasi versione recente di Aspose.Cells.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 or later) | La funzionalità `setExportEditableCharts` è stata introdotta in questa versione. |
| **Java Development Kit (JDK) 8 or newer** | Fornisce l'ambiente di runtime per compilare ed eseguire l'esempio. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | Il grafico è l'oggetto che verrà esportato in DOCX. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Semplifica la gestione delle dipendenze e l'esecuzione. |

Puoi scaricare l'ultimo JAR di Aspose.Cells dal [sito web di Aspose](https://products.aspose.com/cells/java/).

## Passo 1: Configura il progetto e aggiungi la dipendenza Aspose.Cells

Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Per Gradle, aggiungi:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Suggerimento:** Usa la versione esatta che ha introdotto `ExportEditableCharts` (25.10) o qualsiasi versione più recente. Le versioni più vecchie ignoreranno il flag e produrranno un'immagine statica.

## Passo 2: Carica la cartella di lavoro che contiene il grafico

La classe `Workbook` rappresenta l'intero file Excel. Caricarla è un'operazione a una riga:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Perché è importante:** La cartella di lavoro deve essere completamente caricata prima di poter applicare le opzioni di esportazione. Se il percorso del file è errato, Aspose.Cells genera una `FileNotFoundException`.

## Passo 3: Configura le opzioni immagine/stampa per l'output DOCX

`ImageOrPrintOptions` controlla come viene renderizzata la cartella di lavoro. Impostare il formato di salvataggio su `DOCX` indica ad Aspose.Cells di produrre un documento Word invece di un'immagine.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Puoi anche regolare qui la dimensione della pagina, DPI o qualità dell'immagine, ma sono opzionali per l'esportazione del grafico.

## Passo 4: Abilita l'esportazione di grafici modificabili

Dalla versione 25.10 in poi, Aspose.Cells può incorporare i grafici come oggetti grafico nativi di Word. Questo li rende completamente modificabili in Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Caso limite:** Se imposti questo flag a `false` (o lo ometti), il grafico verrà renderizzato come immagine statica. Usa `true` solo quando il pubblico di destinazione deve modificare il grafico dopo la conversione.

## Passo 5: Salva la cartella di lavoro come file DOCX

Infine, invoca `Workbook.save` con le opzioni configurate:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Quando il programma termina, apri `ChartEditable.docx` in Microsoft Word. Dovresti vedere il grafico originale e, se fai clic con il tasto destro, sarà disponibile l'opzione **Edit Data**, confermando che il grafico è davvero modificabile.

## Esempio completo, eseguibile

Di seguito trovi il file sorgente completo. Copialo nel tuo IDE, sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo, e eseguilo.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Output previsto**

* Un file chiamato `ChartEditable.docx` nella directory specificata.  
* Aprendo il file in Word il grafico appare esattamente come in Excel, e puoi fare doppio clic sul grafico per modificare le sue serie di dati.

## Problemi comuni e come evitarli

| Sintomo | Causa | Risoluzione |
|---------|-------|-----|
| Word mostra un'**immagine statica** invece di un grafico modificabile | `setExportEditableCharts` non chiamato o utilizzo di una versione < 25.10 | Assicurati che il flag sia impostato su `true` e che tu stia usando Aspose.Cells 25.10 o più recente. |
| Il DOCX generato è **vuoto** | Percorso file errato per la cartella di lavoro di origine o permessi insufficienti | Verifica il percorso della cartella di lavoro e che l'applicazione abbia accesso in lettura/scrittura. |
| Il layout del grafico appare **distorto** | Impostazioni di pagina in Excel (ad es., righe/colonne nascoste) differiscono dalle impostazioni predefinite di Word | Regola `ImageOrPrintOptions` (ad es., `setOnePagePerSheet(true)`) per controllare la scala. |
| **Prestazioni** degradano su cartelle di lavoro grandi | Esportazione di molti grafici o set di dati grandi | Esporta solo i fogli necessari o usa `setSheetIndex` per limitare l'elaborazione. |

## Estendere la soluzione

* **Grafici multipli:** Itera su tutti i fogli di lavoro e chiama `worksheet.getCharts()` per esportare ogni grafico singolarmente.  
* **Stile DOCX personalizzato:** Dopo il salvataggio, usa Aspose.Words per applicare intestazioni, piè di pagina o stili al documento generato.  
* **Conversione batch:** Avvolgi il codice in un ciclo che elabora una directory di file `.xlsx`, producendo un DOCX per ciascuno.  

## Conclusione

Ora disponi di un metodo affidabile per **export chart to docx** e **convert Excel workbook to docx** mantenendo la piena modificabilità del grafico. I passaggi chiave sono caricare la cartella di lavoro, configurare `ImageOrPrintOptions` per DOCX, abilitare `ExportEditableCharts` e salvare il risultato.

Sperimenta con opzioni aggiuntive—come impostare i margini di pagina o incorporare le formule della cartella di lavoro—per adattare l'output al tuo flusso di lavoro di reporting. Quando devi generare report Word da dati Excel in modo programmatico, questo approccio offre una soluzione pulita e manutenibile.

--- 

*Pronto per provarlo? Clona l'esempio, aggiorna i percorsi dei file e esegui il programma. Se incontri problemi, consulta la documentazione di Aspose.Cells for Java o esplora gli argomenti correlati qui sotto.*  

### Argomenti correlati che potresti esplorare prossimamente

* **convert excel workbook to pdf** – genera report PDF dallo stesso workbook.  
* **Aspose.Cells chart formatting** – personalizza colori, marcatori e assi prima dell'esportazione.  
* **Embedding images in DOCX with Aspose.Words** – combina grafici con altri contenuti Word.  

Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare un grafico Excel con linea di tendenza ed esportarlo come immagine usando Aspose.Cells per Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automatizzare l'accesso ai grafici Excel usando Aspose.Cells Java: Guida passo passo](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Personalizzare le etichette dati dei grafici Excel usando Aspose.Cells per Java: Guida passo passo](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}