---
category: general
date: 2026-06-08
description: Japanisches Ära‑Datum in C# mit Aspose.Cells parsen. Erfahren Sie, wie
  CultureInfo ja‑JP und das japanische Ära‑Format eine genaue Excel‑Datumsumwandlung
  ermöglichen.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: de
og_description: Japanisches Ära‑Datum in C# schnell parsen. Dieses Tutorial zeigt,
  wie CultureInfo ja‑JP und Aspose.Cells Ära‑Strings in korrekte DateTime‑Objekte
  umwandeln.
og_title: Japanisches Ära‑Datum in C# parsen – Aspose.Cells‑Leitfaden
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
title: Japanisches Ära‑Datum in C# mit Aspose.Cells parsen – Vollständige Anleitung
url: /de/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanisches Ära‑Datum in C# mit Aspose.Cells – Vollständige Anleitung

Haben Sie jemals **parse japanese era date**‑Zeichenketten direkt aus einer Excel‑Tabelle verarbeiten müssen? Vielleicht holen Sie Daten aus einem Altsystem, das noch „令和3年5月12日“ verwendet, und Sie möchten ein sauberes `DateTime` für Berichte erhalten. In diesem Tutorial führen wir Sie durch ein vollständiges, sofort ausführbares Beispiel, das diese era‑formatierten Zeichenketten in korrekte C#‑Datumswerte umwandelt – ganz ohne Rätselraten.

Wir verwenden **Aspose.Cells**, die leistungsstarke .NET‑Bibliothek für die Excel‑Manipulation, zusammen mit der **CultureInfo ja-JP**‑Einstellung, die japanische Ären lesen kann. Am Ende haben Sie ein wiederverwendbares Snippet, das „令和“, „平成“ und sogar ältere Ären problemlos verarbeitet.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)
- Aspose.Cells für .NET (Sie können das kostenlose Test‑NuGet‑Paket erhalten: `Install-Package Aspose.Cells`)
- Grundlegende C#‑Kenntnisse – nichts Besonderes, eine Konsolen‑App reicht aus
- Eine IDE Ihrer Wahl (Visual Studio, Rider, VS Code usw.)

Das war’s. Keine zusätzlichen Dienste, keine obskuren Drittanbieter‑Parser.

## Schritt 1: Projekt einrichten und Aspose.Cells hinzufügen

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Öffnen Sie jetzt **Program.cs** und fügen Sie die erforderlichen Namespaces hinzu:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Profi‑Tipp:** Wenn Sie Visual Studio verwenden, schlägt die IDE das Hinzufügen der `using`‑Anweisungen automatisch vor, sobald Sie die Klassennamen eingeben.

## Schritt 2: Arbeitsmappe erstellen und japanische Kultur anwenden

Der Schlüssel, um **parse japanese era date** korrekt zu verarbeiten, besteht darin, Aspose.Cells mitzuteilen, welche Kultur verwendet werden soll. Das Setzen von `CultureInfo` auf `ja-JP` aktiviert das Ära‑bewusste Parsen.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Warum ist das wichtig? Der japanische Kalender hat mehrere Ären (z. B. *Reiwa* (令和), *Heisei* (平成)). Das `CultureInfo`‑Objekt enthält einen `JapaneseCalendar`, der die Startdaten jeder Ära kennt, sodass jede Zeichenkette im japanischen Ära‑Format korrekt interpretiert werden kann.

## Schritt 3: Ein japanisches Ära‑Datum in eine Zelle schreiben

Lassen Sie uns ein Beispiel‑Ära‑Datum in Zelle **A1** einfügen. Ändern Sie die Zeichenkette gern, um verschiedene Ären zu testen.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Wenn Sie lieber mit einer bestehenden Arbeitsmappe arbeiten, können Sie sie mit `new Workbook("path/to/file.xlsx")` laden und den Erstellungs‑Schritt überspringen.

## Schritt 4: Den Wert als C#‑DateTime‑Objekt abrufen

