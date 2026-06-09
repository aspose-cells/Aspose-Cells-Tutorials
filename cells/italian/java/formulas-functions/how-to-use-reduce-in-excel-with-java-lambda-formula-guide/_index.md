---
category: general
date: 2026-06-08
description: Come utilizzare reduce in Excel con Java usando Aspose.Cells. Impara
  la formula lambda in Excel, gli array dinamici in Java, come scrivere una lambda
  e la somma con reduce in un chiaro tutorial passo‑passo.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: it
og_description: Come usare reduce in Excel con Java. Padroneggia la formula lambda
  in Excel, gli array dinamici in Java e la somma con reduce usando un esempio completo
  e eseguibile.
og_title: Come utilizzare Reduce in Excel con Java – Guida alla formula Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Come usare Reduce in Excel con Java – Guida alla formula Lambda
url: /it/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare Reduce in Excel con Java – Guida alle formule Lambda

Ti sei mai chiesto **come utilizzare reduce** in Excel quando scrivi codice Java? Non sei l'unico. Molti sviluppatori si trovano in difficoltà nel combinare le nuove funzioni di array dinamici di Excel con l'automazione basata su Java, e la risposta non è così criptica come sembra.

In questo tutorial percorreremo un esempio concreto che mostra **come utilizzare reduce** insieme a un'espressione **lambda formula Excel**, il tutto alimentato dalla libreria Aspose.Cells per Java. Alla fine sarai in grado di generare array dinamici in Java, scrivere funzioni lambda e calcolare una **somma con reduce**—senza dover manipolare manualmente i fogli di calcolo.

---

## Cosa costruirai

- Un nuovo workbook creato interamente da Java.  
- Un array dinamico **EXPAND** che riempie le celle A1:A5 con i numeri 1‑5.  
- Una formula **REDUCE** che somma quei numeri usando una **lambda formula Excel**.  
- Un file `.xlsx` salvato che potrai aprire in qualsiasi programma di fogli di calcolo per verificare il risultato.

Nessuna macro esterna, nessun VBA—solo puro codice Java e le funzioni moderne di Excel.

---

## Prerequisiti

- Java 17 (o qualsiasi JDK recente) – le versioni più vecchie funzionano ma perderai lo zucchero `var`.  
- Aspose.Cells per Java (la versione di prova gratuita è sufficiente per questa demo).  
- Familiarità di base con la sintassi Java e le formule Excel.  

Se sei nuovo alle **dynamic arrays java**, non preoccuparti—questa guida spiega ogni singolo elemento.

---

## Passo 1: Configura il tuo progetto e importa Aspose.Cells

Prima di tutto, aggiungi la dipendenza Maven di Aspose.Cells al tuo `pom.xml` (o scarica il JAR manualmente).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tip:** Mantieni le dipendenze aggiornate; le versioni più recenti migliorano la velocità di valutazione delle formule, il che è importante quando **come utilizzare reduce** in fogli di grandi dimensioni.

---

## Passo 2: Crea un Workbook e accedi al primo Worksheet

Ora creeremo un workbook nuovissimo. Questa è la base per imparare **come utilizzare reduce** perché l'oggetto workbook ci fornisce un sandbox dove inserire le formule.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Perché è importante:* La classe `Workbook` astrae l'intero file Excel, mentre `Worksheet` rappresenta una singola scheda. Vedrai più avanti come le **dynamic arrays java** possono riempire molte celle da una singola formula posizionata in A1.

---

## Passo 3: Genera un array verticale con EXPAND

La funzione `EXPAND` di Excel può versare valori in un intervallo. La useremo per creare i numeri 1 ‑ 5 nella colonna A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Se apri il workbook risultante, le celle A1:A5 conterranno 1, 2, 3, 4, 5. Questa è la parte **dynamic arrays java**—una formula popola un intero intervallo.

---

## Passo 4: Scrivi una lambda REDUCE per sommare l'array

Qui rispondiamo alla domanda centrale: **come utilizzare reduce** in Excel da Java. La funzione `REDUCE` itera su un array, applicando una lambda che fornisci. Nel nostro caso sommeremo i numeri.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Analizziamo il tutto:

- `0` – il valore iniziale dell'accumulatore (`acc`).  
- `A1:A5` – l'array generato con **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – la **lambda formula Excel** che aggiunge ogni elemento (`x`) all'accumulatore (`acc`).  

Quando la formula viene eseguita, `B1` conterrà **15**, la **somma con reduce** dei numeri 1‑5.

> **Come scrivere lambda** in Excel? Pensala come una funzione anonima dove i primi argomenti sono i parametri e l'espressione finale è il valore di ritorno. In Java inseriamo semplicemente il testo; il motore di Excel fa il lavoro pesante.

---

## Passo 5: Salva il Workbook

Infine, persisti il workbook su disco così potrai aprirlo in Excel, Google Sheets o qualsiasi visualizzatore che supporti `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Apri il file e vedrai:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

La **somma con reduce** appare in B1, confermando che abbiamo dimostrato con successo **come utilizzare reduce** insieme a una **lambda formula Excel** da Java.

---

## Esempio completo funzionante

Di seguito trovi il programma Java completo, pronto per l'esecuzione. Copialo nel tuo IDE, regola la directory di output e premi **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Output previsto** quando apri `new-functions.xlsx`:

- Le celle **A1:A5** contengono `1, 2, 3, 4, 5`.  
- La cella **B1** mostra `15`, confermando la **somma con reduce**.

---

## Domande frequenti & casi limite

### E se avessi bisogno di un array orizzontale invece che verticale?

Scambia gli argomenti colonna/riga in `EXPAND`. Per uno spill orizzontale su B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Posso usare REDUCE per moltiplicare invece di sommare?

Assolutamente. Basta cambiare il corpo della lambda:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Ora B1 mostrerà `120` (5 ! = 120).

### Aspose.Cells supporta funzioni LAMBDA personalizzate?

Sì, puoi definire funzioni LAMBDA nominate tramite la collezione `Names` del workbook, quindi chiamarle come qualsiasi formula integrata. È un approfondimento per un tutorial futuro su **come scrivere lambda** che vivono oltre una singola cella.

### E le versioni più vecchie di Excel che non riconoscono REDUCE?

Se punti a Excel 2019 o versioni precedenti, il motore restituirà `#NAME?`. In questi casi


## Cosa dovresti imparare dopo?


I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}