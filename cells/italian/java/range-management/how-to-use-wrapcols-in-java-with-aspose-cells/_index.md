---
category: general
date: 2026-11-22
description: Scopri come utilizzare wrapcols in Java per convertire un intervallo
  in colonne usando Aspose.Cells. Questa guida illustra passo passo la funzione wrap
  columns di Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: it
lastmod: 2026-11-22
og_description: Come utilizzare wrapcols in Java per convertire un intervallo in colonne.
  Segui questo tutorial per padroneggiare la funzione wrap columns di Excel con Aspose.Cells.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: Come usare wrapcols in Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Come usare wrapcols in Java con Aspose.Cells
url: /it/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare wrapcols in Java con Aspose.Cells

Se hai bisogno di **how to use wrapcols** per rimodellare i dati in una cartella di lavoro Excel, questo tutorial mostra l'intero processo. Vedrai come la formula WRAPCOLS trasforma un intervallo verticale in un insieme di colonne, rendendo facile presentare le liste affiancate.

La guida copre tutto ciò di cui hai bisogno: caricare una cartella di lavoro, applicare la formula WRAPCOLS e salvare il risultato. Non sono necessari riferimenti esterni, quindi puoi copiare il codice e eseguirlo immediatamente. Lungo il percorso spieghiamo anche la *wrap columns excel function* e dimostriamo come **convert range to columns** per scenari di reporting comuni.

## Cosa ti servirà

- Java 17 o versioni successive  
- Aspose.Cells per Java (ultima versione)  
- Un IDE Java (IntelliJ IDEA, Eclipse o VS Code)  
- Un file Excel di input (`input.xlsx`) contenente dati nella colonna A  

## Come usare wrapcols in Java con Aspose.Cells

I seguenti quattro passaggi implementano il flusso di lavoro **how to use wrapcols**. Ogni passaggio include uno snippet di codice, una spiegazione del motivo per cui è importante e un suggerimento per evitare errori comuni.

### Passo 1: Carica la cartella di lavoro

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Perché questo passaggio è importante*: `Workbook` è il punto di ingresso per tutte le operazioni Excel in Aspose.Cells. Caricare il file ti dà accesso a fogli di lavoro, celle e formule.  

**Suggerimento professionale**: Usa un percorso assoluto durante lo sviluppo per evitare `FileNotFoundException`. Passa a un percorso relativo una volta che il progetto è impacchettato.

### Passo 2: Accedi al primo foglio di lavoro

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Il primo foglio di lavoro (`index 0`) contiene tipicamente i dati che vuoi trasformare. Se i tuoi dati si trovano su un foglio diverso, cambia l'indice o usa `get("SheetName")`.  

**Perché questo passaggio è importante**: Lavorare con il foglio di lavoro corretto garantisce che la formula WRAPCOLS faccia riferimento all'intervallo previsto.

