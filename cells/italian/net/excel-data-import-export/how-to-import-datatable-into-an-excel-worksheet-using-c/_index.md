---
category: general
date: 2026-10-26
description: Scopri come importare una DataTable in un foglio di lavoro Excel con
  C# e Aspose.Cells, preservando stili e intestazioni in poche righe di codice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: it
lastmod: 2026-10-26
og_description: come importare una DataTable in un foglio di lavoro Excel usando C#
  e Aspose.Cells. Segui questa guida completa per preservare stili, intestazioni e
  formattazione.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Come importare DataTable in un foglio di lavoro Excel – Guida passo‑passo
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Come importare DataTable in un foglio di lavoro Excel usando C#
url: /it/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come importare DataTable in un foglio di lavoro Excel usando C#

Se hai bisogno di **how to import datatable** in un foglio di lavoro Excel, questa guida mostra i passaggi esatti in C#. Che tu stia costruendo un motore di reporting o esportando dati da una griglia, vedrai come mantenere intatti gli header delle colonne e gli stili delle celle con Aspose.Cells. La soluzione funziona con .NET 6+ e richiede solo poche righe di codice.

Importare una DataTable è un'operazione comune quando si lavora con i fogli di calcolo, ma gli sviluppatori spesso dimenticano di abilitare il trasferimento degli stili o di passare correttamente il flag dell'header. In questo tutorial imparerai a configurare **ImportTableOptions**, attivare **ImportDataTableStyle** e chiamare `ImportDataTable` in modo sicuro. Alla fine avrai un metodo pronto all'uso che potrai inserire in qualsiasi progetto C#.

## Prerequisiti

* .NET 6 SDK o versioni successive installate.
* Una copia con licenza di **Aspose.Cells for .NET** (la versione di prova gratuita funziona per i test).
* Familiarità di base con `DataTable` e i concetti di Excel.
* Un IDE come Visual Studio 2022 (qualsiasi editor che supporta C# funziona).

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.Cells`.

## Passo 1: Recuperare i dati di origine in una DataTable

La prima cosa da fare quando rispondi a **how to import datatable** è avere i dati pronti. Nella maggior parte degli scenari reali la `DataTable` proviene da una query al database, da un parser CSV o da una collezione in memoria. Ecco un esempio minimale che crea una tabella con alcune righe:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Perché è importante*: Costruendo prima la `DataTable`, controlli l'ordine delle colonne, i tipi di dati e i nomi degli header—tutto ciò viene preservato quando successivamente importi la tabella in un foglio di lavoro Excel.

## Passo 2: Creare `ImportTableOptions` e abilitare l'importazione degli stili

Quando rispondi a **how to import datatable**, la decisione successiva è se desideri lo stile visivo (font, colori, bordi) già definito nella `DataTable` di origine. Aspose.Cells fornisce la classe `ImportTableOptions` per un controllo fine. Impostare `ImportDataTableStyle = true` copia le informazioni di stile nel foglio di destinazione.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Perché è importante*: Senza abilitare `ImportDataTableStyle`, le celle importate userebbero lo stile predefinito del foglio, perdendo qualsiasi formattazione personalizzata applicata alla `DataTable`. Questo flag è essenziale per un'esportazione curata.

## Passo 3: Importare la DataTable nel foglio di lavoro, includendo gli header

Ora hai tutto il necessario per rispondere a **how to import datatable** in un file Excel. Crei una cartella di lavoro, scegli un foglio di lavoro e chiami `ImportDataTable`. Il secondo argomento del metodo (`true`) indica ad Aspose.Cells di scrivere gli header delle colonne come prima riga.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Eseguendo `ExportDataTableToExcel("Employees.xlsx")` si genera un file `Employees.xlsx` in cui la prima riga contiene **Id**, **Name** e **Department**, e ogni cella mantiene lo stile definito nella `DataTable` originale.

### Esempio completo eseguibile

Di seguito trovi un programma console completo e autonomo che dimostra **how to import datatable** e salva il risultato nella directory corrente. Copialo e incollalo in un nuovo progetto console e eseguilo.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Output previsto**  
Quando apri `Employees.xlsx`, vedrai:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Tutte le celle mantengono lo stile predefinito della DataTable (font, allineamento). Se hai applicato stili personalizzati alla `DataTable` prima dell'importazione, quegli stili appaiono identicamente nel foglio di lavoro perché `ImportDataTableStyle` è impostato su `true`.

## Problemi comuni e consigli di best‑practice

| Problema | Perché accade | Come evitarlo |
|----------|----------------|---------------|
| **Headers missing** | Passare `false` come secondo argomento a `ImportDataTable` salta i nomi delle colonne. | Usa sempre `true` quando ti servono gli header, oppure scrivili manualmente prima dell'importazione. |
| **Style not transferred** | Dimenticare di abilitare `ImportDataTableStyle`. | Imposta `ImportDataTableStyle = true` in `ImportTableOptions`. |
| **Large tables cause performance lag** | Importare milioni di righe senza paginazione. | Importa in batch o usa `ImportDataTable` con la sovraccarico `startRow` per lo streaming dei dati. |
| **Incorrect worksheet reference** | Usare `workbook.Worksheets[1]` quando esiste solo un foglio. | Usa `workbook.Worksheets[0]` o crea un nuovo foglio con `workbook.Worksheets.Add()`. |
| **License expiration** | La versione di prova di Aspose.Cells mostra una filigrana dopo 30 giorni. | Applica una licenza valida con `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Consiglio professionale**: Se devi applicare un tema personalizzato dopo l'importazione, chiama `ws.Cells.ApplyStyle(style)` dove `style` è un oggetto `Style` che configuri una volta e riutilizzi per le righe.

## Estendere la soluzione

Ora che conosci **how to import datatable**, puoi esplorare scenari correlati:

* **Importing multiple tables** – ripeti l'importazione su fogli di lavoro diversi.
* **Conditional formatting** – dopo l'importazione, aggiungi regole con `ws.Cells.ApplyConditionalFormatting`.
* **Exporting to CSV** – usa `workbook.Save("file.csv", SaveFormat.Csv)` se è richiesto un formato di testo semplice.
* **Reading back into a DataTable** – usa `ws.Cells.ExportDataTable` per verificare l'integrità del round‑trip.

Tutte queste estensioni si basano sul modello di base mostrato sopra: recuperare i dati, configurare le opzioni di importazione e chiamare un unico metodo Aspose.Cells.

## Conclusione

Ora hai una risposta completa e pronta per la produzione a **how to import datatable** in un foglio di lavoro Excel usando C#. Il tutorial ha coperto il recupero dei dati di origine, la configurazione di `ImportTableOptions` con `ImportDataTableStyle` e l'esecuzione dell'importazione con `ImportDataTable`. Seguendo l'esempio di codice manterrai automaticamente gli header e gli stili, e potrai adattare il modello a set di dati più grandi, più fogli o esigenze di formattazione aggiuntive.

Pronto a automatizzare il tuo flusso di lavoro di reporting? Prova a sostituire la `DataTable` di esempio con una query reale al database, sperimenta con stili di cella personalizzati e integra il metodo nel tuo livello di servizio esistente. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come importare array in Excel usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [Come importare dati XML in Excel con Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [Come importare DataTables formattati in HTML in Excel usando Aspose.Cells per .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}