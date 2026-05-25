---
category: general
date: 2026-02-15
description: Crea un workbook in C# ed esporta una DataTable in Excel con formattazione
  delle righe, imposta lo sfondo delle righe e automatizza le attività di Excel in
  pochi minuti.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: it
og_description: Crea rapidamente una cartella di lavoro C#, applica stili alle righe
  e automatizza l'esportazione Excel con esempi di codice completi e consigli di best
  practice.
og_title: Crea Workbook C# – Esporta DataTable in Excel con Formattazione
tags:
- C#
- Excel
- DataExport
title: Crea Workbook C# – Esporta DataTable in Excel con formattazione
url: /it/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare Workbook C# – Esportare DataTable in Excel con Formattazione

Hai mai avuto bisogno di **create workbook C#** e di scaricare un `DataTable` in Excel con uno stile personalizzato? Non sei solo. In molte applicazioni line‑of‑business il requisito è generare un foglio di calcolo ben formattato che un utente non tecnico possa aprire e comprendere immediatamente.  

In questa guida percorreremo una soluzione completa, pronta‑all’uso, che ti mostra **how to create workbook C#**, applica **excel export formatting**, imposta un **row background** e sfrutta **excel automation c#** per produrre un file rifinito. Niente scorciatoie vaghe tipo “vedi la documentazione”—solo il codice completo, spiegazioni sul perché ogni riga è importante e consigli che potrai utilizzare già domani.

---

## Prerequisiti

- .NET 6 (o .NET Framework 4.6+).  
- Visual Studio 2022 o qualsiasi IDE compatibile con C#.  
- Il pacchetto NuGet **Aspose.Cells for .NET** (o qualsiasi libreria che espone `Workbook`, `Worksheet`, `Style`).  
- Familiarità di base con `DataTable`.  

Se non hai ancora Aspose.Cells, esegui:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** La versione di prova gratuita funziona per la maggior parte degli scenari di sviluppo; ricordati solo di sostituire la chiave di licenza prima di distribuire.

![Esempio di create workbook C# che mostra righe formattate in Excel]( "Esempio di create workbook C# con colori di sfondo delle righe")

---

## Passo 1: Inizializzare il Workbook e il Worksheet (Create Workbook C#)

La prima cosa da fare è istanziare un `Workbook`. Pensalo come aprire un nuovo file Excel in memoria.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Perché?**  
`Workbook` contiene l'intero documento Excel, mentre `Worksheet` rappresenta una singola scheda. Iniziare con un workbook pulito garantisce il controllo di ogni aspetto dell'output—nessuno stile predefinito nascosto che si infiltra.

---

## Passo 2: Preparare un DataTable di esempio (Export DataTable Excel)

In un progetto reale estrarresti dati da un database, ma per illustrazione costruiremo un piccolo `DataTable` al volo.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Perché è importante:**  
Esportare un `DataTable` è il modo più comune per trasferire dati tabulari da un'applicazione a Excel. Il metodo sopra è completamente autonomo, quindi puoi copiarlo e incollarlo in qualsiasi progetto e funzionerà.

---

## Passo 3: Creare uno Style per riga (Excel Export Formatting)

Per dare a ogni riga il proprio colore di sfondo, generiamo un oggetto `Style` per ogni riga del `DataTable`. È qui che **excel export formatting** brilla.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Perché lo styling per riga?**  
Se devi evidenziare record specifici (ad esempio fatture scadute) puoi sostituire il semplice ciclo di colori con una logica condizionale—basta impostare `style.ForegroundColor` in base ai dati della riga.

---

## Passo 4: Importare il DataTable con gli Stili di Riga (Set Row Background)

Ora uniamo tutto: i dati, il workbook e gli stili.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Cosa vedrai:**  
Aprendo `EmployeesReport.xlsx` vedrai una riga di intestazione con formattazione predefinita, seguita da quattro righe di dati ciascuna colorata con un colore di sfondo chiaro. Il risultato appare come un report realizzato a mano, non un semplice dump.

---

## Passo 5: Suggerimenti Avanzati per Excel Automation C# (Excel Automation C#)

Di seguito alcuni trucchi rapidi che puoi aggiungere all'esempio di base:

| Suggerimento | Snippet di Codice | Quando Utilizzarlo |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Dopo aver importato i dati per evitare testo troncato. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Quando la tabella può scorrere oltre lo schermo. |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Evidenzia gli stipendi sopra una soglia. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Quando hai bisogno di report in sola lettura. |

Questi snippet dimostrano l'ampiezza di **excel automation c#**—puoi continuare ad estendere il workbook senza riscrivere la logica di importazione di base.

---

## Domande Frequenti & Casi Limite

**Cosa succede se il DataTable ha migliaia di righe?**  
Aspose.Cells trasmette i dati in modo efficiente, ma potresti voler disabilitare la creazione di stile per ogni riga per risparmiare memoria. Invece, applica un unico stile a un intervallo:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Posso esportare in .csv invece di .xlsx?**  
Certo—basta cambiare il formato di salvataggio:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Lo stile verrà perso (CSV non supporta lo styling), ma l'esportazione dei dati rimane la stessa.

**Funziona su .NET Core?**  
Sì. Aspose.Cells supporta .NET Standard 2.0 e versioni successive, quindi lo stesso codice funziona su .NET 6, .NET 7 o .NET Framework.

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}