### Passo 3: Imposta la formula WRAPCOLS

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` è la **wrap columns excel function** che distribuisce i valori da `range` nel numero specificato di colonne. In questo esempio prendiamo i valori da `A1:A10` e li avvolgiamo in tre colonne, a partire da `A1`.  

**Perché questo passaggio è importante**: La formula fa il lavoro pesante—non è necessario alcun ciclo manuale o gestione di array.  

**Suggerimento per convert range to columns**: Regola il secondo argomento (`3`) per corrispondere al numero di colonne di cui hai bisogno. Se la lunghezza dell'intervallo non è un multiplo del conteggio delle colonne, l'ultima colonna conterrà gli elementi rimanenti.

### Passo 4: Salva la cartella di lavoro

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Il salvataggio scrive la formula WRAPCOLS in `output.xlsx`. Quando apri il file in Excel, la formula verrà valutata e mostrerà i dati avvolti in colonne.  

**Perché questo passaggio è importante**: Persistere la cartella di lavoro ti consente di verificare il risultato e condividere il file con utenti non‑Java.

![Wrapcols formula applied in Excel](wrapcols-example.png){: .align-center alt="Screenshot di come usare wrapcols in Excel"}

### Output previsto

Quando apri `output.xlsx`, le celle `A1:C4` (o quante righe sono necessarie) conterranno l'elenco originale da `A1:A10` distribuito su tre colonne. Il layout appare così:

| A | B | C |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
| Item 10 |   |   |

La **wrap columns excel function** riempie automaticamente le celle vuote con spazi, quindi non è necessario alcun codice di pulizia aggiuntivo.

## Comprendere la wrap columns excel function

La formula WRAPCOLS fa parte delle funzioni di array dinamici di Excel introdotte in Excel 365. Funziona in modo simile a `TEXTSPLIT` ma si concentra sulla distribuzione per colonne.  

- **Sintassi**: `=WRAPCOLS(source_range, columns)`  
- **Parametri**:  
  - `source_range` – l'intervallo verticale che vuoi rimodellare.  
  - `columns` – il numero di colonne in cui avvolgere i dati.  

Quando chiami `=WRAPCOLS(A1:A10, 3)`, Excel tratta l'origine come un array monodimensionale e riempie la prima colonna, poi la seconda, e così via, fino a quando tutti i valori sono collocati. Questo rende **how to use wrapcols** uno strumento perfetto per convertire un elenco a colonna singola in un report a più colonne senza VBA.

## Convertire un intervallo in colonne senza formule (opzionale)

Se preferisci eseguire l'operazione **convert range to columns** interamente in Java—senza fare affidamento sul motore di calcolo di Excel—puoi leggere i valori di origine, costruire un array bidimensionale e riscriverli manualmente:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

Questo snippet mostra un modo alternativo per **convert range to columns** quando hai bisogno di un controllo completo sull'output (ad esempio, applicare formattazioni personalizzate per colonna). Tuttavia, usare la **wrap columns excel function** tramite WRAPCOLS è solitamente più conciso e consente a Excel di gestire il ricalcolo automaticamente.

## Casi limite e migliori pratiche

- **Celle vuote**: WRAPCOLS tratta le celle vuote come spazi. Se il tuo intervallo di origine contiene lacune, l'output manterrà quegli spazi.  
- **Intervalli dinamici**: Usa un intervallo denominato o un riferimento a tabella (`Table1[Column]`) per far sì che la formula si adatti quando vengono aggiunte righe.  
- **Prestazioni**: Applicare la formula è O(1) perché Excel la valuta in modo pigro. La conversione programmatica mostrata sopra è O(n) e può essere più lenta per intervalli molto grandi.  
- **Compatibilità di versione**: La funzione WRAPCOLS richiede Excel 365 o versioni successive. Se devi supportare versioni più vecchie, affidati al metodo di conversione lato Java.

## Come usare wrapcols in altri scenari

- **Dashboard di reporting**: Trasforma un elenco verticale di nomi KPI in una tabella compatta con tre colonne per riga.  
- **Moduli di inserimento dati**: Converti una colonna di input utente in un layout affiancato per un confronto visivo più semplice.  
- **Esportazione in CSV**: Dopo aver applicato WRAPCOLS, salva la cartella di lavoro come CSV per ottenere una visualizzazione delimitata che corrisponde al layout delle colonne.

Ciascuno di questi casi segue lo stesso modello **how to use wrapcols**: carica, fai riferimento, imposta la formula, salva.

## Conclusione

Ora sai **how to use wrapcols** in Java con Aspose.Cells per **convert range to columns** in modo efficiente. Applicando la formula `WRAPCOLS` sfrutti la nativa *wrap columns excel function*, mantenendo il tuo codice conciso mentre concedi a Excel il pieno controllo sul calcolo e sulla visualizzazione.  

Sperimenta con diversi conteggi di colonne, intervalli dinamici o la conversione opzionale solo Java per adattarla alle esigenze del tuo progetto. Quando padroneggerai questa tecnica, rimodellare i dati in Excel diventerà un'operazione a una riga anziché un compito manuale.

---

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare wrapcols per convertire un elenco in più colonne in Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [Come usare WRAPCOLS in Java – Guida completa alle formule di array Excel](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [Come usare WRAPCOLS in Java – Esempio completo di Excel WRAPCOLS](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}