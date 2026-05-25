---
category: general
date: 2026-02-23
description: Come creare una cartella di lavoro usando Aspose.Cells e aggiungere marcatori
  con un array JSON. Scopri come aggiungere marcatori, utilizzare un array JSON e
  i marcatori intelligenti di Aspose.Cells in pochi minuti.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: it
og_description: Come creare una cartella di lavoro usando Aspose.Cells, aggiungere
  marcatori e utilizzare un array JSON. Questa guida passo passo ti mostra tutto ciò
  di cui hai bisogno.
og_title: Come creare una cartella di lavoro con Smart Markers – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Come creare una cartella di lavoro con Smart Markers – Guida Aspose.Cells
url: /it/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare una cartella di lavoro con Smart Markers – Guida Aspose.Cells

Ti sei mai chiesto **come creare una cartella di lavoro** che riempia automaticamente i dati da una sorgente JSON? Non sei l'unico—gli sviluppatori chiedono continuamente come aggiungere marker che estraggono valori da array, soprattutto quando lavorano con Aspose.Cells. La buona notizia? È piuttosto semplice una volta compreso il concetto di smart‑marker. In questo tutorial vedremo come creare una cartella di lavoro, aggiungere marker, utilizzare un array JSON e configurare gli smart markers in Aspose.Cells così da generare file Excel al volo.

Copriamo tutto ciò che devi sapere: inizializzare la cartella di lavoro, costruire una `MarkerCollection`, fornire un array JSON, attivare l’opzione “ArrayAsSingle” e, infine, applicare i marker. Alla fine avrai un programma C# completamente funzionante che produce un file Excel con i valori **A**, **B** e **C** popolati automaticamente. Nessun servizio esterno, solo pura magia di Aspose.Cells.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+)
- Pacchetto NuGet Aspose.Cells per .NET (`Install-Package Aspose.Cells`)
- Una conoscenza di base della sintassi C# (se sei alle prime armi, gli snippet sono ampiamente commentati)
- Visual Studio o qualsiasi IDE tu preferisca

Se hai già tutto questo, ottimo—tuffiamoci.

## Passo 1: Come creare una cartella di lavoro (Inizializzare il file Excel)

La prima cosa di cui hai bisogno è un oggetto workbook vuoto. Pensalo come una tela bianca che Aspose.Cells dipingerà successivamente con i dati.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Perché è importante:** `Workbook` è il punto di ingresso per ogni operazione su Excel. Senza di esso non puoi collegare gli smart markers né salvare il file. Creare prima il workbook garantisce anche un ambiente pulito per i passaggi successivi.

## Passo 2: Come aggiungere i marker – Inizializzare una collezione di marker

Gli smart markers vivono all’interno di una `MarkerCollection`. Questa collezione è dove definisci i segnaposto (i marker) e i dati che li sostituiranno.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Consiglio:** Puoi riutilizzare la stessa `MarkerCollection` per più fogli di lavoro, ma mantenerne una per foglio rende il debug più semplice.

## Passo 3: Utilizzare un array JSON – Aggiungere un marker con dati JSON

Ora aggiungiamo effettivamente un marker. Il segnaposto `{SmartMarker}` verrà sostituito dall’array JSON che forniamo. Il JSON deve essere una stringa di array, ad esempio `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Spiegazione:** Il metodo `Add` accetta due argomenti: il testo del marker e la sorgente dati. Qui la sorgente dati è un array JSON, che Aspose.Cells può analizzare automaticamente. Questo è il fulcro dell'**uso di array JSON** con gli smart markers.

## Passo 4: Configurare il marker – Trattare l'array come un valore singolo

Per impostazione predefinita, Aspose.Cells espande un array JSON in righe separate. Se vuoi che l’intero array sia trattato come un unico valore di cella (utile per elenchi a discesa o stringhe concatenate), imposta il flag `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Quando usarlo:** Se desideri che l’array compaia in una sola cella (es. `"A,B,C"`), abilita questo flag. Altrimenti, Aspose.Cells scriverà ogni elemento nella sua riga.

