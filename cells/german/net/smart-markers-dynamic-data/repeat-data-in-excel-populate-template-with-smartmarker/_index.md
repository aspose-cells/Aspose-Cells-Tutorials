---
category: general
date: 2026-02-21
description: Daten in Excel schnell wiederholen mit SmartMarker – erfahren Sie, wie
  Sie Excel‑Vorlagen befüllen und Zeilen mühelos wiederholen.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: de
og_description: Daten in Excel mit SmartMarker wiederholen. Erfahren Sie, wie Sie
  Excel-Vorlagen befüllen, Zeilen wiederholen und Ihre Tabellen automatisieren.
og_title: Daten in Excel wiederholen – Vorlage mit SmartMarker füllen
tags:
- excel
- csharp
- smartmarker
- automation
title: Daten in Excel wiederholen – Vorlage mit SmartMarker füllen
url: /de/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

produce final content with translations. Ensure no extra explanation.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Daten in Excel wiederholen – Vorlage mit SmartMarker füllen

Haben Sie jemals **Daten in Excel wiederholen** müssen, wussten aber nicht, wie Sie manuelles Kopieren‑Einfügen vermeiden können? Sie sind nicht allein. In vielen Reporting‑Szenarien haben Sie eine Liste von Elementen, die automatisch in Zeilen erweitert werden muss, und das manuell zu erledigen ist ein Rezept für Fehler.

Der springende Punkt – die Verwendung des SmartMarkerProcessor aus der **GemBox.Spreadsheet**‑Bibliothek ermöglicht es Ihnen, eine **Excel‑Vorlage** mit einer einzigen Zeile C# zu **befüllen** und Zeilen für jedes Element in Ihrer Sammlung zu wiederholen. In diesem Leitfaden gehen wir die genauen Schritte durch, zeigen Ihnen den vollständigen Code und erklären, warum jedes Element wichtig ist, damit Sie Zeilen in Excel mühelos wiederholen können.

## Was Sie lernen werden

* Wie man die Datenstruktur definiert, die den Wiederholungs‑Vorgang steuert.  
* Wie man einen `SmartMarkerProcessor` an eine Arbeitsmappe anhängt, die ein verstecktes Vorlagen‑Blatt enthält.  
* Wie der Marker `${Repeat:Item}` automatisch in mehrere Zeilen expandiert.  
* Tipps zum Umgang mit Randfällen wie leeren Sammlungen oder benutzerdefinierten Formatierungen.  

Am Ende dieses Tutorials können Sie **Excel aus Daten befüllen** auf eine skalierbare Weise, die leicht zu warten ist und mit jedem .NET‑Projekt funktioniert.

---

## Voraussetzungen

