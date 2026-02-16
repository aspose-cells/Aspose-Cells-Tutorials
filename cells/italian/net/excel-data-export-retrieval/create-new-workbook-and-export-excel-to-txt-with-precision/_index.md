---
category: general
date: 2026-02-15
description: Crea una nuova cartella di lavoro ed esporta Excel in TXT impostando
  la precisione numerica. Impara a impostare le cifre significative e a limitarle
  in C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: it
og_description: Crea una nuova cartella di lavoro ed esporta Excel in TXT, impostando
  le cifre significative per la precisione numerica. Una guida passo‑passo in C#.
og_title: Crea nuovo foglio di lavoro – Esporta Excel in TXT con precisione
tags:
- C#
- Aspose.Cells
- Excel automation
title: Crea nuova cartella di lavoro ed esporta Excel in TXT con precisione
url: /it/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Nuova Cartella di Lavoro – Esporta Excel in TXT con Formattazione Numerica Precisa

Ti sei mai chiesto come **create new workbook** oggetti in C# e scaricarli immediatamente in un file di testo semplice? Non sei l'unico. In molti scenari di data‑pipeline dobbiamo **export Excel to TXT** mantenendo i numeri leggibili, il che significa limitare il numero di cifre che appaiono dopo il punto decimale.  

In questo tutorial percorreremo l'intero processo: dalla creazione di una nuova cartella di lavoro, alla configurazione dell'esportazione in modo che **sets significant digits** (aka limiting significant digits), e infine scrivere il file su disco. Alla fine avrai uno snippet pronto all'uso che rispetta i tuoi requisiti di **numeric precision** — nessuna libreria extra, nessuna magia.

> **Suggerimento:** Se stai già usando Aspose.Cells, le classi mostrate di seguito fanno parte di quella libreria. Se sei su una piattaforma diversa, i concetti sono comunque validi; basta sostituire le chiamate API.

---

## Di cosa avrai bisogno

- .NET 6+ (il codice si compila su .NET Core e .NET Framework allo stesso modo)  
- Aspose.Cells per .NET (versione di prova gratuita o licenza) – installa via NuGet: `dotnet add package Aspose.Cells`  
- Qualsiasi IDE tu preferisca (Visual Studio, Rider, VS Code)  

È tutto. Nessun file di configurazione extra, nessun passaggio nascosto.

---

## Passo 1: Crea una Nuova Cartella di Lavoro

La prima cosa da fare è **create new workbook**. Pensa alla classe `Workbook` come a un file Excel vuoto in attesa di fogli, celle e dati.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Perché è importante:** Iniziando con una cartella di lavoro pulita eviti qualsiasi formattazione nascosta che potrebbe interferire con le impostazioni di precisione in seguito.

---

## Passo 2: Configura le Opzioni di Salvataggio Testo – Imposta le Cifre Significative

Ora indichiamo ad Aspose.Cells quante **significant digits** vogliamo quando scriviamo in un file `.txt`. La classe `TxtSaveOptions` espone una proprietà `SignificantDigits` che fa esattamente questo.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Spiegazione:** `SignificantDigits = 5` significa che l'esportatore manterrà le cinque cifre più importanti di qualsiasi numero, indipendentemente da dove si trovi il punto decimale. È un modo pratico per **set numeric precision** senza formattare manualmente ogni cella.

---

## Passo 3: Salva la Cartella di Lavoro come File di Testo

Con la cartella di lavoro e le opzioni pronte, finalmente **export Excel to txt**. Il metodo `Save` accetta il percorso del file e l'oggetto opzioni che abbiamo appena configurato.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Eseguendo il programma si genera un file che appare così:

```
12346
0.00012346
3.1416
```

Nota come ogni numero rispetti la regola **limit significant digits** che abbiamo impostato in precedenza.

---

## Passo 4: Verifica il Risultato (Opzionale ma Consigliato)

È facile aprire il `numbers.txt` generato in qualsiasi editor, ma potresti voler automatizzare il passaggio di verifica, soprattutto nelle pipeline CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Se la console mostra le tre righe sopra, hai impostato con successo **set significant digits** e l'esportazione funziona come previsto.

---

## Problemi Comuni & Come Evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| I numeri appaiono con troppe cifre decimali | `SignificantDigits` è stato lasciato al valore predefinito (0) | Imposta esplicitamente `SignificantDigits` al conteggio desiderato |
| Viene creato un file vuoto | La cartella di lavoro non ha ricevuto dati prima del salvataggio | Popola le celle **prima** di chiamare `Save` |
| Il percorso del file genera `UnauthorizedAccessException` | Tentativo di scrivere in una cartella protetta | Usa una cartella per cui hai permessi di scrittura (es., `C:\Temp` o `%USERPROFILE%\Documents`) |
| La precisione sembra errata per numeri molto piccoli | Il conteggio delle cifre significative include gli zeri iniziali dopo il decimale | Ricorda che “significant” ignora gli zeri iniziali; 0.000123456 con 5 cifre diventa `0.00012346` |

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il programma completo e autonomo. Incollalo in un nuovo progetto console e premi **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Output console previsto**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

E il file `numbers.txt` conterrà le tre righe mostrate sopra.

---

## Prossimi Passi: Oltre le Basi

- **Export other formats** – Aspose.Cells supporta anche CSV, HTML e PDF. Sostituisci `TxtSaveOptions` con `CsvSaveOptions` o `PdfSaveOptions` secondo necessità.  
- **Dynamic precision** – puoi calcolare `SignificantDigits` a runtime basandoti su input dell'utente o file di configurazione.  
- **Multiple worksheets** – itera su `workbook.Worksheets` ed esporta ciascuna in un proprio file `.txt`.  
- **Localization** – controlla il separatore decimale (`.` vs `,`) tramite `CultureInfo` se devi corrispondere alle impostazioni regionali.  

---

## Riepilogo

Abbiamo preso una nuova istanza **create new workbook**, l'abbiamo riempita di dati e dimostrato come **export Excel to TXT** mentre **setting significant digits** per limitare la precisione dell'output. L'esempio completo funziona subito, e la spiegazione ha coperto il *perché* di ogni riga così potrai adattarlo ai tuoi progetti.

Sentiti libero di sperimentare—cambia il valore `SignificantDigits`, aggiungi più fogli o cambia il formato di output. Se incontri problemi, consulta la documentazione di Aspose.Cells o lascia un commento qui sotto. Buon coding!

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}