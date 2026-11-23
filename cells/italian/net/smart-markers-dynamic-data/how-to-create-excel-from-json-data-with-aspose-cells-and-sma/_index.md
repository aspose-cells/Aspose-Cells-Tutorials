---
category: general
date: 2026-11-22
description: Impara a creare Excel da dati JSON in C# usando Aspose.Cells Smart Marker.
  Guida passo‑passo che copre la progettazione del modello, la gestione del JSON e
  l'esportazione del file.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: it
lastmod: 2026-11-22
og_description: Crea un file Excel dai dati JSON utilizzando Aspose.Cells Smart Marker.
  Segui questo breve tutorial per generare una cartella di lavoro completamente formattata
  da un array JSON.
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: Crea Excel da dati JSON in C# – guida completa ad Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come creare un file Excel da dati JSON con Aspose.Cells e Smart Marker
url: /it/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare Excel da dati JSON con Aspose.Cells e Smart Marker

Se hai bisogno di **creare Excel da dati JSON** in un'applicazione .NET, questo tutorial ti mostra una soluzione completa, pronta per la produzione. Vedrai come incorporare un array JSON in una singola cella, utilizzare la funzionalità **Smart Marker** di **Aspose.Cells**, e generare una cartella di lavoro finale senza dover scrivere codice cella per cella manualmente.

