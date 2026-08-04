---
category: general
date: 2026-02-09
description: Rimuovi l'interfaccia di filtro in Excel con C# eliminando il pulsante
  AutoFilter. Scopri come nascondere il pulsante filtro, mostrare la riga di intestazione
  e mantenere i fogli ordinati.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: it
og_description: Interfaccia di filtro pulita in Excel con C#. Questa guida mostra
  come nascondere il pulsante del filtro, visualizzare la riga di intestazione e mantenere
  i fogli di lavoro puliti.
og_title: Interfaccia per cancellare il filtro in Excel con C# – Rimuovi il pulsante
  AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Interfaccia per cancellare il filtro in Excel con C# – Rimuovi il pulsante
  AutoFilter
url: /it/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

: "Interfaccia di filtro pulita in Excel con C# – Rimuovere il pulsante AutoFilter". Good.

Then paragraph.

Proceed.

Make sure to keep code block placeholders unchanged.

Let's produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interfaccia di filtro pulita in Excel con C# – Rimuovere il pulsante AutoFilter

Ti è mai capitato di dover **cancellare l'interfaccia di filtro** in un foglio Excel ma non sapevi quale riga di codice nasconde davvero quella piccola freccia a discesa? Non sei il solo. Il pulsante di filtro può risultare fastidioso quando si invia un report agli utenti finali che non hanno mai bisogno di modificare la visualizzazione.  

In questo tutorial vedremo un esempio completo e funzionante che **rimuove il pulsante AutoFilter** da una tabella, garantisce che la riga di intestazione rimanga visibile e tocca anche come *nascondere il pulsante di filtro* in modo permanente. Alla fine saprai esattamente **come rimuovere AutoFilter** in C# e perché ogni passaggio è importante.

## Cosa ti serve

- .NET 6+ (o .NET Framework 4.7.2+) – qualsiasi runtime recente va bene.  
- Il pacchetto NuGet **EPPlus** (versione 6.x o successiva) – fornisce `ExcelWorksheet`, `ExcelTable`, ecc.  
- Un semplice file Excel con una tabella chiamata **SalesTable** (creala in pochi click, se necessario).

Questo è tutto. Nessun COM interop, nessuna DLL aggiuntiva, solo qualche `using` e poche righe di codice.

## Interfaccia di filtro pulita: rimuovere il pulsante AutoFilter

Il cuore della soluzione è costituito da tre piccolissime istruzioni. Analizziamole così da capire *perché* sono necessarie, non solo *cosa* fanno.

### Passo 1 – Ottenere un riferimento alla tabella

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Perché è importante: EPPlus lavora con **tabelle** (`ExcelTable`), non con intervalli grezzi. Ottenendo l'oggetto tabella accediamo alla proprietà `AutoFilter`, che controlla l'elemento UI visibile sul foglio. Se provi a manipolare direttamente il foglio di lavoro, influenzerai solo i valori, non il pulsante di filtro.

### Passo 2 – Rimuovere la riga del pulsante AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Impostare `AutoFilter` a `null` dice a EPPlus di eliminare la riga di filtro sottostante. Questa è l'operazione di *clear filter UI* che la maggior parte degli sviluppatori cerca quando chiedono “**come rimuovere autofilter**”. È un approccio pulito, in una sola riga, che funziona su qualsiasi versione di Excel supportata da EPPlus.

### Passo 3 – Mantenere visibile la riga di intestazione

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Quando elimini l'interfaccia di filtro, Excel a volte nasconde la riga di intestazione se il flag `ShowHeader` della tabella è impostato a false. Impostandolo esplicitamente a `true` garantiamo che i titoli delle colonne rimangano sullo schermo – un dettaglio sottile ma importante per un report finale curato.

### Esempio completo, eseguibile

