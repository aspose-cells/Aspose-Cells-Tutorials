---
category: general
date: 2026-10-26
description: Lernen Sie, wie Sie die japanische Kalender‑CultureInfo in C# beim Parsen
  von Ära‑Datumsangaben und beim Einfügen in ein Excel‑Arbeitsblatt mit NPOI verwenden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: de
lastmod: 2026-10-26
og_description: Verwenden Sie die japanische Kalender‑CultureInfo in C#, um Reiwa‑Datumsangaben
  zu parsen und in ein Excel‑Arbeitsblatt zu schreiben. Vollständiger, ausführbarer
  Code mit Erklärungen.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Japanische Kalender‑CultureInfo in C# verwenden – vollständiges Excel‑Beispiel
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
title: Wie man das japanische Kalender‑CultureInfo in C# verwendet, um Daten in Excel
  zu schreiben
url: /de/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man die japanische Kalender‑CultureInfo in C# verwendet, um Daten in Excel zu schreiben

Wenn Sie **die japanische Kalender‑CultureInfo** bei der Arbeit mit Datumsangaben in C# benötigen, zeigt Ihnen diese Anleitung genau, wie das geht. Sie lernen, einen Datums‑String zu parsen, der einen japanischen Ära‑Namen enthält (z. B. *Reiwa 2/5/1*), und anschließend das resultierende `DateTime` in die erste Zelle eines Excel‑Arbeitsblatts mit der NPOI‑Bibliothek zu schreiben.

Das Parsen von ära‑basierten Datumsangaben ohne die richtige `CultureInfo` führt zu `FormatException` oder falschen Monat‑/Tag‑Werten. Durch die Konfiguration von `CultureInfo` auf den japanischen Kalender stellen Sie sicher, dass die .NET‑Laufzeit die Ära korrekt interpretiert und dass der in Excel gespeicherte Wert der ursprünglichen japanischen Schreibweise entspricht.

In diesem Tutorial werden Sie:

* Ein `CultureInfo`‑Objekt erstellen, das den japanischen Kalender verwendet.
* Einen japanischen Ära‑Datums‑String mit `DateTime.Parse` parsen.
* Das geparste `DateTime` in eine NPOI‑Arbeitsblattzelle einfügen.
* Das vollständige, ausführbare Programm sowie die erwartete Ausgabe sehen.

> **Voraussetzungen** – .NET 6.0+ (oder .NET Core 3.1+), das **NPOI**‑NuGet‑Paket und Grundkenntnisse in C# sowie im Umgang mit Excel‑Dateien.

---

## Was Sie benötigen

| Element | Grund |
|------|--------|
| **.NET SDK** (6.0 oder neuer) | Stellt die Laufzeit und Bibliotheken für `CultureInfo` bereit. |
| **NPOI** (`NPOI` NuGet‑Paket) | Ermöglicht das Erstellen und Manipulieren von Excel‑Dateien ohne installierte Office‑Software. |
| **Visual Studio Code**, **Visual Studio** oder eine beliebige C#‑IDE | Zum Kompilieren und Ausführen des Beispiels. |
| **Japanischer Ära‑Datums‑String** (z. B. `"Reiwa 2/5/1"`) | Demonstriert die Verwendung des japanischen Kalenders. |

---

