---
category: general
date: 2026-03-29
description: Scopri come esportare tabelle Excel in testo semplice, scrivere stringhe
  su file e convertire tabelle Excel in CSV o TXT usando C#. Include codice completo
  e consigli.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: it
og_description: Come esportare tabelle Excel in file di testo in C#. Ottieni la soluzione
  completa, il codice e le migliori pratiche per convertire le tabelle Excel e salvare
  file TXT.
og_title: Come esportare dati Excel – Tutorial completo C#
tags:
- C#
- Excel
- File I/O
title: Come esportare i dati di Excel – Guida passo passo C#
url: /it/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare dati Excel – Guida completa C#  

Ti sei mai chiesto **come esportare dati Excel** senza aprire manualmente il foglio? Forse devi scaricare una tabella in un semplice file di testo per un sistema legacy, o vuoi un rapido export CSV per pipeline di data‑analysis. In questo tutorial percorreremo una soluzione pratica, end‑to‑end, che **scrive una stringa su file** e ti mostrerà esattamente come **convertire una tabella Excel** in un formato di testo delimitato usando C#.

Copriamo tutto, dal caricamento della cartella di lavoro, alla scelta della tabella giusta, alla configurazione delle opzioni di esportazione, fino al salvataggio del risultato come file `.txt`. Alla fine potrai **esportare la tabella come CSV** (o con qualsiasi delimitatore tu scelga) e vedrai anche qualche trucco utile per **salvare file txt C#**. Nessun tool esterno necessario—solo qualche pacchetto NuGet e un po' di codice.

---

## Cosa ti serve

- **.NET 6.0+** (o .NET Framework 4.7.2 se preferisci la versione classica)  
- Pacchetto NuGet **Syncfusion.XlsIO** (la classe `ExportTableOptions` si trova qui)  
- Un IDE C# di base (Visual Studio, VS Code, Rider—qualsiasi va bene)  
- Un workbook Excel che contenga almeno una tabella (useremo `ws.Tables[0]` nell’esempio)

> Pro tip: se non hai ancora la libreria Syncfusion, esegui  
> `dotnet add package Syncfusion.XlsIO.Net.Core` da linea di comando.

---

## Passo 1 – Apri il workbook e prendi la prima tabella  

Il primo passo è caricare il file Excel e ottenere un riferimento al foglio che contiene la tabella. Questo passaggio è cruciale perché l'operazione **convert excel table** funziona su un oggetto `ITable`, non su intervalli di celle grezzi.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Perché è importante:* Aprire il workbook con `using` garantisce il rilascio di tutte le risorse non gestite, evitando problemi di lock del file quando poi proverai a **write string to file**.

---

## Passo 2 – Configura le opzioni di esportazione (testo semplice, senza intestazioni, delimitatore punto e virgola)  

Ora diciamo a Syncfusion come vogliamo serializzare la tabella. `ExportTableOptions` ti permette di attivare o disattivare le intestazioni, scegliere un delimitatore e decidere se ottenere una stringa o un array di byte.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Perché è importante:* Impostare `IncludeHeaders = false` corrisponde spesso alle aspettative dei sistemi a valle che conoscono già l'ordine delle colonne. Cambiare il delimitatore è il modo per **export table as CSV** con un separatore personalizzato.

---

## Passo 3 – Esporta la tabella in una stringa  

Con le opzioni pronte, chiamiamo `ExportToString`. Questo metodo estrae l'intera tabella (tutte le righe) e restituisce una singola stringa pronta per l'output su file.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Perché è importante:* La chiamata `ExportToString` fa il lavoro pesante di convertire la griglia Excel in un formato delimitato. Rispetta il `Delimiter` impostato, così ottieni un risultato **export table as csv** pulito senza ulteriori elaborazioni.

---

## Passo 4 – Scrivi il testo esportato su disco  

Infine, persisti la stringa su disco. `File.WriteAllText` è il modo più semplice per **save txt file C#**; crea automaticamente il file se non esiste e lo sovrascrive altrimenti.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Perché è importante:* Scrivendo direttamente la stringa, eviti un passaggio di conversione aggiuntivo. Il file ora contiene righe come `Value1;Value2;Value3`, pronto per qualsiasi parser a valle.

---

## Esempio completo (tutti i passaggi in un unico posto)  

Di seguito trovi il programma completo, pronto per il copia‑incolla, che combina tutto quanto discusso. Include gestione degli errori e commenti per chiarezza.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Output previsto** (il contenuto di `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Ogni riga corrisponde a una riga della tabella Excel originale, con i valori separati da punti e virgola. Se cambi `Delimiter = ","` otterrai un classico file CSV.

---

## Domande frequenti & casi particolari  

### E se il mio workbook ha più tabelle?  
Puoi semplicemente cambiare `ws.Tables[0]` con l'indice appropriato, o iterare su `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Come includere le intestazioni di colonna?  
Imposta `IncludeHeaders = true` in `ExportTableOptions`. È utile quando il sistema a valle si aspetta una riga di intestazione.

### Posso esportare in una cartella diversa in modo dinamico?  
Assolutamente. Usa `Path.Combine` con `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` o qualsiasi percorso fornito dall'utente per rendere la soluzione più flessibile.

### E per file di grandi dimensioni?  
Per tabelle molto grandi, considera lo streaming dell'output invece di caricare l'intera stringa in memoria:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Funziona su .NET Core?  
Sì—Syncfusion.XlsIO supporta .NET 5/6/7. Basta referenziare il pacchetto NuGet appropriato e sei pronto.

---

## Pro tip per esportazioni affidabili  

- **Valida il percorso del file** prima di scrivere. Una directory mancante genera `DirectoryNotFoundException`.  
- **Usa `ExportAsString`** solo quando la tabella sta comodamente in memoria; altrimenti, utilizza `ExportToStream` per dataset enormi.  
- **Attenzione alla cultura**: se i tuoi dati contengono virgole come separatori decimali, scegli un delimitatore punto e virgola (`;`) o tab (`\t`) per evitare errori di parsing CSV.  
- **Blocca la versione**: Syncfusion a volte modifica le firme delle API. Fissa la versione del NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) per mantenere la build riproducibile.

---

## Conclusione  

In questa guida abbiamo mostrato **come esportare tabelle Excel** in file di testo semplice usando C#. Caricando il workbook, configurando `ExportTableOptions`, esportando la tabella in una stringa e infine **scrivendo la stringa su file**, ora disponi di un pattern robusto per **convert excel table**, **export table as csv** e **save txt file C#**.  

Sentiti libero di sperimentare—cambia il delimitatore, includi le intestazioni o itera su più tabelle. Lo stesso approccio funziona per generare report CSV, alimentare parser legacy o semplicemente archiviare contenuti di fogli di calcolo come file di testo leggeri.

Hai altri scenari da affrontare? Forse ti serve **write string to file** in modo asincrono, o vuoi comprimere l'output al volo. Dai un’occhiata ai nostri prossimi tutorial su *asynchronous file I/O in C#* e *zipping files with .NET* per continuare il percorso.

Buon coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}