---
category: general
date: 2026-02-14
description: Crea una cartella di lavoro Excel utilizzando Aspose.Cells e impara come
  elaborare JSON, convertire JSON in Excel e caricare JSON in Excel in pochi semplici
  passaggi.
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: it
og_description: Crea una cartella di lavoro Excel con Aspose.Cells, impara a elaborare
  JSON, converti JSON in Excel e carica JSON in Excel rapidamente e in modo affidabile.
og_title: Crea una cartella di lavoro Excel da JSON – Tutorial passo passo di Aspose.Cells
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Crea cartella di lavoro Excel da JSON – Guida completa ad Aspose.Cells
url: /it/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare una cartella di lavoro Excel da JSON – Guida completa ad Aspose.Cells

Hai mai dovuto **creare una cartella di lavoro Excel** a partire da un frammento di JSON ma non sapevi da dove cominciare? Non sei il solo. Molti sviluppatori si trovano nella stessa situazione quando hanno un payload JSON e hanno bisogno di un foglio di calcolo ordinato per report o scambio dati.  

La buona notizia? Con **Aspose.Cells** puoi trasformare quel JSON in un file Excel completo in poche righe di codice. In questo tutorial vedremo **come elaborare JSON**, **convertire JSON in Excel** e **caricare JSON in Excel** usando il potente `SmartMarkerProcessor`. Alla fine avrai una cartella di lavoro pronta da salvare e una chiara panoramica delle opzioni che puoi regolare.

## Cosa imparerai

- Come configurare un progetto Aspose.Cells per la gestione di JSON.  
- Il codice esatto necessario per **creare una cartella di lavoro Excel** da un array JSON.  
- Perché l'opzione `ArrayAsSingle` è importante e quando potresti volerla modificare.  
- Suggerimenti per gestire strutture JSON più grandi, gestione degli errori e salvataggio del file.  

> **Prerequisiti:** .NET 6+ (o .NET Framework 4.6+), pacchetto NuGet Aspose.Cells per .NET e una conoscenza di base di C#. Non sono necessarie altre librerie.

---

## Passo 1: Installa Aspose.Cells e aggiungi lo spazio dei nomi richiesto

Prima che qualsiasi codice venga eseguito, devi avere la libreria Aspose.Cells referenziata nel tuo progetto.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **Consiglio professionale:** Se usi Visual Studio, l'interfaccia di NuGet Package Manager fa lo stesso lavoro—basta cercare *Aspose.Cells* e cliccare su Installa.

---

## Passo 2: Prepara i dati JSON da convertire

Il `SmartMarkerProcessor` funziona con qualsiasi stringa JSON, ma devi decidere come la libreria deve interpretare gli array. In questo esempio tratteremo un semplice array numerico come **un singolo record**, utile quando ti serve solo un elenco piatto di valori.

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **Perché è importante:** Per impostazione predefinita, Aspose.Cells tratta ogni elemento dell'array come un record separato. Impostare `ArrayAsSingle = true` comprime l'intero array in un unico record, che corrisponde a molti scenari di reporting.

---

## Passo 3: Crea una nuova istanza di Workbook

Ora **creiamo la cartella di lavoro Excel** in memoria. Nessun file viene ancora scritto; stiamo solo preparando il contenitore.

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

A questo punto `workbook.Worksheets[0]` è un foglio vuoto chiamato *Sheet1*. Puoi rinominarlo in seguito se lo desideri.

---

## Passo 4: Configura le opzioni SmartMarker per l'elaborazione JSON

La classe `SmartMarkerOptions` ti offre un controllo granulare su come il JSON viene interpretato. Il flag chiave per il nostro scenario è `ArrayAsSingle`.

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **Quando cambiarlo:** Se il tuo JSON rappresenta una collezione di righe (ad esempio, un array di oggetti), lascia `ArrayAsSingle` impostato su `false`. Ogni oggetto diventerà automaticamente una nuova riga.

---

## Passo 5: Esegui l'elaborazione Smart Marker sul foglio di lavoro

Con la cartella di lavoro e le opzioni pronte, forniamo il JSON al processore. Il processore analizza il foglio alla ricerca di smart marker (segnaposto) e li sostituisce con i dati del JSON. Poiché non abbiamo marker espliciti, il processore crea semplicemente un layout predefinito.

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

