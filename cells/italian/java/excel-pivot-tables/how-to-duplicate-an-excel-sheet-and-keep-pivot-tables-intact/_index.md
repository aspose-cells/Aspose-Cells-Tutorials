---
category: general
date: 2026-10-23
description: Scopri come duplicare un foglio Excel in Java mantenendo intatte le tabelle
  pivot. Questa guida mostra anche come copiare le tabelle pivot, copiare gli intervalli
  Excel e copiare un foglio con i dati pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: it
lastmod: 2026-10-23
og_description: Duplica un foglio Excel in Java mantenendo intatte le tabelle pivot.
  Segui questo tutorial completo per copiare le tabelle pivot, copiare gli intervalli
  Excel e copiare un foglio con i dati pivot.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplica un foglio Excel con tabelle pivot in Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Come duplicare un foglio Excel e mantenere intatte le tabelle pivot in Java
url: /it/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come duplicare un foglio Excel e mantenere intatte le tabelle pivot in Java

Se hai bisogno di **duplicare un foglio Excel** mentre mantieni tutte le tabelle pivot attive, questa guida ti mostra esattamente come fare. Vedrai una soluzione concisa che copia un foglio, copia un intervallo specifico e persino copia una tabella pivot in un altro workbook—tutto in puro Java usando Aspose.Cells.

Duplicare un foglio Excel è un'operazione comune quando generi report mensili da un modello o quando ti serve una copia sandbox per i test. Il codice qui sotto funziona con Aspose.Cells 25.11 o versioni successive, che hanno introdotto l'opzione `setCopyPivotTable(true)`.

## Cosa ti servirà

- Java 17 (o qualsiasi JDK recente) installato
- Aspose.Cells per Java 25.11 o più recente nel tuo progetto (coordinate Maven `com.aspose:aspose-cells:25.11`)
- Un workbook di origine (`SourceWithPivot.xlsx`) che contiene già una tabella pivot
- Un IDE o uno strumento di build a tua scelta (IntelliJ IDEA, Eclipse, Maven, Gradle, ecc.)

## Passo 1: Carica il workbook di origine che contiene la tabella pivot

La prima operazione è aprire il workbook che contiene la pivot che desideri preservare.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Perché questo passo è importante:** Caricare il workbook di origine ti dà accesso agli oggetti worksheet, alle celle e alle tabelle pivot incorporate. Senza questo, non puoi fare riferimento ai dati pivot che intendi copiare.

## Passo 2: Crea un workbook di destinazione vuoto (o caricane uno esistente)

Puoi iniziare con un workbook vuoto oppure aprire un file esistente che riceverà il foglio duplicato.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Suggerimento:** Se hai già un workbook di reporting, sostituisci la riga sopra con `new Workbook("ExistingReport.xlsx")` per aggiungere il foglio duplicato.

## Passo 3: Copia l'intero worksheet – la tabella pivot viene preservata automaticamente

Copiare l'intero worksheet è il modo più semplice per **copiare un foglio con pivot**. Aspose.Cells copia automaticamente la definizione della pivot e la sua cache.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Perché funziona:** `addCopy` clona la struttura del foglio, i valori delle celle, gli stili e qualsiasi tabella pivot incorporata. Il nuovo worksheet in `dstWb` avrà aspetto identico all'originale, inclusa la cache della pivot.

## Passo 4: (Opzionale) Copia solo un intervallo specifico che include la tabella pivot

A volte non vuoi l'intero foglio—potresti aver bisogno solo di una parte che contiene la pivot. È qui che **copia un intervallo Excel** e richiedi esplicitamente che la pivot venga copiata.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Come aiuta:** `setCopyPivotTable(true)` costringe il motore a duplicare la definizione della pivot anche quando copi un intervallo limitato. Senza questo flag, verrebbero copiate solo i dati grezzi e la pivot andrebbe persa.

## Passo 5: Salva il workbook di destinazione

Infine, scrivi il contenuto duplicato in un nuovo file.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Output previsto

Eseguendo il programma si crea `DuplicatedWithPivot.xlsx` nella directory di destinazione. Apri il file in Excel e vedrai:

- Un nuovo worksheet chiamato `Sheet1 (Copy)` (o il nome originale con “Copy” aggiunto)
- La tabella pivot appare esattamente come nel foglio di origine, completamente funzionale
- Se hai usato la copia dell'intervallo opzionale, sono presenti solo le celle A1:G30, ma la pivot funziona comunque perché la sua cache è stata copiata

## Domande comuni e casi particolari

### Come copiare una pivot in un altro workbook senza copiare l'intero foglio?

Se ti serve solo la pivot e i dati sottostanti, copia l'intervallo che contiene sia i dati di origine sia la pivot, quindi usa `setCopyPivotTable(true)`. Lo stesso codice del **Passo 4** si applica; assicurati solo che l'intervallo copra la sorgente dati.

### Cosa succede se il workbook di origine ha più worksheet con pivot?

Ripeti il **Passo 3** per ogni worksheet che desideri duplicare:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Funziona con worksheet protetti?

Aspose.Cells può copiare fogli protetti, ma devi prima rimuovere la protezione se devi modificare la pivot dopo la copia:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Posso copiare una tabella pivot in un workbook esistente che contiene già un foglio con lo stesso nome?

Sì. Usa `addCopy` con un nome univoco:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Consiglio professionale: verifica la cache della pivot

Dopo la copia, puoi confermare programmaticamente che la cache della pivot esista:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Se l'ID della cache stampa un numero non negativo, la pivot è stata duplicata con successo.

## Conclusione

Ora sai come **duplicare un foglio Excel** in Java preservando ogni tabella pivot, come **copiare direttamente le pivot**, come **copiare un intervallo Excel** che include una pivot, e come **copiare un foglio con pivot** o **copiare una pivot in un workbook** usando Aspose.Cells 25.11+. Applica questi pattern per automatizzare la generazione di report, creare cloni di template o costruire ambienti di test che richiedono analisi guidate da pivot identiche.

Pronto a esplorare di più? Prova a esportare il workbook duplicato in PDF, o a rinfrescare programmaticamente la cache della pivot dopo la copia per garantire che i dati più recenti siano riflessi. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}