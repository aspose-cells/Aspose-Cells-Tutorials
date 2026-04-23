---
category: general
date: 2026-03-30
description: Come copiare un foglio di lavoro in C# usando Aspose.Cells – guida passo‑passo
  che copre la copia di un intervallo di celle, la copia di colonne tra fogli, la
  copia della tabella pivot del foglio di lavoro e l'aggiunta di codice per un nuovo
  foglio di lavoro.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: it
og_description: Scopri come copiare un foglio di lavoro in C# con Aspose.Cells. Questa
  guida mostra come copiare un intervallo di celle, preservare le tabelle pivot, copiare
  colonne tra fogli e aggiungere il codice per un nuovo foglio di lavoro.
og_title: Come copiare un foglio di lavoro in C# – Tutorial completo di Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Come copiare un foglio di lavoro in C# con Aspose.Cells – Guida completa
url: /it/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Copiare un Foglio di Lavoro in C# con Aspose.Cells – Guida Completa

Ti sei mai chiesto **come copiare un foglio di lavoro** in C# senza perdere nemmeno una tabella pivot o una formula? Non sei solo: molti sviluppatori si trovano in difficoltà quando devono duplicare un foglio mantenendo intatti tutti gli elementi. In questo tutorial percorreremo una soluzione pratica, end‑to‑end, che non solo copia i dati ma preserva anche la **copy worksheet pivot table**, gestisce **copy cell range** e mostra il **add new worksheet code** di cui avrai bisogno.

Copriamo tutto, dal caricamento della cartella di lavoro di origine al salvataggio del file di destinazione, così potrai copiare colonne tra fogli, preservare gli oggetti e mantenere il codice pulito. Niente riferimenti vaghi, solo un esempio completo e funzionante da inserire subito nel tuo progetto.

## Cosa Copre Questo Tutorial

- Caricamento di un file Excel esistente con Aspose.Cells  
- Utilizzo del **add new worksheet code** per creare un foglio di destinazione  
- Definizione di un **copy cell range** che includa una tabella pivot  
- Configurazione di **CopyOptions** per mantenere grafici, formule e tabelle pivot intatti  
- Esecuzione di **copy columns between sheets** con precisione riga per riga  
- Salvataggio del risultato e verifica che il foglio sia stato copiato correttamente  

Al termine di questa guida sarai in grado di rispondere con sicurezza alla domanda “how to copy worksheet”, sia che tu stia automatizzando report sia che tu stia costruendo un’interfaccia basata su fogli di calcolo.

---

## Come Copiare un Foglio di Lavoro – Panoramica

Prima di immergerci nel codice, delineiamo il flusso ad alto livello. Pensalo come una ricetta:

1. **Load** la cartella di lavoro di origine (`Source.xlsx`).  
2. **Add** un nuovo foglio per contenere la copia (`add new worksheet code`).  
3. **Define** l’area che vuoi duplicare (`copy cell range`).  
4. **Configure** le opzioni di copia affinché la tabella pivot sopravviva (`copy worksheet pivot table`).  
5. **Copy** righe e colonne (`copy columns between sheets`).  
6. **Save** la nuova cartella di lavoro (`Destination.xlsx`).  

Tutto qui—sei passaggi, nessuna magia. Ogni passaggio è spiegato di seguito con snippet di codice e la logica sottostante.

---

## Passo 1 – Carica la Cartella di Lavoro di Origine

Prima di tutto: ti serve un’istanza di `Workbook` che punti al file che vuoi duplicare. Questo passaggio è fondamentale perché Aspose.Cells lavora direttamente sul file system, non sull’interfaccia di Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Perché è importante:* Il caricamento del file crea una rappresentazione in memoria di ogni foglio, cella e oggetto. Senza di esso non c’è nulla da copiare, e qualsiasi tentativo di `add new worksheet code` in seguito fallirebbe perché i dati di origine non sono presenti.

---

## Passo 2 – Aggiungi un Nuovo Foglio (add new worksheet code)

