---
category: general
date: 2026-10-01
description: Impara a eliminare righe da una tabella Excel e a modificare il nome
  della tabella Excel usando C#. Guida passo‑passo con codice completo e migliori
  pratiche.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: it
lastmod: 2026-10-01
og_description: Elimina righe da una tabella Excel e cambia il nome della tabella
  Excel in C#. Segui questo tutorial completo per caricare una cartella di lavoro,
  modificare la tabella e salvare il risultato.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Elimina righe da una tabella Excel e cambia il suo nome in C# – guida completa
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Come eliminare righe da una tabella Excel e cambiarne il nome in C#
url: /it/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eliminare righe da una tabella Excel e cambiarne il nome in C#

Se hai bisogno di **eliminare righe da una tabella Excel** mentre lavori con C#, questa guida mostra i passaggi esatti necessari. Vedrai come **caricare una cartella di lavoro Excel in C#**, rimuovere righe specifiche da una tabella e poi **aggiornare il nome della tabella Excel** affinché il file rimanga coerente.

Il tutorial copre tutto ciò che devi sapere: i pacchetti NuGet richiesti, codice completo eseguibile e le insidie comuni come violazioni della struttura della tabella. Alla fine dell'articolo potrai modificare qualsiasi tabella Excel programmaticamente senza intervento manuale.

## Prerequisiti

