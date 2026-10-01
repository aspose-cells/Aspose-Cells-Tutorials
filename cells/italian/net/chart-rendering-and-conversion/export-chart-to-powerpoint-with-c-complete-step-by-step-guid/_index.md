---
category: general
date: 2026-02-26
description: Esporta grafico in PowerPoint da Excel usando C#. Scopri come convertire
  Excel in PowerPoint, salvare Excel come PowerPoint e mantenere le forme modificabili.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: it
og_description: Esporta il grafico in PowerPoint da Excel usando C#. Questa guida
  mostra come convertire Excel in PowerPoint, salvare la cartella di lavoro come PPTX
  e mantenere le forme modificabili.
og_title: Esporta il grafico in PowerPoint con C# – Tutorial completo di programmazione
tags:
- Aspose.Cells
- C#
- Office Automation
title: Esporta il grafico in PowerPoint con C# – Guida completa passo passo
url: /it/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta grafico in PowerPoint – Tutorial di programmazione completo

Ti sei mai chiesto come **esportare un grafico in PowerPoint** senza perdere la possibilità di modificarlo? In molti scenari di reporting è necessario avere un grafico live all'interno di una presentazione, ma copiare e incollare manualmente è un vero fastidio. La buona notizia è che è possibile farlo programmaticamente con poche righe di C#.

In questa guida percorreremo l’intero processo: dal caricamento di una cartella di lavoro Excel che contiene un grafico con una casella di testo, alla configurazione dell’esportazione in modo che caselle di testo e forme rimangano editabili, fino al salvataggio del risultato come file **PowerPoint**. Alla fine saprai anche come **convertire Excel in PowerPoint**, **salvare Excel come PowerPoint**, e potrai persino regolare le opzioni per scenari particolari.

## Cosa ti serve

- **Aspose.Cells for .NET** (versione 23.10 o successiva). È la libreria che rende la conversione indolore.
- Runtime **.NET 6+** – qualsiasi SDK recente va bene.
- Un semplice file Excel (`ChartWithTextbox.xlsx`) che contenga almeno un grafico e una casella di testo.
- Visual Studio o il tuo IDE preferito.

Non sono necessari altri pacchetti NuGet oltre a Aspose.Cells, ma una conoscenza di base della sintassi C# è sicuramente utile.

## Esporta grafico in PowerPoint – Passo‑passo

Di seguito suddividiamo la soluzione in passaggi discreti e facili da seguire. Ogni passaggio include il codice esatto di cui hai bisogno, più un breve paragrafo “perché” che spiega la logica sottostante.

### Passo 1: Carica la cartella di lavoro Excel che contiene il grafico

Per prima cosa dobbiamo portare il file sorgente in memoria. Usare `Workbook` di Aspose.Cells legge l’intero foglio di calcolo, inclusi grafici, immagini e oggetti incorporati.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Perché è importante:* Se la cartella di lavoro viene aperta senza specificare correttamente il percorso, otterrai una `FileNotFoundException`. Un rapido controllo di validità evita di esportare una diapositiva vuota in seguito.

### Passo 2: Prepara le opzioni di presentazione per mantenere le forme editabili

Aspose.Cells ti permette di decidere se caselle di testo, forme e persino il grafico stesso rimangano **editabili** dopo l’esportazione. Impostare `ExportTextBoxes` e `ExportShapes` a `true` conserva quegli oggetti come elementi nativi di PowerPoint anziché appiattirli in un’immagine statica.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Perché è importante:* Se lasci queste impostazioni ai valori predefiniti (`false`), la diapositiva risultante conterrà una bitmap del grafico, rendendo impossibile modificare le serie o cambiare la didascalia in seguito. Abilitare entrambe le opzioni ti fornisce un vero grafico PowerPoint che si comporta esattamente come quello che disegneresti manualmente.

### Passo 3: Converti Excel in PowerPoint e salva il file

Ora invochiamo il metodo `Save`, passando l’enum `SaveFormat.Pptx` e le opzioni appena configurate. La libreria si occupa di tradurre l’oggetto grafico di Excel in una forma grafico di PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Perché è importante:* La chiamata `Save` esegue tutto il lavoro pesante—mappare le serie di Excel su quelle di PowerPoint, preservare la formattazione degli assi e copiare eventuali caselle di testo collegate. Dopo l’esecuzione di questa riga avrai un file `.pptx` completamente editabile pronto per essere aperto in Microsoft PowerPoint.

### Verifica del risultato

Apri `Result.pptx` in PowerPoint. Dovresti vedere una diapositiva che contiene:

