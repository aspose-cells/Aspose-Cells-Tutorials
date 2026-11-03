---
category: general
date: 2026-10-20
description: Scopri come utilizzare wrapcols in Aspose.Cells, incorporare i font in
  HTML e salvare Excel come HTML con un esempio completo in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: it
lastmod: 2026-10-20
og_description: Come utilizzare wrapcols in Aspose.Cells, incorporare i font in HTML
  e convertire una cartella di lavoro in HTML con una chiara guida passo passo in
  C# per gli sviluppatori.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Come usare wrapcols e incorporare i font esportando Excel in HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Come usare wrapcols e incorporare i font salvando Excel in HTML
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare wrapcols e incorporare i font salvando Excel in HTML

Se hai bisogno di **come usare wrapcols** in una formula Aspose.Cells, questa guida ti mostra i passaggi esatti. Imparerai anche come **incorporare i font in HTML** e **salvare Excel come HTML** in modo che l'output abbia lo stesso aspetto su tutti i browser.  

Il tutorial copre tre scenari pratici: l'uso della funzione `WRAPCOLS`, l'esportazione di una cartella di lavoro con font incorporati e la generazione di un report master‑detail con Smart Markers. Alla fine avrai un unico programma C# eseguibile che dimostra tutte queste funzionalità.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 (o successivo) installato.
* Aspose.Cells per .NET aggiunto al tuo progetto (`dotnet add package Aspose.Cells`).
* Conoscenza di base di C# e delle formule Excel.

Non sono richieste librerie di terze parti aggiuntive; Aspose.Cells gestisce internamente la conversione HTML e l'incorporamento dei font.

## Passo 1: Dimostrare la funzione **come usare wrapcols** in una formula

La funzione `WRAPCOLS` divide un intervallo unidimensionale in un array bidimensionale, riempiendo prima le colonne. Questo è utile quando è necessario ristrutturare i dati per report o grafici.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Perché funziona:**  
`WRAPCOLS` accetta due argomenti – l'intervallo di origine e il numero di colonne. La funzione riempie l'array colonna per colonna, scartando eventuali valori in eccesso (il `3` nell'esempio). Il risultato appare nella cella in alto a sinistra dell'intervallo di destinazione (`B1`), e puoi espandere l'intervallo manualmente se ti serve l'array completo.

> **Consiglio:** Dopo aver impostato la formula, chiama `workbook.CalculateFormula()` per garantire che il risultato sia aggiornato prima di leggere i valori delle celle.

## Passo 2: **Convertire la cartella di lavoro in HTML** e **incorporare i font in html**

Quando esporti un file Excel in HTML, i font vengono spesso sostituiti da quelli predefiniti del browser, il che può compromettere il layout visivo. Aspose.Cells ti consente di incorporare i font esatti utilizzati nella cartella di lavoro direttamente nel file HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Perché l'incorporamento dei font è importante:**  
Quando `EmbedFonts` è `true`, Aspose.Cells converte ogni font TrueType/OpenType utilizzato in una regola `@font-face` codificata in Base64 all'interno dell'HTML generato. Questo elimina la necessità che il computer client abbia i medesimi font installati, garantendo un rendering pixel‑perfect.

> **Caso limite:** Se la cartella di lavoro di origine fa riferimento a un font non installato sul server, Aspose.Cells ricadrà su un font predefinito e genererà un avviso. Assicurati che i font richiesti siano disponibili


## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare WRAPCOLS in C# – Creare una cartella di lavoro Excel con funzioni di avvolgimento](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Come incorporare i font in HTML – Convertire Excel in HTML con C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Come convertire file Excel in HTML usando Aspose.Cells per .NET: Nascondere contenuti sovrapposti](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}