Di seguito trovi una minima console app che apre una cartella di lavoro esistente, esegue i tre passaggi e salva il risultato. Copia‑incolla, premi **F5** e osserva il pulsante di filtro scomparire.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Risultato atteso:** Apri *SalesReport_NoFilter.xlsx* – le frecce di filtro non sono più presenti, ma le intestazioni delle colonne rimangono. Niente più “clic‑per‑filtrare” ingombrante.

> **Consiglio esperto:** Se hai **più tabelle** e vuoi nascondere il pulsante di filtro per tutte, itera su `worksheet.Tables` e applica le stesse tre righe all'interno del ciclo.

## Come rimuovere AutoFilter in Excel usando C# – approfondimento

Ti starai chiedendo: “E se la cartella di lavoro ha già un filtro applicato? Impostare `AutoFilter = null` elimina anche le righe filtrate?” La risposta è **sì**. EPPlus cancella sia l'interfaccia UI sia i criteri di filtro sottostanti, lasciando i dati nell'ordine originale.  

Se vuoi solo *nascondere* il pulsante mantenendo attivo il filtro, puoi invece impostare la proprietà `AutoFilter` a un **nuovo filtro vuoto**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Questa variante è utile quando desideri *nascondere il pulsante di filtro* per un aspetto più pulito ma permetti comunque agli utenti avanzati di attivare i filtri tramite VBA o il ribbon.

### Caso limite: tabelle senza riga di intestazione

Alcuni report legacy usano intervalli semplici anziché tabelle. In quel caso, EPPlus non espone un oggetto `ExcelTable`, quindi il codice sopra genererà un'eccezione. La soluzione è **convertire l'intervallo in una tabella** prima:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Ora hai *rimosso autofilter excel* anche su un intervallo che non partiva da una tabella formale.

## Mostrare la riga di intestazione dopo aver nascosto il pulsante di filtro – perché è importante

Una lamentela comune è che, dopo aver nascosto l'interfaccia di filtro, la riga di intestazione scompaia, soprattutto quando la cartella di lavoro è stata creata originariamente con “Hide Header” attivo. Impostando esplicitamente `salesTable.ShowHeader = true;` eviti questa sorpresa.  

Se devi **nascondere il pulsante di filtro** ma mantenere l'intestazione nascosta (ad esempio per generare un dump di dati grezzo), imposta semplicemente `salesTable.ShowHeader = false;` dopo aver cancellato il filtro. Il codice è simmetrico, il che lo rende facile da alternare in base a un flag di configurazione.

## Nascondere il pulsante di filtro – consigli pratici e insidie

- **Compatibilità di versione:** EPPlus 6+ funziona solo con file `.xlsx`. Se lavori con il vecchio formato `.xls`, dovrai usare un'altra libreria (ad es. NPOI) perché l'API *clear filter UI* non è disponibile.  
- **Performance:** Caricare una cartella di lavoro enorme solo per nascondere un pulsante può essere lento. Considera l'uso di `ExcelPackage.Load(stream, true)` per aprire in modalità **read‑only**, applicare la modifica, poi salvare.  
- **Testing:** Valida sempre manualmente il file di output la prima volta. I test UI automatizzati possono verificare che le frecce di filtro siano realmente assenti (`worksheet.Tables[0].AutoFilter == null`).  
- **Licenza:** EPPlus ha adottato una licenza duale dalla versione 5. Per progetti commerciali è necessaria una licenza a pagamento o l'uso di una libreria alternativa.

## File sorgente completo per copia‑incolla

Di seguito trovi il file esatto da inserire in un nuovo progetto console. Nessuna dipendenza nascosta, tutto è auto‑contenuto.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Esegui `dotnet add package EPPlus --version 6.0.8` (o la più recente) prima di compilare, e avrai un foglio pulito pronto per la distribuzione.

## Conclusione

Ti abbiamo appena mostrato **come rimuovere AutoFilter** e **cancellare l'interfaccia di filtro** in una cartella di lavoro Excel usando C#. Il nucleo di tre righe (`AutoFilter = null;`, `ShowHeader = true;`) fa il lavoro pesante, mentre il boilerplate circostante rende la soluzione

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}