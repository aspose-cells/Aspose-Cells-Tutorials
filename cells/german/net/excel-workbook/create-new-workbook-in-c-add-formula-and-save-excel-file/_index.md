---
category: general
date: 2026-02-23
description: Erstelle ein neues Arbeitsbuch programmgesteuert in C# und füge einer
  Zelle eine Formel hinzu. Lerne, wie man EXPAND verwendet, und speichere das Excel‑Arbeitsbuch
  mühelos.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: de
og_description: Erstelle ein neues Arbeitsbuch programmgesteuert in C#. Füge einer
  Zelle eine Formel hinzu, lerne, wie man EXPAND verwendet, und speichere das Excel‑Arbeitsbuch
  in Sekunden.
og_title: Neues Arbeitsbuch in C# erstellen – Formel hinzufügen und Excel-Datei speichern
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Neues Arbeitsbuch in C# erstellen – Formel hinzufügen und Excel-Datei speichern
url: /de/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues Arbeitsbuch in C# erstellen – Formel hinzufügen und Excel-Datei speichern

Haben Sie sich schon einmal gefragt, wie man **new workbook**‑Objekte aus dem Code heraus erstellt, ohne Excel zu öffnen? Sie sind nicht allein. Viele Entwickler stoßen auf ein Problem, wenn sie ein Tabellenblatt „on the fly“ erzeugen müssen – sei es für einen Bericht, einen Export oder einen schnellen Daten‑Dump.  

Die gute Nachricht? In diesem Leitfaden sehen Sie genau, wie Sie **new workbook** erstellen, eine **add formula to cell** einfügen und anschließend das **excel workbook** mit nur wenigen Zeilen C# **save**. Außerdem gehen wir darauf ein, **how to use expand** zu nutzen, um dynamische Arrays ohne manuelles Kopieren zu erzeugen. Am Ende können Sie **create excel file programmatically** und es an Benutzer oder nachgelagerte Dienste weitergeben.

## Voraussetzungen

- .NET 6.0 oder höher (jede aktuelle .NET‑Runtime funktioniert)
- Aspose.Cells für .NET (Kostenlose Testversion oder lizenziert) – diese Bibliothek liefert die `Workbook`‑ und `Worksheet`‑Klassen, die unten verwendet werden.
- Grundlegende Kenntnisse der C#‑Syntax – tiefgehendes Excel‑Wissen ist nicht nötig.

Wenn Sie das bereits haben, super! Wenn nicht, holen Sie sich Aspose.Cells über NuGet (`Install-Package Aspose.Cells`) und Sie können loslegen.

---

## Schritt 1: Neues Workbook erstellen – Das Fundament

Zuerst müssen wir ein frisches Workbook‑Objekt instanziieren. Stellen Sie sich das vor wie das Öffnen einer brandneuen, komplett leeren Excel‑Datei.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Warum das wichtig ist:** Die `Workbook`‑Klasse ist der Einstiegspunkt für jede Excel‑Manipulation. Durch das Erzeugen einer neuen Instanz reservieren wir Speicher für Blätter, Stile und Formeln – und das ganz ohne Dateisystemzugriff.

---

## Schritt 2: Auf das erste Arbeitsblatt zugreifen

Jedes neue Workbook enthält ein Standard‑Arbeitsblatt (namens *Sheet1*). Wir holen es uns, um Daten und Formeln zu platzieren.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro‑Tipp:** Wenn Sie mehrere Blätter benötigen, rufen Sie einfach `workbook.Worksheets.Add("MySheet")` auf und arbeiten Sie mit dem zurückgegebenen `Worksheet`‑Objekt.

---

## Schritt 3: Formel in Zelle einfügen – Mit EXPAND

Jetzt wird es spannend: Das Einfügen einer Formel. Die `EXPAND`‑Funktion ist ideal, wenn Sie ein statisches Array in einen größeren, automatisch gefüllten Bereich verwandeln wollen.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Wie die EXPAND‑Formel funktioniert

