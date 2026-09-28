---
category: general
date: 2026-04-07
description: Datum und Uhrzeit in Excel mit C# schreiben. Erfahre, wie du ein Datum
  in ein Arbeitsblatt einfügst, den Excel‑Zellwert für das Datum handhabst und das
  japanische Kalenderdatum in nur wenigen Schritten konvertierst.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: de
og_description: Datum/Zeit schnell in Excel schreiben. Dieser Leitfaden zeigt, wie
  man ein Datum in ein Arbeitsblatt einfügt, den Excel‑Zellwert für das Datum verwaltet
  und das japanische Kalenderdatum mit C# konvertiert.
og_title: Datum und Uhrzeit in Excel schreiben – Schritt‑für‑Schritt C#‑Tutorial
tags:
- C#
- Excel automation
- Aspose.Cells
title: Datum und Uhrzeit in Excel schreiben – Vollständiger Leitfaden für C#‑Entwickler
url: /de/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum/Zeit in Excel schreiben – Vollständiger Leitfaden für C#‑Entwickler

Haben Sie jemals **Datum/Zeit in Excel schreiben** müssen, waren sich aber nicht sicher, welcher API‑Aufruf tatsächlich ein korrektes Excel‑Datum speichert? Sie sind nicht der Einzige. In vielen Unternehmens‑Tools müssen wir ein C# `DateTime` in eine Tabelle einfügen, und das Ergebnis sollte sich wie ein echtes Excel‑Datum verhalten – sortierbar, filterbar und bereit für Pivot‑Tabellen.  

In diesem Tutorial gehen wir die genauen Schritte durch, um *Datum in ein Arbeitsblatt einzufügen* mit Aspose.Cells, erklären, warum das Festlegen der Kultur wichtig ist, und zeigen sogar, wie man **japanisches Kalenderdatum** in ein reguläres `DateTime` konvertiert, bevor Sie es schreiben. Am Ende haben Sie ein eigenständiges Snippet, das Sie in jedes .NET‑Projekt kopieren und einfügen können.

## Was Sie benötigen

- **.NET 6+** (oder jede aktuelle .NET‑Version; der Code funktioniert auch unter .NET Framework)  
- **Aspose.Cells for .NET** – ein NuGet‑Paket, das Ihnen ermöglicht, Excel‑Dateien zu manipulieren, ohne dass Office installiert sein muss.  
- Grundlegendes Verständnis von C# `DateTime` und Kulturen.  

Keine zusätzlichen Bibliotheken, kein COM‑Interop und keine Excel‑Installation erforderlich. Wenn Sie bereits eine Arbeitsblatt‑Instanz (`ws`) haben, können Sie loslegen.

## Schritt 1: Japanische Kultur einrichten (Japanisches Kalenderdatum konvertieren)

Wenn Sie ein Datum wie `"R02/05/01"` (Reiwa 2, 1. Mai) erhalten, müssen Sie .NET mitteilen, wie die Ära‑Symbole zu interpretieren sind. Der japanische Kalender ist nicht der standardmäßige Gregorianische Kalender, daher erstellen wir ein `CultureInfo`, das seinen Kalender durch `JapaneseCalendar` ersetzt.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Warum das wichtig ist:**  
Wenn Sie die Zeichenkette mit der Standardkultur parsen, wirft .NET eine FormatException, weil es `R` (die Reiwa‑Ära) nicht einem Jahr zuordnen kann. Durch das Ersetzen durch `JapaneseCalendar` versteht der Parser die Ära‑Symbole und übersetzt sie in das korrekte Gregorianische Jahr.

## Schritt 2: Die ära‑basierte Zeichenkette in ein `DateTime` parsen

Jetzt, da die Kultur bereit ist, können wir sicher `DateTime.ParseExact` aufrufen. Der Formatstring `"ggyy/MM/dd"` sagt dem Parser:

- `gg` – Ära‑Bezeichner (z. B. `R` für Reiwa)  
- `yy` – zweistelliges Jahr innerhalb der Ära  
- `MM/dd` – Monat und Tag.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Pro‑Tipp:** Wenn Sie möglicherweise Daten in anderen Formaten erhalten (z. B. `"Heisei 30/12/31"`), wickeln Sie das Parsen in ein `try/catch` ein und greifen Sie auf `DateTime.TryParseExact` zurück. Das verhindert, dass Ihr gesamter Importvorgang bei einer einzigen fehlerhaften Zeile abstürzt.

## Schritt 3: Das `DateTime` in eine Excel‑Zelle schreiben (Excel‑Zellwert für Datum)

