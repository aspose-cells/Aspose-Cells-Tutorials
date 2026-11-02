---
category: general
date: 2026-07-13
description: Sposta le celle verso l'alto in Excel usando C#. Scopri come rimuovere
  le prime righe, eliminare più righe e rimuovere righe da una tabella in un'unica
  operazione sicura.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: it
lastmod: 2026-07-13
og_description: Sposta le celle verso l'alto in un foglio di lavoro Excel usando C#.
  Questo tutorial mostra come rimuovere le prime righe, eliminare più righe e rimuovere
  in modo sicuro le righe da una tabella.
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: Sposta le celle verso l'alto in Excel con C# – Guida completa alla programmazione
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Sposta le celle verso l'alto in Excel con C# – Guida completa
url: /it/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sposta le Celle Verso l'Alto in Excel con C# – Guida Completa

Ti sei mai chiesto come **spostare le celle verso l'alto** dopo aver eliminato righe in un file Excel? Non sei l'unico. Che tu stia pulendo dati importati o riducendo un enorme report, la capacità di rimuovere le prime righe senza rompere una tabella è una competenza indispensabile per qualsiasi sviluppatore C#.

In questo tutorial percorreremo una soluzione pratica, end‑to‑end, che mostra **come eliminare righe**, mantenere intatta l'intestazione e spostare automaticamente le celle rimanenti verso l'alto. Alla fine potrai **rimuovere righe da una tabella**, **eliminare più righe** e **rimuovere le prime righe** in poche righe di codice.

---

## Cosa Ti Serve

- .NET 6+ (o .NET Framework 4.7.2 e versioni successive)  
- La libreria **Aspose.Cells for .NET** (trial gratuito o licenza)  
- Una conoscenza di base di C# e Visual Studio (o qualsiasi IDE tu preferisca)  

Nessuna altra dipendenza—solo il pacchetto NuGet e un file Excel su cui sperimentare.

---

## Passo 1: Installa Aspose.Cells

Prima di tutto, aggiungi il pacchetto Aspose.Cells al tuo progetto:

```bash
dotnet add package Aspose.Cells
```

Quella singola riga scarica tutto il necessario per lavorare con cartelle di lavoro, fogli di lavoro e tabelle. Se usi Visual Studio, puoi anche fare clic destro sul progetto → **Manage NuGet Packages** → cerca *Aspose.Cells* e premi **Install**.

*Pro tip:* Usa l'ultima versione stabile; a luglio 2026 è **23.9.0**, che supporta i formati Excel più recenti.

---

## Passo 2: Carica la Cartella di Lavoro Contenente la Tabella

Ora apriremo il file Excel che contiene i dati da pulire. Sostituisci `YOUR_DIRECTORY` con il percorso reale sul tuo computer.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

A questo punto abbiamo un oggetto `Worksheet` pronto per la manipolazione. Nota che non abbiamo ancora toccato la tabella—preservare l'intestazione è fondamentale quando più tardi **sposteremo le celle verso l'alto**.

---

## Passo 3: Elimina le Prime Due Righe Mentre Sposti le Celle Verso l'Alto

Ecco il nocciolo della questione: eliminare righe *e* far sì che le celle sottostanti si spostino verso l'alto automaticamente. Aspose.Cells fornisce un metodo `DeleteRows` che fa esattamente questo quando passi `true` per il flag `shiftCellsUp`.

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### Perché il flag `true` è importante

Se ometti il flag `true`, le righe vengono rimosse ma lo spazio che occupavano rimane vuoto, creando buchi nei dati. Impostandolo a **true** si indica alla libreria di comprimere l'intervallo, **spostando le celle verso l'alto** in modo che la riga 3 diventi la nuova riga 1. Questo è il modo più pulito per **rimuovere le prime righe** senza rompere formule o strutture di tabella.

> **Importante:** Eliminare righe che includono l'intestazione della tabella genererà un'eccezione. Mantieni intatta la riga di intestazione (di solito la riga 0) o eliminala separatamente dopo aver ricreato l'intestazione della tabella.

---

## Passo 4: Verifica che la Tabella Sia Ancora Corretta

Dopo l'eliminazione, è buona norma ricontrollare che il riferimento della tabella punti ancora all'intervallo corretto. Puoi stampare l'indirizzo della tabella o aggiornarlo:

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

