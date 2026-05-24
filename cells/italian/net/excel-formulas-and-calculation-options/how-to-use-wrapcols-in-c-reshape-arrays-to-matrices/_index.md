---
category: general
date: 2026-05-23
description: Come utilizzare WRAPCOLS in C# per rimodellare un array 1D in una matrice
  2D. Impara la funzione wrap columns, scrivi la formula nella cella e converti facilmente
  da 1D a 2D.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: it
og_description: Come usare WRAPCOLS in C# ti permette di rimodellare un array 1D in
  una matrice 2D con una singola formula. Segui questa guida per scrivere la formula
  nella cella e padroneggiare la funzione di avvolgimento delle colonne.
og_title: Come utilizzare WRAPCOLS in C# – Trasformare gli array in matrici
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Come usare WRAPCOLS in C# – Rimodellare gli array in matrici
url: /it/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare WRAPCOLS in C# – Rimodellare gli array in matrici

Ti sei mai chiesto **come usare WRAPCOLS** quando devi trasformare una lista piatta di numeri in una tabella ordinata? Non sei solo—molti sviluppatori si trovano in difficoltà quando provano a convertire una lista unidimensionale in una griglia bidimensionale senza scrivere molto codice di loop. La buona notizia? La funzione WRAPCOLS (a volte chiamata wrap columns function) fa il lavoro pesante in una sola riga, e puoi inserirla direttamente in una cartella di lavoro Excel da C#.

In questo tutorial percorreremo l'intero processo: dalla creazione di una cartella di lavoro, alla **scrittura della formula in una cella**, al **rimodellamento dell'array in una matrice**, e infine al **convertire 1d in 2d** usando la formula WRAPCOLS. Alla fine avrai uno snippet riutilizzabile che funziona con qualsiasi array numerico, e comprenderai perché la wrap columns function è spesso un'alternativa più pulita al rimodellamento manuale degli array.

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.6+)  
* La libreria **Aspose.Cells for .NET** (versione di prova gratuita o copia con licenza) – è il componente che ci fornisce gli oggetti `Workbook`, `Worksheet` e `Cell` usati di seguito.  
* Una conoscenza di base della sintassi C#—non è necessario conoscere Excel in modo avanzato.

Li hai? Ottimo—mettiamoci al lavoro.

![Resulting 2x3 matrix after using WRAPCOLS function in C# – how to use WRAPCOLS](https://example.com/images/wrapcols-result.png "How to use WRAPCOLS – resulting 2x3 matrix")

## Passo 1: Configurare il progetto e aggiungere Aspose.Cells

### Perché è importante

Potresti provare a implementare la tua logica di matrice, ma la **wrap columns function** gestisce già i casi limite come divisioni non uniformi e input vuoti. Aggiungere il pacchetto NuGet Aspose.Cells ci fornisce un'API pulita per interagire con le formule Excel direttamente da C#.

```bash
dotnet add package Aspose.Cells
```

*Suggerimento:* Se usi Visual Studio, fai clic destro sul progetto → **Manage NuGet Packages** → cerca **Aspose.Cells** e installa l'ultima versione stabile.

## Passo 2: Creare una nuova cartella di lavoro (o caricarne una esistente)

Ora che la libreria è a posto, possiamo creare un oggetto workbook. È qui che avverrà il passo di **scrittura della formula in una cella**.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Qui abbiamo creato un workbook nuovo di zecca; potresti anche caricare un file esistente con `new Workbook("path/to/file.xlsx")` se devi inserire la matrice in un modello pre‑formattato.

## Passo 3: Inserire la formula WRAPCOLS in una cella

### Il nucleo di “come usare WRAPCOLS”

La funzione **WRAPCOLS** accetta due argomenti: un array (o intervallo) e il numero di colonne desiderate per riga. Nel nostro caso rimodelleremo l'array letterale `{1,2,3,4,5,6}` in **2 righe × 3 colonne**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Nota come la formula rispecchia ciò che digiteresti direttamente in Excel. Posizionandola in `Cells[0,0]` (cella **A1**) stiamo **scrivendo la formula in una cella** senza alcuna logica aggiuntiva.

## Passo 4: Forzare il calcolo affinché la formula venga valutata

Aspose.Cells non valuta le formule automaticamente a meno che non lo si indichi. Questo passo assicura che la cartella di lavoro contenga effettivamente la matrice rimodellata.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

Se salti questa riga, le celle mostreranno ancora il testo della formula invece dei valori calcolati.

## Passo 5: Leggere nuovamente il risultato (opzionale, ma utile per verifica)

Potresti voler confermare che l'operazione di **rimodellamento dell'array in matrice** sia riuscita. Ecco un rapido ciclo che stampa la griglia 2‑by‑3 risultante sulla console.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Output previsto

```
1   2   3
4   5   6
```

La console mostra esattamente lo stesso layout che vedresti in Excel dopo l'esecuzione della formula WRAPCOLS. Questa è la trasformazione **convertire 1d in 2d** in azione.

## Passo 6: Gestire i casi limite – Cosa succede se la lunghezza dell'array non è un multiplo di colonne?

Se l'array di origine ha, ad esempio, 7 elementi e richiedi 3 colonne, WRAPCOLS creerà l'ultima riga con gli elementi rimanenti e lascerà le celle rimanenti vuote. Ecco una rapida modifica per dimostrarlo:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Risultato:

```
1   2   3
4   5   6
7       
```

La **wrap columns function** aggiunge elegantemente celle vuote all'ultima riga, così non è necessario codice aggiuntivo per gestire dimensioni non corrispondenti.

## Passo 7: Usare WRAPCOLS con dati dinamici

Nei progetti reali raramente coderai l'array in modo statico. Invece costruirai una rappresentazione stringa da una collezione C#:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Ora hai **convertito 1d in 2d** per qualsiasi lunghezza, e ottieni ancora lo stesso output di matrice pulito. La formula è costruita a runtime, ma la **wrap columns function** sottostante rimane la stessa.

## Problemi comuni e consigli professionali

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Dimenticare `workbook.CalculateFormula()` | Aspose.Cells lascia le formule non valutate | Chiama sempre il metodo dopo aver impostato una formula |
| Usare un literal di array non numerico | WRAPCOLS si aspetta numeri o stringhe che possono essere convertite | Assicurati che il literal contenga solo numeri (o stringhe tra virgolette) |
| Sovrascrivere dati esistenti involontariamente | Posizionare la formula in una cella che contiene già dati | Scegli una cella vuota (es., A1) o cancella prima l'intervallo |
| Non fare riferimento all'indice del foglio corretto | `Worksheets[0]` è il primo foglio, ma potresti averne aggiunti altri | Verifica `worksheet = workbook.Worksheets["SheetName"];` se necessario |

## Perché WRAPCOLS supera i loop manuali

* **Readability** – Una riga di formula sostituisce decine di loop `for`.  
* **Performance** – Il motore nativo di Excel è altamente ottimizzato per le formule array.  
* **Maintainability** – I futuri sviluppatori possono vedere immediatamente l'intento: “avvolgere questi valori in colonne”.  
* **Portability** – La stessa formula funziona se esporti la cartella di lavoro su Google Sheets o LibreOffice—non è necessaria logica specifica C#.

## Esempio completo funzionante (pronto per copia‑incolla)



## Tutorial correlati

- [Come usare Aspose.Cells per .NET per mostrare gli intervalli di celle come etichette dati nei grafici](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [Come usare Aspose.Cells per .NET per raggruppare righe e colonne in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Come usare la funzione IF di Excel](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}