## Passo 5: Collegare i marker al foglio di lavoro e applicarli

Infine, associa la collezione di marker al foglio di lavoro e indica ad Aspose.Cells di sostituire i segnaposto con i dati reali.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Risultato:** Dopo aver eseguito il programma, `SmartMarkerResult.xlsx` contiene il valore **A** (o l’intero array se `ArrayAsSingle` è true) nella cella `A1`. Apri il file per verificare.

### Output previsto

| A |
|---|
| A |   *(se `ArrayAsSingle` è false, il primo elemento riempie la cella)*

Se imposti `ArrayAsSingle = true`, la cella `A1` conterrà la stringa `["A","B","C"]`.

## Passo 6: Come aggiungere i marker – Scenari avanzati (Opzionale)

Ti starai chiedendo, *e se avessi bisogno di più di un marker?* La risposta è semplice: chiama nuovamente `Add`.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Perché funziona:** Ogni marker opera in modo indipendente, così puoi mescolare “array come singolo” ed “espansione in righe” nello stesso foglio. Questa flessibilità è un tratto distintivo degli **smart markers Aspose.Cells**.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Il marker non viene sostituito | Testo segnaposto mancante o errore di battitura | Assicurati che la cella contenga esattamente la stringa del marker (`{SmartMarker}`) |
| JSON non analizzato | Sintassi JSON non valida (virgolette mancanti) | Usa un validatore JSON o doppio escape delle virgolette nelle stringhe C# |
| L'array si espande in modo inatteso | `ArrayAsSingle` lasciato al valore predefinito `false` | Imposta `["ArrayAsSingle"] = true` per il marker specifico |
| Workbook salvato vuoto | `Apply()` non chiamato prima di `Save()` | Chiama sempre `worksheet.SmartMarkers.Apply()` prima di salvare |

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo che puoi inserire in una console app. Non sono necessari file aggiuntivi.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Esegui il programma, apri `SmartMarkerResult.xlsx` e vedrai l’array JSON (o il suo primo elemento) posizionato ordinatamente nella cella **A1**.

## Passi successivi: estendere la soluzione

Ora che sai **come creare una cartella di lavoro**, **come aggiungere i marker** e **come usare un array JSON** con Aspose.Cells, considera queste idee di approfondimento:

1. **Più fogli di lavoro** – Scorri una lista di fogli e collega collezioni di marker diverse a ciascuno.
2. **JSON dinamico** – Recupera JSON da un’API web (`HttpClient`) e passalo direttamente a `smartMarkerCollection.Add`.
3. **Formattare l’output** – Dopo aver applicato i marker, formatta le celle (font, colori) per rendere il report più curato.
4. **Formati di esportazione** – Salva la cartella di lavoro come PDF, CSV o HTML modificando `workbook.Save("file.pdf")`.

Ognuno di questi argomenti coinvolge naturalmente **smart markers Aspose.Cells**, così potrai ampliare gli stessi concetti di base appena appresi.

## Conclusione

Abbiamo percorso **come creare una cartella di lavoro** da zero, **come aggiungere i marker** e **come usare un array JSON** con gli smart markers di Aspose.Cells. L’esempio completo, eseguibile, dimostra l’intero flusso, dall’inizializzazione del `Workbook` al salvataggio del file finale. Attivando il flag `ArrayAsSingle` ottieni un controllo preciso su come i dati JSON appaiono in Excel, rendendo la soluzione adattabile a molteplici scenari di reporting.

Prova il codice, modifica il JSON e sperimenta con marker aggiuntivi. Quando padroneggerai questi blocchi fondamentali, generare report Excel sofisticati sarà un gioco da ragazzi. Hai domande o vuoi condividere un caso d’uso interessante? Lascia un commento qui sotto—buona programmazione!

![Diagramma che mostra come creare una cartella di lavoro con smart markers in Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "come creare una cartella di lavoro con smart markers Aspose.Cells")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}