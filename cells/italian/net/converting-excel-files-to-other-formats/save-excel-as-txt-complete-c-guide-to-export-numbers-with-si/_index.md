---
category: general
date: 2026-02-21
description: Salva Excel come txt con controllo preciso delle cifre significative.
  Esporta Excel in txt con C# e imposta facilmente le cifre significative.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: it
og_description: Salva Excel come txt rapidamente. Scopri come esportare Excel in txt,
  impostare le cifre significative e controllare l'output di testo usando C#.
og_title: Salva Excel come txt – Esporta numeri con cifre significative in C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Salva Excel come txt – Guida completa C# per esportare numeri con cifre significative
url: /it/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

placeholders unchanged.

Proceed.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salva Excel come txt – Guida completa C# per esportare numeri con cifre significative

Hai mai dovuto **salvare Excel come txt** ma temuto che i numeri perdessero la precisione? Non sei solo. Molti sviluppatori si trovano in difficoltà quando provano a esportare Excel in txt e finiscono con troppe cifre decimali o con un risultato arrotondato in modo impreciso.  

In questo tutorial ti mostreremo un metodo semplice per **esportare Excel in txt** impostando le **cifre significative** in modo che l'output sia esattamente come lo desideri. Alla fine avrai a disposizione uno snippet C# pronto all'uso che salva una cartella di lavoro come testo, esporta numeri in txt e ti dà il pieno controllo sul formato numerico.

## Cosa imparerai

- Come creare una nuova cartella di lavoro e scrivere dati numerici.  
- Il modo corretto per **impostare le cifre significative** usando `TxtSaveOptions`.  
- Come **salvare la cartella di lavoro come testo** e verificare il risultato.  
- Gestione dei casi limite (numeri grandi, valori negativi, problemi di locale).  
- Suggerimenti rapidi per affinare ulteriormente l'output (cambio delimitatore, codifica).

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.6+).  
- Il pacchetto NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).  
- Una conoscenza di base della sintassi C#—non è necessario conoscere a fondo l'interoperabilità con Excel.

> **Pro tip:** Se usi Visual Studio, abilita i *nullable reference types* (`<Nullable>enable</Nullable>`) per intercettare potenziali bug di null in anticipo.

---

## Passo 1: Inizializzare la cartella di lavoro e scrivere un numero

Per prima cosa, ci serve un oggetto workbook. Pensalo come la rappresentazione in memoria di un file Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Perché è importante:**  
Creare la cartella di lavoro programmaticamente evita l'overhead dell'interoperabilità COM, e `PutValue` rileva automaticamente il tipo di dato, garantendo che la cella sia trattata come numero—not stringa.

---

## Passo 2: Configurare TxtSaveOptions per controllare le cifre significative

La classe `TxtSaveOptions` è dove avviene la magia. Impostando `SignificantDigits`, dici ad Aspose.Cells quante cifre significative mantenere quando il file viene scritto.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Perché dovresti impostarla:**  
Quando **esporti numeri in txt**, spesso è necessario una rappresentazione concisa (ad esempio per sistemi di reporting che accettano solo una certa precisione). La proprietà `SignificantDigits` garantisce arrotondamenti coerenti indipendentemente dalla lunghezza originale del numero.

---

## Passo 3: Salvare la cartella di lavoro come file di testo

Ora scriviamo la cartella di lavoro su disco usando le opzioni appena definite.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Ciò che vedrai:**  
Apri `Numbers.txt` e otterrai una singola riga:

```
12350
```

Il valore originale `12345.6789` è stato arrotondato a **quattro cifre significative**, esattamente come richiesto.

---

## Passo 4: Verificare l'output (opzionale ma consigliato)

I test automatici sono una buona abitudine. Ecco un rapido controllo da eseguire subito dopo il salvataggio:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Eseguendo questo blocco otterrai un segno di spunta verde se tutto è allineato, dandoti la certezza che l'operazione **save excel as txt** abbia funzionato come previsto.

---

## Variazioni comuni e casi limite

### Esportare più celle o intervalli

Se devi **esportare excel to txt** per un intero intervallo, basta riempire più celle prima di salvare:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Le stesse `TxtSaveOptions` applicheranno la regola delle 4 cifre a ciascun valore, producendo:

```
12350
0.0001235
-98800
```

### Cambiare il delimitatore

Alcuni sistemi a valle richiedono valori separati da tabulazioni. Modifica il delimitatore così:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Ora ogni cella in una riga appare separata da un tab.

### Gestire separatori decimali specifici del locale

Se il tuo pubblico usa la virgola per i decimali, imposta la cultura:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

L'output rispetterà il locale, trasformando `12350` in `12 350` (spazio come separatore delle migliaia in francese).

---

## Esempio completo (pronto per il copia‑incolla)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Contenuto atteso di `Numbers.txt` (delimitatore predefinito, 4 cifre significative):**

```
12350	0.0001235	-98800
```

Il tab (`\t`) appare perché abbiamo lasciato il delimitatore al valore predefinito (tab) nell'esempio; cambialo in virgola se preferisci il CSV.

---

## Conclusione

Ora sai esattamente **come salvare Excel come txt** controllando il numero di cifre significative. I passaggi—creare una cartella di lavoro, impostare `TxtSaveOptions.SignificantDigits` e salvare—sono tutto ciò che ti serve per **export excel to txt** in modo affidabile.  

Da qui puoi:

- **Export numbers to txt** per insiemi di dati più grandi.  
- Regolare delimitatori, codifica o impostazioni culturali per adattarli a qualsiasi sistema a valle.  
- Combinare questo approccio con altre funzionalità di Aspose.Cells (stili, formule) prima dell'esportazione.

Provalo, modifica `SignificantDigits` a 2 o 6 e osserva come cambia l'output. La flessibilità di **save workbook as text** lo rende uno strumento utile in qualsiasi pipeline di scambio dati.

---

### Argomenti correlati da esplorare

- **Export Excel to CSV** con ordinamento personalizzato delle colonne.  
- **Read txt files back into a workbook** (`Workbook.Load` con `LoadOptions`).  
- **Batch processing** di più fogli di lavoro e consolidamento in un unico file txt.  
- **Performance tuning** per esportazioni su larga scala (streaming vs. in‑memory).

Sentiti libero di lasciare un commento se incontri difficoltà, o di condividere come hai personalizzato l'esportazione per i tuoi progetti. Buon coding!  

---  

*Immagine: uno screenshot del file `Numbers.txt` generato che mostra i valori arrotondati.*  
*Testo alternativo: “File Numbers.txt che visualizza 12350, 0,0001235 e -98800 dopo aver salvato Excel come txt con 4 cifre significative.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}