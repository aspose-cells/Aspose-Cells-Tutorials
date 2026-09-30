---
category: general
date: 2026-03-30
description: Impara come formattare i numeri con separatore usando Aspose.Cells in
  C#. Include impostare un formato numerico personalizzato, aggiungere il separatore
  delle migliaia, formattare le cifre decimali e come formattare la cella.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: it
og_description: Formattare i numeri con separatore in C#. Questa guida mostra come
  impostare un formato numerico personalizzato, aggiungere il separatore delle migliaia,
  formattare le cifre decimali e come formattare una cella usando Aspose.Cells.
og_title: Formattare i numeri con separatore in C# – Tutorial Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formattare i numeri con separatore in C# – Guida completa ad Aspose.Cells
url: /it/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formattare i Numeri con Separatore in C# – Guida Completa ad Aspose.Cells

Hai mai avuto bisogno di **formattare numeri con separatore** in un foglio di calcolo ma non eri sicuro di quale chiamata API utilizzare? Non sei il solo—gli sviluppatori lottano costantemente con i separatori delle migliaia, le cifre decimali e i modelli personalizzati quando esportano dati.  

Buone notizie: Aspose.Cells lo rende un gioco da ragazzi. In questo tutorial vedremo un esempio reale che **imposta un formato numerico personalizzato**, **aggiunge un separatore delle migliaia**, **formatta le cifre decimali**, e mostra **come formattare la cella** per l'output come stringa. Alla fine avrai uno snippet pronto da eseguire che potrai inserire in qualsiasi progetto .NET.

## Cosa Copre Questa Guida

* Il pacchetto NuGet esatto di cui hai bisogno e come installarlo.  
* Codice passo‑passo che crea una cartella di lavoro, scrive un valore numerico e applica un formato personalizzato.  
* Perché `ExportTableOptions.ExportAsString` è il metodo consigliato per recuperare un valore formattato.  
* Problemi comuni—come dimenticare di abilitare `ExportAsString` o usare il mask di formato sbagliato.  
* Come modificare il mask di formato se ti servono un diverso numero di cifre decimali o uno stile di separatore differente.

Non sono necessari link a documentazione esterna; tutto ciò che ti serve è qui. Immergiamoci.

---

## Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| .NET 6.0 o successivo | Aspose.Cells 23.10+ target .NET Standard 2.0+, quindi .NET 6 è sicuro e attuale. |
| Visual Studio 2022 (o qualsiasi IDE C#) | Rende il debug e la gestione dei pacchetti senza problemi. |
| Pacchetto NuGet Aspose.Cells per .NET | Fornisce le classi `Workbook`, `Worksheet` e `ExportTableOptions` che utilizzeremo. |

Puoi installare il pacchetto tramite la Console di Gestione Pacchetti:

```powershell
Install-Package Aspose.Cells
```

È tutto—nessun DLL aggiuntivo, nessun interop COM, solo un singolo riferimento NuGet.

---

## Passo 1: Inizializzare una Nuova Cartella di Lavoro (Come Formattare una Cella)

La prima cosa che facciamo è creare una nuova istanza di `Workbook`. Pensala come un file Excel vuoto pronto a ricevere dati.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Perché è importante:** `Workbook` è il punto di ingresso per ogni operazione in Aspose.Cells. Prelevando il primo foglio di lavoro (`Worksheets[0]`) otteniamo una tela pulita senza dover nominare un foglio.

## Passo 2: Scrivere un Valore Numerico nella Cella di Destinazione

Successivamente, inseriamo un numero grezzo nella cella **A1**. Il valore stesso non è ancora formattato—è semplicemente un double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Consiglio professionale:** usa `PutValue` invece di `PutString` quando intendi applicare in seguito una formattazione numerica. Questo preserva il tipo di dato sottostante, consentendo calcoli compatibili con Excel.

## Passo 3: Impostare un Formato Numerico Personalizzato (Aggiungere Separatore delle Migliaia & Formattare le Cifre Decimali)

Ora arriva il cuore del tutorial: definire una maschera di formato che indica ad Aspose.Cells come visualizzare il numero. La maschera `#,##0.00` fa tre cose:

1. **`#,##0`** – aggiunge un separatore delle migliaia (virgola per impostazione predefinita).  
2. **`.00`** – forza esattamente due cifre decimali.  

Se ti servono un numero diverso di decimali, basta cambiare il numero di `0` dopo il punto decimale.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Perché usiamo `ExportAsString`**: per impostazione predefinita, `ExportString` restituisce il valore grezzo. Impostare `ExportAsString = true` costringe l'API ad applicare la maschera `NumberFormat` prima di convertire in testo. Questo è fondamentale quando ti serve la rappresentazione stringa esatta per report, payload JSON o visualizzazioni UI.

## Passo 4: Esportare il Testo Formattato (Come Formattare una Cella)

Con le opzioni pronte, chiamiamo `ExportString` sulla stessa cella. Il metodo rispetta la maschera appena definita e restituisce una stringa ben formattata.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Eseguendo il programma stampa **`12,345.68`** sulla console—esattamente il formato richiesto.

> **Caso limite:** se il numero di origine ha più di due cifre decimali, la maschera lo arrotonda. Se ti serve il troncamento invece dell'arrotondamento, dovrai pre‑processare il valore con `Math.Truncate` prima di chiamare `PutValue`.

## Passo 5: Regolare il Formato – Variazioni Comuni

### 5.1 Cambiare la Precisione Decimale

Vuoi tre cifre decimali? Basta sostituire la maschera:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Usare un Separatore delle Migliaia Differente

Alcune impostazioni locali preferiscono uno spazio o un punto. Puoi inserire il carattere direttamente:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Oppure affidarti alle impostazioni culturali della cartella di lavoro:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefisso o Suffisso (Valuta, Percentuale)

Aggiungi un simbolo di dollaro o di percentuale direttamente nella maschera:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Nota:** la maschera è sensibile al maiuscolo/minuscolo. `$` e `%` sono simboli letterali; non influenzano il valore numerico sottostante.

## Passo 6: Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il programma completo che puoi copiare in una nuova app console. Include tutti i passaggi, i commenti e la verifica dell'output finale.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Esegui il programma (`dotnet run` dal terminale o premi F5 in Visual Studio) e vedrai il numero formattato stampato esattamente come mostrato.

## Domande Frequenti (FAQ)

**D: Funziona con versioni più vecchie di Excel?**  
R: Sì. La maschera di formato segue la sintassi nativa dei numeri di Excel, quindi qualsiasi versione che riconosce `#,##0.00` renderizzerà la stessa stringa.

**D: E se devo formattare un intervallo di celle?**  
R: Itera sull'intervallo desiderato e applica lo stesso `ExportTableOptions` a ogni cella, oppure imposta la proprietà `Style.Custom` sull'intervallo e poi chiama `ExportString` su una singola cella.

**D: Posso esportare direttamente in CSV con questi formati applicati?**  
R: Assolutamente. Usa `Workbook.Save("output.csv", SaveFormat.CSV);` dopo aver impostato il formato su ogni cella. Aspose.Cells rispetta lo `Style` della cella quando genera il CSV.

## Conclusione

Abbiamo appena mostrato come **formattare numeri con separatore** in C# usando Aspose.Cells, coprendo tutto, da **impostare un formato numerico personalizzato** ad **aggiungere un separatore delle migliaia**, **formattare le cifre decimali**, e l'essenziale **come formattare una cella** per l'esportazione come stringa. Il codice è completamente autonomo, funziona con .NET 6+ e può essere adattato a qualsiasi impostazione locale o requisito di precisione.

Successivamente, potresti esplorare:

* Applicare la stessa tecnica a date e orari (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatizzare esportazioni di massa dove ogni colonna necessita di una maschera diversa.  
* Integrare le stringhe formattate in report PDF con Aspose.Words.

Prova queste, e diventerai rapidamente la persona di riferimento per la formattazione dei fogli di calcolo nel tuo team. Buon coding!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formatted number with separator displayed in Aspose.Cells output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}