---
category: general
date: 2026-02-21
description: Scopri come formattare le colonne quando importi una DataTable in Excel
  usando C#. Include consigli per colorare la seconda colonna in Excel e per importare
  una DataTable in Excel con C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: it
og_description: Come formattare le colonne quando si importa un DataTable in Excel
  usando C#. Codice passo‑passo, colorare la seconda colonna in Excel e le migliori
  pratiche.
og_title: Come formattare le colonne in Excel con C# – Guida completa
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Come formattare le colonne in Excel con C# – Importa DataTable
url: /it/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come formattare le colonne in Excel con C# – Importare DataTable

Ti sei mai chiesto **come formattare le colonne** in un foglio di lavoro Excel estraendo i dati direttamente da un `DataTable`? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando hanno bisogno di una rapida spruzzata di colore—magari rosso per la prima colonna, blu per la seconda—senza dover modificare manualmente ogni cella dopo l'importazione.  

La buona notizia? La risposta è una manciata di righe di codice C#, e avrai un foglio completamente formattato non appena i dati arrivano. In questo tutorial tratteremo anche **import datatable to excel**, ti mostreremo **color second column excel**, e spiegheremo perché l'approccio funziona sia per progetti .NET Framework sia per .NET 6+.

---

## Cosa imparerai

- Recuperare un `DataTable` popolato (o crearne uno al volo).  
- Definire oggetti `Style` per colonna per impostare i colori di primo piano.  
- Creare un workbook, ottenere il primo worksheet e importare la tabella con gli stili applicati.  
- Gestire casi limite come tabelle vuote, righe di partenza personalizzate e conteggi di colonne dinamici.  

Alla fine, sarai in grado di inserire un file Excel formattato in qualsiasi pipeline di reporting—senza necessità di post‑processing.

> **Prerequisito:** Familiarità di base con C# e un riferimento a una libreria di fogli di calcolo che supporta `ImportDataTable` (ad es., Aspose.Cells, GemBox.Spreadsheet o EPPlus con un helper). Il codice qui sotto utilizza **Aspose.Cells** perché il suo overload `ImportDataTable` accetta direttamente un `Style[]`.

---

## Passo 1: Configurare il progetto e aggiungere la libreria Excel

Prima di poter formattare qualcosa, abbiamo bisogno di un progetto che faccia riferimento a una libreria di manipolazione Excel.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Suggerimento:* Se sei su .NET 6, aggiungi il pacchetto tramite `dotnet add package Aspose.Cells`. La libreria funziona su Windows, Linux e macOS, quindi sei pronto per il futuro.

---

## Passo 2: Recuperare o costruire il DataTable di origine

Il nucleo del tutorial si concentra sulla formattazione, ma hai comunque bisogno di un `DataTable`. Di seguito trovi un rapido helper che crea dati di esempio; sostituiscilo con la tua chiamata `GetTable()` in produzione.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Perché è importante:** Usare un `DataTable` mantiene la tua fonte dati agnostica—sia che provenga da SQL, CSV o da una collezione in memoria, la logica di importazione rimane la stessa. Questo è il fondamento di **how to import datatable** in modo efficiente.

---

## Passo 3: Definire gli stili delle colonne (il cuore di “How to Style Columns”)

Ora indichiamo al worksheet come deve apparire ogni colonna. La classe `Style` consente di impostare caratteri, colori, bordi e altro. Per questo esempio cambiamo solo il colore di primo piano.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*E se hai più colonne?* Basta aumentare la dimensione dell'array e riempire gli stili di cui hai bisogno. Le colonne non stilizzate ereditano automaticamente lo stile predefinito del worksheet.

---

## Passo 4: Creare il Workbook e importare il DataTable con gli stili

Con dati e stili pronti, è il momento di mettere tutto insieme.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**Cosa è appena accaduto?**  
- `ImportDataTable` copia righe, colonne e *opzionalmente* la riga di intestazione.  
- Passando `columnStyles`, ogni colonna riceve lo `Style` definito in precedenza.  
- La chiamata è una singola riga, il che significa che **import datatable excel c#** è così semplice.

---

## Passo 5: Verificare il risultato – Output previsto

Apri `StyledDataTable.xlsx` in Excel (o LibreOffice). Dovresti vedere:

| **ID** (red) | **Name** (blue) | **Score** (default) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- Il testo della prima colonna appare in **rosso**, soddisfacendo il requisito “how to style columns”.  
- Il testo della seconda colonna è **blu**, il che copre anche la query **color second column excel**.

Se il file si apre senza errori, hai padroneggiato con successo **how to import datatable** mentre formatti le colonne.

---

## Domande comuni e casi limite

### E se il DataTable è vuoto?
`ImportDataTable` creerà comunque la riga di intestazione (se hai passato `true`). Non vengono aggiunte righe di dati, ma gli stili si applicano comunque alle celle di intestazione.

### È necessario iniziare l'importazione in una cella diversa?
Modifica i parametri `rowIndex` e `columnIndex` in `ImportDataTable`. Per esempio, per iniziare da `B2` usa `1, 1` invece di `0, 0`.

### Vuoi formattare le righe invece delle colonne?
Puoi iterare su `worksheet.Cells.Rows` dopo l'importazione e assegnare uno `Style` per riga. Tuttavia, la formattazione a livello di colonna è molto più efficiente perché la libreria applica lo stile una sola volta per colonna.

### Stai usando EPPlus o ClosedXML?
Quelle librerie non espongono un overload diretto di `ImportDataTable` con un array di stili. La soluzione è importare prima la tabella, poi iterare sull'intervallo di colonne e impostare `Style.Font.Color.SetColor(...)`. La logica rimane la stessa, solo qualche riga in più.

---

## Suggerimenti professionali per codice pronto alla produzione

- **Riutilizza gli stili:** Creare un nuovo `Style` per ogni colonna può essere inefficiente. Conserva gli stili riutilizzabili in un dizionario indicizzato per colore o peso del carattere.  
- **Evita conteggi di colonne hard‑coded:** Rileva `dataTable.Columns.Count` e costruisci l'array `columnStyles` dinamicamente.  
- **Sicurezza dei thread:** Se generi molti workbook in parallelo, istanzia un `Workbook` separato per thread; gli oggetti Aspose.Cells non sono thread‑safe.  
- **Prestazioni:** Per tabelle più grandi di 10 k righe, considera di disabilitare `AutoFitColumns` (scansiona ogni cella) e imposta manualmente le larghezze delle colonne.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Esegui il programma, apri il `StyledDataTable.xlsx` generato, e vedrai le colonne colorate immediatamente. Questo è l'intero workflow **import datatable excel c#** in poche parole.

---

## Conclusione

Abbiamo appena coperto **how to style columns** quando **import datatable to excel** usando C#. Definendo un array `Style[]` e passandolo a `ImportDataTable`, puoi colorare la prima colonna in rosso, la seconda in blu, e lasciare le altre inalterate—tutto in una singola riga di codice.  

L'approccio è scalabile: aggiungi altri oggetti `Style` per colonne aggiuntive, regola le righe di partenza, o sostituisci Aspose.Cells con un'altra libreria con API simile. Ora puoi generare report Excel curati senza mai toccare manualmente il file.

**Passi successivi** che potresti esplorare:

- Usa **conditional formatting** per evidenziare dinamicamente i valori (collegato a “color second column excel”).  
- Esporta più worksheet da un unico set di `DataTable` (ideale per dashboard mensili).  
- Combina questo con la conversione **CSV → DataTable** per costruire un flusso end‑to‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}