## Schritt 1: NPOI installieren

Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet add package NPOI --version 2.6.1
```

Das Paket liefert die Typen `IWorkbook`, `ISheet` und `ICell`, die später verwendet werden.

---

## Schritt 2: Eine CultureInfo erstellen, die den japanischen Kalender verwendet

Der japanische Kalender ist ein ära‑basierter Kalender. Sie müssen die *Japanese*‑Variante des `ja-JP`‑Locales anfordern und explizit den Kalender auf `JapaneseCalendar` setzen.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Warum das wichtig ist** – Die Standard‑`ja-JP`‑Culture verwendet den gregorianischen Kalender. Durch das Neusetzen der `Calendar`‑Eigenschaft wird sichergestellt, dass Ära‑Namen wie *Reiwa* beim Parsen erkannt werden.

---

## Schritt 3: Einen japanischen Ära‑Datums‑String parsen

Jetzt, wo die `CultureInfo` konfiguriert ist, können Sie sicher einen String mit einem Ära‑Namen parsen.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Ausgabe**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Die `Parse`‑Methode interpretiert *Reiwa 2* als das gregorianische Jahr 2020, Monat 5, Tag 1.

### Sonderfall: Umgang mit ungültigen Ären

Wenn ein Benutzer eine nicht unterstützte Ära angibt (z. B. `"Heisei 31/4/30"` nach dem Ende der Heisei‑Ära), wirft `DateTime.Parse` eine `FormatException`. Umhüllen Sie den Aufruf mit einem try‑catch‑Block, um eine benutzerfreundliche Fehlermeldung auszugeben:

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

## Schritt 4: Das geparste DateTime in ein Excel‑Arbeitsblatt schreiben

Mit dem fertigen `DateTime`‑Objekt können Sie es in einer Excel‑Zelle speichern. NPOI formatiert `DateTime`‑Werte automatisch als Excel‑Datumswerte.

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

**Ergebnis** – Beim Öffnen von *JapaneseEraDate.xlsx* wird das Datum **2020‑05‑01** in Zelle A1 angezeigt.

### Warum NPOI verwenden?

*Funktioniert auf jeder Plattform* (Windows, Linux, macOS) und erfordert **keine** Installation von Microsoft Office. Das macht die Lösung geeignet für CI‑Pipelines, Docker‑Container oder serverseitige Verarbeitung.

---

## Schritt 5: Vollständiges, ausführbares Programm

Alles zusammengeführt, hier ein komplettes Konsolen‑Anwendungsbeispiel, das den gesamten Ablauf demonstriert:

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

**So führen Sie das Programm aus**

```bash
dotnet run
```

Nach der Ausführung finden Sie `JapaneseEraDate.xlsx` im Projektordner mit dem korrekt geparsten Datum.

---

## Häufige Stolperfallen und bewährte Tipps

| Stolperfalle | Lösung / Empfehlung |
|---------|----------------------|
| Vergessen, `japaneseCulture.DateTimeFormat.Calendar` zu setzen | Immer eine `JapaneseCalendar`‑Instanz zuweisen; sonst wird der Ära‑Name nicht erkannt. |
| Verwendung von `DateTime.TryParse` ohne die benutzerdefinierte `CultureInfo` | Das gleiche `japaneseCulture` an `TryParse` übergeben, um konsistentes Verhalten zu gewährleisten. |
| Erwartung, dass Excel den Ära‑Namen anzeigt | Die integrierten Excel‑Datumsformate sind nur gregorianisch. Wenn Sie die Ära anzeigen möchten, speichern Sie den Original‑String in einer separaten Spalte oder erstellen Sie ein benutzerdefiniertes Textformat. |
| Nicht‑Entsorgen des `FileStream` | Einen `using`‑Block (wie gezeigt) verwenden, um den Dateihandle sofort freizugeben. |
| Mischen von `CultureInfo`‑Objekten über Threads hinweg | `CultureInfo` ist für Lese‑Operationen thread‑sicher, vermeiden Sie jedoch Änderungen an der `Calendar`‑Eigenschaft nach der Initialisierung. |

---

## Fazit

Sie wissen jetzt, **wie man die japanische Kalender‑CultureInfo** in C# nutzt, um japanische Ära‑Datumsangaben korrekt zu parsen und das resultierende `DateTime` mit NPOI in ein Excel‑Arbeitsblatt zu schreiben. Das vollständige Beispiel deckt Konfiguration, Parsing, Fehlerbehandlung und Excel‑Ausgabe ab und bietet Ihnen eine solide Basis für jede internationalisierte Berichts‑ oder Datenaustausch‑Szenario.

Als Nächstes könnten Sie Folgendes erkunden:

* **Datumsformatierung mit benutzerdefiniertem Text**, um den Ära‑Namen innerhalb von Excel zu erhalten.
* **Datumswerte aus Excel lesen** mittels `cell.DateCellValue` unter Berücksichtigung des japanischen Kalenders.
* **Die gleiche Technik** für andere ära‑basierte Kalender (z. B. thailändischer buddhistischer Kalender) anwenden, indem Sie `JapaneseCalendar` durch die passende `Calendar`‑Unterklasse ersetzen.

Experimentieren Sie gern mit verschiedenen Ära‑Strings, größeren Datensätzen oder der Integration dieser Logik in ASP.NET Core‑APIs, die Excel‑Berichte on‑the‑fly erzeugen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel‑Arbeitsmappe mit japanischen Kalenderdaten erstellen – Vollständige Anleitung](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Japanische Ära‑Datumsangaben in Excel parsen – Vollständige Anleitung für C#‑Entwickler](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Wie man eine Excel‑Arbeitsmappe erstellt und japanische Daten in C# parst](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}