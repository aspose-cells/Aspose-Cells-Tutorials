---
category: general
date: 2026-03-18
description: Copia tabella pivot in C# con Aspose.Cells. Scopri come copiare l'intervallo
  Excel, duplicare la pivot Excel, copiare l'intervallo in un nuovo foglio e copiare
  la pivot in un foglio in pochi minuti.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: it
og_description: Copia tabella pivot in C# usando Aspose.Cells. Impara a duplicare
  la pivot di Excel, copiare l’intervallo di Excel in una nuova posizione e copiare
  la pivot in un foglio con esempi di codice completi.
og_title: Copia della tabella pivot in C# – Guida completa alla programmazione
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copia della tabella pivot in C# – Guida passo passo
url: /it/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia tabella pivot in C# – Guida completa alla programmazione

Ti è mai capitato di dover **copiare una tabella pivot** da una parte di una cartella di lavoro a un'altra, senza perdere le connessioni dati sottostanti? Non sei il solo. Molti sviluppatori incontrano questo ostacolo quando automatizzano report Excel, soprattutto quando la pivot è inserita in un blocco dati più grande. La buona notizia? Con Aspose.Cells puoi copiare la tabella pivot **esattamente come appare**, e imparerai anche a **copiare un intervallo Excel**, **duplicare una pivot Excel**, e persino **copiare una pivot su un foglio** con poche righe di C#.

In questo tutorial affronteremo uno scenario reale: spostare una pivot che occupa *A1:J20* in una nuova area *M1:V20* nello stesso foglio di lavoro. Alla fine avrai un programma eseguibile, comprenderai perché ogni passaggio è importante e saprai come adattare il codice ad altri intervalli o anche a fogli separati. Nessuna documentazione esterna necessaria—tutto è qui.

---

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Aspose.Cells per .NET** (versione 23.9 o successiva). Puoi ottenerlo via NuGet: `Install-Package Aspose.Cells`.
- Un ambiente di sviluppo C# di base (Visual Studio 2022, Rider o VS Code con l’estensione C#).
- Un file Excel (`source.xlsx`) che contiene una tabella pivot nell’intervallo *A1:J20*.

È tutto. Se sai creare un’app console, sei pronto a partire.

---

## Come copiare una tabella pivot in Aspose.Cells

Il cuore della soluzione è una singola chiamata a `Worksheet.Cells.CopyRange`. Questo metodo non solo copia i valori grezzi delle celle, ma preserva automaticamente tabelle pivot, grafici e altri oggetti complessi. Vediamo i dettagli.

### Passo 1: Carica la cartella di lavoro di origine

Per prima cosa dobbiamo caricare la cartella di lavoro in memoria.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Perché è importante:** Il caricamento crea una rappresentazione in‑memoria che Aspose.Cells può manipolare senza avviare Excel. È veloce, thread‑safe e funziona sui server.

### Passo 2: Recupera il primo foglio di lavoro

La maggior parte degli esempi usa il primo foglio, ma puoi puntare a qualsiasi indice o nome.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Suggerimento:** Se devi **copiare una pivot su un foglio** diverso dallo stesso foglio, cambia semplicemente il riferimento `worksheet` con un altro oggetto `Worksheet`.

### Passo 3: Definisci gli intervalli di origine e destinazione

Useremo le strutture `CellArea` per descrivere i blocchi che stiamo spostando.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Spiegazione:** Gli indici di riga e colonna partono da zero. Colonna 0 = **A**, colonna 12 = **M**, e così via. Regola questi numeri se la tua pivot si trova altrove.

### Passo 4: Esegui l’operazione di copia

Ora avviene la magia. Impostare l’ultimo parametro booleano a `true` indica ad Aspose.Cells di copiare tutti gli oggetti—including la pivot.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Perché `true`?** Il flag indica “copia tutti gli oggetti”. Se lo imposti a `false`, verranno spostati solo i valori delle celle e la pivot andrà persa.

### Passo 5: Salva la cartella di lavoro

Infine, scrivi la cartella di lavoro modificata su disco.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Risultato:** `copy-pivot.xlsx` ora contiene la pivot originale in *A1:J20* **e** una copia identica in *M1:V20*. Apri il file in Excel per verificare che entrambe le pivot siano operative e mantengano le loro connessioni dati.

---

