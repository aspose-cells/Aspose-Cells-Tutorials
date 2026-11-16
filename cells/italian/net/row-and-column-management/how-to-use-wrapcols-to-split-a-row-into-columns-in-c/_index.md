---
category: general
date: 2026-11-16
description: Scopri come usare WRAPCOLS in C# per suddividere una riga in colonne,
  automatizzare una cartella di lavoro Excel, calcolare le formule e salvare il file
  Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: it
lastmod: 2026-11-16
og_description: Come utilizzare WRAPCOLS in C# per suddividere una riga in colonne,
  automatizzare una cartella di lavoro Excel, eseguire il calcolo delle formule e
  salvare il file Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Come usare WRAPCOLS in C# – dividere le righe, calcolare le formule e salvare
  i file Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Come usare WRAPCOLS per dividere una riga in colonne in C#
url: /it/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare WRAPCOLS per suddividere una riga in colonne in C#

Se hai bisogno di **come usare WRAPCOLS** in un progetto C#, questa guida ti mostra una soluzione completa e funzionante. Vedrai come suddividere una riga in colonne, automatizzare una cartella di lavoro Excel, attivare il calcolo delle formule Excel e, infine, salvare il file Excel in stile C#.

Lavorare con Excel in modo programmatico spesso significa gestire grandi insiemi di dati, e la funzione `WRAPCOLS` ti consente di rimodellare una singola riga in una matrice senza dover iterare manualmente. I passaggi seguenti coprono tutto ciò di cui hai bisogno—dalla creazione della cartella di lavoro all'output finale del file—così potrai integrare la tecnica in qualsiasi applicazione .NET.

## Cosa copre questo tutorial

* Creazione di una nuova cartella di lavoro e accesso al suo primo foglio.  
* Popolamento di una riga con valori sequenziali (1‑20).  
* Applicazione della formula Excel `WRAPCOLS` per suddividere la riga in blocchi da 5 colonne.  
* Esecuzione del **calcolo delle formule Excel** affinché il risultato diventi parte del foglio.  
* Utilizzo di **save excel file c#** per scrivere la cartella di lavoro su disco.  

Non è necessaria alcuna configurazione esterna oltre alla libreria Aspose.Cells per .NET (o qualsiasi API compatibile che supporti `WRAPCOLS`). Alla fine della guida avrai un file chiamato `WrapColsDemo.xlsx` che contiene quattro righe di cinque colonne ciascuna, derivato dai dati originali a riga singola.

## Prerequisiti

* .NET 6.0 o successivo (il codice funziona anche con .NET Core 3.1 e .NET Framework 4.7+).  
* Un riferimento a **Aspose.Cells** (disponibile via NuGet: `Install-Package Aspose.Cells`).  
* Familiarità di base con la sintassi C# e le formule Excel.  

> **Suggerimento professionale:** Se preferisci un’alternativa gratuita, la libreria open‑source EPPlus supporta anche formule personalizzate, ma `WRAPCOLS` è integrata solo nelle librerie che implementano il motore di calcolo completo di Excel, come Aspose.Cells.

## Passo 1: Creare una nuova cartella di lavoro e ottenere il primo foglio

La prima operazione è istanziare un oggetto `Workbook` e recuperare il suo foglio predefinito. Questo oggetto rappresenta l’intero file Excel in memoria.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Creare la cartella di lavoro programmaticamente è la base delle attività di **automate excel workbook**. Il riferimento `Worksheet` ti permette di manipolare le celle direttamente.

## Passo 2: Riempire la prima riga con i valori 1‑20

Successivamente, popola le celle da `A1` a `T1` con i numeri da 1 a 20. Un semplice ciclo `for` scrive ogni valore nella colonna appropriata.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Perché scrivere i valori programmaticamente? Garantisce che la demo funzioni su qualsiasi macchina senza inserimento manuale dei dati, cosa essenziale quando **automate excel workbook** in processi batch.

## Passo 3: Applicare la funzione WRAPCOLS per suddividere la riga in blocchi da 5 colonne

Ora utilizziamo la formula Excel `WRAPCOLS`. Essa prende un intervallo di origine e un conteggio di colonne, restituendo un array bidimensionale che “avvolge” i dati di origine nel numero specificato di colonne.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Inserire la formula nella cella `A2` indica a Excel di iniziare l’output dalla seconda riga. Il risultato sarà una matrice 4 × 5 perché 20 elementi divisi per 5 colonne producono quattro righe.

### Come funziona WRAPCOLS

* **Intervallo di origine** – `A1:T1` contiene i 20 valori originali.  
* **Conteggio colonne** – `5` dice a Excel di creare cinque colonne per riga.  
* **Risultato** – Excel riempie le celle `A2:E5` con i dati avvolti automaticamente.

