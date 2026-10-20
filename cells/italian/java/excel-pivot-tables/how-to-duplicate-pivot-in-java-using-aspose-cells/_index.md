---
category: general
date: 2026-09-18
description: come duplicare una tabella pivot in Java con Aspose.Cells – copiare una
  tabella pivot tra cartelle di lavoro rapidamente e in modo affidabile
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: it
lastmod: 2026-09-18
og_description: come duplicare una tabella pivot in Java usando Aspose.Cells. Segui
  questo tutorial completo per copiare una tabella pivot tra cartelle di lavoro con
  codice Java pulito.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplica una tabella pivot in Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come duplicare una tabella pivot in Java usando Aspose.Cells
url: /it/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come duplicare una pivot in Java usando Aspose.Cells

Se hai bisogno di **come duplicare una pivot** in un'applicazione Java, questa guida ti mostra i passaggi esatti. Caricando una cartella di lavoro Excel, definendo l'area di celle della pivot e copiando quell'intervallo in una nuova cartella di lavoro, puoi spostare una tabella pivot senza perdere la sua definizione o i dati.

Copiare una tabella pivot è una necessità comune quando generi report, archivi analisi o suddividi una cartella di lavoro grande in parti modulari. In questo tutorial imparerai come **copiare intervalli tra cartelle di lavoro**, come **caricare una cartella di lavoro Excel con Java**, e le sfumature di **come copiare una pivot** in modo sicuro.

Concluderai con un programma Java pronto all'uso che duplica una tabella pivot da `Source.xlsx` a `PivotCopied.xlsx` usando Aspose.Cells per Java.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* JDK 8 o versioni successive installate.
* Maven (o un altro tool di build) per gestire le dipendenze.
* Aspose.Cells per Java versione 23.10 o successiva. Aggiungi la seguente dipendenza Maven al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Una cartella di lavoro di origine (`Source.xlsx`) che contiene una tabella pivot nell'intervallo **A1:H30**.

## Come duplicare una pivot in Java

L'idea di base è semplice:

1. **Carica la cartella di lavoro di origine** – questo ti dà accesso al foglio che contiene la pivot.
2. **Definisci l'area di celle** che racchiude la pivot.
3. **Crea una cartella di lavoro di destinazione** – un file vuoto che riceverà l'intervallo copiato.
4. **Copia l'intervallo** – Aspose.Cells duplica automaticamente la definizione della pivot.
5. **Salva la cartella di lavoro di destinazione** – ora hai un file separato con la stessa pivot.

Di seguito trovi un programma Java completo e eseguibile che segue questi passaggi.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Perché funziona

* **Aspose.Cells** tratta una tabella pivot come parte della collezione di celle del foglio. Quando invochi `copyRange`, la libreria copia non solo i valori delle celle ma anche la cache e la definizione della pivot sottostante, così il nuovo workbook contiene un duplicato pienamente funzionante.
* L'oggetto `CopyOptions` conserva per impostazione predefinita formule, formati e oggetti incorporati. Puoi personalizzarlo (ad esempio, `setCopyColumnWidths(true)`) se hai bisogno di un controllo aggiuntivo.

## Copia di intervalli tra cartelle di lavoro – approfondimento

Mentre l'esempio sopra copia un unico blocco contiguo, `copyRange` può gestire qualsiasi area rettangolare. Se la tua pivot si estende su intervalli non adiacenti, puoi chiamare `copyRange` più volte o usare `Worksheet.copy` per duplicare l'intero foglio.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Suggerimento:** Quando copi cartelle di lavoro di grandi dimensioni, abilita `CopyOptions.setPreserveCellStyle(true)` per evitare duplicazioni di stile non necessarie, migliorando le prestazioni.

## Come copiare una pivot in una cartella di lavoro – gestione di più pivot

Se il foglio di origine contiene più di una pivot, puoi iterare sulle tabelle pivot del foglio e copiare ciascuna individualmente:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Questo approccio garantisce che ogni pivot mantenga il proprio nome originale e la fonte dati.

## Caricare una cartella di lavoro Excel con Java – errori comuni

* **Separatori di percorso file:** Usa le barre oblique (`/`) o `File.separator` per mantenere il codice indipendente dalla piattaforma.
* **Licenza mancante:** Aspose.Cells funziona in modalità di valutazione, ma l'output conterrà una filigrana. Registra una licenza con `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` prima di caricare la cartella di lavoro per rimuovere la filigrana.
* **File di grandi dimensioni:** Per cartelle di lavoro superiori a 100 MB, considera l'uso di `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` con opzioni di streaming per ridurre il consumo di memoria.

## Riepilogo dell'esempio completo end‑to‑end

Mettendo tutto insieme, ecco il programma finale che puoi copiare‑incollare nel tuo IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Output previsto:** Dopo l'esecuzione, `PivotCopied.xlsx` appare nella directory specificata. Aprendolo in Excel vedrai lo stesso layout della tabella pivot, filtri e dati di `Source.xlsx`. Tutti i campi calcolati e la formattazione sono preservati.

## Domande frequenti

* **Funziona con formati Excel più vecchi (.xls)?**  
  Sì. Aspose.Cells rileva automaticamente il formato. Usa `new Workbook("file.xls")` e la stessa logica di copia si applica.

* **E se la pivot fa riferimento a fonti dati esterne?**  
  La copia mantiene il riferimento originale alla fonte dati. Se l'ambiente di destinazione non può raggiungere quella fonte, la pivot mostrerà errori `#REF!`. Per evitarlo, aggiorna la pivot dopo la copia o modifica la sua fonte dati tramite `PivotTable.setDataSource(...)`.

* **Posso copiare una pivot in un foglio con nome specifico?**  
  Assolutamente. Dopo aver creato il foglio di destinazione, rinominalo:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Conclusione

Ora sai **come duplicare le pivot** in Java usando Aspose.Cells, **come copiare intervalli tra cartelle di lavoro**, e le migliori pratiche per **caricare una cartella di lavoro Excel con Java**. Seguendo il processo in cinque passaggi—carica, definisci, crea destinazione, copia e salva—puoi automatizzare la generazione di report, archiviare analisi o suddividere cartelle di lavoro complesse senza perdere la funzionalità della pivot.

Successivamente, esplora argomenti correlati come **copiare pivot in una cartella di lavoro** con più fogli, o integra la pivot duplicata in una pipeline di elaborazione dati più ampia usando Apache POI per scenari non‑Aspose. Sperimenta con diverse impostazioni di `CopyOptions` per ottimizzare le prestazioni su cartelle di lavoro massive.

Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Group Pivot Fields in Excel Workbooks Using Aspose.Cells for Java - Comprehensive Guide](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}