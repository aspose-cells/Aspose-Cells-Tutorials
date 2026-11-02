---
category: general
date: 2026-07-13
description: Formatta la colonna data in Excel durante l'esportazione di una DataTable
  da C#. Impara a esportare una DataTable in Excel con C# e a importare una DataTable
  in Excel con stile in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: it
lastmod: 2026-07-13
og_description: Formatta facilmente la colonna data in Excel. Questa guida ti mostra
  come esportare una datatable in Excel con C# e importare una datatable in Excel
  con stili personalizzati.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Formattare la colonna data in Excel – Tutorial passo‑passo per l’esportazione
  C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Formattare la colonna data in Excel – Guida completa C# per esportare DataTable
url: /it/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formattare la colonna data in Excel – Guida completa C# per esportare DataTable

Ti è mai capitato di dover **format date column Excel** quando estrai dati da un database, ma le celle mostrano timestamp grezzi? Non sei l'unico. In molte applicazioni aziendali l'esportazione predefinita scarica un valore `DateTime` come `2024‑03‑15 00:00:00` e a nessuno piacciono questi dati ingombranti.  

La buona notizia è che puoi controllare l'aspetto esatto di ogni colonna direttamente da C#. In questo tutorial percorreremo una soluzione end‑to‑end che **excel export datatable c#**, applica uno stile data alla prima colonna, uno stile valuta alla seconda e infine **import datatable to excel** con formattazione senza sforzo.

Al termine avrai un metodo riutilizzabile da inserire in qualsiasi progetto .NET, indipendentemente dal fatto che tu stia usando .NET 6, .NET Framework 4.8 o una versione più recente.

---

## Di cosa avrai bisogno

- **Aspose.Cells for .NET** (o qualsiasi libreria che offra `CreateStyle` e `ImportDataTable`). I frammenti di codice usano Aspose perché la sua API è pulita e ampiamente adottata.
- Un **DataTable** che già popoli da SQL, CSV o qualsiasi altra fonte.
- Visual Studio (o il tuo IDE preferito).  
- Runtime .NET 5.0+ (l'esempio punta a .NET 6, ma i framework più vecchi funzionano allo stesso modo).

Se non hai ancora Aspose.Cells, scarica una prova gratuita dal sito ufficiale—non è necessaria la carta di credito.

---

## Passo 1: Recuperare i dati di origine come DataTable

Prima di tutto, ti serve un `DataTable`. In scenari reali proviene solitamente da `SqlDataAdapter.Fill`, ma per chiarezza simuleremo una tabella semplice:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Consiglio:** Quando estrai dati direttamente da una stored procedure, assicurati che i tipi di colonna corrispondano ai formati Excel desiderati. Una colonna `datetime` sarà in seguito il bersaglio del nostro stile **format date column excel**.

---

## Passo 2: Creare una cartella di lavoro Excel e definire gli stili delle colonne

Ora creiamo una nuova cartella di lavoro. L'astuzia per **format date column excel** consiste nel creare un oggetto `Style`, impostare la sua proprietà `Number` al formato data integrato di Excel (codice 14) e assegnare quello stile all'indice di colonna appropriato.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Perché `Number = 14`? Excel memorizza le date come numeri seriali; il formato 14 indica al programma di visualizzare quei numeri usando il modello di data breve della locale. Se ti serve un modello personalizzato (come `dd‑MMM‑yyyy`), puoi impostare `columnStyles[0].Custom = "dd-MMM-yyyy"`.

---

## Passo 3: Importare il DataTable nel foglio di lavoro con gli stili

Con l'array di stili pronto, la chiamata di importazione è una singola riga. Questo è il cuore di **excel export datatable c#** e anche il punto in cui **import datatable to excel** preservando la nostra formattazione.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

L'overload `ImportDataTable` che utilizziamo accetta l'array di stili, applicando ciascuno stile alla colonna corrispondente mentre i dati vengono scritti. Nessun ciclo di post‑elaborazione necessario—la tua colonna data è già formattata correttamente.

---

## Passo 4: Salvare la cartella di lavoro (o inviarla direttamente al browser)

A seconda dello scenario potresti salvare su disco, in uno stream di memoria, o restituire il file come risposta HTTP. Ecco tre pattern comuni:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Attenzione:** Se usi `FileResult` in ASP.NET Core, assicurati di impostare `Response.Headers["Cache-Control"] = "no-cache"` quando il file è generato al volo. Evita che il browser serva una versione obsoleta.

---

## Passo 5: Verificare il risultato – Come appare il foglio Excel

Dopo aver eseguito il codice, apri `ExportedReport.xlsx`. Dovresti vedere:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Nota come il **format date column excel** mostri una data breve pulita, mentre la colonna valuta si allinea automaticamente alle impostazioni regionali. Non è necessario formattare manualmente cella per cella.

![format date column excel example](/images/format-date-column-excel.png)

*Testo alternativo immagine: format date column excel – uno screenshot del foglio Excel con una colonna data formattata correttamente.*

---

## Domande frequenti e casi particolari

### E se il mio DataTable ha più di tre colonne?

Basta estendere l'array `columnStyles`. Per qualsiasi colonna che non formatti esplicitamente, lascia l'elemento `null`; Excel applicherà il formato predefinito Generale.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Come applicare un formato data personalizzato (es. “dd‑MMM‑yyyy”)?

Sostituisci il numero integrato con una stringa personalizzata:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Posso usare questo approccio con EPPlus o ClosedXML?

Sì, il concetto è identico: crea un oggetto stile, assegnalo a una colonna, poi carica il `DataTable`. L'API è diversa, ma il pattern **excel export datatable c#** rimane lo stesso.

### E per i DataSet di grandi dimensioni (100k+ righe)?

`ImportDataTable` è ottimizzato per scritture in blocco, ma potresti raggiungere i limiti di memoria. In tal caso, considera lo streaming delle righe con `Cells.ImportDataTable` a blocchi, o usa `Worksheet.Cells["A1"].PutValue` in un ciclo riutilizzando gli oggetti stile.

---

## Esempio completo (tutti i passaggi in un unico metodo)

Di seguito trovi un metodo autonomo che puoi copiare‑incollare in qualsiasi console app o controller ASP.NET. Dimostra l'intero flusso—dalla recupero dei dati all'esportazione Excel con stile.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Esegui il programma, apri `StyledExport.xlsx` e vedrai il **format date column excel** applicato perfettamente.

---

## Riepilogo e prossimi passi

Abbiamo appena coperto come **format date column excel** durante un **excel export datatable c#**, e come **import datatable to excel** con formattazione per colonna in una singola chiamata. I punti chiave:

1. Crea un `Style` per ogni colonna che desideri formattare.  
2. Usa `Number = 14` per le date, `Number = 2` per le valute, o qualsiasi formato personalizzato ti serva.  
3. Passa l'array di stili a `ImportDataTable`—la libreria gestisce il lavoro pesante.

Cosa potresti esplorare prossimamente?

- **Conditional formatting** per evidenziare le date scadute.  
- **

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come importare DataTable in Excel usando Aspose.Cells per .NET (Guida passo‑passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Esportare dati Excel in DataTable usando Aspose.Cells per .NET: Guida completa](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Esportare stringhe HTML da Excel a DataTable usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}