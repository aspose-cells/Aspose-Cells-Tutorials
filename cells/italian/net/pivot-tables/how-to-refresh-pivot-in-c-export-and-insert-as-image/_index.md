---
category: general
date: 2026-05-04
description: Come aggiornare la tabella pivot in C# ed esportarla come PNG, quindi
  inserire l'immagine nel foglio di lavoro. Segui questa guida passo passo con il
  codice completo.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: it
og_description: Come aggiornare il pivot in C#? Scopri come esportare la tabella pivot
  come immagine e inserirla in un foglio di lavoro con esempi di codice completi.
og_title: Come aggiornare Pivot in C# – Esporta e inserisci come immagine
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Come aggiornare la tabella pivot in C# – Esporta e inserisci come immagine
url: /it/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiornare una tabella pivot in C# – Esportare e inserire come immagine

Aggiornare una pivot in C# è un ostacolo frequente quando si automatizzano i report Excel. In questa guida vedrai esattamente **come aggiornare la pivot**, esportarla come PNG e inserire quell'immagine in un segnaposto del foglio di lavoro—tutto con un unico programma eseguibile.

Se ti stai anche chiedendo *come esportare una pivot* o hai bisogno di **inserire un'immagine nel foglio di lavoro**, sei nel posto giusto. Passeremo in rassegna ogni riga, spiegheremo perché è importante e tratteremo anche alcuni casi limite che potresti incontrare in progetti reali.

---

## Cosa ti serve

Prima di iniziare, assicurati di avere:

- **Aspose.Cells for .NET** (la libreria che fornisce `Workbook`, `Worksheet`, `ImageOrPrintOptions`, ecc.). Puoi ottenerla da NuGet: `Install-Package Aspose.Cells`.
- .NET 6 o versioni successive (il codice qui sotto è destinato a .NET 6, ma funziona con qualsiasi versione recente).
- Una conoscenza di base di C# e della gestione dei file—nulla di complicato.

Questo è tutto. Nessun DLL aggiuntivo, nessun interop COM, solo una semplice app console C#.

---

## Passo 1 – Caricare la cartella di lavoro Excel in stile C#

Per prima cosa, dobbiamo aprire il file di origine. È qui che si trova la parte **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Perché?**  
> Caricare la cartella di lavoro ci dà accesso ai fogli, alle tabelle pivot e ai segnaposto delle immagini. Se il file non viene trovato, Aspose genera una chiara `FileNotFoundException`, che puoi gestire per un'interfaccia più amichevole.

---

## Passo 2 – Preparare le opzioni immagine per esportare la pivot

Ora diciamo ad Aspose come vogliamo che l'immagine esportata appaia. Questo è il fulcro di **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Consiglio:**  
> Se ti serve un JPEG per ridurre le dimensioni del file, cambia `SaveFormat.Png` in `SaveFormat.Jpeg` e regola `Quality` di conseguenza.

---

## Passo 3 – Codice per aggiornare la tabella pivot

Una tabella pivot obsoleta mostra dati vecchi. Aggiornarla garantisce che l'immagine rifletta i numeri più recenti.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Perché aggiornare?**  
> Le tabelle pivot memorizzano nella cache i dati di origine al momento della creazione. Se il foglio di lavoro sottostante cambia (ad esempio, vengono aggiunte nuove righe), la cache diventa obsoleta. Chiamare `Refresh()` costringe Aspose a rieseguire la query sull'intervallo di origine, assicurando che l'immagine esportata non rimanga bloccata con totali vecchi.

---

## Passo 4 – Convertire la pivot aggiornata in un'immagine

Ecco la riga magica che effettivamente **export pivot** in un array di byte.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Cosa ottieni:**  
> `pivotImage` ora contiene un'immagine della tabella pivot codificata in PNG, pronta per essere scritta su disco o incorporata altrove.

---

## Passo 5 – Inserire l'immagine nel foglio di lavoro

Qui è dove **insert image into worksheet**. Inseriremo l'immagine nel primo segnaposto immagine (se presente).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Perché usare un segnaposto?**  
> Molti modelli Excel includono una forma immagine pre‑formattata (dimensione, bordo, posizione). Puntando a `Pictures[0]`, manteniamo intatto il layout. Se il modello non ha un segnaposto, il fallback crea una nuova immagine ancorata alla cella A1.

---

## Passo 6 – Salvare la cartella di lavoro (opzionale)

Infine, persisti le modifiche. Puoi sovrascrivere l'originale o scrivere in un nuovo file.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Risultato atteso:**  
> Apri `output.xlsx` e vedrai la tabella pivot aggiornata, esportata come PNG nitido, e visualizzata nello slot della prima immagine. Il resto della cartella di lavoro rimane invariato.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il blocco di codice completo che puoi inserire in un nuovo progetto console. Nessuna parte è mancante.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Esegui il programma, apri il file risultante e verifica che la pivot rifletta i dati più recenti e appaia come un'immagine ad alta risoluzione.

---

## Domande frequenti & casi limite

| Question | Answer |
|----------|--------|
| **E se la cartella di lavoro ha più fogli di lavoro?** | Modifica `workbook.Worksheets[0]` con l'indice o il nome appropriato (`workbook.Worksheets["Sheet2"]`). |
| **Posso esportare più tabelle pivot?** | Itera su `worksheet.PivotTables` e ripeti i passi 3‑4 per ciascuna. Salva ogni immagine in un segnaposto separato o combinale in un unico foglio. |
| **E se le tabelle pivot grandi causano pressione sulla memoria?** | Usa `ImageOrPrintOptions` con un DPI più basso o esporta in JPEG per ridurre la dimensione dell'array di byte. |
| **Devo rilasciare qualcosa?** | Gli oggetti Aspose sono gestiti; l'istruzione `using` non è obbligatoria, ma puoi avvolgere `Workbook` in un blocco `using` se preferisci una pulizia deterministica. |
| **È compatibile con .NET Core?** | Sì. Aspose.Cells supporta .NET Core, .NET 5/6 e .NET Framework. Basta fare riferimento al pacchetto NuGet appropriato. |

---

## Suggerimenti & buone pratiche

- **Convalida i percorsi**: Usa `Path.Combine` e `Environment.GetFolderPath` per evitare separatori hard‑coded.
- **Gestione degli errori**: Avvolgi l'intero corpo di `Main` in un `try/catch` e registra `Exception.Message` per gli script di produzione.
- **Progettazione del modello**: Inserisci una forma immagine trasparente dove desideri l'immagine della pivot; questo preserva le larghezze delle colonne e le altezze delle righe.
- **Prestazioni**: Se ti serve solo l'immagine, puoi omettere del tutto il salvataggio della cartella di lavoro e scrivere `pivotImage` in un file PNG separato.

---

## Conclusione

Ora sai **how to refresh pivot** in C#, esportare quella vista aggiornata come immagine e **insert image into worksheet** senza problemi. La soluzione completa—caricamento della cartella di lavoro, impostazione delle opzioni di esportazione, aggiornamento della pivot, conversione in PNG e salvataggio del file—copre l'intero flusso di lavoro richiesto.

Pronto per la prossima sfida? Prova a combinare **how to export pivot** con l'elaborazione batch di più file, o esplora il **refresh pivot table code** per sorgenti dati dinamiche come database o feed CSV. Lo stesso schema si applica: carica, aggiorna, esporta, inserisci, salva.

Buon coding, e che le tue automazioni Excel rimangano sempre aggiornate e perfette come un'immagine!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}