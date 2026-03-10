---
category: general
date: 2026-02-15
description: Come copiare il carattere e applicare lo stile della cella in C# con
  un semplice esempio. Scopri come ottenere lo stile della cella e utilizzare la formattazione
  della cella per impostare la dimensione del carattere della casella di testo.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: it
og_description: come copiare il carattere da una cella di un foglio di lavoro e applicare
  lo stile della cella a una casella di testo. Questa guida mostra come ottenere lo
  stile della cella, utilizzare la formattazione della cella e impostare la dimensione
  del carattere della casella di testo.
og_title: come copiare il font da una cella di Excel – Tutorial completo C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: come copiare il carattere da una cella di Excel a una TextBox – Guida passo
  passo
url: /it/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come copiare il font da una cella Excel a una TextBox – Tutorial completo C#

Ti è mai capitato di dover **copiare il font** da una cella di un foglio di calcolo e far sì che una TextBox dell’interfaccia utente abbia esattamente lo stesso aspetto? Non sei l’unico. In molti strumenti di reporting o dashboard personalizzate ti troverai a estrarre dati da Excel e a voler mantenere la fedeltà visiva—famiglia di font, dimensione e colore—intatta.  

La buona notizia è che, con poche righe di C#, puoi **ottenere lo stile della cella**, leggere le sue proprietà del font e **applicare lo stile della cella** a qualsiasi controllo TextBox. In questo tutorial percorreremo un esempio completo, eseguibile, che mostra come **usare la formattazione della cella** e persino **impostare la dimensione del font della textbox** in modo programmatico.

---

## Cosa imparerai

- Come recuperare un oggetto `TextBox` da un componente griglia (`gridJs` nel nostro esempio)  
- Come leggere la famiglia, la dimensione e il colore del font da una specifica cella Excel (`B2`)  
- Come copiare quegli attributi di font nella TextBox affinché l’interfaccia rispecchi il foglio di calcolo  
- Le insidie più comuni (es. conversione del colore) e alcuni **pro tip** per rendere il codice più robusto  
- Uno snippet di codice pronto all’uso che puoi inserire in un’app console o in un progetto WinForms  

**Prerequisiti**  
Devi avere:

1. .NET 6+ (o .NET Framework 4.8) installato  
2. Il pacchetto NuGet EPPlus (per la gestione di Excel)  
3. Un controllo griglia che esponga un dizionario `TextBoxes` (l’esempio usa un fittizio `gridJs`, ma l’idea funziona con qualsiasi libreria UI)

Ora, mettiamoci al lavoro.

---

## Passo 1: Configura il progetto e carica il foglio di lavoro

Per prima cosa, crea un nuovo progetto console o WinForms e aggiungi EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Quindi, carica la cartella di lavoro e prendi la cella il cui stile vuoi copiare.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Perché è importante:** EPPlus ti dà accesso diretto all’oggetto `Style`, che contiene il sotto‑oggetto `Font`. Da lì puoi leggere `Name`, `Size` e `Color`. Questo è il nucleo dell’operazione **get cell style**.

---

## Passo 2: Recupera la TextBox di destinazione dalla tua griglia

Supponendo che la tua griglia UI (`gridJs`) memorizzi le TextBox in un dizionario indicizzato per nome colonna, puoi recuperare quella desiderata così:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Se usi WinForms, `notesTextBox` potrebbe essere un controllo `TextBox`; per WPF potrebbe essere un elemento `TextBox`, e per una griglia basata sul web potrebbe essere un oggetto di interfaccia JavaScript. L’importante è avere un riferimento manipolabile.

---

## Passo 3: Trasferisci la famiglia di font

