---
category: general
date: 2026-02-15
description: Come usare WRAPCOLS per creare un layout a due colonne, aggiungere una
  formula e generare un array di sequenza nei fogli di lavoro C# – guida passo‑passo.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: it
og_description: Come utilizzare WRAPCOLS per creare un layout a due colonne, aggiungere
  formule e generare un array di sequenza in un foglio di lavoro C# – guida completa.
og_title: 'Come usare WRAPCOLS: layout a due colonne in C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Come usare WRAPCOLS: creare un layout a due colonne in C#'
url: /it/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare WRAPCOLS: creare un layout a due colonne in C#

Ti sei mai chiesto **come usare WRAPCOLS** quando hai bisogno di una visualizzazione rapida a due colonne all'interno di un foglio di lavoro in stile Excel? Non sei solo. Molti sviluppatori si trovano in difficoltà quando cercano di suddividere un elenco generato in colonne ordinate senza scrivere un ciclo per ogni cella. La buona notizia? Con la funzione `WRAPCOLS` puoi inserire una singola formula in `A1` e lasciare che Excel (o un motore compatibile) faccia il lavoro pesante.

In questo tutorial vedremo **come aggiungere una formula** che crea un **layout a due colonne**, ti mostreremo **come creare colonne** dinamicamente e persino **generare array di sequenza** al volo. Alla fine avrai uno snippet C# completamente eseguibile che potrai incollare nel tuo progetto, eseguire e vedere immediatamente apparire un blocco ordinato a due colonne.

## Cosa imparerai

- Lo scopo di `WRAPCOLS` e perché è un'alternativa migliore al looping manuale.  
- Come **aggiungere una formula** a una cella del foglio di lavoro usando C#.  
- Come generare un array di sequenza con `SEQUENCE` e inserirlo in `WRAPCOLS`.  
- Suggerimenti per ricalcolare il foglio in modo che la formula venga risolta immediatamente.  
- Gestione dei casi limite (ad es., fogli vuoti, conteggi di colonne personalizzati).

Non sono necessarie librerie esterne oltre a un pacchetto standard per l'elaborazione di Excel – useremo **ClosedXML** per la sua API semplice, ma i concetti si applicano anche a EPPlus, SpreadsheetGear o persino a Google Sheets tramite la sua API.

## Prerequisiti

- .NET 6.0 o successivo (il codice si compila su .NET Core e .NET Framework).  
- Un riferimento a **ClosedXML** (`dotnet add package ClosedXML`).  
- Conoscenze di base di C# – dovresti sentirti a tuo agio con le istruzioni `using` e l'inizializzazione di oggetti.  

Se hai già un workbook aperto, puoi saltare la parte di creazione del file e passare direttamente alla sezione della formula.

## Passo 1: Configurare il foglio di lavoro (Come creare colonne)

Per prima cosa abbiamo bisogno di un oggetto `Worksheet` con cui lavorare. In ClosedXML lo ottieni da un `XLWorkbook`. Lo snippet qui sotto crea un nuovo workbook, aggiunge un foglio chiamato *Demo* e ottiene un riferimento chiamato `worksheet` per chiarezza.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Perché rinominare?**  
> Mantenere il nome della variabile breve (`worksheet`) rende il codice successivo più leggibile, soprattutto quando concatenavi più operazioni. Inoltre rispecchia lo stile di denominazione che trovi nella maggior parte della documentazione, riducendo il carico cognitivo.

## Passo 2: Scrivere la formula (Come aggiungere formula + generare array di sequenza)

Ora arriva la riga magica. Inseriremo una formula nella cella **A1** che fa due cose:

1. **Generare un array di sequenza** di sei numeri (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Raggruppare quei numeri in due colonne** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Cosa sta succedendo?**  
> `SEQUENCE(6)` crea un array verticale `{1;2;3;4;5;6}`. `WRAPCOLS` poi prende quell'array e lo “avvolge” nel numero specificato di colonne—in questo caso **2**. Il risultato è un blocco di 3 righe × 2 colonne che appare così:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Se cambi il secondo argomento a **3**, otterrai invece un layout a tre colonne. Questo è il nocciolo di **come creare colonne** al volo senza cicli manuali.

## Passo 3: Ricalcolare il foglio di lavoro (Assicurarsi che la formula venga valutata)

ClosedXML non valuterà automaticamente le formule quando le scrivi. Devi chiamare `Calculate()` sul workbook (o sul foglio di lavoro specifico) per forzare la valutazione.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Consiglio professionale:** Se lavori con workbook di grandi dimensioni, chiama `Calculate()` solo sui fogli che sono effettivamente cambiati. Questo salva memoria e velocizza l'elaborazione.

Quando apri `WrapColsDemo.xlsx` vedrai il layout a due colonne ordinatamente popolato in **A1:B3**. Non è stato necessario alcun codice aggiuntivo per iterare righe o colonne – `WRAPCOLS` ha gestito tutto.

## Passo 4: Verificare l'output (Cosa aspettarsi)

Dopo aver eseguito il programma, apri il file generato. Dovresti vedere:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Se i numeri appaiono verticalmente (cioè tutti nella colonna A), verifica di aver chiamato `worksheet.Calculate()` **dopo** aver impostato la formula. Alcuni motori richiedono anche `workbook.Calculate()`; lo snippet sopra funziona con il valutatore integrato di ClosedXML.

## Varianti comuni e casi limite

### Cambiare il numero di colonne

Per **creare un layout a due colonne** con un diverso conteggio di righe, basta regolare la dimensione di `SEQUENCE` o il secondo argomento di `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Questo produce un blocco di 4 righe × 3 colonne (12 numeri suddivisi in tre colonne).

### Usare un conteggio di colonne dinamico

Se il conteggio delle colonne proviene da una variabile, incorporalo con l'interpolazione di stringa:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Ora hai **come aggiungere una formula** che si adatta a runtime.

### Fogli di lavoro vuoti

Se il foglio di lavoro è vuoto, `Calculate()` funziona comunque – la formula popolerà le celle a partire da A1. Tuttavia, se in seguito elimini righe/colonne che intersecano l'intervallo di output, potresti vedere errori `#REF!`. Per evitarlo, cancella prima l'intervallo di destinazione:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Compatibilità

`WRAPCOLS` e `SEQUENCE` fanno parte delle funzioni **Dynamic Array** di Excel, introdotte in Office 365. Se punti a versioni più vecchie di Excel, le funzioni non esisteranno e dovrai usare un ciclo manuale. Il valutatore di ClosedXML rispecchia il comportamento più recente di Excel, quindi è sicuro per ambienti moderni.

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Risultato atteso:** Aprendo *WrapColsDemo.xlsx* si vede un layout ordinato a due colonne con i numeri da 1 a 6 disposti come descritto in precedenza.

## Conclusione

Abbiamo coperto **come usare WRAPCOLS** per **creare un layout a due colonne**, dimostrato **come aggiungere una formula** programmaticamente e visto come `SEQUENCE` ti consente di **generare array di sequenza** senza un ciclo. Sfruttando le funzioni di array dinamici di Excel da C#, puoi mantenere il tuo codice conciso, leggibile e manutenibile.

Successivamente, potresti esplorare:

- **Creare conteggi di righe dinamici** con `ROWS` o `COUNTA`.  
- **Stilizzare l'output** (bordi, formati numerici) usando l'API di styling di ClosedXML.  
- **Esportare in CSV** dopo aver costruito il layout, per l'elaborazione a valle.

Provalo, modifica il conteggio delle colonne e scopri quanto rapidamente puoi prototipare fogli di calcolo complessi. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}