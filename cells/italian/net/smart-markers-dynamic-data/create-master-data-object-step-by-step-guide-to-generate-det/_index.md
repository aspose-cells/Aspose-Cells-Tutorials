---
category: general
date: 2026-02-14
description: Crea un oggetto master data in C# e genera il foglio di dettaglio senza
  sforzo. Impara l'intero flusso di lavoro di SmartMarker con esempi pratici di codice.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: it
og_description: Crea un oggetto master data in C# e genera un foglio di dettaglio
  con SmartMarker. Segui il nostro tutorial dettagliato per una soluzione pronta all'uso.
og_title: Crea oggetto Master Data – Guida completa
tags:
- C#
- SmartMarker
- Excel Automation
title: Crea oggetto Master Data – Guida passo passo per generare il foglio di dettaglio
url: /it/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

Check for any stray formatting: ensure code block placeholders remain on separate lines as originally.

Also ensure we didn't translate any URLs or file paths. We kept them.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea oggetto dati master – Tutorial completo

Hai mai avuto bisogno di **create master data object** per un foglio di lavoro Excel ma non eri sicuro di come collegarlo a un foglio di dettaglio SmartMarker? Non sei solo. In molti scenari di reporting l'oggetto master guida un foglio di dettaglio dinamico, e impostare correttamente il collegamento può sembrare assemblare un puzzle senza immagine.  

In questa guida percorreremo l'intero processo—creare l'oggetto dati master, configurare le opzioni SmartMarker per **generate detail sheet**, e infine avviare il processore. Alla fine avrai uno snippet eseguibile da incollare in qualsiasi progetto .NET che utilizza la libreria GrapeCity Documents for Excel (GcExcel).

## Di cosa avrai bisogno

- .NET 6+ (or .NET Framework 4.7.2) con un riferimento a `GcExcel.dll`
- Familiarità di base con C# (variabili, tipi anonimi, inizializzatori di oggetti)
- Un workbook Excel che contiene già tag SmartMarker come `{{OrderId}}` e una tabella per le righe di dettaglio
- Visual Studio, Rider, o qualsiasi editor tu preferisca

È tutto—nessun pacchetto NuGet aggiuntivo oltre alla distribuzione core di GcExcel.

## Passo 1: Crea l'oggetto dati master

La prima cosa da fare è **create master data object** che rispecchia la struttura attesa dai tag SmartMarker. Pensalo come un piccolo modello di report in memoria.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Perché usare un tipo anonimo qui? Perché ti permette di definire un contenitore leggero senza dichiarare una classe completa—perfetto per demo rapide o quando la forma è poco probabile che cambi. Se in seguito ti serve un modello riutilizzabile, basta sostituire `var` con un POCO appropriato.

> **Consiglio professionale:** Mantieni i nomi delle proprietà (`OrderId`, `Product`, `Quantity`) identici ai segnaposto nel tuo foglio di lavoro; SmartMarker li confronta senza distinzione tra maiuscole e minuscole.

## Passo 2: Configura le opzioni SmartMarker per generare un foglio di dettaglio

Ora diciamo a SmartMarker che vogliamo un foglio di lavoro separato per la tabella delle righe. È qui che entra in gioco la parola chiave **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Il pattern `DetailSheetNewName` utilizza segnaposto tra parentesi graffe che vengono sostituiti a runtime. Nel nostro esempio il foglio sarà chiamato `Order_1`. Se in seguito iteri su più ordini, ognuno otterrà una sua scheda—esattamente ciò che la maggior parte dei contabili si aspetta.

## Passo 3: Esegui il processore SmartMarker

Con i dati e le opzioni pronti, l'ultimo passo è invocare il processore sul foglio di lavoro target.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Dietro le quinte, SmartMarker analizza il foglio di lavoro alla ricerca dei tag, inserisce i valori di `orderData` e, poiché `DetailSheet` è `true`, clona il modello in un nuovo foglio chiamato `Order_1`. Tutte le righe di dettaglio appaiono nell'area di dettaglio, preservando qualsiasi formattazione applicata nel modello.

### Esempio completo funzionante

Di seguito trovi un programma console autonomo che apre un workbook modello (`Template.xlsx`), esegue i tre passaggi e salva il risultato come `Result.xlsx`. Puoi copiare‑incollare questo in un nuovo progetto console e premere **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Output previsto

- **Result.xlsx** contiene un foglio chiamato `Order_1`.
- La cella `A1` (o dove hai posizionato `{{OrderId}}`) ora mostra `1`.
- Una tabella che inizia al blocco SmartMarker elenca due righe:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Se apri il file, vedrai la formattazione del modello preservata—bordature, caratteri, formattazione condizionale—tutto intatto.

## Domande comuni e casi particolari

### E se ho più ordini?

Racchiudi l'oggetto master in una collezione e lascia che SmartMarker itera automaticamente:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Ogni ordine genera il proprio foglio (`Order_1`, `Order_2`, …). Il processore tratta l'array esterno come la collezione master.

### Come controllo la posizione del foglio?

Imposta `smartMarkerOptions.DetailSheetInsertIndex = 2;` per posizionare il nuovo foglio dopo la seconda scheda, oppure usa `DetailSheetInsertAfter = "Summary"` per inserire dopo un foglio con nome.

### Posso disabilitare il foglio di dettaglio per un'esecuzione specifica?

Basta impostare `DetailSheet = false;`. SmartMarker scriverà allora le righe di dettaglio nello stesso foglio dove risiedono i tag master.

### E i grandi set di dati?

SmartMarker trasmette i dati in modo efficiente, ma se superi qualche centinaio di migliaia di righe potresti raggiungere il limite di 1.048.576 righe di Excel. In tal caso dividi i dati in più record master o considera l'esportazione in CSV.

## Panoramica visiva

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*L'illustrazione mostra il flusso dall'oggetto master C# → opzioni SmartMarker → elaborazione del foglio di lavoro → nuovo foglio di dettaglio.*

## Conclusione

Ora sai come **create master data object** in C# e configurare SmartMarker per **generate detail sheet** automaticamente. Il modello a tre passaggi—dati, opzioni, processore—copre la maggior parte degli scenari di automazione Excel con GcExcel.  

Da qui potresti esplorare:

- Aggiungere dati di intestazione/piè di pagina a ciascun foglio di dettaglio
- Utilizzare la formattazione condizionale basata sullo stato dell'ordine
- Esportare il workbook generato in PDF con `workbook.SaveAsPdf(...)`

Sentiti libero di sperimentare, rompere le cose e poi rimetterle insieme. È il modo più veloce per padroneggiare l'automazione dei fogli di lavoro. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}