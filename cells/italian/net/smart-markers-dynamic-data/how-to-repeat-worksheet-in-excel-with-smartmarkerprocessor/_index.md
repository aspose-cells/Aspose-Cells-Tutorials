---
category: general
date: 2026-11-19
description: Come duplicare un foglio di lavoro durante il popolamento di Excel con
  dati di un array. Impara a generare più fogli di lavoro e a popolare un foglio da
  un elenco in pochi passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: it
lastmod: 2026-11-19
og_description: Come ripetere un foglio di lavoro usando SmartMarkerProcessor. Segui
  questa guida per popolare Excel con dati di array, generare più fogli di lavoro
  e popolare un foglio di lavoro da un elenco.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Come ripetere un foglio di lavoro in Excel – guida passo passo
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Come ripetere il foglio di lavoro in Excel con SmartMarkerProcessor
url: /it/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come ripetere un foglio di lavoro in Excel con SmartMarkerProcessor

Se hai bisogno di **how to repeat worksheet** durante la generazione di report Excel, questa guida ti mostra una soluzione completa e eseguibile. Alla fine del tutorial sarai in grado di **populate Excel with array** dati, **generate multiple worksheets**, e **populate worksheet from list** usando la libreria SmartMarkerProcessor.

Ripetere un foglio di lavoro è una necessità comune quando ogni dipartimento, regione o periodo di tempo necessita della propria scheda. L'esempio seguente dimostra i passaggi esatti, spiega perché ogni impostazione è importante e copre casi limite come liste vuote o denominazioni personalizzate.

## Prerequisiti

- .NET 6.0 o versioni successive installato
- Un riferimento al pacchetto NuGet **GroupDocs.Viewer** (o equivalente) che contiene `SmartMarkerProcessor`
- Un modello di cartella di lavoro Excel (`.xlsx`) con un marcatore come `${repeat:Dept}` posizionato in una riga che desideri ripetere
- Familiarità di base con C# e LINQ (opzionale ma utile)

Non sono richieste librerie di terze parti aggiuntive.

## Passo 1: Creare l'istanza di SmartMarkerProcessor

Il processore orchestra la sostituzione dei marcatori e la duplicazione dei fogli di lavoro. Istanziare senza argomenti utilizza le opzioni predefinite.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Creare il processore in anticipo ti consente di configurare le opzioni globali prima che vengano applicati i dati. Questa è la base per **how to repeat worksheet** correttamente.

## Passo 2: Abilitare la ripetizione del foglio di lavoro

Per impostazione predefinita il processore sostituisce i marcatori solo nel foglio corrente. Impostare `RepeatWorksheet` su `true` indica al motore di clonare l'intero foglio per ogni elemento nella raccolta di dati.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Abilitare questa opzione è la chiave per **generate multiple worksheets** — il processore creerà una nuova scheda per ogni elemento nell'array `Dept` e manterrà la formattazione originale.

## Passo 3: Preparare la fonte dati come array o lista

SmartMarkerProcessor funziona con qualsiasi enumerable, ma usare un array rende l'intento chiaro quando vuoi **populate worksheet from list**. Qui creiamo un oggetto anonimo che contiene una proprietà `Dept` che contiene un array di stringhe.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Se hai già una `List<string>` puoi passarla direttamente; il processore la tratterà allo stesso modo. La parte importante è che il nome della proprietà (`Dept`) corrisponda al marcatore `${repeat:Dept}` nel modello.

## Passo 4: Caricare il foglio di lavoro modello

Supponendo di avere un `ExcelPackage` (da EPPlus) o un oggetto `Workbook`, recupera il foglio di lavoro che desideri ripetere. La variabile `ws` rappresenta quel foglio.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Se preferisci una libreria diversa (ad es., ClosedXML), lo stesso principio si applica: ottieni un oggetto foglio di lavoro che implementa l'interfaccia richiesta.

## Passo 5: Elaborare il foglio di lavoro con i dati

Ora applica i dati al modello. Il processore clona il foglio per ogni dipartimento, sostituisce il marcatore `${repeat:Dept}` con il nome reale del dipartimento e lascia il resto del foglio intatto.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Dopo il completamento di `Process`, `ws` diventa il primo di diversi fogli di lavoro — uno per dipartimento. Il nome del foglio originale viene preservato, mentre i duplicati ricevono suffissi incrementali (ad es., “Sheet1 (1)”, “Sheet1 (2)”). Puoi rinominarli in seguito se hai bisogno di uno schema di denominazione personalizzato.

