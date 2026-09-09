---
category: general
date: 2026-02-21
description: Ripeti i dati in Excel rapidamente usando SmartMarker—scopri come popolare
  il modello Excel e ripetere le righe senza sforzo.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: it
og_description: Ripeti i dati in Excel usando SmartMarker. Scopri come popolare un
  modello Excel, ripetere le righe e automatizzare i tuoi fogli di calcolo.
og_title: Ripeti i dati in Excel – Popola il modello con SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Ripeti i dati in Excel – Popola il modello con SmartMarker
url: /it/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ripetere dati in excel – Popolare il modello con SmartMarker

Ti è mai capitato di dover **ripetere dati in Excel** ma non sapevi come evitare il copia‑incolla manuale? Non sei il solo. In molti scenari di reporting hai un elenco di elementi che deve espandersi automaticamente in righe, e farlo a mano è una ricetta per errori.

Ecco la questione—usare lo SmartMarkerProcessor della libreria **GemBox.Spreadsheet** ti consente di **popolare un modello Excel** con una singola riga di C# e di far ripetere le righe per ogni elemento della tua collezione. In questa guida percorreremo i passaggi esatti, ti mostreremo il codice completo e spiegheremo perché ogni parte è importante, così potrai ripetere le righe in Excel con fiducia e senza sforzo.

## Cosa imparerai

* Come definire la struttura dati che guida l'operazione di ripetizione.  
* Come collegare uno `SmartMarkerProcessor` a una cartella di lavoro che contiene un foglio modello nascosto.  
* Come il marcatore `${Repeat:Item}` si espande automaticamente in più righe.  
* Suggerimenti per gestire casi limite come collezioni vuote o formattazioni personalizzate.  

Alla fine di questo tutorial sarai in grado di **popolare excel dai dati** in modo scalabile, facile da mantenere e funzionante con qualsiasi progetto .NET.

---

## Prerequisiti

