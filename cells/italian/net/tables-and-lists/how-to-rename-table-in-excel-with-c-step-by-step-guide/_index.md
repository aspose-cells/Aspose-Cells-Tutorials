---
category: general
date: 2026-08-11
description: Come rinominare una tabella in Excel con C# usando Aspose.Cells. Impara
  a creare una cartella di lavoro Excel, aggiungere un intervallo denominato e evitare
  conflitti di rinomina.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: it
lastmod: 2026-08-11
og_description: Come rinominare una tabella in Excel con C# usando Aspose.Cells. Questa
  guida ti mostra come creare una cartella di lavoro Excel, aggiungere un intervallo
  denominato e rinominare in modo sicuro una tabella Excel.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Come rinominare una tabella in Excel con C# – tutorial completo di programmazione
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Come rinominare una tabella in Excel con C# – guida passo passo
url: /it/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come rinominare una tabella in Excel con C# – guida passo‑passo

Se hai bisogno di **how to rename table** in un file Excel in modo programmatico, questo tutorial ti mostra l'approccio esatto usando Aspose.Cells per .NET. Vedrai come **create Excel workbook**, definire un **named range** e rinominare una tabella Excel esistente senza causare conflitti di nome.

La soluzione funziona per qualsiasi progetto .NET che mira a .NET 6 o versioni successive e richiede solo il pacchetto NuGet Aspose.Cells. Alla fine della guida potrai rinominare una tabella Excel in modo sicuro e capire perché può verificarsi un conflitto quando il nome di una tabella coincide con un intervallo definito.

## Prerequisiti

- .NET 6 SDK o versioni più recenti installato  
- Visual Studio 2022 (o qualsiasi IDE C#)  
- Pacchetto Aspose.Cells per .NET (`dotnet add package Aspose.Cells`)  

Non sono richiesti ulteriori assembly di interop Excel perché Aspose.Cells funziona interamente in memoria.

## Panoramica della soluzione

1. **Create Excel workbook** – istanziare un `Workbook` e aggiungere alcuni dati di esempio.  
2. **Add a named range** – usare `Worksheets.Names.Add` per creare un intervallo chiamato `MyRange`.  
3. **Create an Excel table (ListObject)** – convertire i dati in una tabella così da avere qualcosa da rinominare.  
4. **Rename the table** – provare a impostare la proprietà `Name` della tabella con lo stesso identificatore dell'intervallo nominato.  
5. **Handle name conflicts** – catturare l'eccezione, spiegare perché si verifica e mostrare una strategia di rinomina sicura.  

Ogni passaggio è spiegato in dettaglio di seguito.

## Passo 1: Come creare un workbook Excel e popolare i dati

Creare un workbook è la base per qualsiasi attività di automazione Excel. La classe `Workbook` rappresenta l'intero file in memoria.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Why this matters:** Il workbook deve contenere dati prima di poter creare una tabella. Aspose.Cells memorizza i dati in una collezione indicizzata da zero, quindi `Worksheets[0]` si riferisce sempre al primo foglio.

## Passo 2: Come aggiungere un named range al foglio di lavoro

Un **named range** ti consente di riferirti a una cella o a un intervallo specifico tramite un identificatore amichevole. Aggiungere un intervallo è semplice:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Why this matters:** I named range sono memorizzati nella collezione globale dei nomi del workbook. Se in seguito una tabella riceve lo stesso nome, Aspose.Cells genera una `CellException` perché Excel non consente nomi duplicati.

## Passo 3: Come aggiungere una tabella Excel (ListObject)

Una tabella fornisce gestione strutturata dei dati, filtraggio e stile. In Aspose.Cells è chiamata **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Why this matters:** La tabella ora esiste con il nome `InitialTable`. Rinominarla dimostra il processo di **how to rename table**.

## Passo 4: Come rinominare una tabella Excel e gestire i conflitti

Tentare di rinominare la tabella in `MyRange` entrerà in conflitto con il named range creato in precedenza. Il codice seguente mostra il modello corretto per rilevare e risolvere il conflitto.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### Cosa fa il codice

| Passo | Azione | Motivo |
|------|--------|--------|
| **Try rename** | `table.Name = "MyRange"` | Dimostra lo scenario di conflitto. |
| **Catch exception** | Stampa il messaggio di conflitto. | Fornisce un feedback immediato sul problema. |
| **Generate safe name** | `GetUniqueTableName` aggiunge un suffisso numerico finché il nome è disponibile. | Garantisce che il nuovo nome della tabella **non** collida con alcun named range o tabella esistente. |
| **Save workbook** | `workbook.Save("RenamedTable.xlsx")` | Persiste le modifiche così puoi aprire il file in Excel e verificare il risultato. |

**Expected output** quando esegui il programma:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Aprendo `RenamedTable.xlsx` si vede una tabella chiamata `MyRange_1` e un named range separato `MyRange` che punta alla cella A1.

## Perché si verifica il conflitto e migliori pratiche per rinominare una tabella Excel

- Excel memorizza **named ranges** e **table names** nello stesso namespace.  
- Quando tenti di assegnare un nome di tabella che esiste già come intervallo, Aspose.Cells genera una `CellException`.  
- L'approccio consigliato è **check for existing names first** (come mostrato in `NameExists`) o utilizzare una convenzione di denominazione che garantisca l'unicità (ad es., prefissare le tabelle con `tbl_`).  

Applicare questo modello previene errori di runtime e rende la tua automazione più robusta.

## Suggerimenti aggiuntivi per lavorare con Aspose.Cells

- **Pro tip:** Usa `Workbook.Worksheets.Names.Remove("MyRange")` se vuoi intenzionalmente sostituire l'intervallo con un nome di tabella.  
- **Watch out for case sensitivity:** Excel tratta i nomi in modo case‑insensitive; i metodi di supporto usano `OrdinalIgnoreCase` per emulare il comportamento di Excel.  
- **Performance:** Se stai elaborando molti fogli, memorizza nella cache la collezione dei nomi invece di iterare ripetutamente.

## Esempio completo in un unico blocco

Di seguito trovi il programma completo che puoi copiare‑incollare in un progetto console. Include tutti i passaggi dalla creazione del workbook alla rinomina sicura della tabella.



## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare named range a livello di workbook in Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Come implementare formule con named range in .NET usando Aspose.Cells per l'automazione Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Come aggiungere slicer alle tabelle Excel usando Aspose.Cells per .NET: Guida completa](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}