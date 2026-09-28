---
category: general
date: 2026-09-11
description: Crea un nuovo foglio di lavoro e copia un intervallo Excel usando Aspose.Cells.
  Scopri come copiare un intervallo tra fogli preservando le tabelle pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: it
lastmod: 2026-09-11
og_description: Crea un nuovo foglio di lavoro e copia un intervallo Excel con Aspose.Cells.
  Questo tutorial mostra i passaggi esatti per copiare l'intervallo tra i fogli e
  mantenere intatte le tabelle pivot.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Crea un nuovo foglio di lavoro e copia l’intervallo Excel – Guida Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Crea un nuovo foglio di lavoro e copia l'intervallo Excel con Aspose.Cells
url: /it/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un nuovo foglio di lavoro e copia un intervallo Excel con Aspose.Cells

Se hai bisogno di **create new worksheet** e spostare i dati in un file Excel, Aspose.Cells lo rende semplice. Questa guida mostra esattamente come copiare un intervallo Excel da un foglio all'altro preservando eventuali tabelle pivot all'interno dell'intervallo.

Imparerai come **copy excel range**, come **copy range between sheets**, e perché il metodo `copy` di Aspose.Cells mantiene intatte le definizioni delle tabelle pivot. Non sono necessari strumenti esterni—basta un progetto Java con la libreria Aspose.Cells.

## Prerequisiti

- Java 17 o versioni successive installato
- Aspose.Cells per Java (versione 23.12 o successiva) aggiunto al classpath del tuo progetto
- Una cartella di lavoro di origine (`input.xlsx`) che contiene una tabella pivot nell'intervallo che desideri copiare
- Familiarità di base con la sintassi Java e la gestione delle dipendenze Maven/Gradle

## Passo 1: Configura il progetto e importa Aspose.Cells

Crea un semplice progetto Maven (o Gradle, se preferisci) e aggiungi la dipendenza Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Quindi importa le classi necessarie nel tuo file sorgente Java:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Perché questo passo è importante*: Importare le classi corrette ti dà accesso a `Workbook`, `Worksheet`, `Range` e al metodo `copy` che gestirà il trasferimento dell'intervallo.

## Passo 2: Carica la cartella di lavoro di origine

Apri la cartella di lavoro che contiene i dati che desideri copiare. Il codice seguente carica `input.xlsx` da una directory che specifichi:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Spiegazione*: `Workbook` rappresenta l'intero file Excel. Caricarlo una volta ti fornisce accesso in lettura/scrittura a tutti i fogli e alle collezioni di celle.

## Passo 3: Identifica l'intervallo di origine che include la tabella pivot

Seleziona il foglio di lavoro che contiene la tabella pivot e definisci il blocco di celle esatto che desideri copiare. In questo esempio copiamo le celle da A1 a D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Perché è importante*: Creando un oggetto `Range`, indichi ad Aspose.Cells esattamente quali celle (inclusi eventuali oggetti incorporati come le tabelle pivot) devono essere duplicate.

## Passo 4: **Create new worksheet** che riceverà i dati copiati

Ora aggiungiamo un nuovo foglio alla stessa cartella di lavoro. Questo è il punto in cui appare la parola chiave principale:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Spiegazione*: Aggiungere un nuovo foglio isola i dati copiati, facilitando la verifica che l'operazione **copy excel range** sia riuscita senza influenzare il foglio originale.

## Passo 5: Copia l'intervallo – la tabella pivot viene preservata automaticamente

Utilizza il metodo `copy` per spostare l'intervallo dal foglio di origine a quello di destinazione. Aspose.Cells copia formule, formattazione e definizioni delle tabelle pivot:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Perché funziona*: Il metodo `copy` esegue una copia profonda delle celle di origine. Non copia solo i valori; replica l'intera struttura della cella, che include la cache della pivot. Questo è il motivo per cui puoi **copy range aspose.cells** e vedere ancora una tabella pivot funzionale nel nuovo foglio.

## Passo 6: Salva la cartella di lavoro con il nuovo foglio

Infine, scrivi la cartella di lavoro modificata su disco:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Risultato*: `output.xlsx` ora contiene il foglio originale più un nuovo foglio chiamato **Copy** che contiene esattamente lo stesso intervallo, tabella pivot inclusa.

## Esempio completo funzionante

Mettendo insieme tutti i pezzi, ecco il programma completo e eseguibile:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Output previsto**: Apri `output.xlsx` in Excel. Vedrai un foglio chiamato **Copy** le cui celle A1:D20 contengono gli stessi dati, la stessa formattazione e una tabella pivot attiva identica a quella originale.

## Domande comuni e casi particolari

- **What if the source range contains merged cells?**  
  Il metodo `copy` copia anche le informazioni di unione, quindi le celle unite appaiono inalterate nel foglio di destinazione.

- **Can I copy to a different workbook?**  
  Sì. Carica una seconda istanza di `Workbook`, crea un intervallo di destinazione in quella cartella di lavoro e chiama `sourceRange.copy(destinationRange)`. Il metodo gestisce automaticamente la copia tra cartelle di lavoro.

- **What if the destination sheet already has data?**  
  L'operazione di copia sovrascrive qualsiasi cella esistente che interseca l'intervallo di destinazione. Per evitare perdite di dati, assicurati che l'area di destinazione sia vuota o usa una cella di partenza diversa (ad es., `"B2"`).

- **Is the pivot cache duplicated?**  
  Aspose.Cells riutilizza la cache pivot originale, il che significa che la nuova tabella pivot rimane collegata agli stessi dati di origine. Se ti serve una cache indipendente, devi ricreare la tabella pivot dopo la copia.

## Suggerimenti e migliori pratiche

- **Pro tip**: Usa `Workbook.setForceFormulaRecalculation(true)` prima di salvare se il tuo intervallo contiene formule che dipendono da dati al di fuori del blocco copiato.
- **Watch out for** grandi intervalli: copiare fogli massivi può consumare molta memoria. Considera di copiare in blocchi più piccoli se incontri `OutOfMemoryError`.
- **Performance tip**: Disabilita l'aggiornamento dello schermo (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) quando lavori con file molto grandi per velocizzare il processo di copia.

## Conclusione

Ora sai come **create new worksheet** e **copy excel range** tra fogli usando Aspose.Cells, preservando le tabelle pivot e tutti gli attributi delle celle. Questa tecnica ti consente di duplicare programmaticamente blocchi di dati, creare modelli di report o ristrutturare le cartelle di lavoro senza copia‑incolla manuale.

Successivamente, esplora argomenti correlati come **copy range aspose.cells** per operazioni cross‑workbook, l'automazione dell'aggiornamento delle tabelle pivot o l'esportazione del foglio copiato in PDF. Sperimenta con diversi intervalli di origine e nomi di foglio per adattarli al tuo specifico scenario di automazione. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}