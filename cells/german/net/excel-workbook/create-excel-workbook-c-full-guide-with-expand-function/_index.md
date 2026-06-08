---
category: general
date: 2026-06-08
description: Erstelle Excel‑Arbeitsmappe C# Schritt für Schritt und lerne, wie man
  die Expand‑Funktion in Excel für dynamische Bereiche verwendet. Perfekt für .NET‑Entwickler.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: de
og_description: Erstellen Sie ein Excel‑Arbeitsbuch in C# mit einem klaren Beispiel
  und entdecken Sie, wie Sie die Expand‑Funktion in Excel verwenden, um dynamische
  Arrays zu erzeugen.
og_title: Excel-Arbeitsmappe erstellen in C# – Vollständiger Programmierleitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Excel-Arbeitsmappe in C# erstellen – Vollständiger Leitfaden mit Expand‑Funktion
url: /de/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe mit C# erstellen – Vollständige Anleitung mit der EXPAND-Funktion

Haben Sie sich jemals gefragt, wie man **Excel-Arbeitsmappe C# erstellen** kann, ohne sich mit COM-Interop herumzuschlagen oder mit XML zu hantieren? Sie sind nicht allein. In vielen .NET-Projekten müssen wir eine Tabelle erzeugen, sie mit Formeln füllen und an nicht‑technische Benutzer übergeben. Die gute Nachricht? Mit einer modernen Bibliothek wie **Aspose.Cells** ist der gesamte Prozess ein Kinderspiel.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das **eine Excel-Arbeitsmappe C# erstellt**, ein paar Formeln einfügt – einschließlich wie man **die EXPAND‑Funktion in Excel verwendet** – und die Datei speichert, sodass Sie sie sofort in Excel öffnen können. Am Ende wissen Sie nicht nur *was* Sie eingeben müssen, sondern *warum* jede Zeile wichtig ist, und Sie erhalten eine Vorlage, die Sie in jedes Projekt kopieren können.

## Voraussetzungen

- .NET 6 SDK (oder eine aktuelle .NET‑Version) installiert.
- Eine NuGet‑kompatible IDE (Visual Studio, VS Code, Rider usw.).
- Das **Aspose.Cells** NuGet‑Paket – es stellt die Klassen `Workbook` und `Worksheet` bereit, die im Code verwendet werden.
- Grundkenntnisse in C#; keine Excel‑spezifische Erfahrung erforderlich.

Alles bereit? Großartig – lassen Sie uns loslegen.

## Schritt 1: Projekt einrichten und Aspose.Cells hinzufügen

Zuerst erstellen Sie eine Konsolenanwendung und binden die Bibliothek ein.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Pro Tipp:** Wenn Sie sich in einem Firmennetzwerk befinden, müssen Sie möglicherweise einen NuGet‑Proxy konfigurieren. Das Aspose.Cells‑Paket ist leichtgewichtig, sodass die Installation in Sekunden abgeschlossen ist.

Öffnen Sie nun `Program.cs`. Sie sehen die Standard‑`Main`‑Methode – ersetzen Sie sie durch das untenstehende Gerüst.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

Die Zeile `using Aspose.Cells;` bringt die Tabellenklassen in den Gültigkeitsbereich. Wenn Sie sie vergessen, wird der Compiler melden, dass `Workbook` nicht definiert ist – etwas, das wir später vermeiden werden.

## Schritt 2: Excel-Arbeitsmappe mit C# erstellen und auf das erste Arbeitsblatt zugreifen

Mit dem fertig eingerichteten Projekt können wir endlich **eine Excel-Arbeitsmappe C# erstellen**. Der `Workbook`‑Konstruktor liefert uns eine neue, leere Arbeitsmappe, und der Index `Worksheets[0]` gibt das Standardblatt zurück (namens „Sheet1“).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Warum holen wir explizit das erste Arbeitsblatt? Weil viele nachgelagerte APIs (wie das Setzen von Formeln) ein `Worksheet`‑Objekt benötigen, nicht nur das `Workbook`. Das macht den Code auch für spätere Leser klarer.

## Schritt 3: EXPAND‑Funktion in Excel verwenden, um einen dynamischen Bereich zu füllen

Jetzt kommt der Star der Show: **die EXPAND‑Funktion in Excel verwenden**. Die `EXPAND`‑Funktion (ab Excel 365 verfügbar) nimmt ein Quell‑Array und erweitert es auf eine gewünschte Größe. In unserem Beispiel beginnen wir mit einem 3‑Zeilen‑vertikalen Array, das durch `SEQUENCE(3)` erzeugt wird, und erweitern es zu einem 5 × 5‑Block.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Was passiert genau?

1. `SEQUENCE(3)` erzeugt ein vertikales Array `{1;2;3}`.
2. `EXPAND(...,5,5)` weist Excel an, dieses Array auf 5 Zeilen und 5 Spalten zu erweitern.
3. Das Ergebnis ist ein 5 × 5‑Raster, bei dem die ersten drei Zeilen die Zahlen 1‑3 über die Spalten hinweg wiederholen, und die restlichen zwei Zeilen leer sind.

Da wir die Formel als Zeichenkette schreiben, wertet Excel sie *beim Öffnen der Datei* aus, nicht zur Laufzeit. Das bedeutet, dass die Arbeitsmappe leicht bleibt und Änderungen am Quell‑Array automatisch durchschlagen.

> **Randfall:** Öffnet ein Benutzer die Arbeitsmappe in einer älteren Excel‑Version, die `EXPAND` nicht unterstützt, zeigt die Zelle `#NAME?` an. Um dem vorzubeugen, könnten Sie die Formel in `IFERROR` einbetten, aber für moderne Umgebungen ist es sicher, sich auf die Funktion zu verlassen.

