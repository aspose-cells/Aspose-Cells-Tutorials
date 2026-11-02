---
category: general
date: 2026-03-30
description: Erfahren Sie, wie Sie WRAPCOLS in C# verwenden, um eine Excel‑Arbeitsmappe
  zu erstellen, Daten zu Excel hinzuzufügen und die Berechnung von Formeln zu erzwingen,
  während Sie gleichzeitig WRAPROWS nutzen.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: de
og_description: Entdecken Sie, wie Sie WRAPCOLS in C# verwenden, um eine Excel-Arbeitsmappe
  zu erstellen, Daten hinzuzufügen, die Berechnung von Formeln zu erzwingen und WRAPROWS
  für Array‑Formeln zu nutzen.
og_title: Wie man WRAPCOLS in C# verwendet – Vollständige Anleitung
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Wie man WRAPCOLS in C# verwendet – Excel-Arbeitsmappe mit Wrap‑Funktionen erstellen
url: /de/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man WRAPCOLS in C# verwendet – Excel Workbook mit Wrap-Funktionen erstellen

Haben Sie sich jemals gefragt, **wie man WRAPCOLS** verwendet, wenn Sie Excel mit C# automatisieren? Sie sind nicht allein – viele Entwickler stoßen auf ein Problem, wenn sie einen horizontalen Bereich in ein vertikales Array umwandeln wollen, ohne einen Haufen Code zu schreiben. Die gute Nachricht ist, dass Aspose.Cells das kinderleicht macht.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das zeigt, **wie man WRAPCOLS verwendet**, wie man **ein Excel-Workbook im C#‑Stil erstellt**, wie man **Daten zu Excel hinzufügt** und sogar, wie man **die Formelb berechnung erzwingt**, sodass die Ergebnisse sofort angezeigt werden. Wir werden außerdem **wie man WRAPROWS verwendet** für die entgegengesetzte Transformation einstreuen. Am Ende haben Sie ein sofort ausführbares Programm und ein klares Verständnis dafür, warum jeder Schritt wichtig ist.

---

