---
category: general
date: 2026-03-01
description: Importa dati con formattazione in Excel usando C#. Scopri come importare
  un DataTable in Excel e aggiungere colore di sfondo alle celle in pochi passaggi.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: it
og_description: Importa dati con formattazione in Excel usando C#. Guida passo passo
  che mostra come importare una DataTable e aggiungere colore di sfondo alle celle.
og_title: Importa dati con formattazione in Excel – Guida C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importa dati con formattazione in Excel usando C#
url: /it/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importa dati con formattazione in Excel usando C#

Hai mai dovuto **importare dati con formattazione** in una cartella di lavoro Excel ma hai ottenuto solo un foglio piatto e noioso? Non sei solo. La maggior parte degli sviluppatori si imbatte in questo ostacolo quando scopre che l'importazione predefinita elimina tutti i colori e gli stili che hanno impostato con cura nei dati di origine.

In questo tutorial vedremo una soluzione completa, pronta all'uso, che **importa un DataTable in Excel** e **aggiunge il colore di sfondo alle celle di Excel** nello stesso momento. Nessun post‑processing aggiuntivo necessario—il tuo foglio di calcolo avrà esattamente l'aspetto desiderato fin dal primo avvio.

## Cosa imparerai

- Come recuperare i dati in un `DataTable`.
- Come definire un array di oggetti `Style` che contengono i colori di sfondo.
- Come chiamare `ImportDataTable` con quegli stili affinché l'importazione conservi la formattazione.
- Un esempio completo, eseguibile, che puoi inserire in un'app console e vedere subito il risultato.
- Suggerimenti, insidie e varianti per progetti reali.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+).
- La libreria **GemBox.Spreadsheet** (la versione gratuita è sufficiente per la demo).
- Familiarità di base con C# e i concetti di Excel.

Se ti chiedi *perché GemBox?* perché offre un metodo a riga singola `ImportDataTable` che accetta array di stili—esattamente ciò che ci serve per **importare dati con formattazione** senza scrivere un ciclo.

---

## Passo 1: Configura il progetto e aggiungi GemBox.Spreadsheet

Per iniziare, crea una nuova app console:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Consiglio professionale:** La versione gratuita limita i fogli a 150 k celle, più che sufficienti per le demo. Se raggiungi il limite, passa a una licenza a pagamento o passa a EPPlus, ma l'API avrà qualche differenza.

## Passo 2: Recupera i dati di origine come `DataTable`

La prima cosa di cui abbiamo bisogno è un `DataTable` che imiti i dati che normalmente estrarresti da un database. Ecco un piccolo helper che ne crea uno in memoria:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Perché è importante:** Separando il recupero dei dati in un metodo dedicato, puoi sostituire la sorgente—SQL, CSV, servizio web—senza toccare la logica di importazione. Questo mantiene il codice pulito e rende il tutorial **come importare datatable in excel** riutilizzabile.

## Passo 3: Definisci gli stili da applicare

Ora arriva la parte divertente: creeremo un array di oggetti `Style`, ognuno con un `ForegroundColor` distinto. GemBox ti permette di impostare `BackgroundPatternColor` (riempimento cella) e `ForegroundColor` (colore testo). Per questa demo coloreremo le prime due colonne in modo diverso.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Spiegazione:**  
- Gli oggetti `Style` sono contenitori leggeri; non è necessario crearne uno nuovo per ogni cella.  
- Allineando l'ordine dell'array con l'ordine delle colonne, GemBox applica automaticamente lo stile corrispondente durante l'importazione.  
- Questa è la chiave per **importare dati con formattazione**—la formattazione viaggia con i dati, non dopo.

## Passo 4: Importa il `DataTable` nel foglio di lavoro con gli stili

Con dati e stili pronti, possiamo ora creare una cartella di lavoro, scegliere il primo foglio e chiamare `ImportDataTable`. La firma del metodo è la seguente:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Ecco come lo utilizziamo:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Cosa succede dietro le quinte?**  
- `true` indica a GemBox di scrivere i nomi delle colonne nella prima riga.  
- `0, 0` posiziona l'importazione nella cella A1.  
- `importStyles` collega ogni colonna ai colori definiti in precedenza.  

Quando apri *Report.xlsx*, vedrai la colonna **ID** sfumata di azzurro chiaro, la colonna **Name** sfumata di verde chiaro, e la colonna **Score** senza modifiche. Questo è **importare dati con formattazione** in una singola chiamata.

## Passo 5: Verifica il risultato (output previsto)

Apri il file `Report.xlsx` generato. Dovresti vedere qualcosa di simile:

| ID (azzurro chiaro) | Name (verde chiaro) | Score |
|---------------------|---------------------|-------|
| 1                   | Alice               | 93.5 |
| 2                   | Bob                 | 78.0 |
| 3                   | Charlie             | 85.2 |
| 4                   | Diana               | 91.3 |
| 5                   | Ethan               | 67.8 |

- Le celle della colonna **ID** hanno uno sfondo azzurro chiaro.  
- Le celle della colonna **Name** hanno uno sfondo verde chiaro.  
- La colonna **Score** mantiene lo sfondo bianco predefinito.

Questa indicazione visiva rende il report immediatamente leggibile—un piccolo tocco che può migliorare notevolmente l'esperienza dell'utente.

![Foglio Excel che mostra l'importazione di dati con formattazione – colonna ID azzurro chiaro, colonna Name verde chiaro](excel-screenshot.png "esempio di importazione di dati con formattazione")

*Il testo alternativo dell'immagine include la parola chiave principale per la SEO.*

---

## Domande frequenti e casi particolari

### Posso applicare più di semplici colori di sfondo?

Assolutamente. `Style` ti permette di impostare caratteri, bordi, formati numerici e persino formattazione condizionale. Per esempio, per rendere i punteggi superiori a 90 in grassetto e rosso:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Cosa succede se il mio DataTable ha più colonne degli stili?

GemBox applicherà gli stili solo alle colonne che hanno una voce corrispondente nell'array. Le colonne extra utilizzeranno lo stile predefinito—non verrà generato alcun errore.

### Funziona con set di dati di grandi dimensioni?

Sì, ma tieni d'occhio il limite di celle della versione gratuita (150 k celle). Per report molto grandi, valuta la licenza a pagamento o lo streaming dei dati riga per riga con `worksheet.Cells[row, col].Value = …`—anche se perderai la comodità del metodo a una riga.

### Come importare dati con formattazione da un modello Excel esistente?

Puoi caricare prima un workbook modello:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

In questo modo conservi loghi di intestazione, piè di pagina e qualsiasi stile preesistente, continuando a **importare dati con formattazione** per la parte dinamica.

---

## Esempio completo funzionante (pronto per il copia‑incolla)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Esegui il programma (`dotnet run`) e apri il file *Report.xlsx* generato per vedere i colori applicati immediatamente.

---

## Conclusione

Ora disponi di una soluzione solida, fine‑tuned per importare dati con formattazione in Excel usando C#. Buon lavoro!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}