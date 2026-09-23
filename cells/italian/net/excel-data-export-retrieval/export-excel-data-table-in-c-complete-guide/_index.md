---
category: general
date: 2026-03-21
description: Esporta la tabella dati di Excel in un DataTable con intestazioni, limita
  i decimali e esporta le prime 100 righe usando Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: it
og_description: Scopri come esportare una tabella di dati Excel in un DataTable, mantenere
  le intestazioni, limitare le cifre decimali e prelevare le prime 100 righe in C#.
og_title: Esporta la tabella dei dati Excel in C# – Guida passo passo
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Esporta la tabella dati di Excel in C# – Guida completa
url: /it/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Tabella Dati Excel – Guida Completa C#

Hai bisogno di **esportare una tabella dati excel** da una cartella di lavoro in un .NET `DataTable`? Sei nel posto giusto—questa guida ti mostra esattamente come farlo, mantenere le intestazioni di colonna, limitare i decimali e prelevare solo le prime 100 righe.  

Se ti è mai capitato di fissare un foglio di calcolo e pensare, “Come faccio a portarlo nella mia app senza perdere la formattazione?” non sei solo. Nei prossimi minuti trasformeremo quel “cosa‑se” in una soluzione concreta, copia‑incolla, che funziona con Aspose.Cells, una libreria popolare per la manipolazione di Excel.

## Cosa Imparerai

- Come **esportare excel in datatable** usando il metodo `ExportDataTable`.  
- Come mantenere i nomi originali delle colonne (`export excel with headers`).  
- Come **limitare i decimali excel** configurando `ExportTableOptions`.  
- Come recuperare in modo sicuro solo le prime 100 righe (`export first 100 rows`).  

Nessuno script esterno, nessuna stringa magica—solo C# puro che puoi inserire in qualsiasi progetto .NET.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6 o versioni successive (o .NET Framework 4.7+) | Aspose.Cells supporta entrambi, ma i runtime più recenti ti offrono API pronte per l'async. |
| Pacchetto NuGet Aspose.Cells per .NET | Fornisce `Workbook`, `ExportTableOptions` e l'helper `ExportDataTable`. |
| Un file Excel di esempio (ad es., `Numbers.xlsx`) | La fonte dei dati che esporti. |
| Conoscenza di base di C# | Seguirai gli snippet di codice, ma non è richiesto nulla di complesso. |

Se qualcuno di questi termini ti è sconosciuto, aggiungi il pacchetto NuGet con `dotnet add package Aspose.Cells` e crea un piccolo file Excel con qualche numero—i tuoi dati di test.

![esempio di esportazione tabella dati excel](excel-data-table.png "Screenshot di un foglio Excel che sarà esportato in un DataTable")

## Passo 1: Carica la Cartella di Lavoro (export excel data table)

La prima cosa di cui hai bisogno è un'istanza `Workbook` che punti al tuo file Excel. Pensala come aprire un libro prima di poter leggere i capitoli.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Perché è importante:** Caricare la cartella di lavoro ti dà accesso ai fogli, alle celle e agli stili. Se il percorso del file è errato, Aspose lancerà una `FileNotFoundException`, quindi verifica attentamente la posizione.

## Passo 2: Configura le Opzioni di Esportazione – limit decimal places excel

Per impostazione predefinita Aspose esporta ogni valore numerico con precisione completa. Spesso ti servono solo poche cifre significative, soprattutto quando i dati vengono inviati a una griglia UI o a un'API che si aspetta numeri arrotondati.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Consiglio esperto:** Se ti serve una strategia di arrotondamento diversa (ad es., sempre arrotondare per eccesso), puoi post‑processare il `DataTable` dopo l'esportazione. L'impostazione `SignificantDigits` è il modo più rapido per **limitare i decimali excel** senza scrivere loop aggiuntivi.

## Passo 3: Esporta l'Intervallo Desiderato (export first 100 rows)

Ora diciamo ad Aspose quale blocco di celle vogliamo trasferire in un `DataTable`. In questo tutorial preleviamo le prime 100 righe e le prime 10 colonne, ma puoi regolare questi numeri in base al tuo scenario.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Caso limite:** Se il foglio contiene meno di 100 righe, Aspose esporterà semplicemente ciò che esiste senza generare errori. Tuttavia, potresti voler proteggerti da un intervallo inaspettatamente piccolo:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Passo 4: Verifica il Risultato – Dump Rapido su Console

Vedere i dati nel debugger è utile, ma stampare qualche riga sulla console conferma che l'**export excel to datatable** abbia effettivamente funzionato e che i decimali siano stati ridotti.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Output Atteso

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Nota come le colonne numeriche mostrino ora solo quattro cifre significative, corrispondenti all'impostazione `SignificantDigits = 4` applicata in precedenza.

## Passo 5: Raccogli Tutto – Esempio Completo e Eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in un'app console. Include la gestione degli errori, il controllo opzionale del conteggio delle righe e il metodo di supporto per la stampa.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Esegui il programma e vedrai le prime 100 righe del tuo foglio, arrotondate correttamente, con i nomi delle colonne intatti.

## Domande Frequenti & Trappole

| Domanda | Risposta |
|----------|--------|
| **E se il mio foglio ha celle unite?** | `ExportDataTable` appiattisce le celle unite prendendo il valore della cella in alto a sinistra. Se ti serve una gestione personalizzata, separa prima le unioni o leggi gli oggetti `Cell` grezzi. |
| **Posso esportare in un `DataSet` invece?** | Sì—usa `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}