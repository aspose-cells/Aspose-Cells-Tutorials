---
category: general
date: 2026-04-07
description: Wenden Sie ein benutzerdefiniertes Zahlenformat auf eine Tabellenzelle
  an und erfahren Sie, wie Sie Zahlen in einer Tabelle formatieren, während Sie den
  Zellenwert mit C# exportieren. Schnelle, umfassende Anleitung.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: de
og_description: Wenden Sie ein benutzerdefiniertes Zahlenformat auf eine Tabellenzelle
  an und exportieren Sie es als formatierte Zeichenkette. Erfahren Sie, wie Sie Zahlen
  in einer Tabelle formatieren und den Zellenwert exportieren.
og_title: Benutzerdefiniertes Zahlenformat anwenden – Vollständiges C#‑Export‑Tutorial
tags:
- C#
- Spreadsheet
- Number Formatting
title: Benutzerdefiniertes Zahlenformat in C#‑Tabellenexport anwenden – Schritt‑für‑Schritt‑Anleitung
url: /de/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefiniertes Zahlenformat in C# Spreadsheet-Export anwenden – Vollständiges Tutorial

Schon einmal **custom number format** auf eine Zelle anwenden und dann diesen formatierten String aus einer Tabelle extrahieren müssen? Sie sind nicht allein. Viele Entwickler stoßen auf ein Problem, wenn sie feststellen, dass der Rohwert zurückkommt, anstatt des hübschen, lokalisierungsbewussten Strings, den sie erwarten. In diesem Leitfaden zeigen wir Ihnen genau, wie Sie numbers in spreadsheet cells formatieren und wie Sie den Zellenwert als formatierten String mit einer beliebten C#‑Spreadsheet‑Bibliothek exportieren.

Am Ende des Durchlaufs können Sie **custom number format** auf jede numerische Zelle anwenden, das Ergebnis mit `ExportTable` exportieren und die genaue Ausgabe sehen, die Sie in einer UI oder einem Bericht erwarten würden. Keine externen Dokumente nötig – alles ist hier.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch unter .NET Framework 4.7+)
- Ein Verweis auf die Spreadsheet‑Bibliothek, die `Workbook`, `Worksheet` und `ExportTableOptions` bereitstellt (z. B. **Aspose.Cells** oder **GemBox.Spreadsheet**; die gezeigte API entspricht Aspose.Cells)
- Grundkenntnisse in C# – wenn Sie ein `Console.WriteLine` schreiben können, sind Sie startklar

> **Profi‑Tipp:** Wenn Sie eine andere Bibliothek verwenden, sind die Eigenschaftsnamen meist ähnlich (`NumberFormat`, `ExportAsString`). Ordnen Sie sie einfach entsprechend zu.

## Was das Tutorial behandelt

1. Erstellen einer Arbeitsmappe und Auswählen des ersten Arbeitsblatts.  
2. Einfügen eines numerischen Werts in eine Zelle.  
3. Einrichten von `ExportTableOptions`, um **custom number format** anzuwenden und einen String zurückzugeben.  
4. Exportieren der Zelle und Ausgeben des formatierten Ergebnisses.  
5. Behandlung von Randfällen – was, wenn die Zelle eine Formel oder einen Nullwert enthält?

Los geht's.

