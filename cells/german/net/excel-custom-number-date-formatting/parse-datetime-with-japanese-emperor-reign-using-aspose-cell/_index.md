---
category: general
date: 2026-09-24
description: Datum und Uhrzeit mit japanischer Kaiserherrschaft mithilfe von Aspose.Cells
  in C# parsen. Den japanischen Ära‑Kalender aktivieren, Ära‑Strings schreiben und
  genaue DateTime‑Werte abrufen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: de
lastmod: 2026-09-24
og_description: Datum/Zeit mit japanischer Kaiserzeit mithilfe von Aspose.Cells in
  C# parsen. Dieses Tutorial zeigt, wie man den japanischen Ära‑Kalender aktiviert,
  Ära‑Strings schreibt und ein korrektes Datum/Zeit zurückliest.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: DateTime mit japanischer Kaiserherrschaft mit Aspose.Cells parsen – C#‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Datum und Uhrzeit mit japanischer Kaiserherrschaft mithilfe von Aspose.Cells
  parsen
url: /de/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DateTime mit japanischer Kaiserherrschaft mit Aspose.Cells parsen

Wenn Sie **DateTime mit japanischer Kaiserherrschaft** in einer .NET-Anwendung parsen müssen, zeigt Ihnen dieses Handbuch genau, wie Sie dies mit Aspose.Cells tun. Durch Aktivieren des japanischen Ära‑Kalenders, Schreiben eines ära‑basierten Strings und Auslesen des resultierenden `DateTime`‑Werts erhalten Sie zuverlässige, kultursensible Daten ohne manuelle String‑Manipulation.

Die Arbeit mit japanischen Ära‑Daten ist in Finanzen, Regierung und Altsystemen üblich, die noch Daten wie „令和3年5月10日“ speichern. Dieses Tutorial deckt den kompletten Workflow ab, von der Projekt‑Einrichtung bis zum Abrufen eines `DateTime`‑Objekts, das Sie in Berechnungen, Protokollierung oder UI‑Anzeige verwenden können.

## Was Sie lernen werden

- Wie man das Aspose.Cells NuGet‑Paket zu einem C#‑Projekt hinzufügt.  
- Wie man den **Japanese era calendar** über `Workbook.Settings` aktiviert.  
- Wie man einen japanischen Ära‑Datumsstring in eine Zelle schreibt und Aspose.Cells ihn automatisch parsen lässt.  
- Wie man den geparsten `DateTime` über die `DateTimeValue`‑Eigenschaft ausliest.  

**Voraussetzungen**  
- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).  
- Grundlegende Kenntnisse in C# und Visual Studio (oder einer anderen IDE).  
- Internetzugang zum Herunterladen des Aspose.Cells‑Pakets.

---

## Schritt 1: Aspose.Cells installieren

Öffnen Sie Ihren Projektordner in einem Terminal oder der NuGet Package Manager Console und führen Sie aus:

```bash
dotnet add package Aspose.Cells
```

Oder in Visual Studio: Rechts‑klicken Sie das Projekt → **Manage NuGet Packages** → suchen Sie nach **Aspose.Cells** und klicken Sie auf **Install**.  
Damit wird die `Aspose.Cells`‑Assembly hinzugefügt, die die Klassen `Workbook`, `Worksheet` und die benötigten Parsing‑Funktionen bereitstellt.

## Schritt 2: Den japanischen Ära‑Kalender aktivieren

Aspose.Cells deaktiviert das Parsen japanischer Ären standardmäßig. Sie müssen es über das Flag `Workbook.Settings.UseJapaneseEraCalendar` einschalten.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Das Setzen von `UseJapaneseEraCalendar` auf `true` weist die Bibliothek an, Zeichenketten, die Ära‑Namen enthalten (`令和`, `平成`, `昭和` usw.), gemäß den offiziellen japanischen Kalenderregeln zu interpretieren.

## Schritt 3: Einen japanischen Ära‑Datumsstring in eine Zelle schreiben

