---
category: general
date: 2026-03-30
description: Erfahren Sie, wie Sie Zahlen mit Trennzeichen mithilfe von Aspose.Cells
  in C# formatieren. Enthält das Festlegen eines benutzerdefinierten Zahlenformats,
  das Hinzufügen eines Tausendertrennzeichens, das Formatieren von Dezimalstellen
  und das Formatieren von Zellen.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: de
og_description: Zahlen mit Trennzeichen in C# formatieren. Dieser Leitfaden zeigt,
  wie man ein benutzerdefiniertes Zahlenformat festlegt, Tausendertrennzeichen hinzufügt,
  Dezimalstellen formatiert und Zellen mit Aspose.Cells formatiert.
og_title: Zahl mit Trennzeichen in C# formatieren – Aspose.Cells Tutorial
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Zahlen mit Trennzeichen in C# formatieren – Vollständiger Aspose.Cells‑Leitfaden
url: /de/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zahl mit Trennzeichen in C# formatieren – Vollständiger Aspose.Cells Leitfaden

Haben Sie schon einmal **Zahl mit Trennzeichen** in einer Tabelle formatieren müssen, wussten aber nicht, welchen API‑Aufruf Sie verwenden sollten? Sie sind nicht allein – Entwickler kämpfen ständig mit Tausendertrennzeichen, Dezimalstellen und benutzerdefinierten Mustern beim Export von Daten.  

Gute Nachricht: Aspose.Cells macht das kinderleicht. In diesem Tutorial gehen wir ein praxisnahes Beispiel durch, das **ein benutzerdefiniertes Zahlenformat setzt**, **ein Tausendertrennzeichen hinzufügt**, **Dezimalstellen formatiert** und zeigt, **wie man die Zelle** als Zeichenkette ausgibt. Am Ende haben Sie ein einsatzbereites Snippet, das Sie in jedes .NET‑Projekt einfügen können.

## Was dieser Leitfaden abdeckt

* Das genaue NuGet‑Paket, das Sie benötigen, und wie Sie es installieren.  
* Schritt‑für‑Schritt‑Code, der ein Workbook erstellt, einen numerischen Wert schreibt und ein benutzerdefiniertes Format anwendet.  
* Warum `ExportTableOptions.ExportAsString` der bevorzugte Weg ist, um einen formatierten Wert abzurufen.  
* Häufige Stolperfallen – z. B. das Vergessen, `ExportAsString` zu aktivieren, oder die Verwendung einer falschen Formatmaske.  
* Wie Sie die Formatmaske anpassen, wenn Sie eine andere Anzahl von Dezimalstellen oder einen anderen Trennzeichenstil benötigen.

Keine externen Dokumentations‑Links nötig; alles, was Sie brauchen, finden Sie hier. Lassen Sie uns loslegen.

---

## Voraussetzungen

