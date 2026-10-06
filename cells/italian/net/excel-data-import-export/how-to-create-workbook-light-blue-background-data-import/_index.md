---
category: general
date: 2026-02-09
description: Come creare una cartella di lavoro in C# con uno sfondo azzurro chiaro
  e importare dati con intestazioni. Impara ad aggiungere uno sfondo azzurro chiaro,
  utilizzare lo stile predefinito di Excel e importare un DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: it
og_description: Come creare una cartella di lavoro in C# con uno sfondo azzurro chiaro,
  importare dati con intestazioni e applicare lo stile predefinito di Excel—tutto
  in una guida concisa.
og_title: Come creare una cartella di lavoro – Sfondo azzurro chiaro, importazione
  dati
tags:
- C#
- Excel
- Aspose.Cells
title: Come creare una cartella di lavoro – Sfondo azzurro chiaro, importazione dati
url: /it/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un Workbook – Sfondo azzurro chiaro, importazione dati

Ti sei mai chiesto **how to create workbook** in C# che abbia un aspetto un po' più gradevole subito fuori dalla scatola? Forse hai estratto una `DataTable` da un database e sei stanco delle celle bianche e noiose di default. In questo tutorial vedremo come creare un nuovo workbook, aggiungere uno sfondo azzurro chiaro a una colonna e importare dati con intestazioni—tutto usando lo stile predefinito fornito da Excel.

Inseriremo anche alcuni scenari “what‑if”, come la gestione dei valori null o la personalizzazione di più di una colonna. Alla fine, avrai un file Excel completamente stilizzato che potrai inviare agli stakeholder senza alcuna post‑elaborazione.

## Prerequisiti

* **.NET 6+** (il codice funziona anche su .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – la libreria che gestisce le chiamate `Workbook`, `Style` e `ImportDataTable`. Installala tramite NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Una sorgente `DataTable` – ne creeremo una fittizia nell'esempio, ma puoi sostituirla con qualsiasi query ADO.NET.

Li hai? Ottimo, cominciamo.

## Passo 1: Inizializzare un nuovo Workbook (Parola chiave primaria)

La prima cosa da fare è **how to create workbook** – letteralmente. La classe `Workbook` rappresenta l'intero file Excel, e il suo costruttore ti fornisce una tela pulita.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Perché è importante:** Iniziare con un `Workbook` nuovo garantisce di controllare ogni stile fin dall'inizio. Se aprissi un file esistente, erediteresti gli stili lasciati dall'autore originale, il che può portare a formattazioni incoerenti.

## Passo 2: Preparare il DataTable da importare

Per scopi illustrativi, creiamo un semplice `DataTable`. In scenari reali probabilmente chiameresti una stored procedure o un metodo ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Suggerimento:** Se devi preservare l'ordine delle colonne esattamente come appare nel database, imposta il parametro `importColumnNames` di `ImportDataTable` a `true`. Questo indica ad Aspose.Cells di scrivere le intestazioni di colonna per te.

## Passo 3: Definire gli stili delle colonne – Default + Sfondo azzurro chiaro

Ora rispondiamo alla parte **add light blue background** del puzzle. Aspose.Cells ti permette di passare un array di oggetti `Style` che corrispondono a ciascuna colonna che importi. La prima voce è lo stile per la colonna 0, la seconda per la colonna 1, e così via. Se hai meno stili delle colonne, le colonne rimanenti ricadranno nello stile predefinito.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Perché solo due stili?** Nel nostro esempio abbiamo quattro colonne, ma vogliamo che solo la seconda colonna (Name) risalti. La lunghezza dell'array non deve corrispondere al numero di colonne; le voci mancanti ereditano automaticamente lo stile predefinito del workbook.

## Passo 4: Importare il DataTable con intestazioni e stili

Qui è dove uniamo **excel import datatable c#** e **import data with headers**. Il metodo `ImportDataTable` fa il lavoro pesante: scrive i nomi delle colonne, le righe e applica l'array di stili che abbiamo appena creato.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Risultato atteso

Dopo aver eseguito il programma, `workbook` conterrà un unico foglio di lavoro che appare così:

| **ID** | **Name** (azzurro chiaro) | **HireDate** | **Salary** |
|-------|----------------------------|--------------|------------|
| 1     | Alice Johnson              | 5/12/2020    | 72000      |
| 2     | Bob Smith                  | 3/4/2019     | 68000      |
| 3     | Carol White                | *(vuoto)*    | 75000      |

* La colonna **Name** presenta uno sfondo azzurro chiaro, dimostrando che l'array di stili funziona.
* Le intestazioni delle colonne sono generate automaticamente perché abbiamo passato `true` per `importColumnNames`.
* I valori null appaiono come celle vuote, che è il comportamento predefinito di Aspose.Cells.

## Passo 5: Salvare il Workbook (Opzionale ma utile)

Probabilmente vorrai scrivere il file su disco o trasmetterlo a un client web. Il salvataggio è semplice:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Consiglio professionale:** Se stai puntando a versioni più vecchie di Excel, cambia `SaveFormat.Xlsx` in `SaveFormat.Xls`. L'API gestisce la conversione per te.

## Casi limite e variazioni

### Più colonne stilizzate

Se ti serve più di una colonna stilizzata, espandi semplicemente l'array `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Ora sia **Name** che **Salary** saranno azzurro chiaro.

### Formattazione condizionale invece di stili fissi

A volte vuoi che una colonna diventi rossa quando un valore supera una soglia. È qui che **use default style excel** incontra la formattazione condizionale:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importare senza intestazioni

Se il tuo sistema a valle fornisce già le proprie intestazioni, passa semplicemente `false` per l'argomento `importColumnNames`. I dati inizieranno in `A1` e potrai scrivere intestazioni personalizzate in seguito.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Esempio completo funzionante (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}