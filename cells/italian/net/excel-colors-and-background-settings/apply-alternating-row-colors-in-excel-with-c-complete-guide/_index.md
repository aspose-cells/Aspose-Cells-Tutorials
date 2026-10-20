---
category: general
date: 2026-07-03
description: Applica colori alternati alle righe mentre importi una datatable in Excel
  usando C#. Scopri come esportare una datatable C# in Excel, salvare il foglio di
  lavoro con stile e mantenere la formattazione della cartella di lavoro.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: it
og_description: Applica colori alternati alle righe in Excel usando C#. Questo tutorial
  mostra come importare una datatable in Excel, esportare una datatable C# in Excel
  e salvare la cartella di lavoro con la formattazione.
og_title: Applica colori alternati alle righe in Excel con C# – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Applica colori alternati alle righe in Excel con C# – Guida completa
url: /it/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicare colori di riga alternati in Excel con C# – Guida completa

Hai mai dovuto **applicare colori di riga alternati** quando esporti una `DataTable` C# in Excel? Non sei l’unico—gli sviluppatori chiedono continuamente come rendere quei fogli di calcolo più curati senza dover intervenire manualmente su Excel in seguito. La buona notizia? Puoi farlo programmaticamente in poche righe di codice.

In questo tutorial percorreremo **import datatable to excel**, ti mostreremo come **export c# datatable to excel** con una tabella stilizzata e, infine, **save styled table excel** mantenendo la formattazione. Alla fine potrai **save workbook with formatting** con un risultato pronto per una presentazione al cliente.

## Prerequisiti

- .NET 6.0 o successivo (l’esempio usa .NET 6, ma funziona con qualsiasi versione recente)
- Aspose.Cells per .NET (versione di prova gratuita o licenziata) – questa libreria rende lo styling un gioco da ragazzi
- Una sorgente `DataTable` (può provenire da un database, CSV o da una collezione in‑memoria)

> **Pro tip:** Se non hai ancora Aspose.Cells, puoi scaricarlo da NuGet con `dotnet add package Aspose.Cells`.

## Passo 1: Configurare il progetto e caricare i dati

Per prima cosa, crea un’app console (o qualsiasi progetto C#) e aggiungi le istruzioni `using` necessarie. Poi carica i dati in una `DataTable`. Per fare un esempio genereremo una tabella semplice al volo.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Perché è importante:** Avere una `DataTable` pronta significa che puoi **import datatable to excel** con una sola chiamata, eliminando la necessità di inserire manualmente cella per cella.

## Passo 2: Creare un Workbook e definire gli stili di riga alternati

Ora istanzieremo un nuovo `Workbook`. Il trucco per **apply alternating row colors** risiede in `ImportTableOptions.StyleArray`. Useremo i primi due stili predefiniti (tipicamente bianco e grigio chiaro), ma potrai personalizzarli in seguito.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Spiegazione:** `ImportTableOptions` indica ad Aspose.Cells come trattare ogni riga durante l’importazione. Fornendo un `StyleArray` con due voci, la libreria colora automaticamente ogni riga dispari con il primo stile e ogni riga pari con il secondo—esattamente ciò che ti serve per **apply alternating row colors**.

## Passo 3: Importare la DataTable nel foglio di lavoro (incluse le intestazioni)

Con il workbook e gli stili pronti, ora **import datatable to excel**. Il metodo `ImportDataTable` fa il lavoro pesante: scrive le intestazioni di colonna, rispetta lo style array e posiziona i dati a partire dalla cella A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Perché includiamo `true` come secondo argomento:** Indica al metodo di scrivere i nomi delle colonne nella prima riga, fondamentale per un report dall’aspetto professionale.

## Passo 4: Rifinire la tabella (opzionale ma utile)

Se vuoi che le colonne si adattino automaticamente o aggiungere una riga filtro, qualche riga extra la renderà più brillante.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Queste ottimizzazioni non influenzano i colori alternati ma migliorano l’esperienza complessiva dell’utente del file **save styled table excel**.

## Passo 5: Salvare il workbook mantenendo tutta la formattazione

Infine, scriviamo il file su disco. Il metodo `Save` conserva ogni stile impostato, garantendo che le righe alternanti rimangano intatte.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Quando apri `StyledEmployees.xlsx`, vedrai una tabella pulita in cui le righe alternano bianco e grigio chiaro—esattamente il segnale visivo su cui molti utenti contano per la leggibilità.

### Output previsto

| ID | Nome   | Dipartimento | DataAssunzione |
|----|--------|--------------|----------------|
| 1  | Alice  | Finance      | 15‑01‑2020 |
| 2  | Bob    | HR           | 23‑06‑2019 |
| 3  | Charlie| IT           | 10‑03‑2021 |
| 4  | Diana  | Marketing    | 05‑11‑2018 |

- Riga 1, 3 … → sfondo bianco  
- Riga 2, 4 … → sfondo grigio chiaro  

Questo è l’intero processo di **save workbook with formatting**.

## Domande comuni & casi particolari

### E se la mia DataTable contiene migliaia di righe?

Il metodo `ImportDataTable` trasmette i dati in modo efficiente, ma potresti raggiungere i limiti di memoria con tabelle molto grandi. In questi casi, valuta di suddividere l’esportazione in più fogli o di usare la sovraccarico di `ImportDataTable` che consente di specificare riga e colonna di partenza.

### Posso usare colori personalizzati invece di quelli predefiniti?

Assolutamente sì. Basta sostituire le assegnazioni `ForegroundColor` in `styleWhite` e `styleGray` con qualsiasi `System.Drawing.Color` preferisci—pensaci a blu pastello o ai colori del brand aziendale.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Come garantire che lo stile alternato funzioni quando l’utente aggiunge righe in seguito?

Se gli utenti modificano il file manualmente, l’array di stile originale non si estenderà automaticamente. Una rapida soluzione è convertire l’intervallo in una Tabella Excel (`ListObject`) dopo l’importazione; Excel allora ripete il pattern per le nuove righe.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Ora ogni nuova riga eredita i colori alternati.

## Esempio completo funzionante (tutti i passaggi in un unico posto)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Esegui il programma, apri il file generato e vedrai immediatamente i colori alternati applicati—senza alcuna formattazione manuale.

## Conclusione

Abbiamo appena dimostrato come **apply alternating row colors** quando **import datatable to excel** usando C#. Il processo copre tutto ciò che ti serve per **export c# datatable to excel**, **save styled table excel** e **save workbook with formatting** con un aspetto professionale fin da subito.

Prossimi passi? Prova a scambiare i due stili per un tema personalizzato, o trasforma l’intervallo in una Tabella Excel così gli utenti possono ordinare e filtrare mantenendo il pattern di colore. Puoi anche esplorare la formattazione condizionale tramite `ConditionalFormattingCollection` per segnali visivi più dinamici.

Hai un twist

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [Come importare DataTable in Excel usando Aspose.Cells per .NET (Guida passo‑passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Applicare colori e sfondi in Excel usando Aspose.Cells per .NET](/cells/english/net/formatting/colors-and-background/)
- [Automatizzare i colori del tema Excel usando Aspose.Cells .NET per una formattazione efficiente](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}