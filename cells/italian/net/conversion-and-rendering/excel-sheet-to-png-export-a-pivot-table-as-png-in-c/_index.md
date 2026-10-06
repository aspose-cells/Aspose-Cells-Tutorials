---
category: general
date: 2026-03-18
description: Tutorial su come convertire un foglio Excel in PNG, mostrando come esportare
  una tabella pivot, impostare l'area di stampa della pivot ed esportare l'immagine
  di un intervallo Excel utilizzando Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: it
og_description: Tutorial su come convertire un foglio Excel in PNG che ti guida passo
  passo nell'esportazione delle tabelle pivot, nell'impostazione dell'area di stampa
  della pivot e nell'esportazione dell'immagine di un intervallo Excel con C#.
og_title: Foglio Excel in PNG – Guida completa per esportare le tabelle pivot
tags:
- Aspose.Cells
- C#
- Excel automation
title: Foglio Excel in PNG – Esporta una tabella pivot come PNG in C#
url: /it/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# foglio excel a png – Esporta una Tabella Pivot come PNG in C#

Hai mai dovuto trasformare un **foglio excel a png** ma non sapevi come catturare solo la tabella pivot? Non sei solo. In molte pipeline di reporting la visuale di una pivot è la star, e esportarla come PNG ti permette di incorporarla in email, dashboard o documentazione senza dover allegare l’intero workbook.

In questa guida ti mostreremo **come esportare i dati della pivot**, **impostare l’area di stampa della pivot**, e infine **esportare l’immagine dell’intervallo excel** così otterrai un pulito file **esporta foglio di lavoro in immagine**. Niente collegamenti misteriosi a documenti esterni—solo uno snippet completo, eseguibile, e la logica dietro ogni riga.

## Cosa ti serve

- **Aspose.Cells for .NET** (il pacchetto NuGet `Aspose.Cells` – versione 23.12 o successiva).  
- Un ambiente di sviluppo .NET (Visual Studio, Rider o la CLI `dotnet`).  
- Un file Excel (`input.xlsx`) che contenga almeno una tabella pivot.

Questo è tutto. Se hai questi elementi, immergiamoci.

## Passo 1 – Carica il Workbook e prendi il Primo Foglio

Prima di poter toccare la pivot, dobbiamo avere il workbook in memoria.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Perché è importante:* Caricare il file ci dà accesso a tutti gli oggetti (tabelle, grafici, pivot). Usare il primo foglio è un valore predefinito semplice; puoi sostituire `0` con l’indice o il nome reale del foglio se necessario.

## Passo 2 – Recupera l’Intervallo della Tabella Pivot

Una tabella pivot vive all’interno di un blocco di celle. Abbiamo bisogno di quel blocco così possiamo dire a Excel cosa stampare.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Perché lo facciamo:* `PivotTableRange` ci indica le righe/colonne di inizio e fine esatte. Senza di esso, l’esportazione includerebbe l’intero foglio, vanificando lo scopo di **impostare l’area di stampa della pivot**.

## Passo 3 – Definisci l’Area di Stampa Così Solo la Pivot Viene Renderizzata

Il motore di stampa di Excel rispetta la proprietà `PrintArea`. Riducendola alla pivot, evitiamo dati estranei o celle vuote.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Consiglio esperto:* Se hai più pivot nello stesso foglio, puoi combinare i loro intervalli usando una lista separata da virgole (`"0,0:10,5,12,0:22,5"`). Questa è la tecnica **esporta intervallo excel in immagine** per più blocchi.

## Passo 4 – Configura le Opzioni di Esportazione Immagine (Formato PNG)

Aspose.Cells ti permette di perfezionare l’output. PNG è lossless, perfetto per visuali di pivot nitide.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Perché PNG?* A differenza di JPEG, PNG conserva la nitidezza del testo e gli sfondi trasparenti, rendendolo la scelta ideale per scenari **foglio excel a png**.

## Passo 5 – Esporta il Foglio (Area Pivot) in un File PNG

Ora avviene la magia—renderizzare l’area di stampa definita in un’immagine.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Cosa vedrai:* Un file `pivot.png` che contiene solo la tabella pivot, senza righe o colonne aggiuntive. Aprilo con qualsiasi visualizzatore di immagini e avrai una visuale pronta da condividere.

---

## Domande Frequenti & Casi Limite

### E se il workbook ha **più tabelle pivot**?

Recupera `PivotTableRange` di ciascuna pivot, unisci gli intervalli e assegna la stringa combinata a `PrintArea`. Esempio:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Posso esportare in **altri formati immagine**?

Assolutamente. Cambia `imgOptions.ImageFormat = ImageFormat.Jpeg;` (oppure `Bmp`, `Gif`, `Tiff`). Ricorda solo che JPEG introduce artefatti di compressione—di solito non ideale per pivot ricche di testo.

### Come gestire **pivot di grandi dimensioni** che si estendono su più pagine?

Imposta `imgOptions.OnePagePerSheet = false;` per consentire il rendering su più pagine, poi itera attraverso le pagine:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### E le **righe/colonne nascoste**?

Aspose rispetta le impostazioni di visibilità del foglio. Se devi ignorare gli elementi nascosti, rivelali temporaneamente prima dell’esportazione o regola manualmente `PrintArea`.

---

## Esempio Completo (Pronto per Copia‑Incolla)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Esegui il programma e troverai `pivot.png` proprio dove hai indicato. Apri il file—dovresti vedere una resa nitida solo della tabella pivot, nient’altro.

---

## Conclusione

Ora disponi di una **soluzione completa, end‑to‑end** per trasformare un **foglio excel a png** concentrandoti esclusivamente su una tabella pivot. Impostando **l’area di stampa della pivot**, configurando **le opzioni di esportazione immagine**, e usando il metodo `ToImage` di Aspose.Cells, puoi automatizzare la generazione di report, incorporare visuali in pagine web o semplicemente archiviare snapshot analitici.

Qual è il prossimo passo? Prova a sostituire il PNG con un PDF ad alta risoluzione (`ImageFormat.Pdf`), sperimenta con più pivot su un unico foglio, o combina questo approccio con l’esportazione di grafici per una pipeline di esportazione dashboard completa.

Hai un trucco da condividere? Lascia un commento, o avvia il prossimo tutorial dove esploreremo **esporta foglio di lavoro in immagine** per snapshot dell’intero foglio, includendo grafici e formattazione condizionale. Buon coding!  

<img src="pivot.png" alt="esempio di esportazione di tabella pivot da foglio excel a png">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}