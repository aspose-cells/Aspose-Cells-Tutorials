---
category: general
date: 2026-11-16
description: Crea Excel da JSON usando SmartMarker. Scopri come convertire JSON in
  Excel, incorporare JSON in Excel e salvare il file di lavoro xlsx in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: it
lastmod: 2026-11-16
og_description: Crea Excel da JSON rapidamente. Questo tutorial mostra come convertire
  JSON in Excel, incorporare JSON in Excel e salvare il workbook xlsx con Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Crea Excel da JSON con SmartMarker – guida passo‑passo C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Crea Excel da JSON con SmartMarker in C#
url: /it/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Excel da JSON con SmartMarker in C#

Se hai bisogno di **creare Excel da JSON** in un progetto .NET, questa guida mostra una soluzione completa e eseguibile. Utilizzando il processore Smart Marker di Aspose.Cells puoi **convertire JSON in Excel**, inserire la stringa JSON direttamente in una cella e **salvare il workbook xlsx** senza scrivere alcun codice di parsing manuale.

Vedrai come registrare una fonte di dati JSON, inserire uno Smart Marker che restituisce l'intero array come una singola stringa JSON, elaborare il foglio di lavoro e infine scrivere il file su disco. Alla fine del tutorial potrai generare un file Excel che contiene il payload JSON originale nella cella A1, pronto per l'elaborazione o il reporting a valle.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+)
- Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`)
- Conoscenze di base di C# e formattazione JSON
- Un IDE come Visual Studio o VS Code

## Passo 1: Configura il progetto e importa i namespace

Crea una nuova applicazione console e aggiungi il pacchetto Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Quindi includi i namespace richiesti all'inizio di `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Perché?**  
`Aspose.Cells` fornisce il modello del workbook, mentre `Aspose.Cells.SmartMarkers` contiene la classe `SmartMarkerProcessor` che interpreta i marker `&=` nel foglio di lavoro.

## Passo 2: Definisci la fonte di dati JSON

Inserisci la stringa JSON in una variabile. In questo esempio abbiamo un array di ordini:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Perché?**  
Smart Marker funziona con qualsiasi JSON ben formato. Tenere il JSON in una stringa ti consente di registrarlo direttamente senza la necessità di un file su disco.

## Passo 3: Registra i dati JSON con SmartMarkerProcessor

Crea un'istanza di `SmartMarkerProcessor` e associa la stringa JSON a un nome che utilizzerai più tardi nel foglio di lavoro:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Perché?**  
`RegisterJsonDataSource` analizza il JSON e rende disponibile la sua gerarchia agli Smart Marker. Il nome `"OrdersJson"` diventa l'oggetto radice nelle espressioni dei marker.

## Passo 4: Crea un workbook e inserisci lo Smart Marker

Istanzia un nuovo workbook, ottieni il suo primo foglio di lavoro e scrivi uno Smart Marker nella cella A1 che restituirà l'intero array `Orders` come una singola stringa JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Perché?**  
L'espressione `OrdersJson.Orders.ArrayAsSingle` indica a Smart Marker di prendere l'array `Orders` e serializzarlo nuovamente in JSON, inserendo il risultato nella cella di destinazione. Questo è il modo più semplice per **incorporare JSON in Excel**.

## Passo 5: Elabora il foglio di lavoro

Esegui il processore in modo che sostituisca il marker con la stringa JSON effettiva:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Perché?**  
L'elaborazione esamina ogni cella alla ricerca di marker `&=`, li valuta rispetto alle fonti di dati registrate e scrive il valore valutato nuovamente nel foglio di lavoro.

## Passo 6: Salva il workbook come file .xlsx

Infine, scrivi il workbook su disco. Regola il percorso a una cartella in cui hai i permessi di scrittura:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Perché?**  
`SaveFormat.Xlsx` garantisce che il file sia salvato nel moderno formato Office Open XML, soddisfacendo il requisito di **salvare il workbook xlsx**.

## Codice sorgente completo

Mettendo insieme tutti i pezzi, ecco il programma completo, pronto per l'esecuzione:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Output previsto in Excel

Apri `JsonArraySingleCell.xlsx`. La cella A1 conterrà:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

La stringa JSON è una rappresentazione compatta dell'array `Orders` originale, rendendo più semplice il trasporto o il consumo nei flussi di lavoro basati su Excel a valle.

## Variazioni comuni e casi limite

| Situazione | Adeguamento |
|-----------|------------|
| **Multiple JSON objects** | Registra ogni oggetto con un nome distinto (ad es., `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) e riferiscili con marker separati. |
| **Pretty‑printed JSON in a cell** | Usa l'opzione `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Large JSON payloads** | Considera di scrivere il JSON in un foglio nascosto o di utilizzare la conversione in `DataTable` per migliori prestazioni. |
| **Embedding JSON in multiple cells** | Posiziona marker diversi in altre celle, ad es., `&=OrdersJson.Orders[0].Id` per estrarre campi individuali. |

**Consiglio:** Quando si gestiscono JSON molto grandi, aumenta il buffer di memoria del workbook (`WorkbookSettings.MemorySetting`) per evitare `OutOfMemoryException`.

## Testare la soluzione

1. Compila ed esegui l'app console (`dotnet run`).  
2. Verifica che la console stampi il percorso completo del file generato.  
3. Apri il file in Excel o in qualsiasi visualizzatore di fogli di calcolo.  
4. Conferma che la cella A1 contenga la stringa dell'array JSON esattamente come mostrato sopra.

Se la cella contiene il testo del marker (`&=OrdersJson...`) invece del JSON, verifica che il processore sia stato invocato **dopo** aver inserito il marker e che la stringa JSON sia valida.

## Conclusione

Ora sai come **creare Excel da JSON** usando Aspose.Cells Smart Markers, come **convertire JSON in Excel**, incorporare il payload JSON direttamente in una cella e **salvare il workbook xlsx** con una sola riga di codice. Questo approccio elimina il parsing manuale, funziona con qualsiasi struttura JSON e produce un file Excel pulito e conforme agli standard.

### Prossimi passi

- Esplora i **cicli Smart Marker** (`&=OrdersJson.Orders`) per generare una riga per ogni ordine invece di una singola stringa JSON.  
- Combina questa tecnica con le **formule Excel** per calcolare i totali dai dati incorporati.  
- Approfondisci la **lettura di JSON da Excel** usando `Workbook.Load` e `SmartMarkerProcessor` al contrario.

Sentiti libero di sperimentare con diverse forme di JSON, più fogli di lavoro o l'esportazione in altri formati come CSV o PDF. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea Excel da JSON con Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Crea Workbook Excel da JSON – Guida completa Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Salva Workbook Excel da JSON – Guida completa](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}