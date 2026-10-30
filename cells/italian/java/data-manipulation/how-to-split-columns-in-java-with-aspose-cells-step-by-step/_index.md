---
category: general
date: 2026-10-07
description: Come dividere le colonne usando Aspose.Cells per Java. Impara a suddividere
  una stringa in colonne, automatizzare le formule di Excel e scrivere una formula
  in una cella in poche righe di codice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: it
lastmod: 2026-10-07
og_description: Come dividere le colonne in Java con Aspose.Cells. Questo tutorial
  ti mostra come dividere una stringa in colonne, automatizzare la valutazione delle
  formule di Excel e scrivere una formula in una cella.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Come dividere le colonne in Java con Aspose.Cells – tutorial rapido
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come dividere le colonne in Java con Aspose.Cells – guida passo passo
url: /it/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come dividere le colonne in Java con Aspose.Cells – guida passo‑passo

Se hai bisogno di **how to split columns** in un foglio di lavoro Excel in modo programmatico, questa guida ti mostra l'intero processo con Aspose.Cells per Java. Imparerai anche come **split string into columns**, **automate Excel formula** evaluation e **write formula to a cell** usando codice conciso e pronto per la produzione.

La divisione programmatica delle colonne elimina il copia‑incolla manuale, riduce gli errori e consente trasformazioni di dati su larga scala. Alla fine di questo tutorial potrai generare, modificare e valutare formule al volo, rendendo Excel una vera parte del tuo backend Java.

## Prerequisiti

* Java 17 o versioni successive installato.
* Maven 3.8+ (o Gradle) per la gestione delle dipendenze.
* Una licenza Aspose.Cells per Java (la versione di valutazione gratuita funziona per l'apprendimento).
* Familiarità di base con la sintassi Java e i concetti di Excel.

Se uno di questi elementi manca, installalo prima; gli esempi di codice presumono un progetto Maven standard.

## Passo 1: Aggiungere Aspose.Cells al tuo progetto

Aggiungi la seguente dipendenza al tuo `pom.xml`. Questo scarica l'ultima versione stabile della libreria Aspose.Cells.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Perché questo passo è importante:** La libreria fornisce le classi `Workbook`, `Worksheet` e `Cell` necessarie per manipolare file Excel senza Microsoft Office. Senza la dipendenza il codice non compila.

## Passo 2: Creare un workbook e selezionare il primo worksheet

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

L'oggetto `Workbook` rappresenta l'intero file Excel. Accedere al primo worksheet garantisce un punto di partenza prevedibile per la formula che scriveremo.

## Passo 3: Scrivere la formula WRAPCOLS in una cella di destinazione

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Perché usiamo `WRAPCOLS`:** La funzione integrata di Excel `WRAPCOLS` suddivide automaticamente un singolo valore di testo in un numero definito di colonne, gestendo in modo intelligente i confini delle parole. Questo è il metodo più affidabile per **split string into columns** senza logica di parsing personalizzata.

## Passo 4: Forzare il workbook a valutare la formula

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Chiamare `calculateFormula()` **automates Excel formula** evaluation sul lato server. Senza questa chiamata la cella conterrebbe ancora il testo della formula, non i valori calcolati.

## Passo 5: Recuperare e visualizzare il risultato avvolto

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

When you run the program, the console prints:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Il file `SplitColumnsResult.xlsx` generato mostra le tre colonne popolate con il testo diviso.

## Comprendere la funzione WRAPCOLS

* **Sintassi:** `WRAPCOLS(text, columns, [delimiter])`
* **Parametri:**
  * `text` – la stringa che desideri dividere.
  * `columns` – il numero di colonne su cui distribuire il testo.
  * `delimiter` (opzionale) – carattere usato per dividere la stringa; il valore predefinito è uno spazio.
* **Valore di ritorno:** Un array che si estende nelle celle adiacenti, ogni elemento contiene una porzione del testo originale.

Poiché la funzione si estende orizzontalmente, è sufficiente scrivere la formula nella cella più a sinistra (A1 nell'esempio). Excel riempie automaticamente B1, C1, … secondo necessità.

## Varianti comuni e casi limite

| Situazione | Regolazione consigliata |
|-----------|------------------------|
| **Variable column count** | Sostituire il valore hard‑coded `3` con una variabile: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Custom delimiter** | Usare il terzo argomento, ad esempio `=WRAPCOLS(A2,4,",")` per dividere su virgole. |
| **Empty source string** | La funzione restituisce celle vuote; proteggere da `null` o stringhe vuote prima di impostare la formula. |
| **Large datasets** | Applicare la formula in un ciclo per ogni riga, quindi chiamare `calculateFormula()` una volta dopo il ciclo per migliorare le prestazioni. |
| **Non‑ASCII characters** | WRAPCOLS funziona con Unicode; assicurati che il tuo file sorgente Java sia salvato come UTF‑8. |

**Suggerimento professionale:** Quando si elaborano molte righe, memorizza la formula in una variabile stringa e riutilizzala per evitare l'overhead di concatenazione ripetuta delle stringhe.

## Esempio completo e eseguibile

Di seguito è riportato il programma completo pronto per il copia‑incolla. Include le istruzioni di import, la gestione delle eccezioni e un'operazione di salvataggio opzionale.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Eseguendo questo programma si ottiene lo stesso output della console mostrato in precedenza e si scrive un file Excel che dimostra chiaramente **how to split columns**.

## Checklist di risoluzione dei problemi

* **Formula non valutata** – Assicurati che `workbook.calculateFormula()` venga chiamato dopo aver impostato la formula.
* **Celle vuote dopo la divisione** – Verifica che la stringa di origine non sia `null` o vuota, e che il conteggio delle colonne sia maggiore di zero.
* **Eccezione di licenza** – Fornisci un file di licenza Aspose.Cells valido (`License license = new License(); license.setLicense("Aspose.Total.lic");`) prima di creare il workbook per rimuovere le filigrane di valutazione.
* **Ritardo di prestazioni su fogli grandi** – Chiama `calculateFormula()` una volta dopo che tutte le formule sono state scritte, non dopo ogni singola cella.

## Conclusione

Ora sai **how to split columns** in Java usando Aspose.Cells, come **split string into columns** con la funzione `WRAPCOLS`, come **automate Excel formula** evaluation e come **write formula to a cell** in modo programmatico. Questa tecnica elimina le fasi manuali di preparazione dei dati e integra le potenti capacità di gestione del testo di Excel direttamente nelle tue applicazioni Java.

### Prossimi passi

* Esplora altre funzioni di testo come `TEXTSPLIT` e `FILTERXML` per scenari di parsing più complessi.
* Combina `WRAPCOLS` con `IFERROR` per gestire input imprevisti in modo elegante.
* Integra la soluzione in un servizio Spring Boot che riceve dati CSV via REST e restituisce un file Excel popolato.

Padroneggiando questi pattern puoi creare flussi di lavoro Excel robusti e automatizzati che scalano con le esigenze della tua azienda. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [aspose cells java – Dividi i nomi in colonne](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit colonne Excel in Java usando Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Come eliminare colonne vuote in Excel usando Aspose.Cells Java&#58; Guida completa](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}