---
category: general
date: 2026-10-10
description: Scopri come eliminare un'intera riga in una cartella di lavoro Excel
  con C#. Questa guida passo‑passo copre anche come eliminare una riga per indice
  e rimuovere una riga per indice utilizzando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: it
lastmod: 2026-10-10
og_description: Elimina l'intera riga in una cartella di lavoro Excel usando C#. Segui
  questa guida per imparare come eliminare una riga per indice, rimuovere una riga
  per indice e salvare il file in modo sicuro.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Elimina l'intera riga in Excel con C# – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Come eliminare un'intera riga in un file Excel usando C#
url: /it/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Elimina un'intera riga in un file Excel usando C#

Se hai bisogno di **eliminare un'intera riga** in una cartella di lavoro Excel, questa guida ti mostra esattamente come farlo con C#. Che tu stia pulendo dati importati o creando uno strumento di reporting, i passaggi seguenti ti consentono di rimuovere una riga per indice e salvare il risultato senza perdere altri dati.

Vedrai anche come lo stesso approccio risponde alla domanda **how to delete row** per indice, come **remove row by index**, e perché funziona per gli scenari **delete row excel** in C#.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.6+)  
* La libreria **Aspose.Cells for .NET** (disponibile tramite NuGet: `Install-Package Aspose.Cells`)  
* Familiarità di base con progetti console o desktop C#  

Non sono necessari componenti aggiuntivi di interop Excel o COM, il che mantiene la soluzione leggera e sicura per l'esecuzione lato server.

## Passo 1: Configura il progetto e importa gli spazi dei nomi

Crea una nuova applicazione console (o aggiungi il codice a un progetto esistente) e aggiungi le direttive `using` richieste:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Perché è importante*: Importare `Aspose.Cells` ti dà accesso a `Workbook`, `Worksheet` e al metodo `DeleteRows` che esegue la rimozione effettiva della riga.

## Passo 2: Carica la cartella di lavoro e seleziona il foglio di lavoro

Devi caricare il file sorgente (`input.xlsx`) e ottenere il foglio di lavoro che desideri modificare. Il primo foglio di lavoro è accessibile con indice `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Suggerimento**: Se hai bisogno di lavorare con un foglio specifico, sostituisci l'indice con il nome del foglio: `workbook.Worksheets["Data"]`.

## Passo 3: Elimina l'intera riga per il suo indice basato su zero

Aspose.Cells utilizza l'indicizzazione a base zero, quindi la prima riga è `0`. Per eliminare la riga 5 (la sesta riga visiva), chiama `DeleteRows` con `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Spiegazione*:

* `ws.Cells[5, 0]` indica la prima cella della riga che vuoi eliminare.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` indica ad Aspose.Cells di rimuovere **1** riga, e il flag `DeleteEntireRow` garantisce che **l'intera riga** scompaia, spostando verso l'alto le righe sottostanti.

### Come eliminare una riga per indice in altri scenari

* **Elimina più righe consecutive** – modifica il primo argomento con il numero di righe da cancellare:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Elimina l'ultima riga** – usa `ws.Cells.MaxDataRow` per ottenere l'indice dell'ultima riga popolata:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Questi snippet rispondono al requisito **remove row by index** mantenendo il codice facile da leggere.

## Passo 4: Salva la cartella di lavoro con la riga rimossa

Dopo l'eliminazione, scrivi la cartella di lavoro modificata su disco. Puoi sovrascrivere il file originale o crearne uno nuovo.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Se devi mantenere il file originale invariato, basta cambiare il percorso di output. Il metodo `Save` supporta molti formati (`.xls`, `.csv`, `.pdf`, ecc.) – basta cambiare l'estensione del file.

## Esempio completo funzionante

Mettiamo tutto insieme, ecco un programma completo, pronto all'esecuzione:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Output previsto**: Dopo aver eseguito il programma, `output.xlsx` conterrà tutte le righe originali eccetto quella che iniziava alla riga visiva 6. Tutti i dati sotto la riga rimossa si spostano verso l'alto automaticamente, preservando formule e formattazione.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|-------|----------------|-----|
| **Index out of range** | Tentativo di eliminare un indice di riga che non esiste (ad esempio `ws.Cells[1000,0]` in un foglio di 200 righe) | Usa `ws.Cells.MaxDataRow` per verificare l'indice valido più alto prima di chiamare `DeleteRows`. |
| **Partial row deletion** | Omettere `DeleteOptions.DeleteEntireRow` fa sì che vengano cancellati solo i contenuti delle celle | Passa sempre `DeleteOptions.DeleteEntireRow` quando è necessario rimuovere l'intera riga. |
| **Unexpected formula changes** | Eliminare righe che fanno parte di un intervallo di formula può rompere i riferimenti | Ricalcola le formule dopo l'eliminazione (`workbook.CalculateFormula()`) se la cartella di lavoro dipende da intervalli dinamici. |
| **Saving to a read‑only location** | La chiamata `Save` genera un'eccezione se la cartella è protetta | Assicurati che la directory di destinazione sia scrivibile o esegui il programma con i permessi appropriati. |

## Avanzato: Eliminare righe in base a una condizione

A volte è necessario rimuovere righe che soddisfano un certo criterio (ad esempio righe dove la colonna A è vuota). Il ciclo seguente dimostra un modo sicuro per scansionare dal basso verso l'alto ed eliminare le righe corrispondenti:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Scansionare verso l'alto previene il problema dello spostamento degli indici che si verifica quando si eliminano righe iterando in avanti.

## Conclusione

Ora sai come **delete entire row** in una cartella di lavoro Excel usando C#. La guida ha coperto:

* Caricamento di una cartella di lavoro e selezione di un foglio di lavoro  
* Uso di `DeleteRows` con `DeleteOptions.DeleteEntireRow` per **how to delete row** per indice  
* Salvataggio sicuro del file modificato  
* Gestione dei casi limite, consigli sulle prestazioni e un esempio di eliminazione condizionale  

Con queste conoscenze puoi implementare con sicurezza la funzionalità **remove row by index**, automatizzare la pulizia dei dati e integrare la manipolazione di Excel in qualsiasi applicazione C#.

**Passi successivi**: esplora altre funzionalità di Aspose.Cells come l'inserimento di righe, la copia di intervalli o la conversione della cartella di lavoro in PDF—ognuna delle quali si basa sugli stessi oggetti `Workbook` e `Worksheet` che hai appena padroneggiato. Buona programmazione!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Delete an Excel Row Using Aspose.Cells .NET&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}