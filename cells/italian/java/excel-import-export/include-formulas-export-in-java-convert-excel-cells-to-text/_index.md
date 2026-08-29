---
category: general
date: 2026-07-03
description: Includi l'esportazione delle formule in Java per convertire le celle
  di Excel in testo usando Aspose.Cells. Scopri come stampare un intervallo di Excel
  e ottenere la stringa dei valori delle celle in modo efficiente.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: it
og_description: Includi l'esportazione di formule in Java per convertire le celle
  di Excel in testo. Guida passo passo che mostra come stampare un intervallo di Excel
  e recuperare i valori delle celle come stringa.
og_title: Includi l'esportazione delle formule in Java – Converti le celle di Excel
  in testo
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Includi l'esportazione delle formule in Java – Converti le celle di Excel in
  testo
url: /it/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Includere l'Esportazione di Formule in Java – Convertire le Celle di Excel in Testo

Ti è mai capitato di dover **includere l'esportazione di formule** quando estrai dati da una cartella di lavoro Excel? Forse stai creando un servizio di reporting che deve preservare le formule originali mantenendo comunque un blocco di testo ordinato. In tal caso, sei nel posto giusto. Questa guida ti mostra come convertire le celle di Excel in testo semplice—*includendo* eventuali formule incorporate—usando Aspose.Cells per Java.

Tratteremo anche come **stampare l'intervallo Excel**, modificare le **opzioni di esportazione della tabella**, e infine **ottenere la stringa dei valori delle celle** che potrai registrare, inviare tramite un'API o archiviare in un database. Alla fine avrai uno snippet completamente eseguibile e una solida comprensione del perché di ogni chiamata.

## Cosa Otterrai

- Un programma Java completo, pronto per il copia‑incolla, che legge un file `.xlsx`, seleziona un intervallo e lo esporta come stringa formattata.
- Una comprensione della classe `ExportTableOptions` e del motivo per cui attivare `setExportAsString` e `setIncludeFormula` è importante.
- Suggerimenti per gestire fogli di lavoro di grandi dimensioni, trattare diversi tipi di dati e personalizzare il formato di output.
- Una rapida checklist per le insidie comuni (pensa a celle unite, righe nascoste e formati numerici specifici della locale).

### Prerequisiti

