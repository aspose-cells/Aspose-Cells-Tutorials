---
category: general
date: 2026-11-19
description: Imposta il formato valuta in Excel con C# – scopri come impostare il
  formato numerico e lo stile delle colonne di Excel durante l'importazione di un
  foglio di lavoro Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: it
lastmod: 2026-11-19
og_description: Imposta il formato valuta in Excel con C# e scopri come impostare
  il formato numerico, assegnare il formato numerico e formattare le colonne di Excel
  durante l'importazione di un foglio di lavoro.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Imposta il formato valuta in Excel con C# – guida completa passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Imposta il formato valuta durante l'importazione dei dati in Excel usando C#
url: /it/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il formato valuta durante l'importazione dei dati in Excel con C#

Se hai bisogno di **impostare il formato valuta** in un foglio di lavoro Excel, questa guida ti mostra come **impostare il formato numerico** e formattare le colonne durante un **importazione di foglio di lavoro Excel**. Vedrai un esempio completo e eseguibile che assegna il formato numerico corretto a ciascuna colonna di un `DataTable` e importa i dati con lo stile desiderato.

Lavorare con Excel da C# spesso richiede più che semplicemente scaricare valori grezzi—devi anche controllare come appaiono i numeri. Che tu stia generando fatture, report finanziari o dashboard, formattare correttamente valute, percentuali o date rende l'output immediatamente leggibile.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 (o successivo) installato.
* Un riferimento a **Aspose.Cells for .NET** (o qualsiasi libreria che espone una classe `Style` con una proprietà `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Familiarità di base con `DataTable` e le collezioni C#.
* Un IDE come Visual Studio 2022 o VS Code.

## Passo 1: Recupera i dati da scrivere nel foglio di lavoro

Ottieni prima un `DataTable` che contenga i dati grezzi che desideri esportare. Nei progetti reali questo può provenire da una query al database, da una chiamata API o da un parser CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Perché è importante:** Importare un `DataTable` completamente popolato ti consente di tenere separata la logica di recupero dati dalla logica di generazione di Excel, migliorando testabilità e manutenibilità.

## Passo 2: Crea un array di stili – una voce per colonna nel DataTable

Aspose.Cells si aspetta un `Style[]` la cui lunghezza corrisponda al numero di colonne che intendi importare. Ogni elemento può contenere un formato numerico specifico.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Consiglio professionale:** Anche se hai bisogno di formattare solo un sottoinsieme di colonne, devi comunque creare un'istanza `Style` per ogni colonna; altrimenti otterrai una `NullReferenceException` durante l'importazione.

## Passo 3: Assegna il formato numerico alle colonne desiderate

I numeri di stile incorporati differiscono a seconda della libreria. In Aspose.Cells:

* `0` → Generale (intero)  
* `2` → Valuta (es., `$#,##0.00`)  
* `3` → Data, ecc.

Qui **assegniamo il formato numerico** a due colonne: la prima colonna (Id) rimane un intero, mentre la seconda colonna (Amount) riceve un formato valuta.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Come impostare il formato numerico:** Usare la proprietà `Number` è il modo più rapido per scegliere un formato incorporato. Per valute specifiche della locale, considera l'uso di una stringa di formato personalizzata che includa il simbolo di valuta appropriato.

## Passo 4: Importa il DataTable nel foglio di lavoro, applicando gli stili delle colonne

Ora che l'array di stili è pronto, importa i dati. Il metodo `ImportDataTable` rispetta gli stili che hai passato.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Risultato atteso

Quando apri **FinancialReport.xlsx**, vedrai:

| Id | Importo    | Descrizione          |
|----|------------|----------------------|
| 1  | $1,234.56  | Forniture per ufficio |
| 2  | $98,765.43 | Compensi di consulenza |
| 3  | $0.99      | Varie                |

*La colonna **Importo** viene visualizzata usando il formato valuta impostato, mentre **Id** rimane un intero.*

## Come impostare il formato numerico per scenari aggiuntivi

### Assegna il formato numerico alle colonne data

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Usa formati numerici personalizzati per le percentuali

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Formattazione oltre i formati numerici

Puoi anche impostare carattere, colore di sfondo o allineamento sullo stesso oggetto `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Perché funziona:** L'oggetto `Style` aggrega tutte le proprietà visive per una cella. Quando passi l'array a `ImportDataTable`, ogni cella eredita automaticamente lo stile definito.

## Problemi comuni e come evitarli

| Problema | Sintomo | Correzione |
|----------|---------|------------|
| Dimenticare di istanziare ogni `Style` | `NullReferenceException` durante l'importazione | Itera sull'array e chiama `CreateStyle()` prima di impostare le proprietà. |
| Usare l'indice numerico incorporato sbagliato | Formato errato (es., le date appaiono come interi) | Consulta la documentazione della libreria per i corretti costanti `Number`. |
| Non salvare la cartella di lavoro | Nessun file di output o file vuoto | Chiama `workbook.Save(...)` dopo il completamento dell'importazione. |
| Mancata corrispondenza della locale per il simbolo di valuta | `$` appare anche in locale non‑US | Usa una stringa di formato personalizzata con il simbolo appropriato (es., `"€#,##0.00"`). |

## Esempio completo e eseguibile



## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea file excel c# – formatta celle e imposta formato valuta](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Come formattare le colonne Excel in C# – Guida completa](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Crea cartella di lavoro Excel C# – Applica formato valuta e importa DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}