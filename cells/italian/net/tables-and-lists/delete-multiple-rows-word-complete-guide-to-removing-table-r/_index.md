---
category: general
date: 2026-06-27
description: Elimina più righe in Word usando C#. Scopri come eliminare righe di tabelle,
  rimuovere righe di tabelle e modificare le tabelle dei documenti Word in modo efficiente.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: it
og_description: Elimina più righe in Word istantaneamente. Questo tutorial mostra
  come eliminare le righe di una tabella, rimuovere le righe da una tabella di Word
  e gestire la modifica delle tabelle nel documento principale.
og_title: Elimina più righe in Word – Modifica della tabella passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Elimina più righe in Word – Guida completa per rimuovere le righe della tabella
url: /it/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Elimina più righe in Word – Guida completa per rimuovere righe di tabella

Hai mai dovuto **eliminare più righe in documenti Word** ma non sapevi quale chiamata API utilizzare? Non sei solo: la maggior parte degli sviluppatori incontra lo stesso ostacolo quando cerca di ridurre una tabella mantenendo intatta l’intestazione.  

In questo tutorial percorreremo una soluzione concisa, end‑to‑end, che mostra *come eliminare righe di tabella* programmaticamente, *come rimuovere righe di tabella* in modo sicuro, e perché l’approccio funziona per ogni scenario di **cancellazione di righe da una tabella Word** che potresti incontrare.

Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto C#, più una serie di consigli per attività più ampie di **modifica di tabelle in documenti Word**.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.6+)
- Aspose.Words per .NET installato (`dotnet add package Aspose.Words`)
- Una conoscenza di base della sintassi C#
- Un file `.docx` di input che contenga almeno una tabella con una riga di intestazione

> **Pro tip:** Se non hai ancora una licenza, Aspose.Words offre una modalità di valutazione gratuita perfetta per i test.

## Passo 1: Configura il progetto e carica il documento Word

Prima di tutto—crea un’app console (o integrala in un servizio esistente) e aggiungi le direttive `using` necessarie. Quindi carica il documento sorgente.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**Perché è importante:**  
`Document` è il punto di ingresso per ogni operazione di Aspose.Words. Caricare il file una sola volta mantiene basso l’utilizzo di memoria e ti fornisce un handle per tutte le successive chiamate di modifica della tabella.

## Passo 2: Individua la prima tabella (o qualsiasi tabella di cui hai bisogno)

Se il tuo documento contiene diverse tabelle, puoi scegliere quella desiderata per indice o cercando una parola chiave. Per semplicità prenderemo la prima tabella, che di solito contiene i dati che vogliamo ridurre.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**Spiegazione:**  
`GetChild(NodeType.Table, 0, true)` attraversa l’albero del documento in profondità e restituisce il primo nodo `Table` che incontra. Il cast `as Table` converte in modo sicuro il nodo, permettendoci di lavorare con `Rows` in seguito.

## Passo 3: Elimina più righe mantenendo l’intestazione

Ora arriviamo al nocciolo della questione: **eliminare più righe in documenti Word**. Supponiamo che l’intestazione sia nella riga 0 e che tu voglia rimuovere le due righe successive (indici 1 e 2). Il metodo `DeleteRows` fa esattamente questo.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### Come eliminare righe di tabella – Varianti

- **Elimina una singola riga:** `firstTable?.DeleteRows(rowIndex, 1);`
- **Elimina tutte le righe tranne l’intestazione:** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **Elimina righe in base a una condizione:** itera `firstTable.Rows` e chiama `DeleteRows` quando una cella corrisponde ai tuoi criteri.

Questi snippet rispondono alla domanda comune **come rimuovere righe di tabella** in modo flessibile.

## Passo 4: Salva il documento modificato

Dopo che le righe sono state rimosse, basta scrivere il documento su disco. Puoi sovrascrivere il file originale o crearne una copia nuova.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**Cosa vedrai:**  
Se la tabella originale aveva, ad esempio, cinque righe (intestazione + quattro righe di dati), il `output.docx` salvato conterrà ora solo tre righe (intestazione + le due righe di dati rimanenti). Apri il file in Word per verificare che le righe indesiderate siano sparite senza alterare altri contenuti.

![delete multiple rows word example](delete-multiple-rows-word.png)

*Testo alternativo immagine: elimina più righe word – screenshot prima e dopo di una tabella Word.*

## Esempio completo, pronto da eseguire

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

Esegui il programma, apri `output.docx` e vedrai l’intestazione ancora presente mentre le righe scelte sono scomparse. Questo è **eliminare più righe in Word** in azione.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| **NullReferenceException** quando `firstTable` è `null` | Il documento non contiene tabelle o l’indice è errato | Controlla sempre `firstTable != null` prima di chiamare `DeleteRows`. |
| **Righe non eliminate** | Uso di un indice di partenza errato (le tabelle Word partono da zero) | Ricorda che l’intestazione è la riga 0; inizia da 1 per mantenerla. |
| **Salvataggio su file di sola lettura** | I permessi del file impediscono la sovrascrittura | Salva in un percorso diverso o modifica gli attributi del file. |
| **Modifiche di layout inattese** | Eliminare righe che contengono celle unite può corrompere la tabella | Gestisci le celle unite—separa prima o elimina le righe intere con attenzione. |

## Estendere la soluzione – Altre operazioni di modifica tabelle in documenti Word

Se ti interessa una modifica più ampia di **tabelle in documenti Word**, considera i seguenti passi successivi:

- **Inserire nuove righe**: `firstTable?.Rows.Add(new Row(doc));`
- **Aggiornare il testo di una cella**: `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **Applicare stili**: usa `CellFormat` o `RowFormat` per impostare sfumature, bordi o proprietà del font.
- **Esportare in PDF**: `doc.Save("output.pdf", SaveFormat.Pdf);`

Tutte queste operazioni si basano sullo stesso modello di oggetti usato per l’eliminazione delle righe, mantenendo coerente il tuo codice.

## Conclusione

Ti abbiamo appena mostrato come **eliminare più righe in documenti Word** con poche righe di codice C#. L’approccio copre *come eliminare righe di tabella*, *come rimuovere righe di tabella* e il tema più ampio della **modifica di tabelle in documenti Word**.  

Ora disponi di un modello solido e riutilizzabile: carica il documento, individua la tabella, chiama `DeleteRows` con gli indici corretti e salva. Da qui puoi modificare l’intervallo di righe, iterare su più tabelle o combinare con altre funzionalità di editing per soddisfare qualsiasi compito di automazione.

Pronto per andare oltre? Prova ad automatizzare la generazione di fatture, a pulire modelli di report o a costruire uno strumento di aggiornamento massivo che elabori decine di file Word in un solo colpo. Il cielo è il limite, e l’API lo rende indolore.

Se incontri difficoltà, lascia un commento qui sotto—buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Delete Multiple Rows in Excel with Aspose.Cells .NET: A Comprehensive Guide for Data Manipulation](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Delete Multiple Rows in Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}