* .NET 6.0 SDK o versioni successive installate.
* Visual Studio 2022 (o qualsiasi IDE C#) configurato per lo sviluppo .NET.
* La libreria **Aspose.Cells for .NET** aggiunta tramite NuGet (`Install-Package Aspose.Cells`).
* Un file Excel esistente (`Table.xlsx`) che contiene almeno un foglio di lavoro con una tabella.

Questi elementi forniscono l'ambiente necessario per il codice **load Excel workbook c#** e per eseguire le operazioni in modo affidabile.

## Passo 1: Caricare la cartella di lavoro contenente la tabella

La prima operazione è aprire il file della cartella di lavoro. Aspose.Cells legge l'intera cartella di lavoro in memoria, offrendoti il pieno controllo su fogli, tabelle e dati delle celle.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Perché è importante*: Caricare la cartella di lavoro è la base per qualsiasi successiva manipolazione della tabella. L'oggetto `Workbook` espone la collezione `Worksheets`, che utilizzerai per individuare la tabella di destinazione.

## Passo 2: Accedere al primo foglio di lavoro e alla sua prima tabella

La maggior parte dei file Excel memorizza le tabelle nel primo foglio di lavoro, ma è possibile regolare l'indice se necessario. Il codice seguente recupera il primo oggetto `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Se il foglio di lavoro non contiene una tabella, `sheet.Tables.Count` sarà zero e dovresti gestire questo caso. Tentare di accedere a `sheet.Tables[0]` quando non esistono tabelle genera un'eccezione, motivo per cui è consigliata una clausola di guardia nel codice di produzione.

## Passo 3: Eliminare righe dalla tabella Excel

Per **rimuovere righe da una tabella Excel**, chiama `DeleteRows(startRow, totalRows)`. Il parametro `startRow` è basato su zero rispetto alla prima riga di dati della tabella (la riga dopo l'intestazione).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Perché usare `DeleteRows` invece di eliminare righe del foglio di lavoro?

`DeleteRows` aggiorna l'intervallo interno della tabella, preservando formule, stili e nomi definiti che appartengono alla tabella. Eliminare direttamente le righe del foglio di lavoro potrebbe rompere la struttura della tabella e generare un'eccezione.

**Caso limite**: Se l'eliminazione lasciasse la tabella senza righe di dati, Aspose.Cells genera un `ArgumentException`. Proteggi da ciò controllando `table.RowCount` prima dell'eliminazione.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Passo 4: Cambiare il nome della tabella Excel

Dopo aver rimosso le righe, potresti voler assegnare alla tabella un identificatore più descrittivo. La proprietà `Name` imposta il nome definito della tabella, che è usato nelle formule e in VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Perché rinominare?* Un nome di tabella chiaro migliora la leggibilità nelle formule (`=SUM(SalesData2026[Amount])`) ed evita collisioni di nomi quando più tabelle condividono scopi simili.

## Passo 5: Salvare la cartella di lavoro modificata (opzionale)

Rendi permanenti le modifiche salvando in un nuovo file o sovrascrivendo l'originale. Salvare in una nuova posizione è più sicuro durante lo sviluppo.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

Il metodo `Save` scrive la cartella di lavoro aggiornata, includendo l'intervallo della tabella modificato e il nuovo nome della tabella, su disco.

## Esempio completo funzionante

Unendo tutti i passaggi si ottiene un programma autonomo che puoi eseguire immediatamente.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Output previsto** (supponendo che il file e la tabella esistano):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Eseguendo il programma il file Excel viene aggiornato esattamente come descritto: le righe vengono rimosse, il nome della tabella cambia e il risultato viene salvato senza modifiche manuali.

## Domande comuni e risoluzione dei problemi

| Domanda | Risposta |
|----------|--------|
| *Cosa succede se la tabella copre celle unite?* | `DeleteRows` rispetta gli intervalli uniti. Se una cella unita attraversa il confine dell'eliminazione, Aspose.Cells regola automaticamente l'unione. Verifica il risultato visivamente se ti affidi a unioni complesse. |
| *Posso eliminare righe da una tabella che fa parte di una cache pivot?* | Eliminare righe da una tabella di origine che alimenta una tabella pivot **non** aggiorna automaticamente la cache pivot. Chiama `pivotTable.RefreshData()` dopo aver modificato la tabella di origine. |
| *È possibile eliminare righe in base a una condizione (ad esempio valore < 0)?* | Sì. Itera attraverso `table.ListObjects` o `table.Rows` per individuare le righe corrispondenti, quindi raccogli i loro indici e chiama `DeleteRows` per ciascun intervallo. |
| *Devo rilasciare l'oggetto `Workbook`?* | `Workbook` implementa `IDisposable`. Avvolgilo in un blocco `using` per un rilascio deterministico delle risorse, specialmente quando si elaborano file di grandi dimensioni. |
| *In che cosa differisce dall'uso di EPPlus?* | EPPlus supporta anche la manipolazione delle tabelle ma utilizza un'API diversa (`ExcelTable`). I concetti di caricamento di una cartella di lavoro, eliminazione di righe e rinomina della tabella sono analoghi. Scegli la libreria che corrisponde ai tuoi requisiti di licenza. |

## Best practice quando si modificano tabelle Excel in C#

* **Convalidare gli indici** – Gli indici delle righe della tabella sono basati su zero; errori di off‑by‑one causano eliminazioni inaspettate.
* **Verificare le collisioni di nome** – Excel non consente nomi definiti duplicati; verifica sempre l'unicità prima di assegnare un nuovo nome.
* **Eseguire il backup dei file originali** – Gli script automatizzati possono corrompere i dati; conserva una copia della cartella di lavoro di origine.
* **Usare le istruzioni `using`** – Garantisce che i handle dei file vengano rilasciati prontamente:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Testare con casi limite** – Tabelle con una sola riga di dati, tabelle che coprono l'intero foglio di lavoro e tabelle collegate a grafici dovrebbero essere verificate dopo le modifiche.

## Conclusione

Ora sai come **eliminare righe da una tabella Excel** e **cambiare il nome della tabella Excel** usando C#. La soluzione completa carica la cartella di lavoro, accede alla tabella di destinazione, rimuove le righe desiderate, rinomina la tabella e salva il risultato. Applica queste tecniche per automatizzare la generazione di report, la pulizia dei dati o qualsiasi flusso di lavoro che richieda la gestione programmatica delle tabelle Excel.

Successivamente, esplora argomenti correlati come **aggiornare i valori delle celle in una tabella Excel**, **aggiungere nuove righe programmaticamente** e **esportare i dati della tabella in CSV**. Padroneggiare queste operazioni ti darà il pieno controllo sui file Excel dall'interno delle tue applicazioni C#.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come rinominare una tabella in Excel con C# – Guida passo‑passo](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Creare una tabella Excel in C# – Guida passo‑passo](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Ottenere la prima tabella da una cartella di lavoro Excel in C# – Guida completa](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}