Eseguendo il programma dovresti vedere qualcosa come `Table1!A1:D8` invece dell'originale `A1:D10`, confermando che le righe sono state rimosse e le celle spostate verso l'alto.

---

## Passo 5: Salva la Cartella di Lavoro Modificata

Infine, scrivi le modifiche su disco. Puoi sovrascrivere il file originale o crearne una copia nuova—come preferisci.

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

Apri `modified_table.xlsx` in Excel e vedrai le prime due righe scomparse, le righe rimanenti spostate verso l'alto e la tabella ancora intatta. L'operazione ha effettivamente **eliminato più righe** mantenendo l'integrità dei dati.

---

## Casi Limite e Problemi Comuni

| Situazione | Cosa Accade | Come Gestirla |
|------------|-------------|----------------|
| **La riga di intestazione fa parte dell'intervallo da eliminare** | Aspose.Cells lancia `InvalidOperationException` perché una tabella non può perdere l'intestazione. | Elimina solo le righe di dati, oppure ricrea l'intestazione dopo l'eliminazione usando `sheet.Cells["A1"].PutValue("Header")`. |
| **La tabella si estende su più fogli di lavoro** | Eliminare righe su un foglio non influisce sugli altri. | Itera su ogni foglio e le relative tabelle se hai bisogno di una pulizia globale. |
| **File di grandi dimensioni (>100 MB)** | L'uso di memoria aumenta notevolmente. | Usa `LoadOptions` con `MemoryPreference` impostato a `MemoryPreference.MemoryOnly` per ridurre l'impronta RAM. |
| **Devi mantenere le formule che fanno riferimento alle righe eliminate** | Le formule possono diventare `#REF!`. | Usa `sheet.Cells.DeleteRows(startRow, count, true, true)` – il quarto argomento indica ad Aspose.Cells di aggiornare le formule. |

---

## Domande Frequenti

**D: Posso eliminare righe in base a una condizione anziché a un indice fisso?**  
R: Assolutamente. Scorri `sheet.Cells.Rows` e chiama `DeleteRows(rowIndex, 1, true)` ogni volta che la condizione è soddisfatta. Ricorda di iterare all'indietro per evitare lo spostamento degli indici.

**D: Funziona con file `.xls`?**  
R: Sì. Aspose.Cells supporta sia i formati `.xlsx` sia i legacy `.xls`. L'API è la stessa.

**D: Cosa succede se il mio workbook contiene più tabelle e ne voglio modificare solo una?**  
R: Individua la tabella specifica per nome: `Table myTable = sheet.Tables["MyTable"];` poi usa `myTable.Range.StartRow` per calcolare le righe da eliminare.

---

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione, che incorpora tutto quanto discusso. Copialo in una console app, aggiusta i percorsi dei file e premi **F5**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**Risultato atteso:**  
- Le righe 1‑2 scompaiono dal foglio.  
- La riga 3 diventa la nuova riga 1, la riga 4 diventa la riga 2, ecc.  
- L'intervallo della tabella si aggiorna automaticamente, confermando che **spostare le celle verso l'alto** ha funzionato come previsto.

---

## Conclusione

Abbiamo appena visto come **spostare le celle verso l'alto** in un foglio Excel usando C#. Sfruttando il metodo `DeleteRows` di Aspose.Cells con il flag `true`, puoi **rimuovere le prime righe**, **eliminare più righe** e **rimuovere righe da una tabella** senza compromettere il modello dei dati. L'approccio è veloce, affidabile e funziona con tutti i formati Excel moderni.

Pronto per il passo successivo? Prova a combinare questa tecnica con un filtro condizionale per eliminare righe vuote o duplicate. Oppure esplora le API di styling di Aspose.Cells per riapplicare la formattazione dopo lo spostamento. Il cielo è il limite quando domini la manipolazione delle righe in Excel.

Hai domande o un caso d'uso interessante da condividere? Lascia un commento qui sotto, e buona programmazione!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che ampliano le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Elimina più righe in Excel con Aspose.Cells .NET: Guida completa per la manipolazione dei dati](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Come inserire ed eliminare righe in Excel con Aspose.Cells per .NET: Guida completa](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Come eliminare righe vuote in Excel usando Aspose.Cells .NET per la pulizia dei dati](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}