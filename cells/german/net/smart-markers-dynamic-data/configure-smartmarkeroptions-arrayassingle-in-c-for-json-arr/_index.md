---
category: general
date: 2026-09-21
description: Konfigurieren Sie SmartMarkerOptions ArrayAsSingle in C#, um JSON‑Arrays
  als einzelnen Zellenwert in einer Excel‑Arbeitsmappe zu exportieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: de
lastmod: 2026-09-21
og_description: Konfigurieren Sie SmartMarkerOptions ArrayAsSingle in C#, um JSON‑Arrays
  als einzelnen Zellenwert zu exportieren. Lernen Sie die komplette Schritt‑für‑Schritt‑Lösung.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: SmartMarkerOptions ArrayAsSingle in C# konfigurieren – vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: SmartMarkerOptions ArrayAsSingle in C# für JSON‑Arrays konfigurieren
url: /de/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarkerOptions ArrayAsSingle in C# für JSON-Arrays konfigurieren

Wenn Sie **SmartMarkerOptions ArrayAsSingle** beim Erstellen von Excel-Dateien mit Aspose.Cells konfigurieren müssen, zeigt Ihnen dieser Leitfaden genau, wie das geht. Sie sehen, wie Sie ein JSON-Array in einer Zelle intakt halten, anstatt seine Elemente über mehrere Zeilen zu verteilen.

Die Arbeit mit JSON-Daten in Tabellenkalkulationen bedeutet oft die Wahl zwischen einer abgeflachten Ansicht und einer kompakten Darstellung. In vielen Reporting‑Szenarien – z. B. beim Speichern einer Liste von Tags oder einer Menge von Kennungen – möchten Sie, dass der gesamte JSON‑String in einer einzigen Zelle bleibt. Das **ArrayAsSingle**‑Flag in `SmartMarkerOptions` macht das möglich.

In diesem Tutorial werden Sie:

* Einen `DataTable` erstellen, der ein JSON‑Array in einer Spalte enthält.
* Smart Markers in einem Excel‑Arbeitsblatt platzieren.
* **SmartMarkerOptions ArrayAsSingle** konfigurieren, sodass das JSON‑Array als einzelner Zellenwert behandelt wird.
* Die Marker verarbeiten und das Arbeitsbuch speichern.
* Das Ergebnis überprüfen.

> **Voraussetzungen** – Sie benötigen die Aspose.Cells für .NET‑Bibliothek (v23.12 oder neuer) und eine .NET‑Entwicklungsumgebung (Visual Studio 2022 empfohlen). Grundkenntnisse in C# und DataTables werden vorausgesetzt.

---

## Schritt 1: Datenquelle mit einem JSON-Array vorbereiten

Zuerst erstellen Sie einen `DataTable`, der die Daten nachahmt, die Sie von einem Service oder einer Datenbank erhalten würden. Die **Names**‑Spalte enthält einen JSON‑kodierten String, der ein Array von Namen darstellt.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Warum dieser Schritt?*  
Smart Markers lesen Daten direkt aus .NET‑Objekten. Indem Sie das JSON‑Array in einer String‑Spalte ablegen, bewahren Sie die exakte JSON‑Syntax, die später unverändert in eine Zelle geschrieben werden kann.

---

## Schritt 2: Smart Markers in ein neues Arbeitsbuch einfügen

Erzeugen Sie ein frisches Arbeitsbuch, wählen Sie das erste Arbeitsblatt aus und schreiben Sie Smart Markers, die die gesamte Tabelle sowie die spezifische **Names**‑Spalte referenzieren.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Der Marker `&=dataTable.Names` weist Aspose.Cells an, die Zelle durch den Wert der **Names**‑Spalte für jede Zeile in `dataTable` zu ersetzen. Da wir nur eine Zeile haben, wird der Marker einmal verarbeitet.

---

## Schritt 3: **SmartMarkerOptions ArrayAsSingle konfigurieren**

Standardmäßig erweitert Aspose.Cells einen array‑ähnlichen String in separate Zeilen. Das Setzen von `ArrayAsSingle` auf `true` überschreibt dieses Verhalten und zwingt den gesamten JSON‑String, in einer einzigen Zelle zu bleiben.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Warum `ArrayAsSingle` aktivieren?*  
Wenn `ArrayAsSingle` **false** ist, interpretiert die Engine `["Alice","Bob"]` als zwei separate Werte und schreibt sie in benachbarte Zeilen. Wird es auf **true** gesetzt, wird der String als atomarer Wert behandelt, was entscheidend ist, um das JSON‑Format in Excel zu bewahren.

