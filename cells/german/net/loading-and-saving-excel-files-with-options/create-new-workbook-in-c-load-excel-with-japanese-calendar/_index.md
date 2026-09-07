---
category: general
date: 2026-02-26
description: Erstellen Sie ein neues Arbeitsbuch in C# und lernen Sie, wie Sie Excel‑Dateien
  laden, den Kalender auf Japanisch einstellen und Daten mühelos aus Excel extrahieren.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: de
og_description: Erstellen Sie eine neue Arbeitsmappe in C# und lernen Sie schnell,
  wie Sie Excel laden, einen japanischen Kalender einstellen und Daten aus Excel‑Dateien
  extrahieren.
og_title: Neues Arbeitsbuch in C# erstellen – Excel mit japanischem Kalender laden
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Neues Arbeitsbuch in C# erstellen – Excel mit japanischem Kalender laden
url: /de/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues Arbeitsbuch in C# erstellen – Excel mit japanischem Kalender laden

Haben Sie jemals **create new workbook** in C# erstellen müssen, waren sich aber nicht sicher, wie Excel den japanischen Kalender respektieren soll? Sie sind nicht allein. In vielen Unternehmensszenarien erhalten Sie Tabellen, die Daten im japanischen Ära‑System speichern, und das korrekte Auslesen dieser Daten kann sich anfühlen, als würde man eine Geheimsprache entschlüsseln.

Hier ist die Sache: Sie können **create new workbook**, dem Loader mitteilen, Daten mit dem japanischen Kalender zu interpretieren, und dann **extract date from excel** mit nur wenigen Codezeilen. In diesem Leitfaden gehen wir durch *how to load excel*, *how to set calendar* für japanische Daten und schließlich *read Japanese dates* aus einer Zelle. Kein Schnickschnack – nur ein vollständiges, ausführbares Beispiel, das Sie in Ihr Projekt kopieren‑und‑einfügen können.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch unter .NET Framework 4.6+)  
- Die **Aspose.Cells** Bibliothek (Kostenlose Testversion oder lizenzierte Version). Installieren Sie sie über NuGet:

```bash
dotnet add package Aspose.Cells
```

- Eine Excel‑Datei (`JapanDates.xlsx`), die japanische Ära‑Daten in Zelle A1 enthält.

Das war’s. Wenn Sie das haben, können wir sofort loslegen.

---

## Neues Arbeitsbuch erstellen und japanischen Kalender festlegen

Der erste Schritt ist, ein **create new workbook**‑Objekt zu erstellen und die `LoadOptions` zu konfigurieren, damit der Parser weiß, welcher Kalender zu verwenden ist.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Profi‑Tipp:** Die Eigenschaft `LoadOptions.Calendar` akzeptiert mehrere Enums (`Gregorian`, `Japanese`, `Hijri` usw.). Die richtige Auswahl stellt sicher, dass die Bibliothek den Ära‑Text (z. B. „令和3年“) in ein .NET `DateTime` übersetzt.

![Beispiel‑Screenshot neues Arbeitsbuch](image-url.png "Screenshot, der eine neue Arbeitsbuch‑Instanz mit japanischen Kalendereinstellungen zeigt"){: .align-center alt="Beispiel‑Screenshot neues Arbeitsbuch"}

### Warum das funktioniert

- **Workbook creation**: `new Workbook()` gibt Ihnen ein leeres Blatt—keine versteckten Arbeitsblätter, keine Standarddaten.
- **LoadOptions**: Durch Zuweisen von `CalendarType.Japanese` *vor* dem Aufruf von `Load` behandelt der Parser alle era‑basierten Zeichenketten als Daten statt als reinen Text.
- **GetDateTime()**: Nach dem Laden gibt `cellA1.GetDateTime()` ein echtes `DateTime`‑Objekt zurück, sodass Sie arithmetische Operationen, Formatierungen oder Datenbankeinfügungen ohne zusätzliche Konvertierungsschritte durchführen können.

---

## Excel‑Datei korrekt laden

