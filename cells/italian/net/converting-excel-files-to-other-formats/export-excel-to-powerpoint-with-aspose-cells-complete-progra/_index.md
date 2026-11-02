---
category: general
date: 2026-08-14
description: Esporta Excel in PowerPoint usando Aspose.Cells e scopri come calcolare
  le formule di Excel nel codice. Esempio C# passo‑passo con codice sorgente completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: it
lastmod: 2026-08-14
og_description: Esporta Excel in PowerPoint con Aspose.Cells e calcola le formule
  di Excel nel codice. Segui questa guida completa per generare file PPTX modificabili
  dai workbook.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Esporta Excel in PowerPoint con Aspose.Cells – tutorial completo C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Esporta Excel in PowerPoint con Aspose.Cells – guida completa di programmazione
url: /it/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Excel in PowerPoint con Aspose.Cells – guida completa di programmazione

Se hai bisogno di **esportare Excel in PowerPoint** in modo programmatico, questa guida ti mostra esattamente come farlo con Aspose.Cells per .NET. Imparerai anche come **calcolare le formule di Excel nel codice**, copiare le tabelle pivot senza perdere le definizioni e utilizzare la nuova funzione Office‑365 EXPAND per gli array dinamici.

Nelle sezioni seguenti esamineremo un esempio reale in C#, spiegheremo perché ogni riga è importante e tratteremo le insidie più comuni in modo da poter adattare la soluzione ai tuoi progetti.

## Cosa copre questo tutorial

* Caricamento di una cartella di lavoro esistente (`input.xlsx`)  
* Copia di un intervallo che contiene una tabella pivot mantenendo la sua definizione  
* Esportazione della cartella di lavoro in un file PowerPoint (`.pptx`) con caselle di testo e forme modificabili  
* Esportazione di un intervallo di celle come stringhe utilizzando una logica personalizzata  
* Calcolo delle formule di Excel nel codice, inclusa la funzione Office‑365 EXPAND  
* Salvataggio della cartella di lavoro finale con tutte le modifiche applicate  

