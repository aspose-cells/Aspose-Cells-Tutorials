---
category: general
date: 2026-11-16
description: Impara come espandere un array in Excel usando Aspose.Cells, le funzioni
  di array dinamico e un riduttore lambda, quindi scrivi il file Excel da C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: it
lastmod: 2026-11-16
og_description: Come espandere un array in Excel usando Aspose.Cells, le funzioni
  di array dinamico e un riduttore lambda. Segui l'esempio completo in C# per scrivere
  il file Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Come espandere un array in Excel con Aspose.Cells – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come espandere un array in Excel con Aspose.Cells
url: /it/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come espandere un array in Excel con Aspose.Cells

Se hai bisogno di **come espandere un array** in un foglio di lavoro Excel da C#, questo tutorial mostra i passaggi esatti. Creerai una cartella di lavoro Excel, utilizzerai funzioni di array dinamici come `EXPAND` e `REDUCE`, applicherai un accumulatore **lambda**, e infine **scriverai il file Excel** su disco. L'approccio funziona con Aspose.Cells 23.10 o versioni successive e non richiede l'installazione manuale di Excel.

Al termine di questa guida avrai un file `ExpandReduceDemo.xlsx` completamente funzionante che dimostra la potenza delle formule di array dinamici in un contesto programmatico.

## Cosa ti serve

- .NET 6.0 (o qualsiasi versione .NET supportata da Aspose.Cells)
- Pacchetto Aspose.Cells per .NET (`dotnet add package Aspose.Cells`)
- Un editor di codice o IDE (Visual Studio, VS Code, Rider, ecc.)

Non è necessario alcun ulteriore interop COM o installazione di Office perché Aspose.Cells gestisce il formato del file internamente.

## Passo 1: Creare una cartella di lavoro Excel

Il primo compito è **creare una cartella di lavoro Excel** in memoria. Aspose.Cells fornisce la classe `Workbook`, che rappresenta un intero file XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Perché è importante:** Istanziare un `Workbook` ti fornisce una tela pulita. Il foglio di lavoro predefinito è già pronto, quindi non è necessario aggiungerne uno manualmente a meno che tu non voglia più fogli.

## Passo 2: Inserire una costante di array verticale

Il motore di array dinamici di Excel può lavorare con costanti di array letterali. Inseriremo l'array verticale `{1;2;3;4;5}` nella cella **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Suggerimento:** Il punto e virgola (`;`) separa le righe nella costante, mentre una virgola (`,`) separerebbe le colonne. Questo rispecchia la sintassi di Excel.

## Passo 3: Espandere l'array in una matrice

Ora rispondiamo alla domanda principale – **come espandere un array** – usando la funzione `EXPAND`. La formula espande l'array a colonna singola in una matrice 5 righe × 2 colonne, a partire da **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Perché EXPAND?** `EXPAND(source, rows, cols)` costringe l'intervallo di origine a occupare le dimensioni specificate, riempiendo con celle vuote se necessario. È il modo più leggibile per generare una matrice più grande da un singolo array.

## Passo 4: Ridurre la matrice con un accumulatore lambda

La funzione `REDUCE` itera su un intervallo e aggrega i valori usando un'espressione **lambda**. Qui sommiamo i valori di ogni colonna in una singola colonna, posizionando il risultato in **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Come usare lambda:** `LAMBDA(acc, val, acc+val)` riceve l'accumulatore corrente (`acc`) e il valore della cella successiva (`val`). Restituisce il nuovo accumulatore, eseguendo effettivamente un totale cumulativo. Questo dimostra **come usare lambda** nelle formule Excel dal codice.

## Passo 5: Calcolare le formule affinché i risultati compaiano

Aspose.Cells non valuta automaticamente le formule quando le imposti. Chiamare `CalculateFormula` forza il motore a calcolare ogni formula nella cartella di lavoro.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Nota:** Se apri il file generato in Excel, i valori saranno già visibili perché sono stati pre‑calcolati.

## Passo 6: Scrivere il file Excel su disco

Infine, **scrivi il file Excel** usando il metodo `Save`. Scegli una cartella per la quale hai i permessi di scrittura.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Risultato atteso

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **La colonna B** e **C** contengono la matrice 5 × 2 prodotta da `EXPAND`.
- **La cella D1** mostra `15`, la somma di tutti i numeri, calcolata dalla formula `REDUCE` + **lambda**.

## Domande comuni e casi limite

- **Posso espandere a più colonne rispetto a quelle fornite dalla sorgente?**  
  Sì. `EXPAND` riempie le colonne mancanti con celle vuote. Lo stesso vale per le righe.

- **Cosa succede se l'array di origine è orizzontale (`{1,2,3,4,5}`)?**  
  `EXPAND` tratterà l'origine come una singola riga; puoi comunque specificare righe e colonne per rimodellarlo.

- **`REDUCE` funziona con dati non numerici?**  
  La lambda deve restituire un valore compatibile con il tipo dell'accumulatore. Per la concatenazione di testo potresti usare `LAMBDA(acc, val, acc & val)`.

- **Devo chiamare `CalculateFormula` per ogni modifica?**  
  Solo quando hai bisogno dei valori calcolati prima di salvare. Excel ricalcolerà all'apertura se lo salti.

## Consigli professionali

- **Performance:** Per cartelle di lavoro grandi, chiama `workbook.CalculateFormula` una sola volta dopo aver impostato tutte le formule, invece di farlo dopo ogni cella.
- **Sicurezza della versione:** `EXPAND` e `REDUCE` sono disponibili in Excel 365 e versioni successive. Aspose.Cells le implementa indipendentemente dalla versione di Excel di destinazione perché il motore di calcolo è integrato.
- **Debug delle formule:** Usa `sheet.Cells["B1"].Formula` per leggere la stringa esatta impostata; questo aiuta quando costruisci formule in modo dinamico.

## Conclusione

Ora sai **come espandere un array** in Excel usando Aspose.Cells, sfruttare le **funzioni di array dinamici**, applicare una **lambda** con `REDUCE` e **scrivere il file Excel** da C#. Questo esempio end‑to‑end può essere adattato a trasformazioni di dati più complesse, come la trasposizione di matrici, totali cumulativi o aggregazioni personalizzate.

---

*Passi successivi:*  
- Esplora altre funzioni dinamiche come `FILTER`, `SORT` e `UNIQUE`.  
- Combina più espressioni `LAMBDA` per costruire funzioni definite dall'utente riutilizzabili.  
- Integra la generazione della cartella di lavoro nelle API ASP.NET Core per la creazione di report al volo.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare una cartella di lavoro Excel C# con una formula di array dinamico](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Come espandere un array in Excel e popolare un modello](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Come espandere un array in C# con Aspose.Cells – Guida passo‑passo](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}