---

## Schritt 4: Smart Markers mit den konfigurierten Optionen verarbeiten

Führen Sie nun die Smart‑Marker‑Engine aus und übergeben Sie das Options‑Objekt, das Sie gerade konfiguriert haben.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Während der Verarbeitung liest Aspose.Cells die `dataTable`, wendet die Marker an und beachtet das `ArrayAsSingle`‑Flag, sodass das JSON‑Array unverändert bleibt.

---

## Schritt 5: Das Arbeitsbuch speichern und das Ergebnis überprüfen

Schreiben Sie schließlich das Arbeitsbuch auf die Festplatte. Öffnen Sie die erzeugte Datei in Excel oder einem anderen Tabellen‑Viewer, um zu bestätigen, dass Zelle **A2** den exakten JSON‑String enthält.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Erwartete Ausgabe

| A   |
|-----|
| **["Alice","Bob"]** |

Zelle **A2** zeigt das JSON‑Array als einzelnen Textwert, exakt so, wie er im `DataTable` gespeichert ist. Es werden keine zusätzlichen Zeilen erzeugt.

---

## Gemeinsame Variationen und Edge‑Case‑Behandlung

| Situation | Wie anpassen |
|-----------|--------------|
| **Mehrere Zeilen mit JSON-Arrays** | Die gleiche `ArrayAsSingle`‑Einstellung funktioniert; das JSON‑Array jeder Zeile bleibt in ihrer eigenen Zelle. |
| **Verschiedene JSON‑Strukturen (Objekte, verschachtelte Arrays)** | Solange das JSON ein String ist, hält `ArrayAsSingle` es intakt. Bei komplexen Objekten müssen ggf. Anführungszeichen escaped werden. |
| **Verwendung einer anderen Datenquelle (z. B. List\<T\>)** | Ersetzen Sie den `DataTable` durch jede aufzählbare Sammlung; die Marker‑Syntax (`&=myList.Property`) bleibt gleich. |
| **Export nach CSV statt XLSX** | `ArrayAsSingle` gilt weiterhin, aber denken Sie daran, dass CSV keine Zellformatierung bewahrt; Sie müssen das JSON ggf. in Anführungszeichen setzen. |

**Pro‑Tipp:** Setzen Sie `ArrayAsSingle` immer *vor* dem Aufruf von `ProcessSmartMarkers`. Eine Änderung des Flags nach der Verarbeitung hat keinen Einfluss auf bereits erzeugte Zellen.

---

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie in eine Konsolenanwendung kopieren‑und‑einfügen können. Es enthält alle `using`‑Direktiven und Kommentare zur Klarheit.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Führen Sie das Programm aus, öffnen Sie `SmartMarkerJson.xlsx`, und Sie sehen das JSON‑Array in Zelle **A2** erhalten.

---

## Fazit

Sie wissen jetzt, wie Sie **SmartMarkerOptions ArrayAsSingle** in C# konfigurieren, um ein JSON‑Array als einzelnen Zellenwert zu erhalten, wenn Sie Aspose.Cells‑Smart‑Marker verwenden. Die Schritte – `DataTable` vorbereiten, Marker einfügen, das `ArrayAsSingle`‑Flag setzen, verarbeiten und speichern – bilden ein wiederholbares Muster, das Sie in jedem Szenario anwenden können, in dem eine kompakte JSON‑Darstellung in Excel erforderlich ist.

Als Nächstes könnten Sie:

* **Aspose.Cells Smart Markers** für das Durchlaufen von Sammlungen erkunden.
* **Verschachtelte JSON‑Objekte** exportieren, indem Sie die Zellformatierung anpassen.
* **Bedingte Formatierung** mit Smart Markers kombinieren, um reichhaltigere Berichte zu erstellen.

Experimentieren Sie gern mit verschiedenen Datenstrukturen und teilen Sie Ihre Erkenntnisse. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden demonstrierten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren Projekten zu erkunden.

- [Excel-Arbeitsmappe aus JSON erstellen – Vollständiger Aspose.Cells Leitfaden](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Excel-Arbeitsmappe mit Aspose Cells .NET konfigurieren](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Excel-Arbeitsmappe mit Aspose Cells .NET konfigurieren](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}