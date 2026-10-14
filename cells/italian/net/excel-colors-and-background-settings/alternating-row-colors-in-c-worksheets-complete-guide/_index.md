---
category: general
date: 2026-05-30
description: Scopri come aggiungere colori alternati alle righe nei fogli di lavoro
  C#, impostare lo sfondo delle celle con un riempimento solido e personalizzare lo
  stile delle celle del foglio di lavoro senza sforzo.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: it
og_description: Colori alternati delle righe nei fogli di lavoro C# semplificati.
  Impara a impostare lo sfondo delle celle, utilizzare un riempimento solido e padroneggiare
  lo stile delle celle del foglio di lavoro.
og_title: Colori Alternati delle Righe nei Fogli di Lavoro C# – Guida Completa
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Colori Alternati delle Righe nei Fogli di Lavoro C# – Guida Completa
url: /it/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Colori di riga alternati nei fogli di lavoro C# – Guida completa

Ti sei mai chiesto come rendere il tuo esportazione Excel più curata usando **alternating row colors**? Non sei solo—gli sviluppatori chiedono costantemente come *add background color* alle righe senza scrivere milioni di righe di codice.  

In questo tutorial vedremo un modo semplice per **set cell background** su ogni riga, applicare un **solid fill pattern**, e controllare lo **worksheet cell style** in modo che il risultato sia sia leggibile che visivamente attraente.

## Cosa imparerai

- Recuperare i dati in un `DataTable` (o qualsiasi fonte tabellare).  
- Creare un array di oggetti `Style` che alternano due colori.  
- Importare il `DataTable` in un foglio di lavoro applicando quegli stili.  
- Verificare l'output e regolare i colori o i pattern se necessario.  

Non sono necessari strumenti esterni oltre a un ambiente .NET e una libreria per fogli di calcolo (useremo **Aspose.Cells** negli esempi). Alla fine avrai un metodo riutilizzabile che potrai inserire in qualsiasi pipeline di reporting.

---

## Passo 1: Recupera i dati di origine come `DataTable`

Prima di tutto—senza dati non c’è nulla da formattare. Di seguito trovi un piccolo helper che crea un `DataTable` con righe di esempio. In un progetto reale lo sostituirai con una chiamata al database o un parser CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Perché è importante:** Avere i dati in un `DataTable` consente al motore del foglio di lavoro di *import*arli in una sola chiamata, preservando automaticamente i nomi delle colonne e i tipi di dati.

## Passo 2: Crea gli stili **Alternating Row Colors**

Ora genereremo un array di oggetti `Style`—uno per riga—così che le righe pari ottengano una sfumatura giallo chiaro mentre le righe dispari ricevano un delicato ciano. Questo è il nucleo della tecnica **alternating row colors**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Perché usare un **Solid Fill Pattern**?

La proprietà `Pattern` indica al motore come renderizzare il colore. Un riempimento `Solid` garantisce che l'intero sfondo della cella sia dipinto, eliminando eventuali linee di griglia sottili che altrimenti potrebbero apparire. Questo è il modo più comune per **set cell background** quando si desidera un aspetto pulito.

## Passo 3: Importa il `DataTable` con gli stili preparati

Con l'array di stili pronto, la chiamata di importazione diventa una singola riga. Aspose.Cells applicherà automaticamente lo stile corrispondente a ogni riga.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Cosa succede dietro le quinte?**  
> La libreria itera su ogni riga, copia i valori nelle celle e poi applica lo `Style` corrispondente da `rowStyles`. Poiché abbiamo già definito un **solid fill pattern**, ogni cella in una riga eredita lo stesso colore di sfondo, fornendoti perfetti **alternating row colors**.

## Passo 4: Salva la cartella di lavoro e verifica il risultato

Un rapido salvataggio ti permette di aprire il file in Excel (o in qualsiasi visualizzatore compatibile) e vedere l'effetto.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Quando apri il file, le righe 1, 3, 5… saranno giallo chiaro, mentre le righe 2, 4, 6… saranno ciano chiaro. le intestazioni di colonna rimangono bianche, facendo risaltare i dati.

![Foglio di lavoro con colori di riga alternati](/images/alternating-row-colors.png "Screenshot del foglio di lavoro con colori di riga alternati")

*Testo alternativo dell'immagine:* **alternating row colors** screenshot di un foglio di lavoro dove lo sfondo di ogni riga alterna tra giallo chiaro e ciano chiaro.

## Passo 5: Personalizzare ulteriormente (Opzionale)

### Cambia i colori

Se il tuo brand utilizza tonalità diverse, basta sostituire `Color.LightYellow` e `Color.LightCyan` con qualsiasi `System.Drawing.Color` preferisci. Per esempio:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Usa un diverso **Background Type**

Mentre `BackgroundType.Solid` è il più comune, puoi sperimentare con `BackgroundType.Gray125`, `BackgroundType.Horizontal`, o qualsiasi pattern supportato dalla libreria. Questo cambia la texture visiva mantenendo comunque **adding background color**.

### Applica un **Worksheet Cell Style** a colonne specifiche

A volte vuoi l'effetto alternato solo sulle colonne dati, lasciando intatta la prima colonna (es. ID). Crea uno stile separato per quella colonna e assegnalo dopo l'importazione:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Conclusione

Ora hai una soluzione completa e riutilizzabile per **alternating row colors** nei fogli di lavoro C#. Creando un array di oggetti `Style`, **setting cell background** con un **solid fill pattern**, e importando un `DataTable` in una sola chiamata, puoi produrre report dall'aspetto professionale con codice minimo.  

Da qui potresti:

- **Add background color** alle righe di intestazione per maggiore enfasi.  
- Combina la tecnica con la formattazione condizionale per indicazioni visive dinamiche.  
- Esplora altre proprietà **worksheet cell style** come caratteri, bordi o formati numerici.

Provalo nella tua prossima routine di esportazione—i tuoi utenti ti ringrazieranno per fogli di calcolo più puliti e leggibili. Buon coding!

## Cosa dovresti imparare dopo?

- [Imposta l'altezza delle righe nel foglio di lavoro con Aspose.Cells per .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Converti i nomi delle celle Excel in indici di riga e colonna usando Aspose.Cells per .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Imposta i colori delle schede del foglio di lavoro in Excel usando Aspose.Cells .NET - Guida completa](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}