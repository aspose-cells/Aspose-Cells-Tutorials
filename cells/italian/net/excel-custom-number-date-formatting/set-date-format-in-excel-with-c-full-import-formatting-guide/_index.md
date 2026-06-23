---
category: general
date: 2026-06-17
description: Imposta il formato data in Excel usando C# e imposta anche lo sfondo
  della cella, applica il colore del testo e colora la colonna di Excel durante l'importazione.
  Impara passo dopo passo.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: it
og_description: Imposta il formato data in Excel con C# mentre imposti lo sfondo della
  cella, applichi il colore del testo e colori la colonna di Excel durante l'importazione.
  Tutorial completo.
og_title: Imposta il formato data in Excel con C# – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Imposta il formato data in Excel con C# – Guida completa alla formattazione
  dell'importazione
url: /it/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il formato data in Excel con C# – Guida completa al formattazione di importazione

Hai mai dovuto **impostare il formato data** in un foglio Excel generato da codice C#, ma volevi anche che la colonna avesse uno sfondo o un colore del testo personalizzato? Non sei l’unico. In molti scenari di reporting estrai un `DataTable` da un database, lo inserisci in un foglio di lavoro e poi ti affretti a far apparire correttamente le date e a far risaltare le colonne con i colori giusti.  

In questo tutorial vedremo una soluzione pulita, end‑to‑end, che **imposta il formato data**, **imposta lo sfondo della cella**, **applica il colore del testo** e persino **colora una colonna di Excel** durante l’importazione dei dati. Alla fine avrai un modello riutilizzabile che gestisce la **formattazione di importazione Excel** senza i soliti tentativi ed errori.

> **Cosa ti servirà**  
> * .NET 6+ (o .NET Framework 4.7+)  
> * Aspose.Cells per .NET (la versione di prova gratuita è sufficiente per i test)  
> * Una sorgente `DataTable` – qualsiasi query ADO.NET andrà bene  
> * Visual Studio o il tuo IDE preferito  

Iniziamo.

---

## Panoramica della soluzione

Divideremo il problema in tre parti logiche:

1. **Recuperare i dati di origine** – un `DataTable` con le righe che vuoi esportare.  
2. **Creare stili specifici per colonna** – uno stile per la colonna data, un altro per una colonna di testo, più eventuali formattazioni aggiuntive che desideri.  
3. **Importare la tabella con gli stili** – usa `Worksheet.Cells.ImportDataTable` così ogni colonna eredita lo stile che hai preparato.

Perché questo approccio? Perché Aspose.Cells ti permette di allegare direttamente un array di `Style` alla chiamata `ImportDataTable`, il che significa che non è necessario un secondo passaggio per ri‑applicare la formattazione. È più veloce, meno soggetto a errori e mantiene il codice ordinato.

---

## Passo 1: Recuperare i dati da esportare

Prima di tutto – ti serve un `DataTable`. In un progetto reale probabilmente chiamerai una stored procedure o utilizzerai Entity Framework per riempirlo, ma per scopi dimostrativi simuleremo una semplice tabella con una colonna data e una di testo.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Consiglio professionale:** Se la tua sorgente utilizza date nullable, assicurati che il tipo della colonna sia `typeof(DateTime?)` – Aspose rispetterà comunque il formato che assegnerai in seguito.

---

## Passo 2: Preparare un array di stili – Uno per colonna

Ora creiamo un `Style[]` la cui lunghezza corrisponde al numero di colonne del `DataTable`. Ogni voce conterrà la formattazione per la rispettiva colonna.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Impostare il formato data per la prima colonna

La prima colonna (`OrderDate`) dovrebbe essere visualizzata come “MM/dd/yyyy”. Aspose utilizza l’indice di formato numerico interno 14 per la data breve, ma puoi anche fornire una stringa di formato personalizzata se preferisci.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Perché è importante:** Excel memorizza le date come numeri seriali. Assegnando un formato numerico, dici a Excel di renderizzare quei seriali come date leggibili dall’uomo invece che come numeri grezzi.

### 2.2 Impostare lo sfondo della cella per la seconda colonna

Diamo alla colonna `CustomerName` uno sfondo azzurro chiaro. È qui che entra in gioco **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Nota:** Senza impostare `Pattern` a `Solid`, il colore di primo piano non apparirà perché il pattern predefinito è “None”.

### 2.3 Applicare il colore del testo (foreground) – Opzionale extra

Se vuoi anche che il testo abbia un colore di contrasto, puoi modificare lo stesso stile:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Questo soddisfa il requisito **apply foreground color** mantenendo intatto lo sfondo della colonna.

---

## Passo 3: Importare il DataTable con gli stili definiti

Con gli stili pronti, l’ultimo passo è una singola riga che importa i dati e applica gli stili colonna per colonna.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Come funziona:** Aspose legge l’array `columnStyles` e mappa ogni `Style` all’indice di colonna corrispondente. La riga di intestazione eredita lo stile predefinito a meno che non fornisci uno stile separato per la riga 0.

### 3.1 Salvare la cartella di lavoro

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Esegui il programma, apri *FormattedReport.xlsx* e dovresti vedere:

- la colonna **OrderDate** visualizzata come data (es. `06/15/2026`).  
- la colonna **CustomerName** con riempimento azzurro chiaro e testo blu scuro.  

Questo è l’intero flusso di lavoro di **excel import formatting** in meno di 30 righe di C#.

---

## Riepilogo passo‑passo (con il perché)

| Passo | Cosa fai | Perché è importante |
|------|-------------|----------------|
| **Recupera dati** | Chiama `GetData()` per riempire un `DataTable`. | Fornisce una sorgente strutturata che Aspose può ingerire direttamente. |
| **Crea array di stili** | Alloca `Style[]` corrispondente al conteggio delle colonne. | Consente la formattazione per colonna in una singola chiamata di importazione. |
| **Imposta formato data** | `columnStyles[0].Number = 14;` | Garantisce che le date vengano visualizzate correttamente in Excel. |
| **Imposta colore di sfondo** | `ForegroundColor = LightBlue; Pattern = Solid;` | Evidenzia la colonna, soddisfacendo **set cell background**. |
| **Applica colore del testo** | `Font.Color = DarkBlue;` | Migliora la leggibilità e soddisfa **apply foreground color**. |
| **Importa con gli stili** | `ImportDataTable(..., columnStyles);` | Importazione in un solo passaggio che rispetta tutta la formattazione. |
| **Salva cartella di lavoro** | `wb.Save(...);` | Persiste il risultato per gli utenti successivi. |

---

## Gestione dei casi limite e domande frequenti

### E se ho più di due colonne?

Basta espandere l’array `columnStyles` e assegnare un `Style` a ciascun indice di cui ti interessa curare lo stile. Gli indici non assegnati torneranno allo stile predefinito, il che è perfettamente accettabile.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Come formattare una colonna come valuta?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Posso cambiare lo stile della riga di intestazione separatamente?

Sì. Dopo l’importazione, puoi prendere la prima riga e applicare uno stile distinto:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Cosa succede se il DataTable contiene date nulle?

Aspose lascerà quelle celle vuote. Se preferisci un segnaposto come “N/A”, puoi pre‑processare la tabella:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Quindi regola lo stile per visualizzare un formato personalizzato che mostri “N/A” per il valore sentinella.

---

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto da copiare‑incollare. Eseguilo come applicazione console e otterrai un file Excel ben formattato.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}