- Java 17 o superiore (il codice compila anche con versioni precedenti ma utilizzeremo l'ultima LTS).
- Aspose.Cells for Java 23.10 (o qualsiasi versione recente) — puoi scaricarlo da Maven Central.
- Un file di esempio `input.xlsx` posizionato in una cartella a tua disposizione (il percorso è hard‑coded nell'esempio per chiarezza).

Se li hai già, tuffiamoci.

## Passo 1: Configura il Progetto e Aggiungi le Dipendenze

Prima, crea un progetto Maven (o Gradle, se preferisci). Aggiungi la dipendenza Aspose.Cells al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Suggerimento:** Se utilizzi un proxy aziendale, assicurati che il repository sia raggiungibile; altrimenti la compilazione fallirà con l'errore “Could not resolve dependencies”.

Una volta che Maven ha terminato il download, sei pronto per scrivere del Java.

## Passo 2: Carica la Cartella di Lavoro e Ottieni il Foglio di Lavoro Desiderato

La prima riga dell'esempio di codice mostra come aprire una cartella di lavoro esistente:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Sostituisci `YOUR_DIRECTORY` con il percorso assoluto o relativo al tuo file. Il costruttore `Workbook` rileva automaticamente il formato del file (XLS, XLSX, CSV, ecc.), quindi non è necessario specificarlo.

Successivamente, recuperiamo il primo foglio:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Perché il primo foglio? In molti modelli i dati si trovano nella prima scheda, ma puoi passare qualsiasi indice o anche usare `get("SheetName")` se preferisci un approccio basato sul nome.

## Passo 3: Definisci l'Intervallo da Esportare

Ora arriva il cuore dell'operazione **convert excel cells text**. Indichi ad Aspose.Cells quali celle estrarre creando un oggetto `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

La stringa `"A1:C3"` è un classico indirizzo in stile A1. Può anche essere costruita programmaticamente:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Questa flessibilità è utile quando la dimensione dell'intervallo è dinamica—ad esempio, leggi l'ultima riga usata con `ws.getCells().getMaxDataRow()`.

## Passo 4: Configura le Opzioni di Esportazione della Tabella per Includere le Formule

Qui è dove avviene la magia dell'**include formulas export**. Per impostazione predefinita, Aspose.Cells restituisce i valori *visualizzati*. Se una cella contiene `=SUM(A1:A3)`, otterrai il numero calcolato, non il testo della formula. Per cambiarlo, configura `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Perché entrambe le impostazioni? `setExportAsString(true)` indica all'API di concatenare le celle usando il delimitatore predefinito (tab per le colonne, newline per le righe). `setIncludeFormula(true)` cambia la fonte del valore da “valore visualizzato” a “formula grezza”. Se vuoi solo i valori, impostala a `false`.

### Regolazioni Opzionali

- `eto.setExportHiddenRows(true);` – include le righe nascoste in Excel.
- `eto.setExportHiddenColumns(true);` – stesso per le colonne.
- `eto.setExportAsHTML(true);` – ottieni HTML invece di testo semplice.

Sentiti libero di sperimentare; la classe delle opzioni è un playground per le **export table options**.

## Passo 5: Recupera l'Intervallo come Stringa Formattata

Ora estraiamo i dati:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Il `txt` restituito appare più o meno così (supponendo che A1:C3 contenga un mix di valori e formule):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Nota il tab (`\t`) che separa le colonne e il newline (`\n`) che separa le righe. Puoi dividere la stringa in seguito se ti serve un array 2‑D:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Passo 6: Stampa il Risultato – “Print Excel Range” Semplificato

Infine, stampiamo la stringa sulla console:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Eseguendo il programma stampa l'output esatto mostrato sopra. Da qui potresti scrivere la stringa in un file di log, inviarla via HTTP o archiviarla in un documento NoSQL.

## Esempio Completo, Pronto da Eseguire

Mettendo tutto insieme, ecco il programma completo. Copia, incolla e premi **Run**—senza import mancanti.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Output Atteso (esempio)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Se la tua cartella di lavoro contiene numeri formattati come date, appariranno nel formato specifico della locale (ad es., `2026‑07‑03`). Per forzare date ISO, puoi modificare le `ExportTableOptions` con un `NumberFormat` personalizzato.

## Gestione dei Casi Limite e Domande Frequenti

### Cosa succede se l'intervallo contiene celle unite?

Le celle unite sono trattate come il valore della cella in alto a sinistra. Il resto dell'area unita apparirà come stringhe vuote. Se ti serve l'indirizzo dell'area unita, interroga `Cell.getMergedRange()` prima dell'esportazione.

### Posso esportare un foglio enorme (centinaia di migliaia di righe)?

Sì, ma fai attenzione al consumo di memoria. Usa `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` per consentire ad Aspose.Cells di streammare i dati su disco. Inoltre, considera di esportare a blocchi (ad es., 10 000 righe alla volta) per mantenere la stringa gestibile.

### Come cambio il delimitatore di colonna?

`ExportTableOptions` espone `setSeparator(char separator)`. Per un output in stile CSV, impostalo a `','`:

```java
eto.setSeparator(',');
```

### Le formule rispettano i riferimenti esterni?

Se una formula punta a un altro workbook, Aspose.Cells manterrà il testo del riferimento (`='[Other.xlsx]Sheet1'!A1`). Non valuterà il valore esterno a meno che non carichi anche quel workbook.

## Suggerimenti Pro per Codice Pronto per la Produzione

- **Cache the workbook** se stai leggendo il

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}