Se vuoi controllare la cella esatta in cui i dati iniziano, puoi aggiungere un marker come `"${Array}"` nella cella **A1** prima di eseguire il processore. Per questo tutorial ci affidiamo al comportamento predefinito, che scrive i valori dell'array in celle consecutive a partire da **A1**.

---

## Passo 6: Salva la cartella di lavoro su disco (o su stream)

L'ultimo passo è persistere la cartella di lavoro. Puoi salvarla su file, su un memory stream o anche restituirla direttamente da una web API.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Eseguendo il programma completo si ottiene un file Excel con i numeri **1**, **2** e **3** posizionati rispettivamente nelle celle **A1**, **A2** e **A3**.

---

## Esempio completo funzionante

Di seguito trovi l'applicazione console completa, pronta per l'esecuzione, che unisce tutti i passaggi. Copia‑incolla il codice in un nuovo progetto console C# e premi **F5**.

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Output previsto in Excel**

| Numbers |
|---------|
| 1       |
| 2       |
| 3       |

La riga di intestazione (“Numbers”) è opzionale ma dimostra come puoi mescolare modifiche manuali delle celle con l'elaborazione tramite smart‑marker.

---

## Domande frequenti e casi particolari

### E se il mio JSON è un oggetto, non un array?

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

Puoi comunque usare `SmartMarkerProcessor`. Inserisci marker come `${Name}`, `${Age}`, `${Country}` nel foglio, poi chiama `StartSmartMarkerProcessing`. Il processore sostituirà ogni marker con il valore corrispondente.

### Come gestisco file JSON di grandi dimensioni (megabyte)?

- **Stream del JSON**: invece di caricare l'intera stringa, leggi il file con un `StreamReader` e passa il testo a `StartSmartMarkerProcessing`.  
- **Aumenta il limite di memoria**: imposta `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` se incontri `OutOfMemoryException`.  
- **Elaborazione a blocchi**: suddividi il JSON in array più piccoli e processa ogni blocco su un nuovo foglio.

### Posso esportare in CSV invece di XLSX?

Assolutamente. Dopo l'elaborazione, chiama semplicemente:

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

La disposizione dei dati rimane la stessa; cambia solo il formato del file.

### Come formatto le celle (font, colori) dopo aver caricato il JSON?

Puoi applicare la formattazione dopo il passaggio dello smart‑marker:

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

Poiché il processore viene eseguito per primo, qualsiasi formattazione applicata successivamente non verrà sovrascritta.

---

## Suggerimenti e buone pratiche

- **Imposta sempre `ArrayAsSingle` in modo consapevole** – dimenticare questo flag è una causa comune di duplicazione inattesa delle righe.  
- **Valida il JSON prima dell'elaborazione** – una stringa malformata genera `JsonParseException`. Avvolgi la chiamata in un blocco `try/catch` per una gestione degli errori più elegante.  
- **Usa smart marker nominati** (`${Orders}`) per migliorare la leggibilità, soprattutto quando lavori con oggetti JSON nidificati.  
- **Mantieni la cartella di lavoro in memoria** se la restituisci da una web API; inviare un `MemoryStream` evita I/O su disco non necessario.  
- **Compatibilità di versione**: il codice sopra funziona con Aspose.Cells 23.12 e versioni successive. Controlla le note di rilascio se utilizzi una versione più vecchia.

---

## Conclusione

Ti abbiamo appena mostrato come **creare una cartella di lavoro Excel** da JSON usando Aspose.Cells, coprendo tutto, dall'installazione della libreria al salvataggio del file finale. Padroneggiando `SmartMarkerProcessor` e le sue opzioni, puoi **caricare JSON in Excel**, **convertire JSON in Excel** e persino personalizzare l'output per scenari di reporting complessi.  

Pronto per il passo successivo? Prova a fornire un array JSON nidificato di oggetti, aggiungi formattazione condizionale o esporta il risultato come PDF—tutto con la stessa API di Aspose.Cells. I tuoi pipeline dati‑a‑Excel sono ora a pochi linee di codice di distanza.

Se hai domande o incontri difficoltà, lascia un commento qui sotto. Buona programmazione e divertiti a trasformare JSON in splendide cartelle di calcolo! 

![Crea una cartella di lavoro Excel con dati JSON](/images/create-excel-workbook-json.png "Illustrazione di un array JSON trasformato in un foglio Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}