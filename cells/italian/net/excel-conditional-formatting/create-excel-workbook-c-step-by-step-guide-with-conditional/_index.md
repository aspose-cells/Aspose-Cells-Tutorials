---
category: general
date: 2026-03-27
description: Crea un workbook Excel in C# con Aspose.Cells, applica la formattazione
  condizionale, importa un DataTable in Excel e salva il workbook come xlsx—tutto
  in un unico tutorial.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: it
og_description: Crea una cartella di lavoro Excel in C# usando Aspose.Cells, applica
  la formattazione condizionale, importa una datatable in Excel e salva la cartella
  di lavoro come xlsx in pochi minuti.
og_title: Crea un workbook Excel in C# – Guida completa con formattazione condizionale
tags:
- Aspose.Cells
- C#
- Excel automation
title: Creare una cartella di lavoro Excel in C# – Guida passo passo con formattazione
  condizionale
url: /it/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un workbook Excel C# – Tutorial di programmazione completo

Hai mai avuto bisogno di **create excel workbook c#** al volo ma non sapevi da dove cominciare? Non sei l'unico—molti sviluppatori si trovano di fronte a questo ostacolo quando automatizzano per la prima volta i report. In questa guida ti mostreremo esattamente come **create excel workbook c#** con Aspose.Cells, applicare la formattazione condizionale, importare un datatable in Excel e infine salvare il workbook come xlsx.  

Ciò che otterrai da questo tutorial è un'app console pronta‑all'uso che produce un file Excel colorato, più una spiegazione chiara di ogni riga così potrai adattarla ai tuoi progetti. Nessuna documentazione esterna necessaria; basta copiare, incollare e eseguire.  

### Prerequisiti

- .NET 6+ (o .NET Framework 4.7.2+) installato  
- Visual Studio 2022 o qualsiasi editor C# che preferisci  
- Aspose.Cells per .NET (puoi scaricare il pacchetto NuGet di prova gratuito)  

Se li hai, immergiamoci.

## Crea un workbook Excel C# – Inizializza il Workbook

La prima cosa da fare è **create excel workbook c#** istanziando la classe `Workbook`. Questo oggetto rappresenta l'intero file Excel in memoria.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Perché è importante:** La classe `Workbook` astrae il formato del file, così non devi gestire XML a basso livello o interop COM. Ti fornisce anche l'accesso a stili, tabelle e smart markers fin da subito.

## Applica la formattazione condizionale

Ora che il workbook esiste, **applichiamo la formattazione condizionale** per evidenziare le righe in cui la quantità supera 100. La formattazione condizionale vive sul foglio di lavoro, non sulla cella, il che la rende riutilizzabile.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Consiglio professionale:** Se ti servono regole più complesse (ad esempio, tra due valori), chiama semplicemente `AddCondition` di nuovo con `OperatorType.Between`.

## Scrivi intestazioni e Smart Markers

Prima di **import datatable to excel**, abbiamo bisogno di celle segnaposto—smart markers—che la libreria sostituirà con i dati reali. Pensali come tag di modello.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Perché gli smart markers?** Ti permettono di mantenere il layout di Excel separato dal codice. Progetti il foglio una volta, poi fornisci semplicemente un `DataTable` e la libreria fa il resto.

## Importa DataTable in Excel

Ecco il cuore di **import datatable to excel**. Costruiamo un `DataTable` che rispecchia i campi degli smart marker e lo passiamo a `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Caso limite:** Se la tua tabella ha più colonne di quelle necessarie, basta omettere le colonne extra dagli smart markers; verranno ignorate.

## Salva il Workbook come XLSX

Infine, **save workbook as xlsx** su disco. Il metodo `Save` determina automaticamente il formato dall'estensione del file.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

Questo è l'intero programma. Quando lo esegui, vedrai un file chiamato `SmartMarkersConditional.xlsx` nella cartella di output.

### Output previsto

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

Le righe con **Quantity > 100** (Apple e Cherry) avranno testo rosso su sfondo giallo grazie alla formattazione condizionale aggiunta in precedenza.

## Crea file Excel programmaticamente – Elenco completo del codice sorgente

Di seguito trovi il codice sorgente completo, pronto da copiare. Contiene ogni parte di cui abbiamo parlato, più qualche commento aggiuntivo per chiarezza.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Suggerimento:** Se devi generare più fogli, ripeti semplicemente i passaggi 2‑6 su una nuova istanza `Worksheet` ottenuta tramite `workbook.Worksheets.Add()`.

## Perché usare Aspose.Cells per l'automazione Excel in C#?

- **Performance:** Funziona interamente in memoria, senza interop COM, quindi è veloce anche con grandi dataset.  
- **Feature‑rich:** Supporta smart markers, formattazione condizionale, grafici, tabelle pivot e molto altro.  
- **Cross‑platform:** Funziona su Windows, Linux e macOS con .NET Core/5/6+.  

Se sei bloccato su una funzionalità specifica—ad esempio, aggiungere un grafico o proteggere un foglio—cerca semplicemente “asp​ose.cells add chart c#” e troverai un modello simile.

## Prossimi passi e argomenti correlati

- **Export to PDF:** Dopo aver **create excel workbook c#**, puoi esportare immediatamente in PDF con `workbook.Save("output.pdf")`.  
- **Leggi file Excel esistenti:** Usa `new Workbook("ExistingFile.xlsx")` per modificare un modello.  
- **Importazione bulk:** Per dati massivi, considera `ImportArray` o `ImportDataTable` con `ImportOptions` per migliorare la velocità.  

Sentiti libero di sperimentare con regole condizionali diverse, colori, o anche aggiungere una riga totale usando formule. Il cielo è il limite quando **create excel file programmatically**.

---

*Pronto a provarlo da solo? Prendi il codice, eseguilo e apri il file generato `SmartMarkersConditional.xlsx`. Se incontri problemi, lascia un commento qui sotto—buon coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}