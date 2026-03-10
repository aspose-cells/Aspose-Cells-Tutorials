---
category: general
date: 2026-02-15
description: Crea un nuovo workbook in C# e copia una tabella pivot senza perdere
  la sua definizione. Scopri come copiare le righe, preservare la tabella pivot e
  duplicare la tabella pivot facilmente.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: it
og_description: Crea un nuovo workbook in C# e copia una tabella pivot preservandone
  la definizione. Guida passo‑passo per sviluppatori.
og_title: Crea una nuova cartella di lavoro in C# – Mantieni la tabella pivot
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crea una nuova cartella di lavoro in C# – Conserva la tabella pivot
url: /it/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un nuovo workbook in C# – Conserva la tabella pivot

Hai mai dovuto **creare un nuovo workbook** in C# che contenga una copia esatta di una tabella pivot da un altro file? Non sei il solo. In molti flussi di reporting la tabella pivot è il cuore dell'analisi, e perderne la definizione quando sposti i dati è un incubo.

La buona notizia? Con poche righe di codice Aspose.Cells puoi copiare le righe — inclusa la tabella pivot — in un workbook nuovo e mantenere tutto intatto. Di seguito vedrai **come copiare le righe**, **conservare le impostazioni della tabella pivot**, e persino **duplicare la tabella pivot** tra file senza rompere formule o cache.

## Cosa copre questo tutorial

In questa guida percorreremo:

1. Caricamento del workbook sorgente che contiene già una tabella pivot.  
2. **Creare un nuovo workbook** per la destinazione.  
3. Uso di `CopyRows` per trasferire l'intervallo che contiene la tabella pivot.  
4. Salvataggio del risultato garantendo che la tabella pivot rimanga funzionale.  

Nessuna documentazione esterna necessaria — solo il codice, il perché, e qualche suggerimento pratico da incollare direttamente nel tuo progetto.

> **Consiglio professionale:** Aspose.Cells funziona con .NET Core, .NET Framework e persino Xamarin, quindi lo stesso snippet gira ovunque tu ne abbia bisogno.

---

![Crea nuovo workbook con tabella pivot copiata](/images/create-new-workbook-pivot.png "crea nuovo workbook con tabella pivot copiata")

## Passo 1 – Crea un nuovo workbook e carica il file sorgente

La prima cosa che facciamo è **creare nuovi oggetti workbook**. Uno contiene i dati originali, l'altro riceverà l'intervallo copiato.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Perché è importante:*  
`Workbook` è il punto di ingresso per qualsiasi manipolazione di Excel in Aspose.Cells. Istanziando un workbook nuovo garantiamo una tela pulita — nessuno stile nascosto o foglio di lavoro estraneo che possa interferire in seguito.

## Passo 2 – Come copiare le righe includendo una tabella pivot

Ora arriva il nocciolo del problema: **come copiare le righe** che racchiudono la tabella pivot senza appiattirla. Il metodo `CopyRows` fa esattamente questo.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Alcune cose da notare:

* `startRow` e `totalRows` definiscono il blocco che contiene la tabella pivot.  
* Il metodo copia **sia** i dati grezzi sia la cache della pivot, così il workbook di destinazione sa come ricostruire la tabella pivot al volo.  
* Se la tua pivot inizia più in basso nel foglio, basta cambiare gli indici — non serve una chiamata API diversa.

> **Domanda comune:** *La pivot copiata perderà il riferimento ai dati di origine?*  
> No. Aspose.Cells incorpora la cache direttamente nel foglio di lavoro, quindi la pivot diventa autonoma nel nuovo file.

## Passo 3 – Conserva la tabella pivot durante il salvataggio della destinazione

Dopo che le righe sono state copiate, la tabella pivot vive nel workbook di destinazione esattamente come nel sorgente. Il salvataggio del file è semplice.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Quando apri `destination.xlsx` in Excel, vedrai la tabella pivot pronta per l'aggiornamento. Il comportamento **preserve pivot table** è automatico perché la cache è viaggiata con le righe.

### Verifica del risultato

Apri il file e:

1. Fai clic sulla tabella pivot.  
2. Nota che appare l'elenco dei campi — questo significa che la cache è intatta.  
3. Prova a fare un aggiornamento; i dati si aggiornano senza errori.

Se incontri un errore *#REF!*, ricontrolla che l'intervallo copiato includa le righe della cache nascoste (di solito subito dopo i dati visibili).

## Passo 4 – Duplica la tabella pivot in più workbook (opzionale)

A volte hai bisogno della stessa pivot in diversi report. Il pattern che abbiamo appena usato scala bene — basta ripetere la copia per ogni nuovo workbook.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Questo snippet **duplica la tabella pivot** tre volte con un unico ciclo. Regola l'array `targets` per adattarlo al tuo calendario di reporting.

### Casi limite da tenere presente

| Situazione | Cosa controllare | Correzione |
|------------|------------------|------------|
| La pivot usa una fonte dati esterna | La cache potrebbe fare riferimento a una connessione che non esiste sulla nuova macchina | Incorpora la fonte dati o ricrea la connessione nel workbook di destinazione |
| Pivot molto grande ( > 100 k righe ) | `CopyRows` può consumare molta memoria | Usa `CopyRows` a blocchi o considera `Copy` con `PasteOptions` per limitare l'uso di memoria |
| Il foglio ha righe/colonne nascoste | Le righe della cache nascoste potrebbero essere saltate se copi solo le righe visibili | Copia sempre l'intervallo esatto di righe che contiene la cache, non solo l'area visibile |

## Esempio completo funzionante

Mettendo tutto insieme, ecco un programma autonomo che puoi inserire in un'app console.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Esegui il programma, apri `destination.xlsx` e vedrai la stessa tabella pivot pronta per analizzare i tuoi dati. Nessuna ricreazione manuale necessaria.

---

## Conclusione

Abbiamo appena mostrato come **creare un nuovo workbook** in C# e **copiare la tabella pivot** mantenendo vive tutte le impostazioni. Usando `CopyRows` ottieni un modo affidabile per **conservare la tabella pivot**, rispondere alla domanda secolare “**come copiare le righe**” e persino **duplicare la tabella pivot** in più report con codice minimo.

Passi successivi? Prova a modificare l'intervallo copiato per includere grafici che fanno riferimento alla stessa pivot, o sperimenta con `PasteOptions` per mantenere la formattazione esattamente. Lo stesso pattern funziona per altri oggetti Aspose.Cells come tabelle e intervalli denominati, quindi sentiti libero di estenderlo.

Hai un caso particolare — magari una pivot che estrae dati da un DB esterno, o un workbook che vive nel cloud? Lascia un commento qui sotto, e lo affronteremo insieme. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}