**Prerequisiti**  
* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7.2+)  
* Aspose.Cells per .NET v25.11 o versioni più recenti (l'opzione `CopyPivotTable` è stata introdotta nella v25.11)  
* Una conoscenza di base di C# e dei concetti di Excel come intervalli, tabelle pivot e formule  

> **Consiglio professionale:** Installa Aspose.Cells tramite NuGet (`Install-Package Aspose.Cells`) per mantenere il tuo progetto aggiornato con le ultime funzionalità.

## Esporta Excel in PowerPoint con Aspose.Cells

Il primo compito principale è convertire la cartella di lavoro in una presentazione PowerPoint mantenendo tutti gli elementi visivi modificabili. Questo è fondamentale quando si desidera generare automaticamente deck di diapositive da report finanziari o dashboard.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Perché funziona

* **`Workbook`** carica l'intero file Excel in memoria, fornendoti pieno accesso all'API.  
* **`CopyRange`** con `CopyPivotTable = true` garantisce che la fonte dati, la cache e il layout della tabella pivot vengano duplicati esattamente—cosa che le versioni precedenti di Aspose.Cells non potevano fare.  
* Aggiungere un nuovo foglio di lavoro (`Copy`) ti consente di mantenere intatto il foglio originale, utile per le tracce di audit.

## Esporta la cartella di lavoro in PowerPoint con oggetti modificabili

Ora trasformiamo la cartella di lavoro in un file PowerPoint. Abilitando `ExportEditableObjects`, ogni grafico, forma o casella di testo diventa un oggetto PowerPoint nativo che gli utenti possono modificare direttamente dopo l'esportazione.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Spiegazione

* **`WorkbookDesigner`** è un helper di alto livello che prepara la cartella di lavoro per l'esportazione, gestendo Smart Markers, intervalli nominati e aggiustamenti di layout.  
* Impostare `ExportEditableObjects = true` indica ad Aspose.Cells di tradurre i disegni di Excel in forme PowerPoint anziché appiattirli in immagini. Questo produce un deck di diapositive **completamente modificabile**.

> **Caso limite:** se la tua cartella di lavoro contiene grafici complessi basati su connessioni dati esterne, assicurati che tali connessioni siano risolte prima di chiamare `ExportToPptx`, altrimenti il grafico potrebbe apparire vuoto.

## Esporta un intervallo come stringhe usando una logica personalizzata

A volte hai bisogno di valori stringa grezzi per l'elaborazione a valle (ad esempio, alimentare un parser CSV). La classe `ExportTableOptions` ti consente di controllare come viene convertita ogni cella.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Perché potresti usarlo

* **Tipo di dato uniforme:** Esportare come stringhe evita errori di incompatibilità di tipo quando il consumatore si aspetta testo.  
* **Formattazione personalizzata:** Sostituisci `value.ToString()` con qualsiasi formattatore personalizzato (ad esempio, `value.ToString("yyyy-MM-dd")` per le date).

## Calcola le formule di Excel nel codice

Una esigenza frequente è **calcolare le formule di Excel nel codice** senza aprire Excel. Aspose.Cells fornisce un motore di calcolo integrato che funziona offline e supporta le ultime funzioni di Office‑365, inclusa `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Come funziona il motore di calcolo

* La proprietà `Formula` memorizza l'espressione esattamente come la digiteresti in Excel.  
* `CalculateFormula()` avvia una ricalcolazione completa della cartella di lavoro, rispettando le dipendenze tra le celle.  
* La funzione `EXPAND` (disponibile in Excel 365) restituisce un intervallo di spill basato sulla cella sorgente (`B1`) e sul numero di righe (`5`) e colonne (`3`) specificate.  

> **Suggerimento:** se devi calcolare solo una parte della cartella di lavoro, usa `Worksheet.CalculateFormula()` per limitare l'ambito e migliorare le prestazioni.

## Salva la cartella di lavoro con tutte le modifiche applicate

Infine, scrivi la cartella di lavoro modificata su disco. Puoi salvare in uno dei formati supportati (`.xlsx`, `.xls`, `.csv`, ecc.) modificando l'estensione del file.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Cosa verificare

* Apri `result.xlsx` in Excel per confermare la copia della tabella pivot, il risultato della formula `EXPAND` e eventuali stringhe esportate personalizzate.  
* Apri `output.pptx` in PowerPoint; dovresti vedere una diapositiva che rispecchia il layout di Excel e tutti i grafici/caselle di testo dovrebbero essere modificabili.

## Domande comuni e risoluzione dei problemi

| Question | Answer |
|----------|--------|
| **Ho bisogno di una licenza per usare Aspose.Cells?** | Sì. Una versione di prova è valida per la valutazione, ma una licenza completa rimuove le filigrane di valutazione e sblocca la funzionalità `CopyPivotTable`. |
| **Cosa succede se il PPTX esportato mostra forme vuote?** | Verifica che gli oggetti di disegno della cartella di lavoro non siano nascosti (`Visible = true`) e che eventuali collegamenti a immagini esterne siano incorporati prima dell'esportazione. |
| **Posso esportare più fogli di lavoro in diapositive PPTX separate?** | Usa `WorkbookDesigner.ExportToPptx` in un ciclo, specificando un `ExportOptions` diverso per ogni foglio di lavoro, oppure combinali in un'unica presentazione aggiungendo diapositive manualmente tramite Aspose.Slides. |
| **`CalculateFormula` è thread‑safe?** | No. Esegui i calcoli su un singolo thread o clona la cartella di lavoro per thread per evitare condizioni di gara. |

## Conclusione

Ora disponi di una **soluzione completa, end‑to‑end per esportare Excel in PowerPoint** usando Aspose.Cells, e comprendi come **calcolare le formule di Excel nel codice**—inclusa la moderna funzione `EXPAND`. Il tutorial ha coperto il caricamento di una cartella di lavoro, la copia di tabelle pivot, l'esportazione in PowerPoint modificabile, l'esportazione personalizzata di stringhe, il calcolo delle formule e il salvataggio finale.

Da qui puoi:

* Estendere l'esportazione per includere più diapositive per foglio di lavoro (la parola chiave secondaria: *calculate Excel formulas in code* può essere riutilizzata nella generazione dei dati dei grafici).  
* Integrare Aspose.Slides per aggiungere animazioni o layout di diapositiva master.  
* Sostituire il semplice delegato `CustomExport` con una formattazione sensibile alla localizzazione per progetti internazionali.  

Sentiti libero di sperimentare con diversi intervalli, esplorare altre funzioni di Office‑365 (ad esempio, `FILTER`, `SORT`), e combinare questo flusso di lavoro con la consegna automatizzata di email per pipeline di reporting completamente automatizzate.

---


## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Automatizza l'esportazione dei dati Excel usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Come esportare i grafici Excel in PDF usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Esporta le celle Excel in immagine usando Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}