![apply custom number format example](https://example.com/image.png "apply custom number format")

## Schritt 1 – Arbeitsmappe erstellen und das erste Arbeitsblatt abrufen

Das Erste, das Sie benötigen, ist ein Workbook‑Objekt. Denken Sie daran wie an die Excel‑Datei, die Sie in der Office‑App öffnen würden. Sobald Sie es haben, holen Sie sich das erste Blatt – die meisten Tutorials beginnen dort, weil es das Beispiel kompakt hält.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Warum das wichtig ist:** Eine neue Arbeitsmappe bietet Ihnen ein sauberes Blatt, sodass keine versteckte Formatierung später unser custom number format beeinträchtigt.

## Schritt 2 – Numerischen Wert in Zelle B2 einfügen (die Zelle, die wir exportieren werden)

Jetzt benötigen wir etwas zum Formatieren. Zelle **B2** ist ein praktischer Ort – leicht zu referenzieren und weit genug vom Standard‑A1‑Eckpunkt entfernt, um versehentliche Überschreibungen zu vermeiden.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Was, wenn der Wert eine Formel ist?**  
Wenn Sie später den Rohwert durch eine Formel ersetzen (z. B. `=SUM(A1:A10)`), wird die Export‑Routine das von uns im nächsten Schritt angewendete number format weiterhin berücksichtigen, weil die Formatierung an die Zelle und nicht an den Werttyp gebunden ist.

## Schritt 3 – Exportoptionen konfigurieren, um den Wert als formatierten String zu erhalten

Hier ist das Herzstück des Tutorials: Wir weisen die Bibliothek an, beim Export **custom number format** anzuwenden. Der `NumberFormat`‑String folgt dem gleichen Muster, das Sie in Excel unter der Kategorie „Benutzerdefiniert“ verwenden würden.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` stellt sicher, dass die Methode einen `string` statt eines rohen double zurückgibt.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` spiegelt das Excel‑Muster wider: Kommas für Tausender, zwei Dezimalstellen und Klammern für negative Zahlen.

> **Warum ein benutzerdefiniertes Format verwenden?** Es garantiert Konsistenz über Kulturen hinweg (z. B. US‑ vs. europäische Zahlentrenner) und ermöglicht es Ihnen, geschäftsspezifische Stile wie buchhalterische Klammern einzubetten.

## Schritt 4 – Zelle mit den konfigurierten Optionen exportieren

Jetzt holen wir tatsächlich den Wert aus dem Arbeitsblatt und lassen die Bibliothek das schwere Heben übernehmen, indem sie das von uns definierte Format anwendet.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Randfall – leere Zelle:** Wenn `B2` leer wäre, wäre `formattedResult` `null`. Sie können dies mit einer einfachen Null‑Prüfung vor dem Ausgeben abfangen.

## Schritt 5 – Formatierten String anzeigen

Abschließend schreiben wir das Ergebnis in die Konsole. In einer echten Anwendung könnten Sie diesen String in ein PDF, eine E‑Mail oder ein UI‑Label einfügen.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Erwartete Ausgabe**

```
1,234.56
```

Wenn Sie den Rohwert zu `-9876.54` ändern, liefert dasselbe Format `(9,876.54)` – genau das, was viele Buchhaltungsberichte benötigen.

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolenprojekt kopieren‑und‑einfügen können. Es kompiliert und läuft unverändert, vorausgesetzt, Sie haben das passende NuGet‑Paket für die Spreadsheet‑Bibliothek hinzugefügt.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Schnell‑Check

- **Kompiliert es?** Ja – stellen Sie nur sicher, dass die `Aspose.Cells` (oder äquivalente) DLL referenziert wird.  
- **Funktioniert es mit anderen Kulturen?** Der Format‑String ist kultur‑agnostisch; die Bibliothek respektiert das von Ihnen angegebene Muster. Wenn Sie lokalspezifische Trennzeichen benötigen, können Sie vor dem Export eine `CultureInfo`‑Behandlung hinzufügen.

## Häufige Fragen & Variationen

### Wie **format number in spreadsheet** mit einem anderen Muster anwenden?

Ersetzen Sie den `NumberFormat`‑String. Zum Beispiel, um einen Prozentsatz mit einer Dezimalstelle anzuzeigen:

```csharp
NumberFormat = "0.0%";
```

### Was, wenn ich **how to export cell value** als HTML statt als Klartext benötige?

Die meisten Bibliotheken besitzen eine Überladung, die einen Exporttyp akzeptiert. Sie würden `ExportAsString = true` setzen und `ExportHtml = true` (oder Ähnliches) hinzufügen. Das Prinzip bleibt gleich: Format definieren, dann die Ausgabe­darstellung wählen.

### Kann ich das Format auf einen gesamten Bereich anwenden, nicht nur auf eine Zelle?

Absolut. Sie können `NumberFormat` einem `Style`‑Objekt zuweisen und diesen Stil dann auf einen `Range` anwenden. Der Exportaufruf bleibt unverändert; er übernimmt den Stil automatisch.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Was passiert, wenn die Zelle eine Formel enthält?

Die Export‑Routine wertet zunächst die Formel aus und formatiert dann den resultierenden numerischen Wert. Kein zusätzlicher Code ist nötig – stellen Sie nur sicher, dass `Calculate` aufgerufen wurde, falls Sie die automatische Berechnung deaktiviert haben.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Fazit

Sie wissen jetzt, wie man **custom number format** auf eine Spreadsheet‑Zelle anwendet, **format number in spreadsheet** in Kontexten verwendet und **how to export cell value** als sofort anzeigbaren String exportiert. Das kompakte Code‑Beispiel oben deckt jeden Schritt ab – von der Erstellung der Arbeitsmappe bis zur finalen Ausgabe – sodass Sie es direkt in ein Produktionsprojekt einbinden können.

Bereit für die nächste Herausforderung? Versuchen Sie, diese Technik mit **how to format numeric cell** für Datumsangaben, Währungssymbole oder bedingte Formatierung zu kombinieren. Oder erkunden Sie den Export mehrerer Zellen als CSV, wobei das custom format jeder Zelle erhalten bleibt. Der Himmel ist die Grenze, und mit diesen Grundlagen haben Sie ein solides Fundament.

Viel Spaß beim Coden und vergessen Sie nicht zu experimentieren – manchmal tauchen die besten Lösungen auf, wenn Sie den Format‑String nur ein wenig anpassen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}