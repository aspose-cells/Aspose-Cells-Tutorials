---
category: general
date: 2026-07-03
description: Scopri come esportare una tabella Excel in un file .txt e salvare una
  tabella Excel in un file .txt usando C#. Esporta i dati di Excel come testo semplice
  con un esempio di codice completo.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: it
og_description: Come esportare una tabella Excel come testo semplice. Questa guida
  ti mostra come esportare i dati di Excel come testo semplice e salvare la tabella
  Excel in un file .txt con Aspose.Cells.
og_title: Come esportare una tabella Excel – Tutorial completo C#
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Come esportare una tabella Excel – Guida completa passo passo
url: /it/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare una tabella Excel – Guida completa passo‑passo

Ti sei mai chiesto **come esportare una tabella Excel** senza caricare l’intero workbook in memoria? Non sei l’unico. In molti lavori di automazione il sistema a valle accetta solo un semplice file `.txt`, quindi devi **salvare la tabella Excel in un file .txt** in modo rapido e affidabile.  

In questo tutorial vedremo una soluzione pulita in C# che **esporta i dati Excel come testo semplice** usando Aspose.Cells. Alla fine avrai un programma pronto da eseguire, comprenderai perché ogni riga è importante e vedrai come personalizzare l’esportazione per i tuoi casi particolari.

## Di cosa avrai bisogno

- **Aspose.Cells for .NET** (qualsiasi versione recente, ad es. 23.12).  
- .NET 6 SDK o successivo – il codice compila anche con .NET Core.  
- Un file di esempio `input.xlsx` che contenga almeno una tabella Excel.  
- Un editor di testo o IDE (Visual Studio, VS Code, Rider… a tua scelta).

Non sono necessari altri pacchetti NuGet oltre ad Aspose.Cells, e il tutto funziona su Windows, Linux o macOS.

## Passo 1: Configura il progetto e gli import

Per prima cosa, crea un’app console e importa gli spazi dei nomi necessari.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Suggerimento:** Se usi la CLI di .NET, esegui `dotnet new console -n ExcelTableExport` e poi `dotnet add package Aspose.Cells` prima di incollare il codice sopra.

## Passo 2: Carica il workbook e prendi il primo foglio di lavoro

L’oggetto workbook rappresenta l’intero file Excel. Caricarlo una sola volta mantiene basso l’utilizzo di memoria.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Perché scegliamo il primo foglio? In molti report generati i dati si trovano nel primo foglio, ma puoi cambiare l’indice o usare `wb.Worksheets["SheetName"]` per un foglio con nome.

## Passo 3: Recupera la prima tabella definita sul foglio

Le tabelle Excel (ListObjects) forniscono dati strutturati, rendendo l’esportazione prevedibile.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Se il tuo workbook contiene più tabelle, itera semplicemente `ws.Tables` o scegli tramite `tbl.Name`.

## Passo 4: Configura le opzioni di esportazione – Esporta ogni cella come stringa

Aspose.Cells ti permette di controllare il formato di ogni cella durante l’esportazione. Impostare `ExportAsString` garantisce che numeri, date e formule diventino testo semplice.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Aggiungere un’azione di esportazione personalizzata per rimuovere gli spazi bianchi

Spesso i dati di origine contengono spazi iniziali o finali. Rimuoverli rende il file `.txt` finale più pulito.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

La lambda riceve l’oggetto `Cell` e un `TextWriter`. Puoi anche aggiungere logica condizionale qui—ad es., sostituire le virgole con punti e virgola per un output in stile CSV.

## Passo 5: Esporta la tabella a partire dalla cella A1 in un file di testo

Ora scriviamo effettivamente la tabella su disco. Il metodo `ExportTable` scorre la tabella riga per riga, applicando le opzioni appena definite.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Ciò che vedrai:** Ogni riga della tabella Excel diventa una linea in `Table.txt`. Le colonne sono separate, di default, da un carattere di tabulazione (`\t`)—perfetto per il parsing a valle.

### Esempio di output previsto

Supponendo che `input.xlsx` contenga una tabella con tre colonne (`ID`, `Name`, `Score`) e due righe di dati, `Table.txt` apparirà così:

```
1    Alice    85
2    Bob      92
```

Nota che gli spazi sono stati rimossi e tutto è testo semplice—esattamente ciò che richiede **export excel data as plain text**.

## Gestione dei casi limite più comuni

| Situazione | Cosa fare | Perché |
|------------|-----------|--------|
| **La tabella ha celle vuote** | La lambda scrive `cell.StringValue.Trim()` che restituisce una stringa vuota per le celle vuote. | Mantiene l’allineamento delle colonne senza aggiungere caratteri indesiderati. |
| **Hai bisogno di un delimitatore personalizzato** | Sostituisci `writer.Write(cell.StringValue.Trim());` con `writer.Write($"{cell.StringValue.Trim()},");` e rimuovi il delimitatore finale dopo ogni riga. | Alcuni sistemi preferiscono virgole o pipe invece dei tab. |
| **Fogli di lavoro molto grandi ( > 100 k righe )** | Usa `ExportTableOptions` con `ExportAsString = true` e trasmetti il file come mostrato; Aspose.Cells elabora le righe in modalità streaming, evitando errori OOM. | Garantisce scalabilità. |
| **Più tabelle in un unico foglio** | Cicla su `ws.Tables` e chiama `ExportTable` per ciascuna, aggiungendo opzionalmente una linea separatrice tra le esportazioni. | Ti consente di **save Excel table to .txt file** per ogni tabella. |

## Esempio completo funzionante

Di seguito trovi il programma completo da copiare‑incollare in `Program.cs`. Sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo che esista sulla tua macchina.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Esegui il programma con `dotnet run`. Se tutto è configurato correttamente, vedrai il messaggio di conferma e un nuovo file `Table.txt` contenente **export excel data as plain text**.

## Bonus: Conferma visiva (opzionale)

Se ti piace vedere rapidamente uno screenshot del file risultante, aprilo con qualsiasi editor di testo. Qui sotto trovi un’immagine segnaposto che mostra il layout previsto.

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Testo alternativo:* **how to export excel table** – mostra l’output in testo semplice di una tabella Excel esportata.

## Riepilogo e prossimi passi

Abbiamo coperto tutto ciò che devi sapere **how to export Excel table** usando Aspose.Cells, dal caricamento del workbook al trimming dei valori delle celle fino alla scrittura di un file `.txt` pulito.  

- Ora sai **save Excel table to .txt file** con logica personalizzata.  
- Puoi adattare la lambda per gestire date, numeri o delimitatori personalizzati.  
- Per progetti più grandi, considera di incapsulare la logica in un metodo o classe riutilizzabile.

**Cosa fare dopo?** Prova a esportare più tabelle, o cambia il formato di output in CSV modificando il delimitatore. Potresti anche esplorare **export excel data as plain text** direttamente su uno stream di rete per integrazioni in tempo reale.

Hai domande o incontri un problema? Lascia un commento, e buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare altre funzionalità dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}