![Beispiel für die Verwendung von WRAPCOLS in C#](alt="Screenshot, der die Excel-Arbeitsmappe nach Verwendung von WRAPCOLS in C# zeigt")

## Was dieser Leitfaden abdeckt

* Ein neues Workbook mit Aspose.Cells einrichten.
* Zellen programmgesteuert befüllen (**add data to Excel**).
* Die `WRAPCOLS`‑Funktion anwenden, um eine Zeile in eine Spalte zu verwandeln.
* `WRAPROWS` verwenden, um eine Spalte zurück in eine Zeile zu drehen (**how to use wraprows**).
* Die Engine zwingen, Formeln sofort zu berechnen (**force formula calculation**).
* Die Datei speichern und die Ausgabe prüfen.

Keine externe Dokumentation erforderlich – alles, was Sie benötigen, finden Sie hier.

---

## Wie man WRAPCOLS in C# verwendet – Schritt‑für‑Schritt‑Implementierung

Unten finden Sie die vollständige Quelldatei. Sie können sie gerne in ein neues Konsolenprojekt kopieren, das Aspose.Cells‑NuGet‑Paket hinzufügen und **F5** drücken.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Warum jede Zeile wichtig ist

| Schritt | Erklärung |
|------|-------------|
| **1️⃣ Ein neues Workbook erstellen** | Dies ist die Grundlage. Aspose.Cells behandelt ein `Workbook`‑Objekt als die gesamte Excel‑Datei, sodass Sie effektiv **ein Excel‑Workbook im C#‑Stil erstellen**. |
| **2️⃣ Das erste Arbeitsblatt holen** | Ein neues Workbook enthält immer mindestens ein Arbeitsblatt (`Worksheets[0]`). Der frühe Zugriff verhindert Null‑Referenz‑Überraschungen. |
| **3️⃣ Daten zu Excel hinzufügen** | Durch die Verwendung von `PutValue` **fügen wir Daten zu Excel hinzu**, ohne uns um die Zellenformatierung kümmern zu müssen. Die Zahlen `1` und `2` sind unsere Testdaten für die Wrap‑Funktionen. |
| **4️⃣ Wie man WRAPCOLS verwendet** | `WRAPCOLS(A1:B1, 1)` weist Excel an, den Bereich `A1:B1` zu nehmen und seine Werte vertikal, jeweils eine pro Zeile, auszugeben. Das Ergebnis landet in `C1` und erstreckt sich nach unten (`C1`, `C2`, …). |
| **5️⃣ Wie man WRAPROWS verwendet** | `WRAPROWS(A1:B1, 2)` macht das Gegenteil: Es erzeugt eine horizontale Ausgabe, die beiden Werte in einer einzigen Zeile beginnend bei `C2` platziert. |
| **6️⃣ Formelberechnung erzwingen** | Standardmäßig kann Aspose.Cells die Berechnung bis zum Öffnen der Datei in Excel verzögern. Der Aufruf von `CalculateFormula()` **erzwingt die Formelberechnung**, sodass Sie die Ergebnisse sofort nach dem Speichern auslesen können. |
| **7️⃣ Das Workbook speichern** | Der letzte Schritt schreibt alles auf die Festplatte. Öffnen Sie die resultierende `WrapFunctions.xlsx`, um das Ergebnis zu sehen. |

## Excel Workbook in C# erstellen – Umgebung einrichten

Bevor Sie den Code ausführen, stellen Sie sicher, dass Sie die richtigen Werkzeuge haben:

1. **.NET 6.0+** – Die neueste LTS‑Version funktioniert am besten.
2. **Visual Studio 2022** (oder VS Code mit der C#‑Erweiterung).
3. **Aspose.Cells für .NET** – Installation über NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. Ein beschreibbarer Ordner für die Ausgabedatei.

Diese Voraussetzungen sind minimal; weder COM‑Interop noch eine Office‑Installation sind erforderlich, weshalb Aspose.Cells eine beliebte Wahl für serverseitige Excel‑Generierung ist.

## Daten zu Excel hinzufügen – Best Practices

Wenn Sie **Daten zu Excel** programmgesteuert **hinzufügen**, beachten Sie diese Tipps:

* **Verwenden Sie `PutValue`** für rohe Zahlen oder Zeichenketten; es erkennt den Datentyp automatisch.
* **Vermeiden Sie das Hard‑Coden von Zelladressen** in großen Projekten – nutzen Sie Schleifen oder benannte Bereiche für Skalierbarkeit.
* **Setzen Sie Zellstile sparsam** ein; jede Stiländerung verursacht Overhead. Wenn Sie Formatierung benötigen, erstellen Sie ein einzelnes Stil‑Objekt und wenden es auf mehrere Zellen an.

In unserem kleinen Beispiel fügen wir nur zwei Zahlen ein, aber dasselbe Muster skaliert auf tausende von Zeilen.

## Wie man WRAPROWS verwendet – Beispiel für ein horizontales Array

Wenn Sie das Gegenteil von `WRAPCOLS` benötigen, ist `WRAPROWS` Ihre Lösung. Die Syntax lautet:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – der Bereich, den Sie transformieren möchten.
* `rows_per_item` – optional; gibt an, wie viele Zeilen jedes Element belegt. In unserer Demo haben wir `2` verwendet, um beide Werte in einer einzigen Zeile zu erzwingen.

Sie können experimentieren, indem Sie das zweite Argument ändern:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Öffnen Sie die Arbeitsmappe und Sie werden sehen, dass die Werte über drei Spalten verteilt werden, wobei jede Spalte die ursprünglichen Zahlen nach Bedarf wiederholt.

## Formelberechnung erzwingen – Wann und warum

Sie fragen sich vielleicht: „Muss ich wirklich `CalculateFormula()` aufrufen?“ Die Antwort ist **ja**, wenn:

* Sie planen, nach dem Speichern die berechneten Werte **programmgesteuert** auszulesen.
* Sie möchten sicherstellen, dass die Datei in Excel mit den bereits angezeigten korrekten Ergebnissen geöffnet wird.
* Sie laufen in einer **kopf­losen Umgebung** (z. B. einer Web‑API), in der kein Benutzer manuell eine Neuberechnung auslöst.

Das Überspringen dieses Schrittes beschädigt das Workbook nicht, aber die Zellen zeigen den Formelttext (`=WRAPCOLS(...)`) anstelle der berechneten Werte, bis Excel neu berechnet.

## Erwartete Ausgabe – Was zu erwarten ist

Nach dem Ausführen des Programms und dem Öffnen von `WrapFunctions.xlsx`:

| Zelle | Formel | Angezeigter Wert |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (in C1) und `2` (in C2) – eine vertikale Liste |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` in C2 und `2` in D2 – eine horizontale Liste |

Sie werden also eine Spalte von Werten sehen, die bei **C1** beginnt, und eine Zeile von Werten, die bei **C2** beginnt. Das bestätigt, dass beide Wrap‑Funktionen wie erwartet funktionieren.

## Randfälle & Variationen

| Szenario | Was ändert sich? | Vorgeschlagene Anpassung |
|----------|-------------------|--------------------------|
| **Large range (A1:Z1)** | Mehr Werte, die vertikal ausgegeben werden | Erhöhen Sie das zweite Argument von `WRAPCOLS`, wenn Sie mehrere Spalten pro Gruppe wünschen. |
| **Non‑numeric data** | Zeichenketten werden auf dieselbe Weise behandelt | Keine Code‑Änderung; `PutValue` akzeptiert jedes Objekt. |
| **Dynamic range** | Sie kennen die Größe zur Compile‑Zeit nicht | Verwenden Sie `sheet.Cells.MaxDataColumn` und `MaxDataRow`, um den Adress‑String zu erstellen. |
| **Multiple worksheets** | Sie müssen Wrap‑Funktionen auf verschiedenen Blättern anwenden | Referenzieren Sie das korrekte Arbeitsblatt (`workbook.Worksheets["Sheet2"]`). |

## Profi‑Tipps aus der Praxis

* **Pro‑Tipp:** Packen Sie die Workbook‑Erstellung in einen `using`‑Block, wenn Sie .NET Core 3.1+ anvisieren, um sicherzustellen, dass alle Ressourcen sofort freigegeben werden.
* **Achtung:** Das Setzen derselben Formel in einem großen Bereich ohne Aufruf von `CalculateFormula()` kann Leistungsengpässe verursachen. Verarbeiten Sie Formeln nach Möglichkeit stapelweise.
* **Tipp:** Wenn Sie die berechneten Werte im Code zurücklesen müssen, rufen Sie `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}