---
category: general
date: 2026-10-13
description: Scopri come salvare Excel come TXT con Aspose.Cells. Questa guida copre
  l'esportazione di Excel in TXT, la scrittura di valori in una cella e l'impostazione
  delle cifre significative in pochi passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: it
lastmod: 2026-10-13
og_description: Salva Excel come TXT con Aspose.Cells. Scopri come esportare Excel
  in TXT, scrivere un valore in una cella e impostare le cifre significative in poche
  righe di codice C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Salva Excel come TXT – guida passo‑passo per gli sviluppatori .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Come salvare Excel come TXT usando Aspose.Cells in C#
url: /it/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come salvare Excel come TXT usando Aspose.Cells in C#

Se hai bisogno di **salvare Excel come TXT** rapidamente, questo tutorial mostra l'intero processo in meno di cinque minuti. Vedrai come esportare Excel in TXT, scrivere un valore in una cella e impostare le cifre significative in modo che il file di testo contenga esattamente i dati che ti aspetti.

Esportare un foglio di calcolo come TXT è utile quando i sistemi a valle accettano solo input di testo semplice, quando è necessario generare log o quando si desidera un dump leggibile da un umano dei calcoli. L'esempio seguente funziona con Aspose.Cells v25.10 o versioni successive e gira su qualsiasi runtime .NET 6+.

## Prerequisiti

* Una copia con licenza di **Aspose.Cells for .NET** (la versione di prova gratuita è valida per i test).
* .NET 6 SDK o versioni successive installate.
* Un IDE come Visual Studio 2022, VS Code o Rider.
* Conoscenze di base di C# — non è necessaria un'esperienza avanzata di automazione di Excel.

Puoi installare il pacchetto NuGet di Aspose.Cells con:

```bash
dotnet add package Aspose.Cells
```

## Passo 1: Creare una cartella di lavoro e accedere al suo primo foglio di lavoro (salvare excel come txt)

La prima cosa da fare quando vuoi **salvare Excel come TXT** è creare un oggetto `Workbook`. Questo oggetto rappresenta l'intero file Excel in memoria.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Perché è importante:** La classe `Workbook` è il punto di ingresso per tutte le operazioni sui fogli di calcolo. Iniziando con una cartella di lavoro nuova eviti qualsiasi formattazione nascosta che potrebbe influire sull'output di testo semplice.

## Passo 2: Scrivere un numero ad alta precisione in una cella (scrivere valore nella cella)

Ora devi **scrivere valore nella cella** A1. Il metodo `PutValue` rileva automaticamente il tipo di dato e lo memorizza come valore numerico.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Suggerimento:** Se in seguito devi scrivere stringhe, date o formule, lo stesso metodo `PutValue` funziona — basta passare il tipo .NET appropriato.

## Passo 3: Configurare le opzioni di esportazione per mantenere solo la precisione necessaria (impostare le cifre significative)

Durante l'esportazione in un file TXT, spesso si desidera limitare il numero di cifre per mantenere il file di dimensioni ridotte o per corrispondere a una specifica a valle. La classe `TxtSaveOptions` fornisce una proprietà `SignificantDigits` a questo scopo.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Perché impostare le cifre significative:** Senza questa impostazione, Aspose.Cells scrive il valore a doppia precisione completo, il che può produrre stringhe lunghe come `12345.6789012345`. Impostando `SignificantDigits = 6` si riduce l'output a `12345.7`, corrispondente alla maggior parte dei requisiti di reportistica.

## Passo 4: Esportare la cartella di lavoro come file TXT (esportare excel in txt)

Infine, **esporti Excel in TXT** chiamando `Workbook.Save` con le opzioni configurate in precedenza.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Quando il codice termina, `LimitedDigits.txt` contiene:

```
12345.7
```

> **Verifica del risultato:** Apri il file in qualsiasi editor di testo (Notepad, VS Code) per confermare che siano presenti solo sei cifre significative e che non compaiano virgole o delimitatori di tabulazione aggiuntivi.

## Esempio completo, eseguibile

Di seguito è riportata un'applicazione console autonoma che puoi copiare, incollare ed eseguire immediatamente.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Spiegazione di ciascun blocco**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | Importa lo spazio dei nomi Aspose.Cells necessario per `Workbook`, `Worksheet` e `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Istanzia una cartella di lavoro Excel vuota in memoria. |
| `worksheet.Cells["A1"].PutValue(...);` | **scrivi valore nella cella** A1 con un numero a doppia precisione. |
| `TxtSaveOptions` | Configura il comportamento **imposta cifre significative** per l'esportazione TXT. |
| `workbook.Save(..., txtOptions);` | Esegue l'operazione **esporta excel in txt**, creando il file di testo semplice. |

## Casi limite e suggerimenti aggiuntivi

| Scenario | How to handle |
|----------|---------------|
| **Fogli di lavoro grandi** (molte righe/colonne) | Usa `txtOptions.Encoding = Encoding.UTF8` se hai bisogno del supporto Unicode, e considera lo streaming del file con `Workbook.Save(Stream, txtOptions)` per evitare un elevato utilizzo di memoria. |
| **Delimitatori personalizzati** (valori separati da virgola) | `TxtSaveOptions` espone anche `Separator` — impostalo a `','` per produrre un output in stile CSV mantenendo comunque il formato TXT. |
| **Mantenere le formule** | Imposta `txtOptions.ExportFormulas = true` per scrivere il testo della formula invece del valore calcolato. |
| **Separatori decimali specifici per locale** | Regola `txtOptions.DecimalSeparator` a `','` per le impostazioni locali europee. |
| **Fogli di lavoro multipli** | Itera su `workbook.Worksheets` e chiama `Save` per ciascuno, aggiungendo il nome del foglio al nome del file. |

## Domande frequenti

**D: `SignificantDigits` arrotonda o tronca?**  
R: Arrotonda al valore più vicino in base al numero specificato di cifre significative, garantendo che l'output sia matematicamente accurato a quella precisione.

**D: Posso esportare direttamente in uno stream di memoria?**  
R: Sì. Sostituisci il percorso del file con un'istanza `MemoryStream`: `workbook.Save(stream, txtOptions);`. Questo è utile per le API web che devono restituire il contenuto TXT senza toccare il file system.

**D: E se devo mantenere la formattazione originale (ad esempio le date)?**  
R: Usa `txtOptions.ExportFormattedValues = true`. Questo costringe Aspose.Cells a scrivere il testo visualizzato nella cella anziché il valore grezzo.

## Conclusione

Ora sai come **salvare Excel come TXT** con pieno controllo su precisione, formattazione e posizione di output. Seguendo i quattro passaggi — creare una cartella di lavoro, **scrivere valore nella cella**, **impostare le cifre significative** e **esportare Excel in TXT** — puoi integrare l'esportazione di testo semplice in qualsiasi applicazione .NET.

Successivamente, esplora argomenti correlati come **esportare foglio di calcolo come TXT con delimitatori personalizzati**, **convertire Excel in CSV**, o **usare Aspose.Cells per generare report JSON**. Ognuno di questi si basa sugli stessi concetti fondamentali mostrati qui, fornendoti un toolkit versatile per lo scambio di dati tra piattaforme.

Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Salva Excel come testo – Guida completa C# per esportare Excel in TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Crea nuova cartella di lavoro ed esporta Excel in TXT con precisione](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Crea nuova cartella di lavoro – Esporta Excel in TXT con precisione completa](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}