---
category: general
date: 2026-03-22
description: Come usare le lambda in C# per lavorare con le formule di Excel. Impara
  a scrivere una formula in una cella, convertire un intervallo in un array, visualizzare
  l'array nella console e calcolare la cotangente in Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: it
og_description: Come usare lambda in C# per manipolare le formule di Excel, convertire
  un intervallo in array, scrivere una formula in una cella, visualizzare l'array
  nella console e calcolare la cotangente in Excel.
og_title: Come usare Lambda in C# con le formule Excel – Passo dopo passo
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Come utilizzare le lambda in C# con le formule Excel – Guida completa
url: /it/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare Lambda in C# con le formule di Excel – Guida completa

Ti sei mai chiesto **come usare lambda** quando automatizzi Excel da C#? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono combinare la potenza delle nuove funzioni di array dinamici di Excel con la capacità `LAMBDA` di C#. La buona notizia? È in realtà piuttosto semplice una volta che vedi come i pezzi si incastrano.

In questo tutorial vedremo **come scrivere una formula in una cella**, **come convertire un intervallo in un array**, **come visualizzare quell'array nella console**, e persino **come calcolare la cotangente in Excel**—tutto mostrando **come usare lambda** all'interno di una chiamata `REDUCE`. Alla fine avrai uno snippet eseguibile da inserire in qualsiasi progetto .NET che fa riferimento a Aspose.Cells (o a una libreria simile).

---

## Cosa imparerai

- Come **scrivere una formula in una cella** usando C#.
- Come **convertire un intervallo in un array** con la funzione `EXPAND`.
- Come **visualizzare l'array nella console** dopo il calcolo.
- Come **calcolare la cotangente in Excel** usando `COT` e `COTH`.
- La sintassi esatta per **come usare lambda** all'interno della funzione `REDUCE` di Excel da C#.

> **Prerequisito:** È necessario avere una versione recente di .NET (Core 6+ o .NET Framework 4.7+) e la libreria Aspose.Cells per .NET installata tramite NuGet.

---

## Passo 1: Configurare la cartella di lavoro e scrivere la formula nella cella

La prima cosa che facciamo è creare una nuova cartella di lavoro e ottenere il primo foglio. Poi **scriviamo una formula in una cella** – in questo caso `A1` conterrà il risultato di una chiamata `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Perché è importante:** Scrivere la formula direttamente dal codice ti permette di generare fogli di calcolo complessi al volo senza aprire Excel. Inoltre prepara il terreno per il passo successivo, dove **convertiamo l'intervallo in un array**.

---

## Passo 2: Convertire l'intervallo in un array con EXPAND

`EXPAND` è il modo di Excel per trasformare un piccolo intervallo in una matrice più grande. Posizionando la formula in `A1`, Excel “spilla” un blocco 4 × 5 a partire da quella cella. Da C#, non dobbiamo copiare manualmente i valori – la libreria si occuperà del lavoro pesante quando chiamiamo `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Come usare lambda:** Non ancora, ma resta in attesa. Prima dobbiamo avere i dati nel foglio, poi li ridurremo con una lambda.

---

## Passo 3: Usare LAMBDA dentro REDUCE – Il nocciolo di “Come usare Lambda”

Excel 365 ha introdotto `REDUCE`, che accetta un **valore iniziale**, un **intervallo** e una **LAMBDA** che indica come combinare ogni elemento. Da C# assegniamo semplicemente la stringa della formula; la lambda vive all'interno della formula di Excel, non nel codice C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Spiegazione:**  
- `0` è l'accumulatore iniziale (`acc`).  
- `A1:D4` è l'intervallo che vogliamo elaborare (le prime quattro colonne dello spill).  
- `LAMBDA(acc, x, acc + x)` dice a Excel di aggiungere ogni cella (`x`) all'accumulatore.  

Questa è l'essenza di **come usare lambda** per l'aggregazione in un contesto di foglio di calcolo.

---

## Passo 4: Calcolare la cotangente in Excel – Da gradi a iperbolico

Se ti servono risultati trigonometrici, le funzioni `COT` e `COTH` di Excel sono un gioco da ragazzi. Le inseriremo rispettivamente in `G1` e `G2`.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Perché è utile:** Conoscere **come calcolare la cotangente in Excel** può farti risparmiare la scrittura di codice matematico personalizzato, soprattutto quando il workbook verrà condiviso con persone non sviluppatrici.

---

## Passo 5: Forzare il calcolo e recuperare l'array espanso

Ora chiediamo al workbook di valutare tutte le formule, quindi estraiamo l'array spillato da `A1`. È qui che **visualizziamo l'array nella console**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Ciò che vedrai:**  
- Una matrice 4 × 5 formattata correttamente, stampata riga per riga.  
- La somma calcolata dalla lambda `REDUCE`.  
- I due valori di cotangente.

Questo completa il flusso da **scrivere formula in una cella** fino a **visualizzare l'array nella console**.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l'intero programma che puoi inserire in un'app console. Ricorda di aggiungere prima il pacchetto NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Output console previsto (i valori variano in base al contenuto predefinito di B1:C2, che di default è 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Sentiti libero di popolare `B1:C2` con i tuoi numeri prima di eseguire – la matrice rifletterà quei valori.

---

## Pro Tips & Errori comuni

- **Consiglio:** Se vuoi che l'intervallo spill inizi altrove, cambia semplicemente la cella di destinazione (`A1`). La funzione `EXPAND` rispetta l'ancora.
- **Attenzione a:** Le celle vuote nell'intervallo di origine diventano `0` nell'array spillato, il che può influenzare la somma della `REDUCE`.
- **Caso limite:** Quando il workbook contiene formule che dipendono da funzioni volatili (es. `NOW()`), chiama `workbook.Calculate()` dopo aver impostato tutte le formule per assicurarti che tutto sia aggiornato.
- **Nota sulle prestazioni:** Per spill di grandi dimensioni, considera di limitare la dimensione nella chiamata `EXPAND`; altrimenti potresti allocare più memoria del necessario.
- **Compatibilità:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}