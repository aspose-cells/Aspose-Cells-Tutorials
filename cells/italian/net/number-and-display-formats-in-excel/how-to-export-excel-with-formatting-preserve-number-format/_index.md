---
category: general
date: 2026-03-22
description: Come esportare Excel con formattazione e preservare il formato numerico.
  Scopri come convertire un intervallo Excel, ottenere il risultato di una formula
  e esportare Excel con formattazione usando Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: it
og_description: Come esportare Excel con formattazione e preservare il formato dei
  numeri. Guida passo‑passo per convertire un intervallo Excel, ottenere il risultato
  della formula e esportare Excel con formattazione in C#.
og_title: Come esportare Excel con formattazione – Conserva il formato numerico
tags:
- C#
- Aspose.Cells
- Excel automation
title: Come esportare Excel con formattazione – Conservare il formato numerico
url: /it/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel con formattazione – Conservare il formato numerico

Ti sei mai chiesto **come esportare Excel** mantenendo l’aspetto di ogni cella esattamente come lo vedi nella cartella di lavoro? Forse devi inviare un report a un cliente, alimentare un controllo grid, o semplicemente archiviare i valori in un database. Il punto dolente è solitamente la perdita della formattazione numerica o le formule che diventano stringhe grezze.  

In questo tutorial passeremo in rassegna un esempio completo, pronto‑da‑eseguire in C#, che **conserva il formato numerico**, **converte un intervallo Excel** in un `DataTable`, **ottiene il risultato della formula**, e infine **esporta Excel con formattazione** usando Aspose.Cells. Alla fine avrai un unico metodo da inserire in qualsiasi progetto e chiamare con un riferimento al foglio di lavoro.

> **Anteprima rapida:** il codice crea una cartella di lavoro, scrive un valore e una formula, indica ad Aspose.Cells di esportare le celle come stringhe formattate, e stampa `123.456 | 246.912` – esattamente ciò che ti aspetti di vedere in Excel.

---

## Di cosa avrai bisogno

- **Aspose.Cells for .NET** (la versione di prova gratuita è sufficiente per imparare)
- .NET 6.0 o successivo (l’API è la stessa su .NET Framework)
- Un ambiente di sviluppo C# di base (Visual Studio, VS Code, Rider… a tua scelta)

Non sono necessari pacchetti NuGet aggiuntivi oltre a Aspose.Cells. Se non lo hai ancora installato, esegui:

```bash
dotnet add package Aspose.Cells
```

---

## Passo 1 – Creare una cartella di lavoro e scrivere valori (inclusa una formula)

Per prima cosa creiamo una nuova cartella di lavoro e inseriamo un valore numerico in **A1**. Poi aggiungiamo una semplice formula in **B1** che moltiplica la prima cella per due. Questo prepara il terreno per dimostrare **ottenere il risultato della formula** più avanti.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Perché è importante:**  
- `PutValue` memorizza il numero grezzo, mentre `PutFormula` memorizza il calcolo.  
- Aspose.Cells mantiene viva la formula, così quando più tardi chiediamo il valore della cella otterremo realmente `246.912`, non la stringa `"=A1*2"`.

---

## Passo 2 – Dire ad Aspose.Cells di esportare i valori come stringhe formattate

Se chiami semplicemente `ExportDataTable` con le impostazioni predefinite, le celle numeriche verranno restituite come i loro valori `double` sottostanti. Questo elimina separatori delle migliaia, simboli di valuta o decimali personalizzati che potresti aver impostato. La classe `ExportTableOptions` ci permette di **conservare il formato numerico** e **esportare come stringa**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Punto chiave:** `ExportNumberFormat = true` è l’opzione che fa funzionare **conservare il formato numerico**. Senza di essa vedresti `"123.456"` e `"246.912"` come numeri grezzi, il che può andare bene nel codice ma non quando incolli i dati in un’interfaccia che si aspetta la stessa formattazione di Excel.

---

## Passo 3 – Stampare i dati esportati (verifica)

Ora che abbiamo un `DataTable` pieno di stringhe formattate, scarichiamo il contenuto sulla console. Questo dimostra anche che siamo riusciti a **ottenere il risultato della formula** senza valutare la formula noi stessi.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

L’esecuzione del programma stampa:

```
123.456 | 246.912
```

Nota come la seconda colonna mostri il **risultato della formula**, non il testo della formula. È esattamente ciò di cui hai bisogno quando **esporti Excel con formattazione** per l’elaborazione successiva.

---

## Passo 4 – Convertire intervalli Excel più grandi (opzionale)

L’esempio sopra gestisce una piccola porzione `A1:B1`, ma scenari reali spesso richiedono l’esportazione di tabelle intere. Lo stesso metodo funziona per qualsiasi blocco rettangolare – basta regolare i parametri `firstRow`, `firstColumn`, `totalRows` e `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Consiglio professionale:** Se il tuo foglio ha già una riga di intestazione, imposta `includeColumnNames` su `true`. Aspose.Cells utilizzerà la prima riga dell’intervallo come nomi di colonna, il che è comodo quando successivamente colleghi il `DataTable` a una griglia UI.

---

## Passo 5 – Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **I numeri perdono virgole o simboli di valuta** | `ExportAsString` è `false` o `ExportNumberFormat` è omesso | Imposta sia `ExportAsString = true` **che** `ExportNumberFormat = true`. |
| **Le celle con formula restituiscono il testo della formula** | Non hai chiamato `CalculateFormula` prima dell’esportazione (necessario solo se la cartella non è impostata su calcolo automatico) | Abilita il calcolo automatico (`workbook.CalculateFormula()`) o usa `ExportAsString` che forza la valutazione. |
| **Le intestazioni appaiono come righe di dati** | `includeColumnNames` è impostato su `false` mentre il tuo intervallo include una riga di intestazione | Imposta `includeColumnNames = true` per trattare la prima riga come nomi di colonna. |
| **Intervalli grandi causano pressione sulla memoria** | L’esportazione dell’intero foglio in una volta carica tutto in memoria | Esporta a blocchi (ad esempio 500 righe alla volta) e unisci i `DataTable` se necessario. |

---

## Passo 6 – Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l’intero programma, dalle istruzioni `using` al metodo `Main`. Incollalo in un’app console e premi **F5** – vedrai subito l’output formattato.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Output previsto**

```
123.456 | 246.912

Press any key to exit...
```

Questo è l’intero flusso **come esportare Excel**, con formattazione intatta, risultati delle formule valutati, e un `DataTable` pulito pronto per qualsiasi consumatore .NET.

---

## Conclusione

Abbiamo coperto tutto ciò che devi sapere su **come esportare Excel** mantenendo **il formato numerico**, **convertendo un intervallo Excel** in un `DataTable`, e **ottenendo i risultati delle formule** senza parsing aggiuntivo. La chiave è la configurazione di `ExportTableOptions` – una volta impostati `ExportAsString` e `ExportNumberFormat` su `true`, Aspose.Cells fa il lavoro pesante per te.

Da qui puoi:

- Collegare il `DataTable` a un `DataGrid` WPF o a una vista ASP.NET MVC.  
- Scrivere la tabella in un file CSV mantenendo la rappresentazione visiva esatta.  
- Estendere l’approccio a più fogli o intervalli dinamici.

Sentiti libero di sperimentare con formati diversi (valuta, percentuali) e blocchi di dati più grandi. Se incontri qualche strano comportamento, torna alla tabella **problemi comuni** – copre le difficoltà più frequenti quando **esporti Excel con formattazione**.

Buona programmazione, e che i tuoi fogli esportati siano sempre lucidi come gli originali!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}