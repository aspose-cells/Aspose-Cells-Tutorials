---
category: general
date: 2026-03-25
description: Crea una cartella di lavoro Excel da JSON e salvala come file xlsx. Scopri
  come esportare JSON in xlsx, generare Excel da JSON e popolare Excel da JSON in
  pochi minuti.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: it
og_description: Crea una cartella di lavoro Excel da JSON istantaneamente. Questa
  guida mostra come esportare JSON in XLSX, generare Excel da JSON e popolare Excel
  da JSON con Aspose.Cells.
og_title: Crea cartella di lavoro Excel da JSON – Tutorial completo C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Crea cartella di lavoro Excel da JSON – Guida passo‑a‑passo
url: /it/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una cartella di lavoro Excel da JSON – Tutorial completo C#

Hai mai avuto bisogno di **creare una cartella di lavoro Excel** da un payload JSON ma non sapevi da dove cominciare? Non sei solo; molti sviluppatori si trovano di fronte a questo ostacolo quando cercano di trasformare i dati di un'API in un foglio di calcolo ordinato. La buona notizia? Con poche righe di C# e Aspose.Cells puoi **esportare json in xlsx**, **generare excel da json**, e **popolare excel da json** senza dover gestire convertitori di terze parti.

In questa guida percorreremo l’intero processo—partendo da una stringa JSON grezza, inserendola in uno SmartMarker, e infine **salvare la cartella di lavoro come xlsx** su disco. Alla fine avrai un file Excel pronto all’uso che appare così:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Suggerimento:** Se stai già usando Aspose.Cells altrove nel tuo progetto, puoi riutilizzare la stessa istanza `Workbook` per più importazioni JSON—ottimo per l’elaborazione batch.

---

## Di cosa avrai bisogno

- **.NET 6+** (o qualsiasi versione recente del .NET Framework che supporti C# 10)
- **Aspose.Cells for .NET** – installa via NuGet: `dotnet add package Aspose.Cells`
- Una conoscenza di base della sintassi C# (non è necessario conoscere a fondo Excel)

Tutto qui. Nessun servizio esterno, nessun interop COM, solo codice gestito puro.

---

## Passo 1: Inizializza una nuova cartella di lavoro Excel

La prima cosa che facciamo è creare un nuovo oggetto workbook. Pensalo come l’apertura di un file Excel vuoto dove inseriremo i dati in seguito.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Perché partire con un nuovo workbook? Garantisce una tela pulita, evita stili residui da esecuzioni precedenti e mantiene le dimensioni del file minime—perfetto per pipeline automatizzate.

---

## Passo 2: Prepara i dati JSON da importare

Per dimostrazione useremo un piccolo array JSON, ma puoi sostituirlo con qualsiasi JSON valido che ricevi da un servizio web, da un file o da una query al database.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Nota le virgolette doppie escape (`\"`)—è solo la sintassi dei literal string in C#. In uno scenario reale probabilmente leggeresti questo da un file:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Passo 3: Indica a SmartMarker di trattare l’intero array come un unico record

Il motore SmartMarker di Aspose.Cells può iterare automaticamente sulle collezioni. Abilitando **ArrayAsSingle**, trattiamo l’intero array JSON come un unico record, esattamente ciò che ci serve per una tabella piatta.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Se dimentichi questo flag, SmartMarker proverà a creare un foglio separato per ogni elemento—definitivamente non quello che vuoi quando generi una semplice tabella.

---

## Passo 4: Inserisci un token SmartMarker nel foglio di lavoro

I token SmartMarker hanno la forma `${jsonArray}`. Quando il processore viene eseguito, sostituisce il token con i dati della sorgente JSON. Metteremo il token nella cella **A1** così l’output inizierà dall’angolo in alto a sinistra.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Puoi anche pre‑formattare la riga di intestazione prima della elaborazione. Per esempio, imposta il carattere grassetto sulla prima riga:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Passo 5: Esegui il processore SmartMarker

Ora avviene la magia. Il processore legge il JSON, mappa ogni proprietà a una colonna e scrive le righe sotto il token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Dietro le quinte, Aspose.Cells:

1. Analizza il JSON in un oggetto .NET.
2. Abbina i nomi delle proprietà (`Name`, `Score`) alle intestazioni di colonna.
3. Scrive ogni elemento dell’array come una nuova riga.

Se il tuo JSON contiene oggetti nidificati, puoi riferirti a loro con la notazione a punti (`${parent.child}`) – una funzionalità comoda per report più complessi.

---

## Passo 6: Salva la cartella di lavoro come file XLSX

Infine, persisti il workbook su disco. L’estensione `.xlsx` indica a Excel (e alla maggior parte delle altre applicazioni di fogli di calcolo) che si tratta di un workbook OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Puoi, naturalmente, streammare il workbook direttamente in una risposta HTTP se stai costruendo un’API web:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per l’esecuzione, che incorpora tutti i passaggi descritti sopra. Copialo in un nuovo progetto console e premi **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Risultato atteso:** Aprendo `json-single.xlsx` vedrai due righe sotto l’intestazione in grassetto—`John` con un punteggio di `90` e `Anna` con `85`. I nomi delle colonne vengono inferiti automaticamente dai nomi delle proprietà JSON.

---

## Domande frequenti & casi particolari

### E se le chiavi del mio JSON contengono spazi o caratteri speciali?

SmartMarker si aspetta nomi identificatori validi. Sostituisci gli spazi con underscore o usa una mappatura personalizzata:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Come esportare un grande array JSON (migliaia di righe)?

Il processore streamma i dati internamente, quindi l’uso della memoria rimane contenuto. Tuttavia, potresti voler:

- Incrementare il limite `MaxRows` del foglio (`worksheet.Cells.MaxRow = 1_048_576;` – il massimo di Excel).
- Disattivare le linee della griglia per migliorare le prestazioni (`worksheet.IsGridlinesVisible = false;`).

### Posso aggiungere più tabelle JSON nella stessa cartella di lavoro?

Certo. Basta posizionare token SmartMarker diversi in intervalli separati (ad es., `${orders}` in `A10`, `${customers}` in `D1`) e chiamare `Process` una volta per token o una volta con un oggetto JSON composito che contiene entrambi gli array.

---

## Bonus: Aggiungere un grafico semplice (opzionale)

Se vuoi visualizzare i punteggi, aggiungi rapidamente un grafico a colonne dopo che i dati sono stati popolati:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

Il grafico farà riferimento automaticamente alle righe appena aggiunte, fornendoti un report rifinito in un solo passaggio.

---

## Conclusione

Ora sai **come creare una cartella di lavoro Excel** da una stringa JSON, **esportare json in xlsx**, **generare excel da json**, e **popolare excel da json** usando la funzionalità SmartMarker di Aspose.Cells. La soluzione completa—inizializzare un workbook, configurare SmartMarker, processare il JSON e salvare il file—si riduce a poche righe di codice, ma scala a set di dati molto grandi.

Quali sono i prossimi passi? Prova a sostituire il JSON statico con una chiamata API, aggiungi formattazione condizionale basata sui punteggi, o genera più fogli per diversi domini di dati. Lo stesso schema funziona per CSV, XML o anche set di risultati di database—basta cambiare la stringa di origine e adeguare il token SmartMarker.

Buona programmazione, e che i tuoi fogli di calcolo siano sempre ordinati!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}