---
category: general
date: 2026-03-29
description: Come analizzare le date giapponesi in C# usando DateTimeParser e CultureInfo.
  Impara l'analisi delle date dell'era giapponese, consigli per l'analisi delle date
  in C# e gestisci i casi limite.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: it
og_description: Come analizzare le date giapponesi in C# usando DateTimeParser e CultureInfo.
  Ottieni una soluzione passo‑passo per l'analisi delle date dell'era giapponese.
og_title: Come analizzare le date giapponesi in C# – Guida completa
tags:
- C#
- .NET
- DateTime
- Localization
title: Come analizzare le date giapponesi in C# – Guida completa
url: /it/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Analizzare le Date Giapponesi in C# – Guida Completa

Ti sei mai chiesto **come analizzare le date giapponesi** all'interno di un'applicazione .NET? Forse stai lavorando su un sistema finanziario che riceve date come “令和3年5月12日” da un cliente giapponese, e hai bisogno di convertirle in un normale `DateTime`. Non sei solo—i problemi di localizzazione compaiono continuamente.  

La buona notizia è che, con le impostazioni culturali corrette e una piccola classe di supporto, **come analizzare le date giapponesi** diventa un gioco da ragazzi. In questo tutorial percorreremo ogni passaggio, dalla configurazione di `CultureInfo` per *ja‑JP* alla gestione dei casi limite come le epoche storiche. Alla fine avrai un `DateTimeParser` riutilizzabile che funziona per qualsiasi data della moderna era giapponese.

> **Cosa otterrai** – un esempio completo e eseguibile, spiegazioni del *perché* ogni riga è importante, consigli per le epoche più vecchie e una rapida checklist così non dimenticherai mai un passaggio.

## Prerequisiti

- .NET 6+ (o .NET Framework 4.7 + – l'API che usiamo non è cambiata)
- Conoscenza di base di C# (dovresti sentirti a tuo agio con le istruzioni `using` e `Console.WriteLine`)
- Nessun pacchetto NuGet esterno—tutto risiede in `System` e `System.Globalization`

Se hai già un progetto aperto, ottimo—basta incollare il codice. Altrimenti, crea una nuova app console con `dotnet new console -n JapaneseDateDemo` e sei pronto.

## Passo 1: Comprendere il Sistema di Calendario Giapponese

Prima di immergerci nel codice, rispondiamo al “perché”. Le date giapponesi sono espresse in formato **era** (元号), dove il numero dell'anno si resetta quando un nuovo imperatore sale al trono. Per esempio:

- **令和** (Reiwa) è iniziata il 01‑05‑2019.
- **平成** (Heisei) ha coperto il periodo 1989‑2019.
- **昭和** (Showa) è durata dal 1926‑1989.

La classe `JapaneseCalendar` di .NET conosce già queste ere, ma devi indicare al parser quale cultura utilizzare. È qui che entra in gioco **cultureinfo ja‑jp**—collega il calendario alla locale giapponese.

## Passo 2: Creare un Wrapper Piccolo – `DateTimeParser`

Invece di spargere `CultureInfo` ovunque, incapsuleremo la logica in un piccolo helper. Questo rende il codice riutilizzabile e mantiene pulita il resto dell'applicazione.

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**Perché questo helper?**  
- **Responsabilità singola** – tutto il parsing specifico della locale vive in un unico posto.  
- **Gestione degli errori** – forniamo messaggi chiari quando il formato è errato.  
- **Pronto per il futuro** – se in seguito devi supportare le ere più vecchie *Taisho* o *Meiji*, basta regolare il pattern o aggiungere un fallback.

## Passo 3: Collegare Tutto in `Program.cs`

Ora useremo il wrapper per analizzare effettivamente una stringa di esempio. Nota come otteniamo la cultura giapponese con `CultureInfo.GetCultureInfo("ja-JP")`. Questo soddisfa il requisito **cultureinfo ja‑jp** e garantisce che il `JapaneseCalendar` sia attivo.

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Quando esegui `dotnet run` vedrai:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Questo è il nocciolo di **come analizzare le date giapponesi**. Semplice, vero?

## Passo 4: Gestire i Casi Limite & le Ere più Vecchie

### 4.1 Date Storiche Prima del 1912

Il `JapaneseCalendar` integrato supporta solo le ere moderne (da Meiji in poi). Se devi analizzare date dei periodi *Taisho* (1912‑1926) o *Meiji* (1868‑1912), lo stesso pattern funziona—basta assicurarsi che la stringa includa il nome corretto dell'era (“大正”, “明治”). Il parser restituirà comunque un corretto `DateTime` gregoriano.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Era Mancante (Input Ambiguo)

Se un cliente invia “2021年5月12日” senza era, il parser fallirà perché il pattern si aspetta un'era (`ggg`). Hai due opzioni:

1. **Assumere il Gregoriano** – ricorrere a `CultureInfo.InvariantCulture` e a un pattern diverso.
2. **Rifiutare l'input** – informare il chiamante che l'era è obbligatoria.

Ecco una rapida adattazione:

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 Nota sulla Sicurezza dei Thread

Gli oggetti `CultureInfo` sono di sola lettura dopo la creazione, quindi puoi riutilizzare in sicurezza la stessa istanza tra i thread. Il `DateTimeParser` stesso non mantiene stato mutabile, rendendolo **thread‑safe** – un fatto utile per API web ad alto rendimento.

## Passo 5: Mettere Tutto Insieme – Un Esempio Pronto da Copiare

Di seguito trovi il codice completo che puoi inserire in un nuovo progetto console. Nessun pacchetto esterno, nessuna dipendenza nascosta.

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}