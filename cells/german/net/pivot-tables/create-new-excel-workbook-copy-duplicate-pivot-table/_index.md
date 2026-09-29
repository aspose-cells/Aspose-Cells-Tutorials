---
category: general
date: 2026-02-09
description: Erstellen Sie eine neue Excel-Arbeitsmappe und lernen Sie, Pivot‑Tabellen
  mühelos zu kopieren. Dieser Leitfaden zeigt, wie man eine Pivot‑Tabelle dupliziert
  und die Arbeitsmappe als neue speichert.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: de
og_description: Erstellen Sie eine neue Excel-Arbeitsmappe in C# und kopieren Sie
  sofort eine Pivot‑Tabelle. Erfahren Sie, wie Sie eine Pivot‑Tabelle duplizieren
  und die Arbeitsmappe als neue speichern, mit einem vollständigen Codebeispiel.
og_title: Neues Excel‑Arbeitsbuch erstellen – Schritt‑für‑Schritt Pivot‑Kopie
tags:
- excel
- csharp
- aspose.cells
- automation
title: Neues Excel‑Arbeitsbuch erstellen – Pivot‑Tabelle kopieren & duplizieren
url: /de/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues Excel‑Arbeitsbuch erstellen – Pivot‑Tabelle kopieren & duplizieren

Haben Sie jemals **ein neues Excel‑Arbeitsbuch erstellen** müssen, das eine komplexe Pivot‑Tabelle aus einer bestehenden Datei übernimmt? Sie sind nicht allein – viele Entwickler stoßen bei der Automatisierung von Reporting‑Pipelines auf dieses Problem. Die gute Nachricht ist, dass Sie mit wenigen Zeilen C# und der Aspose.Cells‑Bibliothek **wie man Pivot kopiert** schnell, **Pivot‑Tabelle duplizieren** und **Arbeitsbuch als neu speichern** können, ohne Excel manuell zu öffnen.

In diesem Leitfaden gehen wir den gesamten Prozess durch, vom Laden des Quell‑Arbeitsbuchs bis zum Speichern der duplizierten Version. Am Ende haben Sie ein einsatzbereites Snippet, das Sie in jedes .NET‑Projekt einbinden können. Keine Ausschweifungen, nur eine praktische Lösung, die Sie noch heute testen können.

## Was dieses Tutorial abdeckt

* **Voraussetzungen** – .NET 6+ (oder .NET Framework 4.6+), Visual Studio und das NuGet‑Paket Aspose.Cells für .NET.
* Schritt‑für‑Schritt‑Code, der **ein neues Excel‑Arbeitsbuch erstellt**, die Pivot‑Tabelle kopiert und das Ergebnis auf die Festplatte schreibt.
* Erklärungen, **warum** jede Zeile wichtig ist, nicht nur **was** sie tut.
* Tipps zum Umgang mit Sonderfällen wie ausgeblendeten Arbeitsblättern oder großen Datenbereichen.
* Ein kurzer Blick auf **wie man ein Arbeitsblatt kopiert**, falls Sie jemals das gesamte Blatt statt nur der Pivot‑Tabelle benötigen.

Bereit? Dann legen wir los.

![Illustration zum Erstellen eines neuen Excel‑Arbeitsbuchs](image.png "Diagramm, das Quell‑Arbeitsbuch, Pivot‑Kopie und Ziel‑Arbeitsbuch zeigt")

## Schritt 1: Projekt einrichten und Aspose.Cells installieren

Bevor wir **ein neues Excel‑Arbeitsbuch erstellen** können, benötigen wir ein Projekt, das die richtige Bibliothek referenziert.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Warum das wichtig ist:* Aspose.Cells arbeitet vollständig im Speicher, sodass Sie Excel auf dem Server nie starten müssen. Es bewahrt außerdem die Pivot‑Cache‑Informationen, was für eine echte **Pivot‑Tabelle duplizieren** unerlässlich ist.

> **Profi‑Tipp:** Wenn Sie .NET Core anvisieren, stellen Sie sicher, dass der Runtime‑Identifier (RID) Ihres Projekts zur Zielplattform passt; andernfalls können native Bibliotheks‑Ladefehler auftreten.

## Schritt 2: Quell‑Arbeitsbuch laden, das die Pivot‑Tabelle enthält

Jetzt werden wir **wie man Pivot kopiert** aus einer bestehenden Datei. Das Quell‑Arbeitsbuch kann überall auf der Festplatte, als Stream oder sogar als Byte‑Array liegen.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Warum wir einen Bereich wählen:* Eine Pivot‑Tabelle befindet sich innerhalb eines normalen Zellbereichs, hat aber auch versteckte Cache‑Daten, die dem Blatt zugeordnet sind. Durch das Kopieren des Bereichs **einschließlich der Pivot‑Tabelle** stellt Aspose.Cells sicher, dass der Cache mitkopiert wird, sodass Sie im Ziel‑Datei eine funktionale **Pivot‑Tabelle duplizieren** erhalten.

