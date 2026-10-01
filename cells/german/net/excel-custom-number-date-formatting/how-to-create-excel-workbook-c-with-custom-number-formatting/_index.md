---
category: general
date: 2026-10-01
description: Erfahren Sie, wie Sie in C# eine Excel‑Arbeitsmappe erstellen, ein benutzerdefiniertes
  Zahlenformat anwenden, die Dezimalstellen einer Zelle festlegen und die Arbeitsmappe
  als XLSX speichern – in einer vollständigen Schritt‑für‑Schritt‑Anleitung.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: de
lastmod: 2026-10-01
og_description: Erstellen Sie eine Excel-Arbeitsmappe in C# mit benutzerdefiniertem
  Zahlenformat, setzen Sie die Dezimalstellen der Zelle und speichern Sie die Arbeitsmappe
  als XLSX. Folgen Sie dieser vollständigen Anleitung für präzise numerische Ausgaben.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Excel-Arbeitsmappe in C# erstellen – benutzerdefiniertes Zahlenformat &
  XLSX-Export
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Wie man ein Excel‑Arbeitsbuch in C# mit benutzerdefinierter Zahlenformatierung
  erstellt
url: /de/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Excel‑Arbeitsbuch in C# mit benutzerdefiniertem Zahlenformat erstellt

Wenn Sie **ein Excel‑Arbeitsbuch in C#** erstellen müssen, das Zahlen genau so anzeigt, wie Sie es wünschen, zeigt Ihnen dieses Tutorial in wenigen klaren Schritten, wie das geht. Sie lernen, ein benutzerdefiniertes Zahlenformat anzuwenden, Dezimalstellen einer Zelle festzulegen und schließlich **das Arbeitsbuch als xlsx zu speichern** für die Weiterverwendung.

