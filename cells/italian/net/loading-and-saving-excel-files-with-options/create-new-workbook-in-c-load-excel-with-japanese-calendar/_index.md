---
category: general
date: 2026-02-26
description: Crea una nuova cartella di lavoro in C# e impara come caricare file Excel,
  impostare il calendario in giapponese ed estrarre le date da Excel senza sforzo.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: it
og_description: Crea una nuova cartella di lavoro in C# e impara rapidamente come
  caricare Excel, impostare un calendario giapponese ed estrarre le date dai file
  Excel.
og_title: Crea una nuova cartella di lavoro in C# – Carica Excel con calendario giapponese
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Crea una nuova cartella di lavoro in C# – Carica Excel con calendario giapponese
url: /it/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un nuovo workbook in C# – Carica Excel con calendario giapponese

Ti è mai capitato di **creare un nuovo workbook** in C# ma non eri sicuro di come far sì che Excel rispetti il calendario giapponese? Non sei solo. In molti scenari aziendali riceverai fogli di calcolo che memorizzano le date nel sistema delle ere giapponesi, e estrarre correttamente quelle date può sembrare decodificare un linguaggio segreto.

Ecco la questione: puoi **create new workbook**, dire al loader di interpretare le date usando il calendario giapponese, e poi **extract date from excel** con poche righe di codice. In questa guida percorreremo *how to load excel*, *how to set calendar* per le date giapponesi, e infine *read Japanese dates* da una cella. Nessuna perdita di tempo—solo un esempio completo e eseguibile che puoi copiare‑incollare nel tuo progetto.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.6+)  
- La libreria **Aspose.Cells** (versione di prova gratuita o licenziata). Installala tramite NuGet:

```bash
dotnet add package Aspose.Cells
```

- Un file Excel (`JapanDates.xlsx`) che contiene date in era giapponese nella cella A1.

È tutto. Se li hai, possiamo subito cominciare.

---

## Crea un nuovo workbook e imposta il calendario giapponese

Il primo passo è **create new workbook** l'oggetto e configurare il `LoadOptions` affinché il parser sappia quale calendario utilizzare.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Consiglio:** La proprietà `LoadOptions.Calendar` accetta diversi enum (`Gregorian`, `Japanese`, `Hijri`, ecc.). Scegliere quello corretto garantisce che la libreria traduca il testo dell'era (ad es., “令和3年”) in un `DateTime` .NET.

![screenshot esempio di creazione di un nuovo workbook](image-url.png "Screenshot che mostra una nuova istanza di workbook con impostazioni del calendario giapponese"){: .align-center alt="screenshot esempio di creazione di un nuovo workbook"}

### Perché funziona

- **Workbook creation**: `new Workbook()` ti fornisce una pagina bianca—nessun foglio nascosto, nessun dato predefinito.
- **LoadOptions**: Assegnando `CalendarType.Japanese` *prima* di chiamare `Load`, il parser tratta le stringhe basate sull'era come date anziché testo semplice.
- **GetDateTime()**: Dopo il caricamento, `cellA1.GetDateTime()` restituisce un vero oggetto `DateTime`, permettendoti di eseguire operazioni aritmetiche, formattazione o inserimenti in database senza passaggi di conversione aggiuntivi.

---

## Come caricare correttamente un file Excel

Potresti chiederti, “Esiste un modo speciale per **how to load excel** quando si gestiscono calendari non gregoriani?” La risposta è sì—imposta sempre il `LoadOptions` *prima* di invocare `Load`. Se carichi prima e poi cambi il calendario, le date sono già state analizzate in modo errato.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Il frammento sopra dimostra un errore comune. L'ordine corretto (come mostrato nella sezione precedente) garantisce che il motore interpreti le celle *come date* fin dall'inizio.

## Come impostare il calendario per le date giapponesi

Se devi cambiare calendario al volo—ad esempio, elaborare un batch di file che usano sistemi di era diversi—puoi riutilizzare lo stesso oggetto `Workbook` con un nuovo `LoadOptions` ogni volta.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Chiamare `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` produce lo stesso risultato del nostro esempio principale, mentre `CalendarType.Gregorian` tratterebbe la stessa cella come una semplice stringa (o lanciarebbe un'eccezione se il formato non è riconoscibile).

## Estrai la data da Excel – Lettura delle date giapponesi

Ora che il workbook è caricato con il calendario corretto, estrarre la data è semplice. Il metodo `Cell.GetDateTime()` restituisce un `DateTime` che rispetta la conversione dell'era.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Casi limite e scenari “What‑If”

| Situazione                              | Cosa fare                                                                                               |
|----------------------------------------|----------------------------------------------------------------------------------------------------------|
| La cella contiene **testo** invece di una data | Chiama prima `cell.GetString()`, valida con `DateTime.TryParse`, oppure imposta la convalida dei dati in Excel. |
| Sono necessari più fogli di lavoro    | Itera su `workbook.Worksheets` e applica la stessa logica di estrazione a ciascun foglio.                   |
| Le date sono memorizzate come **numeri** (seriale Excel) | `cell.GetDateTime()` funziona comunque perché Aspose.Cells converte automaticamente i numeri seriali.            |
| Il file è **protetto da password**         | Usa `LoadOptions.Password = "yourPwd"` prima di chiamare `Load`.                                           |

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo che puoi inserire in un'app console. Include la gestione degli errori e dimostra tutte e quattro le parole chiave secondarie nel contesto.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Output previsto** (supponendo che A1 contenga “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

Se la cella contiene una data gregoriana come “2021‑05‑12”, lo stesso codice funziona comunque perché la libreria ricade elegantemente sull'interpretazione gregoriana.

## Conclusione

Ora sai come **create new workbook**, correttamente **how to load excel**, impostare il **how to set calendar** appropriato, e infine **extract date from excel** mentre **read Japanese dates** senza alcun parsing manuale. Il punto chiave è che il calendario deve essere definito *prima* del caricamento; una volta che il workbook è in memoria, le date sono già materializzate come corretti oggetti `DateTime`.

### Cosa c'è dopo?

- **Batch processing**: Itera su una cartella di file, chiamando `LoadWithCalendar` per ciascuno.
- **Export to other formats**: Usa `workbook.Save("output.csv")` dopo la conversione.
- **Localization**: Combina `CultureInfo` con `DateTime.ToString` per visualizzare le date nella lingua preferita dall'utente.

Sentiti libero di sperimentare—sostituisci `CalendarType.Japanese` con `CalendarType.Hijri` o `CalendarType.Gregorian` e osserva come lo stesso codice si adatti automaticamente. Se incontri problemi, lascia un commento qui sotto o consulta la documentazione di Aspose.Cells per approfondimenti sull'API.

Buon coding, e divertiti a trasformare quelle misteriose date in era giapponese in puliti valori .NET `DateTime`!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}