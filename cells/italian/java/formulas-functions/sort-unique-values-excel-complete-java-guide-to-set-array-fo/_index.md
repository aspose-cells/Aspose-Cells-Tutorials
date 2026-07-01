---
category: general
date: 2026-06-30
description: Ordina valori unici in Excel usando Java. Scopri come impostare la formula,
  ricalcolare le formule e generare un elenco unico in Excel con Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: it
og_description: Ordina valori unici in Excel con Java. Questa guida mostra come impostare
  la formula, ricalcolare le formule e generare un elenco unico in Excel in pochi
  minuti.
og_title: Ordina valori unici in Excel – Tutorial Java per formule matriciali
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Ordina valori unici in Excel – Guida completa Java per impostare formule di
  matrice
url: /it/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ordina Valori Unici in Excel – Guida Completa Java per Impostare Formule di Array

Ti sei mai chiesto come **ordinare valori unici in Excel** senza trascinare le formule? Non sei l'unico. In molti scenari di reporting è necessario un elenco pulito, ordinato alfabeticamente, di voci distinte, e farlo manualmente è una seccatura.  

La buona notizia? Con poche righe di codice Java puoi **impostare una formula di array** su un foglio di lavoro, poi **ricalcolare le formule** così l'intervallo espanso si riempie automaticamente. In questo tutorial passeremo in rassegna tutto—dalla creazione di una cartella di lavoro alla generazione di un elenco unico in stile Excel—così potrai incorporare la soluzione direttamente nella tua applicazione.

## Cosa Copre Questo Tutorial

- Configurare un progetto Java con Aspose.Cells (la libreria che alimenta lo snippet di codice).  
- Utilizzare le funzioni `SORT` e `UNIQUE` insieme per **generare un elenco unico in Excel**.  
- Applicare una **formula di array** a una cella programmaticamente.  
- Attivare un passaggio di calcolo in modo che il passaggio **come ricalcolare le formule** avvenga istantaneamente.  
- Verificare l'output e perfezionare la soluzione per casi limite come celle vuote o intervalli non contigui.

Alla fine di questa guida sarai in grado di inserire un metodo pronto all'uso in qualsiasi servizio Java che necessita di esportare fogli Excel puliti.

> **Suggerimento Pro:** Se stai già usando Maven, aggiungere Aspose.Cells come dipendenza ti salva dal gestire manualmente i file JAR.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Java 8 o superiore | Aspose.Cells è destinato a Java 8+. |
| Maven (o Gradle) | Semplifica la gestione delle dipendenze. |
| Aspose.Cells per Java | Fornisce le API `Workbook`, `Worksheet` e delle formule che utilizzeremo. |
| Familiarità di base con le funzioni di Excel | Comprendere `SORT` e `UNIQUE` ti aiuta ad adattare il codice. |

> *Se non hai ancora Aspose.Cells, aggiungi questo al tuo `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Passo 1: Creare una Nuova Cartella di Lavoro (Inizio di Come Impostare la Formula)

Per prima cosa abbiamo bisogno di una cartella di lavoro vuota. Pensala come una tela bianca dove più tardi **imposteremo una formula di array** nella cella `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Perché creare una nuova cartella di lavoro?*  
> Garantisce un ambiente pulito, evitando formule nascoste che potrebbero interferire con i nostri dati di test.

---

## Passo 2: Popolare Dati di Esempio (Opzionale ma Utile)

Per vedere chiaramente il risultato, riempiamo la colonna **B** con alcune voci duplicate.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Perché usare la colonna B?*  
> La formula che scriveremo fa riferimento a `B1:B10`, quindi mantenere i dati lì rispecchia l'esempio classico di Excel.

---

## Passo 3: Impostare una Formula di Array Che **Ordina Valori Unici in Excel**

Ora avviene la magia. Combiniamo `UNIQUE` (per rimuovere i duplicati) con `SORT` (per ordinarli alfabeticamente). L'espressione risultante è una **formula di array**, il che significa che si espanderà automaticamente nelle celle adiacenti.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Come Funziona

- `UNIQUE(B1:B10)` esamina l'intervallo e restituisce un array verticale di stringhe distinte.  
- `SORT(...)` prende quell'array e lo ordina in ordine crescente.  
- Avvolgere il tutto in `=` e chiamare `setFormulaArray` indica ad Aspose.Cells di trattare il risultato come un **array espanso**, proprio come farebbe Excel.

