---
category: general
date: 2026-08-11
description: Crea un foglio Excel da una DataTable in C# ed esporta la DataTable in
  Excel con denominazione automatica del foglio. Scopri come aggiungere righe alla
  DataTable e salvare la cartella di lavoro come xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: it
lastmod: 2026-08-11
og_description: Crea un foglio Excel da una DataTable in C#. Questo tutorial mostra
  come esportare una DataTable in Excel, aggiungere righe alla DataTable, generare
  più fogli Excel e salvare la cartella di lavoro come xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Crea un foglio Excel da una DataTable in C# – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Crea un foglio Excel da una DataTable in C# – guida passo passo
url: /it/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un foglio Excel da una DataTable in C# – guida passo‑passo

Se hai bisogno di **creare un foglio excel** da una `DataTable` in C#, questa guida ti mostra esattamente come farlo. Vedrai come **esportare la datatable in excel**, aggiungere righe, gestire nomi di fogli duplicati e, infine, **salvare la cartella di lavoro come xlsx**.

L'esempio utilizza Aspose.Cells, una libreria .NET ampiamente usata per l'automazione di Excel. Gli stessi concetti si applicano ad altre librerie che supportano l'elaborazione in stile SmartMarker, ma il codice qui sotto funziona subito con Aspose.Cells 22.12 o versioni successive.

## Prerequisiti

* .NET 6.0 SDK o versioni successive installate  
* Un riferimento al pacchetto NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Familiarità di base con `DataTable` e le applicazioni console C#  

Questi requisiti mantengono il tutorial autonomo ed evitano l'uso di strumenti esterni.

## Passo 1: Crea una DataTable da esportare in Excel

Il primo passo è creare una `DataTable` che rispecchi i dati che desideri nel foglio di lavoro. Qui creiamo una tabella chiamata **Sheet1**, aggiungiamo una colonna `Id` e inseriamo due righe.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Perché è importante:**  
`DataTable` è una comoda rappresentazione in‑memoria di dati tabulari. Dare alla tabella il nome `"Sheet1"` indica ad Aspose.Cells quale foglio mirare durante l'elaborazione dei SmartMarkers.

## Passo 2: Aggiungi righe alla DataTable (espansione opzionale)

Se i dati di origine sono dinamici, spesso dovrai aggiungere righe in un ciclo. Il frammento seguente dimostra un modello tipico:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Suggerimento:** Quando aggiungi molte righe, considera di disabilitare i vincoli (`dataTable.Constraints.Clear()`) per migliorare le prestazioni.

## Passo 3: Configura le opzioni SmartMarker per creare più fogli excel automaticamente

Le opzioni SmartMarker ti consentono di controllare come gestire i nomi di fogli duplicati. Impostare `DetailSheetNewName` a `"Sheet1_{0}"` indica ad Aspose.Cells di rinominare i fogli successivi come `Sheet1_1`, `Sheet1_2` e così via.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Perché è importante:**  
Quando elabori diversi oggetti `DataTable` che condividono lo stesso nome, Excel normalmente genera un errore perché i nomi dei fogli devono essere unici. Il pattern `DetailSheetNewName` elimina automaticamente quel conflitto.

## Passo 4: Elabora i SmartMarkers ed esporta la datatable in excel

Ora creiamo un nuovo `Workbook`, eseguiamo `ProcessSmartMarkers` e lasciamo che Aspose.Cells popoli il(i) foglio(i) di lavoro in base alla `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Spiegazione:**  
`ProcessSmartMarkers` analizza la cartella di lavoro alla ricerca di marker come `&=Sheet1!A1` (non mostrati qui) e li sostituisce con i dati provenienti da `dataTable`. Poiché abbiamo iniziato con una cartella di lavoro vuota, Aspose.Cells crea un nuovo foglio corrispondente al nome della tabella e lo riempie con le righe che abbiamo aggiunto.

## Passo 5: Salva la cartella di lavoro come xlsx

Infine, scrivi la cartella di lavoro su disco con il moderno formato OpenXML (`.xlsx`). Puoi modificare il percorso per adattarlo al tuo ambiente.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Risultato:**  
Eseguendo il programma si genera un file Excel che contiene:

| Nome foglio | Righe |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (se un'altra DataTable con lo stesso nome fosse elaborata) |

La logica di rinominare i fogli garantisce **creare più fogli excel** senza gestire manualmente i nomi.

## Varianti comuni e casi limite

| Situazione | Come gestirla |
|-----------|------------------|
| **Tabelle molto grandi** (≥ 100 000 righe) | Usa `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` prima dell'elaborazione per mantenere basso l'utilizzo di memoria. |
| **Ordine personalizzato delle colonne** | Riordina gli oggetti `DataColumn` nella `DataTable` prima di chiamare `ProcessSmartMarkers`. |
| **Multiple DataTable con nomi diversi** | Chiama `ProcessSmartMarkers` per ogni tabella; Aspose.Cells creerà automaticamente un foglio separato per ogni nome. |
| **Necessità di una riga di intestazione con stile** | Dopo l'elaborazione, accedi a `Worksheet.Cells["A1"]` e applica le proprietà `Style` (font, sfondo). |
| **Salvataggio su stream invece che su file** | Sostituisci `workbook.Save(outputPath, SaveFormat.Xlsx)` con `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Consiglio professionale:** Avvolgi sempre le operazioni sul file system in blocchi `try…catch` per rilevare subito eventuali problemi di permessi.

## Codice sorgente completo (pronto da copiare)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Output previsto

Eseguendo il programma stampa:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Aprendo `DuplicateSheets.xlsx` si vede un foglio chiamato **Sheet1** con la colonna `Id` contenente i valori `1, 2, 3, 4, 5`. Se in seguito elabori un'altra `DataTable` chiamata `"Sheet1"` nella stessa cartella di lavoro, Aspose.Cells creerà automaticamente **Sheet1_1**, **Sheet1_2**, ecc.

## Conclusione

Ora sai come **creare un foglio excel** da una `DataTable` in C#, **esportare la datatable in excel**, **aggiungere righe alla datatable**, generare **creare più fogli excel** con denominazione automatica e **salvare la cartella di lavoro come xlsx**. L'esempio completo e eseguibile dimostra il flusso di lavoro end‑to‑end e fornisce consigli pratici per set di dati di grandi dimensioni e per lo styling personalizzato.

### Cosa fare dopo?

* Esplora la **formattazione delle celle** (font, colori, bordi) accedendo a `Worksheet.Cells` dopo `ProcessSmartMarkers`.  
* Usa i **cicli SmartMarker** per generare report master‑detail in un'unica cartella di lavoro.  
* Passa all'**esportazione CSV** modificando `SaveFormat.Csv` se ti serve una rappresentazione in testo semplice.  

Sentiti libero di adattare il codice alle tue fonti di dati—che si tratti di una query al database, di una risposta API o di una collezione in‑memoria. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare e salvare una cartella di lavoro Excel come ODS usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Come creare e salvare una cartella di lavoro Excel come SVG usando Aspose.Cells per Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java | Guida alle operazioni di cartella di lavoro](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}