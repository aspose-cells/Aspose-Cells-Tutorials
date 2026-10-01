---
category: general
date: 2026-10-01
description: colori alternati delle colonne in Excel usando C# – impara a creare un
  file Excel da un DataTable, impostare il colore di sfondo delle celle in C# e importare
  un DataTable in Excel con colonne stilizzate.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: it
lastmod: 2026-10-01
og_description: Colori alternati delle colonne in Excel resi facili. Segui questa
  guida per creare un file Excel da un DataTable, impostare il colore di sfondo delle
  celle in C# e importare il DataTable in Excel con colonne stilizzate.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Aggiungi colori alternati alle colonne in Excel con C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Come aggiungere colori alternati alle colonne in Excel usando C#
url: /it/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere colori di colonna alternati in Excel usando C#

Se hai bisogno di **alternating column colors excel** in un report generato dalla tua applicazione, questa guida ti mostra una soluzione completa. Vedrai come creare un file Excel da un `DataTable`, impostare il colore di sfondo delle celle in stile C#, e importare il datatable in Excel applicando uno stile distinto a ogni colonna.

Il tutorial copre tutto ciò di cui hai bisogno: pacchetti NuGet richiesti, un esempio completo e eseguibile, e spiegazioni sul perché ogni passaggio è importante. Alla fine avrai una cartella di lavoro stilizzata che può essere aperta direttamente in Microsoft Excel.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 (o successivo) SDK installato  
* Visual Studio 2022 (o qualsiasi IDE compatibile con C#)  
* La libreria **Aspose.Cells for .NET** – installala con  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells fornisce le classi `Workbook`, `Worksheet`, `Style` e `BackgroundType` usate nell'esempio.

## Passo 1: Recuperare i dati di origine come `DataTable`

Il primo compito è ottenere i dati che vuoi esportare. Nei progetti reali potresti riempire il `DataTable` da una query al database, una chiamata API o qualsiasi collezione in memoria.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Perché è importante:**  
Un `DataTable` è un contenitore universale che si mappa perfettamente a un foglio di lavoro Excel. Usare un `DataTable` ti permette di **create excel file from datatable c#** senza scrivere cicli personalizzati per ogni colonna.

## Passo 2: Creare un nuovo workbook e ottenere il suo primo worksheet

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Spiegazione:**  
`Workbook` è l'oggetto radice; `Worksheets[0]` ti restituisce il foglio predefinito dove verranno inseriti i dati.

## Passo 3: Preparare uno stile distinto per ogni colonna (colori di sfondo alternati)

Per ottenere **alternating column colors excel**, generiamo uno `Style` per ogni colonna e assegniamo un colore di sfondo chiaro che alterna due tonalità.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Perché usiamo un ciclo:**  
Il ciclo garantisce che **set cell background color c#** venga applicato in modo coerente, anche se il numero di colonne cambia a runtime. Questo rende la soluzione robusta per report dinamici.

## Passo 4: Importare il `DataTable` nel worksheet, applicando gli stili di colonna

Aspose.Cells può importare direttamente un `DataTable`, e possiamo passare l'array di stili per colorare ogni colonna.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Cosa succede dietro le quinte:**  
`ImportDataTable` scrive la riga di intestazione, poi ogni riga di dati. Poiché abbiamo fornito `columnStyles`, ogni cella di una data colonna riceve lo stile corrispondente, ottenendo i colori alternati desiderati.

## Passo 5: Salvare il workbook stilizzato su file

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Quando apri *StyledTable.xlsx* in Excel vedrai ogni colonna ombreggiata alternativamente, rendendo la tabella più leggibile.

## Esempio completo ed eseguibile

Riunendo tutti i pezzi, ecco un programma autonomo che puoi copiare, incollare ed eseguire.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Output previsto

* Un file chiamato **StyledTable.xlsx** situato in `C:\Temp\`.  
* Il foglio mostra tre colonne (`Id`, `Name`, `Score`) con colori di sfondo alternati: colonne 1 e 3 in *LightYellow*, colonna 2 in *LightCyan*.  
* Tutte le righe del `DataTable` appaiono sotto la riga di intestazione.

## Domande comuni e casi particolari

| Domanda | Risposta |
|----------|--------|
| *Posso usare altri colori?* | Sì. Sostituisci `System.Drawing.Color.LightYellow` e `LightCyan` con qualsiasi valore `System.Drawing.Color`. |
| *E se il DataTable ha molte colonne?* | Il ciclo crea automaticamente uno stile per ogni colonna, quindi il pattern si scala senza modifiche al codice. |
| *Devo rilasciare il workbook?* | Aspose.Cells implementa `IDisposable`. Se avvolgi il `Workbook` in un blocco `using`, le risorse vengono rilasciate prontamente. |
| *Come applicare gli stessi colori alternati alle righe invece che alle colonne?* | Crea un `Style[]` per le righe e chiama `worksheet.Cells.ImportDataTable(..., rowStyles)` – le overload di Aspose.Cells supportano entrambi. |
| *Posso scrivere il file direttamente su uno stream (ad es., per una web API)?* | Sì. Usa `workbook.Save(stream, SaveFormat.Xlsx);` invece di un percorso file. |

## Consigli dal campo

* **Consiglio professionale:** Cache gli oggetti stile se generi molti worksheet in un'unica esecuzione – creare uno stile è relativamente economico, ma riutilizzarli riduce il churn di memoria.  
* **Attenzione a:** Quando usi `System.Drawing.Color` su piattaforme non Windows, aggiungi il pacchetto NuGet `System.Drawing.Common` e assicurati che il runtime supporti GDI+.

## Conclusione

Ora sai come **alternating column colors excel** creando un file Excel da un `DataTable` in C#, impostando i colori di sfondo delle celle con Aspose.Cells, e **import datatable to excel** con un array di stili per colonna. Questo approccio è veloce, manutenibile e funziona con qualsiasi dimensione di set di dati.

### Passi successivi

* Esplora **set cell background color c#** per la formattazione condizionale (ad es., evidenziare punteggi bassi).  
* Combina questa tecnica con **create excel file from datatable c#** per generare report multi‑sheet.  
* Approfondisci l'API di charting di Aspose.Cells per aggiungere riepiloghi visivi allo stesso workbook.

Sentiti libero di adattare i colori, il formato del file o la fonte dei dati per soddisfare le esigenze del tuo progetto. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Imposta lo sfondo della colonna in Excel con C# – Guida completa](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Aggiungi colore di sfondo in Excel – Stili di riga alternati in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Crea Workbook C# – Importa DataTable in Excel con Stili](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}