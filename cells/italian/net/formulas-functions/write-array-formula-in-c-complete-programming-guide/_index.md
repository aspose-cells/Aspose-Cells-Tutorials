---
category: general
date: 2026-07-03
description: Scrivi una formula di matrice in C# per creare un array a 2 colonne,
  calcolare la cella di Excel e distribuire l'elenco in colonne. Segui questo esempio
  passo‑passo usando Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: it
og_description: Scrivi una formula di array in C# per creare un array a 2 colonne,
  calcolare la cella di Excel e disporre l'elenco in colonne. Scopri l'intero processo
  con codice eseguibile.
og_title: Scrivi formula di array in C# – Guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: Scrivi formula di array in C# – Guida completa alla programmazione
url: /it/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Scrivi una formula array in C# – Guida completa alla programmazione

Ti è mai capitato di **scrivere una formula array** in C# ma non sapevi come far sì che Excel restituisca un elenco ben formattato? Non sei solo. Molti sviluppatori si trovano in difficoltà quando cercano di *generare risultati di array Excel* senza aprire l'interfaccia. In questo tutorial percorreremo un esempio conciso, end‑to‑end, che **scrive una formula array**, **calcola la cella Excel**, e **avvolge l'elenco in colonne** per **creare un array a 2 colonne** che puoi salvare e ispezionare.

Useremo la popolare libreria Aspose.Cells perché permette di manipolare le cartelle di lavoro interamente via codice. Alla fine avrai uno snippet pronto da eseguire, una spiegazione chiara di ogni riga e idee per estendere il modello a dataset più grandi. Niente superflui—solo le parti pratiche che puoi copiare‑incollare subito.

## Cosa ti serve

Prima di iniziare, assicurati di avere:

* .NET 6.0 o successivo (il codice funziona anche su .NET Core)  
* Un riferimento a **Aspose.Cells** (puoi scaricarlo da NuGet: `Install-Package Aspose.Cells`)  
* Una cartella in cui leggere/scrivere file Excel – la chiameremo `YOUR_DIRECTORY` negli esempi  

Questo è tutto. Nessun interop Excel aggiuntivo, nessun COM, solo codice gestito puro.

![Esempio di scrittura di formula array in C#](write-array-formula.png "Screenshot che mostra l'array a 2 colonne generato in Excel – scrivi formula array in C#")

## Passo 1: Scrivi la formula array con Aspose.Cells

La prima cosa da fare è **scrivere la formula array** in una cella. Nella sintassi di Excel la funzione `WRAPCOLS` prende un elenco piatto e lo rimodella in una matrice. Ecco come farlo programmaticamente:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**Perché è importante:** La proprietà `Formula` contiene la stringa letterale della formula Excel. Usando `WRAPCOLS` diciamo a Excel di prendere l'array lineare `{1,2,3,4}` e disporlo in un layout a 2 colonne, creando effettivamente **un array a 2 colonne**. La formula stessa è una *formula array*—noterai le parentesi graffe intorno ai numeri.

## Passo 2: Calcola la cella Excel affinché la formula venga valutata

Scrivere la formula non basta; dobbiamo **calcolare la cella Excel** così il motore la valuta. Aspose.Cells non ricalcola automaticamente a meno che non lo chiedi:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**Perché questo passaggio è cruciale:** Senza invocare `Calculate()`, la cella rimane in uno stato “in sospeso” e la cartella di lavoro salvata conterrà la formula grezza, non i valori calcolati. Ricalcolando esplicitamente, garantiamo che l'array di output sia materializzato nel file.

## Passo 3: Avvolgi l'elenco in colonne – vedi il risultato

A questo punto il foglio contiene un blocco a 2 colonne a partire da `A1`. Se apri il file vedrai:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

Questa è la rappresentazione visiva di **avvolgere l'elenco in colonne** usando la funzione `WRAPCOLS`. Se preferisci un numero diverso di colonne, cambia semplicemente il secondo argomento:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

Ora l'array appare così:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**Consiglio professionale:** Quando lavori con dataset più grandi, costruisci dinamicamente la stringa dell'elenco (ad es., usando `string.Join(",", myNumbers)`) per evitare di codificare valori fissi.

## Passo 4: Salva la cartella di lavoro e verifica l'output

Infine, persisti la cartella di lavoro su disco così da poterla aprire in Excel e confermare il lavoro di **generare array Excel**:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Apri `output.xlsx` e vedrai l'array a 2 colonne esattamente come descritto. Se modifichi la formula e ricalcoli, il file salvato si aggiorna automaticamente—nessun aggiornamento manuale necessario.

## Esempio completo, eseguibile

Mettendo tutto insieme, ecco il programma completo che puoi inserire in una console app:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**Output previsto:** Quando apri `output.xlsx`, le celle `A1:B2` contengono i numeri da 1 a 4 disposti in due colonne. La console stampa una conferma amichevole.

## Casi limite e domande frequenti

### E se ho bisogno di un intervallo dinamico invece di un elenco hard‑coded?

Puoi costruire la parte elenco della formula a runtime:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

Questo continua a **generare array Excel**, ma ora i dati di origine provengono dalla logica della tua applicazione.

### `WRAPCOLS` funziona su versioni più vecchie di Excel?

`WRAPCOLS` è disponibile a partire da Excel 365/2019. Se punti a versioni più vecchie, dovrai simulare il comportamento con trucchi `INDEX` e `MOD`, ma diventa rapidamente ingombrante. Usare Aspose.Cells ti permette di mantenere la formula moderna e produrre comunque un file compatibile per la maggior parte degli utenti.

### Posso scrivere la formula su un intervallo invece che su una singola cella?

Sì—assegna la stessa formula alla cella in alto a sinistra dell'intervallo, poi chiama `Calculate()` sull'oggetto range:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

Il risultato è identico, ma hai più controllo su dove vive l'array.

## Considerazioni sulle prestazioni

Quando **calcoli celle Excel** per molte formule, Aspose.Cells può eseguire calcoli in batch per velocizzare. Se generi migliaia di array, chiama `workbook.CalculateFormula()` una sola volta dopo aver impostato tutte le formule, invece di `Calculate()` su ogni cella. Questo riduce drasticamente l'overhead.

## Prossimi passi

Ora che sai come **scrivere una formula array**, **calcolare la cella Excel**, e **avvolgere l'elenco in colonne** per **creare un array a 2 colonne**, potresti esplorare:

* **Generare array Excel** per report multi‑foglio  
* Applicare stili (bordi, formati numerici) all'intervallo risultante  
* Esportare la cartella di lavoro in PDF o CSV per elaborazioni successive  
* Combinare con regole di convalida dati per creare fogli di calcolo interattivi  

Ognuno di questi si basa sulla tecnica centrale che abbiamo trattato, permettendoti di automatizzare flussi di lavoro Excel complessi interamente da C#.

---

**In sintesi**, questa guida ti ha mostrato come **scrivere una formula array** in C# usando Aspose.Cells, forzare il passaggio di **calcolare la cella Excel** e **avvolgere l'elenco in colonne** per **creare un array a 2 colonne** che puoi **generare file Excel array**. Il codice è completamente eseguibile, le spiegazioni coprono il *perché* di ogni riga, e hai consigli per scalare e gestire casi limite.

Provalo, modifica il numero di colonne, inserisci i tuoi dati e guarda Excel fare il lavoro pesante per te. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Create Excel List Objects Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Import Multi Dimensional Array Excel Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}