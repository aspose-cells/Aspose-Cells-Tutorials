---
category: general
date: 2026-03-21
description: Come esportare i dati di Excel con i nomi delle colonne, preservare il
  formato numerico e leggere righe specifiche usando Aspose.Cells in C#. Impara a
  leggere il foglio di lavoro Excel ed esportare le righe specifiche in modo efficiente.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: it
og_description: Come esportare i dati Excel con i nomi delle colonne, preservare il
  formato numerico e leggere righe specifiche usando Aspose.Cells. Un esempio completo
  e eseguibile per gli sviluppatori C#.
og_title: Come esportare dati Excel in C# – Guida completa alla programmazione
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Come esportare i dati di Excel in C# – Guida passo‑passo
url: /it/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare dati Excel in C# – Guida completa di programmazione

Ti sei mai chiesto **come esportare excel** senza perdere la formattazione originale? Forse hai provato un rapido copia‑incolla e ti sei ritrovato con date visualizzate come “44728” o intestazioni di colonna mancanti. È frustrante, vero? In questo tutorial vedrai un metodo pulito, end‑to‑end, per leggere un foglio Excel, preservare il formato numerico, esportare con i nomi delle colonne e persino selezionare solo le righe di cui hai bisogno.

Useremo la libreria Aspose.Cells perché offre un controllo granulare sulle opzioni di esportazione. Alla fine di questa guida avrai uno snippet riutilizzabile da inserire in qualsiasi progetto .NET, e comprenderai perché ogni opzione è importante. Nessuna documentazione esterna necessaria—tutto ciò che ti serve è qui.

---

## Cosa imparerai

- **Leggere un foglio Excel** in memoria con Aspose.Cells.  
- **Esportare righe specifiche** (ad es. righe 0‑49) mantenendo i nomi delle colonne.  
- **Preservare il formato numerico** così che valute, date e percentuali rimangano intatte.  
- Come **esportare con i nomi delle colonne** e includere i commenti delle celle, se ti servono.  
- Un esempio completo, pronto‑all‑uso in C#, più consigli per le difficoltà più comuni.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+).  
- Aspose.Cells per .NET installato via NuGet (`Install-Package Aspose.Cells`).  
- Un file Excel (`input.xlsx`) posizionato in una cartella a cui puoi fare riferimento.

> **Consiglio professionale:** se lavori su una pipeline CI, considera di prelevare il pacchetto NuGet da un feed privato per evitare sorprese di licenza.

---

## Passo 1 – Installa Aspose.Cells e aggiungi i namespace

Per prima cosa, assicurati che il pacchetto Aspose.Cells sia nel tuo progetto. Apri la Console di Gestione Pacchetti e esegui:

```powershell
Install-Package Aspose.Cells
```

Quindi aggiungi le direttive `using` necessarie nella parte superiore del tuo file C#:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Queste importazioni ti danno accesso a `Workbook`, `Worksheet`, `ExportTableOptions` e `DataTable`—i componenti fondamentali per **leggere un foglio Excel** ed esportare i dati.

---

## Passo 2 – Carica la cartella di lavoro (Leggi il file Excel)

