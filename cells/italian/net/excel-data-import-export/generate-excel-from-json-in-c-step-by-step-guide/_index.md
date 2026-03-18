---
category: general
date: 2026-03-18
description: Impara a generare Excel da JSON con C#, consentire nomi di fogli duplicati,
  creare un foglio di dettaglio e salvare la cartella di lavoro in C# in pochi minuti.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: it
og_description: Genera Excel da JSON usando C#. Questa guida mostra come consentire
  nomi di fogli duplicati, creare un foglio di dettaglio e salvare la cartella di
  lavoro in C# con Aspose.Cells.
og_title: Genera Excel da JSON in C# – Tutorial completo
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Genera Excel da JSON in C# – Guida passo‑passo
url: /it/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generare Excel da JSON in C# – Guida passo‑passo

Ti è mai capitato di **generare Excel da JSON** ma non eri sicuro quale libreria potesse gestire il lavoro pesante? Non sei l'unico. In molte applicazioni aziendali riceviamo payload come JSON e dobbiamo trasferire quei dati in fogli di calcolo ben formattati—pensa a report di vendite, dump di inventario o log di audit. La buona notizia? Con il motore SmartMarker di Aspose.Cells puoi trasformare una stringa JSON in un file Excel completo in poche righe.

In questo tutorial percorreremo l'intero processo: dalla preparazione del payload JSON, alla configurazione di SmartMarker per **consentire nomi di foglio duplicati**, alla creazione di un **foglio di dettaglio**, e infine al **salvataggio del workbook in stile C#**. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto .NET.

> **Riepilogo veloce:**  
> • Obiettivo principale – generare Excel da JSON.  
> • Obiettivi secondari – consentire nomi di foglio duplicati, creare foglio di dettaglio, salvare workbook C#.  

## Prerequisiti

- .NET 6.0 SDK (o qualsiasi versione recente di .NET).  
- Visual Studio 2022 o VS Code con l'estensione C#.  
- Una licenza attiva o una prova gratuita di **Aspose.Cells for .NET** (il pacchetto NuGet è `Aspose.Cells`).  
- Un file Excel modello (`template.xlsx`) che contiene già tag SmartMarker come `&=Name` e un segnaposto per la tabella di dettaglio.

Se qualcuno di questi ti è sconosciuto, non farti prendere dal panico—l'installazione del pacchetto NuGet è un unico comando, e il modello può essere una semplice cartella di lavoro con alcune celle segnaposto.

## Panoramica della soluzione

Ad alto livello faremo:

1. Definire una stringa JSON che rispecchi i dati che vogliamo nel foglio.  
2. Configurare `SmartMarkerOptions` in modo che i nomi di foglio duplicati siano consentiti e che un **foglio di dettaglio** ottenga un nome prevedibile.  
3. Caricare il modello Excel che contiene i tag SmartMarker.  
4. Eseguire il processore SmartMarker per unire i dati JSON nel workbook.  
5. Salvare il file finale con `workbook.Save(...)`.

Ogni passaggio è spiegato di seguito, con snippet di codice completi e il motivo per cui il passaggio è importante.

---

## Passo 1 – Preparare il payload JSON da unire

La prima cosa di cui hai bisogno è un documento JSON che corrisponda ai tag SmartMarker presenti nel tuo modello. Considera il JSON come la fonte di verità; ogni chiave diventa un segnaposto nel file Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Perché è importante:**  
SmartMarker legge la gerarchia JSON ed espande automaticamente le tabelle per collezioni come `Orders`. Se la struttura del tuo JSON non corrisponde ai tag, la fusione produrrà silenziosamente righe vuote—un errore comune.

## Passo 2 – Configurare SmartMarker per consentire nomi di foglio duplicati e nominare il foglio di dettaglio

Per impostazione predefinita Aspose.Cells vieta i nomi di foglio duplicati, il che può essere un ostacolo quando generi un foglio di dettaglio per ogni record master. La classe `SmartMarkerOptions` ti consente di allentare questa regola e anche di specificare un modello di denominazione per i fogli di dettaglio appena creati.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Perché è importante:**  
Se stai iterando su più clienti e ogni iterazione crea un nuovo foglio, il motore normalmente lancia un'eccezione. Impostare `AllowDuplicateSheetNames` a `true` indica ad Aspose.Cells di aggiungere automaticamente un suffisso numerico, mantenendo il processo fluido.

## Passo 3 – Caricare il modello Excel che contiene i tag SmartMarker