Die Arbeit mit numerischen Daten erfordert oft ein Gleichgewicht zwischen Präzision und Lesbarkeit. Am Ende dieses Tutorials haben Sie ein wiederverwendbares Muster, das angezeigte Ziffern auf eine bestimmte Anzahl signifikanter Stellen begrenzt, während der ursprüngliche Wert in der Datei erhalten bleibt. Es werden keine externen Skripte benötigt – nur C# und die Aspose.Cells-Bibliothek.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 SDK oder neuer installiert  
* Visual Studio 2022 (oder jede C#‑IDE)  
* Das **Aspose.Cells for .NET** NuGet‑Paket (`Install-Package Aspose.Cells`) – diese Bibliothek stellt die in den Beispielen verwendeten Klassen `Workbook`, `Worksheet` und `ExportTableOptions` bereit.  

Diese Anforderungen sind minimal; derselbe Code funktioniert in .NET Core, .NET Framework und sogar in Azure Functions.

## Schritt 1: Excel‑Arbeitsbuch in C# erstellen – Datei initialisieren

Der erste Vorgang besteht darin, ein neues `Workbook`‑Objekt zu instanziieren. Dieses Objekt repräsentiert die gesamte Excel‑Datei im Speicher und enthält automatisch ein Standard‑Arbeitsblatt.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Warum das wichtig ist:**  
Das vorzeitige Erstellen des Arbeitsbuchs gibt Ihnen eine leere Leinwand. Das Standard‑Arbeitsblatt (`Worksheets[0]`) ist bereit für die Dateneingabe, sodass Sie kein neues Blatt hinzufügen müssen, es sei denn, Ihr Szenario erfordert mehrere Registerkarten.

## Schritt 2: Numerischen Wert in eine Zelle schreiben

Jetzt fügen Sie eine Beispielzahl in die Zelle **A1** ein. Der von uns verwendete Wert (`123.456789`) enthält mehr Dezimalstellen, als wir schließlich anzeigen möchten, was uns später das Runden demonstrieren lässt.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tipp:** `PutValue` erkennt den Datentyp automatisch, sodass Sie die Zahl nicht in einen String konvertieren müssen.

## Schritt 3: Benutzerdefiniertes Zahlenformat anwenden – sichtbare Dezimalstellen begrenzen

Um zu steuern, wie Excel die Zahl anzeigt, erstellen wir ein `Style` mit einem **benutzerdefinierten Zahlenformat**. Das Muster `"0.######"` weist Excel an, bis zu sechs Dezimalstellen anzuzeigen, aber nachfolgende Nullen wegzulassen.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Wie das funktioniert:**  
Die Formatzeichenfolge folgt der benutzerdefinierten Format‑Syntax von Excel. `0` erzwingt eine Ziffer, während `#` eine Ziffer nur anzeigt, wenn sie signifikant ist. Durch die Kombination erhalten Sie eine flexible Anzeige, die dennoch die ursprüngliche Genauigkeit beibehält.

## Schritt 4: Dezimalstellen einer Zelle festlegen – mit ExportTableOptions

Wenn Sie **Dezimalstellen einer Zelle** für exportierte Daten festlegen müssen (z. B. beim Konvertieren in ein DataTable), ermöglicht Aspose.Cells die Angabe der Anzahl **signifikanter Stellen**. Dieser Schritt stellt sicher, dass die exportierte CSV‑ oder DataTable‑Datei dieselben Rundungsregeln wie im Arbeitsbuch anwendet.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Warum `SignificantDigits` verwenden?**  
Im Gegensatz zu einer festen Dezimalanzahl bewahren signifikante Stellen die Größenordnung der Zahl, während sie die Präzision begrenzen – das ist häufig das, was Analysten bei der Datenzusammenfassung erwarten.

## Schritt 5: Arbeitsblattdaten exportieren und **Arbeitsbuch als xlsx speichern**

Abschließend exportieren Sie die Daten (falls Sie ein DataTable benötigen) und speichern das Arbeitsbuch auf dem Datenträger. Der Aufruf `ExportDataTable` berücksichtigt die konfigurierten `ExportTableOptions`, und `workbook.Save` schreibt eine standardmäßige XLSX‑Datei.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Erwartetes Ergebnis:**  
Wenn Sie *SigDigits.xlsx* in Excel öffnen, zeigt die Zelle **A1** `123.5`. Der zugrunde liegende Wert bleibt `123.456789`, aber die angezeigte Zahl folgt der 4‑signifikanten‑Stellen‑Regel. Wenn Sie das Blatt in ein DataTable exportieren, wird der Wert in der Tabelle ebenfalls auf `123.5` gerundet.

## Benutzerdefiniertes Zahlenformat auf weitere Zellen anwenden

Wenn Sie einen Bereich statt einer einzelnen Zelle formatieren müssen, verwenden Sie das `Style`‑Objekt erneut:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro‑Tipp:** Das Wiederverwenden eines Style‑Objekts reduziert den Speicherverbrauch und garantiert eine konsistente Formatierung über das gesamte Blatt hinweg.

## Wie man Zahlen in Excel mit C# formatiert – gängige Varianten

| Szenario | Formatzeichenfolge | Ergebnis |
|----------|--------------------|----------|
| Fest, zwei Dezimalstellen | `"0.00"` | `123.46` |
| Währung (US) | `"$#,##0.00"` | `$123.46` |
| Prozent mit einer Dezimalstelle | `"0.0%"` | `12,346.0%` |
| Wissenschaftliche Notation | `"0.00E+00"` | `1.23E+02` |

Wählen Sie das Muster, das Ihren Berichtsanforderungen entspricht. Alle Muster sind mit der zuvor gezeigten `Style.Custom`‑Eigenschaft kompatibel.

## Dezimalstellen einer Zelle dynamisch basierend auf Benutzereingabe festlegen

Manchmal ist die erforderliche Präzision zur Compile‑Zeit nicht bekannt. Sie können die Formatzeichenfolge zur Laufzeit erstellen:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Randfall:** Wenn `decimals` null ist, wird das Format zu `"0"` (Ganzzahldarstellung). Validieren Sie stets die Benutzereingabe, um fehlerhafte Formatzeichenfolgen zu vermeiden.

## Arbeitsbuch als XLSX speichern – bewährte Methoden

* **Verwenden Sie absolute Pfade**, wenn Sie in ein bekanntes Verzeichnis schreiben (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Entsorgen** Sie das `Workbook`, wenn Sie es in einer `using`‑Anweisung einbetten, um nicht verwaltete Ressourcen sofort freizugeben:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Versionskompatibilität:** Aspose.Cells schreibt Dateien, die mit Excel 2010‑2023 kompatibel sind, sodass nachgelagerte Benutzer keine Formatprobleme erleben.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige Programm, das Sie sofort kopieren, einfügen und ausführen können. Es enthält alle notwendigen `using`‑Direktiven, Kommentare und Fehlerbehandlungen.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Verifizierungsschritte**

1. Programm ausführen (`dotnet run`).  
2. Öffnen Sie `SigDigits.xlsx`.  
3. Bestätigen Sie, dass **A1** `123.5` anzeigt.  
4. Wenn Sie die XML‑Datei des Dokuments öffnen (`.xlsx` ist ein ZIP‑Archiv), sehen Sie das benutzerdefinierte Format `"0.######"` im `s`‑Attribut des `<c>`‑Elements.

## Fazit

In diesem Tutorial haben Sie gelernt, wie man **ein Excel‑Arbeitsbuch in C# erstellt**, **ein benutzerdefiniertes Zahlenformat anwendet**, **Dezimalstellen einer Zelle festlegt** und **das Arbeitsbuch als xlsx speichert** mit Aspose.Cells. Die Lösung demonstriert sowohl die visuelle Formatierung in Excel als auch das Runden beim Datenexport über `ExportTableOptions`.

Ab hier können Sie:

* Den Ansatz auf ganze Bereiche oder Tabellen ausweiten.  
* Mehrere Stile (Schriften, Rahmen) mit `StyleFlag` kombinieren.  
* Die Berichtserstellung automatisieren, indem Sie über Datenquellen iterieren und dieselbe Formatierungslogik anwenden.  

Probieren Sie gern verschiedene Formatzeichenfolgen, Dezimalzahlen oder Exportoptionen aus, um Ihre spezifischen Berichtsanfordernisse zu erfüllen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel‑Arbeitsbuch in C# erstellen – Währungsformat anwenden und DataTable importieren](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Excel‑Arbeitsbuch in C# erstellen – Schritt‑für‑Schritt‑Leitfaden mit bedingter Formatierung](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Excel‑Arbeitsbuch in C# erstellen – Kommentar hinzufügen & als XLSX speichern](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}