---
category: general
date: 2026-09-21
description: Configura SmartMarkerOptions ArrayAsSingle in C# per esportare gli array
  JSON come valore unico in una cella di una cartella di lavoro Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: it
lastmod: 2026-09-21
og_description: Configura SmartMarkerOptions ArrayAsSingle in C# per esportare gli
  array JSON come valore di una singola cella. Scopri la soluzione completa passo‑passo.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Configura SmartMarkerOptions ArrayAsSingle in C# – guida completa
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Configura SmartMarkerOptions ArrayAsSingle in C# per gli array JSON
url: /it/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configura SmartMarkerOptions ArrayAsSingle in C# per array JSON

Se hai bisogno di **configurare SmartMarkerOptions ArrayAsSingle** durante la generazione di file Excel con Aspose.Cells, questa guida ti mostra esattamente come farlo. Vedrai come mantenere intatto un array JSON in una singola cella invece di distribuire i suoi elementi su più righe.

Lavorare con dati JSON nei fogli di calcolo spesso significa scegliere tra una visualizzazione appiattita e una rappresentazione compatta. In molti scenari di reporting — come la memorizzazione di un elenco di tag o di un set di identificatori — desideri che l’intera stringa JSON rimanga in una singola cella. Il flag **ArrayAsSingle** in `SmartMarkerOptions` rende possibile questa operazione.

In questo tutorial tu:

* Creerai un `DataTable` che contiene un array JSON in una colonna.
* Inserirai Smart Markers in un foglio di lavoro Excel.
* **Configurerai SmartMarkerOptions ArrayAsSingle** in modo che l’array JSON sia trattato come valore di una singola cella.
* Elaborerai i marker e salverai la cartella di lavoro.
* Verificherai l’output.

> **Prerequisiti** – È necessaria la libreria Aspose.Cells per .NET (v23.12 o successiva) e un ambiente di sviluppo .NET (Visual Studio 2022 consigliato). Si presume una conoscenza di base di C# e dei DataTable.

---

## Step 1: Prepare the data source with a JSON array

Per prima cosa, costruisci un `DataTable` che imiti i dati che riceveresti da un servizio o da un database. La colonna **Names** contiene una stringa codificata in JSON che rappresenta un array di nomi.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Perché questo passaggio?*  
Gli Smart Markers leggono i dati direttamente dagli oggetti .NET. Inserendo l’array JSON in una colonna di tipo stringa, preservi la sintassi JSON esatta, che in seguito può essere scritta in una cella senza modifiche.

---

## Step 2: Insert Smart Markers into a new workbook

Crea una nuova cartella di lavoro, seleziona il primo foglio e scrivi gli Smart Markers che fanno riferimento all’intera tabella e alla colonna **Names** specifica.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Il marker `&=dataTable.Names` indica ad Aspose.Cells di sostituire la cella con il valore della colonna **Names** per ogni riga in `dataTable`. Poiché abbiamo solo una riga, il marker verrà elaborato una sola volta.

---

## Step 3: **Configure SmartMarkerOptions ArrayAsSingle**

Per impostazione predefinita, Aspose.Cells espande una stringa simile a un array in righe separate. Impostare `ArrayAsSingle` a `true` sovrascrive questo comportamento, costringendo l’intera stringa JSON a rimanere in una singola cella.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Perché abilitare `ArrayAsSingle`?*  
Quando `ArrayAsSingle` è `false`, il motore interpreta `["Alice","Bob"]` come due valori separati e li scrive in righe adiacenti. Impostandolo a `true` la stringa viene trattata come valore atomico, fondamentale per preservare il formato JSON all’interno di Excel.

---

## Step 4: Process the Smart Markers with the configured options

Ora esegui il motore Smart Marker, passando l’oggetto opzioni appena configurato.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Durante l’elaborazione, Aspose.Cells legge il `dataTable`, applica i marker e rispetta il flag `ArrayAsSingle`, lasciando intatto l’array JSON.

---

## Step 5: Save the workbook and verify the result

Infine, scrivi la cartella di lavoro su disco. Apri il file generato in Excel o in qualsiasi visualizzatore di fogli di calcolo per confermare che la cella **A2** contenga esattamente la stringa JSON.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Output previsto

| A   |
|-----|
| **["Alice","Bob"]** |

La cella **A2** mostra l’array JSON come valore di testo unico, esattamente come memorizzato nel `DataTable`. Non vengono create righe aggiuntive.

---

## Common variations and edge‑case handling

| Situazione | Come adattare |
|------------|---------------|
| **Più righe con array JSON** | La stessa impostazione `ArrayAsSingle` funziona; l’array JSON di ogni riga rimane nella propria cella. |
| **Strutture JSON diverse (oggetti, array annidati)** | Finché il JSON è una stringa, `ArrayAsSingle` lo manterrà intatto. Per oggetti complessi potresti dover eseguire l’escape delle virgolette. |
| **Utilizzo di una fonte dati diversa (es. List\<T\>)** | Sostituisci il `DataTable` con qualsiasi collezione enumerabile; la sintassi del marker (`&=myList.Property`) rimane invariata. |
| **Esportazione in CSV invece di XLSX** | `ArrayAsSingle` si applica comunque, ma ricorda che il CSV non preserva la formattazione delle celle; potresti dover racchiudere il JSON tra virgolette. |

**Suggerimento professionale:** Imposta sempre `ArrayAsSingle` *prima* di chiamare `ProcessSmartMarkers`. Modificare il flag dopo l’elaborazione non ha effetto sulle celle già generate.

---

## Full, runnable example

Di seguito trovi il programma completo che puoi copiare‑incollare in un’applicazione console. Include tutte le direttive `using` e i commenti per chiarezza.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Esegui il programma, apri `SmartMarkerJson.xlsx` e vedrai l’array JSON preservato nella cella **A2**.

---

## Conclusion

Ora sai come **configurare SmartMarkerOptions ArrayAsSingle** in C# per mantenere un array JSON come valore di una singola cella quando utilizzi gli smart markers di Aspose.Cells. I passaggi — preparare un `DataTable`, inserire i marker, impostare il flag `ArrayAsSingle`, elaborare e salvare — costituiscono un modello ripetibile che puoi applicare a qualsiasi scenario in cui è necessaria una rappresentazione compatta del JSON all’interno di Excel.

Successivamente, potresti esplorare:

* **Smart markers di Aspose.Cells** per iterare su collezioni.
* Esportare **oggetti JSON annidati** personalizzando la formattazione delle celle.
* Combinare **formattazione condizionale** con gli smart markers per report più ricchi.

Sentiti libero di sperimentare con strutture dati diverse e condividere i tuoi risultati. Buona programmazione!

## What Should You Learn Next?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}