L'approccio funziona con qualsiasi payload JSON—che tu stia esportando risultati di API, serializzando oggetti o creando report. Alla fine della guida avrai un progetto C# pronto all'uso che legge una stringa JSON, la applica a un **modello Excel**, e salva il risultato in un nuovo file.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.6+)
- Visual Studio 2022 (o qualsiasi IDE che supporti C#)
- **Aspose.Cells for .NET** pacchetto NuGet (versione 23.10 o successiva)
- Un semplice file modello Excel che contiene il tag Smart Marker `<%=Fruits:ArrayAsSingle%>` nella cella di destinazione

> **Suggerimento:** Mantieni il modello in una cartella a cui la tua applicazione può accedere a runtime (ad es., `Resources` o un percorso configurabile).  

## Passo 1: Preparare il payload JSON

Prima, definisci l'array JSON che vuoi inserire nel foglio di lavoro. In questo esempio utilizziamo un elenco di nomi di frutta.

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

La stringa JSON può essere generata dinamicamente (ad es., `JsonSerializer.Serialize(myList)`) o letta da una fonte esterna come un'API REST. Il punto chiave è che la stringa deve essere un array JSON valido perché **Smart Marker** si aspetta una rappresentazione JSON quando si utilizza l'opzione `ArrayAsSingle`.

## Passo 2: Costruire la sorgente dati per Smart Marker

Il motore Smart Marker di Aspose.Cells funziona con qualsiasi oggetto .NET. Creiamo un oggetto anonimo che contiene la stringa JSON sotto una proprietà chiamata `Fruits`. Il nome della proprietà deve corrispondere al nome del marker usato nel modello.

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **Perché un oggetto anonimo?** Ti consente di passare un contenitore di dati leggero senza definire una classe dedicata, il che accelera il prototipaggio. Per progetti più grandi puoi sostituirlo con un DTO fortemente tipizzato.

## Passo 3: Progettare il modello Excel con un segnaposto Smart Marker

Crea un file Excel (`SmartMarkerTemplate.xlsx`) che contiene il segnaposto dove apparirà il JSON. Inserisci il seguente marker nella cella desiderata (ad es., **A1**):

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – corrisponde al nome della proprietà nella sorgente dati.
- `ArrayAsSingle` – indica a Smart Marker di scrivere l'intero array JSON come una singola stringa, preservando parentesi e virgolette.

![Excel template with Smart Marker placeholder](excel-template.png){alt="Modello Excel contenente <%=Fruits:ArrayAsSingle%> per creare Excel da dati JSON"}

## Passo 4: Caricare la cartella di lavoro e inizializzare il processore Smart Marker

Ora carica il file modello in un'istanza `Aspose.Cells.Workbook` e crea un `SmartMarkerProcessor` che gestirà la sostituzione.

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

Caricare la cartella di lavoro una sola volta e riutilizzare la stessa istanza `SmartMarkerProcessor` è più efficiente rispetto a creare un nuovo processore per ogni cella.

## Passo 5: Applicare la sorgente dati per sostituire il marker

Il metodo `ApplyTemplate` esamina la cartella di lavoro alla ricerca di tutti i marker e li sostituisce con i valori dell'oggetto fornito.

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

Poiché abbiamo usato `ArrayAsSingle`, la cella ora contiene la stringa JSON grezza:

```
["Apple","Banana","Cherry"]
```

Se hai bisogno di un formato diverso (ad es., un elenco separato da virgole), potresti usare `ArrayAsCommaSeparated` invece di `ArrayAsSingle`.

## Passo 6: Salvare la cartella di lavoro elaborata

Infine, scrivi la cartella di lavoro modificata in un nuovo file. Puoi scegliere qualsiasi formato supportato (`.xlsx`, `.xls`, `.csv`, ecc.).

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

Il file risultante `JsonExported.xlsx` può essere aperto in Excel, Google Sheets o qualsiasi visualizzatore compatibile, e mostrerà l'array JSON esattamente come inserito.

## Esempio completo funzionante

Mettere insieme tutti i pezzi ti fornisce un programma console autonomo:

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### Output previsto

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

## Gestione di variazioni comuni e casi limite

| Situazione                                 | Regolazione consigliata |
|-------------------------------------------|------------------------|
| **Oggetti JSON di grandi dimensioni** (dizionari annidati) | Usa `ArrayAsJson` per incorporare l'intera gerarchia di oggetti, oppure mappa il JSON a un modello fortemente tipizzato e utilizza marker annidati (`<%=Parent.Child%>`). |
| **Array JSON multipli** in celle diverse | Aggiungi proprietà aggiuntive all'oggetto anonimo (ad es., `Vegetables = vegJson`) e i corrispondenti marker (`<%=Vegetables:ArrayAsSingle%>`). |
| **Necessità di suddividere l'array in righe** | Sostituisci `ArrayAsSingle` con `Array` – Smart Marker creerà una nuova riga per ogni elemento. |
| **Modello memorizzato come risorsa incorporata** | Carica la cartella di lavoro da uno stream: `Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`. |
| **Esecuzione in ASP.NET Core** | Usa `IWebHostEnvironment.ContentRootPath` per costruire il percorso completo al modello e ai file di output. |

## Considerazioni sulle prestazioni

- **Riutilizza l'oggetto `Workbook`** quando elabori molti record in batch; crea il processore una sola volta per cartella di lavoro.
- **Disabilita il calcolo** (`workbook.CalculateFormula = false`) se il modello contiene formule complesse che non sono necessarie per la fase di inserimento del JSON.
- **Salvataggio in streaming** (`workbook.Save(stream, SaveFormat.Xlsx)`) riduce il carico I/O quando si invia il file direttamente nella risposta al client.

## Conclusione

Ora sai come **creare Excel da dati JSON** in C# usando **Aspose.Cells** e la funzionalità **Smart Marker**. Il tutorial ha coperto la preparazione del JSON, la creazione della sorgente dati, la progettazione del modello, l'elaborazione dei marker e il salvataggio del file—tutto all'interno di un unico programma eseguibile.

Da qui puoi:

- Estendere il modello con tag **Smart Marker** aggiuntivi per report più ricchi.
- Passare a `Array` o `ArrayAsJson` per esportare il JSON come righe o strutture annidate.
- Combinare questa tecnica con librerie di generazione Excel in **C#** come EPPlus o ClosedXML se ti serve un'alternativa gratuita.

Buona programmazione e divertiti a trasformare JSON in cartelle di lavoro Excel rifinite!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Importa dati JSON in Excel usando Aspose.Cells Java: Guida completa](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Tutorial Aspose Cells GridJs – Esporta dati Excel in JSON con caricamento lazy](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [Crea Excel a partire da JSON con Smart Marker di Aspose.Cells](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}