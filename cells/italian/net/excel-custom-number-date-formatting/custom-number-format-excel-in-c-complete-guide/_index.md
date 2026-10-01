---
category: general
date: 2026-03-22
description: Tutorial su formato numerico personalizzato in Excel che mostra come
  importare una datatable in Excel, impostare il colore di sfondo della colonna, formattare
  la colonna come valuta e salvare la cartella di lavoro come xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: it
og_description: Tutorial di Excel sul formato numerico personalizzato che ti guida
  nell'importazione di una DataTable, nell'impostazione del colore di sfondo della
  colonna, nella formattazione di una colonna come valuta e nel salvataggio della
  cartella di lavoro come xlsx.
og_title: Formato numerico personalizzato in Excel con C# – Guida passo passo
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Formato numerico personalizzato in Excel con C# – Guida completa
url: /it/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formato Numerico Personalizzato Excel – Tutorial Full‑Stack C#

Ti sei mai chiesto come applicare uno **custom number format excel** direttamente da C#? Forse hai provato a esportare un DataTable in un foglio di calcolo solo per vedere numeri semplici, senza colori e senza formattazione valuta. È un problema comune—soprattutto quando ti serve un report curato per gli stakeholder.

In questa guida risolveremo quel problema insieme: imparerai a **import datatable to excel**, a **set column background color**, a **format column as currency** e infine a **save workbook as xlsx** con un formato numerico personalizzato che farà risaltare i tuoi dati. Niente riferimenti vaghi, solo una soluzione completa e pronta all'uso che puoi copiare‑incollare nel tuo progetto.

---

## Cosa Costruirai

Al termine di questo tutorial avrai un'app console C# autonoma che:

1. Recupera un `DataTable` (puoi sostituire lo stub con la tua query).  
2. Crea un nuovo workbook Excel usando Aspose.Cells (o qualsiasi libreria compatibile).  
3. Applica un carattere blu e grassetto alla prima colonna, uno sfondo giallo‑chiaro alla seconda e un formato valuta (`$#,##0.00`) alla terza.  
4. Salva il file come `DataTableWithStyleArray.xlsx` in una cartella a tua scelta.

Vedrai esattamente come ogni riga contribuisce al file Excel finale, e discuteremo perché queste scelte sono importanti per manutenibilità e performance.

---

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+).  
- Aspose.Cells per .NET (versione di prova gratuita o licenziata). Installa via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Familiarità di base con `DataTable` e le applicazioni console C#.

---

## Passo 1: Recupera i Dati di Origine come DataTable

Per prima cosa, ci servono dei dati da esportare. In uno scenario reale probabilmente chiameresti un repository o eseguirai una query SQL. Per illustrazione creiamo una tabella semplice in memoria.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Perché è importante:** Usare un `DataTable` ti fornisce una fonte tabellare, consapevole dello schema, che si mappa perfettamente su righe e colonne di Excel. Ti permette anche di riutilizzare la stessa logica di esportazione per qualsiasi set di dati senza riscrivere codice.

---

## Passo 2: Crea un Nuovo Workbook e Ottieni il Primo Worksheet

Ora creiamo un workbook Excel. La classe `Workbook` rappresenta l'intero file; il suo `Worksheets[0]` è il foglio predefinito dove inseriremo i dati.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Se ti servono più fogli, basta chiamare `workbook.Worksheets.Add("SheetName")` e ripetere i passaggi di stilizzazione per ciascuno.

---

## Passo 3: Definisci gli Stili delle Colonne – Font, Sfondo e Formato Numerico

Lo styling in Aspose.Cells avviene tramite oggetti `Style`. Costruiremo un array in cui ogni elemento corrisponde a una colonna del DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Perché un array di stili?** Passare un array a `ImportDataTable` ti consente di applicare uno stile distinto a ogni colonna in una singola chiamata, il che è sia conciso che performante. Garantisce inoltre che la formattazione rimanga sincronizzata con l'ordine dei dati.

---

## Passo 4: Importa il DataTable Applicando gli Stili