- Il grafico originale, ancora collegato ai suoi dati (puoi fare doppio‑click per modificare le serie).
- Qualsiasi casella di testo presente nel foglio Excel, ora una casella di testo nativa di PowerPoint.
- Il layout della diapositiva è scelto automaticamente (di solito una diapositiva vuota).

Se noti elementi mancanti, ricontrolla che la cartella di lavoro sorgente avesse effettivamente oggetti visibili e che `ExportTextBoxes` / `ExportShapes` fossero impostati a `true`.

### Converti Excel in PowerPoint: gestire più fogli di lavoro

Spesso una cartella di lavoro contiene più di un foglio, ognuno con il proprio grafico. Per impostazione predefinita Aspose.Cells esporta **tutti** i grafici da **tutti** i fogli in diapositive separate. Se ti serve solo un sottoinsieme, puoi filtrarli prima del salvataggio:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Consiglio esperto:* Impostare `chart.IsVisible = false` è più leggero che rimuovere completamente il grafico, e ti permette di attivare o disattivare l’inclusione senza modificare il file sorgente.

### Salva Excel come PowerPoint – Personalizzare le dimensioni della diapositiva

PowerPoint utilizza per impostazione predefinita una diapositiva di 10 pollici per 5,63 pollici. Se il tuo grafico appare troppo compresso, puoi modificare le dimensioni della diapositiva tramite l’oggetto `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Ora il grafico esportato avrà più spazio di respiro e le caselle di testo manterranno il layout originale.

### Come convertire Excel in PPT: gestire oggetti nascosti

Righe, colonne o forme nascoste possono talvolta infiltrarsi nell’esportazione. Per rimuoverle, esegui una rapida pulizia prima del salvataggio:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Questo passaggio non è sempre necessario, ma previene spazi inattesi nella tua presentazione finale.

### Salva cartella di lavoro come PPTX – Esempio completo funzionante

Mettendo tutto insieme, ecco un programma console pronto all’uso che dimostra l’intero flusso:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Eseguendo questo programma verrà creato `Result.pptx` con un grafico e una casella di testo editabili, esattamente quello che ti aspetteresti quando **salvi una cartella di lavoro come pptx** manualmente.

![Esempio di esportazione di grafico in PowerPoint](/images/export-chart-to-powerpoint.png "Esporta grafico in PowerPoint – diapositiva editabile")

## Domande frequenti e casi limite

**E se il file Excel contiene un grafico con una fonte dati esterna collegata?**  
Aspose.Cells copia i valori *correnti* dei dati nel grafico PowerPoint. Non preserva il collegamento esterno, perché PowerPoint non può riferirsi a una connessione dati Excel nello stesso modo. Se ti servono aggiornamenti in tempo reale, considera l’inserimento del file Excel originale nella PPTX come oggetto OLE.

**Posso esportare un grafico che utilizza un tema personalizzato?**  
Sì. La libreria tenta di mappare i colori del tema di Excel negli slot del tema di PowerPoint. Per palette molto personalizzate potresti dover regolare i colori dopo l’esportazione usando l’API di PowerPoint (ad esempio Aspose.Slides).

**Esiste un limite al numero di grafici?**  
Praticamente nessuno—Aspose.Cells trasmette i dati in streaming, quindi anche una cartella di lavoro con decine di grafici verrà esportata, sebbene la dimensione del PPTX risultante cresca linearmente.

**È necessaria una licenza per Aspose.Cells?**  
Una valutazione gratuita funziona, ma aggiunge una filigrana sulla prima diapositiva. Per uso in produzione, ottieni una licenza adeguata per rimuovere la filigrana e sbloccare le prestazioni complete.

## Riepilogo

Abbiamo visto come **esportare un grafico in PowerPoint** usando C#, dimostrato il codice esatto per caricare una cartella di lavoro Excel, configurare `PresentationOptions` per mantenere caselle di testo e forme editabili, e infine salvare il risultato come `.pptx`. Hai anche imparato a **convertire Excel in PowerPoint**, **salvare Excel come PowerPoint**, e a rispondere alla domanda “**come convertire Excel in ppt**” con un esempio completo e funzionante.

## Cosa fare dopo?

- **Salva cartella di lavoro come PPTX** con più diapositive: itera su ogni foglio di lavoro e chiama `Save` con `PresentationOptions` per ciascuno.
- Esplora **Aspose.Slides** se devi modificare programmaticamente il PPTX generato (aggiungere transizioni, note del relatore, ecc.).
- Prova a esportare **grafici pivot** o **grafici 3‑D**—le stesse opzioni si applicano, ma potresti dover regolare la formattazione degli assi in seguito.

Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione ufficiale di Aspose.Cells per le ultime modifiche API. Buona programmazione e divertiti a trasformare quei grafici Excel in presentazioni PowerPoint lucide con poche righe di C#! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}