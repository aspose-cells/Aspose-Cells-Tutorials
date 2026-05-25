---
category: general
date: 2026-03-30
description: Crea PowerPoint da Excel rapidamente usando Aspose.Cells e Aspose.Slides.
  Scopri come esportare il foglio di lavoro come immagine e salvare la presentazione
  come PPTX in C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: it
og_description: Crea PowerPoint da Excel in C# con Aspose. Esporta il foglio di lavoro
  come immagine, mantieni le forme modificabili e salva il risultato come PPTX.
og_title: Crea PowerPoint da Excel – Tutorial completo C#
tags:
- Aspose
- C#
- Office Automation
title: Crea PowerPoint da Excel – Guida passo‑passo C#
url: /it/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PowerPoint da Excel – Tutorial Completo C#

Ti è mai capitato di **creare PowerPoint da Excel** ma non eri sicuro quale libreria potesse mantenere i tuoi grafici modificabili? Non sei il solo. In molti scenari di reporting vorrai trasformare un foglio di calcolo in una presentazione senza perdere la possibilità di modificare le caselle di testo in seguito. Questa guida ti mostra esattamente come **convertire Excel in PowerPoint** usando Aspose.Cells e Aspose.Slides, coprendo anche come **esportare il foglio di lavoro come immagine** e infine **salvare la presentazione come PPTX**.

Passeremo in rassegna ogni riga di codice, spiegheremo *perché* ogni impostazione è importante e discuteremo anche cosa fare se il tuo workbook contiene grafici complessi che preferisci esportare come immagine. Alla fine avrai un'app console C# pronta all'uso che prende `ShapesDemo.xlsx` e genera `Result.pptx` – il tutto con caselle di testo modificabili e immagini nitide.

## Cosa ti servirà

- .NET 6.0 o versioni successive (l'API funziona anche con .NET Framework, ma .NET 6 è l'opzione ideale).  
- Pacchetti NuGet **Aspose.Cells** e **Aspose.Slides** (le licenze di prova gratuite funzionano per i test).  
- Una conoscenza di base della sintassi C# – se sai scrivere un `Console.WriteLine`, sei pronto.  

Nessun interop COM aggiuntivo, nessun Office installato sul server e nessun copia‑incolla manuale di immagini. Tutto è gestito programmaticamente.

---

## Crea PowerPoint da Excel – Carica il Workbook e Imposta le Opzioni di Esportazione

La prima cosa che facciamo è aprire il file Excel e indicare ad Aspose.Cells come vogliamo che il foglio venga renderizzato. L'oggetto `ImageOrPrintOptions` è dove avviene la magia: abilitiamo `ExportShapes` e `ExportEditableTextBoxes` in modo che tutte le forme (inclusi i grafici) diventino parte della diapositiva **e** rimangano modificabili dopo la conversione.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Perché queste impostazioni?**  
- `OnePagePerSheet` impedisce che il foglio venga diviso in più diapositive – ottieni un'unica immagine a piena dimensione.  
- `ExportShapes` indica ad Aspose.Cells di rasterizzare i grafici *e* le forme vettoriali, preservandone l'aspetto.  
- `ExportEditableTextBoxes` è il segreto che ti permette di fare doppio clic su una casella di testo in PowerPoint e modificare il testo senza riaprire Excel.  

> **Consiglio:** Se ti serve solo un'immagine statica di un grafico, imposta `ExportShapes = false` e utilizza il metodo `ExportExcelChartAsPicture` più tardi (vedi la sezione finale).

---

## Converti Excel in PowerPoint – Genera Immagine dal Foglio di Lavoro

Con le opzioni pronte, ora trasformiamo il foglio di lavoro in un `System.Drawing.Image`. Il `WorksheetToImageConverter` si occupa del lavoro pesante, applicando le impostazioni appena definite.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

L'argomento `0` indica la prima pagina (ne abbiamo solo una grazie a `OnePagePerSheet`). L'`sheetImage` risultante mantiene il DPI originale, quindi la tua diapositiva non apparirà pixelata anche su display ad alta risoluzione.

