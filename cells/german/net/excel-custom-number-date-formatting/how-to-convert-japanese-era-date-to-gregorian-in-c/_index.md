---
category: general
date: 2026-10-01
description: Konvertieren Sie ein japanisches Ära-Datum in ein gregorianisches DateTime
  mit Aspose.Cells in C#. Erfahren Sie, wie Sie den japanischen Kalender schnell konvertieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: de
lastmod: 2026-10-01
og_description: Japanisches Ära-Datum in ein gregorianisches DateTime in C# konvertieren.
  Dieses Tutorial erklärt, wie man den japanischen Kalender genau mit Aspose.Cells
  umwandelt.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Japanisches Ära‑Datum in das gregorianische Datum in C# konvertieren – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Wie man ein japanisches Ära-Datum in das gregorianische Datum in C# konvertiert
url: /de/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man japanische Ära‑Datumsangaben in das Gregorianische Datum in C# konvertiert

Wenn Sie **japanische Ära‑Datums‑Strings** in Gregorianische Daten in C# **konvertieren** müssen, zeigt Ihnen diese Anleitung genau, wie das geht. Egal, ob Sie Legacy‑Daten verarbeiten, Benutzereingaben lesen oder Berichte erstellen – die Aspose.Cells‑Bibliothek macht die Konvertierung unkompliziert. Außerdem erfahren Sie, wie Sie **japanische Kalender**‑Werte am besten **konvertieren**, wenn Sie mit Tabellenkalkulationen arbeiten.

Das Tutorial deckt jeden Schritt ab – vom Erstellen einer Arbeitsmappe bis zum Abrufen eines `DateTime`‑Werts – sodass Sie ein vollständiges, ausführbares Programm kopieren und einfügen können. Keine externe Dokumentation ist nötig; folgen Sie einfach dem Code und den Erklärungen unten.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)
* Eine Lizenz für **Aspose.Cells** (die kostenlose Testversion reicht für Tests)
* Eine Entwicklungsumgebung wie Visual Studio 2022 oder VS Code
* Grundlegende Kenntnisse von C#‑Konsolenanwendungen

## Japanisches Ära‑Datum mit Aspose.Cells konvertieren

Der Kern der Konvertierung besteht aus wenigen einfachen API‑Aufrufen. Aspose.Cells interpretiert japanische Ära‑Strings automatisch (z. B. „Reiwa 2/04/01“) und stellt das Ergebnis als `DateTime`‑Objekt bereit, sobald das Arbeitsblatt neu berechnet wurde.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Warum jeder Schritt wichtig ist

| Schritt | Zweck | Wie es bei der Konvertierung hilft |
|---------|-------|------------------------------------|
| **Arbeitsmappe erstellen** | Stellt einen Container bereit, der Excel‑Formeln und Datumssysteme versteht. | Die interne Datums‑Engine der Bibliothek wird nur innerhalb einer Arbeitsmappe aktiviert. |
| **Ära‑String einfügen** | Liefert den rohen japanischen Kalendertext, den Sie übersetzen möchten. | Aspose.Cells erkennt Ära‑Namen wie *Reiwa*, *Heisei*, *Showa* usw. |
| **Stil setzen** | Erzwingt, dass die Zelle als Wert‑Zelle und nicht als Literal‑String behandelt wird. | Ohne Stil könnte die `Calculate`‑Methode die Zelle ignorieren, sodass der Text unverändert bleibt. |
| **Berechnen** | Löst das Parsen des Ära‑Strings und die Konvertierung in die interne serielle Datumszahl aus. | Die Bibliothek wandelt „Reiwa 2/04/01“ → serielle Zahl → Gregorianisches `DateTime`. |
| **`DateTimeValue` lesen** | Gibt das konvertierte .NET‑`DateTime`‑Objekt zurück. | Sie haben nun ein Standard‑`DateTime`, das Sie in jeder .NET‑API verwenden können. |

## Wie man japanischen Kalender in anderen Szenarien konvertiert

