---
category: general
date: 2026-06-08
description: Come collegare i fogli in Excel usando SmartMarkerProcessor per report
  master‑detail. Popola il foglio master e genera un report Excel master‑detail senza
  sforzo.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: it
og_description: Come collegare i fogli in Excel usando SmartMarkerProcessor. Impara
  a popolare il foglio master e a generare un report master‑detail in pochi minuti.
og_title: Come collegare i fogli in Excel con SmartMarker – Passo dopo passo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Come collegare i fogli in Excel con SmartMarker – Guida passo passo
url: /it/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come collegare i fogli in Excel con SmartMarker – Guida passo‑passo

Ti sei mai chiesto **come collegare i fogli** in Excel senza copiare manualmente le righe o scrivere loop VBA interminabili? Non sei solo. La maggior parte degli sviluppatori si blocca quando ha bisogno di un report master‑detail pulito che rimanga sincronizzato con le modifiche dei dati. La buona notizia? SmartMarkerProcessor fa il lavoro pesante per te, trasformando poche righe di C# in un workbook master‑detail completo.

In questo tutorial percorreremo i passaggi esatti per **popolare il foglio master**, configurare il foglio detail e, infine, **generare il report master‑detail** che si aggiorna automaticamente. Alla fine avrai un modello riutilizzabile da inserire in qualsiasi progetto .NET.

> **Nota preliminare:** Hai bisogno di GrapeCity Documents for Excel (GcExcel) versione 2024 o successiva, un ambiente di sviluppo .NET (Visual Studio 2022 funziona benissimo) e una conoscenza di base di C#. Non sono richiesti pacchetti NuGet aggiuntivi oltre a GcExcel.

---

## Panoramica della soluzione

Prima di immergerci nel codice, analizziamo cosa significa realmente “collegare i fogli” nel contesto di SmartMarker:

1. **Master sheet** – Contiene una riga per entità (ad es., un elenco di clienti).
2. **Detail sheet** – Contiene le righe che appartengono a una riga master (ad es., ordini per ciascun cliente).
3. **SmartMarker syntax** – Un piccolo linguaggio di markup (`{MasterSheet}#master;{DetailSheet}#detail`) che indica al processore come associare le due tabelle di dati.
4. **Processor options** – Abilitare `MasterDetail` fa sì che il motore ripeta automaticamente le righe master e inserisca le righe detail correlate subito sotto.

Comprendere questi elementi ti aiuterà a modificare l'approccio in seguito—magari avrai bisogno di un annidamento a tre livelli o di formattazione condizionale. Tieni presente questo modello mentale mentre procediamo con l'implementazione.

---

## Passo 1: Preparare i dati gerarchici per l'elaborazione Master‑Detail

La prima cosa di cui hai bisogno è una fonte dati che rifletta la relazione master‑detail. Nella maggior parte degli scenari reali proviene da un database, ma per chiarezza useremo un oggetto anonimo.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Perché questo è importante:** SmartMarker non indovina magicamente le relazioni; cerca nomi di proprietà corrispondenti (`MasterId` → `Id`). Strutturando i dati in questo modo forniamo al processore una mappa chiara, che è la pietra angolare di **come collegare i fogli** in modo efficace.

> **Consiglio esperto:** Se i tuoi dati vivono in oggetti `DataTable`, esponili semplicemente come proprietà con gli stessi nomi—SmartMarker funziona con qualsiasi collezione enumerabile.

---

## Passo 2: Creare un workbook e caricare un modello

SmartMarker opera su un workbook Excel esistente, solitamente un modello che contiene già i nomi dei fogli e i segnaposto. Creiamo un workbook in memoria e aggiungiamo due fogli vuoti chiamati *MasterSheet* e *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Puoi anche caricare un file `.xlsx` dal disco (`wb.Open("Template.xlsx")`) se preferisci progettare il layout prima in Excel. La parte importante è che i nomi dei fogli corrispondano a quelli che farai riferimento nella stringa SmartMarker.

---

## Passo 3: Istanziare SmartMarkerProcessor e abilitare la modalità Master‑Detail