> **Nota:** Se stai usando una versione più vecchia di Excel che non dispone di `SORT` o `UNIQUE`, puoi tornare a `SORT(UNIQUE(...))` con la funzione **LET** o utilizzare formule di array legacy (`=INDEX(...)`). Il tutorial si concentra sull'approccio moderno degli array dinamici perché è il modo più pulito per **generare un elenco unico in Excel** oggi.

---

## Passo 4: Ricalcolare le Formule Così l'Intervallo Espanso Viene Popolato

Dopo che la formula è stata inserita, la cartella di lavoro non la valuta automaticamente. È qui che entra in gioco il passaggio **come ricalcolare le formule**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Chiamare `calculateFormula()` forza Aspose.Cells a eseguire il motore di Excel, riempiendo le celle `A1`, `A2`, … con i valori unici ordinati.

> *Perché non fare affidamento sulla valutazione pigra?*  
> In un contesto server‑side spesso è necessario avere i dati pronti per l'esportazione (CSV, PDF, ecc.) subito dopo il calcolo, quindi una chiamata esplicita garantisce coerenza.

---

## Passo 5: Verificare il Risultato (Debug Opzionale)

È sempre una buona idea stampare i valori espansi sulla console—soprattutto quando ti stai insegnando una nuova API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Eseguendo il programma stampa:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Apri `SortedUniqueValues.xlsx` e vedrai gli stessi dati espandersi da `A1` verso il basso.

---

## Gestione dei Casi Limite

### Celle Vuote nell'Intervallo di Origine

Se `B1:B10` contiene celle vuote, `UNIQUE` le tratterà come una voce distinta. Per ignorare le celle vuote, avvolgi l'intervallo con `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Dati Non Contigui

Quando i tuoi dati si trovano in più colonne, puoi unirli con `CHOOSE` o `TEXTJOIN` prima di applicare `UNIQUE`. Ad esempio:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Queste modifiche dimostrano la flessibilità di **come impostare la formula** per scenari più complessi.

---

## Esempio Completo Funzionante (Tutti i Passi Combinati)

Di seguito trovi il programma Java completo e eseguibile. Copialo e incollalo nel tuo IDE, aggiungi la dipendenza Aspose.Cells e premi *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Output previsto** (mostrato nella console) corrisponde all'elenco ordinato e deduplicato di cui abbiamo parlato prima. Aprendo il file Excel generato si vedono gli stessi valori espandersi da `A1` verso il basso.

---

## Domande Frequenti

**D: Questo funziona con versioni più vecchie di Excel (pre‑Office 365)?**  
R: Le funzioni `SORT` e `UNIQUE` fanno parte del motore Dynamic Array introdotto in Excel 365. Per file legacy dovresti usare formule di array classiche come `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells può ancora valutarle, ma la sintassi è più verbosa.

**D: Posso impostare la formula di array su un intervallo diverso da `A1`?**  
R: Assolutamente. Basta cambiare l'indirizzo in `cells.get("A1")`. L'array espanso inizierà sempre dalla cella specificata ed espanderà verso destra e verso il basso secondo necessità.

**D: E se i miei dati di origine sono più grandi di `B1:B10`?**  
R: Sostituisci l'intervallo statico con uno dinamico, ad esempio `B:B` o un intervallo denominato. La formula diventa `=SORT(UNIQUE(B:B))`. Fai attenzione ai riferimenti a intere colonne su fogli molto grandi; possono influire sulle prestazioni.

---

## Conclusione

Abbiamo appena coperto **come impostare una formula** in Java per **ordinare valori unici in Excel**, come **ricalcolare le formule**, e come **generare un elenco unico in Excel** usando la potente API di Aspose.Cells. I passaggi sono semplici: creare una cartella di lavoro, popolare i dati, applicare una formula di array, avviare il calcolo e verificare il risultato.  

Da qui puoi espandere—aggiungere formattazione condizionale, esportare in PDF, o integrare il metodo in un servizio web che fornisce report pronti. L'idea di base rimane la stessa: lasciare che le funzioni di Excel facciano il lavoro pesante e far orchestrare il processo a Java.  

Pronto a migliorare la tua automazione di Excel? Prova a sostituire `SORT` con `SORTBY` per ordinare per una colonna secondaria, o sperimenta con `FILTER` per escludere righe che non soddisfano le regole di business. Le possibilità sono praticamente infinite.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}