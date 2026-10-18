---
category: general
date: 2026-06-27
description: Come formattare le colonne di Excel in C# con colori alternati. Impara
  a creare un workbook Excel in C#, importare DataTable in Excel e esportare come
  .xlsx.
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: it
og_description: Come formattare le colonne di Excel in C# con colori alternati. Segui
  questo tutorial passo‑passo per creare una cartella di lavoro Excel in C#, importare
  un DataTable e esportare in .xlsx.
og_title: Come formattare le colonne di Excel in C# – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Come formattare le colonne di Excel in C# – Guida completa
url: /it/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come formattare le colonne Excel in C# – Guida completa

Ti sei mai chiesto **come formattare le colonne Excel** in C# senza strapparsi i capelli? Non sei l'unico. Che tu stia generando un report di vendite o scaricando un dump di database in un foglio di calcolo, far apparire quelle colonne ordinate può fare la differenza tra “meh” e “wow”.

In questo tutorial percorreremo un **esempio completo e eseguibile** che ti mostra come **creare un workbook Excel in C#**, **importare un DataTable in Excel** e **applicare colori alternati alle colonne** così ogni colonna risalta. Alla fine saprai anche come **esportare un DataTable come xlsx** con una singola riga di codice. Niente superflui, solo codice pratico da copiare‑incollare.

> **Cosa ti servirà**  
> - .NET 6 o successivo (qualsiasi versione recente va bene)  
> - Il pacchetto NuGet **Aspose.Cells** (o qualsiasi simile) – lo useremo perché è puro C# e non richiede Excel installato.  
> - Una semplice sorgente `DataTable` – ne genereremo una al volo per scopi dimostrativi.

Iniziamo.

![Esempio di come formattare le colonne Excel in C#](excel-columns.png "Come formattare le colonne Excel in C#")

## Passo 1: Creare un workbook Excel in C#  

La prima cosa da fare è avviare un nuovo workbook. Pensalo come aprire un quaderno nuovissimo dove scriverai i tuoi dati.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**Perché è importante:** `Workbook` è il punto di ingresso per ogni operazione su Excel. Crearlo **crea un excel workbook c#** senza bisogno di COM interop, e l'oggetto vive interamente in memoria fino a quando decidi di salvarlo.

> **Consiglio professionale:** Se punti a un ambiente server, preferisci una libreria che non dipenda dall'installazione di Microsoft Office. Aspose.Cells, EPPlus o ClosedXML soddisfano tutti questi requisiti.

## Passo 2: Preparare gli stili – Applicare colori alternati alle colonne  

Ora arriva la parte divertente: far sì che ogni altra colonna abbia una tonalità diversa. Questo indizio visivo aiuta i lettori a scansionare tabelle grandi più rapidamente.

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**Cosa sta succedendo?**  
- `workbook.CreateStyle()` ci fornisce una tela pulita per ogni colonna.  
- Il ternario `(i % 2 == 0) ? Color.Blue : Color.Green` è il cuore di **apply alternating column colors** – le colonne con indice pari diventano blu, quelle dispari verdi.  
- Puoi estendere questo blocco per impostare riempimenti di sfondo, bordi o formati numerici senza modificare il resto del codice.

> **Caso limite:** Se la tua tabella ha più di qualche decina di colonne, creare uno stile per colonna può consumare memoria. In quello scenario, riutilizza due oggetti stile (blueStyle, greenStyle) e assegnali in base all'indice della colonna.

## Passo 3: Costruire un DataTable di esempio (o usare il tuo)  

Per una demo autonoma genereremo un `DataTable` con qualche riga. Nei progetti reali sostituirai `GetSampleData()` con la tua logica di recupero dati.

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

Ora collega questo al flusso principale:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## Passo 4: Importare DataTable nel foglio di lavoro con gli stili  

Aspose.Cells rende l'importazione una singola riga. La sovraccarico che usiamo ci permette di passare l'array di stili che abbiamo creato prima.

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**Perché usare questo overload?**  
- Rispetta la riga di intestazione, così non devi scrivere manualmente i nomi delle colonne.  
- Applica l'array **columnStyles** colonna per colonna, dandoci i colori alternati senza loop aggiuntivi.  
- È veloce – l'intera tabella viene caricata in memoria con una sola chiamata.

## Passo 5: Salvare il workbook – Esportare DataTable come .xlsx  

Infine, persisti il workbook su disco. Qui avviene **export datatable as xlsx**.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

Quando apri `output.xlsx` vedrai:

| **ID** | **Name**      | **Score** | **Date**    |
|--------|---------------|-----------|-------------|
| *1* (blu) | *Student 1* (verde) | *77* (blu) | *2026‑06‑26* (verde) |
| *2* (verde) | *Student 2* (blu) | *79* (verde) | *2026‑06‑25* (blu) |
| …      | …             | …         | …           |

*I caratteri blu e verde si alternano per colonna, esattamente come abbiamo programmato.*

## Passo 6: Problemi comuni e come evitarli  

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Stili non applicati** | Passare `null` o una lunghezza dell'array non corrispondente a `ImportDataTable`. | Assicurarsi che `columnStyles.Length == dataTable.Columns.Count`. |
| **File bloccato dopo il salvataggio** | Un altro processo (ad esempio Excel) ha il file aperto. | Chiudere eventuali visualizzatori prima dell'esecuzione, oppure salvare in un percorso temporaneo e spostare il file dopo. |
| **Consumo di memoria eccessivo con tabelle enormi** | Creare uno stile per colonna per migliaia di colonne. | Riutilizzare due oggetti stile e assegnarli in base a `(col % 2)`. |
| **Formato data errato** | Excel interpreta `DateTime` come un numero. | Impostare `columnStyles[i].Number = 14; // built‑in date format` per le colonne data. |

## Passo 7: Prossimi passi – Oltre la formattazione semplice  

Ora che hai padroneggiato **come formattare le colonne Excel** con font alternati, puoi sperimentare con:

- **Formattazione condizionale** – evidenzia le celle che soddisfano regole di business.  
- **Oggetti tabella** – trasforma l'intervallo in una Tabella Excel per filtri automatici.  
- **Generazione di grafici** – visualizza i dati direttamente dal workbook.  
- **Streaming di esportazioni di grandi dimensioni** – usa `SaveOptions` per scrivere file enormi senza caricare tutto in RAM.

Tutti questi si basano sugli stessi concetti fondamentali trattati: creare un workbook, stilare le celle, importare i dati e salvare.

---

### Conclusione  

Hai appena imparato **come formattare le colonne Excel** in C# dall'inizio alla fine: creare un workbook Excel in C#, applicare colori alternati alle colonne, importare un DataTable in Excel e infine esportare il DataTable come file .xlsx. Il codice completo, pronto da copiare‑incollare, funziona subito, e le spiegazioni rispondono al “perché” dietro ogni riga.

Sentiti libero di modificare i colori, aggiungere bordi o passare a un'altra libreria se preferisci. Il modello rimane lo stesso, e il risultato è sempre un foglio di calcolo pulito e professionale pronto per gli stakeholder.

Hai domande o vuoi condividere i tuoi trucchi di styling? Lascia un commento qui sotto e continuiamo la conversazione. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come importare DataTable in Excel usando Aspose.Cells per .NET (Guida passo‑passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Come creare e configurare workbook Excel con Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Come creare e formattare tabelle Excel usando Aspose.Cells per .NET | Guida passo‑passo](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}