Se mai dovessi **split row into columns** con una dimensione di blocco diversa, basta modificare il secondo argomento. Per esempio, `WRAPCOLS(A1:T1,4)` produrrebbe cinque righe di quattro colonne ciascuna.

## Passo 4: Calcolare le formule affinché il risultato di WRAPCOLS sia materializzato

Una formula appena aggiunta rimane non valutata finché il motore di calcolo non viene eseguito. Invocando `CalculateFormula()`, garantisci che il passaggio di **excel formula calculation** scriva i valori effettivi nel foglio.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Eseguire il calcolo è fondamentale quando in seguito **save excel file c#**, perché il file salvato deve contenere i valori calcolati, non solo il testo della formula. Senza questo passaggio, la cartella di lavoro di output mostrerebbe `#N/A` o la formula grezza anziché i numeri attesi.

## Passo 5: Salvare la cartella di lavoro su disco

Infine, persisti la cartella di lavoro usando il metodo `Save`. Puoi specificare qualsiasi percorso file valido; l’esempio utilizza una directory segnaposto che dovrai sostituire con la tua.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

La chiamata `Save` dimostra **save excel file c#** nella sua forma più semplice. Aspose.Cells sceglie automaticamente il formato XLSX in base all’estensione del file. Se ti serve un file `.xls` più vecchio, cambia l’estensione di conseguenza.

### Output previsto

Apri `WrapColsDemo.xlsx` e vedrai:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

La riga singola originale è stata **split row into columns** su quattro righe, ognuna contenente cinque colonne.

## Codice sorgente completo

Unire tutti i passaggi produce un programma compatto e autonomo:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Copia il codice in un nuovo progetto console, ripristina il pacchetto NuGet Aspose.Cells e avvia. Il programma crea il file Excel sul desktop in pochi secondi.

## Varianti comuni e casi limite

| Situazione | Adeguamento |
|-----------|------------|
| **Dimensione blocco diversa** | Cambia `WRAPCOLS(A1:T1,5)` in `WRAPCOLS(A1:T1, n)` dove `n` è il conteggio di colonne desiderato. |
| **Più righe di origine** | Usa `WRAPCOLS(A1:A10,5)` per avvolgere un intervallo verticale in una matrice a 5 colonne. |
| **Intervallo di origine dinamico** | Costruisci la stringa di indirizzo in C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) prima di assegnare la formula. |
| **Fogli di lavoro grandi** | Chiama `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` per saltare le celle che generano errori e migliorare le prestazioni. |
| **Salvataggio come CSV** | Sostituisci `workbook.Save(outputPath)` con `workbook.Save(outputPath, SaveFormat.Csv)`. |

Queste varianti mostrano come lo stesso modello **how to use wrapcols** possa essere adattato a molteplici scenari di ristrutturazione dei dati.

## Consigli per la risoluzione dei problemi

* **Formula non valutata** – Assicurati di chiamare `workbook.CalculateFormula()` *dopo* aver impostato la formula. Saltare questo passaggio lascia la cella con il testo grezzo `WRAPCOLS`.  
* **Accesso al file negato** – Verifica che la directory di destinazione esista e che il processo abbia i permessi di scrittura. Usare `Environment.SpecialFolder.Desktop` evita la maggior parte dei problemi di permessi.  
* **Numero di righe errato** – Ricontrolla il secondo argomento di `WRAPCOLS`. Definisce il conteggio di colonne, non quello di righe; le righe derivano dal totale delle celle di origine diviso per quel conteggio di colonne.

## Conclusione

Ora sai **come usare WRAPCOLS** in C# per **split row into columns**, creare completamente **automate excel workbook**, eseguire **excel formula calculation** e **save excel file c#** con un unico, pulito codice. Questa tecnica elimina le operazioni manuali di copia‑incolla e scala senza sforzo per grandi pipeline di trasformazione dei dati.

### Prossimi passi

* Esplora altre funzioni di array dinamico come `SEQUENCE`, `FILTER` e `UNIQUE` per arricchire il tuo toolkit di automazione Excel.  
* Combina `WRAPCOLS` con le API di generazione di grafici per produrre report pronti alla pubblicazione.  
* Integra il codice in un servizio in background che elabora upload CSV e genera file Excel ristrutturati per analisi successive.

Sentiti libero di sperimentare con intervalli di origine e conteggi di colonne diversi—adatta la formula, riesegui il calcolo e osserva l’aggiornamento immediato della cartella di lavoro. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci alternativi nei tuoi progetti.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}