Als Nächstes holen Sie das erste Arbeitsblatt und platzieren einen japanischen Ära‑Datumsstring in Zelle **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Warum das funktioniert:**  
Wenn `UseJapaneseEraCalendar` aktiv ist, prüft `PutValue` die Zeichenkette, erkennt das Ära‑Präfix (`令和`) und wandelt es intern in das entsprechende gregorianische Jahr (2021) um. Die Bibliothek speichert den Wert dann als echtes `DateTime`‑Objekt, nicht nur als Text.

## Schritt 4: Den geparsten `DateTime`‑Wert auslesen

Lesen Sie nun den `DateTimeValue` der Zelle. Aspose.Cells gibt automatisch das gregorianische Datum zurück.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Das Ausführen des Programms gibt aus:

```
Parsed Gregorian date: 2021-05-10
```

Die Ausgabe bestätigt, dass **Parse DateTime with Japanese Emperor Reign** „令和3年5月10日“ korrekt in den 10. Mai 2021 umgewandelt hat.

## Schritt 5: Randfälle und gängige Varianten behandeln

### Mehrere Ära‑Formate
Aspose.Cells erkennt mehrere Ära‑Darstellungen:

| Ära (Japanisch) | Gregorianisches Jahresintervall |
|-----------------|---------------------------------|
| 明治 (Meiji)    | 1868‑1912                       |
| 大正 (Taishō)   | 1912‑1926                       |
| 昭和 (Shōwa)    | 1926‑1989                       |
| 平成 (Heisei)   | 1989‑2019                       |
| 令和 (Reiwa)    | 2019‑present                    |

Wenn Ihre Quelldaten Vollbreiten‑Zeichen, Leerzeichen oder das Kanji „年“, „月“, „日“ mischen, funktioniert der Parser weiterhin. Beispiel: `"平成31年4月30日"` wird zu `2019-04-30`.

### Ungültige Zeichenketten
Wenn die Zeichenkette nicht geparst werden kann (z. B. `"令和99年13月40日"`), gibt `DateTimeValue` `DateTime.MinValue` zurück. Sie können diesen Zustand prüfen:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Deaktivieren der Funktion
Falls Sie später rohe Ära‑Zeichenketten ohne Konvertierung speichern müssen, setzen Sie das Flag wieder auf `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Leistungshinweis
Das Aktivieren des Ära‑Kalenders verursacht einen kleinen Overhead bei jedem `PutValue`‑Aufruf, der Zeichenketten verarbeitet. Wenn Sie nur wenige Zellen parsen, aktivieren Sie das Flag unmittelbar vor der Operation und deaktivieren Sie es danach wieder, um die Auswirkungen zu minimieren.

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie sofort kopieren, einfügen und ausführen können.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Erwartete Ausgabe**

```
Parsed Gregorian date: 2021-05-10
```

Das Programm demonstriert den End‑to‑End‑Ablauf für **Parse DateTime with Japanese Emperor Reign** mit Aspose.Cells, von der Erstellung der Arbeitsmappe bis zum Erhalt eines nutzbaren `DateTime`‑Objekts.

---

## Fazit

Sie wissen jetzt, wie Sie **DateTime mit japanischer Kaiserherrschaft** in C# parsen, indem Sie:

1. **Aspose.Cells** installieren.  
2. Den **Japanese era calendar** über `Workbook.Settings` aktivieren.  
3. Ära‑basierte Zeichenketten in Zellen schreiben.  
4. Den resultierenden `DateTimeValue` auslesen.  

Dieser Ansatz eliminiert manuelle Parsing‑Logik, respektiert offizielle Ära‑Grenzen und lässt sich nahtlos in bestehenden .NET‑Datums‑Handling‑Code integrieren.

**Nächste Schritte**  
- Weitere kulturspezifische Funktionen von Aspose.Cells erkunden, wie **C# date parsing** für Hijri‑ oder Thai‑Buddhist‑Kalender.  
- Kombinieren Sie diese Technik mit **Workbook Settings** wie `CalcEngine`, um Formeln auszuwerten, die sich auf Ära‑Daten beziehen.  
- Verwenden Sie das geparste `DateTime` in Berichten, Datenbankspeicherung oder UI‑Komponenten, die gregorianische Daten benötigen.

Experimentieren Sie gern mit verschiedenen Ära‑Zeichenketten, behandeln Sie ungültige Eingaben und integrieren Sie die Lösung in größere Daten‑Import‑Pipelines. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Features zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}