| Anforderung | Grund |
|-------------|-------|
| .NET 6.0 oder höher | Aspose.Cells 23.10+ zielt auf .NET Standard 2.0+ ab, daher ist .NET 6 sicher und aktuell. |
| Visual Studio 2022 (oder jede C#‑IDE) | Erleichtert Debugging und Paketverwaltung. |
| Aspose.Cells for .NET NuGet‑Paket | Stellt die Klassen `Workbook`, `Worksheet` und `ExportTableOptions` bereit, die wir verwenden werden. |

Sie können das Paket über die Package Manager Console installieren:

```powershell
Install-Package Aspose.Cells
```

Das war’s – keine zusätzlichen DLLs, kein COM‑Interop, nur ein einziger NuGet‑Verweis.

---

## Schritt 1: Neues Workbook initialisieren (Wie man Zelle formatiert)

Das Erste, was wir tun, ist eine frische `Workbook`‑Instanz zu erstellen. Stellen Sie sich das vor wie eine leere Excel‑Datei, die bereit ist, Daten zu erhalten.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Warum das wichtig ist:** `Workbook` ist der Einstiegspunkt für jede Operation in Aspose.Cells. Indem wir das erste Arbeitsblatt (`Worksheets[0]`) holen, erhalten wir eine saubere Leinwand, ohne ein Blatt benennen zu müssen.

---

## Schritt 2: Numerischen Wert in die Zielzelle schreiben

Als Nächstes setzen wir eine rohe Zahl in Zelle **A1**. Der Wert selbst ist noch nicht formatiert – es ist einfach ein `double`.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro‑Tipp:** Verwenden Sie `PutValue` statt `PutString`, wenn Sie später eine numerische Formatierung anwenden wollen. Das bewahrt den zugrunde liegenden Datentyp und ermöglicht Excel‑kompatible Berechnungen.

---

## Schritt 3: Benutzerdefiniertes Zahlenformat setzen (Tausendertrennzeichen hinzufügen & Dezimalstellen formatieren)

Jetzt kommt der Kern des Tutorials: Definition einer Formatmaske, die Aspose.Cells sagt, wie die Zahl angezeigt werden soll. Die Maske `#,##0.00` bewirkt drei Dinge:

1. **`#,##0`** – fügt ein Tausendertrennzeichen (standardmäßig Komma) hinzu.  
2. **`.00`** – erzwingt exakt zwei Dezimalstellen.  

Wenn Sie eine andere Anzahl von Dezimalstellen benötigen, ändern Sie einfach die Anzahl der `0` hinter dem Dezimalpunkt.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Warum wir `ExportAsString` verwenden:** Standardmäßig gibt `ExportString` den Rohwert zurück. Durch Setzen von `ExportAsString = true` zwingt man die API, die `NumberFormat`‑Maske anzuwenden, bevor sie in Text umgewandelt wird. Das ist entscheidend, wenn Sie die exakte Zeichenketten‑Darstellung für Berichte, JSON‑Payloads oder UI‑Anzeige benötigen.

---

## Schritt 4: Formatierten Text exportieren (Wie man Zelle formatiert)

Mit den vorbereiteten Optionen rufen wir `ExportString` für dieselbe Zelle auf. Die Methode respektiert die gerade definierte Maske und liefert eine schön formatierte Zeichenkette zurück.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Beim Ausführen des Programms wird **`12,345.68`** in der Konsole ausgegeben – exakt das Format, das wir verlangt haben.

> **Randfall:** Hat die Ausgangszahl mehr als zwei Dezimalstellen, rundet die Maske. Wenn Sie stattdessen abschneiden wollen, müssen Sie den Wert vor dem Aufruf von `PutValue` mit `Math.Truncate` vorverarbeiten.

---

## Schritt 5: Format anpassen – Häufige Varianten

### 5.1 Dezimalpräzision ändern

Möchten Sie drei Dezimalstellen? Ersetzen Sie einfach die Maske:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Anderes Tausendertrennzeichen verwenden

Einige Regionen bevorzugen ein Leerzeichen oder einen Punkt. Sie können das Zeichen direkt einbetten:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Oder sich auf die Kultur‑Einstellungen des Workbooks verlassen:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Präfix oder Suffix (Währung, Prozent)

Fügen Sie ein Dollar‑ oder Prozentzeichen direkt in die Maske ein:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Hinweis:** Die Maske ist case‑sensitive. `$` und `%` sind literale Symbole; sie beeinflussen nicht den zugrunde liegenden numerischen Wert.

---

## Schritt 6: Vollständiges Beispiel (Kopieren‑und‑Einfügen bereit)

Unten finden Sie das komplette Programm, das Sie in eine neue Konsolen‑App kopieren können. Es enthält alle Schritte, Kommentare und die abschließende Ausgabe‑Verifikation.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Führen Sie das Programm aus (`dotnet run` im Terminal oder drücken Sie F5 in Visual Studio) und Sie sehen die formatierte Zahl exakt wie gezeigt.

---

## Häufig gestellte Fragen (FAQ)

**F: Funktioniert das mit älteren Excel‑Versionen?**  
A: Ja. Die Formatmaske folgt der nativen Excel‑Zahlenformat‑Syntax, sodass jede Version, die `#,##0.00` versteht, dieselbe Zeichenkette rendert.

**F: Was, wenn ich einen Zellbereich formatieren muss?**  
A: Durchlaufen Sie den gewünschten Bereich und wenden Sie dieselben `ExportTableOptions` auf jede Zelle an, oder setzen Sie die Eigenschaft `Style.Custom` für den Bereich und rufen Sie anschließend `ExportString` für eine einzelne Zelle auf.

**F: Kann ich direkt nach CSV exportieren, wobei diese Formate angewendet werden?**  
A: Absolut. Verwenden Sie `Workbook.Save("output.csv", SaveFormat.CSV);` nachdem Sie das Format für jede Zelle gesetzt haben. Aspose.Cells berücksichtigt den `Style` der Zelle beim Erzeugen von CSV.

---

## Fazit

Wir haben gezeigt, wie man **Zahl mit Trennzeichen** in C# mithilfe von Aspose.Cells formatiert, von **benutzerdefiniertem Zahlenformat setzen** über **Tausendertrennzeichen hinzufügen**, **Dezimalstellen formatieren** bis hin zum essenziellen **Wie man Zelle formatiert** für den String‑Export. Der Code ist vollständig eigenständig, funktioniert mit .NET 6+ und lässt sich für jede Kultur oder Präzisionsanforderung anpassen.

Als Nächstes könnten Sie:

* dieselbe Technik auf Datums‑ und Zeitwerte anwenden (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Bulk‑Exporte automatisieren, bei denen jede Spalte eine andere Maske benötigt.  
* Die formatierten Zeichenketten in PDF‑Berichte mit Aspose.Words integrieren.

Probieren Sie das aus, und Sie werden schnell zur Ansprechperson für Tabellen‑Formatierung in Ihrem Team. Viel Spaß beim Coden!   ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formatiertes Zahl mit Trennzeichen angezeigt in Aspose.Cells Ausgabe"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}