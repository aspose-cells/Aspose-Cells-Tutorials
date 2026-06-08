---
category: general
date: 2026-06-08
description: Analizza la data dell’era giapponese in C# usando Aspose.Cells. Scopri
  come CultureInfo ja-JP e il formato dell’era giapponese consentono una conversione
  accurata delle date in Excel.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: it
og_description: Analizza rapidamente le date dell'era giapponese in C#. Questo tutorial
  mostra come CultureInfo ja-JP e Aspose.Cells trasformano le stringhe dell'era in
  oggetti DateTime corretti.
og_title: Analizza la data dell'era giapponese in C# – Guida Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Analizza la data dell'era giapponese in C# con Aspose.Cells – Guida completa
url: /it/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizza le date dell'era giapponese in C# con Aspose.Cells – Guida completa

Hai mai dovuto **parse japanese era date** direttamente da un foglio Excel? Forse stai estraendo dati da un sistema legacy che utilizza ancora “令和3年5月12日” e desideri un `DateTime` pulito per generare report. In questo tutorial ti guideremo passo passo attraverso un esempio completo, pronto all'uso, che trasforma quelle stringhe formattate per l'era in date C# corrette—senza indovinare.

Useremo **Aspose.Cells**, la potente libreria .NET per la manipolazione di Excel, insieme all'impostazione **CultureInfo ja-JP** che sa leggere le ere giapponesi. Alla fine avrai uno snippet riutilizzabile che gestisce “令和”, “平成” e anche ere più vecchie senza alcuno sforzo.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.6+)
- Aspose.Cells per .NET (puoi scaricare il pacchetto di prova gratuito NuGet: `Install-Package Aspose.Cells`)
- Conoscenza di base di C#—nulla di complicato, basta un'app console
- Un IDE a tua scelta (Visual Studio, Rider, VS Code, ecc.)

Tutto qui. Nessun servizio aggiuntivo, nessun parser di terze parti obscuro.

## Passo 1: Configura il progetto e aggiungi Aspose.Cells

Per prima cosa, crea un nuovo progetto console:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Ora apri **Program.cs** e aggiungi gli spazi dei nomi richiesti:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Se stai usando Visual Studio, l'IDE suggerirà di aggiungere le istruzioni `using` automaticamente dopo aver digitato i nomi delle classi.

## Passo 2: Crea un Workbook e applica la cultura giapponese

La chiave per **parse japanese era date** correttamente è indicare ad Aspose.Cells quale cultura utilizzare. Impostare `CultureInfo` su `ja-JP` attiva l'analisi consapevole delle ere.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Perché è importante? Il calendario giapponese ha più ere (ad es., *Reiwa* (令和), *Heisei* (平成)). L'oggetto `CultureInfo` contiene un `JapaneseCalendar` che conosce le date di inizio di ogni era, così qualsiasi stringa che segue il formato dell'era giapponese può essere interpretata correttamente.

## Passo 3: Scrivi una stringa di data dell'era giapponese in una cella

Inseriamo una data di esempio dell'era nella cella **A1**. Sentiti libero di modificare la stringa per testare diverse ere.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Se preferisci lavorare con un workbook esistente, puoi caricarlo con `new Workbook("path/to/file.xlsx")` e saltare il passaggio di creazione.

## Passo 4: Recupera il valore come oggetto C# DateTime

Ora avviene la magia. Chiamando `GetDateTime()`, Aspose.Cells legge la cella usando il `CultureInfo` impostato in precedenza e restituisce un `DateTime` corretto.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Output previsto**

```
Parsed DateTime: 2021-05-12
```

Questo è l'intero flusso di **parse japanese era date**—quattro linee di codice concise.

## Passo 5: Gestione dei casi limite e delle ere alternative

I dati del mondo reale non sono sempre puliti. Ecco alcuni scenari che potresti incontrare e come gestirli.

### 5.1 Stringhe non valide o vuote

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Ere più vecchie (Showa, Taisho)

Lo stesso `CultureInfo ja-JP` funziona automaticamente per le ere più vecchie:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Utilizzare `DateTime.ParseExact` per validazione rigorosa

Se vuoi imporre il pattern esatto dell'era giapponese, usa una stringa di formato personalizzata:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Questo approccio genera una `FormatException` quando la stringa devia, il che può essere utile per controlli di qualità dei dati.

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare‑incollare in **Program.cs** ed eseguire.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Eseguilo con `dotnet run` e dovresti vedere:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**parse japanese era date** completato, e hai un modello per qualsiasi era potresti incontrare.

![Flusso di lavoro per analizzare le date dell'era giapponese – mostra la creazione del workbook, l'impostazione della cultura, la scrittura nella cella e la chiamata GetDateTime](parse-japanese-era-date.png "Diagramma che illustra come analizzare le date dell'era giapponese usando Aspose.Cells e CultureInfo ja-JP")

## Domande frequenti

- **Questo funziona con file .xlsx che contengono già date dell'era?**  
  Sì. Finché il `Settings.CultureInfo` del workbook è impostato su `ja-JP` *prima* di chiamare `GetDateTime()`, Aspose.Cells interpreterà correttamente le stringhe esistenti.

- **E i fusi orari?**  
  L'analisi restituisce un `DateTime` con `Kind = Unspecified`. Se ti serve UTC o l'ora locale, applica `DateTime.SpecifyKind` o converti dopo l'analisi.

- **Posso analizzare più celle contemporaneamente?**  
  Assolutamente. Itera sull'intervallo desiderato e chiama `GetDateTime()` su ogni cella—ricorda solo di gestire le eccezioni per voci malformate.

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **parse japanese era date** in C# usando Aspose.Cells e il `CultureInfo ja-JP` integrato. Dalla configurazione del workbook, alla scrittura di stringhe formattate per l'era, al recupero di un `DateTime` pulito, fino alla gestione dei casi limite come ere più vecchie e validazione rigorosa—questa guida ti offre una soluzione pronta per la produzione.

Successivamente, potresti esplorare **Excel date conversion** per date seriali numeriche, o approfondire **C# DateTime parsing** con calendari personalizzati per altre località. Lo stesso schema funziona per il calendario buddista tailandese, il calendario ebraico e altro ancora—basta sostituire il `CultureInfo`.

Hai un caso particolare su cui stai lavorando? Lascia un commento e risolviamo insieme. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come implementare la convalida delle date in .NET usando Aspose.Cells: Guida completa](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Modifica il sistema di data di Excel a 1904 usando Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Converti efficientemente Excel in PDF con formati data personalizzati usando Aspose.Cells per Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}