Ora che abbiamo sia lo stile sorgente sia il controllo di destinazione, copiamo la famiglia di font.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Non tutti i framework UI espongono una proprietà `FontFamily` che accetti una semplice stringa. In WinForms imposteresti `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Adatta di conseguenza.

---

## Passo 4: Trasferisci la dimensione del font

La dimensione del font è memorizzata come `float` in EPPlus. Applicala direttamente:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Se il tuo controllo usa i punti (come la maggior parte), puoi assegnare il valore senza conversione. Per griglie basate su CSS potresti dover aggiungere `"pt"`.

---

## Passo 5: Trasferisci il colore del font

La conversione del colore è la parte più delicata perché EPPlus conserva i colori come interi ARGB, mentre molti framework UI si aspettano un `System.Drawing.Color` o una stringa esadecimale CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Perché funziona:** `GetColor()` risolve i colori basati su tema e restituisce un `System.Drawing.Color` concreto. Se la cella utilizza il colore predefinito (nessuna impostazione esplicita), impostiamo il valore predefinito a nero per evitare eccezioni di riferimento nullo.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco una minima app console che legge un file Excel, estrae il font da **B2** e lo applica a una TextBox simulata.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Output previsto (supponendo che B2 usi Arial, 12 pt, blu):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Esegui il programma, apri la tua UI e vedrai che la TextBox “Notes” ora rispecchia esattamente lo stile del font della cella **B2**. Nessuna regolazione manuale necessaria.

---

## Domande frequenti & casi limite

### E se la cella usa un colore di tema invece di un valore RGB esplicito?

`GetColor()` di EPPlus risolve automaticamente i colori di tema in un `System.Drawing.Color` concreto. Tuttavia, se utilizzi una libreria più vecchia che restituisce solo l’indice del tema, dovrai mappare quell’indice a una tavolozza di colori da solo.

### Posso copiare altri attributi di stile (es. grassetto, corsivo)?

Assolutamente. L’oggetto `ExcelStyle.Font` espone anche `Bold`, `Italic`, `Underline` e `Strike`. Basta impostare le proprietà corrispondenti sul tuo controllo UI:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### E se il controllo griglia non espone una proprietà `FontColor`?

La maggior parte dei framework UI moderni la supporta, ma se il tuo accetta solo una stringa CSS, converti il `Color` in esadecimale:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Come gestire più celle contemporaneamente?

Itera sull’intervallo desiderato, recupera lo stile di ogni cella e applicalo alla TextBox corrispondente. Ricorda di cacheare gli oggetti stile se elabori molte righe per evitare colli di bottiglia di prestazioni.

---

## Pro tip & insidie comuni

- **Cachea l’ExcelPackage** – aprire e chiudere il file per ogni cella è costoso. Carica la cartella di lavoro una sola volta e riutilizza l’oggetto `ExcelWorksheet`.  
- **Attenzione ai colori null** – una cella che eredita il colore predefinito restituisce `null`. Fornisci sempre un fallback (nero o il valore predefinito del controllo).  
- **Gestisci il DPI scaling** – se punti a monitor ad alta DPI, le dimensioni del font possono apparire leggermente più grandi. Regola con `Graphics.DpiX` se necessario.  
- **Sicurezza dei thread** – EPPlus non è thread‑safe. Se elabori molti fogli in parallelo, crea un `ExcelPackage` separato per ogni thread.

---

## Conclusione

Ora sai **come copiare il font** da una cella Excel e **applicare lo stile della cella** a qualsiasi controllo TextBox usando C#. Recuperando lo `Style` della cella, estraendo le proprietà del suo `Font` e assegnandole all’elemento UI, mantieni la coerenza visiva senza copie manuali.  

La soluzione completa—caricamento della cartella di lavoro, ottenimento dello stile della cella e impostazione della famiglia, dimensione e colore del font della TextBox—copre il nucleo di **use cell formatting** e dimostra come **set textbox font size** correttamente.  

Come passo successivo, prova ad estendere l’esempio per copiare colori di sfondo, bordi o addirittura l’intero contenuto della cella. Se lavori con una libreria data‑grid che supporta il rendering ricco delle celle, ora puoi fornire le stesse informazioni di stile estratte da Excel, mantenendo UI e report perfettamente sincronizzati.

Hai altre domande? Lascia un commento o esplora argomenti correlati come “dynamic Excel‑to‑UI binding” e “theme‑aware colour conversion”. Buon coding!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}