* .NET 6.0 o successivo (il codice utilizza le funzionalità moderne di C#).  
* Il pacchetto NuGet **GemBox.Spreadsheet** (la versione gratuita funziona fino a 150 righe).  
* Un file modello Excel di base (`Template.xlsx`) con un foglio nascosto chiamato `HiddenTemplate`.  
* Familiarità con gli oggetti C# e LINQ è utile ma non obbligatoria.

---

## Passo 1 – Definire la struttura dati per la ripetizione

Prima di tutto, ti serve una fonte dati che il motore SmartMarker possa iterare. Nella maggior parte delle applicazioni reali questo proviene da un database, un'API o un file CSV. Per semplicità useremo un tipo anonimo con una singola proprietà chiamata `Item` che contiene un array di stringhe.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Perché è importante:** Il marcatore `${Repeat:Item}` all'interno del modello Excel cerca una proprietà chiamata `Item`. Se rinomini la proprietà, aggiorna di conseguenza il marcatore. Questo stretto accoppiamento garantisce che il modello rimanga sincronizzato con il tuo codice, rendendo più semplice **popolare il modello excel** senza indovinare i nomi delle colonne.

### Varianti comuni

* **Oggetti complessi:** Invece di un semplice array di stringhe puoi fornire una lista di oggetti (`new[] { new { Name = "A", Qty = 10 } }`). Il marcatore ripeterà le righe e potrai fare riferimento a `${Item.Name}` e `${Item.Qty}` nel foglio.  
* **Collezioni vuote:** Se `Item` è vuoto, SmartMarker rimuove semplicemente il blocco di ripetizione, lasciando il modello intatto—ideale per sezioni opzionali.

---

## Passo 2 – Creare lo SmartMarkerProcessor per il foglio modello nascosto

Successivamente, carica la tua cartella di lavoro e istanzia uno `SmartMarkerProcessor`. Puntalo sulla cartella di lavoro che contiene il foglio modello nascosto; SmartMarker copierà quel foglio in uno visibile ed espanderà i marcatori di ripetizione.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Consiglio professionale:** Se hai più modelli nello stesso file, puoi specificare il nome del foglio sorgente quando chiami `processor.Process`. Questo è utile quando devi **ripetere righe in excel** per diverse sezioni di un report.

### Gestione dei casi limite

* **Foglio modello mancante:** Avvolgi il caricamento in un try/catch e registra un errore chiaro—questo previene fallimenti silenziosi quando il percorso del file è errato.  
* **Grandi set di dati:** Per migliaia di righe, considera lo streaming dell'output su un file (`processor.Save`) invece di tenere tutto in memoria.

---

## Passo 3 – Applicare i dati ed espandere il marcatore `${Repeat:Item}`

Ora arriva la riga magica che effettivamente ripete le righe. Passa l'oggetto creato nel Passo 1 a `processor.Process`. SmartMarker individuerà ogni marcatore `${Repeat:Item}`, duplicherà la riga per ogni elemento e sostituirà i segnaposto con i valori reali.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Cosa dovresti vedere

Quando apri `Result.xlsx`, il foglio modello nascosto è stato copiato in un nuovo foglio visibile (per impostazione predefinita chiamato `Sheet1`). La riga che conteneva `${Repeat:Item}` ora appare tre volte, con le celle che mostrano rispettivamente **A**, **B** e **C**.

| Item |
|------|
| A    |
| B    |
| C    |

Se aggiungi altre colonne come `${Item.Price}`, queste verranno riempite automaticamente dalla fonte dati.

---

## Come ripetere righe in Excel senza SmartMarker (confronto rapido)

| Approccio               | Complessità del codice | Manutenzione | Prestazioni |
|-------------------------|------------------------|--------------|-------------|
| Copia‑incolla manuale   | Alta                   | Bassa        | Scarsa      |
| Macro VBA               | Media                  | Media        | Buona       |
| **SmartMarkerProcessor**| Bassa                  | Alta         | Eccellente  |

Come puoi vedere, usare SmartMarker per **ripetere dati in excel** ti offre la separazione più pulita tra la progettazione del modello e la logica di business. È anche indipendente dal linguaggio—concetti simili esistono nelle librerie Java, Python e JavaScript.

---

## Suggerimenti avanzati & errori comuni

### 1. Formattare le righe ripetute

SmartMarker copia l'intera riga—including stili di cella, bordi e formattazione condizionale. Se ti serve uno stile diverso per la prima o l'ultima riga, aggiungi marcatori extra come `${If:Item.IsFirst}` e usa formule condizionali all'interno di Excel.

### 2. Gestire grandi set di dati

Quando lavori con più di 10 000 righe, disabilita il calcolo automatico di Excel prima dell'elaborazione:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Riabilitalo dopo il salvataggio per mantenere le prestazioni rapide.

### 3. Popolare Excel dai dati di un database reale

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Quindi usa `${Repeat:Order}` nel modello per elencare ogni ordine. Questo schema dimostra quanto sia semplice **popolare excel dai dati** direttamente da Entity Framework.

### 4. Usare più blocchi di ripetizione

Puoi avere diversi marcatori `${Repeat:...}` nello stesso foglio o in fogli diversi. SmartMarker li elabora in sequenza, quindi l'ordine è importante solo se un blocco dipende dall'output di un altro.

---

## Esempio completo eseguibile

Di seguito trovi un'applicazione console autonoma che puoi incollare in Visual Studio ed eseguire immediatamente. Dimostra tutti e tre i passaggi più il salvataggio del file.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Output previsto:** `Result.xlsx` contiene un foglio in cui la riga con `${Repeat:Item}` appare tre volte, mostrando A, B e C. Nessun aggiustamento manuale necessario.

---

## Conclusione

Ora sai come **ripetere dati in excel** in modo efficiente sfruttando lo SmartMarkerProcessor. Definendo un semplice oggetto dati, caricando un modello di cartella di lavoro e chiamando `Process`, puoi **popolare il modello excel**, **ripetere righe in excel**, e in generale **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}