---

## Salva la Presentazione come PPTX – Inserisci Immagine in una Diapositiva

Ora creiamo un nuovo file PowerPoint, aggiungiamo una diapositiva e inseriamo il bitmap. Aspose.Slides tratta l'immagine come una forma *picture frame*, che puoi successivamente ridimensionare o spostare come qualsiasi oggetto nativo di PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **E se l'immagine è più grande della dimensione della diapositiva?**  
> PowerPoint ritaglierà automaticamente tutto ciò che supera le dimensioni della diapositiva. Una soluzione rapida è scalare l'immagine prima di inserirla:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Puoi quindi passare `newWidth` e `newHeight` a `AddPictureFrame`.

---

## Esporta Foglio di Lavoro come Immagine – Salva il File PPTX

Infine salviamo la presentazione su disco. Il flag `SaveFormat.Pptx` garantisce il moderno formato OpenXML, che funziona su tutte le versioni recenti di PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Quando apri `Result.pptx` vedrai una singola diapositiva che appare esattamente come il tuo foglio Excel, ma potrai comunque cliccare su qualsiasi casella di testo e modificarne il contenuto direttamente in PowerPoint.

---

## Esporta Grafico Excel come Immagine – Quando Sono Preferibili le Immagini Raster

A volte non servono forme modificabili; un PNG di alta qualità di un grafico è sufficiente. Aspose.Cells può esportare un grafico specifico in un'immagine senza convertire l'intero foglio:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Puoi quindi incorporare `chart.png` in una diapositiva nello stesso modo in cui abbiamo aggiunto `sheetImage`. Questo approccio riduce la dimensione del file PPTX ed è utile quando i dati circostanti non sono necessari nella diapositiva.

---

## Problemi Comuni e Come Evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Il testo appare sfocato** | Esportato a DPI basso (default 96). | Imposta `imageOptions.Dpi = 300;` prima della conversione. |
| **Le forme scompaiono** | `ExportShapes` impostato a `false`. | Assicurati che `ExportShapes = true` quando ti servono grafiche modificabili. |
| **Dimensioni della diapositiva non corrispondono** | Immagine più grande delle dimensioni della diapositiva. | Scala l'immagine (vedi snippet di codice) o cambia la dimensione della diapositiva tramite `presentation.SlideSize`. |
| **Eccezione di licenza** | Uso della versione di prova senza corretta attivazione. | Chiama `License license = new License(); license.SetLicense("Aspose.Total.lic");` all'inizio di `Main`. |

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi l'intero programma, pronto da inserire in un nuovo progetto console. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene il tuo file Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Output previsto:**  
Eseguendo il programma stampa `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Aprendo il PPTX vedrai una singola diapositiva che rispecchia il foglio Excel originale, con caselle di testo modificabili.

---

## Riepilogo e Prossimi Passi

Ora sai come **creare PowerPoint da Excel** usando le potenti API di Aspose, come **esportare il foglio di lavoro come immagine**, e come **salvare la presentazione come PPTX** mantenendo la modificabilità. Lo stesso schema funziona per workbook con più fogli—basta iterare su `workbook.Worksheets` e aggiungere una nuova diapositiva per ciascuno.

**Cosa esplorare dopo?**  

- **Conversione batch:** Scorri una cartella di file Excel e genera una presentazione per file.  
- **Layout dinamici:** Usa `slide.LayoutSlide` per applicare template PowerPoint pre‑progettati.  
- **Esportazione solo grafico:** Combina lo snippet “Export Excel chart as picture” con segnaposti diapositive per un deck più leggero.  
- **Stile avanzato:** Applica sfondi personalizzati, transizioni o animazioni alle diapositive tramite Aspose.Slides.  

Sentiti libero di sperimentare—cambia il DPI, sostituisci `ShapeType.Ellipse` con un frame circolare, o anche incorpora più immagini per diapositiva. Il cielo è il limite quando hai il controllo programmatico su

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}