Der gleiche Ansatz funktioniert für jeden von Aspose.Cells unterstützten japanischen Ära‑Namen:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Umgang mit ungültigen oder mehrdeutigen Strings

* **Ungültiger Ära‑Name** – Aspose.Cells wirft eine `FormatException`. Wickeln Sie die Konvertierung in `try/catch`, um eine benutzerfreundliche Fehlermeldung auszugeben.
* **Fehlendes Jahr/Monat/Tag** – Die Bibliothek erwartet das vollständige Muster „Ära Jahr/Monat/Tag“. Wenn Sie Teil‑Daten erhalten, fügen Sie fehlende Teile hinzu oder verwerfen Sie die Eingabe frühzeitig.
* **Unterschiedliche Locale‑Einstellungen** – Die Konvertierung hängt **nicht** von der aktuellen Thread‑Culture ab; sie verwendet stets die in Aspose.Cells integrierte japanische Ära‑Map. Das macht die Methode sicher für serverseitige Verarbeitung.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Praktische Tipps und häufige Fallstricke

* **Immer `SetStyle`** vor `Calculate` aufrufen. Das Überspringen dieses Schrittes ist eine häufige Fehlerquelle, weil die Zelle dann ein reiner Textbehälter bleibt.
* **Die gleiche Arbeitsmappe wiederverwenden**, wenn Sie viele Daten konvertieren müssen. Für jede Konvertierung eine neue Arbeitsmappe zu erstellen, verursacht unnötigen Overhead.
* **Batch‑Konvertierung** – Füllen Sie eine Spalte mit Ära‑Strings, rufen Sie `worksheet.Calculate()` einmal auf und lesen Sie dann die gesamte Spalte von `DateTimeValue`s. Das ist deutlich effizienter als das Berechnen pro Zelle.
* **Versionskompatibilität** – Die Ära‑Konvertierungslogik wurde in Aspose.Cells 22.9 eingeführt. Stellen Sie sicher, dass Sie diese Version oder eine neuere verwenden; ältere Releases behandeln den String als reinen Text.

## Vollständiges funktionierendes Beispiel (Konsolen‑App)

Unten finden Sie ein eigenständiges Programm, das Sie sofort kompilieren und ausführen können. Es demonstriert sowohl eine Reiwa‑ als auch eine Heisei‑Konvertierung und behandelt Fehler elegant.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Erwartete Konsolenausgabe**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Das Ausführen dieses Programms bestätigt, dass die Bibliothek **japanische Ära‑Datums‑Strings** korrekt **konvertiert** und nicht unterstützte Werte freundlich meldet.

## Fazit

Sie wissen jetzt, wie Sie **japanische Ära‑Datums‑Strings** in standardisierte Gregorianische `DateTime`‑Objekte mit Aspose.Cells in C# **konvertieren**. Der Vorgang reduziert sich auf das Einfügen des Ära‑Texts, das Anwenden eines Stils, das Neuberechnen des Arbeitsblatts und das Auslesen von `DateTimeValue`. Wenn Sie den obigen Schritten folgen, können Sie zudem die breitere Frage beantworten, **wie man japanische Kalender**‑Daten in großen Mengen konvertiert, Fehler behandelt und die Leistung optimiert.

### Nächste Schritte

* Erkunden Sie **Formatierungsoptionen**, um das Gregorianische Datum mit einem benutzerdefinierten Zahlenformat zurück in das Arbeitsblatt zu schreiben.
* Kombinieren Sie diese Konvertierung mit **Daten‑Import‑Pipelines** (z. B. dem Einlesen von CSV‑Dateien, die Ära‑Datumsangaben enthalten).
* Prüfen Sie weitere Aspose.Cells‑Funktionen wie **Datumsarithmetik** und **regionale Einstellungen** für komplexere Kalenderszenarien.

Viel Spaß beim Coden und passen Sie das Beispiel gern an Ihre eigenen Daten‑Verarbeitungs‑Workflows an!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungs‑Ansätze in Ihren eigenen Projekten zu erkunden.

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}