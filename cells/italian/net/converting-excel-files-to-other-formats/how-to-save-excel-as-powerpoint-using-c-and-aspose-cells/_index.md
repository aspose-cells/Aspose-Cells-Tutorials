---
category: general
date: 2026-08-17
description: Salva Excel come PowerPoint con C# – guida passo‑passo per convertire
  file XLSX, rendere le caselle di testo modificabili e generare output PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: it
lastmod: 2026-08-17
og_description: Salva Excel come PowerPoint in C# con un esempio di codice completo.
  Scopri come convertire XLSX, rendere le caselle di testo modificabili e esportare
  in PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Salva Excel come PowerPoint in C# – guida completa alla conversione
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Come salvare Excel come PowerPoint usando C# e Aspose.Cells
url: /it/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come salvare Excel come PowerPoint usando C# e Aspose.Cells

Se hai bisogno di **salvare Excel come PowerPoint** in un progetto .NET, questa guida ti mostra una soluzione completa, pronta‑da‑eseguire. Vedrai come caricare una cartella di lavoro XLSX, rendere ogni casella di testo sul foglio modificabile e esportare il risultato in un file PPTX—tutto con poche righe di C#.

Convertire Excel in PowerPoint è una necessità comune per dashboard di reporting, presentazioni o generazione automatica di slide. Questo tutorial copre anche **come modificare le caselle di testo** programmaticamente, così puoi personalizzare il contenuto della slide prima di salvare.

## Prerequisiti

* SDK .NET 6.0 (o successivo) installato  
* Un ambiente di sviluppo come Visual Studio 2022 o VS Code  
* Una licenza Aspose.Cells per .NET (o una chiave di valutazione gratuita) – scarica dal [sito web di Aspose](https://products.aspose.com/cells/net/)  
* Il file `input.xlsx` che desideri convertire  

> **Suggerimento:** Se utilizzi la versione di valutazione gratuita, il PPTX di output conterrà una filigrana. Una versione con licenza la rimuove.

## Passo 1: Installa il pacchetto NuGet Aspose.Cells

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.Cells
```

Questo aggiunge l'assembly `Aspose.Cells`, che fornisce le classi `Workbook`, `Worksheet` e `Shape` necessarie per la conversione.

## Passo 2: Crea lo scheletro di un'applicazione console

Crea un nuovo progetto console (se non ne hai già uno):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Sostituisci il `Program.cs` generato con il codice mostrato nei passaggi successivi.

## Passo 3: Carica la cartella di lavoro e seleziona il primo foglio di lavoro

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Perché è importante:**  
`Workbook` legge il file Excel in memoria, mentre `Worksheet` ti dà accesso alle celle, ai grafici e alle forme del foglio. Il primo foglio di lavoro è spesso il report predefinito che vuoi presentare.

## Passo 4: Rendi ogni casella di testo sul foglio modificabile

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Perché ti serve:**  
Per impostazione predefinita, le caselle di testo importate da Excel sono di sola lettura quando vengono visualizzate in PowerPoint. Impostare `IsEditable = true` consente a te (o agli utenti di PowerPoint in seguito) di modificare il testo direttamente sulla slide.

## Passo 5: Salva la cartella di lavoro come presentazione PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Cosa succede dietro le quinte:**  
`Workbook.Save` rileva il valore enum `SaveFormat.Pptx` e traduce il layout del foglio Excel—incluse righe, colonne, grafici e le caselle di testo ora modificabili—in oggetti slide di PowerPoint.

## Codice sorgente completo (eseguibile)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Output previsto

Quando esegui il programma (`dotnet run`), dovresti vedere:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Aprendo `output.pptx` in Microsoft PowerPoint verrà mostrata una slide che rispecchia il foglio Excel originale. Tutte le caselle di testo possono essere modificate direttamente facendo doppio clic su di esse.

## Domande comuni e casi particolari

| Question | Answer |
|----------|--------|
| **Posso convertire un foglio di lavoro specifico invece del primo?** | Sì. Sostituisci `workbook.Worksheets[0]` con `workbook.Worksheets["SheetName"]` o con qualsiasi indice tu abbia bisogno. |
| **Cosa succede se la cartella di lavoro contiene più fogli?** | Chiama `workbook.Save` una volta per ogni foglio di lavoro, fornendo un nome file PPTX distinto per ciascuno, oppure combinali in un'unica presentazione usando gli oggetti `Presentation` di Aspose.Slides. |
| **I grafici verranno conservati?** | Aspose.Cells converte automaticamente i grafici Excel in oggetti grafico di PowerPoint. Non è necessario alcun codice aggiuntivo. |
| **Come modifico la dimensione della slide?** | Dopo `workbook.Save`, puoi caricare il PPTX generato con Aspose.Slides e regolare `Presentation.SlideSize`. |
| **E se devo modificare il testo della casella di testo prima di salvare?** | Accedi a `shapeItem.TextBox.Text` all'interno del ciclo, modificalo, quindi imposta `IsEditable = true`. Esempio: `shapeItem.TextBox.Text = "New title";` |

## Suggerimenti per la risoluzione dei problemi

* **“ShapeType.TextBox” non trovato** – Assicurati di utilizzare la versione 25.11 o successiva di Aspose.Cells; le versioni precedenti non hanno la proprietà `IsEditable`.  
* **Errori di file non trovato** – Verifica che `YOUR_DIRECTORY` sia un percorso assoluto o che il percorso relativo punti alla posizione corretta.  
* **Licenza non applicata** – Chiama `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` prima di caricare la cartella di lavoro per rimuovere le filigrane di valutazione.

## Conclusione

Ora sai come **salvare Excel come PowerPoint** con C# caricando una cartella di lavoro XLSX, rendendo ogni casella di testo modificabile ed esportando in PPTX. Questo metodo gestisce automaticamente grafici, immagini e formattazione delle celle, fornendoti una presentazione pronta da mostrare.

Successivamente, esplora argomenti correlati come **convertire Excel in PowerPoint con Aspose.Slides**, **come modificare le caselle di testo programmaticamente dopo la conversione**, o **elaborare in batch più cartelle di lavoro**. Ognuno di questi si basa sui passaggi fondamentali trattati qui e può automatizzare ulteriormente il tuo flusso di lavoro di reporting.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire Excel in PowerPoint usando Aspose.Cells per .NET: Guida completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Come copiare una tabella pivot in C# – Convertire Excel in PPTX, copiare intervallo e rendere modificabile la casella di testo](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Come salvare file Excel in più formati usando Aspose.Cells .NET (Guida 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}