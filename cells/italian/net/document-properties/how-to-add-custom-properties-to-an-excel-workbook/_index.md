---
category: general
date: 2026-10-01
description: Scopri come aggiungere proprietà personalizzate a una cartella di lavoro
  Excel utilizzando Aspose.Cells. Questa guida mostra anche come aggiungere l'ID del
  progetto e leggere le proprietà personalizzate.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: it
lastmod: 2026-10-01
og_description: Aggiungi proprietà personalizzate a una cartella di lavoro Excel con
  Aspose.Cells. Segui questo tutorial completo per aggiungere un ID progetto, impostare
  le informazioni del revisore e leggere le proprietà personalizzate programmaticamente.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Aggiungi proprietà personalizzate alla cartella di lavoro di Excel – guida
  passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come aggiungere proprietà personalizzate a una cartella di lavoro Excel
url: /it/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere proprietà personalizzate a una cartella di lavoro Excel

Se hai bisogno di **aggiungere proprietà personalizzate** a una cartella di lavoro Excel, questa guida ti mostra esattamente come farlo con Aspose.Cells per .NET. Imparerai anche come aggiungere un ID progetto, impostare il nome di un revisore e, successivamente, **leggere le proprietà personalizzate** dal file.

Lavorare con metadati personalizzati ti consente di incorporare informazioni specifiche per il business direttamente all'interno del foglio di calcolo, facilitando il tracciamento di proprietà, versione o qualsiasi altro contesto senza dover mantenere un database separato. I passaggi seguenti coprono l'intero flusso di lavoro end‑to‑end, dalla creazione della cartella di lavoro alla persistenza delle nuove proprietà.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate  
* Una licenza valida di Aspose.Cells per .NET (o una prova gratuita)  
* Visual Studio 2022 (o qualsiasi IDE C#)  

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.Cells`.

## Passo 1: Configurare il progetto e importare i namespace

Crea una nuova applicazione console e aggiungi il riferimento a Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Il namespace `Aspose.Cells` contiene le classi `Workbook`, `Worksheet` e `CustomPropertyCollection` che utilizzeremo.

## Passo 2: Caricare una cartella di lavoro esistente (o crearne una nuova)

Puoi iniziare con un file `.xlsb` esistente o generare una nuova cartella di lavoro. L'esempio seguente carica un file chiamato **Data.xlsb** situato in una cartella chiamata `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Se il file non esiste, sostituisci il codice con `new Workbook();` per creare una cartella di lavoro vuota.

## Passo 3: Aggiungere proprietà personalizzate al primo foglio di lavoro

L'operazione principale è **aggiungere proprietà personalizzate** a un foglio di lavoro. Aspose.Cells memorizza le proprietà personalizzate in una collezione che si comporta come un dizionario.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Il motivo per cui usiamo `CustomProperties.Add` invece di `CustomProperties["Name"] = value` è che il metodo `Add` crea la voce se non esiste e garantisce che venga memorizzato il tipo di dato corretto. Questo approccio previene incompatibilità di tipo accidentali che potrebbero causare errori di runtime durante la lettura dei valori in seguito.

## Passo 4: Salvare la cartella di lavoro con le nuove proprietà

Dopo aver inserito i metadati, salva le modifiche in un nuovo file in modo che l'originale rimanga intatto.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

A questo punto il file Excel contiene i metadati personalizzati che hai definito. Puoi verificare le proprietà usando i passaggi nella sezione successiva.

## Passo 5: Leggere le proprietà personalizzate da una cartella di lavoro

La lettura delle **proprietà personalizzate di Excel** segue lo stesso modello di collezione. Questo frammento dimostra come recuperare i valori appena memorizzati.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

L'indicizzatore `CustomPropertyCollection` restituisce un oggetto `CustomProperty`; accedere alla sua proprietà `Value` ti fornisce i dati memorizzati nel loro tipo originale. Verificare la presenza di `null` prima del cast evita `NullReferenceException` se una proprietà è mancante.

### Output della console previsto

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Il timestamp rifletterà il momento esatto in cui hai chiamato `Add` al passo 3.

## Consiglio professionale: Aggiornare una proprietà personalizzata esistente

Se devi **aggiungere informazioni personalizzate** in seguito (ad esempio, modificare il revisore), usa il setter di `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Questo modello garantisce che la proprietà venga aggiornata o creata, il che è utile in flussi di lavoro iterativi come la generazione automatica di report.

## Passo 6: Verificare le proprietà in Excel (opzionale)

1. Apri il file salvato `DataWithProps.xlsb` in Microsoft Excel.  
2. Vai su **File → Info → Proprietà → Proprietà avanzate**.  
3. Seleziona la scheda **Personalizzate**.  

Vedrai le voci `ProjectId`, `Reviewer` e `CreatedOn` elencate con i rispettivi valori.

## Esempio completo funzionante

Di seguito trovi il programma completo e autonomo che combina tutti gli snippet precedenti. Copialo in `Program.cs` ed eseguilo; la console mostrerà i valori recuperati.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

L'esecuzione di questo programma produce l'output della console mostrato in precedenza e crea `DataWithProps.xlsb` contenente i metadati incorporati.

## Domande comuni e casi particolari

| Domanda | Risposta |
|---|---|
| **Posso memorizzare tipi non primitivi?** | Aspose.Cells supporta `string`, `int`, `double`, `DateTime` e `bool`. Per oggetti complessi, serializzali prima in JSON o XML e memorizza la stringa. |
| **E se la cartella di lavoro è protetta da password?** | Apri la cartella di lavoro con una password (`new Workbook(path, password)`) prima di accedere a `CustomProperties`. Le proprietà rimangono accessibili dopo la decrittazione. |
| **Le proprietà personalizzate sopravvivono alla conversione di formato?** | Quando si salva in un formato diverso (ad esempio, `.xlsx`), Aspose.Cells preserva le proprietà personalizzate purché il formato di destinazione le supporti. |
| **Come eliminare una proprietà personalizzata?** | Usa `worksheet.CustomProperties.Remove("PropertyName");`. Questo rimuove la voce dalla collezione. |

## Prossimi passi

Ora che sai **come aggiungere proprietà personalizzate**, potresti esplorare argomenti correlati come:

* **excel custom properties** per il versionamento dei documenti  
* **read custom properties** da più fogli di lavoro in una singola cartella  
* Utilizzare **Aspose.Cells** per creare tabelle pivot che fanno riferimento ai metadati personalizzati  
* Esportare la cartella di lavoro in PDF mantenendo le proprietà personalizzate  

Sperimenta con diversi tipi di dati, combina le proprietà personalizzate con i commenti delle celle o integra i metadati in un più ampio sistema di gestione dei documenti.

**Pronto a automatizzare i tuoi report Excel?** Aggiungi il codice sopra al tuo progetto, adatta i nomi delle proprietà alle esigenze della tua azienda, e avrai un foglio di calcolo auto‑descrittivo pronto per l'elaborazione successiva.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea cartella di lavoro Excel – Aggiungi proprietà personalizzate e salva come XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Come accedere alle proprietà personalizzate del documento in Excel usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Padroneggia le proprietà personalizzate di Excel usando Aspose.Cells .NET per una gestione dati avanzata](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}