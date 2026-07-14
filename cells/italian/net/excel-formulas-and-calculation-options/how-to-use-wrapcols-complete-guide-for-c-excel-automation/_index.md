---
category: general
date: 2026-07-13
description: Come usare WRAPCOLS in C# per convertire un array in colonne, applicare
  una formula matriciale in Excel e creare un workbook Excel programmaticamente—tutto
  con passaggi chiari.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: it
lastmod: 2026-07-13
og_description: Come usare WRAPCOLS in C# ti consente di convertire rapidamente un
  array in colonne, applicare una formula matriciale in stile Excel e valutare il
  risultato programmaticamente.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Come usare WRAPCOLS in C# – Creazione rapida di cartelle di lavoro Excel
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Come utilizzare WRAPCOLS – Guida completa per l'automazione Excel con C#
url: /it/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare WRAPCOLS – Guida completa per l'automazione Excel con C#

Ti sei mai chiesto **come usare WRAPCOLS** quando devi trasformare un elenco piatto in una tabella ordinata all'interno di un file Excel generato da C#? Non sei il solo. Che tu stia costruendo un motore di reporting, esportando i risultati di un sondaggio o semplicemente giocando con i dati, la funzione WRAPCOLS può rimodellare istantaneamente un array nel numero di colonne che specifichi.  

In questo tutorial percorreremo l'intero processo: dalla **creazione programmatica di una cartella di lavoro Excel** all'**applicazione di una formula array in stile Excel**, e infine **valutare la formula con C#**. Alla fine sarai in grado di **convertire un array in colonne** con una singola riga di codice, senza dover fare gymnastics cella‑per‑cella manuali.

> **Cosa otterrai:** un esempio di codice eseguibile, spiegazione di ogni passaggio, consigli per le insidie più comuni e suggerimenti per estendere la soluzione.

---

## Prerequisiti

Prima di immergerci, assicurati di avere:

- .NET 6.0+ (o qualsiasi runtime .NET recente)
- Un IDE C# (Visual Studio, Rider o VS Code)
- La libreria **Aspose.Cells for .NET** (la versione di prova gratuita va benissimo) – è il modo più semplice per manipolare file Excel senza dover installare Excel.
- Familiarità di base con la sintassi C# e le formule Excel.

Se preferisci un'altra libreria (ad es., EPPlus o ClosedXML), i concetti fondamentali rimangono gli stessi—basta sostituire le chiamate API.

---

## Step 1: Configura il progetto e aggiungi la libreria Excel

Prima di tutto, crea una nuova console app e aggiungi Aspose.Cells tramite NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Suggerimento professionale:** Usa il flag `--version` per bloccare a una versione stabile nota, ad esempio `Aspose.Cells 24.9`.

Ora apri `Program.cs`. Inizieremo aggiungendo gli spazi dei nomi richiesti:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Avere la libreria referenziata garantisce che possiamo **create excel workbook programmatically** e lavorare con le formule.

---

## Step 2: Crea una nuova cartella di lavoro e la cella di destinazione

Successivamente, istanzia una cartella di lavoro fresca e scegli la cella dove vivrà la formula WRAPCOLS. In termini di Excel, la cella **A1** corrisponde a riga 0, colonna 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Perché lo facciamo? L'oggetto `Workbook` è il contenitore di tutti i fogli, gli stili e i calcoli. Riferendo esplicitamente la cella, manteniamo il codice chiaro ed evitiamo “numeri magici” in seguito.

---

## Step 3: Inserisci la formula array WRAPCOLS

Ora arriva il cuore del tutorial—**come usare WRAPCOLS**. La funzione prende un array e un conteggio di colonne, poi restituisce un intervallo bidimensionale. In sintassi Excel appare così:

```
=WRAPCOLS({1,2,3,4}, 2)
```

Questo indica a Excel di disporre i numeri 1‑4 in **2 colonne**, ottenendo:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Per incorporare quella formula da C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Nota che stiamo usando una **stringa** che rispecchia ciò che digiteresti nella barra della formula di Excel. Questo è il passaggio **apply array formula excel**, e Aspose.Cells la tratta automaticamente come formula array perché WRAPCOLS restituisce un intervallo.

---

## Step 4: Forza il calcolo affinché la formula venga valutata

Excel normalmente ricalcola in modo pigro—solo quando apri il file. Poiché vogliamo leggere il risultato immediatamente, dobbiamo attivare un calcolo:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Chiamare `Calculate()` è l'azione **evaluate excel formula c#** che costringe il motore a calcolare ogni formula, inclusa la nostra array WRAPCOLS. Senza questa chiamata, `targetCell.Value` sarebbe ancora `null`.

---

## Step 5: Recupera e verifica il risultato

Ora che la cartella di lavoro è stata calcolata, possiamo estrarre il(i) valore(i) dalle celle occupate dall'array. La cella in alto a sinistra (A1) contiene il primo elemento, mentre le celle adiacenti contengono il resto. Leggiamo l'intero blocco 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

Quando esegui il programma, la console dovrebbe mostrare:

```
1   3
2   4
```

Quell'output conferma che abbiamo **convertito con successo un array in colonne** usando WRAPCOLS.

---

## Step 6: Salva la cartella di lavoro (opzionale ma utile)

Se desideri aprire il file in Excel e vedere la formula in tempo reale, basta salvarlo:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Aprendo il file vedrai la formula WRAPCOLS in A1 e l'intervallo a 2 colonne popolato sotto di essa. Questo passaggio è utile per il debug o per consegnare il file agli utenti finali.

---

## Domande comuni & casi limite

### E se ho bisogno di più di due colonne?

Basta cambiare il secondo argomento di WRAPCOLS. Per esempio, `=WRAPCOLS({1,2,3,4,5,6},3)` produrrebbe tre colonne:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Aggiorna la riga C# di conseguenza:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Posso fornire un intervallo dinamico invece di un array hard‑coded?

Assolutamente. Puoi costruire la stringa dell'array programmaticamente:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

In questo modo **apply array formula excel** avviene al volo, perfetto per report con dimensioni di dati variabili.

### Come gestire gli errori?

Se la formula è malformata, `Calculate()` lancerà una `CellsException`. Avvolgi il calcolo in un blocco try/catch e registra l'errore:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Funziona con versioni più vecchie di Excel?

WRAPCOLS è stata introdotta in Excel 365/2021. Quando salvi il file in un formato `.xls` più vecchio, la formula potrebbe andare persa. Usa `.xlsx` se hai bisogno che la funzione sopravviva al di fuori del motore C#.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo, pronto per il copia‑incolla:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Esegui `dotnet run` e dovresti vedere la matrice stampata, seguita da una conferma che il file `.xlsx` esiste.

---

## Riepilogo & prossimi passi

Abbiamo coperto **come usare WRAPCOLS** per **convertire un array in colonne**, dimostrato la tecnica **apply array formula excel** da C#, forzato un calcolo per **evaluate excel formula c#**, e salvato il risultato per l'uso successivo.  

Se vuoi approfondire:

- **Conteggi di colonne dinamici:** lascia che il numero di colonne sia una variabile inserita dall'utente.
- **Stilizzare l'output:** applica font, bordi o formattazione condizionale tramite Aspose.Cells dopo il calcolo.
- **Combinare con altre funzioni:** annida WRAPCOLS dentro `LET` o `FILTER`.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aspose.Cells .NET: Come creare e formattare cartelle di lavoro Excel programmaticamente](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [Come creare e salvare una cartella di lavoro Excel come ODS usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Come creare intervalli denominati a livello di cartella di lavoro in Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}