---
category: general
date: 2026-10-10
description: Applica rapidamente il formato numerico in Excel importando una DataTable,
  impostando i formati data e valuta e preservando la riga di intestazione in un unico
  passaggio.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: it
lastmod: 2026-10-10
og_description: Applica il formato numerico di Excel in C# usando Aspose.Cells. Impara
  a impostare il formato data di Excel, il formato valuta di Excel e a preservare
  la riga di intestazione di Excel durante l'importazione di una DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Applica il formato numerico di Excel in C# – guida passo‑a‑passo
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Come applicare il formato numerico in Excel con Aspose.Cells
url: /it/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come applicare il formato numerico in Excel con Aspose.Cells

Se hai bisogno di **applicare il formato numerico in Excel** durante il caricamento dei dati da un `DataTable`, questa guida ti mostra esattamente come fare. Imparerai anche a **impostare il formato data in Excel**, **impostare il formato valuta in Excel** e a **preservare la riga di intestazione in Excel** durante l'importazione, così il foglio di lavoro risultante avrà un aspetto professionale senza ulteriori post‑processing.

Copriamo tutto, dall'installazione della libreria alla scrittura di uno snippet completo e eseguibile. Alla fine sarai in grado di importare qualsiasi `DataTable` in una cartella di lavoro Excel, formattare automaticamente le colonne numeriche e mantenere intatta la riga di intestazione—tutto in poche righe di C#.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+)
* Visual Studio 2022 (o qualsiasi IDE C# tu preferisca)
* **Aspose.Cells for .NET** – installa via NuGet:

```bash
dotnet add package Aspose.Cells
```

* Una sorgente `DataTable` – l'esempio utilizza un metodo di supporto `GetTable()` che restituisce dati di esempio.

> **Pro tip:** Aspose.Cells è una libreria commerciale, ma offre una modalità di valutazione gratuita che disabilita il watermark per un massimo di 30 giorni.

## Passo 1: Creare una cartella di lavoro e accedere al primo foglio

L'oggetto workbook è il punto di ingresso per tutte le operazioni Excel. Creare un nuovo workbook ti fornisce un foglio di lavoro predefinito all'indice 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Perché questo passo?*  
`Workbook` gestisce il formato file, il motore di calcolo e il repository degli stili. Accedere al `Worksheet` subito ci permette di passare il foglio di destinazione al metodo di importazione in seguito.

## Passo 2: Recuperare i dati sorgente come DataTable

Nei progetti reali i dati provengono spesso da una query al database, da un parser CSV o da una risposta API. Per illustrazione generiamo un semplice `DataTable` con tre colonne: **Product**, **Price**, e **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Perché questo passo?*  
Un `DataTable` fornisce una rappresentazione tabellare in memoria che Aspose.Cells può importare direttamente, preservando l'ordine delle colonne e i tipi di dato.

## Passo 3: Preparare un array di `Style` – uno stile per colonna

Aspose.Cells ti consente di applicare uno stile distinto a ciascuna colonna durante l'importazione passando un array di oggetti `Style`. La lunghezza dell'array deve corrispondere al numero di colonne nella tabella sorgente.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Perché questo passo?*  
Se si omette la creazione esplicita (`CreateStyle()`), il tentativo di impostare `Number` genererà una `NullReferenceException`. Inizializzare ogni `Style` garantisce che le assegnazioni successive abbiano successo.

## Passo 4: Assegnare i formati numerici – valuta e data

Excel identifica i formati numerici integrati tramite ID.  
* **14** – Valuta (es. `$1,234.00`)  
* **22** – Data breve (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Nota:** Se ti serve un formato personalizzato (es. `"¥#,##0.00"`), usa `Style.Custom = "¥#,##0.00"` invece di un ID integrato.

*Perché questo passo?*  
Applicare il **formato numerico** corretto al momento dell'importazione elimina la necessità di un secondo passaggio che scorre le celle per cambiare la formattazione. Garantisce inoltre che il **format excel cells date** e il **set currency format excel** siano coerenti in tutte le righe.

## Passo 5: Importare il DataTable preservando la riga di intestazione

Il metodo `ImportDataTable` può copiare i dati, mantenere la prima riga come intestazione e applicare gli stili di colonna che abbiamo preparato.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Output previsto** – Apri `FormattedReport.xlsx` e vedrai:

| Prodotto | Prezzo (valuta) | Data di rilascio (data) |
|----------|-----------------|--------------------------|
| Widget A | $12.99          | 05/01/2023               |
| Widget B | $23.50          | 06/15/2023               |
| Widget C | $7.75           | 07/30/2023               |

La riga di intestazione è intatta, la colonna **Prezzo** mostra il simbolo della valuta e la colonna **Data di rilascio** visualizza il formato data breve—tutto senza alcun ulteriore codice di stile.

### Gestione dei casi limite più comuni

| Situazione                                 | Soluzione |
|--------------------------------------------|-----------|
| **Più colonne rispetto agli stili**        | Assicurati che `columnStyles.Length` sia uguale a `sourceTable.Columns.Count`. Le voci mancanti usano lo stile predefinito del workbook. |
| **Valori null nelle colonne numeriche**    | Excel tratta `null` come cella vuota; il formato numerico si applica comunque quando viene inserito un valore. |
| **Valuta locale personalizzata**           | Usa `columnStyles[i].Custom = "\"€\"#,##0.00"` e imposta `columnStyles[i].Number = -1` per disabilitare l'ID integrato. |
| **Tabelle molto grandi ( > 100 000 righe )**| Considera l'overload di `ImportDataTable` con `ImportTableOptions` per lo streaming dei dati e ridurre il carico di memoria. |
| **Applicare lo stesso stile a più colonne**| Riutilizza la stessa istanza `Style` nell'array (es. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Utilizzare una stringa di formato personalizzata

Se gli ID integrati non soddisfano le tue esigenze, puoi definire un formato numerico personalizzato:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Questo approccio ti dà il pieno controllo su **format excel cells date** e **set currency format excel** oltre gli ID predefiniti.

## Conclusione

Ora sai come **applicare il formato numerico in Excel** in modo efficiente quando importi un `DataTable` con Aspose.Cells. Creando un array di `Style` per colonna, assegnando ID numerici integrati o personalizzati e usando l'overload di `ImportDataTable` che **preserve header row excel**, puoi generare fogli di lavoro pronti per la pubblicazione in un'unica operazione.

### Cosa fare dopo?

* Esplora **set date format excel** con pattern personalizzati come `"dddd, mmmm dd, yyyy"`.
* Combina questa tecnica con **conditional formatting** per evidenziare valori fuori intervallo.
* Usa **format excel cells date** in tabelle pivot o grafici per report dinamici.

Sentiti libero di sperimentare con diversi ID numerici o stringhe personalizzate per adeguarti alla guida di stile della tua organizzazione. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [apply number format excel – Guida passo‑a‑passo per formattare le colonne](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Applicare il formato valuta e importare DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Guida completa al formato di importazione](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}