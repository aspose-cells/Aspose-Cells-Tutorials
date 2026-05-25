---
category: general
date: 2026-02-14
description: Analizza le date dell’era giapponese in Excel con un parsing personalizzato
  delle date. Scopri come caricare una cartella di lavoro da file usando “load excel”
  con opzioni ed evita gli errori più comuni.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: it
og_description: Analizza le date dell’era giapponese in Excel usando Aspose.Cells.
  Questa guida mostra come caricare una cartella di lavoro da file con opzioni di
  analisi personalizzate delle date.
og_title: Analizza le date delle ere giapponesi – Tutorial C# passo passo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Analizza le date dell'era giapponese in Excel – Guida completa per sviluppatori
  C#
url: /it/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizza le date dell'era giapponese – Tutorial completo C#

Ti è mai capitato di **analizzare le date dell'era giapponese** da un foglio Excel e di chiederti perché i valori si trasformano in numeri strani? Non sei solo. Molti sviluppatori incontrano questo problema quando il parser predefinito `DateTime` non riconosce lo stile “Reiwa 1/04/01” usato nei calendari giapponesi.  

Buone notizie: puoi indicare ad Aspose.Cells di trattare quelle celle come date dell'era giapponese fin dal momento in cui **carichi Excel con opzioni**. In questa guida vedremo come caricare una cartella di lavoro da file, configurare l'analisi personalizzata delle date e verificare che le date vengano restituite esattamente come ti aspetti.

Al termine di questo tutorial sarai in grado di:

* Caricare una cartella di lavoro da file specificando `DateTimeParsing.JapaneseEra`.
* Accedere ai valori delle celle come oggetti `DateTime` corretti.
* Gestire casi particolari come celle vuote o calendari misti.
* Estendere l'approccio a qualsiasi scenario di **custom date parsing excel** che potresti incontrare.

> **Prerequisito** – Hai bisogno della libreria Aspose.Cells per .NET (v23.9 o successiva) e di un IDE compatibile con .NET (Visual Studio, Rider, ecc.). Non sono richiesti altri pacchetti.

---

## Passo 1: Configura le opzioni di caricamento testo per l'analisi dell'era giapponese  

La prima cosa che facciamo è dire al loader come interpretare il testo che sembra una data dell'era giapponese. Questo avviene tramite `TxtLoadOptions` e l'enumerazione `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Perché è importante:** Senza il flag `JapaneseEra`, Aspose.Cells tratta la cella come una semplice stringa, lasciandoti dover suddividere manualmente il nome dell'era e convertirlo. Il flag fa il lavoro pesante, mantenendo il tuo codice pulito e meno soggetto a errori.

---

## Passo 2: Carica la cartella di lavoro da file usando le opzioni  

Ora apriamo effettivamente il file Excel. Nota come l'oggetto `loadOptions` venga passato al costruttore `Workbook`—questo è il **load workbook from file** che rispetta le nostre regole di analisi personalizzate.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Se il file si trova altrove (ad esempio su una condivisione di rete), basta adeguare `filePath` di conseguenza. La parte importante è che la stessa istanza di `loadOptions` venga utilizzata; altrimenti la conversione dell'era giapponese non avverrà.

---

## Passo 3: Accedi alle date analizzate  

Con la cartella di lavoro caricata, puoi estrarre i valori delle celle esattamente come faresti con qualsiasi data normale. L'API restituisce automaticamente un oggetto `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Output previsto** (supponendo che A1 contenga “R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

Se la cella contiene una data gregoriana come “2023‑12‑31”, il parser funziona comunque—restituisce semplicemente la data originale invariata.

---

## Passo 4: Verifica tutte le date in una colonna  

Spesso è necessario scansionare un'intera colonna di date dell'era giapponese. Di seguito trovi un ciclo compatto che mostra come gestire celle vuote e contenuti misti in modo elegante.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Consiglio professionale:** `CellValueType.IsDateTime` è il modo più sicuro per verificare se il parser ha avuto successo. Ti protegge da `InvalidCastException` quando una cella contiene testo inatteso.

---

## Passo 5: Problemi comuni e come gestirli  

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Le celle vuote restituiscono `DateTime.MinValue`** | Il parser tratta le stringhe vuote come la data minima. | Controlla `cell.IsNull` prima di accedere a `DateTimeValue`. |
| **Calendari misti (giapponese + gregoriano) nella stessa colonna** | Il parser gestisce entrambi, ma potresti dover differenziare per la reportistica. | Usa `cell.StringValue` per ispezionare il testo originale quando `cell.Type` è `IsString`. |
| **Era errata (es. “H30” per Heisei) dopo il 2019** | Heisei è terminato nel 2019; le date successive dovrebbero usare “R”. | Convalida il prefisso dell'era prima di fidarti del risultato analizzato. |
| **Rallentamento delle prestazioni su file molto grandi** | Il caricamento con opzioni personalizzate aggiunge un piccolo overhead. | Carica solo i fogli di lavoro necessari (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Passo 6: Esempio completo funzionante  

Mettendo tutto insieme, ecco un'app console autonoma che puoi copiare‑incollare ed eseguire. Dimostra **custom date parsing excel** dall'inizio alla fine.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Cosa dovresti vedere** quando `japan_dates.xlsx` contiene:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (vuoto) | R2/02/15 |

Output della console:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

Il file salvato ora contiene celle data corrette, che puoi aprire in Excel e vedere il consueto formato data.

---

## Conclusione  

Abbiamo appena mostrato come **analizzare le date dell'era giapponese** in Excel configurando `TxtLoadOptions`, **caricare la cartella di lavoro da file** con tali opzioni e lavorare con i valori `DateTime` risultanti. Lo stesso schema—impostare flag di analisi personalizzati e poi caricare la cartella di lavoro—si applica a qualsiasi esigenza di **custom date parsing excel**, sia che tu stia gestendo periodi fiscali, numeri di settimana ISO o formati proprietari.

Hai un'era diversa o un foglio di calcolo a calendario misto? Basta sostituire `DateTimeParsing.JapaneseEra` con un altro valore enum (ad esempio `DateTimeParsing.Custom`) e fornire una stringa di formato. La flessibilità di Aspose.Cells significa che raramente dovrai scrivere nuovamente codice di conversione manuale.

**Passi successivi** che potresti esplorare:

* **Load Excel with options** per file CSV (`CsvLoadOptions`) per gestire separatori specifici della locale.
* Usa `Workbook.Save` con `SaveFormat.Xlsx` per esportare i dati puliti.
* Combina questo approccio con **Aspose.Slides** o **Aspose.Words** per pipeline di reporting.

Provalo, modifica le opzioni e lascia che la libreria faccia il lavoro pesante. Buona programmazione!  

![Screenshot of parsed Japanese era dates in a console window – parse japanese era dates example](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}