Jetzt passiert die Magie. Durch Aufruf von `GetDateTime()` liest Aspose.Cells die Zelle unter Verwendung der zuvor gesetzten `CultureInfo` und gibt ein korrektes `DateTime` zurück.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Erwartete Ausgabe**

```
Parsed DateTime: 2021-05-12
```

Damit ist der gesamte **parse japanese era date**‑Ablauf abgeschlossen – vier kompakte Code‑Zeilen.

## Schritt 5: Sonderfälle und alternative Ären behandeln

Echte Daten sind nicht immer sauber. Hier einige Szenarien, denen Sie begegnen könnten, und wie Sie sie handhaben.

### 5.1 Ungültige oder leere Zeichenketten

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

### 5.2 Ältere Ären (Showa, Taisho)

Das gleiche `CultureInfo ja-JP` funktioniert automatisch für ältere Ären:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Verwendung von `DateTime.ParseExact` für strenge Validierung

Wenn Sie das exakte japanische Ära‑Muster erzwingen wollen, verwenden Sie einen benutzerdefinierten Format‑String:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Dieser Ansatz wirft eine `FormatException`, wenn die Zeichenkette abweicht – nützlich für Datenqualitäts‑Checks.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Programm, das Sie in **Program.cs** kopieren und ausführen können.

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

Führen Sie es mit `dotnet run` aus und Sie sollten sehen:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom – **parse japanese era date** erledigt, und Sie haben eine Vorlage für jede mögliche Ära.

![Ablaufdiagramm zum Parsen des japanischen Ära‑Datums – zeigt die Erstellung der Arbeitsmappe, das Festlegen der Kultur, das Schreiben in die Zelle und den Aufruf von GetDateTime](parse-japanese-era-date.png "Diagramm, das zeigt, wie man das japanische Ära‑Datum mit Aspose.Cells und CultureInfo ja-JP parst")

## Häufig gestellte Fragen beantwortet

- **Funktioniert das mit .xlsx‑Dateien, die bereits Ära‑Datumswerte enthalten?**  
  Ja. Solange die `Settings.CultureInfo` des Arbeitsbuchs vor dem Aufruf von `GetDateTime()` auf `ja-JP` gesetzt ist, interpretiert Aspose.Cells die vorhandenen Zeichenketten korrekt.

- **Wie sieht es mit Zeitzonen aus?**  
  Das Parsen liefert ein `DateTime` mit `Kind = Unspecified`. Wenn Sie UTC oder lokale Zeit benötigen, verwenden Sie `DateTime.SpecifyKind` oder konvertieren Sie nach dem Parsen.

- **Kann ich mehrere Zellen gleichzeitig parsen?**  
  Absolut. Durchlaufen Sie den gewünschten Bereich und rufen Sie `GetDateTime()` für jede Zelle auf – denken Sie nur daran, Ausnahmen für fehlerhafte Einträge zu behandeln.

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **parse japanese era date**‑Zeichenketten in C# mit Aspose.Cells und der integrierten `CultureInfo ja-JP` zu verarbeiten. Von der Einrichtung der Arbeitsmappe, dem Schreiben von Ära‑formatierten Zeichenketten, dem Abrufen eines sauberen `DateTime` bis hin zur Behandlung von Sonderfällen wie älteren Ären und strenger Validierung – dieser Leitfaden liefert eine produktionsreife Lösung.

Als Nächstes könnten Sie **Excel date conversion** für numerische Serien‑Datumswerte erkunden oder tiefer in **C# DateTime parsing** mit benutzerdefinierten Kalendern für andere Regionen einsteigen. Das gleiche Muster funktioniert für den thailändischen buddhistischen Kalender, den hebräischen Kalender und mehr – einfach die `CultureInfo` austauschen.

Haben Sie ein spezielles Problem? Hinterlassen Sie einen Kommentar, und wir lösen es gemeinsam. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

- [Wie man Datumsvalidierung in .NET mit Aspose.Cells implementiert: Ein umfassender Leitfaden](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Excel-Datumsystem auf 1904 umstellen mit Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Excel effizient in PDF konvertieren mit benutzerdefinierten Datumsformaten mittels Aspose.Cells für Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}