---
category: general
date: 2026-05-30
description: Popola rapidamente il modello Excel e impara come riempire Excel con
  i dati usando Aspose.Cells SmartMarker. Guida completa in C# con codice eseguibile.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: it
og_description: Popola il modello Excel e riempi il file Excel con i dati usando Aspose.Cells
  SmartMarker. Segui questo tutorial passo‑passo in C# per risultati immediati.
og_title: Popola modello Excel – Inserisci dati Excel tramite SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Popola il modello Excel – Compila i dati Excel tramite SmartMarker
url: /it/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Popola il modello Excel – Inserisci dati in Excel tramite SmartMarker

Hai mai avuto bisogno di **popolare un modello Excel** ma non sapevi come automatizzare il processo? In questo tutorial ti mostreremo come **riempire Excel con dati** usando Aspose.Cells SmartMarker—uno strumento che trasforma una cartella di lavoro statica in un generatore di report dinamico.

Immagina di avere un foglio di fattura pre‑progettato, un cruscotto di vendite o qualsiasi modulo ripetibile. Invece di digitare manualmente i valori, puoi fornire un oggetto C# e lasciare che SmartMarker faccia il lavoro pesante. Alla fine di questa guida avrai un progetto completamente eseguibile che prende un modello, inserisce righe, totali e persino formattazione condizionale—tutto senza toccare l’interfaccia utente.

## Cosa imparerai

- Come preparare una fonte dati che corrisponda ai marker nel tuo modello Excel.  
- Come istanziare **SmartMarkerProcessor** e abilitare il supporto per gli intervalli.  
- Come **popolare il modello Excel** con collezioni annidate, come gli articoli di un ordine.  
- Suggerimenti per gestire casi particolari come collezioni vuote o formati numerici personalizzati.  

Nessun servizio esterno, nessuna macro VBA—solo puro C# e Aspose.Cells. Tutto ciò che ti serve è .NET 6 (o successivo) e il pacchetto NuGet Aspose.Cells.

## Prerequisiti

- Visual Studio 2022 (o qualsiasi IDE preferisci).  
- .NET 6 SDK installato.  
- Aspose.Cells per .NET (puoi ottenere una prova gratuita dal sito Aspose).  
- Un modello Excel di base con tag SmartMarker (ne creeremo uno tra poco).

Se qualcuno di questi ti è sconosciuto, non panico; i passaggi seguenti ti guidano attraverso ogni requisito.

## Passo 1: Progetta il modello Excel con i tag SmartMarker

Prima, apri una nuova cartella di lavoro e disponi le parti statiche—logo aziendale, intestazioni, ecc. Poi inserisci i segnaposto SmartMarker dove dovrebbero apparire i dati dinamici.

| Cell | Content |
|------|---------|
| A1   | **Fattura** |
| A3   | `{{CompanyName}}` |
| A5   | **Dettagli ordine** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Perché è importante:** SmartMarker legge le parentesi graffe doppie e le associa alle proprietà dell'oggetto che passerai in seguito. La collezione `Orders.Items` indica al motore di ripetere la riga per ogni elemento dell'elenco.

> **Consiglio:** Usa l'opzione `RangeSmartMarker` (la abiliteremo più tardi) quando hai bisogno che il motore espanda automaticamente l'intervallo—perfetto per tabelle che crescono o si riducono.

Salva il file come `InvoiceTemplate.xlsx` nella cartella `Resources` del tuo progetto.

## Passo 2: Prepara la fonte dati che corrisponde ai marker del modello

Ora creiamo un oggetto anonimo C# (o una classe fortemente tipizzata) i cui nomi di proprietà corrispondono ai marker. La chiave è replicare esattamente la gerarchia.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Perché è importante:** L'array `Orders` contiene un unico ordine, e ogni ordine ha un array `Items`. SmartMarker itererà su `Items`, clonando la riga per ogni elemento. Se in seguito avrai più ordini, basta aggiungere altri oggetti all'array `Orders`—non sono necessarie modifiche al codice.

## Passo 3: Carica il modello e crea un'istanza di SmartMarkerProcessor

Con i dati pronti, carichiamo la cartella di lavoro, creiamo il processore e gli diciamo di rispettare i marker di intervallo.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Perché è importante:** `SmartMarkerProcessor` è il motore che analizza i marker, espande gli intervalli e scrive i valori. Separando il processore dalla cartella di lavoro, mantieni il codice pulito e riutilizzabile.

## Passo 4: Elabora il foglio di lavoro con RangeSmartMarker abilitato

La magia avviene quando chiamiamo `Process`. Impostare `RangeSmartMarker = true` indica a SmartMarker di trattare l'intero intervallo di righe come un blocco ripetibile, inserendo o eliminando righe automaticamente secondo necessità.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

A questo punto il motore ha:

1. Scansionato il foglio di lavoro alla ricerca di tag `{{...}}`.  
2. Mappato ogni tag a una proprietà su `data`.  
3. Rilevato l'intervallo della tabella (A7:D7) e duplicato tre volte—una per ogni elemento.  
4. Calcolato l'espressione `Price * Qty` per la colonna totale.

## Passo 5: Salva la cartella di lavoro risultante

Infine, scrivi la cartella di lavoro popolata su disco (o trasmettila a un client web).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Apri `InvoicePopulated.xlsx` e vedrai una tabella ordinatamente riempita:

| Nome   | Quantità | Prezzo | Totale |
|--------|----------|--------|--------|
| Pen    | 2        | 1.5    | 3.00   |
| Notebook | 1      | 3.75   | 3.75   |
| Stapler | 1       | 5.00   | 5.00   |

Il passo di **popolare il modello Excel** è ora completato, e hai riempito con successo **Excel con dati** per qualsiasi numero di righe.

## Gestione dei casi comuni

### Collezioni vuote

Se `Items` è vuoto, SmartMarker lascerà intatta l'intestazione della tabella ma non inserirà righe. Per evitare uno spazio vuoto, puoi aggiungere un blocco condizionale:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Formati numerici personalizzati

A volte servono simboli di valuta o separatori delle migliaia. Dopo l'elaborazione, puoi applicare uno stile programmaticamente:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Grandi insiemi di dati

Per migliaia di righe, abilita l'opzione `UseFastMode` per migliorare le prestazioni:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Esempio completo funzionante

Di seguito trovi il programma completo, autonomo, che puoi copiare‑incollare in un'app console. Include tutti i directive `using`, la preparazione dei dati, l'elaborazione e il salvataggio.



## Cosa dovresti imparare dopo?

- [Popola Excel con dati usando Aspose.Cells e Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Come popolare le celle Excel con Aspose.Cells per .NET: Guida passo passo](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automatizza l'esportazione dei dati Excel usando Aspose.Cells per .NET: Guida passo passo](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}