---
category: general
date: 2026-10-07
description: Crea fogli di dettaglio duplicati in Excel usando C#. Scopri come generare
  più fogli di lavoro e creare un report da tabelle in un'unica esecuzione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: it
lastmod: 2026-10-07
og_description: Crea fogli di dettaglio duplicati in Excel con C#. Questo tutorial
  mostra come generare più fogli di lavoro e produrre un report Excel completo a partire
  da tabelle.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Crea fogli di dettaglio duplicati in Excel – guida passo‑passo C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Crea fogli di dettaglio duplicati in Excel usando C#
url: /it/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea fogli di dettaglio duplicati in Excel usando C#

Se hai bisogno di **creare fogli di dettaglio duplicati** in una cartella di lavoro Excel, questa guida ti accompagna passo passo nel processo completo. Vedrai come **generare più fogli di lavoro** da un set di dati master‑detail e produrre un report Excel rifinito direttamente dalle tabelle.

Generare un report Excel dalle tabelle è una necessità comune per sistemi di fatturazione, dashboard di inventario o qualsiasi scenario in cui un record master ha diverse righe di dettaglio correlate. Alla fine di questo tutorial avrai un programma C# eseguibile che crea una cartella di lavoro con un foglio master e un foglio con nome unico per ogni gruppo di dettaglio.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 (o successivo) installato  
* Visual Studio 2022 o qualsiasi IDE compatibile con C#  
* Il pacchetto NuGet **Aspose.Cells for .NET** (fornisce `SmartMarkerProcessor`)  

Puoi aggiungere il pacchetto con il seguente comando:

```bash
dotnet add package Aspose.Cells
```

## Panoramica della soluzione

La soluzione segue questi cinque passaggi:

1. **Ottenere la fonte dati** che contiene una tabella master e due tabelle detail.  
2. **Configurare il processore Smart‑marker** affinché ogni foglio di dettaglio duplicato riceva un nome unico.  
3. **Creare una nuova cartella di lavoro** e inserire uno smart‑marker che fa riferimento alla tabella master.  
4. **Eseguire il processore** per generare il foglio master e tutti i fogli detail.  
5. **Salvare la cartella di lavoro** – ogni foglio detail ora ha un nome distinto.

Ogni passaggio è spiegato in dettaglio di seguito, con codice completo e motivazioni.

## Passo 1: Ottenere la fonte dati che contiene una tabella master e due tabelle detail

Il primo compito è costruire un `DataSet` che imiti i dati che normalmente otterresti da un database. Il `DataSet` deve contenere una tabella chiamata **Master** e una o più tabelle chiamate **Detail**. Il motore Smart‑marker utilizza questi nomi di tabella per popolare la cartella di lavoro.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Perché è importante:**  
*Smart‑marker* funziona con oggetti `DataSet`; ogni nome di tabella diventa un marker che il motore può sostituire. Strutturando i dati in questo modo permetti al processore di duplicare automaticamente il foglio detail per ogni `InvoiceId` distinto.

## Passo 2: Configurare il processore Smart‑marker per assegnare a ogni foglio detail duplicato un nome unico

Quando il processore incontra un marker detail, crea un nuovo foglio di lavoro per ogni gruppo di righe. Per impostazione predefinita i nuovi fogli condividono lo stesso nome, il che genera un conflitto di denominazione. Impostare `DetailSheetNewName` indica al motore come rinominare ogni copia.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Perché è importante:**  
Senza un modello di denominazione unico la cartella di lavoro genererebbe un'eccezione quando il processore tenta di aggiungere un secondo foglio detail. Il segnaposto `{0}` garantisce che ogni foglio riceva un nome distinto e prevedibile.

## Passo 3: Creare una nuova cartella di lavoro e inserire uno smart‑marker che fa riferimento alla tabella master

Ora crei un nuovo `Workbook`, aggiungi un marker che punta alla tabella **Master**, e opzionalmente formatti la riga di intestazione.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Perché è importante:**  
Il marker `{{Master}}` indica al processore di espandere la tabella master a partire da `A1`. Le righe successive diventano le righe di dati per ogni record master. Questo è il punto di ingresso per **generate excel report from tables**.

## Passo 4: Eseguire il processore smart‑marker per generare il foglio master e i fogli detail

Con la fonte dati, il processore e il modello pronti, invochi `Process`. Il motore espande il marker master, poi crea un foglio detail separato per ogni `InvoiceId` distinto.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Perché è importante:**  
`processor.Process` esegue il lavoro pesante: legge le righe master, crea un foglio detail per ogni chiave unica e rinomina quei fogli secondo il modello definito in precedenza. Il risultato è una cartella di lavoro che soddisfa il requisito **how to generate multiple worksheets**.

## Passo 5: Salvare la cartella di lavoro risultante – ogni foglio detail ora ha un nome distinto

La chiamata `Save` scrive il file su disco. Quando apri la cartella di lavoro, vedrai:

* **Sheet1** – il foglio master contenente le intestazioni delle fatture.  
* **Detail_1**, **Detail_2**, … – ogni foglio contiene le righe della tabella **Detail** che appartengono a una fattura specifica.

Di seguito è presente un mock‑up del layout previsto della cartella di lavoro (l'immagine è illustrativa; puoi sostituirla con uno screenshot reale se lo desideri).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Output previsto

| Nome foglio | Descrizione contenuto |
|------------|----------------------|
| **Sheet1** | Righe master: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Righe detail dove `InvoiceId = 101` |
| **Detail_2** | Righe detail dove `InvoiceId = 102` |

Aprendo `DuplicatedDetailSheets.xlsx` dovresti vedere esattamente questa struttura.

## Codice sorgente completo (pronto da copiare)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come nominare i fogli automaticamente – Generare più fogli in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Come creare fogli di lavoro – Guida passo‑passo per la generazione dinamica di Excel](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Come generare un report Excel in C# – Guida completa usando SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}