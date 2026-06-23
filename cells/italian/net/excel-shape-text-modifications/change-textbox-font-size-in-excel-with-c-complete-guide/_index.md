---
category: general
date: 2026-05-30
description: Modifica la dimensione del carattere della casella di testo in Excel
  usando C#. Scopri come modificare rapidamente il carattere della casella di testo
  di Excel con codice passo‑passo.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: it
og_description: Modifica la dimensione del carattere della casella di testo in Excel
  usando C#. Questa guida mostra come modificare il carattere della casella di testo
  di Excel in modo sicuro ed efficiente.
og_title: Modifica la dimensione del carattere della casella di testo in Excel con
  C# – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Modifica la dimensione del carattere della casella di testo in Excel con C#
  – Guida completa
url: /it/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifica la dimensione del carattere della casella di testo in Excel con C# – Guida completa

Hai bisogno di **modificare la dimensione del carattere della casella di testo** in un foglio di lavoro Excel da C#? Sei nel posto giusto. Che tu stia generando report, costruendo una dashboard o semplicemente modificando un modello, regolare l'aspetto di una casella di testo può rendere il tuo foglio di calcolo molto più professionale.

In questo tutorial **modificheremo il carattere della casella di testo in Excel** oltre alla sola dimensione — pensa a famiglia di caratteri, grassetto e persino alla gestione di più forme. Alla fine avrai uno snippet pronto all'uso che copre ogni aspetto del processo, dall'apertura della cartella di lavoro alla pulizia degli oggetti COM. Niente superfluo, solo codice pratico che puoi inserire nel tuo progetto subito.

## Prerequisiti — Cosa ti serve

Prima di immergerci, assicurati di avere quanto segue sulla tua macchina:

| Requisito | Perché è importante |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Fornisce il compilatore C# e il runtime. |
| **Microsoft.Office.Interop.Excel** NuGet package | Fornisce i tipi COM interop necessari per interagire con Excel. |
| **Excel installed** (any recent version) | Il livello Interop funziona solo quando l'app Office è presente. |
| **Basic C# knowledge** | Ti sarà facile seguire, ma spiegheremo ogni riga. |

Se qualcuno di questi manca, fermati ora e installalo; il resto della guida presuppone che siano presenti.

## Passo 1: Configura il progetto e importa gli spazi dei nomi

Prima di tutto—crea una nuova console app (o integrala in una esistente) e importa lo spazio dei nomi interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Suggerimento:** Se stai puntando a .NET 6+, aggiungi il pacchetto `Microsoft.Office.Interop.Excel` tramite `dotnet add package Microsoft.Office.Interop.Excel`. Questo garantisce che l'alias `Excel` venga risolto correttamente.

## Passo 2: Apri la cartella di lavoro e individua il foglio di destinazione

Ora dobbiamo avviare Excel, aprire il file e puntare al foglio che contiene la casella di testo. Avvolgere questo in un blocco `try/finally` garantisce che gli oggetti COM vengano rilasciati anche se qualcosa va storto.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Perché è importante

Aprire la cartella di lavoro via COM ci fornisce un modello di oggetti live—ciò significa che qualsiasi modifica apportiamo si riflette immediatamente nel file. Impostare `Visible = false` velocizza le cose ed evita finestre pop‑up durante l'automazione.

## Passo 3: Recupera la forma della casella di testo

Excel tratta le caselle di testo come oggetti `Shape` nella collezione `Shapes`, non come una collezione dedicata `TextBox`. Ecco perché il codice qui sotto appare un po' diverso dallo snippet che potresti aver visto online.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Attenzione:** La collezione `Shapes` è indicizzata a partire da 1, quindi aggiungiamo `+1` all'indice zero‑based `textboxIndex` che passi. Dimenticare questo porta a errori “indice fuori intervallo” difficili da debug.

## Passo 4: Modifica la dimensione del carattere della casella di testo (e il nome)

Qui è dove finalmente **modifichiamo la dimensione del carattere della casella di testo**. La proprietà `TextFrame2` ci dà accesso alle opzioni di formattazione rich‑text, che includono `Font.Name` e `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Perché usiamo `TextFrame2`

`TextFrame2` è il modello di oggetti più recente introdotto con Office 2007. Supporta funzionalità tipografiche avanzate ed è generalmente più affidabile rispetto al vecchio `TextFrame`. Usarlo garantisce che la nostra operazione di **modifica della dimensione del carattere della casella di testo** funzioni su versioni moderne di Excel.

## Passo 5: Salva, pulisci e verifica

Dopo aver regolato il carattere, dobbiamo persistere le modifiche e rilasciare ogni riferimento COM. Saltare la pulizia può lasciare processi Excel orfani in background.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Suggerimento:** Se devi **modificare il carattere della casella di testo in Excel** su molti fogli, avvolgi la logica interna in un ciclo che itera su `Workbook.Worksheets`. Ricorda solo di reimpostare `textboxIndex` per ogni foglio.

## Gestione dei casi limite — Caselle di testo multiple e forme mancanti

I fogli di calcolo reali raramente contengono una sola casella di testo. Di seguito trovi due strategie rapide che puoi adottare senza riscrivere l'intero metodo.

### 1. Modifica *tutte* le caselle di testo su un foglio

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identifica una casella di testo per il suo **Nome** invece dell'indice

Se hai dato alla tua casella di testo un nome significativo (ad esempio “TitleBox”), puoi recuperarla direttamente:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Entrambi gli approcci ti permettono di **modificare il carattere della casella di testo in Excel** con precisione, indipendentemente da come è strutturata la cartella di lavoro.

## Panoramica visiva (Opzionale)

Se preferisci un rapido indizio visivo, immagina il diagramma seguente:

![Screenshot che mostra un foglio di lavoro Excel con una casella di testo evidenziata – dimostra come modificare la dimensione del carattere della casella di testo](change-textbox-font-size.png)

*Testo alternativo:* *modifica la dimensione del carattere della casella di testo in Excel – casella di testo evidenziata pronta per la modifica del carattere.*

## Esempio completo funzionante

Mettendo tutto insieme, ecco un unico file che puoi copiare‑incollare in un progetto console e eseguire immediatamente (basta aggiornare il percorso del file e il nome del foglio).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Cosa dovresti imparare dopo?

- [Modificare la dimensione del carattere in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Come personalizzare la dimensione del carattere nelle celle Excel usando Aspose.Cells .NET | Guida completa](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Come impostare gli stili di carattere in Excel usando Aspose.Cells per .NET (Guida passo‑passo)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}