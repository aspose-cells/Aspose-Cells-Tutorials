---
category: general
date: 2026-06-08
description: Wie man Tabellenblätter in Excel mit SmartMarkerProcessor für Master‑Detail‑Berichte
  verknüpft. Master‑Tabelle befüllen und mühelos einen Master‑Detail‑Excel‑Bericht
  erstellen.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: de
og_description: Wie man Tabellen in Excel mit SmartMarkerProcessor verknüpft. Lernen
  Sie, das Masterblatt zu füllen und in wenigen Minuten einen Master‑Detail‑Bericht
  zu erstellen.
og_title: Wie man Arbeitsblätter in Excel mit SmartMarker verknüpft – Schritt für
  Schritt
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Wie man Arbeitsblätter in Excel mit SmartMarker verknüpft – Schritt‑für‑Schritt‑Anleitung
url: /de/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Tabellen in Excel mit SmartMarker verknüpft – Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, **wie man Tabellen verknüpft** in Excel, ohne manuell Zeilen zu kopieren oder endlose VBA‑Schleifen zu schreiben? Sie sind nicht allein. Die meisten Entwickler stoßen an Grenzen, wenn sie einen sauberen Master‑Detail‑Bericht benötigen, der synchron bleibt, wenn sich Daten ändern. Die gute Nachricht? SmartMarkerProcessor übernimmt die schwere Arbeit für Sie und verwandelt ein paar Zeilen C# in ein vollwertiges Master‑Detail‑Arbeitsbuch.

In diesem Tutorial führen wir Sie durch die genauen Schritte, um **Master‑Tabelle zu befüllen**, das Detail‑Blatt einzurichten und schließlich **Master‑Detail‑Bericht zu erzeugen**, der automatisch aktualisiert wird. Am Ende haben Sie ein wiederverwendbares Muster, das Sie in jedes .NET‑Projekt einbinden können.

> **Voraussetzungs‑Hinweis:** Sie benötigen GrapeCity Documents for Excel (GcExcel) Version 2024 oder neuer, eine .NET‑Entwicklungsumgebung (Visual Studio 2022 funktioniert hervorragend) und Grundkenntnisse in C#. Keine zusätzlichen NuGet‑Pakete über GcExcel hinaus sind erforderlich.

---

## Überblick über die Lösung

Bevor wir in den Code eintauchen, lassen Sie uns aufschlüsseln, was „Tabellen verknüpfen“ im Kontext von SmartMarker tatsächlich bedeutet:

1. **Master sheet** – Enthält eine Zeile pro Entität (z. B. eine Kundenliste).
2. **Detail sheet** – Enthält Zeilen, die zu einer Master‑Zeile gehören (z. B. Bestellungen für jeden Kunden).
3. **SmartMarker syntax** – Eine winzige Auszeichnungssprache (`{MasterSheet}#master;{DetailSheet}#detail`), die dem Prozessor mitteilt, wie die beiden Datentabellen zu binden sind.
4. **Processor options** – Durch Aktivieren von `MasterDetail` wiederholt die Engine automatisch die Master‑Zeilen und bettet die zugehörigen Detail‑Zeilen darunter ein.

Das Verständnis dieser Bausteine hilft Ihnen später, den Ansatz anzupassen – vielleicht benötigen Sie eine dreistufige Verschachtelung oder bedingte Formatierung. Halten Sie dieses mentale Modell bereit, während wir die Implementierung Schritt für Schritt durchgehen.

---

## Schritt 1: Hierarchische Daten für die Master‑Detail‑Verarbeitung vorbereiten

Das Erste, was Sie benötigen, ist eine Datenquelle, die die Master‑Detail‑Beziehung widerspiegelt. In den meisten realen Szenarien kommt das aus einer Datenbank, aber zur Veranschaulichung verwenden wir ein anonymes Objekt‑Literal.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Warum das wichtig ist:** SmartMarker errät Beziehungen nicht magisch; es sucht nach passenden Eigenschaftsnamen (`MasterId` → `Id`). Durch diese Struktur geben wir dem Prozessor eine klare Zuordnung, die das Fundament dafür bildet, **wie man Tabellen verknüpft** effektiv zu nutzen.

> **Pro‑Tipp:** Wenn Ihre Daten in `DataTable`‑Objekten vorliegen, geben Sie sie einfach als Eigenschaften mit denselben Namen frei – SmartMarker funktioniert mit jeder aufzählbaren Sammlung.

---

## Schritt 2: Ein Arbeitsbuch erstellen und eine Vorlage laden

SmartMarker arbeitet gegen ein vorhandenes Excel‑Arbeitsbuch, meist eine Vorlage, die bereits die Blattnamen und Platzhalter‑Marker enthält. Lassen Sie uns ein Arbeitsbuch im Speicher erzeugen und zwei leere Arbeitsblätter mit den Namen *MasterSheet* und *DetailSheet* hinzufügen.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Sie können auch eine `.xlsx`‑Datei von der Festplatte laden (`wb.Open("Template.xlsx")`), wenn Sie das Layout lieber zuerst in Excel entwerfen. Wichtig ist, dass die Blattnamen mit denen übereinstimmen, die Sie im SmartMarker‑String referenzieren werden.