Sie fragen sich vielleicht: „Gibt es einen speziellen Weg, **how to load excel** zu verwenden, wenn man mit nicht‑Gregorianischen Kalendern arbeitet?“ Die Antwort lautet ja – setzen Sie immer die `LoadOptions` *vor* dem Aufruf von `Load`. Wenn Sie zuerst laden und dann den Kalender ändern, wurden die Daten bereits falsch geparst.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Das obige Snippet zeigt ein häufiges Stolperstein. Die korrekte Reihenfolge (wie im vorherigen Abschnitt gezeigt) garantiert, dass die Engine die Zellen *als Daten* von Anfang an interpretiert.

---

## Kalender für japanische Daten festlegen

Wenn Sie Kalender on the fly umschalten müssen – zum Beispiel beim Verarbeiten einer Stapel von Dateien, die unterschiedliche Ära‑Systeme verwenden – können Sie dasselbe `Workbook`‑Objekt mit jeweils neuen `LoadOptions` wiederverwenden.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Der Aufruf `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` liefert das gleiche Ergebnis wie unser Hauptbeispiel, während `CalendarType.Gregorian` dieselbe Zelle als reine Zeichenkette behandeln würde (oder eine Ausnahme wirft, wenn das Format nicht erkannt wird).

---

## Datum aus Excel extrahieren – japanische Daten lesen

Jetzt, da das Arbeitsbuch mit dem richtigen Kalender geladen ist, ist das Auslesen des Datums unkompliziert. Die Methode `Cell.GetDateTime()` gibt ein `DateTime` zurück, das die Ära‑Umwandlung berücksichtigt.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Randfälle & Was‑wenn‑Szenarien

| Situation                              | Was zu tun ist                                                                                               |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Cell contains **text** instead of a date | Rufen Sie zuerst `cell.GetString()` auf, validieren Sie mit `DateTime.TryParse` oder erzwingen Sie die Datenvalidierung in Excel. |
| Multiple worksheets need processing    | Durchlaufen Sie `workbook.Worksheets` und wenden Sie dieselbe Extraktionslogik auf jedes Blatt an. |
| Dates are stored as **numbers** (Excel serial) | `cell.GetDateTime()` funktioniert weiterhin, da Aspose.Cells Seriennummern automatisch konvertiert. |
| File is **password‑protected**         | Verwenden Sie `LoadOptions.Password = "yourPwd"` bevor Sie `Load` aufrufen. |

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das komplette Programm, das Sie in eine Konsolen‑App einfügen können. Es enthält Fehlerbehandlung und demonstriert alle vier sekundären Schlüsselwörter im Kontext.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Erwartete Ausgabe** (angenommen, A1 enthält „令和3年5月12日“):

```
Japanese date in A1 → 2021-05-12
```

Wenn die Zelle ein gregorianisches Datum wie „2021‑05‑12“ enthält, funktioniert derselbe Code weiterhin, da die Bibliothek elegant auf die gregorianische Interpretation zurückgreift.

---

## Fazit

Sie wissen jetzt, wie man **create new workbook**, korrekt **how to load excel**, den passenden **how to set calendar** festlegt und schließlich **extract date from excel**, während man **read Japanese dates** ohne manuelles Parsen ausführt. Die zentrale Erkenntnis ist, dass der Kalender *vor* dem Laden definiert werden muss; sobald das Arbeitsbuch im Speicher ist, wurden die Daten bereits als richtige `DateTime`‑Objekte materialisiert.

### Was kommt als Nächstes?

- **Batch processing**: Durchlaufen Sie einen Ordner mit Dateien und rufen Sie für jede `LoadWithCalendar` auf.
- **Export to other formats**: Verwenden Sie `workbook.Save("output.csv")` nach der Konvertierung.
- **Localization**: Kombinieren Sie `CultureInfo` mit `DateTime.ToString`, um Daten in der bevorzugten Sprache des Benutzers anzuzeigen.

Fühlen Sie sich frei zu experimentieren – tauschen Sie `CalendarType.Japanese` gegen `CalendarType.Hijri` oder `CalendarType.Gregorian` aus und beobachten Sie, wie derselbe Code sich automatisch anpasst. Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar oder prüfen Sie die Aspose.Cells‑Dokumentation für tiefere API‑Einblicke.

Viel Spaß beim Coden und genießen Sie es, diese mysteriösen japanischen Ära‑Daten in saubere .NET `DateTime`‑Werte zu verwandeln!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}