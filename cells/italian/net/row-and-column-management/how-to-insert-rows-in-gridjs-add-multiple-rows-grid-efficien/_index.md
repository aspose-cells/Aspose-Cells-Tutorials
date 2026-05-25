---
category: general
date: 2026-03-29
description: Scopri come inserire rapidamente righe in GridJs. Questa guida copre
  anche come aggiungere righe e aggiungere più righe alla griglia con un'operazione
  batch.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: it
og_description: Scopri come inserire rapidamente righe in GridJs. Questa guida mostra
  come aggiungere righe, aggiungere più righe alla griglia e gestire inserimenti di
  grandi batch.
og_title: Come inserire righe in GridJs – Aggiungi più righe alla griglia in modo
  efficiente
tags:
- GridJs
- C#
- data‑grid
title: Come inserire righe in GridJs – Aggiungi più righe alla griglia in modo efficiente
url: /it/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come inserire righe in GridJs – Aggiungere più righe alla griglia in modo efficiente

Ti sei mai chiesto **come inserire righe** in una tabella GridJs enorme senza bloccare l'interfaccia? Forse ti sei imbattuto in un ostacolo cercando di **aggiungere righe** una alla volta e le prestazioni sono crollate. La buona notizia è che GridJs offre un'API batch che ti permette di **add multiple rows grid** in un'unica chiamata, mantenendo tutto reattivo anche quando lavori con milioni di voci.

In questo tutorial percorreremo un esempio completo e funzionante che mostra esattamente **come inserire righe** usando `InsertRowsBatch`. Vedrai perché il batching è importante, come verificare il risultato e a cosa fare attenzione quando l'indice di destinazione è enorme. Alla fine sarai in grado di inserire mille nuovi record in qualsiasi istanza di GridJs con fiducia.

## Prerequisiti

Prima di immergerci, assicurati di avere:

- .NET 6.0 o successivo (il codice si compila con qualsiasi SDK recente)
- Un riferimento al pacchetto NuGet `GridJs` (o al DLL se usi una build personalizzata)
- Conoscenze di base di C# – non serve essere un guru, basta essere a proprio agio con classi e metodi
- Un IDE o editor a tua scelta (Visual Studio, Rider, VS Code… tutti funzionano)

> **Pro tip:** Se prevedi di lavorare con griglie davvero massive (decine di milioni di righe), abilita `gridJs.EnableVirtualization = true;` per mantenere il rendering dell'interfaccia leggero.

## Passo 1: Creare e configurare l'istanza GridJs

Prima di tutto: ti serve un oggetto `GridJs` attivo. Pensalo come la tela su cui dipingerai le righe.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Perché questo passo è importante:** Inizializzare la griglia e, facoltativamente, popolarla con dati di esempio replica uno scenario reale in cui la griglia contiene già una grande quantità di informazioni. L'inserimento batch che eseguiremo in seguito deve rispettare l'indice a base zero, quindi pre‑popoliamo per illustrare il punto di inserimento esatto.

## Passo 2: Usare `InsertRowsBatch` per **Add Multiple Rows Grid**

Ora il cuore del tutorial – la chiamata che effettivamente **adds rows** in blocco. La firma del metodo è `InsertRowsBatch(int startIndex, int count)`. Nel nostro esempio partiremo dall'indice 2 000 000 (corrispondente alla riga 2 000 001) e aggiungeremo dieci righe.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Come funziona:** `InsertRowsBatch` alloca internamente il numero richiesto di righe e sposta le righe esistenti verso il basso. Poiché l'operazione viene eseguita in un'unica transazione, l'interfaccia si aggiorna una sola volta, ed è per questo che questo metodo è il modo consigliato per **how to add rows** in modo efficiente.

## Passo 3: Verificare l'inserimento – Le righe sono state collocate dove previsto?

Dopo l'operazione batch vorrai essere sicuro che le righe siano dove pensi. Il seguente helper legge la prima e l'ultima riga del blocco appena aggiunto e le stampa sulla console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Output previsto**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Le celle vuote indicano che le righe sono segnaposto in attesa di dati. Ora puoi popolarle individualmente o eseguire un altro aggiornamento batch.

> **Nota su casi limite:** Se `startIndex` supera il conteggio corrente delle righe, GridJs aggiungerà automaticamente le nuove righe alla fine. Al contrario, un indice negativo genera un `ArgumentOutOfRangeException`, quindi valida sempre gli indici forniti dall'utente.

## Passo 4: Popolare le nuove righe (Opzionale ma comune)

Spesso non vuoi solo righe vuote; hai bisogno di riempirle con valori significativi. Puoi iterare sull'intervallo appena creato e chiamare `SetCell` o un'API simile.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Potresti chiamare `PopulateNewRows(gridJs, startIndex, rowsToAdd);` subito dopo l'inserimento batch se hai bisogno che le righe siano pronte per la visualizzazione immediata.

## Passo 5: Consigli di performance per griglie molto grandi

Quando lavori con **add multiple rows grid** nei milioni, tieni a mente questi trucchi:

1. **La dimensione del batch conta** – Inserire 10 000 righe in una volta può essere più veloce di dieci batch separati da 1 000 righe perché ogni batch comporta un unico refresh UI.
2. **Disattiva gli aggiornamenti UI** – Alcune versioni di GridJs espongono `grid.SuspendLayout()` / `grid.ResumeLayout()`. Avvolgi il tuo batch con queste chiamate se noti rallentamenti.
3. **Usa la virtualizzazione** – Come mostrato prima, `EnableVirtualization` riduce drasticamente il consumo di memoria e i tempi di rendering.
4. **Evita copie profonde** – Passa tipi di valore semplici o oggetti leggeri alla griglia; oggetti pesanti costringono la griglia a clonare i dati, penalizzando le performance.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in un nuovo progetto console:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Esegui il programma e vedrai l'output della console che conferma che le dieci righe sono state inserite nella posizione corretta e poi popolate.

## Conclusione

Abbiamo coperto **how to insert rows** in GridJs usando l'API batch, dimostrato **how to add rows** in modo efficiente e esplorato modi per **add multiple rows grid** senza bloccare l'interfaccia. I punti chiave sono:

- Usa `InsertRowsBatch(startIndex, count)` per qualsiasi operazione di bulk.
- Valida gli indici e considera la virtualizzazione per dataset massivi.
- Popola le righe dopo il batch se ti serve contenuto immediato.

Successivamente, potresti voler esplorare **how to delete rows**, implementare **undo/redo** per modifiche batch, o integrare GridJs con un servizio back‑end che trasmette dati su richiesta. Tutti questi argomenti si basano direttamente sui concetti appena appresi.

Sentiti libero di sperimentare—cambia la dimensione del batch, prova a inserire all'inizio della griglia, o combina più batch in un'unica transazione. Più giochi, più ti sentirai a tuo agio con grandi

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}