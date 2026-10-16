---
category: general
date: 2026-10-10
description: Crea una cartella di lavoro Excel in C# e imposta il valore della cella
  con una data dell’era giapponese, quindi applica un formato personalizzato e leggi
  la cella data usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: it
lastmod: 2026-10-10
og_description: Crea una cartella di lavoro Excel in C# e analizza le date dell’era
  giapponese. Impara a impostare il valore di una cella, applicare un formato personalizzato
  e leggere una cella data con Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Crea una cartella di lavoro Excel in C# – guida completa all'analisi delle
  date
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Come creare una cartella di lavoro Excel e analizzare le date giapponesi in
  C#
url: /it/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una cartella di lavoro Excel e analizzare le date giapponesi in C#

Se hai bisogno di **create Excel workbook** da zero, questa guida ti mostra esattamente come. Imparerai a **set cell value** con una stringa di data dell'era giapponese, **apply custom format** che comprende l'era, e infine **read date cell** per ottenere un .NET `DateTime`. L'esempio completo funziona con l'ultima versione di Aspose.Cells per .NET, così puoi copiare‑incollare il codice in qualsiasi progetto C#.

Lavorare con date che includono le ere giapponesi può essere complicato perché il parser predefinito di Excel non riconosce i simboli dell'era. Utilizzando un formato numerico personalizzato (`[ja-JP-Era]`) si indica a Excel come interpretare la stringa, consentendo un'affidabile **excel date parsing**. I passaggi seguenti coprono l'intero flusso di lavoro, dalla creazione della cartella di lavoro all'estrazione della data.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+)
- Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`)
- Familiarità di base con C# e Visual Studio o qualsiasi IDE a tua scelta

## Passo 1: Create Excel workbook and add a worksheet

La prima operazione è **create Excel workbook** in memoria. Aspose.Cells crea automaticamente un foglio di lavoro predefinito, ma è possibile aggiungerne altri se necessario.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

La creazione della cartella di lavoro alloca le strutture interne che in seguito contengono celle, stili e formule. Nessun file viene scritto a questo punto, il che mantiene l'operazione veloce e testabile.

## Passo 2: Set cell value with a Japanese era date string

Successivamente, **set cell value** alla rappresentazione dell'era giapponese `"R5-04-01"` (Reiwa 5, 1 aprile). La stringa segue il modello `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

L'utilizzo di `PutValue` memorizza il testo grezzo. Excel lo tratterà come una stringa finché un formato numerico non gli indica il contrario. Questo approccio funziona per qualsiasi rappresentazione di calendario personalizzato, non solo per le ere giapponesi.

## Passo 3: Apply a custom number format that understands the Japanese era

Ora **apply custom format** affinché Excel possa tradurre la stringa dell'era in una data seriale reale. Il formato `[ja-JP-Era]yyyy/MM/dd` indica al motore di interpretare il carattere dell'era iniziale (`R` per Reiwa) e calcolare la data gregoriana.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Il formato personalizzato viene memorizzato nell'oggetto style della cella. Aspose.Cells rispetta questo formato sia durante il rendering sia durante la conversione del valore, consentendo un'affidabile **excel date parsing** più avanti nella pipeline.

## Passo 4: Retrieve the parsed DateTime value from the cell

Infine, **read date cell** per ottenere un .NET `DateTime`. La proprietà `DateTimeValue` restituisce il valore convertito in base al formato personalizzato applicato in precedenza.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Quando il programma viene eseguito, la console stampa:

```
Parsed Gregorian date: 2023-04-01
```

L'output conferma che la stringa dell'era giapponese `"R5-04-01"` è stata interpretata correttamente come 1 aprile 2023.

## Esempio completo e eseguibile

Unendo i pezzi si ottiene un programma autonomo che puoi compilare ed eseguire immediatamente.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Eseguendo il programma si crea `JapaneseEraDate.xlsx` con la cella A1 che mostra `2023/04/01` mentre la console visualizza la stessa data gregoriana. Il file può essere aperto in Excel per vedere il valore formattato.

## Perché questo approccio funziona

- **create excel workbook** – L'istanziazione di `Workbook` costruisce l'intera struttura del file Excel in memoria senza toccare il disco.
- **set cell value** – `PutValue` memorizza il testo grezzo, necessario prima di applicare un formato specifico per la cultura.
- **apply custom format** – Il token `[ja-JP-Era]` colma il divario tra la notazione dell'era e il sistema interno di date seriali di Excel.
- **read date cell** – `DateTimeValue` utilizza automaticamente lo stile della cella per eseguire la conversione, fornendoti un `DateTime` nativo.
- **excel date parsing** – Delegando l'analisi allo stile della cella, eviti la manipolazione manuale delle stringhe, riducendo i bug e migliorando il supporto locale.

## Casi limite e consigli pratici

- **Different eras** – Usa `S` per Showa, `H` per Heisei, `R` per Reiwa. La stessa stringa di formato funziona per tutte le ere.
- **Invalid strings** – Se la cella contiene una data dell'era malformata, `DateTimeValue` restituisce `DateTime.MinValue`. Controlla `dateCell.IsDate` prima di leggere.
- **Multiple cells** – Applica il formato personalizzato a un'intera area (`range.ApplyStyle(style)`) quando devi analizzare molte date.
- **Performance** – Impostare lo stile una volta per colonna è più veloce rispetto a cella per cella per fogli di grandi dimensioni.
- **Saving options** – Aspose.Cells può esportare in XLSX, XLS, CSV o PDF. Scegli il formato che corrisponde all'elaborazione a valle.

## Domande frequenti

**Posso usare la cultura .NET integrata invece di un formato personalizzato?**  
La classe .NET `CultureInfo` non comprende i simboli delle ere giapponesi nello stesso modo di Excel. Utilizzare un formato numerico personalizzato è il metodo più affidabile per **excel date parsing** delle stringhe di era.

**Cosa succede se devo scrivere nuovamente la data in Excel nel formato era?**  
Imposta il valore della cella su un `DateTime` e applica lo stesso formato personalizzato. Excel visualizzerà automaticamente l'era.

**Funziona su versioni più vecchie di Excel?**  
Il token `[ja-JP-Era]` è supportato da Excel 2010 e versioni successive. Aspose.Cells emula il comportamento, quindi la cartella di lavoro viene visualizzata correttamente anche quando aperta in versioni più vecchie di Excel che non supportano nativamente le ere.

## Conclusione

Ora sai come **create Excel workbook**, **set cell value** con una stringa dell'era giapponese, **apply custom format** e **read date cell** per ottenere un `DateTime`. Questo modello fornisce un **excel date parsing** robusto senza gestire manualmente le stringhe, rendendo il tuo codice di automazione C# sia conciso sia affidabile.

Successivamente, esplora argomenti correlati come **formatting multiple date columns**, **working with other cultural calendars**, o **exporting the workbook to PDF**. Ogni estensione si basa sugli stessi principi trattati qui, così potrai adattare la soluzione a un'ampia gamma di scenari di localizzazione. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea cartella di lavoro Excel in C# – Applica formato numerico personalizzato](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Crea cartella di lavoro Excel con formato personalizzato – Guida C#](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Automazione Excel con Aspose.Cells .NET: Crea cartella di lavoro e imposta collegamenti esterni](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}