Ora abbiamo bisogno di un luogo dove incollare i dati copiati. Qui entra in gioco il **add new worksheet code**. Puoi dare al foglio qualsiasi nome; in questo esempio lo chiamiamo `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Consiglio professionale:* Se prevedi di copiare più fogli, chiama `Worksheets.Add` all’interno di un ciclo e assegna a ciascun foglio un nome univoco. In questo modo eviti collisioni di nomi e mantieni ordinata la cartella di lavoro.

---

## Passo 3 – Definisci il Copy Cell Range

Un **copy cell range** indica ad Aspose.Cells esattamente quali righe e colonne duplicare. In molti scenari reali l’intervallo include una tabella pivot, quindi è necessario essere precisi.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Perché è necessario:* Dichiarando esplicitamente l’intervallo eviti di copiare l’intero foglio (potrebbe essere inefficiente) e garantisci che la tabella pivot rimanga all’interno dell’area copiata. Questo è il fulcro di **how to copy worksheet** quando ti serve solo una parte del foglio.

---

## Passo 4 – Imposta le Opzioni di Copia (preserve copy worksheet pivot table)

Aspose.Cells offre un oggetto `CopyOptions` che controlla cosa viene incollato. Per mantenere la tabella pivot, i grafici e le formule, impostiamo `PasteType.All` e abilitiamo `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Spiegazione:* `PasteType.All` è l’opzione più inclusiva, mentre `PasteSpecial` indica al motore di trattare correttamente oggetti complessi—come le tabelle pivot. Saltare questo passaggio è un errore comune; il foglio copiato perderebbe le sue funzionalità interattive.

---

## Passo 5 – Copia Righe e Colonne (copy columns between sheets)

Ora arriva la parte più impegnativa: spostare effettivamente i dati. Useremo `CopyRows` e `CopyColumns` per gestire **copy columns between sheets**. Eseguire entrambi assicura che le celle unite e le larghezze delle colonne vengano preservate.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Cosa succede:* `CopyRows` sposta i dati riga per riga, mentre `CopyColumns` fa lo stesso colonna per colonna. Eseguire entrambi garantisce che l’intero blocco rettangolare sia duplicato, cosa essenziale quando devi **copy columns between sheets** con larghezze o colonne nascoste differenti.

---

## Passo 6 – Salva la Cartella di Lavoro

Infine, scrivi le modifiche su disco. Questo passaggio completa il processo di **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Suggerimento di verifica:* Apri `Destination.xlsx` e controlla che il foglio `"Copy"` sia identico all’originale, che le tabelle pivot siano operative e che le larghezze delle colonne corrispondano. Se qualcosa non quadra, ricontrolla le impostazioni di `CopyOptions`.

---

## Casi Limite e Varianti Comuni

### Copia di Più Fogli di Lavoro

Se devi duplicare diversi fogli, avvolgi la logica precedente in un ciclo `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Conservare le Formule tra Cartelle di Lavoro Diverse

Quando le cartelle di lavoro di origine e destinazione hanno intervalli denominati diversi, imposta `copyOptions` su `PasteType.Formulas` oltre a `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Grandi Intervalli e Prestazioni

Per dataset massivi (centinaia di migliaia di righe), considera di usare solo `CopyRows` e saltare `CopyColumns` se le larghezze delle colonne non sono critiche. Questo può ridurre di qualche secondo i tempi di esecuzione.

---

## Esempio Completo

Di seguito trovi il programma completo, pronto per l’esecuzione, che racchiude tutto quanto discusso. Incollalo in una console app, adatta i percorsi dei file e premi **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Risultato atteso:** Aprendo `Destination.xlsx` vedrai un foglio chiamato **Copy** che rispecchia il primo foglio di `Source.xlsx`—incluse tabelle pivot, formattazione e larghezze delle colonne. Il file originale rimane intatto.

---

## Domande Frequenti

**D: Funziona con file .xlsx creati da Excel 2019?**  
R: Assolutamente. Aspose.Cells supporta tutti i formati Excel moderni, quindi lo stesso codice funziona per `.xlsx`, `.xlsm` e anche per i più vecchi file `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}