## Copia un intervallo Excel in una nuova posizione – una variazione rapida

A volte ti serve solo **copiare un intervallo Excel** senza preoccuparti delle pivot. Lo stesso metodo `CopyRange` fa al caso tuo; basta impostare l’ultimo argomento a `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Quando usarlo:** Se stai spostando dati grezzi per un foglio di calcolo temporaneo, disabilitare la copia degli oggetti risparmia memoria e velocizza l’operazione.

---

## Duplica una pivot Excel su più fogli

E se vuoi **duplicare una pivot Excel** su un foglio di lavoro diverso? Il modello rimane lo stesso; devi solo riferire un altro `Worksheet` come destinazione.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Caso limite:** Se la pivot di origine utilizza una tabella che risiede nel foglio originale, Aspose.Cells copierà anche la definizione della tabella sottostante, garantendo che la nuova pivot funzioni subito.

---

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| **La pivot perde la cache** | Uso di `CopyRange` con `false` o di una routine di copia personalizzata che ignora gli oggetti. | Passa sempre `true` quando ti serve la pivot stessa. |
| **Le celle di destinazione contengono già dati** | Sovrascrive silenziosamente, potenzialmente corrompendo formule esistenti. | Pulisci l’area di destinazione prima: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **L’intervallo di origine non include l’intera pivot** | Le tabelle pivot coprono più righe/colonne di quanto ti aspetti (es. righe nascoste). | Usa `worksheet.PivotTables[0].DataRange` per ottenere programmaticamente i limiti esatti. |
| **Copia tra cartelle di lavoro** | `CopyRange` funziona solo all’interno della stessa cartella di lavoro. | Usa `sourceWorksheet.Cells.CopyRange` verso un intervallo temporaneo, poi `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Output atteso & verifica

Dopo aver eseguito il programma:

1. Apri `copy-pivot.xlsx`.
2. Vedrai due tabelle pivot identiche—una in **A1:J20**, l’altra in **M1:V20**.
3. Aggiorna qualsiasi pivot; entrambe dovrebbero riflettere gli stessi dati sottostanti.
4. Se hai duplicato su un altro foglio, anche quel foglio conterrà una copia funzionante.

Un modo rapido per verificare via codice:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Consiglio avanzato: Automatizza il rilevamento dell’intervallo

Hard‑coding di `CellArea` funziona per report statici, ma il codice di produzione spesso deve individuare la pivot dinamicamente.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Perché farlo?** Rende la soluzione resiliente ai cambiamenti di layout—niente più errori “Oops, la pivot è passata a B2”.

---

![copy pivot table example](copy-pivot.png){alt="esempio di copia tabella pivot"}

*Lo screenshot (segnaposto) mostra la pivot originale a sinistra e quella duplicata a destra.*

---

## Riepilogo

Abbiamo appena coperto come **copiare una tabella pivot** in C# usando Aspose.Cells, esplorato modi per **copiare un intervallo Excel**, **duplicare una pivot Excel**, e persino **copiare una pivot su un foglio** tra fogli diversi. I punti chiave sono:

- Usa `Worksheet.Cells.CopyRange` con il flag `true` per preservare gli oggetti complessi.
- Definisci gli oggetti `CellArea` di origine e destinazione con indici a base zero.
- Modifica il foglio di destinazione se devi **copiare una pivot su un foglio**.
- Fai attenzione a casi limite come dati esistenti, righe nascoste e scenari cross‑workbook.

---

## Cosa fare dopo?

- **Scoperta dinamica delle pivot**: Crea un helper che scansioni una cartella di lavoro alla ricerca di tutte le pivot e le replichi automaticamente.
- **Esportazione in PDF/HTML**: Dopo la copia, potresti voler rendere il foglio in un formato report—Aspose.Cells lo gestisce anche.
- **Ottimizzazione delle prestazioni**: Per cartelle di lavoro molto grandi, considera di disabilitare il calcolo prima della copia e riabilitarlo dopo.

Sentiti libero di sperimentare: cambia le coordinate di destinazione, copia in una cartella di lavoro nuova, o anche itera su più fogli per creare un report consolidato. Le possibilità sono infinite, e con le basi che ora possiedi, potrai adattare il codice a praticamente qualsiasi compito di automazione Excel.

Buon coding, e che le tue pivot rimangano sempre perfettamente sincronizzate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}