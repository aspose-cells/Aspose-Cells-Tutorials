---
category: general
date: 2026-03-18
description: Scopri come applicare colori alternati alle righe in un foglio di lavoro
  usando C#. Include impostare il colore di sfondo della riga, aggiungere uno sfondo
  giallo chiaro e colorare le righe in modo alternato.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: it
og_description: Applica colori alternati alle righe in C# per migliorare la leggibilità.
  Questa guida mostra come impostare il colore di sfondo della riga, aggiungere uno
  sfondo giallo chiaro e colorare le righe alternativamente.
og_title: Applica colori alternati alle righe in C# – Tutorial completo
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Applica colori alternati alle righe in C# – Guida passo passo
url: /it/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicare colori di riga alternati in C# – Tutorial completo

Hai mai dovuto **applicare colori di riga alternati** a un foglio di lavoro basato su dati ma non sapevi da dove cominciare? Non sei l’unico — la maggior parte degli sviluppatori si imbatte in questo ostacolo al primo tentativo di rendere le tabelle più amichevoli. La buona notizia? In poche righe di C# puoi **impostare il colore di sfondo della riga**, aggiungere un **leggero sfondo giallo**, e ottenere una griglia rifinita che migliora immediatamente la leggibilità.

In questo tutorial percorreremo l’intero processo, dal recuperare un `DataTable` in memoria allo stilizzare ogni riga con una delicata striscia giallo‑bianca. Alla fine sarai in grado di **colorare le righe alternatamente** con sicurezza, e vedrai anche alcune varianti utili per quando ti servono tonalità diverse o tematiche dinamiche.

## Cosa ti servirà

Prima di immergerci, assicurati di avere a disposizione:

- Un progetto .NET che targetti .NET 6 o versioni successive (il codice funziona anche su .NET Framework 4.7+).  
- Una libreria per fogli di calcolo che supporti oggetti di stile – l’esempio utilizza un’API generica `Workbook`/`Worksheet` che rispecchia librerie come **Aspose.Cells**, **GemBox.Spreadsheet**, o **ClosedXML**.  
- Una sorgente `DataTable` – può provenire da una query al database, da un’importazione CSV, o da qualsiasi collezione in‑memory.  

Nessun pacchetto NuGet aggiuntivo oltre alla libreria per fogli di calcolo stessa. Se usi Aspose.Cells, lo spazio dei nomi è `Aspose.Cells`; per ClosedXML è `ClosedXML.Excel`. Sostituisci le chiamate `CreateStyle` e `ImportDataTable` di conseguenza.

## Passo 1: Recuperare i dati di origine come DataTable

Prima di tutto—prendi i dati che vuoi visualizzare. Nelle app reali questo di solito significa interrogare un database, ma per chiarezza utilizzeremo un metodo di supporto chiamato `GetData()` che restituisce un `DataTable` popolato.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Perché è importante:** Il `DataTable` definisce le righe e le colonne che successivamente riceveranno la sfumatura alternata. Se la tabella è vuota, non c’è nulla da stilizzare, quindi verifica sempre che `Rows.Count` > 0 prima di procedere.

### Consiglio professionale
Se estrai dati da Entity Framework, puoi usare `DataTable.Load(reader)` dopo aver eseguito un `SqlCommand`. Questo mantiene il codice pulito ed evita definizioni manuali delle colonne.

## Passo 2: Allocare un array per contenere uno stile per ogni riga

Successivamente, ci serve un contenitore che corrisponda al numero di righe. La maggior parte delle API per fogli di calcolo permette di passare un array di stili al metodo di importazione, quindi creeremo un `Style[]` dimensionato esattamente al conteggio delle righe.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Spiegazione:** Pre‑allocando l’array, evitiamo di creare un nuovo oggetto stile ad ogni iterazione, il che può rappresentare un vantaggio di prestazioni quando si gestiscono migliaia di righe.

## Passo 3: Applicare colori di riga alternati (Giallo chiaro / Bianco)