### Output previsto

Quando apri la cartella di lavoro risultante, dovresti vedere:

- **Sheet1** – il modello originale (spesso lasciato vuoto o usato come master)
- **Sheet1 (1)** – popolato con “HR”
- **Sheet1 (2)** – popolato con “IT”
- **Sheet1 (3)** – popolato con “Finance”

Ogni foglio contiene lo stesso layout ma con il nome del dipartimento sostituito dove compariva `${repeat:Dept}`.

## Gestione dei casi limite

### Array vuoti o null

Se `Dept` è null o vuoto, il processore non creerà fogli aggiuntivi. Per evitare una cartella di lavoro completamente vuota, puoi aggiungere una guardia:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Nomi di foglio di lavoro personalizzati

Lo schema di denominazione predefinito potrebbe non adattarsi a tutti i requisiti di reporting. Dopo l'elaborazione, rinomina ogni foglio usando un ciclo:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Popolamento di colonne aggiuntive

Se hai bisogno di **populate excel with array** valori oltre un singolo marcatore, estendi l'oggetto dati:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Quindi regola i marcatori del modello a `${repeat:Dept.Name}` e `${repeat:Dept.Headcount}`. Il processore ripeterà la riga per ogni dipartimento e riempirà entrambe le colonne.

## Esempio completo funzionante

Di seguito è un'applicazione console autonoma che dimostra l'intero flusso dal caricamento del modello al salvataggio della cartella di lavoro finale.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Spiegazione delle sezioni chiave**

- **Processor creation** – stabilisce il motore che interpreterà i marcatori.
- **RepeatWorksheet option** – attiva la funzionalità principale che risponde a *how to repeat worksheet*.
- **Data source** – utilizza un array (`new[]`) per soddisfare **populate excel with array**.
- **Template loading** – dimostra un modo comune per ottenere un oggetto foglio di lavoro.
- **Processing** – esegue la duplicazione e l'inserimento dei dati in una sola chiamata.
- **Renaming** – mostra come trasformare i nomi generici “(1)”, “(2)” in titoli significativi, un requisito tipico dopo **generate multiple worksheets**.

Eseguendo questo programma si genera `Result.xlsx` con tre schede specifiche per dipartimento, ciascuna popolata dall'array.

## Problemi comuni e consigli professionali

- **Marker spelling** – il marcatore deve corrispondere esattamente al nome della proprietà (`${repeat:Dept}`). Un errore di battitura impedisce la ripetizione.
- **Worksheet index** – dopo l'elaborazione, il foglio originale rimane all'indice 0; i fogli generati seguono sequenzialmente. Un indice errato può portare a rinominare la scheda sbagliata.
- **Large data sets** – generare centinaia di fogli può aumentare drasticamente la dimensione del file. Considera di suddividere i report o usare un unico foglio con sezioni raggruppate se le prestazioni diventano un problema.
- **Thread safety** – `SmartMarkerProcessor` non è thread‑safe. Crea un'istanza separata per thread se elabori più cartelle di lavoro in parallelo.

## Conclusione

Ora sai **how to repeat worksheet** in Excel usando SmartMarkerProcessor, come **populate excel with array** dati, come **generate multiple worksheets**, e come **populate worksheet from list** in modo efficiente. L'esempio completo collega tutti i concetti, e il passaggio opzionale di rinominare ti consente di produrre nomi di schede puliti e facili da usare.

Successivamente, potresti esplorare:

- Utilizzare **populate worksheet from list** con oggetti complessi (collezioni annidate)
- Applicare la formattazione condizionale dopo la duplicazione del foglio di lavoro
- Esportare la cartella di lavoro generata in PDF o CSV per il consumo a valle

Sentiti libero di adattare il codice ai tuoi scenari di reporting e goditi l'automazione delle cartelle di lavoro Excel con fiducia!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come ripetere i fogli di lavoro – Guida completa per l'automazione di Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Crea foglio di lavoro per elemento – Come ripetere il foglio di lavoro in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Come espandere un array in Excel e popolare un modello](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}