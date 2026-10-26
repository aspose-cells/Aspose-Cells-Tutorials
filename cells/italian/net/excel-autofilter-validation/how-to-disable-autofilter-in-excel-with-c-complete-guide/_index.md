---
category: general
date: 2026-10-26
description: disabilita l'autofiltro in Excel usando C#. Questo tutorial mostra come
  rimuovere l'autofiltro da una tabella Excel programmaticamente e include un esempio
  completo funzionante.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: it
lastmod: 2026-10-26
og_description: Disabilita rapidamente l'autofiltro in Excel. Segui questa guida per
  rimuovere l'autofiltro da una tabella Excel usando C# e Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Disabilita l'autofiltro in Excel con C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Come disabilitare l'autofiltro in Excel con C# – guida completa
url: /it/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come disabilitare l'autofiltro in Excel con C# – guida completa

Se hai bisogno di **disabilitare l'autofiltro in Excel**, questa guida ti mostra esattamente come farlo da C#. Che tu stia pulendo un report prima della pubblicazione o automatizzando una pipeline di esportazione dati, rimuovere il filtro garantisce che il foglio di lavoro mostri ogni riga. Imparerai anche come **rimuovere l'autofiltro da una tabella Excel** con una singola chiamata affidabile.

Utilizzeremo la popolare libreria **Aspose.Cells for .NET** perché funziona senza richiedere l'installazione di Excel sul server. Alla fine di questo tutorial avrai un'applicazione console autonoma che carica una cartella di lavoro, trova la prima tabella e disabilita il suo autofiltro. La soluzione funziona con file .xlsx creati da Excel 2007 o versioni successive.

## Cosa ti servirà

| Prerequisito | Perché è importante |
|--------------|---------------------|
| .NET 6.0 or later | Fornisce il runtime per il codice C#. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Consente l'accesso programmatico a fogli di lavoro, tabelle e autofiltri. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | Un file Excel di esempio (`Sample.xlsx`) che contiene almeno una tabella con un autofiltro applicato. Il codice opera sulla prima tabella; avere una tabella ci permette di dimostrare la disattivazione del filtro. |
| Visual Studio 2022 (or any C# IDE) | Rende la compilazione e il debug dell'app console semplici. |

> **Suggerimento:** Se preferisci un'alternativa gratuita, puoi adattare il codice per usare **ClosedXML** o **EPPlus**; l'idea principale—impostare la proprietà `AutoFilter` della tabella a `null`—rimane la stessa.

## Passo 1: Crea un nuovo progetto console

Apri un terminale o il prompt dei comandi di Visual Studio e esegui:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

Questo crea un nuovo progetto chiamato `ExcelFilterDemo` e include la libreria Aspose.Cells.

## Passo 2: Carica la cartella di lavoro e individua il primo foglio di lavoro

La prima operazione logica è aprire il file della cartella di lavoro. Aspose.Cells legge il file in un oggetto `Workbook` che ti dà accesso diretto a fogli di lavoro e tabelle.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Perché questo passo?** Caricare la cartella di lavoro è necessario prima di poter manipolare qualsiasi oggetto Excel. Usare il primo foglio di lavoro (`Worksheets[0]`) rispecchia lo scenario tipico in cui i dati principali si trovano sul primo foglio.

## Passo 3: Recupera la prima tabella definita sul foglio di lavoro

Le tabelle Excel (chiamate anche ListObjects) sono i contenitori che ospitano dati strutturati. Ogni tabella può avere il proprio autofiltro. Per rimuovere il filtro dobbiamo prima ottenere un riferimento all'oggetto tabella.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Caso limite:** Se la cartella di lavoro può contenere fogli senza tabelle, avvolgi l'accesso in un controllo `if (worksheet.Tables.Count > 0)`. Questo previene errori di runtime e rende la soluzione robusta.

## Passo 4: Disabilita l'autofiltro per la tabella

La disabilitazione effettiva è una singola riga: assegna `null` alla proprietà `AutoFilter` dell'oggetto `Table`. Questo cancella qualsiasi criterio di filtro e rimuove le frecce a discesa dalla riga di intestazione.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Dopo l'esecuzione di questa riga, la tabella si comporta come un intervallo normale senza interfaccia di filtro.

## Passo 5: Salva la cartella di lavoro modificata

Infine, scrivi le modifiche su disco. Puoi sovrascrivere il file originale o crearne uno nuovo per mantenere intatto l'originale.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Codice sorgente completo

Mettendo insieme tutti i pezzi, il programma completo appare così:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Esegui il programma con `dotnet run`. Dopo l'esecuzione, apri `Sample_NoFilter.xlsx` in Excel; vedrai che le frecce del filtro sono scomparse e tutte le righe sono visibili.

## Verifica che l'autofiltro sia davvero rimosso

1. Apri il file salvato (`Sample_NoFilter.xlsx`) in Microsoft Excel.  
2. Fai clic su qualsiasi intestazione di colonna – non dovresti vedere la freccia a discesa del filtro.  
3. Se vedi ancora le frecce, verifica che la tabella a cui hai puntato sia effettivamente quella con il filtro. Puoi elencare tutte le tabelle con:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

L'output della console dovrebbe riportare `Has AutoFilter: False` per la tabella che hai modificato.

## Problemi comuni e come evitarli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | Il foglio di lavoro non contiene tabelle. | Aggiungi un controllo `if (worksheet.Tables.Count == 0)` prima di accedere. |
| Il file salvato mostra ancora i filtri | Hai modificato il foglio o la tabella sbagliati. | Usa `wb.Worksheets["SheetName"]` o itera attraverso `wb.Worksheets` per individuare la tabella corretta. |
| Il programma si arresta su versioni .NET più vecchie | Aspose.Cells richiede .NET 6.0+ per il pacchetto più recente. | Aggiorna il framework di destinazione nel file `.csproj`. |
| NullReferenceException quando `table.AutoFilter` è già null | Hai chiamato il codice due volte sullo stesso file senza ricaricarlo. | Ricarica la cartella di lavoro o verifica `if (table.AutoFilter != null)` prima di assegnare. |

## Estendere la soluzione

Ora che sai come **disabilitare l'autofiltro in Excel**, potresti voler:

* **Rimuovere l'autofiltro da una tabella Excel** solo quando è soddisfatta una condizione specifica (ad esempio, quando è impostata una flag utente). Aggiungi una dichiarazione `if` attorno a `table.AutoFilter = null;`.
* **Applicare un nuovo filtro** programmaticamente dopo aver cancellato quello vecchio, usando `table.AutoFilter.Range` e `table.AutoFilter.AddFilterColumn(...)`.
* **Elaborare più tabelle** nella stessa cartella di lavoro iterando su `worksheet.Tables` e disabilitando ogni filtro.

Queste estensioni seguono lo stesso modello mostrato sopra e mantengono il codice pulito.

## Conclusione

Ora hai un metodo conciso e pronto per la produzione per **disabilitare l'autofiltro in Excel** usando C#. Caricando la cartella di lavoro, accedendo alla prima tabella e impostando `table.AutoFilter = null`, rimuovi efficacemente **l'autofiltro da una tabella Excel** senza intervento manuale. L'esempio completo compila, viene eseguito e produce un file pulito pronto per ulteriori automazioni o distribuzioni.

Sentiti libero di sperimentare con tabelle aggiuntive, logica condizionale o librerie alternative. Se incontri casi limite, fai riferimento alla sezione di risoluzione dei problemi o esplora l'ampia documentazione di Aspose.Cells per la gestione avanzata dei filtri. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to remove autofilter from Excel tables using C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}