Aspose.Cells behandelt ein .NET `DateTime` als natives Excel‑Datum, wenn Sie `PutValue` verwenden. Die Bibliothek konvertiert die Ticks automatisch in die Excel‑Seriennummer (die Anzahl der Tage seit dem 1900‑01‑00). Das bedeutet, dass die Zelle einen korrekten **Excel‑Zellwert für Datum** anzeigt und Sie sie später mit den integrierten Datumsformaten von Excel formatieren können.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Was Sie in Excel sehen werden:**  
Zelle C1 enthält nun die Seriennummer `44796`, die Excel als `2020‑05‑01` darstellt (oder in welchem Format Sie auch immer angewendet haben). Der zugrunde liegende Wert ist ein echtes Datum, kein String, sodass das Sortieren wie erwartet funktioniert.

## Schritt 4: Arbeitsmappe speichern (Abschluss)

Wenn Sie die Arbeitsmappe noch nicht gespeichert haben, tun Sie es jetzt. Dieser Schritt dreht sich nicht ausschließlich um das Schreiben des Datums/Zeit, aber er vervollständigt den Arbeitsablauf.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Das war's – vier prägnante Schritte, und Sie haben erfolgreich **Datum/Zeit in Excel geschrieben**, wobei Sie ein japanisches Ära‑Datum verarbeitet haben.

---

![Beispiel für das Schreiben von Datum/Zeit in Excel](/images/write-datetime-to-excel.png "Screenshot, der ein C#‑Projekt zeigt, das ein DateTime in die Excel‑Zelle C1 schreibt")

*Das obige Bild veranschaulicht die endgültige Excel‑Datei, in der das Datum korrekt in Zelle C1 angezeigt wird.*

## Häufige Fragen & Sonderfälle

### Was ist, wenn die Arbeitsblatt‑Variable noch nicht bereit ist?

Sie können eine neue Arbeitsmappe on the fly erstellen:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Wie bewahre ich die ursprüngliche japanische Ära‑Zeichenkette im Blatt auf?

Wenn Sie sowohl die ursprüngliche Zeichenkette als auch das geparste Datum benötigen, schreiben Sie sie in benachbarte Zellen:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Funktioniert das mit älteren .NET‑Versionen?

Ja. `JapaneseCalendar` existiert seit .NET 2.0, und Aspose.Cells unterstützt .NET Framework 4.5+. Stellen Sie lediglich sicher, dass Sie die richtige Assembly referenzieren.

### Was ist mit Zeitzonen?

`DateTime.ParseExact` gibt einen **Kind** von `Unspecified` zurück. Wenn Ihre Quelldaten UTC sind, konvertieren Sie sie zuerst:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Kann ich ein benutzerdefiniertes Datumsformat festlegen (z. B. „yyyy年MM月dd日“)?

Absolut. Verwenden Sie die `Style.Custom`‑Eigenschaft:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Jetzt zeigt Excel `2020年05月01日` an, während es weiterhin einen echten Datumswert speichert.

## Zusammenfassung

Wir haben alles behandelt, was Sie benötigen, um **Datum/Zeit in Excel** aus C# zu **schreiben**:

1. **Konfigurieren** Sie eine japanische Kultur mit `JapaneseCalendar`, um **japanische Kalenderdaten**‑Zeichenketten zu **konvertieren**.  
2. **Parsen** Sie die ära‑basierte Zeichenkette mit `DateTime.ParseExact`.  
3. **Fügen** Sie das resultierende `DateTime` in eine Zelle ein und stellen Sie einen korrekten **Excel‑Zellwert für Datum** sicher.  
4. **Speichern** Sie die Arbeitsmappe, damit die Daten erhalten bleiben.

Mit diesen vier Schritten können Sie sicher **Datum in ein Arbeitsblatt einfügen**, unabhängig vom Quellformat. Der Code ist vollständig ausführbar, erfordert nur Aspose.Cells und funktioniert auf jeder modernen .NET‑Runtime.

## Was kommt als Nächstes?

- **Massenimport:** Durchlaufen Sie Zeilen in einer CSV, parsen Sie jedes japanische Datum und schreiben Sie sie in aufeinanderfolgende Zellen.  
- **Styling:** Wenden Sie bedingte Formatierung an, um überfällige Termine hervorzuheben.  
- **Performance:** Nutzen Sie `WorkbookDesigner` oder `CellStyle`‑Caching, wenn Sie mit Tausenden von Zeilen arbeiten.  

Fühlen Sie sich frei zu experimentieren – tauschen Sie die japanische Ära gegen den Gregorianischen Kalender aus, ändern Sie die Zielzelle oder geben Sie in ein anderes Dateiformat aus (CSV, ODS). Die Kernidee bleibt dieselbe: parsen, konvertieren und **Datum/Zeit in Excel schreiben** mit Zuversicht.

Viel Spaß beim Programmieren, und möge Ihre Tabellen immer korrekt sortieren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}