Ecco il cuore dell'operazione: inseriamo il `DataTable` nel worksheet, chiediamo ad Aspose di includere la riga di intestazione e forniamo il nostro array `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Cosa succede dietro le quinte?** Aspose itera su ogni colonna, scrive l'intestazione, poi scrive i valori di ogni riga. Durante questo processo applica lo `Style` corrispondente dall'array, così ottieni un'intestazione blu per “Product”, una colonna “Quantity” con sfondo giallo e una colonna “Revenue” formattata correttamente come valuta.

---

## Passo 5: Salva il Workbook come File XLSX

Infine, persi il workbook su disco. Il metodo `Save` sceglie automaticamente il formato XLSX in base all'estensione del file.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Suggerimento:** Se devi trasmettere il file in streaming (ad esempio per un'API web), usa `workbook.Save(stream, SaveFormat.Xlsx)` invece di un percorso file.

---

## Esempio Completo Funzionante

Di seguito trovi il programma completo che puoi incollare in un nuovo progetto console. Compila ed esegue così com'è, producendo un file Excel stilizzato.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Risultato Atteso

Aprendo `DataTableWithStyleArray.xlsx` vedrai:

| **Product** (blu, grassetto) | **Quantity** (giallo‑chiaro) | **Revenue** (valuta) |
|------------------------------|------------------------------|----------------------|
| Widget A                     | 120                          | $3,450.75            |
| Widget B                     | 85                           | $2,190.00            |
| Widget C                     | 60                           | $1,580.40            |

Il **custom number format excel** specificato (`$#,##0.00`) garantisce che ogni cella di revenue mostri il simbolo del dollaro, il separatore delle migliaia e due decimali—esattamente ciò che i team finanziari si aspettano.

---

## Domande Frequenti & Casi Limite

### Posso usarlo con una libreria Excel diversa?

Assolutamente. Il concetto—creare uno stile per colonna e applicarlo durante l'importazione—si traduce in EPPlus, ClosedXML o NPOI. Le chiamate API cambiano, ma il pattern rimane lo stesso.

### Cosa succede se il mio DataTable ha più colonne degli stili?

Aspose applicherà lo stile predefinito a qualsiasi colonna senza una voce corrispondente nell'array `columnStyles`. Per evitare sorprese, dimensiona l'array a `dataTable.Columns.Count` o genera gli stili dinamicamente in un ciclo.

### Come imposto un formato numerico personalizzato per le date?

Basta impostare `style.Custom = "dd‑mm‑yyyy"` (o qualsiasi stringa di formato Excel valida). Lo stesso approccio basato su array funziona per date, percentuali o notazione scientifica.

### Esiste un modo per auto‑dimensionare le colonne dopo l'importazione?

Sì—chiama `worksheet.AutoFitColumns();` dopo l'importazione. Esegue un rapido calcolo della larghezza basato sul contenuto delle celle.

### E per set di dati molto grandi (100k+ righe)?

`ImportDataTable` è ottimizzato per operazioni bulk, ma potresti raggiungere limiti di memoria. In tal caso, considera lo streaming delle righe manualmente con `Cells[i, j].PutValue(...)` e riutilizza un unico oggetto `Style` per ridurre l'overhead.

---

## Consigli Pro & Trappole Comuni

- **Evita di hard‑codare i percorsi** in codice di produzione; usa `Environment.GetFolderPath` o impostazioni di configurazione.  
- **Dispose del workbook** se lo utilizzi in un servizio a lungo termine—racchiudilo in un blocco `using` per liberare le risorse native.  
- **Fai attenzione ai separatori specifici della cultura**. Il formato personalizzato `$#,##0.00` forza il punto come separatore decimale indipendentemente dalla locale del sistema, il che è solitamente quello che vuoi per i report finanziari.  
- **Ricorda di referenziare System.Drawing** (o `System.Drawing.Common` su .NET Core) per le struct di colore usate nello styling.  
- **Testa l'output su diverse versioni di Excel**; le versioni più vecchie potrebbero interpretare alcuni formati personalizzati in modo leggermente diverso.

---

## Conclusione

Abbiamo coperto tutto ciò che ti serve per **custom number format excel** file da C#: estrarre dati da un `DataTable`, **import datatable to excel**, applicare un **set column background color**, usare **format column as currency** e infine **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}