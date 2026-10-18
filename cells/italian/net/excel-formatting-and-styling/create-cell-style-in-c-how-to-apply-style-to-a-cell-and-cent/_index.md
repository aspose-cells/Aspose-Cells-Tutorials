---
category: general
date: 2026-02-21
description: Crea rapidamente lo stile di cella in C#. Scopri come applicare lo stile
  a una cella, centrare il testo nella cella, impostare l'allineamento della cella
  e padroneggiare la formattazione delle celle.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: it
og_description: Crea uno stile per le celle in C# e impara come applicare lo stile
  a una cella, centrare il testo nella cella e impostare l'allineamento della cella
  con una guida chiara, passo dopo passo.
og_title: Crea stile di cella in C# – Applica lo stile a una cella e centra il testo
tags:
- C#
- Aspose.Cells
- Excel automation
title: Creare stile di cella in C# – Come applicare lo stile a una cella e centrare
  il testo
url: /it/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea stile di cella in C# – Guida completa all'applicazione di stili e allineamento del testo al centro

Hai mai dovuto **create cell style** in un foglio di lavoro Excel ma non sapevi da dove cominciare? Non sei solo. In molti progetti di automazione, la capacità di **apply style to cell** oggetti è la differenza tra un foglio di calcolo banale e un report curato.  

In questo tutorial percorreremo un esempio completo e eseguibile che ti mostra **how to center text** all'interno di una cella, impostare l'allineamento e aggiungere un bordo sottile—tutto in poche righe di C#. Alla fine saprai esattamente perché ogni elemento è importante e come personalizzarlo per i tuoi scenari.

## Cosa imparerai

- Una chiara comprensione del workflow **create cell style** usando Aspose.Cells (o qualsiasi libreria simile).
- Il codice esatto da copiare‑incollare in un'app console per **apply style to cell**.
- Approfondimenti su **center text in cell**, **set cell alignment** e la gestione di casi particolari come celle unite o formati numerici personalizzati.
- Consigli per estendere lo stile—font diversi, colori di sfondo o formattazione condizionale.

> **Prerequisito:** Visual Studio 2022 (o qualsiasi IDE C#) e il pacchetto NuGet Aspose.Cells for .NET. Non sono richieste altre dipendenze.

---

## Passo 1: Configura il tuo progetto e importa i namespace

Prima di poter **create cell style**, ci serve un progetto che faccia riferimento alla libreria Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Perché è importante:* L'importazione di `Aspose.Cells` ci dà accesso alle classi `Workbook`, `Worksheet`, `Style` e `Border`. Se usi una libreria diversa (ad es., EPPlus), i nomi delle classi cambiano ma il concetto rimane lo stesso.

---

## Passo 2: Crea una cartella di lavoro e ottieni la prima cella

Ora **create cell style** ottenendo prima un riferimento alla cella che vogliamo formattare.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Nota che abbiamo usato `Cell` invece del generico `var`—la tipizzazione esplicita rende il codice più chiaro per i principianti. La chiamata a `PutValue` scrive una stringa così possiamo vedere l'effetto dello stile in seguito.

---

## Passo 3: Definisci lo stile – Centra il testo, aggiungi un bordo sottile

Ecco il cuore dell'operazione **create cell style**. Imposteremo l'allineamento orizzontale, un bordo sottile e qualche dettaglio opzionale.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Perché lo facciamo:*  
- **HorizontalAlignment** e **VerticalAlignment** insieme rispondono alla domanda “**how to center text** in a cell?”.  
- Aggiungere tutti e quattro i bordi garantisce che la cella assomigli a un'etichetta incorniciata, utile per intestazioni.  
- Il colore di sfondo non è obbligatorio, ma dimostra come si possa estendere lo stile in seguito.

---

## Passo 4: Applica lo stile definito alla cella selezionata

Ora che lo stile esiste, **apply style to cell** con una singola chiamata di metodo.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

È tutto—Aspose.Cells si occupa di copiare lo stile nella collezione di stili interna della cella. Se ti serve la stessa formattazione su un intervallo, puoi usare `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Passo 5: Salva la cartella di lavoro e verifica il risultato

Un rapido salvataggio ti permette di aprire il file in Excel e confermare che il testo sia davvero centrato e che il bordo sia visibile.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Output previsto:* Quando apri **StyledCell.xlsx**, la cella **A1** contiene “Hello, styled world!” centrata sia orizzontalmente sia verticalmente, circondata da un bordo grigio sottile e impostata su uno sfondo grigio chiaro.

---

## Varianti comuni e casi particolari

### 1. Centrare il testo in un'area unita

Se unisci le celle **A1:C1** e vuoi comunque che il testo sia centrato, devi applicare lo stile alla cella in alto a sinistra **dopo** aver effettuato l'unione:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Utilizzare un formato numerico

A volte è necessario **set cell alignment** *e* visualizzare numeri con un formato specifico:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

L'allineamento rimane centrato mentre il numero appare come `12,345.68`.

### 3. Riutilizzare gli stili in modo efficiente

Creare un nuovo `Style` per ogni cella può penalizzare le prestazioni. Invece, crea un unico oggetto stile e riutilizzalo su molte celle o intervalli. La classe `StyleFlag` ti consente di applicare solo le parti di cui ti interessa, risparmiando memoria.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Consigli professionali e trappole da evitare

- **Non dimenticare l'allineamento verticale** – centrare solo orizzontalmente spesso risulta poco armonioso, soprattutto con righe alte.
- **Tipi di bordo**: `CellBorderType.Thin` funziona per la maggior parte dei report, ma puoi passare a `Medium` o `Dashed` per creare gerarchie visive.
- **Gestione dei colori**: Quando lavori con .NET Core, usa `System.Drawing.Color` dal pacchetto `System.Drawing.Common`; altrimenti otterrai un errore a runtime.
- **Formato di salvataggio**: Se ti serve compatibilità con versioni più vecchie di Excel, cambia `SaveFormat.Xlsx` in `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt text: screenshot che mostra una cella con testo centrato e bordo sottile creati dal tutorial su create cell style.*

---

## Esempio completo funzionante (pronto per il copy‑paste)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Esegui questo programma, apri **StyledCell.xlsx** e vedrai esattamente il risultato descritto prima. Sentiti libero di modificare il testo, lo stile del bordo o il colore di sfondo per adattarlo al tuo brand.

---

## Conclusione

Abbiamo appena **created cell style** da zero, **applied style to cell**, e dimostrato **how to center text** sia orizzontalmente sia verticalmente. Padroneggiando questi blocchi di costruzione ora puoi formattare intestazioni, evidenziare totali o creare interi modelli di report senza mai uscire da C#.  

Se sei curioso dei prossimi passi, prova a:

- **Applicare lo stesso stile a un'intera riga** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Aggiungere formattazione condizionale** per cambiare lo sfondo in base ai valori delle celle.
- **Esportare in PDF** mantenendo lo stile.

Ricorda, lo styling è importante tanto per la leggibilità quanto per l'estetica. Sperimenta, itera, e presto i tuoi fogli di calcolo avranno un aspetto professionale quanto il tuo codice.

*Buon coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}