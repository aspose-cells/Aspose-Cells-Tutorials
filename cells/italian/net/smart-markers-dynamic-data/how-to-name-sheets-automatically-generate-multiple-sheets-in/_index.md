---
category: general
date: 2026-02-09
description: Come denominare i fogli in C# con SmartMarker – impara a generare più
  fogli e automatizzare la denominazione dei fogli con poche righe di codice.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: it
og_description: Come nominare i fogli in C# usando le opzioni SmartMarker. Questa
  guida mostra come generare più fogli e automatizzare la denominazione dei fogli
  senza sforzo.
og_title: Come denominare automaticamente i fogli – Guida rapida C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Come denominare i fogli automaticamente – Genera più fogli in C#
url: /it/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Nominare i Fogli Automaticamente – Generare più Fogli in C#

Ti sei mai chiesto **come nominare i fogli** in una cartella di lavoro Excel senza dover cliccare manualmente su “Rinomina” ogni volta? Non sei l’unico. In molti scenari di reporting ti ritrovi con decine di fogli di dettaglio che necessitano di nomi sistematici, e farlo a mano è un incubo.  

La buona notizia è che, con poche righe di C#, puoi **generare più fogli** e **automatizzare la denominazione dei fogli** in modo che ogni nuovo foglio di dettaglio segua uno schema prevedibile. In questo tutorial percorreremo la soluzione completa, spiegheremo perché ogni parte è importante e ti forniremo un esempio di codice pronto all'uso.

## Cosa Copre Questa Guida

* Configurare una cartella di lavoro che contiene SmartMarkers.  
* Configurare `SmartMarkerOptions` per controllare il nome base dei fogli generati.  
* Eseguire `ProcessSmartMarkers` affinché la libreria crei `Detail`, `Detail_1`, `Detail_2`, … automaticamente.  
* Suggerimenti per gestire casi limite come nomi di fogli esistenti o convenzioni di denominazione personalizzate.  
* Un esempio completo, eseguibile, che puoi incollare in Visual Studio e vedere il risultato immediatamente.

Non è richiesta alcuna esperienza pregressa con Aspose.Cells—basta una configurazione base di C# e un IDE a tua scelta.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6.0 o successivo | Funzionalità linguistiche moderne e compatibilità con la libreria |
| Aspose.Cells per .NET (pacchetto NuGet) | Fornisce l'elaborazione di `SmartMarker` e la creazione dei fogli |
| Un progetto console vuoto (o qualsiasi app .NET) | Ci dà un luogo dove eseguire il codice |

Installa la libreria con:

```bash
dotnet add package Aspose.Cells
```

Ora che abbiamo le basi coperte, immergiamoci nell'implementazione reale.

## Passo 1: Creare una Cartella di Lavoro con SmartMarkers

Per prima cosa ci serve una cartella di lavoro che contenga un segnaposto SmartMarker. Pensa a uno SmartMarker come a un tag di modello che indica al motore dove inserire i dati e, nel nostro caso, quando creare un nuovo foglio.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Consiglio:** Mantieni il foglio modello leggero. Solo le righe che necessitano di duplicazione dovrebbero contenere SmartMarkers; tutto il resto rimane statico.

## Passo 2: Configurare le Opzioni di SmartMarker – Il Cuore della Denominazione dei Fogli

Ora arriva la magia. Impostando `DetailSheetNewName` diciamo al motore quale nome base usare per ogni foglio generato. La libreria aggiungerà “_1”, “_2”, ecc., ogni volta che il nome base esiste già.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Se mai avessi bisogno di una convenzione diversa (ad es., “Report_2023”), basta cambiare la stringa. Il motore gestisce le collisioni automaticamente, ed è per questo che questo approccio **automatizza la denominazione dei fogli** senza codice aggiuntivo.

## Passo 3: Elaborare gli SmartMarkers e Generare i Fogli

Con la cartella di lavoro, i dati e le opzioni pronti, una singola chiamata al metodo fa il lavoro pesante.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Risultato Atteso

Quando apri *GeneratedSheets.xlsx* vedrai:

| Nome Foglio | Contenuto |
|------------|-----------|
| Template   | Il layout originale del marcatore (conservato per riferimento) |
| Detail     | Primo set di righe (Apple, Banana, Cherry) |
| Detail_1   | Seconda copia – dati identici (utile quando hai più collezioni) |
| Detail_2   | …e così via, a seconda di quante gruppi di SmartMarker distinti hai |

Lo schema di denominazione (`Detail`, `Detail_1`, `Detail_2`) dimostra **come nominare i fogli** programmaticamente e **generare più fogli** secondo necessità.

## Casi Limite & Varianti

### 1. Nomi di Fogli Esistenti

Se la tua cartella di lavoro contiene già un foglio chiamato “Detail”, il motore inizierà con “Detail_1”. Questo evita sovrascritture accidentali.

### 2. Formati di Incremento Personalizzati

Vuoi “Detail‑A”, “Detail‑B” invece dei suffissi numerici? Puoi post‑elaborare i nomi dopo `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Molteplici Gruppi di SmartMarker

Se la tua cartella di lavoro contiene più di un gruppo di SmartMarker (ad es., `{{invoice}}` e `{{detail}}`), ogni gruppo genererà il proprio set di fogli basato sullo stesso `DetailSheetNewName`. Per dare a ciascun gruppo un prefisso distinto, crea istanze separate di `SmartMarkerOptions` e chiama `ProcessSmartMarkers` per ogni collezione.

## Consigli Pratici dal Campo

* **Consiglio:** Disattiva `AllowDuplicateNames` in `WorkbookSettings` se vuoi che la libreria lanci un’eccezione invece di rinominare silenziosamente i fogli. Questo aiuta a individuare bug nella logica di denominazione in anticipo.  
* **Attenzione a:** Nomi base molto lunghi. Excel limita i nomi dei fogli a 31 caratteri; la libreria tronca automaticamente, ma potresti ritrovarti con nomi ambigui.  
* **Nota sulle prestazioni:** Generare centinaia di fogli può consumare memoria. Dispone della cartella di lavoro (`wb.Dispose()`) non appena hai finito, soprattutto se l’app è in esecuzione in un servizio a lunga durata.

## Panoramica Visiva

![Diagramma su come nominare i fogli](image.png "Diagramma che mostra il flusso dal modello SmartMarker ai fogli generati – come nominare i fogli")

*Il testo alternativo include la parola chiave principale per soddisfare la SEO.*

## Codice Sorgente Completo (Pronto per Copia‑Incolla)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Esegui il programma, apri il file generato e vedrai i fogli denominati automaticamente secondo lo schema che abbiamo definito.

## Conclusione

Ora sai **come nominare i fogli** in una cartella di lavoro C#, **come generare più fogli** con SmartMarker e **come automatizzare la denominazione dei fogli** così da non dover più rinominare nulla manualmente. L'approccio scala da poche pagine di dettaglio a centinaia, e lo stesso schema funziona per qualsiasi collezione che passi a `ProcessSmartMarkers`.

Cosa fare dopo? Prova a sostituire la fonte dati con una query al database, sperimenta formati di suffisso personalizzati, o collega più gruppi di SmartMarker per un motore di reporting completo. Il cielo è il limite quando lasci che la libreria gestisca il lavoro ripetitivo di denominazione.

Se questa guida ti è stata utile, metti una stella su GitHub, condividila con i colleghi o lascia un commento qui sotto con i tuoi trucchi di denominazione. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}