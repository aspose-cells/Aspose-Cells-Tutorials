---
category: general
date: 2026-10-10
description: Crea una cartella di lavoro Excel in C# e utilizza la funzione WRAPCOLS
  per suddividere i dati dell'array in colonne. Segui una guida completa passo‑passo
  con codice eseguibile.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: it
lastmod: 2026-10-10
og_description: Crea una cartella di lavoro Excel in C# e applica la funzione WRAPCOLS
  per suddividere i dati dell'array in colonne. Questa guida mostra il codice completo
  e spiega ogni passaggio.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Crea una cartella di lavoro Excel e suddividi i dati con WRAPCOLS in C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come creare una cartella di lavoro Excel e suddividere i dati con WRAPCOLS
  in C#
url: /it/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una cartella di lavoro Excel e dividere i dati con WRAPCOLS in C#

Se devi **creare una cartella di lavoro Excel** in modo programmatico, questa guida ti mostra esattamente come farlo e come **dividere i dati di un array** tra le colonne usando la funzione `WRAPCOLS`. Otterrai un esempio completo e funzionante che produce un file `.xlsx` con i dati distribuiti in tre colonne.

Il tutorial copre tutto ciò di cui hai bisogno: i pacchetti NuGet richiesti, ogni riga di codice, perché la formula `WRAPCOLS` funziona e come adattare la soluzione a diverse dimensioni di array o numeri di colonne. Alla fine sarai in grado di integrare la tecnica **use wrapcols function** in qualsiasi progetto C# che genera file Excel.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 SDK o versioni successive installate  
* Un IDE C# (Visual Studio, VS Code, Rider, ecc.)  
* Il pacchetto NuGet **Aspose.Cells for .NET** – la libreria che fornisce la classe `Workbook` usata negli esempi  

Non è necessaria un'installazione di Office; Aspose.Cells scrive il file `.xlsx` direttamente.

## Passo 1 – creare una cartella di lavoro Excel

Il primo compito è istanziare un nuovo oggetto workbook e ottenere un riferimento al primo foglio di lavoro. Questo passo è la base per qualsiasi ulteriore manipolazione.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` rappresenta l'intero file, mentre `Worksheet` rappresenta un singolo foglio. Creando la cartella di lavoro in memoria eviti I/O su disco fino a quando non la salvi esplicitamente.

## Passo 2 – applicare WRAPCOLS per dividere le colonne dell'array

Ora inserirai una formula nella cella **A1** che utilizza `WRAPCOLS`. La funzione riceve due argomenti: l'array di origine e il numero di colonne in cui vuoi che l'array venga avvolto.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Perché funziona:** `WRAPCOLS` prende l'array piatto `{1,2,3,4,5,6}` e lo riempie riga per riga, creando tre colonne per riga. Il primo argomento può essere qualsiasi letterale di array Excel, un intervallo denominato o una formula di array dinamico. Il secondo argomento (`3`) indica a Excel quante colonne generare prima di passare alla riga successiva.

### Utilizzare la funzione con diversi tipi di dati

La funzione `WRAPCOLS` non è limitata ai numeri. Puoi dividere valori di testo, date o tipi misti:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Quando l'array di origine contiene stringhe, Excel tratta automaticamente il risultato come celle di testo. Questa flessibilità ti consente di **excel formula split data** per report, dashboard o attività di migrazione dati.

## Passo 3 – calcolare le formule così il foglio è popolato

Le formule sono memorizzate come stringhe finché non chiedi al workbook di valutarle. Chiamare `CalculateFormula` forza la valutazione e scrive i risultati nelle celle.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Senza questa chiamata il file salvato conterrebbe solo il testo della formula, non i valori calcolati. Il metodo opera su tutto il workbook, quindi puoi inserire altre formule altrove e tutte verranno risolte con una singola chiamata.

## Passo 4 – salvare il workbook per vedere il risultato

Infine, scrivi il workbook su disco. Scegli una cartella in cui hai i permessi di scrittura e assegna al file un nome chiaro.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Quando apri `output.xlsx` in Excel (o in qualsiasi visualizzatore compatibile), vedrai:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Se hai usato l'esempio a tipi misti, le righe 3‑4 conterranno rispettivamente testo e numeri.

## Varianti avanzate e gestione dei casi limite

### Numero di colonne variabile a runtime

Spesso il numero di colonne necessario dipende dall'input dell'utente. Puoi costruire la stringa della formula in modo dinamico:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Array di grandi dimensioni e performance

`WRAPCOLS` può gestire migliaia di elementi, ma valutare array estremamente grandi in una singola cella può aumentare il tempo di calcolo. Se noti rallentamenti:

* Suddividi l'array di origine in blocchi più piccoli e scrivi ogni blocco in una cella di partenza diversa.  
* Usa `WorkbookSettings` per abilitare il calcolo multithread:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Gestione delle celle vuote

Se l'array di origine contiene stringhe vuote (`""`) o valori `NULL`, `WRAPCOLS` inserisce celle vuote, preservando la disposizione delle colonne. Questo comportamento è utile quando hai bisogno di colonne segnaposto per inserimenti futuri.

### Utilizzare intervalli denominati invece di letterali

Per una migliore manutenibilità, definisci un intervallo denominato che contiene i dati di origine, quindi fai riferimento a esso:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Ora la formula legge i dati dal foglio stesso, consentendo **how to use wrapcols** in scenari di reporting dinamico.

## Errori comuni e consigli professionali

* **Non omettere il secondo argomento.** `WRAPCOLS(array)` senza il conteggio delle colonne restituisce una singola colonna, vanificando lo scopo di dividere i dati.  
* **Evita di mescolare dimensioni di array.** L'array di origine deve essere monodimensionale; fornire un array bidimensionale (es. `{ {1,2},{3,4} }`) genera un errore `#VALUE!`.  
* **Salva dopo il calcolo.** Se chiami `wb.Save` prima di `CalculateFormula`, il file conterrà solo il testo della formula.  
* **Verifica i permessi di file.** Quando esegui in ambienti con restrizioni (es. ASP.NET), assicurati che l'identità del processo possa scrivere nella cartella di destinazione.  

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire. Include tutti gli import, la gestione degli errori e i commenti.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Eseguendo il programma otterrai `output.xlsx` con tre regioni distinte che dimostrano **excel formula split data** usando la funzione `WRAPCOLS`.

## Conclusione

Ora sai come **creare file Excel workbook** in C# e come **usare la funzione wrapcols** per **dividere le colonne di un array** in modo efficiente. I passaggi principali—instanziare `Workbook`, inserire la formula `WRAPCOLS`, calcolare e salvare—formano un modello riutilizzabile per qualsiasi attività di automazione che richieda la distribuzione dei dati tra colonne.

Da qui puoi:

* Combinare `WRAPCOLS` con altre funzioni di array dinamico come `FILTER` o `SORT`.  
* Esportare grandi set di dati da database e lasciare che Excel gestisca automaticamente il layout.  
* Costruire report guidati dall'utente dove il numero di colonne è selezionato tramite un controllo UI.

Sperimenta con diverse fonti di array, conteggi di colonne e formule aggiuntive per estendere questa base. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}