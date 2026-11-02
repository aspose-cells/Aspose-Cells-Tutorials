---
category: general
date: 2026-06-27
description: Impara a analizzare le date dell'era giapponese in C# e poi formattare
  datetime yyyy‑mm‑dd per l'output ISO. Codice passo‑passo, casi limite e consigli.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: it
og_description: Analizza la data dell’era giapponese in C# e formatta la data/ora
  yyyy-mm-dd senza sforzo. Esempio completo con spiegazioni e insidie.
og_title: Analizza la data dell'era giapponese in C# – Guida completa alla programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Analizza la data dell'era giapponese in C# – Guida completa
url: /it/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizza la data dell'era giapponese in C# – Guida completa

Ti è mai capitato di dover **analizzare una data dell'era giapponese** in un'app .NET e chiederti perché il risultato sembra errato? Non sei l'unico. In molti sistemi legacy, le date arrivano nello stile “R3‑04‑01”, e devi convertirle in una stringa **format datetime yyyy-mm-dd** pulita per API o database.  

In questo tutorial percorreremo passo passo le operazioni necessarie, spiegheremo perché ogni elemento è importante e ti mostreremo come gestire i casi limite più insidiosi che spesso colpiscono gli sviluppatori.

> **Nota:** Tutto il codice è pronto per il copia‑incolla in un'app console che targetizza .NET 6 o versioni successive.

## Di cosa avrai bisogno

- .NET 6 SDK (o qualsiasi versione recente)
- Familiarità di base con C# e lo spazio dei nomi `System.Globalization`
- Un IDE o editor – Visual Studio, VS Code, Rider, o quello che preferisci

Nessun pacchetto NuGet esterno è richiesto; tutto è incluso nella BCL.

## Passo 1: Configurare la cultura giapponese con il calendario imperiale

Per prima cosa, ci serve un `CultureInfo` che conosca il calendario imperiale giapponese. Per impostazione predefinita, `ja-JP` utilizza il calendario gregoriano, quindi sostituiamo il suo `DateTimeFormat.Calendar` con un'istanza di `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Perché è importante:** Il `JapaneseCalendar` traduce i simboli dell'era (come “R” per Reiwa) nell'anno gregoriano corretto. Senza di esso, `DateTime.Parse` genererebbe una `FormatException`.

## Passo 2: Analizzare la stringa di data basata sull'era

Ora possiamo passare una stringa come `"R3-04-01"` a `DateTime.Parse`. La cultura che abbiamo appena configurato indica al parser come interpretare la parte “R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Se preferisci un approccio più sicuro che eviti eccezioni su input errati, sostituisci `Parse` con `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Suggerimento:** La stringa di formato personalizzata `"ggy-MM-dd"` indica al parser esattamente cosa aspettarsi. “gg” è il designatore dell'era, “y” l'anno all'interno di quell'era.

## Passo 3: Convertire il risultato in ISO 8601 (`format datetime yyyy-mm-dd`)

Infine, stampiamo il `DateTime` in un formato ISO standard. Il format specifier `"yyyy-MM-dd"` fa esattamente questo.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Eseguendo il programma ottieni:

```
2021-04-01
```

Questa è la **format datetime yyyy-mm-dd** che cercavi, pronta per payload JSON, inserimenti SQL o qualsiasi sistema a valle.

![parse japanese era date example](placeholder.png){alt="esempio di analisi della data dell'era giapponese"}

## Gestione di altre ere e casi limite

### Multiple Eras

Il Giappone ha attraversato diverse ere (Meiji, Taishō, Shōwa, Heisei, Reiwa). Il `JapaneseCalendar` le mappa automaticamente, quindi `"H30-12-31"` (Heisei 30) diventa `2018-12-31`. Mantieni la stessa logica di parsing; il calendario fa il lavoro pesante.

### Input non valido

Se una stringa non corrisponde al pattern previsto, `Parse` genera un'eccezione. Usa `TryParseExact` come mostrato prima, oppure pre‑valida con un'espressione regolare:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Fusi orari

Gli oggetti `DateTime` sono “kind‑agnostic” per impostazione predefinita. Se ti serve un timestamp UTC, chiama:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Oppure utilizza `DateTimeOffset` per una piena consapevolezza del fuso.

## Esempio completo funzionante

Ecco lo snippet intero da inserire in un nuovo progetto console:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Output console previsto**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Riepilogo

Abbiamo coperto come **analizzare le date dell'era giapponese**:

1. Creare un `CultureInfo` per `ja-JP` e sostituire il calendario con `JapaneseCalendar`.
2. Utilizzare `DateTime.Parse` o il più robusto `TryParseExact` con un formato personalizzato.
3. Formattare il `DateTime` risultante con `"yyyy-MM-dd"` per ottenere la desiderata **format datetime yyyy-mm-dd**.

Questo è tutto ciò di cui hai bisogno per collegare i dati legacy dell'era giapponese a sistemi moderni conformi a ISO.

## Prossimi passi

- **Elaborazione batch:** Scorri un CSV di date dell'era e scrivi le stringhe ISO in un database.
- **Localizzazione:** Converti le date ISO nuovamente in formato era per la visualizzazione UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Calendari personalizzati:** Esplora `TaiwanCalendar` o `HijriCalendar` per altre esigenze regionali.

Sentiti libero di sperimentare—cambia la stringa dell'era, testa i casi limite o integra questa logica in endpoint ASP.NET Core. Se incontri difficoltà, lascia un commento qui sotto; buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci alternativi nei tuoi progetti.

- [Come implementare la convalida delle date in .NET usando Aspose.Cells: Guida completa](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Modifica il sistema di data di Excel a 1904 usando Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Come implementare e formattare i commenti di Excel usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}