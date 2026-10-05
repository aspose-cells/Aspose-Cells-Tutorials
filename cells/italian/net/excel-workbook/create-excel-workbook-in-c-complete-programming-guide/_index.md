---
category: general
date: 2026-06-05
description: Crea rapidamente una cartella di lavoro Excel in C# e impara come impostare
  il formato numerico delle celle, esportare una cella Excel e convertire il valore
  della cella in stringa con precisione a due decimali.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: it
og_description: Crea una cartella di lavoro Excel in C# e padroneggia l'impostazione
  del formato numerico delle celle, l'esportazione della cella Excel come stringa
  e la formattazione dei numeri con due decimali.
og_title: Crea una cartella di lavoro Excel in C# – Guida completa passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Crea cartella di lavoro Excel in C# – Guida completa alla programmazione
url: /it/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un Excel Workbook in C# – Guida completa alla programmazione

Ti sei mai chiesto come **create Excel workbook** in C# senza lottare con l'interoperabilità COM o trucchi CSV ingarbugliati? Non sei solo. Molti sviluppatori hanno bisogno di un modo pulito, nativo .NET, per generare un file .xlsx, inserire un numero in una cella e poi esportare quel valore come una stringa formattata correttamente.  

In questo tutorial ti guideremo passo passo—partendo da un workbook vuoto, impostando il formato numerico della cella, formattando il numero con due decimali, e infine imparando **how to export Excel cell** come stringa. Alla fine vedrai anche come **convert cell value to string** senza perdere precisione.

> **Pro tip:** Il metodo qui sotto utilizza la libreria **Aspose.Cells for .NET**, che è un'API collaudata e di livello commerciale. Se cerchi un'alternativa gratuita, EPPlus o ClosedXML funzionano in modo simile, ma gli snippet di codice saranno leggermente diversi.

## Prerequisiti

- .NET 6.0 SDK (o qualsiasi versione recente di .NET) installato.
- Visual Studio 2022 o VS Code con l'estensione C#.
- Il pacchetto NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Non sono necessarie altre dipendenze—tutto il resto è incluso nella libreria.

## Passo 1: Installa Aspose.Cells e configura il progetto

Apri il tuo terminale (o la Console di Gestione Pacchetti) ed esegui:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Questo crea una nuova app console chiamata `ExcelDemo` e importa l'assembly `Aspose.Cells`.  

Perché questo passo è importante: senza la libreria, non puoi **create Excel workbook** oggetti o manipolare le celle in modo type‑safe.

## Passo 2: Crea il Workbook e ottieni il primo Worksheet

Ora apri `Program.cs` e sostituisci il codice predefinito con lo snippet qui sotto. Mostra la prima cosa da fare quando **create Excel workbook**—istanziare la classe `Workbook` e ottenere un riferimento al foglio predefinito.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Perché?** L'oggetto `Workbook` è la rappresentazione in memoria di un file Excel. Per impostazione predefinita contiene un worksheet, al quale accediamo tramite l'indice basato su zero.

## Passo 3: Inserisci un valore numerico in una cella specifica

Puntiamo alla riga 5, colonna 2 (indici basati su zero) e inseriamo un numero decimale. Questo dimostra **format number with two decimals** più avanti.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

Il metodo `PutValue` memorizza il double grezzo. A questo punto, Excel mostrerebbe la precisione completa a meno che non applichiamo un formato.

## Passo 4: Imposta il formato numerico della cella (due cifre decimali)

Qui è dove **set cell number format**. Useremo l'oggetto `Style` per definire un formato numerico personalizzato `"0.00"`—esattamente due decimali.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Perché usare uno stile invece della conversione in stringa? Mantenere la cella come tipo numerico preserva la sua natura calcolabile (puoi ancora sommare, fare medie, ecc.) mostrando esattamente ciò di cui hai bisogno.

## Passo 5: Esporta il valore della cella come stringa formattata

A volte hai bisogno del valore **how to export excel cell** come testo semplice—magari per scriverlo in un file di log o inviarlo tramite una web API. Aspose.Cells ti permette di allegare opzioni di esportazione a una cella, indicando alla libreria di renderizzare il valore come stringa usando lo stesso formato numerico.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

Ora, quando leggiamo il valore della cella tramite l'API di esportazione, riceveremo una stringa che rispetta già la regola dei due decimali.

## Passo 6: Recupera la stringa formattata (Convert Cell Value to String)

Eseguiamo effettivamente l'esportazione e vediamo il risultato. Il metodo `ExportString` restituisce il contenuto della cella come stringa, applicando eventuali `ExportTableOptions` che abbiamo allegato.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Quando esegui il programma, la console stampa:

```
Formatted cell value: 12345.68
```

Nota l'arrotondamento da `12345.6789` a `12345.68`—questo è l'effetto di **format number with two decimals**.

## Passo 7: (Opzionale) Salva il Workbook su disco

Se vuoi vedere il risultato anche in un file `.xlsx` reale, chiama semplicemente `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Aprendo `DemoWorkbook.xlsx` vedrai lo stesso numero nella cella **C6**, formattato con due cifre decimali.

## Casi limite e domande comuni

### E se la cella ha già uno stile?

Il metodo `GetStyle` restituisce una copia dello stile esistente, quindi qualsiasi formattazione precedente (font, colore, ecc.) viene mantenuta. Sovrascrivi solo la proprietà `Custom`, lasciando intatto il resto.

### Come influisce la cultura sul separatore decimale?

Aspose.Cells rispetta il `CultureInfo` del thread. Se ti serve una virgola invece di un punto, imposta:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Lo stesso formato `"0.00"` ora renderizzerà `12 345,68`.

### Posso esportare un intervallo di celle in una volta?

Sì—usa `Worksheet.ExportDataTable` o `Worksheet.ExportString` con un indirizzo di intervallo. Le `ExportTableOptions` definite per una singola cella possono essere riutilizzate per l'intero intervallo.

### E se non voglio che il valore sia arrotondato ma troncato?

Cambia il formato personalizzato in `"0.00"` con una modalità di arrotondamento, o tronca manualmente prima di inserire il valore:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Output atteso della console**

```
Formatted cell value: 12345.68
```

Apri `DemoWorkbook.xlsx` → vai alla cella **C6** → vedrai lo stesso numero con due cifre decimali.

## Conclusione

Abbiamo appena coperto tutto ciò di cui hai bisogno per **create Excel workbook** in C#, **set cell number format**, **format number with two decimals**, capire **how to export Excel cell** dati, e **convert cell value to string** per l'elaborazione successiva.  

I punti chiave sono:

1. Usa `Workbook` e `Worksheet` per creare un file Excel in memoria.  
2. Applica uno stile personalizzato (`"0.00"`) per imporre la visualizzazione a due decimali.  
3. Allega `ExportTableOptions` a una cella quando ti serve una rappresentazione stringa che rispetti lo stesso formato.  

Da qui puoi sperimentare—aggiungere più celle, applicare formattazione condizionale o persino generare grafici. Se sei curioso di stilizzare i font o aggiungere formule, consulta la documentazione di Aspose.Cells su **cell styling** e **formula evaluation**.

Hai altre domande sull'automazione di Excel in C#? Lascia un commento, e buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Padroneggia le operazioni sui Workbook in Aspose.Cells .NET: carica file Excel e traccia i precedenti delle celle in modo efficace](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Padroneggia la formattazione delle celle Excel e la gestione dei Workbook con Aspose.Cells per .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Padroneggia Aspose.Cells per .NET: gestione avanzata di Workbook e celle Excel](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}