Ora introduciamo il motore che leggerà i marker e incollerà i dati. Il `SmartMarkerProcessor` accetta il workbook come argomento del costruttore, e il flag `Options.MasterDetail` gli dice di trattare i marker `#master` e `#detail` come una coppia collegata.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Perché abilitare `MasterDetail`?** Senza questo flag, il processore tratterebbe `{MasterSheet}#master` e `{DetailSheet}#detail` come operazioni indipendenti, perdendo la relazione cruciale tra le righe. Impostare il flag è la singola riga che fa funzionare **come collegare i fogli**.

---

## Passo 4: Definire la stringa SmartMarker ed eseguire il processore

La stringa dei marker indica a SmartMarker quale foglio è il master e quale il detail. La sintassi è semplice: `{SheetName}#master;{SheetName}#detail`. Puoi anche aggiungere marker aggiuntivi (ad es., `#header`) ma non sono necessari per un report di base.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Quando `Process` viene eseguito, il motore:

1. Scrive ogni riga master in *MasterSheet* a partire dalla prima riga vuota dopo l'intestazione.
2. Per ogni riga master, scansiona la collezione `Details`, seleziona le righe dove `MasterId` corrisponde all'`Id` del master e le scrive in *DetailSheet* direttamente sotto la voce master corrispondente.

---

## Passo 5: Salvare o esportare il workbook risultante

A questo punto hai un workbook completamente popolato. Puoi salvarlo su disco, trasmetterlo a un client web o persino convertirlo in PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Apri il file e vedrai due fogli: *MasterSheet* elenca `A` e `B`, mentre *DetailSheet* mostra `Item1` sotto il master `1` e `Item2` sotto il master `2`. Questa è l'essenza di **popolare il foglio master** e **generare il report master‑detail** in un unico passaggio.

---

## Panoramica visiva

![Diagramma che illustra come collegare i fogli in Excel usando SmartMarkerProcessor](https://example.com/diagram.png "Diagramma di collegamento dei fogli")

Il diagramma (il testo alternativo include la parola chiave principale) mostra il flusso dei dati da oggetti C# → SmartMarkerProcessor → fogli Excel collegati.

---

## Gestione dei casi limite comuni

### Più righe detail per master

Se una riga master ha diversi detail correlati, SmartMarker ripete la riga master una sola volta e poi scrive *tutte* le righe detail corrispondenti sotto di essa. Non è necessario alcun codice aggiuntivo—basta assicurarsi che la collezione `Details` contenga ogni riga.

### Dettagli mancanti

Quando una voce master non ha righe detail corrispondenti, il foglio detail semplicemente salta quella sezione. Se ti serve un segnaposto (ad es., “Nessun elemento”), puoi aggiungere una colonna calcolata nel modello che utilizza una formula Excel come `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Grandi dataset

Elaborare decine di migliaia di righe può richiedere molta memoria. Per mantenere le prestazioni fluide:

- Usa `processor.Options.EnableStreaming = true` (disponibile in GcExcel 2025+).
- Suddividi i dati in blocchi e processa ciascun blocco separatamente, poi unisci i workbook.

### Mappatura personalizzata delle colonne

Se i nomi delle tue proprietà non coincidono (`MasterKey` vs `Id`), puoi usare il metodo `SmartMarkerProcessor.Map` per creare un alias prima della elaborazione.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Esempio completo funzionante

Ecco un programma completo, pronto per il copia‑incolla, che puoi eseguire subito.

```csharp
using System;
using GrapeCity.Documents.Excel;

namespace MasterDetailDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare hierarchical data
            var sampleData = new
            {
                Master = new[]
                {
                    new { Id = 1, Name = "A" },
                    new { Id = 2, Name = "B" }
                },
                Details = new[]
                {
                    new { MasterId = 1, Item = "Item1" },
                    new { MasterId = 1, Item = "Item1‑Extra" },
                    new { MasterId = 2, Item = "Item2" }
                }
            };

            // 2️⃣ Create workbook and template sheets
            IWorkbook wb = new Workbook();

            var master = wb.Worksheets.Add("MasterSheet");
            master.Range["A1"].Value


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Formule di collegamento esterno master in Excel usando Aspose.Cells per Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Fogli Excel dinamici master in Java con Aspose.Cells&#58; Guida completa](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Report Excel dinamici master usando Aspose.Cells Java&#58; Intervalli denominati & Formule complesse](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}