Ora leggiamo effettivamente **il foglio Excel**. Il costruttore `Workbook` accetta il percorso del file, e Aspose.Cells gestirà sia i formati `.xlsx` sia i più vecchi `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Perché è importante:** caricare la cartella di lavoro una sola volta e riutilizzare lo stesso oggetto `Worksheet` è molto più efficiente rispetto all’aprire il file più volte, soprattutto per fogli di grandi dimensioni.

---

## Passo 3 – Configura le opzioni di esportazione (Preserva formato numerico e nomi colonne)

Qui diciamo ad Aspose.Cells *come* esportare. La classe `ExportTableOptions` permette di affinare l’output. Attiveremo tre flag:

1. `ExportAsString = true` – forza ogni cella a diventare una stringa, garantendo che i numeri mantengano la loro rappresentazione visiva.  
2. `IncludeCellComments = true` – copia eventuali commenti associati alle celle (utile per la documentazione).  
3. `PreserveNumberFormat = true` – conserva il formato numerico originale (simboli di valuta, pattern di data, ecc.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Caso limite:** se imposti `ExportAsString` a `false` ma vuoi comunque mantenere i formati numerici, potresti ottenere valori numerici grezzi (ad es. 44728 per una data). Tenere entrambi i flag attivi evita questa sorpresa.

---

## Passo 4 – Recupera il primo foglio di lavoro (Leggi foglio Excel)

La maggior parte dei file semplici ha i dati di cui hai bisogno nel primo foglio, quindi lo otterremo per indice. Se ti serve un foglio diverso, sostituisci `0` con l’indice corretto (zero‑based) o usa `workbook.Worksheets["NomeFoglio"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Perché è utile:** accedere direttamente all’oggetto worksheet ti dà il pieno controllo sulla sua collezione `Cells`, fondamentale per **esportare righe specifiche** più avanti.

---

## Passo 5 – Esporta un intervallo di celle (Esporta righe specifiche)

Ecco il cuore del tutorial: esportare le righe 0‑49 e le colonne 0‑4 (cioè le prime 50 righe e le prime cinque colonne) in un `DataTable`. Chiederemo anche ad Aspose.Cells di includere i nomi delle colonne come prima riga del `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Cosa fa questo codice

- **`startRow: 0`** – inizia dall’estremità superiore del foglio.  
- **`totalRows: 50`** – prende le prime 50 righe (cioè **esporta righe specifiche**).  
- **`totalColumns: 5`** – limita l’esportazione alle prime cinque colonne.  
- **`includeColumnNames: true`** – assicura che le intestazioni del `DataTable` corrispondano alla riga di intestazione di Excel, soddisfacendo il requisito **esporta con nomi colonne**.  
- **`exportOptions`** – applica le impostazioni del Passo 3, così i valori numerici rimangono visualizzati come “$1,234.56” anziché “1234.56”.

---

## Passo 6 – Verifica l’esportazione (Come appare il risultato)

Stampiamo le prime righe nella console così puoi vedere che la formattazione è stata mantenuta.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Output previsto (esempio):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Nota come le date compaiano nel formato `MM/dd/yyyy` e la valuta mantenga il simbolo `$`—grazie a **preserve number format**.

---

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| Le date diventano numeri grandi | `ExportAsString` lasciato a `false` | Mantieni `ExportAsString = true` o converti manualmente le celle |
| Mancano le intestazioni di colonna | `includeColumnNames` impostato a `false` | Impostalo a `true` quando ti serve **esporta con nomi colonne** |
| I commenti scompaiono | `IncludeCellComments` non abilitato | Attiva `IncludeCellComments` in `ExportTableOptions` |
| Viene esportato il foglio sbagliato | Uso di `Worksheets[0]` su file con più fogli | Specifica il nome del foglio: `workbook.Worksheets["Data"]` |
| Eccezione out‑of‑range | `totalRows` supera le righe effettive | Usa `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Esportare l’intero foglio mantenendo i formati

Se in seguito decidi di aver bisogno dell’intero foglio, sostituisci semplicemente `totalRows` e `totalColumns` con le dimensioni massime del foglio:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Ora hai una routine **read excel worksheet** che funziona per qualsiasi dimensione, preservando comunque **number format** e **exporting with column names**.

---

## Esempio completo (pronto da copiare‑incollare)

Di seguito trovi il programma completo che puoi inserire in un’app console. Include tutti i passaggi, le importazioni e una semplice stampa di verifica.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Salva questo file come `Program.cs`, esegui `dotnet run` e dovresti vedere l’anteprima formattata nel terminale.

---

## Conclusione

Abbiamo appena percorso **come esportare excel** dati usando Aspose.Cells, coprendo tutto, dal caricamento della cartella di lavoro alla preservazione del formato numerico, all’esportazione con i nomi delle colonne e al limitare l’esportazione a righe specifiche. Il codice è autonomo, completamente eseguibile, e include salvaguardie pratiche per i casi limite più comuni.

Pronto per la prossima sfida? Prova a esportare direttamente in CSV mantenendo la formattazione originale, oppure inserisci il `DataTable` in un contesto Entity Framework Core per inserimenti massivi nel database. Entrambi gli scenari si basano sugli stessi fondamenti trattati qui.

Se ti è stato utile

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}