---
category: general
date: 2026-06-27
description: come utilizzare wrapcols e wrap rows excel in C#. Impara a creare un
  workbook Excel in C# e a ricalcolare le formule Excel con un esempio passo‑passo.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: it
og_description: come usare wrapcols e wrap rows in Excel con C#. Questa guida mostra
  come creare un workbook Excel in C# e ricalcolare le formule di Excel in pochi minuti.
og_title: come usare wrapcols in C# – Tutorial completo sull’avvolgimento in Excel
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Come usare wrapcols in C# – Guida completa con Excel WRAPROWS e ricalcolare
  le formule
url: /it/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come usare wrapcols in C# – Guida completa con Excel WRAPROWS e ricalcolo delle formule

Ti sei mai chiesto **come usare wrapcols** quando devi rimodellare un elenco lungo in una griglia ordinata? Forse hai provato il trucco manuale copia‑incolla, ma è lento, soggetto a errori e, francamente, una seccatura. La buona notizia? `WRAPCOLS` di Excel (e il suo fratello `WRAPROWS`) può fare il lavoro pesante per te—*e* puoi controllarli dal codice C#.

In questo tutorial vedremo come creare una cartella di lavoro Excel in C#, applicare `WRAPCOLS` e `WRAPROWS`, e infine **ricalcolare le formule di Excel** affinché i dati avvolti vengano visualizzati immediatamente. Alla fine avrai uno snippet pronto all'uso da inserire in qualsiasi progetto .NET.

## Cosa imparerai

- Come **creare excel workbook c#** usando la libreria Aspose.Cells (senza necessità di interop COM).  
- La sintassi esatta per la funzione `WRAPCOLS` e come differisce da `WRAPROWS`.  
- Perché è necessario **ricalcolare le formule di Excel** dopo aver inserito le funzioni, e come farlo in modo efficiente.  
- Un esempio completo e eseguibile che puoi copiare‑incollare e vedere il risultato in un file `.xlsx`.  

**Prerequisiti** – Hai bisogno di .NET 6+ (o .NET Framework 4.7+), Visual Studio 2022 o qualsiasi IDE preferisci, e del pacchetto NuGet Aspose.Cells per .NET. Se sei nuovo a Aspose.Cells, non preoccuparti; i passaggi sono semplici e spiegati completamente.

---

## Passo 1: Configura il progetto e installa Aspose.Cells

Per iniziare, crea un nuovo progetto console:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Suggerimento:** Se usi Visual Studio, fai clic destro sul progetto → *Gestisci pacchetti NuGet* → cerca **Aspose.Cells** e installalo.

La libreria ci fornisce le classi `Workbook`, `Worksheet` e `Cell` di cui avremo bisogno per il resto del tutorial.

## Passo 2: Crea una cartella di lavoro Excel e popola i dati di esempio

Ora avvieremo una cartella di lavoro, otterremo il primo foglio di lavoro e riempiremo le colonne **A** e **B** con numeri di esempio. Questi dati saranno successivamente avvolti in colonne e righe.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Perché è importante:** Avere dati deterministici ti permette di verificare che `WRAPCOLS` e `WRAPROWS` facciano esattamente ciò che ti aspetti.

## Passo 3: Applica la funzione `WRAPCOLS` – **come usare wrapcols**

`WRAPCOLS` prende un intervallo unidimensionale e lo distribuisce su un numero specificato di colonne, aggiungendo automaticamente nuove righe secondo necessità. Ecco la formula esatta che inseriremo nella cella **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Spiegazione:** Il secondo argomento (`3`) indica a Excel di creare tre colonne per riga. Quindi i primi tre valori (1, 2, 3) finiscono in A1:C1, i successivi tre (4, 5, 6) vanno in A2:C2, e i valori rimanenti riempiono la riga successiva.

## Passo 4: Applica la funzione `WRAPROWS` – wrap rows excel

`WRAPROWS` fa l'opposto: prende un intervallo verticale e lo dispone in un numero impostato di righe per colonna. Inseriremo questa formula in **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Spiegazione:** Con `2` righe per colonna, i valori “A, B” vanno in B1:B2, “C, D” in C1:C2, e così via. La funzione espande automaticamente il foglio in orizzontale.

