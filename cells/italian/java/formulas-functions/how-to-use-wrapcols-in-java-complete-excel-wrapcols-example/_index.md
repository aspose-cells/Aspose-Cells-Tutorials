---
category: general
date: 2026-06-21
description: Come utilizzare WRAPCOLS con Aspose.Cells Java per convertire un array
  in righe, scrivere una formula in una cella e popolare le celle con la formula –
  guida passo passo.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: it
og_description: Come utilizzare WRAPCOLS in Java con Aspose.Cells per convertire un
  array in righe, scrivere una formula in una cella e popolare le celle con la formula—tutto
  in una guida.
og_title: Come usare WRAPCOLS in Java – Esempio completo di WRAPCOLS in Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Come usare WRAPCOLS in Java – Esempio completo di WRAPCOLS in Excel
url: /it/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare WRAPCOLS in Java – Esempio completo di Excel WRAPCOLS

Ti sei mai chiesto **come utilizzare WRAPCOLS** quando devi trasformare un semplice array in una tabella ordinata in Excel? Non sei il solo. Molti sviluppatori si bloccano al primo sguardo alla funzione `WRAPCOLS` e pensano: “Come scrivo effettivamente questa formula in una cella da Java?” La buona notizia? È piuttosto semplice una volta conosciuti i passaggi giusti.

In questo tutorial percorreremo un esempio completo e eseguibile di Aspose.Cells per Java che **converte un array in righe**, scrive la formula direttamente in una cella e ti mostra come **popolare le celle con formula** per scenari reali. Alla fine avrai un quadro chiaro dell'**excel wrapcols example** e sarai pronto ad adattarlo ai tuoi progetti.

## Prerequisiti

Prima di immergerci, assicurati di avere:

- Java 17 o successiva (il codice funziona con qualsiasi JDK recente).
- Libreria Aspose.Cells per Java (puoi scaricare l'ultimo JAR da Maven Central).
- Una conoscenza di base della sintassi Java e delle formule Excel.
- Un IDE o un semplice editor di testo—non è necessario alcuno strumento speciale.

Hai tutto? Ottimo, cominciamo.

## Passo 1: Configurare il progetto e caricare una cartella di lavoro

Prima di tutto—crea un nuovo progetto Maven (o Gradle) e aggiungi la dipendenza Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Ora possiamo caricare una cartella di lavoro esistente (o crearne una nuova) e prendere il primo foglio di lavoro:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Perché carichiamo una cartella di lavoro** – Aspose.Cells lavora con una rappresentazione in‑memoria di un file Excel. Caricando (o creando) una cartella di lavoro otteniamo l'accesso a celle, righe e formule, indispensabili per qualsiasi operazione di **write formula to cell**.

## Passo 2: Inserire la formula WRAPCOLS in una cella

Il cuore del tutorial è la funzione `WRAPCOLS`. Essa prende un array monodimensionale e lo “avvolge” in un numero specificato di colonne, facendo traboccare automaticamente il resto in nuove righe. Ecco la sintassi che utilizzeremo:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Nota come la formula sia una semplice stringa passata a `setFormula`. Aspose.Cells si occupa del lavoro pesante—analizza la formula, la valuta e diffonde i risultati nel foglio. Questo è il modo più diretto per **populate cells with formula** senza iterare manualmente su righe e colonne.

### Cosa fa la formula

- `{1,2,3}` – un array letterale contenente tre numeri.
- `2` – il numero di colonne per riga.
- Risultato:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (vuoto)

Se volessi tre colonne invece, basta cambiare il secondo argomento in `3`, e l'array riempirebbe una singola riga.

## Passo 3: Salvare la cartella di lavoro e verificare l'output

Ora che la formula si trova in **A1**, salviamo la cartella di lavoro su disco così potrai aprirla in Excel e vedere il risultato:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Apri `output.xlsx` e vedrai esattamente ciò che il commento descriveva—due colonne nella prima riga e il valore rimanente nella seconda riga. Questa è l'essenza dell'**excel wrapcols example**.

## Passo 4: Estendere l'esempio – Convertire array più grandi

I progetti reali raramente lavorano solo con tre numeri. Supponiamo di avere una collezione più ampia, ad esempio `{10,20,30,40,50,60,70}` e di voler tre colonne per riga. Ecco come adegueresti il codice:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Ora il risultato inizia in **C5**, producendo:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Questo dimostra come puoi **convert array to rows** in modo dinamico, semplicemente modificando la stringa della formula. Nessun ciclo, nessuna assegnazione manuale di celle—Aspose.Cells gestisce il resto.

## Passo 5: Gestire casi limite e problemi comuni

### 1. Array vuoti

Se l'array letterale è vuoto (`{}`), `WRAPCOLS` restituisce un errore `#VALUE!`. Per evitare di rompere il foglio, proteggi la generazione della formula:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Dati non numerici

`WRAPCOLS` funziona anche con testo. Per esempio, `WRAPCOLS({"A","B","C","D"},2)` produce una disposizione a due colonne di stringhe. Ricorda solo di racchiudere le stringhe tra virgolette all'interno dell'array letterale.

### 3. Compatibilità

La funzione `WRAPCOLS` è disponibile in Excel 365 e Excel 2019+ (Office 2019, Excel per il web). Se devi supportare versioni più vecchie, dovrai ricorrere a cicli manuali o usare un'altra funzione compatibile con lo spill.

## Passo 6: Consigli pratici e trucchi da esperto

- **Consiglio da esperto:** Usa `Cell.setFormulaLocal` se ti serve un separatore locale (virgola vs punto e virgola) in base alle impostazioni regionali dell'utente.
- **Attenzione a:** Sovrascrivere dati esistenti. L'area di spill sostituirà qualsiasi contenuto già presente nell'intervallo di destinazione.
- **Nota sulle prestazioni:** Impostare una formula è poco costoso; il lavoro pesante avviene quando **salvi** o **ricalcoli** la cartella di lavoro. Se generi migliaia di formule, considera di disabilitare il calcolo automatico (`wb.calculateFormula()` più tardi) per velocizzare l'elaborazione.

## Esempio completo funzionante

Di seguito trovi la classe Java completa, pronta per l'esecuzione, che incorpora tutto ciò di cui abbiamo parlato:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Output previsto:** Apri `output.xlsx` e vedrai tre distinte aree di spill:

- **A1:B2** – numeri 1‑3 avvolti in due colonne.
- **C5:E7** – numeri 10‑70 avvolti in tre colonne.
- **G1:H2** – nomi di frutta avvolti in due colonne.

## Conclusione

Abbiamo appena coperto **come utilizzare WRAPCOLS** con Aspose.Cells per Java, mostrandoti come **convert array to rows**, **write formula to cell**, e **populate cells with formula** in modo pulito e riutilizzabile. L'approccio elimina i noiosi cicli, sfrutta il comportamento nativo di spill di Excel e mantiene il codice conciso.

Pronto per la prossima sfida? Prova a combinare `WRAPCOLS` con fonti di dati dinamiche—magari estraendo valori da un database, costruendo la stringa dell'array al volo e lasciando che Excel gestisca il layout. Puoi anche sperimentare con altre funzioni di spill come `SEQUENCE` o `FILTER` per creare report ancora più ricchi.

Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione completa di Aspose. Buona programmazione e goditi la potenza delle moderne formule Excel direttamente da Java!

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}