| Argument | Bedeutung |
|----------|-----------|
| `{1,2,3}` | Das Quell‑Array (eine horizontale Liste von drei Zahlen) |
| `5`       | Gewünschte Zeilenanzahl im Ergebnis |
| `1`       | Gewünschte Spaltenanzahl (bei 1 bleibt das Ergebnis vertikal) |

Wenn Excel dies auswertet, entsteht eine **vertikale** Liste:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Warum EXPAND verwenden?** Es erspart manuelles Kopieren oder VBA‑Schleifen. Die Funktion formt Daten dynamisch um, wodurch Ihre Tabellen robuster und leichter zu warten sind.

---

## Schritt 4: Excel‑Workbook speichern – Ergebnis persistieren

Nachdem die Formel gesetzt ist, schreiben wir das Workbook auf die Festplatte. Sie können jeden Ordner wählen, in den Sie Schreibrechte haben.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Was Sie sehen werden:** Öffnen Sie `ExpandFormula.xlsx` in Excel, und Zelle `A1` zeigt das erweiterte Array an. Die Formel bleibt in der Zelle, sodass bei Änderung des Quell‑Arrays das Ergebnis automatisch aktualisiert wird.

---

## Optional: Ausgabe programmgesteuert verifizieren

Falls Sie Excel nicht manuell öffnen möchten, können Sie die Werte wieder einlesen und prüfen, ob sie den Erwartungen entsprechen.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Das Ausführen des obigen Codes gibt aus:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|----------|
| **Kann ich EXPAND mit einem größeren Quell‑Array nutzen?** | Absolut. Ändern Sie einfach `{1,2,3}` zu einem beliebigen Konstanten‑ oder Zellbereich, z. B. `EXPAND(A1:C1,10,1)`. |
| **Was, wenn ich ein horizontales Ergebnis brauche?** | Tauschen Sie die Zeilen‑/Spalten‑Argumente: `EXPAND({1,2,3},1,5)` erzeugt eine 1‑Zeilen‑5‑Spalten‑Ausgabe. |
| **Funktioniert das in älteren Excel‑Versionen?** | `EXPAND` ist ab Excel 365/2021 verfügbar. Für ältere Versionen müssten Sie das Array mit `INDEX`/`SEQUENCE` simulieren. |
| **Muss ich `workbook.CalculateFormula()` aufrufen?** | Nein. Aspose.Cells wertet Formeln beim Speichern automatisch aus, sodass die Werte sofort sichtbar sind. |
| **Wie füge ich vor dem Speichern mehrere Blätter hinzu?** | Rufen Sie `workbook.Worksheets.Add("SecondSheet")` auf und wiederholen Sie die Zell‑Manipulations‑Schritte im neuen Arbeitsblatt. |

---

## Vollständiges Beispiel

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren Sie es in ein Konsolen‑App‑Projekt, passen Sie den Ausgabepfad an und drücken Sie **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Erwartete Konsolenausgabe:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Öffnen Sie die erzeugte Datei und Sie sehen dieselben Zahlen in Spalte **A**.

---

## Visuelle Zusammenfassung

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*Das Bild zeigt das frisch erstellte Workbook mit dem EXPAND‑Ergebnis.*

---

## Fazit

Sie wissen jetzt, wie man **new workbook** erstellt, **add formula to cell** einfügt und das **excel workbook** mit C# **save** kann. Durch das Beherrschen von **how to use expand** lassen sich dynamische Arrays ohne manuellen Aufwand erzeugen, und der gesamte Prozess ermöglicht es Ihnen, **create excel file programmatically** für jede Automatisierungssituation zu nutzen.

Was kommt als Nächstes? Ersetzen Sie das konstante Array durch einen Zellbereich, experimentieren Sie mit unterschiedlichen `EXPAND`‑Dimensionen oder verketten Sie mehrere Formeln über verschiedene Blätter hinweg. Das gleiche Muster funktioniert auch für Diagramme, Formatierungen und sogar Pivot‑Tabellen – also weiter erkunden.

Falls Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar. Viel Spaß beim Coden und genießen Sie die Macht der programmgesteuerten Excel‑Verarbeitung!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}