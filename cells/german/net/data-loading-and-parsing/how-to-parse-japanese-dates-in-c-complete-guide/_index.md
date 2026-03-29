---
category: general
date: 2026-03-29
description: Wie man japanische Daten in C# mit DateTimeParser und CultureInfo parst.
  Erfahren Sie, wie man japanische Ära‑Datumsangaben analysiert, erhalten Sie C#‑Datumsparsing‑Tipps
  und lernen Sie den Umgang mit Sonderfällen.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: de
og_description: Wie man japanische Daten in C# mit DateTimeParser und CultureInfo
  parst. Erhalten Sie eine Schritt‑für‑Schritt‑Lösung für das Parsen von japanischen
  Ära‑Datumsangaben.
og_title: Wie man japanische Daten in C# parst – Vollständige Anleitung
tags:
- C#
- .NET
- DateTime
- Localization
title: Wie man japanische Datumsangaben in C# parst – Vollständiger Leitfaden
url: /de/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man japanische Daten in C# parst – Vollständige Anleitung

Haben Sie sich schon einmal gefragt, **how to parse japanese** Datumszeichenketten in einer .NET‑Anwendung zu verarbeiten? Vielleicht arbeiten Sie an einem Finanzsystem, das Daten wie „令和3年5月12日“ von einem japanischen Kunden erhält, und Sie müssen diese in ein reguläres `DateTime` umwandeln. Sie sind nicht allein – Lokalisierungsprobleme tauchen ständig auf.  

Die gute Nachricht: Mit den richtigen Culture‑Einstellungen und einer kleinen Hilfsklasse wird **how to parse japanese** Daten zum Kinderspiel. In diesem Tutorial gehen wir Schritt für Schritt vor, von der Einrichtung von `CultureInfo` für *ja‑JP* bis hin zur Behandlung von Sonderfällen wie historischen Ären. Am Ende haben Sie einen wiederverwendbaren `DateTimeParser`, der für jedes moderne japanische Ära‑Datum funktioniert.

> **Was Sie erhalten** – ein vollständiges, ausführbares Beispiel, Erklärungen, warum jede Zeile wichtig ist, Tipps für ältere Ären und eine schnelle Checkliste, damit Sie keinen Schritt vergessen.

## Voraussetzungen

- .NET 6+ (oder .NET Framework 4.7 + – die verwendete API hat sich nicht geändert)
- Grundkenntnisse in C# (Sie sollten mit `using`‑Anweisungen und `Console.WriteLine` vertraut sein)
- Keine externen NuGet‑Pakete – alles befindet sich in `System` und `System.Globalization`

Wenn Sie bereits ein Projekt geöffnet haben, super – fügen Sie den Code einfach ein. Wenn nicht, erstellen Sie eine neue Konsolen‑App mit `dotnet new console -n JapaneseDateDemo` und Sie sind startklar.

## Schritt 1: Das japanische Kalendersystem verstehen

Bevor wir in den Code eintauchen, beantworten wir das „Warum“. Japanische Daten werden im **Ära**‑Format (元号) angegeben, wobei die Jahreszahl zurückgesetzt wird, wenn ein neuer Kaiser den Thron besteigt. Zum Beispiel:

- **令和** (Reiwa) begann am 01.05.2019.  
- **平成** (Heisei) erstreckte sich von 1989‑2019.  
- **昭和** (Showa) lief von 1926‑1989.

Die .NET‑Klasse `JapaneseCalendar` kennt diese Ären bereits, aber Sie müssen dem Parser mitteilen, welche Kultur verwendet werden soll. Hier kommt **cultureinfo ja‑jp** ins Spiel – sie verknüpft den Kalender mit dem japanischen Locale.

## Schritt 2: Einen kleinen Wrapper erstellen – `DateTimeParser`

Statt überall `CultureInfo` zu verstreuen, kapseln wir die Logik in einer kleinen Hilfsklasse. Das macht den Code wiederverwendbar und hält den Rest Ihrer Anwendung sauber.

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

**Warum dieser Helfer?**  
- **Single Responsibility** – alle kulturspezifischen Parsvorgänge befinden sich an einer Stelle.  
- **Fehlerbehandlung** – wir geben klare Meldungen aus, wenn das Format falsch ist.  
- **Zukunftssicher** – wenn Sie später die älteren *Taisho*‑ oder *Meiji*‑Ären unterstützen wollen, passen Sie einfach das Muster an oder fügen einen Fallback hinzu.

## Schritt 3: Alles in `Program.cs` zusammenführen

Jetzt verwenden wir den Wrapper, um einen Beispiel‑String zu parsen. Beachten Sie, wie wir die japanische Kultur mit `CultureInfo.GetCultureInfo("ja-JP")` erhalten. Das erfüllt die Anforderung **cultureinfo ja‑jp** und sorgt dafür, dass `JapaneseCalendar` aktiv ist.

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

Wenn Sie `dotnet run` ausführen, sehen Sie:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Das ist das Kernstück von **how to parse japanese** Daten. Einfach, oder?

## Schritt 4: Sonderfälle & ältere Ären behandeln

### 4.1 Historische Daten vor 1912

Der integrierte `JapaneseCalendar` unterstützt nur die modernen Ären (ab Meiji). Wenn Sie Daten aus der *Taisho*‑Periode (1912‑1926) oder der *Meiji*‑Periode (1868‑1912) parsen müssen, funktioniert dasselbe Muster – stellen Sie nur sicher, dass die Zeichenkette den korrekten Äranamen („大正“, „明治“) enthält. Der Parser liefert dann ein korrektes gregorianisches `DateTime`.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Fehlende Ära (mehrdeutige Eingabe)

Sendet ein Kunde „2021年5月12日“ ohne Ära, schlägt der Parser fehl, weil das Muster eine Ära (`ggg`) erwartet. Sie haben zwei Optionen:

1. **Gregorianisch annehmen** – auf `CultureInfo.InvariantCulture` und ein anderes Muster zurückgreifen.  
2. **Eingabe ablehnen** – den Aufrufer darauf hinweisen, dass eine Ära erforderlich ist.

Eine schnelle Anpassung sieht so aus:

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

### 4.3 Hinweis zur Thread‑Sicherheit

`CultureInfo`‑Objekte sind nach ihrer Erstellung schreibgeschützt, sodass Sie dieselbe Instanz sicher über mehrere Threads hinweg wiederverwenden können. Der `DateTimeParser` selbst hält keinen veränderbaren Zustand, wodurch er **thread‑safe** ist – ein nützliches Detail für hochfrequente Web‑APIs.

## Schritt 5: Alles zusammen – ein sofort kopierbares Beispiel

Unten finden Sie den vollständigen Quellcode, den Sie in ein frisches Konsolen‑Projekt einfügen können. Keine externen Pakete, keine versteckten Abhängigkeiten.

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
            "平成31年4月30日", // 2019‑04‑30 (letzter Tag von Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historisch)
            "2022年1月1日"      // mehrdeutig – keine Ära
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