## Schritt 4: Eine Kotangens‑Formel hinzufügen

Fügen wir noch eine Formel hinzu, um zu zeigen, wie einfach es ist, mathematische Ausdrücke einzufügen. Wir berechnen den Kotangens von π/4, der exakt `1` ist.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Die Excel‑Funktion `COT` wird nicht so häufig verwendet wie `SIN` oder `COS`, ist aber perfekt für trigonometrische Workflows. Beim Öffnen der Arbeitsmappe zeigt die Zelle **B1** den Wert `1` an.

## Schritt 5: Arbeitsmappe speichern und Ergebnis überprüfen

All diese Arbeit wäre sinnlos, wenn wir die Datei nicht speichern würden. Die Methode `Save` schreibt die im Speicher befindliche Arbeitsmappe auf die Festplatte. Wählen Sie einen Ordner, in den Sie Schreibzugriff haben, und geben Sie der Datei einen aussagekräftigen Namen.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Programm ausführen:

```bash
dotnet run
```

Sie sollten die Konsolenausgabe sehen, die das Speichern bestätigt. Öffnen Sie `output.xlsx` in Excel, und Sie werden feststellen:

- Zellen **A1:E5** sind mit der erweiterten Sequenz gefüllt (1,2,3 in den ersten drei Zeilen, leere Zellen in den Zeilen 4‑5).
- Zelle **B1** zeigt den Wert `1` aus der Kotangens‑Formel.

Das ist der komplette Zyklus: **Excel-Arbeitsmappe C# erstellen**, Formeln einbetten und eine nutzbare Tabelle erzeugen.

![Screenshot der erzeugten Excel-Arbeitsmappe, die das erweiterte Array und das Kotangens-Ergebnis zeigt](/images/create-excel-workbook-csharp.png "Beispiel für das Erstellen einer Excel-Arbeitsmappe mit C#")

*Bildbeschreibung: Excel-Arbeitsmappe C# – Ansicht der befüllten Tabelle.*

## Schritt 6: Optional – Spalten automatisch anpassen für ein professionelles Aussehen

Wenn Sie die Datei an Endbenutzer verteilen möchten, sorgt ein schneller Auto‑Fit für ein professionelles Aussehen.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Diese Zeile durchläuft jede Spalte, die Daten enthält, und passt die Breite an den längsten Eintrag an. Es ist ein kleiner Schliff, verhindert jedoch das gefürchtete “…###”-Überlauf‑Problem, wenn Zahlen breiter als die Standardspaltenbreite sind.

## Schritt 7: Abschluss und nächste Schritte

Herzlichen Glückwunsch – Sie haben gerade gelernt, wie man **eine Excel-Arbeitsmappe C# von Grund auf erstellt** und wie man **die EXPAND‑Funktion in Excel verwendet**, um dynamische Arrays zu erzeugen. Der Code ist bewusst minimal gehalten, sodass Sie ihn in jedes Projekt kopieren können, aber die Konzepte lassen sich skalieren:

- **Dynamische Datenquellen:** Ersetzen Sie `SEQUENCE(3)` durch einen Verweis auf einen anderen Bereich oder eine benannte Tabelle.
- **Bedingte Formatierung:** Verwenden Sie `ws.Cells["A1:E5"].Style`, um Farben basierend auf Werten hinzuzufügen.
- **Diagramme und Grafiken:** Aspose.Cells kann Diagramme, Bilder und sogar Pivot‑Tabellen einbetten.

Fühlen Sie sich frei zu experimentieren – ändern Sie die `EXPAND`‑Dimensionen, probieren Sie `FILTER` oder `SORT` aus, oder verketten Sie mehrere Formeln. Die Bibliothek übernimmt alles, ohne dass Sie das Low‑Level‑OpenXML‑Format berühren müssen.

---

### Häufig gestellte Fragen

**F: Funktioniert das mit .NET Framework 4.8?**  
A: Absolut. Aspose.Cells zielt auf .NET Standard 2.0 ab, das sowohl mit .NET Core als auch dem klassischen Framework kompatibel ist.

**F: Was ist, wenn ich das Blatt schützen muss?**  
A: Verwenden Sie `ws.Protect(ProtectionType.All, "yourPassword");` vor dem Speichern.

**F: Kann ich die Arbeitsmappe direkt in einen `MemoryStream` schreiben?**  
A: Ja – `workbook.Save(stream, SaveFormat.Xlsx);` ist praktisch für Web‑APIs, die die Datei als Download zurückgeben.

## TL;DR

Wir haben eine **vollständige C#‑Konsolenanwendung** erstellt, die:

1. **Erstellt eine Excel-Arbeitsmappe C#** mit Aspose.Cells.
2. **Verwendet die EXPAND‑Funktion in Excel**, um ein 3‑Zeilen‑Array in einen 5 × 5‑Block zu verwandeln.
3. Fügt eine Kotangens‑Formel (`COT(PI()/4)`) hinzu.
4. Speichert die Datei und passt optional die Spaltenbreite automatisch an.

Sie haben nun eine solide Grundlage für jede Automatisierungsaufgabe, die das Erzeugen von Excel‑Dateien aus .NET beinhaltet. Viel Spaß beim Programmieren, und mögen Ihre Tabellen stets fehlerfrei bleiben!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man arbeitsmappenbezogene benannte Bereiche in Excel mit Aspose.Cells .NET erstellt](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Wie man Union‑Bereiche in Excel mit Aspose.Cells .NET (C#‑Leitfaden) erstellt und verwendet](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Excel‑Arbeitsmappe mit Diagrammen mithilfe von Aspose.Cells .NET erstellen | Schritt‑für‑Schritt‑Leitfaden](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}