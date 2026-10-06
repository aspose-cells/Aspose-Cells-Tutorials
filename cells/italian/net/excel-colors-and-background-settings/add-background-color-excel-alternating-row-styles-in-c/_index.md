---
category: general
date: 2026-04-07
description: Aggiungi colore di sfondo alle righe di Excel usando C#. Scopri come
  applicare colori alternati alle righe, impostare stili di sfondo solidi e importare
  una DataTable in Excel in un unico flusso di lavoro.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: it
og_description: Aggiungi colore di sfondo alle righe di Excel con C#. Questa guida
  mostra come applicare colori alternati alle righe, impostare uno sfondo solido e
  importare una datatable in Excel in modo efficiente.
og_title: Aggiungi colore di sfondo in Excel – Stili di riga alternati in C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Aggiungi colore di sfondo in Excel – Stili di riga alternati in C#
url: /it/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere colore di sfondo excel – Stili di riga alternati in C#

Hai mai avuto bisogno di **add background color excel** righe ma non sapevi come farlo senza mille righe di codice complicato? Non sei solo—la maggior parte degli sviluppatori si imbatte in questo ostacolo quando tenta per la prima volta di far apparire i propri fogli di calcolo più di un semplice dump grezzo di dati.  

La buona notizia? In pochi minuti puoi **apply alternating row colors**, impostare un **solid background** e persino **import datatable to excel** usando un modello pulito e riutilizzabile in C#.  

In questo tutorial percorreremo l’intero processo, dall’estrazione dei dati in una `DataTable` alla formattazione di ogni riga con un pattern a strisce giallo‑chiaro‑bianco. Non sono necessarie librerie esterne oltre a un solido pacchetto di gestione Excel (come **ClosedXML** o **GemBox.Spreadsheet**), e vedrai perché questo approccio è sia performante sia facile da mantenere.

## Cosa imparerai

- Come recuperare i dati e inserirli in un foglio di lavoro Excel.
- Come **style excel rows** con colori di sfondo alternati.
- Il meccanismo dietro **set solid background** usando l’oggetto `Style`.
- Come **import datatable to excel** mantenendo gli stili delle righe.
- Suggerimenti per gestire casi limite come tabelle vuote o schemi di colore personalizzati.

> **Pro tip:** Se stai già usando un oggetto workbook (`wb`) da una libreria che supporta la creazione di stili, puoi riutilizzare le stesse istanze `Style` su più fogli di lavoro—risparmiando memoria e mantenendo il codice ordinato.

---

## Passo 1: Recuperare i dati – Preparare il DataTable

Prima che possa avvenire qualsiasi formattazione abbiamo bisogno di una fonte di righe. Nella maggior parte degli scenari reali ciò proviene da un database, un'API o un file CSV. Per illustrazione, creeremo semplicemente un `DataTable` in memoria.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** Usare un `DataTable` ti fornisce un contenitore tabellare, consapevole dello schema, che la libreria Excel può importare direttamente, eliminando la necessità di scrivere cicli cella‑per‑cella.

---

## Passo 2: Creare gli stili di riga – **Apply alternating row colors**

Ora costruiremo un array di oggetti `Style`—uno per riga—così che ogni riga possa ricevere il proprio sfondo. Il pattern che useremo è un classico giallo chiaro per le righe pari e bianco per le righe dispari.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` ti fornisce un oggetto stile pulito che puoi modificare senza influenzare gli altri.  
- L'operatore ternario `(i % 2 == 0)` decide se la riga è pari (giallo chiaro) o dispari (bianco).  
- Impostare `Pattern = BackgroundType.Solid` è il passaggio cruciale che **set solid background**; senza di esso il colore verrebbe ignorato.

---

## Passo 3: Ottenere il foglio di lavoro di destinazione

La maggior parte delle librerie espone una collezione di fogli di lavoro. Lavoreremo con il primo, ma puoi puntare a qualsiasi indice o nome tu preferisca.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Se il workbook è appena creato, la libreria di solito crea un foglio predefinito per te. In caso contrario, puoi aggiungerne uno esplicitamente:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Passo 4: Importare il DataTable con gli stili di riga – **Import datatable to excel**

Con gli stili pronti, l'ultimo passaggio è inserire il `DataTable` nel foglio applicando lo stile corrispondente a ogni riga.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` indica al metodo di scrivere le intestazioni di colonna come prima riga.  
- `0, 0` segna l'angolo in alto a sinistra (A1) come punto di inserimento.  
- `rowStyles` allinea ogni `Style` con la riga dati corrispondente, fornendoci i colori alternati che abbiamo preparato in precedenza.

---

## Passo 5: Salvare il workbook

L'ultimo pezzo del puzzle è persistere il workbook su un file così da poterlo aprire in Excel e vedere il risultato.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Apri il file e dovresti vedere un foglio ordinatamente formattato:

- Riga di intestazione in grassetto (stile predefinito della libreria).  
- Riga 1, 3, 5… con uno sfondo bianco pulito.  
- Riga 2, 4, 6… con un riempimento giallo chiaro sottile, rendendo più facile la lettura.

### Anteprima dell'output previsto

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Le righe 2, 4, 6, … appaiono con uno sfondo giallo chiaro—esattamente l'effetto **apply alternating row colors** che ci siamo prefissati.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Il testo alternativo include la parola chiave principale per SEO.)*

---

## Gestione dei casi limite e variazioni

### DataTable vuoto

Se `dataTable.Rows.Count` è zero, l'array `rowStyles` sarà vuoto e `ImportDataTable` scriverà comunque la riga di intestazione (se `includeHeaders` è `true`). Non viene sollevata alcuna eccezione, ma potresti voler proteggere la generazione di un file quasi vuoto:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Schemi di colore personalizzati

Vuoi una striscia blu/grigio invece di giallo/bianco? Basta sostituire i valori `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Sentiti libero di prelevare i colori da un file di configurazione così che i non‑sviluppatori possano modificare la palette senza toccare il codice.

### Riutilizzare gli stili su più fogli di lavoro

Se esporti diverse tabelle nello stesso workbook, puoi generare l'array di stili una volta e riutilizzarlo:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Assicurati solo che entrambe le tabelle abbiano lo stesso numero di righe, oppure genera un nuovo array per foglio.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco un programma autonomo che puoi copiare‑incollare in un’app console.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Esegui il programma, apri `Report.xlsx` e vedrai lo sfondo alternato esattamente come descritto.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}