## Passo 5: Ricalcola tutte le formule – **ricalcolare le formule di Excel**

Quando imposti una formula programmaticamente, Excel non calcolerà il risultato finché la cartella di lavoro non viene aperta o finché non istruisci esplicitamente la libreria a valutarla. È qui che entra in gioco **ricalcolare le formule di Excel**:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Perché è necessario:** Senza chiamare `CalculateFormula()`, le celle mostreranno il testo grezzo `=WRAPCOLS(...)` quando apri il file, il che vanifica lo scopo del tutorial.

## Passo 6: Salva la cartella di lavoro e verifica l'output

Infine, scrivi la cartella di lavoro su disco. Puoi aprire il file risultante in Excel per vedere il layout avvolto.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Risultato atteso

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Le colonne A‑C** sono popolate dalla chiamata `WRAPCOLS` (tre colonne per riga).  
- **Le righe B‑I** sono popolate dalla chiamata `WRAPROWS` (due righe per colonna).  

Apri `output.xlsx` e vedrai il layout esatto mostrato sopra. Se i numeri non corrispondono, ricontrolla le stringhe delle formule e assicurati che sia stato chiamato `CalculateFormula()`.

---

## Domande comuni e casi limite

### Cosa succede se l'intervallo di origine è vuoto?
Sia `WRAPCOLS` che `WRAPROWS` restituiranno semplicemente un array vuoto, risultando in una cella vuota. È sicuro chiamare le funzioni anche quando non sei sicuro della presenza dei dati.

### Posso avvolgere più di un intervallo alla volta?
Sì—basta inserire formule aggiuntive in altre celle. Ogni formula funziona in modo indipendente, quindi potresti avere `WRAPCOLS` in D1, `WRAPROWS` in E1, ecc.

### In che modo differisce da una semplice trasposizione copia‑incolla?
`WRAPCOLS`/`WRAPROWS` gestiscono automaticamente la *paginazione*. Se hai 20 elementi e richiedi 3 colonne, la funzione crea il numero necessario di righe (7 in questo caso) senza che tu debba calcolare manualmente le dimensioni.

### La libreria supporta le formule di array dinamici (Excel 365)?
Aspose.Cells supporta pienamente le funzioni di array dinamici, inclusi `WRAPCOLS` e `WRAPROWS`. Il motore di calcolo disperderà i risultati proprio come Excel nativo.

### E per quanto riguarda le prestazioni su grandi set di dati?
Per milioni di righe, considera di eseguire il calcolo in batch (`workbook.CalculateFormula(FormulaCalculationOptions)`) o di disabilitare il calcolo automatico mentre inserisci le formule, per poi riabilitarlo prima di salvare.

---

## Codice sorgente completo (pronto per l'esecuzione)

Di seguito trovi il programma completo—copialo in `Program.cs` e premi **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Conclusione

Ora sai **come usare wrapcols** (e il suo corrispondente `WRAPROWS`) da C# per rimodellare i dati in un foglio Excel, e comprendi perché **ricalcolare le formule di Excel** è un passaggio obbligatorio. Questo schema—*creare excel workbook c# → inserire funzioni WRAP → ricalcolare*—è una solida base per qualsiasi attività di reporting o presentazione dati che richieda layout dinamici di colonne o righe.

Cosa fare dopo? Prova a sperimentare con:

- Diversi conteggi di colonne/righe (`WRAPCOLS(..., 5)` o `WRAPROWS(..., 4)`).  
- Combinare `WRAPCOLS` con altre funzioni di array dinamici come `FILTER` o `SORT`.  
- Esportare la cartella di lavoro in PDF con `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Sentiti libero di modificare il campione, aggiungere formattazione o integrarlo in una pipeline di automazione più ampia. Se incontri problemi, lascia un commento qui sotto—buon coding!

![Diagram showing how wrapcols and wraprows transform a single column into a grid – how to use wrapcols example](wrapcols-wraprows-diagram.png "how to use wrapcols example")

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare Aspose.Cells per .NET per raggruppare righe e colonne in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Come nascondere righe e colonne in Excel usando Aspose.Cells .NET: Guida completa](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [Come creare e configurare cartelle di lavoro Excel con Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}