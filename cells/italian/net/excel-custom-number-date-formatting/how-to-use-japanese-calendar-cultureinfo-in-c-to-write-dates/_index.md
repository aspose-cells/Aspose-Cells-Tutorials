---
category: general
date: 2026-10-26
description: Scopri come utilizzare il CultureInfo del calendario giapponese in C#
  per analizzare le date di era e inserirle in un foglio di lavoro Excel con NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: it
lastmod: 2026-10-26
og_description: Usa CultureInfo del calendario giapponese in C# per analizzare le
  date dell'era Reiwa e scriverle in un foglio di lavoro Excel. Codice completo e
  eseguibile con spiegazioni.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Utilizzare CultureInfo del calendario giapponese in C# – esempio completo
  di Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Come utilizzare CultureInfo del calendario giapponese in C# per scrivere le
  date in Excel
url: /it/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare CultureInfo del calendario giapponese in C# per scrivere date in Excel

Se hai bisogno di **usare CultureInfo del calendario giapponese** mentre lavori con le date in C#, questa guida ti mostra esattamente come. Imparerai a analizzare una stringa di data che contiene un nome di era giapponese (ad esempio, *Reiwa 2/5/1*) e poi a scrivere il `DateTime` risultante nella prima cella di un foglio di lavoro Excel usando la libreria NPOI.

Analizzare date basate su era senza il corretto `CultureInfo` porta a `FormatException` o a valori di mese/giorno errati. Configurando `CultureInfo` sul calendario giapponese, garantisci che il runtime .NET interpreti correttamente l'era e che il valore che memorizzi in Excel corrisponda alla notazione giapponese originale.

In questo tutorial imparerai:

* Creare un oggetto `CultureInfo` che utilizzi il calendario giapponese.
* Analizzare una stringa di data dell'era giapponese con `DateTime.Parse`.
* Inserire il `DateTime` analizzato in una cella di un foglio di lavoro NPOI.
* Visualizzare il programma completo, eseguibile, e l'output previsto.

> **Prerequisiti** – .NET 6.0+ (o .NET Core 3.1+), il pacchetto NuGet **NPOI**, e una conoscenza di base di C# e della gestione dei file Excel.

---

## Cosa ti servirà

| Voce | Motivo |
|------|--------|
| **.NET SDK** (6.0 o successivo) | Fornisce il runtime e le librerie per `CultureInfo`. |
| **NPOI** (pacchetto NuGet `NPOI`) | Consente di creare e manipolare file Excel senza Office installato. |
| **Visual Studio Code**, **Visual Studio**, o qualsiasi IDE C# | Per compilare ed eseguire l'esempio. |
| **Stringa di data dell'era giapponese** (es., `"Reiwa 2/5/1"`) | Dimostra l'uso del calendario giapponese. |

---

## Passo 1: Installa NPOI

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package NPOI --version 2.6.1
```

Il pacchetto fornisce i tipi `IWorkbook`, `ISheet` e `ICell` utilizzati più avanti.

---

## Passo 2: Crea un CultureInfo che utilizzi il calendario giapponese

Il calendario giapponese è un calendario basato su era. Devi richiedere la variante *Japanese* della locale `ja-JP` e impostare esplicitamente il calendario su `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Perché è importante** – La cultura predefinita `ja-JP` utilizza il calendario gregoriano. Riassegnare la proprietà `Calendar` garantisce che i nomi di era come *Reiwa* siano riconosciuti durante l'analisi.

---

## Passo 3: Analizza una stringa di data dell'era giapponese

Ora che il `CultureInfo` è configurato, puoi analizzare in modo sicuro una stringa che contiene un nome di era.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Il metodo `Parse` interpreta *Reiwa 2* come l'anno gregoriano 2020, mese 5, giorno 1.

### Caso limite: gestione di epoche non valide

Se un utente fornisce un'era non supportata (ad esempio, `"Heisei 31/4/30"` dopo la fine dell'era Heisei), `DateTime.Parse` genera una `FormatException`. Avvolgi la chiamata in un blocco try‑catch per fornire un messaggio di errore amichevole:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Passo 4: Scrivi il `DateTime` analizzato in un foglio di lavoro Excel

Con l'oggetto `DateTime` pronto, puoi memorizzarlo in una cella Excel. NPOI formatta automaticamente i valori `DateTime` come date Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Risultato** – Aprendo *JapaneseEraDate.xlsx* si vede la data **2020‑05‑01** nella cella A1.

### Perché usare NPOI?

*Funziona su qualsiasi piattaforma* (Windows, Linux, macOS) e **non** richiede Microsoft Office. Questo rende la soluzione adatta a pipeline CI, container Docker o elaborazione lato server.

---

## Passo 5: Programma completo e eseguibile

Mettendo tutto insieme, ecco un'applicazione console completa che dimostra l'intero flusso:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Come eseguire**

```bash
dotnet run
```

Dopo l'esecuzione, troverai `JapaneseEraDate.xlsx` nella cartella del progetto con la data correttamente analizzata.

---

## Errori comuni e consigli di best‑practice

| Problema | Correzione / Raccomandazione |
|----------|------------------------------|
| Dimenticare di impostare `japaneseCulture.DateTimeFormat.Calendar` | Assegna sempre un'istanza di `JapaneseCalendar`; altrimenti il nome dell'era non viene riconosciuto. |
| Usare `DateTime.TryParse` senza il `CultureInfo` personalizzato | Passa lo stesso `japaneseCulture` a `TryParse` per mantenere un comportamento coerente. |
| Aspettarsi che Excel mostri il nome dell'era | I formati data integrati di Excel sono solo gregoriani. Se hai bisogno di visualizzare l'era, memorizza la stringa originale in una colonna separata o crea un formato testo personalizzato. |
| Non rilasciare il `FileStream` | Usa un blocco `using` (come mostrato) per garantire che il handle del file venga rilasciato tempestivamente. |
| Mescolare oggetti `CultureInfo` tra thread | `CultureInfo` è thread‑safe per operazioni di sola lettura, ma evita di modificare la sua proprietà `Calendar` dopo la configurazione iniziale. |

---

## Conclusione

Ora sai come **usare CultureInfo del calendario giapponese** in C# per analizzare accuratamente le date dell'era giapponese e scrivere il `DateTime` risultante in un foglio di lavoro Excel con NPOI. L'esempio completo copre la configurazione, l'analisi, la gestione degli errori e l'output Excel, fornendoti una solida base per qualsiasi scenario di reporting internazionalizzato o di scambio dati.

Successivamente, potresti esplorare:

* *Formattare le date con testo personalizzato* per mantenere il nome dell'era all'interno di Excel.  
* *Leggere le date da Excel* usando `cell.DateCellValue` rispettando il calendario giapponese.  
* *Applicare la stessa tecnica* per altri calendari basati su era (ad esempio, il calendario buddista tailandese) sostituendo `JapaneseCalendar` con la sottoclasse `Calendar` appropriata.  

Sentiti libero di sperimentare con diverse stringhe di era, set di dati più grandi, o di integrare questa logica in API ASP.NET Core che generano report Excel al volo. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea cartella di lavoro Excel con date del calendario giapponese – Guida completa](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Analizza date dell'era giapponese in Excel – Guida completa per sviluppatori C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Come creare una cartella di lavoro Excel e analizzare date giapponesi in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}