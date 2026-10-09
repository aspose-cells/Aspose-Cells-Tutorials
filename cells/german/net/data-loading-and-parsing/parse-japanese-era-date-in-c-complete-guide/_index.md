---
category: general
date: 2026-06-27
description: Erfahren Sie, wie Sie japanische Ära‑Daten in C# parsen und dann das
  Datum im Format yyyy‑mm‑dd für ISO‑Ausgabe formatieren. Schritt‑für‑Schritt‑Code,
  Randfälle und Tipps.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: de
og_description: Japanisches Ära‑Datum in C# parsen und das Datum im Format yyyy‑mm‑dd
  mühelos formatieren. Vollständiges Beispiel mit Erklärungen und Fallstricken.
og_title: Japanisches Ära‑Datum in C# parsen – Vollständiger Programmierleitfaden
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
title: Japanisches Ära‑Datum in C# parsen – Vollständiger Leitfaden
url: /de/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanisches Ära‑Datum in C# parsen – Komplettanleitung

Haben Sie jemals **parse Japanese era date** in einer .NET‑App parsen müssen und sich gefragt, warum das Ergebnis falsch aussieht? Sie sind nicht allein. In vielen Altsystemen kommen Daten im Stil „R3‑04‑01“ vor, und Sie müssen sie in einen sauberen **format datetime yyyy-mm-dd**‑String für APIs oder Datenbanken umwandeln.  

In diesem Tutorial gehen wir die genauen Schritte durch, um das zu erreichen, erklären, warum jeder Teil wichtig ist, und zeigen Ihnen, wie Sie die kniffligen Randfälle behandeln, die Entwicklern häufig Probleme bereiten.

> **Hinweis:** Der gesamte Code ist bereit zum Kopieren‑Einfügen in eine Konsolenanwendung, die .NET 6 oder höher targetiert.

## Was Sie benötigen

- .NET 6 SDK (oder jede aktuelle Version)
- Grundlegende Kenntnisse in C# und dem Namespace `System.Globalization`
- Eine IDE oder ein Editor – Visual Studio, VS Code, Rider, oder was Sie bevorzugen

Keine externen NuGet‑Pakete erforderlich; alles ist in der BCL enthalten.

## Schritt 1: Die japanische Kultur mit dem kaiserlichen Kalender einrichten

Zuerst benötigen wir ein `CultureInfo`, das den japanischen kaiserlichen Kalender kennt. Standardmäßig verwendet `ja-JP` den Gregorianischen Kalender, also ersetzen wir dessen `DateTimeFormat.Calendar` durch eine Instanz von `JapaneseCalendar`.

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

> **Warum das wichtig ist:** Der `JapaneseCalendar` übersetzt Ärasymbole (wie „R“ für Reiwa) in das korrekte Gregorianische Jahr. Ohne ihn würde `DateTime.Parse` eine `FormatException` auslösen.

## Schritt 2: Das ära‑basierte Datums‑String parsen

Jetzt können wir einen String wie `"R3-04-01"` an `DateTime.Parse` übergeben. Die gerade konfigurierte Kultur teilt dem Parser mit, wie er den Teil „R3“ interpretieren soll.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Wenn Sie einen sichereren Ansatz bevorzugen, der Ausnahmen bei fehlerhaften Eingaben vermeidet, ersetzen Sie `Parse` durch `TryParseExact`:

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

> **Profi‑Tipp:** Der benutzerdefinierte Formatstring `"ggy-MM-dd"` teilt dem Parser exakt mit, was erwartet wird. „gg“ ist der Äradesignator, „y“ das Jahr innerhalb dieser Ära.

## Schritt 3: Das Ergebnis in ISO 8601 konvertieren (`format datetime yyyy-mm-dd`)

Abschließend geben wir das `DateTime` in einem standardisierten ISO‑Format aus. Der Formatspezifizierer `"yyyy-MM-dd"` bewirkt genau das.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Beim Ausführen des Programms wird ausgegeben:

```
2021-04-01
```

Das ist das **format datetime yyyy-mm-dd**, das Sie gesucht haben, bereit für JSON‑Payloads, SQL‑Einfügungen oder jedes nachgelagerte System.

![Beispiel für das Parsen eines japanischen Ära-Datums](placeholder.png){alt="Beispiel für das Parsen eines japanischen Ära-Datums"}

## Umgang mit anderen Äras und Randfällen

### Mehrere Äras

Japan hat mehrere Äras durchlaufen (Meiji, Taishō, Shōwa, Heisei, Reiwa). Der `JapaneseCalendar` ordnet sie automatisch zu, sodass `"H30-12-31"` (Heisei 30) zu `2018-12-31` wird. Verwenden Sie einfach dieselbe Parsing‑Logik; der Kalender übernimmt die schwere Arbeit.

### Ungültige Eingabe

Wenn ein String nicht dem erwarteten Muster entspricht, wirft `Parse` eine Ausnahme. Verwenden Sie `TryParseExact` wie oben gezeigt, oder prüfen Sie vorher mit einem regulären Ausdruck:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Zeitzonen

`DateTime`‑Objekte sind standardmäßig „kind‑agnostisch“. Wenn Sie einen UTC‑Zeitstempel benötigen, rufen Sie auf:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Oder verwenden Sie `DateTimeOffset` für vollständiges Zeitzonen‑Bewusstsein.

## Vollständiges funktionierendes Beispiel

Hier ist das komplette Snippet, das Sie in ein neues Konsolenprojekt einfügen können:

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

**Erwartete Konsolenausgabe**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Zusammenfassung

Wir haben behandelt, wie man **parse Japanese era date**‑Strings parst, indem man:

1. Ein `CultureInfo` für `ja-JP` erstellt und durch `JapaneseCalendar` ersetzt.
2. `DateTime.Parse` oder das robustere `TryParseExact` mit einem benutzerdefinierten Format verwendet.
3. Das resultierende `DateTime` mit `"yyyy-MM-dd"` formatiert, um das gewünschte **format datetime yyyy-mm-dd** zu erhalten.

Damit haben Sie alles, was Sie benötigen, um Legacy‑Japan‑Ära‑Daten in moderne ISO‑konforme Systeme zu überführen.

## Was kommt als Nächstes?

- **Batch‑Verarbeitung:** Durchlaufen Sie eine CSV mit Ära‑Daten und schreiben Sie ISO‑Strings in eine Datenbank.
- **Lokalisierung:** Konvertieren Sie ISO‑Daten zurück ins Ära‑Format für die UI‑Anzeige (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Benutzerdefinierte Kalender:** Erkunden Sie `TaiwanCalendar` oder `HijriCalendar` für andere regionale Anforderungen.

Fühlen Sie sich frei zu experimentieren – tauschen Sie den Ära‑String aus, testen Sie Randfälle oder integrieren Sie diese Logik in ASP.NET‑Core‑Endpoints. Wenn Sie auf ein Problem stoßen, hinterlassen Sie unten einen Kommentar; happy coding!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Datumsvalidierung in .NET mit Aspose.Cells implementiert: Ein umfassender Leitfaden](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Excel‑Datumsystem auf 1904 mit Aspose.Cells .NET ändern](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Wie man Excel‑Kommentare mit Aspose.Cells für .NET implementiert und formatiert: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}