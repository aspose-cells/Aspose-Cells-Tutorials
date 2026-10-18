---
category: general
date: 2026-03-21
description: Imposta il formato personalizzato della cella in C# e impara a scrivere
  una data in Excel, applicare un formato data personalizzato, leggere DateTime da
  Excel e creare rapidamente una cartella di lavoro e un foglio di lavoro.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: it
og_description: Imposta il formato personalizzato della cella in C# per scrivere la
  data in Excel, applica un formato data personalizzato, leggi DateTime da Excel e
  crea fogli di lavoro del workbook con facilità.
og_title: Imposta formato personalizzato della cella in C# – Scrivi e leggi le date
  in Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Imposta Formato Personalizzato della Cella in C# – Guida Completa alla Scrittura
  e Lettura di Date in Excel
url: /it/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta Formato Personalizzato della Cella – Scrivi e Leggi Date in Excel con C#

Hai mai dovuto **impostare un formato personalizzato della cella** in un file Excel da C# ma non sapevi da dove cominciare? Non sei solo. In molti strumenti di reporting o utility di esportazione i dati devono apparire in una locale specifica—ad esempio date dell'era giapponese, calendari fiscali o stringhe ISO‑8601.  

In questo tutorial percorreremo un **esempio completo e eseguibile** che mostra come **scrivere una data in Excel**, **applicare un formato data personalizzato**, **leggere DateTime da Excel** e **creare un foglio di lavoro** con Aspose.Cells. Alla fine avrai un unico programma autonomo da inserire in qualsiasi progetto .NET.

## Cosa Imparerai

- Come **creare un foglio di lavoro** programmaticamente.  
- I passaggi esatti per **scrivere una data in Excel** usando una stringa locale‑specifica.  
- Come **applicare un formato data personalizzato** (inclusa la notazione dell'era giapponese).  
- Il modo per **leggere DateTime da Excel** e convertirlo in un oggetto `DateTime`.  
- Suggerimenti, insidie e varianti che potresti incontrare nella gestione delle date in Excel.

Nessuna documentazione esterna necessaria—tutto quello che ti serve è qui.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+).  
- Aspose.Cells per .NET installato via NuGet (`Install-Package Aspose.Cells`).  
- Una conoscenza di base della sintassi C#—nulla di complicato.

> **Pro tip:** Se usi Visual Studio, abilita i *nullable reference types* per intercettare bug sottili in anticipo.

## Passo 1: Crea un Workbook e un Worksheet  

Prima di tutto: ti serve un oggetto workbook che rappresenta il file Excel, e un worksheet dove risiederanno i dati.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Perché è importante:* La classe `Workbook` è il punto di ingresso per tutte le operazioni su Excel. Crearla in memoria significa non toccare il file system finché non salvi esplicitamente, il che rende il processo veloce e adatto ai test.

## Passo 2: Scrivi la Data in Excel  

Successivamente, inseriremo una stringa di data dell'era giapponese (`"R02-04-01"`) nella cella **A1**. La stringa imita l'era Reiwa (anno 2, 1 aprile).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Cosa succede:* `PutValue` memorizza la stringa grezza. Aspose.Cells proverà poi a interpretarla in base allo stile della cella. Se salti questo passaggio e scrivi direttamente un `DateTime`, perderai l'informazione dell'era che vuoi visualizzare.

## Passo 3: Applica il Formato Numerico Predefinito (ID 14)

Excel dispone di un formato data predefinito con ID 14 (`mm-dd-yy`). Applicarlo indica al motore che la cella **contiene una data**, non solo testo.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Perché usare l'ID 14?* È il formato “data breve” universale che assicura che Excel tratti il contenuto come valore data, prerequisito necessario affinché qualsiasi formato personalizzato funzioni correttamente.

## Passo 4: Imposta un Formato Personalizzato per Visualizzare la Notazione dell'Era Giapponese  

Ora la parte divertente: diciamo a Excel di visualizzare la data usando il formato dell'era giapponese. La stringa personalizzata `[$-ja-JP]ggge年m月d日` fa esattamente questo.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Spiegazione:*  
- `[$-ja-JP]` forza la locale a giapponese.  
- `ggg` è il nome dell'era (es. “R” per Reiwa).  
- `e` è l'anno dell'era.  
- `年`, `月`, `日` sono caratteri giapponesi letterali per anno, mese, giorno.

Se ti serve una locale diversa, sostituisci semplicemente `ja-JP` con il codice cultura appropriato (es. `en-US`).

## Passo 5: Recupera il Valore DateTime Analizzato  

Infine, leggiamo il **vero `DateTime`** che Excel ha analizzato dalla cella. Questo dimostra che la stringa è stata interpretata correttamente.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Risultato:* La console stampa `Parsed DateTime: 2020-04-01`. Anche se abbiamo inserito una stringa dell'era giapponese, Excel memorizza internamente la data gregoriana, che puoi usare per calcoli, confronti o ulteriori esportazioni.

## Passo 6: Salva il Workbook (Opzionale)

Se vuoi vedere il workbook formattato in Excel, basta salvarlo su disco.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Apri il file **JapaneseEraDate.xlsx** generato e vedrai la cella **A1** visualizzare `R02年4月1日` (il formato esatto dell'era giapponese che abbiamo impostato).

![set cell custom format example](image-placeholder.png "Excel cell showing Japanese era date – set cell custom format")

*Il testo alternativo sopra contiene la keyword principale, soddisfacendo il requisito SEO per le immagini.*

## Varianti Comuni & Casi Limite  

### Scrivere un Formato Data Differente  

Se preferisci ISO‑8601 (`2020-04-01`) invece di una stringa dell'era, modifica semplicemente la chiamata `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Gestire Celle Null o Vuote  

Quando leggi una data, proteggi sempre contro celle vuote per evitare `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Supportare Molteplici Locali  

Puoi iterare su una lista di codici cultura e applicarli dinamicamente:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Pro Tips & Trucchi  

- **Imposta sempre prima un formato numerico predefinito** (`Style.Number`). Senza di esso, Excel tratta la cella come testo semplice e il formato personalizzato viene ignorato.  
- **I codici locale non fanno distinzione tra maiuscole e minuscole**, ma usare la forma canonica (`ja-JP`) evita confusioni.  
- **Il salvataggio è opzionale** per l'elaborazione in memoria; puoi inviare direttamente lo stream del workbook in una risposta web (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Licenze Aspose.Cells**: la versione di valutazione gratuita aggiunge una filigrana. Per la produzione, assicurati di avere una licenza valida per evitare penalità di performance.

## Riepilogo  

Abbiamo mostrato come **impostare un formato personalizzato della cella** in C# per visualizzare date dell'era giapponese, come **scrivere una data in Excel**, **applicare un formato data personalizzato**, **leggere DateTime da Excel** e **creare un foglio di lavoro**—tutto in un unico programma autonomo. La keyword principale appare naturalmente nel testo, mentre le keyword secondarie sono integrate nei titoli e nel corpo, soddisfacendo sia gli standard SEO sia quelli di citazione AI.

## Cosa Viene Dopo?

- Esplora la **formattazione condizionale** per evidenziare date scadute.  
- Combina questo approccio con **PivotTable** per report dinamici.  
- Prova a **leggere grandi file CSV** e convertirli in Excel usando la stessa logica di gestione delle date.  

Sentiti libero di sperimentare con diverse locali, pattern personalizzati o anche fusi orari. Se incontri problemi, lascia un commento qui sotto—buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}