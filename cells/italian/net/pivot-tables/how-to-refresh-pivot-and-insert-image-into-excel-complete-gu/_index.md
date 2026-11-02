---
category: general
date: 2026-04-07
description: Scopri come aggiornare le tabelle pivot, inserire un'immagine in Excel
  e salvare la cartella di lavoro di Excel con un segnaposto per l'immagine in pochi
  passaggi.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: it
og_description: Come aggiornare la tabella pivot in Excel, inserire un'immagine in
  Excel e salvare la cartella di lavoro Excel usando C# con un segnaposto immagine.
  Esempio di codice passo‑passo.
og_title: Come aggiornare la tabella pivot e inserire un'immagine in Excel – Guida
  completa
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come aggiornare la tabella pivot e inserire un'immagine in Excel – Guida completa
url: /it/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiornare una tabella pivot e inserire un'immagine in Excel – Guida completa

Ti sei mai chiesto **come aggiornare una pivot** quando i dati di origine cambiano, e poi inserire un grafico o un'immagine della tabella appena aggiornata nello stesso foglio? Non sei il solo. In molti flussi di reporting i dati vivono in un database, la tabella pivot li estrae, e il file Excel finale deve mostrare i numeri più recenti come immagine—così gli utenti successivi non possono modificare accidentalmente la fonte.

In questo tutorial vedremo passo passo esattamente questo: **come aggiornare una pivot**, **inserire un'immagine in Excel**, e infine **salvare la cartella di lavoro Excel** usando un **segnaposto immagine**. Alla fine avrai un unico programma C# eseguibile che fa tutto, e comprenderai perché ogni riga è importante.

> **Pro tip:** L'approccio funziona con Aspose.Cells 2024 o versioni successive, il che significa che non è necessario avere Excel installato sul server.

---

## Di cosa avrai bisogno

- **Aspose.Cells per .NET** (pacchetto NuGet `Aspose.Cells`).  
- .NET 6.0 SDK o versioni successive (il codice compila anche con .NET 8).  
- Un file Excel di base (`input.xlsx`) che contiene già una tabella pivot e un segnaposto immagine (il primo oggetto immagine nel foglio).  
- Un po' di curiosità sui modelli di oggetti di Excel.

Nessun interop COM aggiuntivo, nessuna installazione di Office, solo puro C#.

---

## Come aggiornare la pivot e catturare i dati più recenti

La prima cosa da fare è dire a Excel (o meglio, ad Aspose.Cells) che la tabella pivot deve ricalcolarsi in base all'intervallo di origine più recente. Saltare questo passaggio ti lascia con numeri obsoleti, vanificando lo scopo dell'automazione.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Perché è importante:**  
Quando chiami `Refresh()`, il motore della pivot riesegue la logica di aggregazione. Se in seguito esporti la pivot come immagine, la foto mostrerà i totali *correnti*, non quelli presenti quando il file è stato salvato l'ultima volta.

---

## Inserire un'immagine in Excel usando un segnaposto immagine

Ora che la pivot è aggiornata, dobbiamo trasformarla in un'immagine statica. Questo è utile quando vuoi bloccare il visual per la distribuzione o incorporarlo in una slide PowerPoint in seguito.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

L'oggetto `ImageOrPrintOptions` ti permette di controllare risoluzione, sfondo e formato. PNG è senza perdita e funziona benissimo per la maggior parte dei report aziendali.

---

## Aggiungere un segnaposto immagine a un foglio di lavoro

La maggior parte dei modelli Excel contiene già una forma o immagine che funge da “slot” per grafiche dinamiche. Se non ne hai uno, inserisci semplicemente un'immagine vuota in Excel e salva il modello—Aspose.Cells la esporrà come `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**E se hai più segnaposti?**  
Basta cambiare l'indice (`Pictures[1]`, `Pictures[2]`, …) o iterare su `worksheet.Pictures` per trovarne uno per nome.

---

## Salvare la cartella di lavoro Excel dopo le modifiche

Infine, persistiamo le modifiche. La cartella di lavoro ora contiene una pivot aggiornata, un PNG appena generato e il segnaposto immagine aggiornato con quell'immagine.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Quando apri `output.xlsx` vedrai lo slot immagine riempito con l'istantanea più recente della pivot. Nessun passaggio manuale richiesto.

---

## Esempio completo funzionante (tutti i passaggi insieme)

Di seguito trovi il programma completo, pronto per il copia‑incolla. Include le istruzioni `using` necessarie, la gestione degli errori e i commenti che spiegano ogni riga non ovvia.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Risultato atteso:**  
Apri `output.xlsx`. Il primo oggetto immagine ora mostra un PNG della tabella pivot appena aggiornata. Se modifichi i dati di origine in `input.xlsx` ed esegui nuovamente il programma, l'immagine si aggiorna automaticamente—senza necessità di copia‑incolla manuale.

---

## Variazioni comuni & casi limite

| Situazione | Cosa cambiare |
|-----------|----------------|
| **Più tabelle pivot** | Itera su `sheet.PivotTables` e aggiorna ciascuna, poi scegli quella necessaria per l'immagine. |
| **Formato immagine diverso** | Imposta `ImageFormat = ImageFormat.Jpeg` (o `Bmp`) in `ImageOrPrintOptions`. |
| **Selezione dinamica del segnaposto** | Usa `sheet.Pictures["MyPlaceholderName"]` invece di un indice. |
| **Cartelle di lavoro molto grandi** | Aumenta `Workbook.Settings.CalculateFormulaEngine` a `EngineType.Fast` per refresh più rapidi. |
| **Esecuzione su server headless** | Aspose.Cells funziona completamente senza interfaccia UI, quindi non serve configurazione aggiuntiva. |

---

## Domande frequenti

**D: Funziona con cartelle di lavoro abilitate alle macro (`.xlsm`)?**  
R: Sì. Aspose.Cells le tratta come qualsiasi altra cartella di lavoro; le macro vengono preservate ma non eseguite durante il refresh.

**D: E se la pivot utilizza una fonte dati esterna?**  
R: Devi assicurarti che la stringa di connessione sia valida sulla macchina che esegue il codice. Usa `pivotTable.CacheDefinition.ConnectionInfo` per modificarla programmaticamente.

**D: Posso inserire l'immagine in un intervallo di celle specifico invece di un segnaposto?**  
R: Assolutamente. Usa `sheet.Pictures.Add(row, column, pivotImg)` dove `row` e `column` sono indici a zero.

---

## Conclusione

Abbiamo coperto **come aggiornare una pivot**, **inserire un'immagine in Excel**, **aggiungere un segnaposto immagine** e infine **salvare la cartella di lavoro Excel**—tutto in un compatto snippet C#. Aggiornando prima la pivot, garantisci che l'immagine rifletta i numeri più recenti, e usando un segnaposto mantieni i tuoi modelli puliti e riutilizzabili.

Prossimi passi consigliati:

- Esportare la stessa immagine in un report PDF (`PdfSaveOptions`).  
- Automatizzare un batch di file con dati di origine diversi.  
- Usare Aspose.Slides per incollare il PNG direttamente in una slide PowerPoint.

Sentiti libero di sperimentare—sostituisci il PNG con un JPEG, cambia DPI, o aggiungi più immagini. L'idea di base rimane la stessa: mantieni i dati aggiornati, catturali come immagine e inseriscili dove serve.

Buon coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}