---
category: general
date: 2026-10-16
description: Come copiare una tabella pivot in Java con Aspose.Cells – impara a copiare
  un intervallo su un altro foglio e a copiare un intervallo tra fogli di lavoro in
  modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: it
lastmod: 2026-10-16
og_description: Come copiare una tabella pivot in Java usando Aspose.Cells. Questo
  tutorial ti mostra come copiare un intervallo in un altro foglio e copiare un intervallo
  tra fogli di lavoro con il codice completo.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Come copiare una tabella pivot tra fogli di lavoro in Java – guida passo
  passo
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Come copiare una tabella pivot tra fogli di lavoro in Java
url: /it/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot tra fogli di lavoro in Java

Se hai bisogno di **come copiare una tabella pivot** da un foglio all'altro nello stesso workbook, questa guida fornisce una soluzione completa, pronta all'uso. Vedrai come copiare l'intervallo di origine che contiene la tabella pivot, preservarne la funzionalità e verificare il risultato—tutto usando Aspose.Cells per Java.

Copiare una tabella pivot è un'operazione comune quando generi report in modo programmatico, e farlo correttamente evita di perdere la cache della pivot o di rompere le formule. Alla fine di questo tutorial sarai in grado di **copiare intervallo su un altro foglio** e **copiare intervallo tra fogli di lavoro** senza alcun passaggio manuale.

## Cosa imparerai

* Caricare un file Excel esistente con una tabella pivot.
* Definire l'intervallo di origine che contiene la tabella pivot.
* Definire un intervallo di destinazione su un foglio di lavoro diverso.
* Utilizzare `CopyOptions` per mantenere intatta la tabella pivot.
* Verificare che la tabella pivot copiata funzioni come previsto.

**Prerequisiti**

* Java 17 o successiva.
* Aspose.Cells per Java (versione 23.12 o successiva).  
* Un file Excel (`input.xlsx`) che contiene una tabella pivot nel primo foglio.

---

## Come copiare una tabella pivot con Aspose.Cells

Il nucleo dell'operazione è un processo in quattro passaggi: caricare la cartella di lavoro, individuare l'intervallo di origine, impostare l'intervallo di destinazione ed eseguire la copia. Di seguito ogni passaggio è spiegato in dettaglio.

### Passo 1: Caricare la cartella di lavoro

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Perché questo passaggio?*  
Caricare la cartella di lavoro porta l'intero file in memoria, fornendoti l'accesso a fogli di lavoro, celle e alla cache della pivot. Aspose.Cells legge automaticamente il formato del file, quindi non è necessario preoccuparsi di `.xls` vs `.xlsx`.

### Passo 2: Individuare l'intervallo di origine che contiene la tabella pivot

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Perché questo passaggio?*  
Una tabella pivot è memorizzata in un blocco di celle che fa anche riferimento a una cache nascosta. Selezionando l'intervallo esatto (`A1:G20` in questo esempio), garantisci che la cache rimanga collegata quando l'intervallo viene copiato.

### Passo 3: Definire l'intervallo di destinazione su un altro foglio

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Perché questo passaggio?*  
Scegliere una destinazione su un foglio di lavoro diverso ti consente di **copiare intervallo su un altro foglio**. La cella in alto a sinistra (`A1`) è un punto di partenza comune, ma puoi posizionarla ovunque modificando l'indirizzo.

### Passo 4: Copiare l'intervallo di origine preservando la tabella pivot

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Perché questo passaggio?*  
`CopyOptions` controlla cosa viene trasferito. Usare `PasteType.PASTE_ALL` garantisce che la tabella pivot, la sua formattazione e le formule sottostanti vengano duplicate. Senza queste opzioni, potrebbero essere copiati solo i valori grezzi, interrompendo la funzionalità della pivot.

### Passo 5: Salvare la cartella di lavoro e verificare il risultato

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Apri `output.xlsx` in Excel e conferma che:

* Il secondo foglio contiene una tabella pivot pienamente funzionale identica a quella originale.
* Aggiornare la tabella pivot aggiorna i dati, dimostrando che la cache è intatta.

## Copiare intervallo su un altro foglio usando Java

Se il tuo obiettivo è semplicemente **copiare intervallo su un altro foglio** senza una tabella pivot, lo stesso codice funziona con un intervallo di celle normale. L'unica modifica è l'indirizzo di origine. La configurazione di `CopyOptions` rimane invariata, garantendo che formule e formattazione vengano preservate.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Questo frammento dimostra la flessibilità dell'API per scenari sia con pivot che senza pivot.

## Copiare intervallo tra fogli di lavoro senza perdere formule

Quando **copiare intervallo tra fogli di lavoro**, le formule che fanno riferimento ad altri fogli possono rompersi se le referenze relative cambiano. Per evitare ciò:

1. Usa `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` se ti servono solo le formule.
2. Mantieni il foglio di destinazione nella stessa cartella di lavoro affinché le referenze interne rimangano valide.
3. Dopo la copia, chiama `workbook.calculateFormula();` per forzare un ricalcolo.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Questi passaggi aggiuntivi garantiscono che un intervallo copiato si comporti esattamente come l'originale, anche quando si estende su più fogli di lavoro.

## Consigli professionali e errori comuni

| Situazione | Suggerimento |
|------------|--------------|
| **Cache della pivot non aggiornata** | Dopo la copia, chiama `destSheet.getPivotTables().get(0).refresh();` per aggiornare la cache. |
| **Copiare in una cartella di lavoro diversa** | Usa `Workbook destWorkbook = new Workbook();` e poi `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Ricorda di copiare separatamente la cache della pivot se necessario. |
| **Tabelle pivot di grandi dimensioni** | Aumenta la dimensione dell'heap Java (`-Xmx2g`) per evitare `OutOfMemoryError` durante la copia. |
| **Preservare gli stili** | Imposta `copyOptions.setPasteType(PasteType.PASTE_ALL)`; altrimenti, vengono copiate solo i valori. |

## Output previsto

Eseguendo il programma completo si genera `output.xlsx`. Quando aperto in Excel:

* **Sheet2!A1:G20** mostra la stessa tabella pivot di **Sheet1!A1:G20**.
* L'elenco dei campi pivot, le etichette di riga/colonna e i valori dei dati corrispondono all'origine.
* Aggiornare la pivot aggiorna i numeri, confermando che la cache è funzionale.

La console stamperà:

```
Pivot table copied successfully.
```

## Conclusione

In questo tutorial hai imparato **come copiare una tabella pivot** da un foglio di lavoro a un altro usando Aspose.Cells per Java. Caricando la cartella di lavoro, selezionando l'intervallo di origine corretto, definendo una destinazione e configurando `CopyOptions`, puoi in modo affidabile **copiare intervallo su un altro foglio** e **copiare intervallo tra fogli di lavoro** preservando tutta la funzionalità della pivot.  

Successivamente, potresti esplorare:

* Esportare la tabella pivot copiata in PDF o HTML.
* Automatizzare gli aggiornamenti della tabella pivot su più cartelle di lavoro.
* Usare `CopyOptions` per copiare solo elementi specifici (ad esempio, valori, formati).

Sentiti libero di sperimentare con diversi indirizzi di intervallo, strutture di cartelle di lavoro o anche copie tra cartelle di lavoro. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come copiare intervallo in Java – Copia Tabella Pivot con Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Come Copiare Tabella Pivot in Java – Guida Completa Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copia Tabella Pivot Excel – Guida Passo‑Passo Usando Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}