Il tuo modello è la tela su cui SmartMarker dipingerà i dati. Può contenere qualsiasi formattazione—colori, formule, grafici—così non devi ricreare quella logica programmaticamente.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Suggerimento:**  
Mantieni il modello in una cartella che faccia parte dell'output del tuo progetto (ad esempio, `Content\Templates`). In questo modo puoi fare riferimento ad esso con un percorso relativo ed evitare di codificare percorsi assoluti.

## Passo 4 – Eseguire il processore SmartMarker con il JSON e le opzioni

Ora avviene la magia. Il `SmartMarkerProcessor` legge il JSON, rispetta le opzioni impostate e riempie il workbook di conseguenza.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Cosa succede dietro le quinte?**  
- Il processore scansiona ogni cella alla ricerca di marker come `&=Name` o `&=Orders.Item`.  
- Sostituisce i marker semplici con valori scalari (`Name`, `Date`).  
- Per le collezioni (`Orders`), crea un nuovo foglio di dettaglio (denominato “Detail”) e popola una riga di tabella per ogni elemento.  
- Poiché abbiamo consentito nomi di foglio duplicati, se il modello aveva già un foglio chiamato “Detail”, il motore creerà “Detail (2)”.

## Passo 5 – Salvare il workbook unito su disco

Infine, scrivi il workbook popolato su un file. Puoi scegliere qualsiasi formato supportato da Aspose.Cells—XLSX, CSV, PDF, ecc. Qui useremo il moderno XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Perché è importante:**  
Il salvataggio è il punto in cui effettivamente **salvi il workbook in stile C#**. Se devi inviare il file in streaming a un client web, puoi usare `workbook.Save(Stream, SaveFormat.Xlsx)` invece.

## Esempio completo funzionante

Mettiamo tutto insieme, ecco un'app console completa, pronta da eseguire. Assicurati di aver installato il pacchetto NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) prima di compilare.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Risultato atteso

- **Foglio 1** (il foglio master) mostrerà “John” nella cella `Name` e “2023‑01‑01” nella cella `Date`.  
- Apparirà un nuovo foglio **Detail**, contenente una tabella con due righe: una per l'ordine Laptop e una per l'ordine Mouse.  
- Se il modello aveva già un foglio chiamato “Detail”, il nuovo foglio sarà denominato “Detail (2)”, grazie al flag `AllowDuplicateSheetNames`.

![Output Excel che mostra il foglio master con nome e data, più un foglio Detail con le righe degli ordini](excel-output.png "generare excel da json risultato")

*Testo alternativo dell'immagine:* **generate excel from json – esempio di cartella di lavoro con fogli master e detail**

## Domande comuni e casi limite

### E se il mio JSON contiene collezioni nidificate?

SmartMarker può gestire array nidificati, ma dovrai aggiungere fogli di dettaglio aggiuntivi o usare marker gerarchici. Ad esempio, `&=Orders.SubItems.Product` genererebbe automaticamente un foglio di terzo livello.

### Come personalizzare il modello di denominazione per fogli duplicati?

Invece di un `DetailSheetNewName` statico, puoi assegnare una callback tramite `smartMarkerOptions.DetailSheetNameGenerator`. Questo ti permette di inserire timestamp o ID unici nel nome del foglio.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Posso generare CSV invece di XLSX?

Assolutamente. Sostituisci la chiamata finale a `Save` con:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Il resto della pipeline rimane identico.

### Funziona in ASP.NET Core?

Sì. Lo stesso codice può essere eseguito all'interno di un'azione di controller. Basta inviare lo stream del workbook nella risposta:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

## Consigli professionali e insidie

- **Consiglio pro:** Mantieni i tag SmartMarker in un foglio “Template” separato. In questo modo puoi proteggere il foglio da modifiche accidentali pur consentendo al processore di leggerlo.  
- **Attenzione a:** chiavi JSON che contengono spazi o caratteri speciali. Aspose.Cells si aspetta identificatori JavaScript validi; rinominale o usa l'attributo `JsonProperty` se stai deserializzando da un POCO.  
- **Suggerimento di performance:** Se stai elaborando migliaia di righe, imposta `smartMarkerOptions.EnableCache = true` per riutilizzare i marker compilati.  
- **Controllo versione:** Il codice sopra mira a Aspose.Cells 23.9+. Le versioni precedenti potrebbero non supportare `AllowDuplicateSheetNames`.

## Conclusione

Ora hai una ricetta completa, end‑to‑end, per **generare Excel da JSON** in C#. Configurando `SmartMarkerOptions` abbiamo dimostrato come **consentire nomi di foglio duplicati**, controllare la denominazione del **foglio di dettaglio**, e infine **salvare il workbook in stile C#**. L'approccio è completamente autonomo—nessun servizio esterno, solo un singolo pacchetto NuGet.

Prossimi passi? Prova a sostituire la sorgente JSON con una API reale

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}