## Schritt 3: Neues Excel‑Arbeitsbuch erstellen, um die kopierten Daten zu empfangen

Hier erstellen wir tatsächlich **ein neues Excel‑Arbeitsbuch**, das die duplizierte Pivot‑Tabelle enthält.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Warum ein frisches Arbeitsbuch?** Ein sauberer Start garantiert, dass keine Restformatierungen oder versteckten Objekte die kopierte Pivot‑Tabelle beeinträchtigen. Außerdem wird die resultierende Datei kleiner, was für automatisierte E‑Mail‑Anhänge praktisch ist.

## Schritt 4: Pivot‑Bereich in das neue Arbeitsbuch kopieren

Jetzt führen wir die eigentliche **wie man Pivot kopiert**‑Operation aus.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Das erledigt in einem Schritt das Schwergewicht:

* Die Zellwerte, Formeln und Formatierungen werden übertragen.
* Der Pivot‑Cache wird dupliziert, sodass die neue Pivot‑Tabelle voll funktionsfähig bleibt.
* Alle relativen Verweise innerhalb der Pivot‑Tabelle passen sich automatisch an den neuen Standort an.

### Umgang mit Sonderfällen

* **Ausgeblendete Arbeitsblätter:** Wenn das Quellblatt ausgeblendet ist, wird die Pivot‑Tabelle trotzdem korrekt kopiert, Sie möchten jedoch das Zielblatt für die Benutzer sichtbar machen:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Große Datensätze:** Für Bereiche mit mehr als ein paar tausend Zeilen sollten Sie `CopyTo` mit `CopyOptions` verwenden, um den Vorgang zu streamen und den Speicherverbrauch zu reduzieren.

## Schritt 5: Ziel‑Arbeitsbuch als neue Datei speichern

Abschließend **speichern wir das Arbeitsbuch als neu** und überprüfen das Ergebnis.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Wenn Sie `copied.xlsx` öffnen, sehen Sie eine exakte Kopie der ursprünglichen Pivot‑Tabelle, bereit für weitere Bearbeitung oder Verteilung.

### Optional: Wie man ein Arbeitsblatt anstelle nur der Pivot‑Tabelle kopiert

Manchmal möchten Sie das gesamte Blatt, nicht nur die Pivot‑Tabelle. Die gleiche API macht das trivial:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Damit wird die **wie man ein Arbeitsblatt kopiert**‑Anfrage beantwortet und ist praktisch, wenn Sie zusätzliche Blatt‑Einstellungen erhalten müssen.

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier ist eine eigenständige Konsolen‑App, die Sie kompilieren und ausführen können:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Erwartete Ausgabe:** Die Konsole gibt eine Erfolgsmeldung aus und `copied.xlsx` erscheint in `C:\Reports` mit einer funktionalen Pivot‑Tabelle, die identisch mit der in `source.xlsx` ist.

## Häufige Fragen & Stolperfallen

* **Brechen Formeln innerhalb der Pivot‑Tabelle?** Nein – weil der Pivot‑Cache mit dem Bereich mitkopiert wird, bleiben alle berechneten Felder erhalten.
* **Was, wenn die Quell‑Pivot externe Datenverbindungen nutzt?** Diese Verbindungen werden *nicht* kopiert. Sie müssen sie im Ziel‑Arbeitsbuch erneut herstellen oder die Pivot‑Tabelle zuerst in eine statische Tabelle umwandeln.
* **Kann ich mehrere Pivot‑Tabellen auf einmal kopieren?** Ja – definieren Sie einfach einen größeren Bereich, der alle Pivot‑Tabellen umfasst, oder iterieren Sie über jedes `PivotTable`‑Objekt in `sourceSheet.PivotTables` und kopieren Sie sie einzeln.
* **Muss ich die `Workbook`‑Objekte freigeben?** Sie implementieren `IDisposable`, daher ist das Einhüllen in `using`‑Anweisungen eine gute Gewohnheit, besonders in hochdurchsatz‑Diensten.

## Fazit

Sie wissen jetzt, **wie man ein neues Excel‑Arbeitsbuch erstellt**, eine Pivot‑Tabelle kopiert, **Pivot‑Tabelle dupliziert** und **Arbeitsbuch als neu speichert** mit C# und Aspose.Cells. Die Schritte sind einfach: laden, erstellen, kopieren und speichern. Mit dem optionalen **wie man ein Arbeitsblatt kopiert**‑Snippet haben Sie zudem eine Alternative für die vollständige Blatt‑Duplizierung.

Als Nächstes könnten Sie erkunden:

* Benutzerdefinierte Formatierung zur duplizierten Pivot‑Tabelle hinzufügen.
* Das Pivot‑Cache programmgesteuert nach Datenänderungen aktualisieren.
* Das Arbeitsbuch in PDF oder CSV für nachgelagerte Systeme exportieren.

Probieren Sie es aus, passen Sie den Bereich an und lassen Sie die Automatisierung die mühselige Arbeit aus Ihrem Reporting‑Workflow übernehmen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}