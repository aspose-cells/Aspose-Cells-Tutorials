---
category: general
date: 2026-03-25
description: Impara come esportare Excel in DataTable in C# rapidamente. Questo tutorial
  copre l'esportazione di Excel con i nomi delle colonne e l'esportazione dei dati
  di Excel come stringa per una gestione affidabile dei dati.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: it
og_description: Esporta Excel in DataTable in C# con nomi delle colonne e conversione
  in stringa. Segui questo tutorial conciso per una soluzione pronta all'uso.
og_title: Esporta Excel in DataTable in C# – Guida completa
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Esporta Excel in DataTable in C# – Guida passo passo
url: /it/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Excel in DataTable in C# – Guida passo‑passo

Hai mai avuto bisogno di **esportare Excel in DataTable** ma non eri sicuro di quali flag attivare? Non sei solo—molti sviluppatori incontrano lo stesso ostacolo quando provano per la prima volta a estrarre i dati di un foglio di calcolo in un `DataTable`.  

La buona notizia? Con poche righe di codice puoi **esportare Excel con i nomi delle colonne** e persino **esportare i dati di Excel come stringa** per evitare problemi di incompatibilità di tipo. Di seguito troverai un esempio completo e funzionante più il “perché” di ogni impostazione, così potrai adattarlo a qualsiasi progetto senza indovinare.

## Cosa copre questo tutorial

* Come creare un workbook in memoria (senza file fisico necessario).  
* Popolare alcune righe di esempio così puoi vedere subito il risultato.  
* Configurare `ExportTableOptions` affinché ogni cella sia trattata come stringa.  
* Esportare un intervallo rettangolare in un `DataTable` mantenendo la prima riga come intestazioni di colonna.  
* Verificare l'output e stampare la prima riga sulla console.  

Nessun link a documentazione esterna necessario—tutto ciò che ti serve è qui. Se hai già un file Excel su disco, basta sostituire la riga di creazione del workbook con `new Workbook("path/to/file.xlsx")` e sei pronto.

---

## Passo 1: Configura il progetto e aggiungi il pacchetto NuGet Aspose.Cells

Prima di scrivere qualsiasi codice, assicurati che il tuo progetto faccia riferimento a **Aspose.Cells for .NET** (la libreria che fornisce la classe `Workbook`). Puoi aggiungerlo tramite il NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Suggerimento:** Usa l'ultima versione stabile (a partire da marzo 2026, è la 22.12) per ottenere le correzioni di bug più recenti e miglioramenti delle prestazioni.

---

## Passo 2: Crea un Workbook e riempilo con dati di esempio

Inizieremo con un `Workbook` nuovissimo e scriveremo un paio di righe così potrai vedere l'esportazione in azione. Questo passaggio dimostra anche **come esportare excel in datatable** quando i dati di origine sono solo in memoria.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Perché è importante:* Inserendo prima la riga di intestazione (`A1` & `B1`), possiamo successivamente indicare all'esportatore di trattare la prima riga come nomi di colonna—esattamente ciò che significa **esportare excel con i nomi delle colonne**.

---

## Passo 3: Indica ad Aspose.Cells di trattare ogni cella come stringa

Quando esporti celle numeriche o di data, Aspose tenta di dedurre il tipo .NET. Questo può causare bug sottili se il tuo codice a valle si aspetta stringhe. Il flag `ExportTableOptions.ExportAsString` forza una conversione uniforme in stringa.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Perché usarlo?* Immagina una colonna che a volte contiene numeri e a volte testo (ad esempio “00123” vs. “ABC”). Esportando tutto come stringa eviti di perdere gli zeri iniziali o di generare eccezioni di conversione di tipo.

---

## Passo 4: Esporta l'intervallo desiderato in un DataTable

Ora effettivamente **esportiamo excel in datatable**. Il metodo `ExportDataTable` accetta la riga/colonna di inizio, il numero di righe/colonne, un flag per l'estrazione dei nomi delle colonne e le opzioni che abbiamo appena creato.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Cosa succede dietro le quinte?*  
- `startRow: 0` indica la prima riga di Excel (la riga di intestazione).  
- `exportColumnNames: true` indica ad Aspose di trasferire “Name” e “Age” nella collezione di colonne del `DataTable`.  
- `totalRows`/`totalColumns` possono essere più grandi dei dati reali; le celle in eccesso diventano stringhe vuote grazie a `ExportAsString`.

---

## Passo 5: Verifica il risultato – Stampa la prima riga

Un rapido dump sulla console dimostra che la conversione è riuscita e che i nomi delle colonne sono intatti.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Output previsto**

```
First row: Alice, 30
```

Se cambi i dati di esempio, la console rifletterà automaticamente tali modifiche—non è necessario alcun codice aggiuntivo.

---

## Domande frequenti & casi particolari

| Question | Answer |
|----------|--------|
| **Posso esportare un foglio che esiste già su disco?** | Sì—sostituisci `new Workbook()` con `new Workbook("myFile.xlsx")`. Il resto dei passaggi rimane identico. |
| **Cosa succede se il mio file Excel ha celle unite?** | Le celle unite vengono separate; il valore della cella in alto a sinistra viene usato per l'intero intervallo unito. |
| **Devo preoccuparmi dei formati numerici specifici per cultura?** | No quando `ExportAsString = true`; tutto arriva come la stringa grezza mostrata in Excel. |
| **Quante righe posso esportare in una volta?** | Aspose.Cells può gestire milioni di righe, ma il consumo di memoria cresce con le dimensioni del `DataTable`. Considera il paging se raggiungi i limiti. |
| **E le colonne nascoste?** | Le colonne nascoste vengono esportate a meno che non imposti `ExportHiddenColumns = false` in `ExportTableOptions`. |

---

## Bonus: Esportare in CSV invece di DataTable

Talvolta potresti preferire un file piatto. Le stesse `ExportTableOptions` possono essere riutilizzate con `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Quella singola riga ti fornisce un CSV pronto per l'importazione mantenendo **l'esportazione dei dati di excel come stringa**.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Esegui il programma (`dotnet run`) e vedrai il risultato del **export excel to datatable** stampato sulla console. Sostituisci i dati di esempio, modifica `totalRows`/`totalColumns` o punta il workbook a un file reale—tutto scala.

---

## Conclusione

Ora hai una **soluzione completa e autonoma per esportare Excel in DataTable** in C#. Configurando `ExportTableOptions.ExportAsString` garantisci che **l'esportazione dei dati di excel sia come stringa**, e impostando `exportColumnNames: true` ottieni le familiari intestazioni di colonna che ti aspetti quando **esporti excel con i nomi delle colonne**.

* Alimenta il `DataTable` in Entity Framework o Dapper per inserimenti massivi.  
* Passalo a un motore di reporting come **FastReport** o **RDLC**.  
* Converti in JSON per una risposta API (`JsonConvert.SerializeObject(table)`).

Sentiti libero di sperimentare—prova a esportare un foglio più grande, o combina questo con **how to export excel to datatable** da una condivisione di rete. Il modello rimane lo stesso e il codice è pronto per la produzione.

---

![Diagramma del flusso di conversione Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "diagramma export excel to datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}