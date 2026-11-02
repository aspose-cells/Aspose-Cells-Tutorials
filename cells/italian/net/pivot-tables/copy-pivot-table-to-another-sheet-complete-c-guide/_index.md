---
category: general
date: 2026-06-27
description: Copia la tabella pivot in un altro foglio in C# usando Aspose.Cells.
  Impara passo passo come preservare i dati e la formattazione della tabella pivot.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: it
og_description: Copia la tabella pivot in un altro foglio in C# con Aspose.Cells.
  Questo tutorial mostra esattamente come duplicare una pivot mantenendo intatta la
  sua formattazione.
og_title: Copia tabella pivot in un altro foglio – Guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Copia tabella pivot in un altro foglio – Guida completa C#
url: /it/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia Tabella Pivot in un'Altra Scheda – Guida Completa C#

Hai mai avuto bisogno di **copiare una tabella pivot in un'altra scheda** ma temuto di perdere i slicer, i campi calcolati o la formattazione? Non sei solo. Molti sviluppatori incontrano questo problema quando automatizzano i report Excel, e la frustrazione è reale. In questa guida percorreremo una soluzione pulita, end‑to‑end che **preserva la tabella pivot** esattamente come appare.

Useremo **Aspose.Cells for .NET**, una potente libreria che consente di manipolare i file Excel senza mai aprire Excel stesso. Alla fine di questo tutorial avrai uno snippet C# pronto all'uso che copia una tabella pivot da un foglio di lavoro a un altro, mantenendo intatti tutti i collegamenti ai dati sottostanti.

## Cosa Copre Questo Tutorial

- Configurare un progetto .NET e aggiungere il pacchetto NuGet Aspose.Cells.  
- Caricare una cartella di lavoro esistente che contiene già una tabella pivot.  
- Definire sia l'intervallo di origine (la pivot originale) sia l'intervallo di destinazione su un foglio diverso.  
- Utilizzare `CopyOptions` per **preservare la tabella pivot** durante la copia.  
- Salvare il risultato e verificare che la pivot funzioni nella sua nuova posizione.  

Nessuno strumento esterno, nessun copia‑incolla manuale e nessuna magia nascosta—solo codice diretto che puoi inserire in qualsiasi app console C# o servizio.

> **Perché dovresti interessartene:** L'automazione della duplicazione delle pivot fa risparmiare ore di lavoro manuale, soprattutto nei pipeline di reportistica notturna dove decine di cartelle di lavoro necessitano di strutture pivot identiche su più fogli.

---

## Passo 1: Configura il Progetto e Aggiungi Aspose.Cells

Prima di tutto. Se non l'hai già fatto, crea un nuovo progetto console .NET:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Ora aggiungi il pacchetto Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Consiglio professionale:** Usa l'ultima versione stabile (a partire da giugno 2026 v23.12). Include correzioni di bug per la gestione di `CopyPivotTable`.

## Passo 2: Carica la Cartella di Lavoro e Accedi ai Fogli di Lavoro

Apri la cartella di lavoro che contiene la tabella pivot di origine. Nella maggior parte degli scenari reali il file si trova su un'unità condivisa, ma per questa demo supporremo che sia in una cartella locale chiamata `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Qui creiamo un nuovo foglio chiamato **CopyDestination** dove verrà inserita la pivot. Se hai già un foglio di destinazione, basta recuperarlo per indice o nome.

## Passo 3: Definisci gli Intervalli di Origine e Destinazione

Una tabella pivot vive all'interno di un blocco rettangolare di celle. Devi indicare ad Aspose.Cells quale blocco copiare. In questo esempio la pivot occupa le righe 0‑20 e le colonne 0‑10 (indicizzazione a base zero).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Nota come calcoliamo dinamicamente la riga e la colonna finale. In questo modo, anche se in seguito cambi la dimensione dell'intervallo di origine, la destinazione si adatterà automaticamente.

## Passo 4: Esegui la Copia Mantenendo la Pivot

Ora avviene la magia. Passando un oggetto `CopyOptions` con `CopyPivotTable = true`, Aspose.Cells sa di mantenere intatta la definizione della tabella pivot.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Dietro le quinte, Aspose.Cells ricrea la cache della pivot, aggiorna il riferimento alla fonte dati e riapplica qualsiasi formattazione. Questa è la **duplicazione della pivot di Excel** che stavi cercando.

## Passo 5: Salva e Verifica il Risultato

Infine, scrivi la cartella di lavoro su disco. Puoi mantenere il file originale intatto salvando con un nuovo nome.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Apri il file risultante `copy-pivot.xlsx` e vedrai la tabella pivot perfettamente replicata sul foglio **CopyDestination**, completa di slicer, campi calcolati e formattazione. La fonte dati sottostante punta ancora alla tabella originale, quindi l'aggiornamento funziona esattamente come prima.

> **E se la pivot di origine copre un intervallo dinamico?**  
> Usa `Worksheet.PivotTables[0].CacheDefinition.SourceData` per recuperare i limiti effettivi, quindi costruisci `sourceRange` da quelle informazioni. Questo gestisce i casi in cui righe o colonne possono espandersi nel tempo.

## Bonus: Preserva la Formattazione della Pivot tra le Copie

A volte la copia predefinita perde la formattazione condizionale o i formati numerici personalizzati. Per proteggersi da ciò, estendi il `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Abilitare `CopyFormatting` garantisce che il requisito di **preservare la formattazione della pivot** sia soddisfatto, fornendoti una copia perfetta a livello di pixel.

## Output Atteso

Quando esegui il programma, la console uscirà silenziosamente (a meno che non aggiungi log). Aprendo `copy-pivot.xlsx` dovresti vedere:

- Foglio 1: Dati originali e tabella pivot invariati.  
- **CopyDestination**: Una replica esatta della pivot, posizionata a partire dalla riga 31 (poiché le righe sono basate su 1 nell'interfaccia di Excel).  
- Tutti i slicer e i filtri funzionanti; cliccando “Refresh” aggiorna entrambe le pivot simultaneamente.

---

## Conclusione

Abbiamo appena dimostrato come **copiare una tabella pivot in un'altra scheda** usando Aspose.Cells in C#. I passaggi—configurare il progetto, caricare la cartella di lavoro, definire gli intervalli, copiare con `CopyPivotTable = true` e salvare—formano un modello affidabile che puoi riutilizzare in qualsiasi pipeline di automazione.

Se vuoi andare oltre, considera:

- **Duplicazione della pivot di Excel** su più cartelle di lavoro (ciclo attraverso i file).  
- Utilizzare l'opzione **Aspose.Cells copy range with pivot** per spostare le pivot tra diverse cartelle di lavoro.  
- Automatizzare gli aggiornamenti con `PivotTable.RefreshData()` dopo la copia.

Sentiti libero di sperimentare con diversi intervalli di origine, o combinare questa tecnica con la generazione di grafici per dashboard di reportistica completamente automatizzate. Hai domande? Lascia un commento, e buona programmazione!

![Screenshot che mostra la tabella pivot copiata in un nuovo foglio](copy-pivot-screenshot.png "esempio di copia della tabella pivot in un'altra scheda")

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Modificare i Dati di Origine della Tabella Pivot Usando Aspose.Cells per .NET | Guida all'Analisi dei Dati](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Padroneggiare la Formattazione delle Tabelle Pivot in .NET Usando Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Accedere alle Fonti Dati Esterne delle Tabelle Pivot in .NET usando Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}