Ora arriva il cuore della questione: **applicare colori di riga alternati**. Cicleremo su ogni riga, creeremo una nuova istanza di stile dal workbook, e imposteremo lo sfondo in base all’indice della riga. Le righe pari ottengono un riempimento giallo chiaro, le righe dispari rimangono bianche.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Perché funziona
- **`rowIndex % 2 == 0`** verifica se la riga è pari.  
- **`Color.LightYellow`** fornisce una tonalità delicata e non invasiva, perfetta per le tabelle di dati.  
- **`BackgroundType.Solid`** garantisce che il riempimento copra l’intera cella, ottenendo l’effetto **set row background color**.  

Puoi sostituire `Color.LightYellow` con qualsiasi altra sfumatura (ad es. `Color.LightCyan`) se preferisci un aspetto diverso. La stessa logica ti permette anche di **colorare le righe alternatamente** in base ad altri criteri, come flag di stato.

## Passo 4: Importare il DataTable nel Worksheet con gli stili preparati

Infine, trasferiamo tutto nel foglio di lavoro. La maggior parte delle librerie espone una sovraccarico di `ImportDataTable` che accetta un array di stili. Il flag `true` indica all’API di scrivere le intestazioni di colonna, e le coordinate `0, 0` partono dalla cella in alto a sinistra.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Risultato:** Il foglio di lavoro ora mostra i dati con un pulito pattern di **alternating row shading** — giallo chiaro sulle righe pari, bianco sulle dispari. Gli utenti possono scansionare la griglia senza che gli occhi saltino avanti e indietro.

### Output previsto
Se apri il foglio di calcolo risultante, vedrai qualcosa di simile:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Le righe 1, 3, 5… hanno uno **sfondo giallo chiaro**, mentre le righe 2, 4, 6… rimangono **bianche**. La riga di intestazione (riga 0) eredita lo stile predefinito a meno che non la personalizzi separatamente.

## Varianti opzionali & casi particolari

### 1. Usare una palette di colori diversa
Se il giallo chiaro non si adatta al tuo brand, sostituisci semplicemente `Color.LightYellow` con un altro `System.Drawing.Color`. Per un tema blu‑grigio potresti usare:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Ombreggiatura dinamica basata sui dati
A volte vuoi evidenziare le righe che soddisfano una condizione (ad es. scorte basse). Combina il controllo modulo con un test personalizzato:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Applicare stili solo a colonne specifiche
Se ti serve il **set row background color** solo su certe colonne, crea uno stile separato per ciascuna colonna e assegnalo dopo l’importazione usando l’API di intervallo celle del worksheet.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Consiglio di prestazioni per tabelle grandi
Quando gestisci > 10.000 righe, considera di riutilizzare un unico oggetto stile per ogni colore invece di crearne uno nuovo per riga. L’array conterrà quindi riferimenti ai due stili condivisi, riducendo drasticamente l’uso di memoria.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Esempio completo funzionante

Di seguito trovi un programma autonomo che puoi incollare in una console app. Usa un’API fittizia `Workbook`/`Worksheet`; sostituisci i tipi con quelli della libreria che hai scelto.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** Un file chiamato `AlternatingRows.xlsx` dove ogni riga alterna un riempimento giallo chiaro e bianco, rendendo la tabella più gradevole alla vista.

## Domande frequenti

**D: Questo approccio funziona con la formattazione condizionale in stile Excel?**  
R: Sì. Se la tua libreria supporta regole condizionali, puoi tradurre la stessa logica in una regola che verifica `MOD(ROW(),2)=0`. Il metodo basato su codice mostrato qui è più portabile tra le librerie che non hanno la formattazione condizionale integrata.

**D: E se devo **colorare le righe alternatamente** in una tabella PDF invece che in un foglio Excel?**  
R: La maggior parte dei generatori di tabelle PDF (ad es. iTextSharp, PdfSharp) ti permette di impostare un `BackgroundColor` per riga. Si applica lo stesso calcolo modulo—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}