---

## Schritt 3: SmartMarkerProcessor instanziieren und Master‑Detail‑Modus aktivieren

Jetzt holen wir die Engine, die die Marker liest und die Daten einfügt. Der `SmartMarkerProcessor` nimmt das Arbeitsbuch als Konstruktor‑Argument, und das Flag `Options.MasterDetail` weist ihn an, die `#master`‑ und `#detail`‑Marker als verknüpftes Paar zu behandeln.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Warum `MasterDetail` aktivieren?** Ohne dieses Flag würde der Prozessor `{MasterSheet}#master` und `{DetailSheet}#detail` als unabhängige Vorgänge behandeln und die entscheidende Beziehung zwischen den Zeilen verlieren. Das Setzen des Flags ist die einzige Zeile, die **wie man Tabellen verknüpft** tatsächlich funktionieren lässt.

---

## Schritt 4: SmartMarker‑String definieren und den Prozessor ausführen

Der Marker‑String sagt SmartMarker, welches Blatt das Master‑ und welches das Detail‑Blatt ist. Die Syntax ist einfach: `{SheetName}#master;{SheetName}#detail`. Sie können auch zusätzliche Marker hinzufügen (z. B. `#header`), die für einen Basis‑Bericht jedoch nicht nötig sind.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Wenn `Process` ausgeführt wird, erledigt die Engine:

1. Schreibt jede Master‑Zeile in *MasterSheet* beginnend in der ersten leeren Zeile nach der Kopfzeile.
2. Für jede Master‑Zeile scannt sie die `Details`‑Sammlung, wählt Zeilen aus, bei denen `MasterId` mit der Master‑`Id` übereinstimmt, und schreibt sie direkt unter die entsprechende Master‑Eintragung in *DetailSheet*.

---

## Schritt 5: Das resultierende Arbeitsbuch speichern oder exportieren

An diesem Punkt haben Sie ein vollständig befülltes Arbeitsbuch. Sie können es auf die Festplatte speichern, an einen Web‑Client streamen oder sogar in PDF konvertieren.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Öffnen Sie die Datei und Sie sehen zwei Blätter: *MasterSheet* listet `A` und `B` auf, während *DetailSheet* `Item1` unter Master `1` und `Item2` unter Master `2` zeigt. Das ist das Wesentliche von **Master‑Tabelle befüllen** und **Master‑Detail‑Bericht erzeugen** in einem Schritt.

---

## Visual Overview

![Diagramm, das zeigt, wie man Tabellen in Excel mit SmartMarkerProcessor verknüpft](https://example.com/diagram.png "Diagramm zum Verknüpfen von Tabellen")

Das Diagramm (Alt‑Text enthält das Haupt‑Keyword) zeigt den Datenfluss von C#‑Objekten → SmartMarkerProcessor → verknüpfte Excel‑Tabellen.

---

## Häufige Randfälle behandeln

### Mehrere Detail‑Zeilen pro Master

Wenn eine Master‑Zeile mehrere zugehörige Details hat, wiederholt SmartMarker die Master‑Zeile einmal und schreibt dann *alle* passenden Detail‑Zeilen darunter. Kein zusätzlicher Code nötig – stellen Sie nur sicher, dass Ihre `Details`‑Sammlung jede Zeile enthält.

### Fehlende Details

Wenn ein Master‑Eintrag keine passenden Detail‑Zeilen hat, überspringt das Detail‑Blatt einfach diesen Abschnitt. Wenn Sie einen Platzhalter benötigen (z. B. „Keine Artikel“), können Sie in der Vorlage eine berechnete Spalte hinzufügen, die eine Excel‑Formel wie `=IF(COUNTA(A2:B2)=0,"No items","")` verwendet.

### Große Datensätze

Die Verarbeitung von Zehntausenden von Zeilen kann speicherintensiv sein. Um die Leistung flott zu halten:

- Verwenden Sie `processor.Options.EnableStreaming = true` (verfügbar in GcExcel 2025+).
- Teilen Sie die Daten in Stücke und verarbeiten Sie jedes Stück separat, dann fügen Sie die Arbeitsbücher zusammen.

### Benutzerdefinierte Spaltenzuordnung

Wenn Ihre Eigenschaftsnamen nicht übereinstimmen (`MasterKey` vs `Id`), können Sie vor der Verarbeitung die Methode `SmartMarkerProcessor.Map` nutzen, um ein Alias zu erstellen.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein komplettes, copy‑paste‑bereites Programm, das Sie sofort ausführen können.



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie zusätzliche API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Externe Verknüpfungsformeln in Excel mit Aspose.Cells für Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Dynamische Excel-Tabellen in Java mit Aspose.Cells: Ein umfassender Leitfaden](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamische Excel-Berichte mit Aspose.Cells Java: Benannte Bereiche & komplexe Formeln](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}