* .NET 6.0 oder höher (der Code verwendet moderne C#‑Features).  
* Das **GemBox.Spreadsheet**‑NuGet‑Paket (die kostenlose Version funktioniert für bis zu 150 Zeilen).  
* Eine einfache Excel‑Vorlagendatei (`Template.xlsx`) mit einem versteckten Blatt namens `HiddenTemplate`.  
* Kenntnisse in C#‑Objekten und LINQ sind hilfreich, aber nicht erforderlich.

---

## Schritt 1 – Datenstruktur für die Wiederholung definieren

Zuerst benötigen Sie eine Datenquelle, über die die SmartMarker‑Engine iterieren kann. In den meisten realen Anwendungen stammt diese aus einer Datenbank, einer API oder einer CSV‑Datei. Der Übersicht halber verwenden wir einen anonymen Typ mit einer einzigen Eigenschaft namens `Item`, die ein Array von Zeichenketten enthält.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Warum das wichtig ist:** Der Marker `${Repeat:Item}` in der Excel‑Vorlage sucht nach einer Eigenschaft namens `Item`. Wenn Sie die Eigenschaft umbenennen, passen Sie den Marker entsprechend an. Diese enge Kopplung stellt sicher, dass die Vorlage mit Ihrem Code synchron bleibt, was das **Befüllen von Excel‑Vorlagen** erleichtert, ohne Spaltennamen raten zu müssen.

### Häufige Variationen

* **Komplexe Objekte:** Statt eines einfachen Zeichenketten‑Arrays können Sie eine Liste von Objekten bereitstellen (`new[] { new { Name = "A", Qty = 10 } }`). Der Marker wiederholt die Zeilen und Sie können `${Item.Name}` und `${Item.Qty}` im Blatt referenzieren.  
* **Leere Sammlungen:** Wenn `Item` leer ist, entfernt SmartMarker einfach den Wiederholungsblock und lässt die Vorlage unverändert – ideal für optionale Abschnitte.

---

## Schritt 2 – SmartMarkerProcessor für das versteckte Vorlagenblatt erstellen

Als Nächstes laden Sie Ihre Arbeitsmappe und instanziieren einen `SmartMarkerProcessor`. Zeigen Sie ihn auf die Arbeitsmappe, die das versteckte Vorlagenblatt enthält; SmartMarker kopiert dieses Blatt in ein sichtbares und erweitert die Wiederholungs‑Marker.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro‑Tipp:** Wenn Sie mehrere Vorlagen in derselben Datei haben, können Sie beim Aufruf von `processor.Process` den Namen des Quellblatts angeben. Das hilft, wenn Sie **Zeilen in Excel wiederholen** müssen für verschiedene Abschnitte eines Berichts.

### Umgang mit Randfällen

* **Fehlendes Vorlagenblatt:** Wickeln Sie das Laden in ein try/catch und protokollieren Sie einen klaren Fehler – das verhindert stille Fehlfunktionen, wenn der Dateipfad falsch ist.  
* **Große Datensätze:** Bei tausenden Zeilen sollten Sie erwägen, die Ausgabe in eine Datei zu streamen (`processor.Save`), anstatt alles im Speicher zu halten.

---

## Schritt 3 – Daten anwenden und den Marker `${Repeat:Item}` expandieren

Jetzt kommt die magische Zeile, die tatsächlich die Zeilen wiederholt. Übergeben Sie das in Schritt 1 erstellte Objekt an `processor.Process`. SmartMarker findet jeden `${Repeat:Item}`‑Marker, dupliziert die Zeile für jedes Element und ersetzt Platzhalter durch die tatsächlichen Werte.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Was Sie sehen sollten

Wenn Sie `Result.xlsx` öffnen, wurde das versteckte Vorlagenblatt in ein neues sichtbares Blatt kopiert (standardmäßig `Sheet1` genannt). Die Zeile, die `${Repeat:Item}` enthielt, erscheint nun dreimal, wobei die Zellen **A**, **B** und **C** jeweils anzeigen.

| Artikel |
|---------|
| A |
| B |
| C |

Wenn Sie weitere Spalten wie `${Item.Price}` hinzugefügt haben, würden diese automatisch aus der Datenquelle ausgefüllt.

---

## Wie man Zeilen in Excel ohne SmartMarker wiederholt (schneller Vergleich)

| Vorgehensweise               | Code‑Komplexität | Wartung | Leistung |
|------------------------------|------------------|---------|----------|
| Manuelles Kopieren‑Einfügen  | Hoch             | Niedrig | Schlecht |
| VBA‑Makro                    | Mittel           | Mittel  | Gut      |
| **SmartMarkerProcessor**     | Niedrig          | Hoch    | Ausgezeichnet |

Wie Sie sehen, bietet die Verwendung von SmartMarker zum **Wiederholen von Daten in Excel** die sauberste Trennung zwischen Vorlagendesign und Geschäftslogik. Es ist zudem sprachunabhängig – ähnliche Konzepte existieren in Java-, Python- und JavaScript‑Bibliotheken.

---

## Fortgeschrittene Tipps & häufige Fallstricke

### 1. Formatierung der wiederholten Zeilen

SmartMarker kopiert die gesamte Zeile – einschließlich Zellstile, Rahmen und bedingte Formatierung. Wenn Sie für die erste oder letzte Zeile einen anderen Stil benötigen, fügen Sie zusätzliche Marker wie `${If:Item.IsFirst}` hinzu und verwenden Sie bedingte Formeln in Excel.

### 2. Umgang mit großen Datensätzen

Bei der Arbeit mit > 10 000 Zeilen deaktivieren Sie die automatische Berechnung von Excel vor der Verarbeitung:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Aktivieren Sie sie nach dem Speichern wieder, um die Leistung flott zu halten.

### 3. Excel aus Daten einer echten Datenbank befüllen

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Verwenden Sie dann `${Repeat:Order}` in der Vorlage, um jede Bestellung aufzulisten. Dieses Muster zeigt, wie einfach es ist, **Excel aus Daten zu befüllen** direkt aus Entity Framework.

### 4. Verwendung mehrerer Wiederholungsblöcke

Sie können mehrere `${Repeat:...}`‑Marker im selben Blatt oder in verschiedenen Blättern haben. SmartMarker verarbeitet sie sequenziell, sodass die Reihenfolge nur wichtig ist, wenn ein Block vom Ergebnis eines anderen abhängt.

---

## Vollständiges ausführbares Beispiel

Unten finden Sie eine eigenständige Konsolenanwendung, die Sie in Visual Studio einfügen und sofort ausführen können. Sie demonstriert alle drei Schritte sowie das Speichern der Datei.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Erwartete Ausgabe:** `Result.xlsx` enthält ein Blatt, in dem die Zeile mit `${Repeat:Item}` dreimal erscheint und A, B sowie C anzeigt. Keine manuellen Anpassungen erforderlich.

---

## Fazit

Sie wissen jetzt, wie Sie **Daten in Excel** effizient wiederholen können, indem Sie den SmartMarkerProcessor nutzen. Durch das Definieren eines einfachen Datenobjekts, das Laden einer Vorlagenarbeitsmappe und den Aufruf von `Process` können Sie **Excel‑Vorlage befüllen**, **Zeilen in Excel wiederholen** und im Allgemeinen **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}