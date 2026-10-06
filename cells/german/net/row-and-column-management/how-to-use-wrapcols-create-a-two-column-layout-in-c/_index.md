---
category: general
date: 2026-02-15
description: Wie man WRAPCOLS verwendet, um ein zweispaltiges Layout zu erstellen,
  eine Formel hinzuzufügen und ein Sequenz‑Array in C#‑Arbeitsblättern zu erzeugen
  – Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: de
og_description: Wie man WRAPCOLS verwendet, um ein zweispaltiges Layout zu erstellen,
  Formeln hinzuzufügen und ein Sequenz‑Array in einem C#‑Arbeitsblatt zu generieren
  – vollständige Anleitung.
og_title: 'Wie man WRAPCOLS verwendet: Zweispaltiges Layout in C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Wie man WRAPCOLS verwendet: Erstellen eines zweispaltigen Layouts in C#'
url: /de/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man WRAPCOLS verwendet: Erstellen eines Zwei‑Spalten‑Layouts in C#

Haben Sie sich jemals gefragt, **wie man WRAPCOLS verwendet**, wenn Sie eine schnelle Zwei‑Spalten‑Ansicht in einem Excel‑ähnlichen Arbeitsblatt benötigen? Sie sind nicht allein. Viele Entwickler stoßen auf ein Problem, wenn sie versuchen, eine generierte Liste in ordentliche Spalten zu teilen, ohne für jede Zelle eine Schleife zu schreiben. Die gute Nachricht? Mit der `WRAPCOLS`‑Funktion können Sie eine einzelne Formel in `A1` einfügen und Excel (oder eine kompatible Engine) die schwere Arbeit erledigen lassen.

In diesem Tutorial führen wir Sie durch **wie man eine Formel hinzufügt**, die ein **Zwei‑Spalten‑Layout erstellt**, zeigen Ihnen **wie man Spalten** dynamisch erstellt und sogar **Sequenz‑Array**‑Werte on‑the‑fly erzeugt. Am Ende haben Sie ein vollständig ausführbares C#‑Snippet, das Sie in Ihr Projekt einfügen, ausführen und sofort einen ordentlichen Zwei‑Spalten‑Block erscheinen sehen.

## Was Sie lernen werden

- Der Zweck von `WRAPCOLS` und warum es eine bessere Alternative zum manuellen Schleifen ist.  
- Wie man **eine Formel hinzufügt** zu einer Arbeitsblattzelle mit C#.  
- Wie man ein Sequenz‑Array mit `SEQUENCE` erzeugt und in `WRAPCOLS` einspeist.  
- Tipps zum Neuberechnen des Blatts, damit die Formel sofort ausgewertet wird.  
- Umgang mit Randfällen (z. B. leere Arbeitsblätter, benutzerdefinierte Spaltenzahlen).

Keine externen Bibliotheken über ein Standard‑Excel‑Verarbeitungspaket hinaus werden benötigt – wir verwenden **ClosedXML** wegen seiner einfachen API, aber die Konzepte lassen sich auf EPPlus, SpreadsheetGear oder sogar Google Sheets über dessen API übertragen.

---

## Voraussetzungen

- .NET 6.0 oder höher (der Code kompiliert unter .NET Core und .NET Framework).  
- Ein Verweis auf **ClosedXML** (`dotnet add package ClosedXML`).  
- Grundlegende C#‑Kenntnisse – Sie sollten mit `using`‑Anweisungen und Objektinitialisierung vertraut sein.

Wenn Sie bereits eine Arbeitsmappe geöffnet haben, können Sie den Teil zur Dateierstellung überspringen und direkt zum Formelsektion springen.

---

## Schritt 1: Arbeitsblatt einrichten (Wie man Spalten erstellt)

Zuerst benötigen wir ein `Worksheet`‑Objekt, mit dem wir arbeiten können. In ClosedXML erhalten Sie es von einem `XLWorkbook`. Das untenstehende Snippet erstellt eine neue Arbeitsmappe, fügt ein Blatt namens *Demo* hinzu und holt sich eine Referenz namens `worksheet` zur Übersicht.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Warum umbenennen?**  
> Einen kurzen Variablennamen (`worksheet`) zu behalten, macht den späteren Code leichter lesbar, besonders wenn Sie mehrere Operationen verketten. Es spiegelt zudem den Namensstil wider, den Sie in den meisten Dokumentationen sehen, und reduziert die kognitive Belastung.

---

## Schritt 2: Formel schreiben (Wie man eine Formel hinzufügt + Sequenz‑Array erzeugt)

Jetzt kommt die magische Zeile. Wir setzen eine Formel in die Zelle **A1**, die zwei Dinge erledigt:

1. **Ein Sequenz‑Array** von sechs Zahlen erzeugen (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Diese Zahlen in zwei Spalten einwickeln** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Was passiert?**  
> `SEQUENCE(6)` erzeugt ein vertikales Array `{1;2;3;4;5;6}`. `WRAPCOLS` nimmt dieses Array dann und „wickelt“ es in die angegebene Spaltenzahl – in diesem Fall **2**. Das Ergebnis ist ein 3‑Zeilen × 2‑Spalten‑Block, der folgendermaßen aussieht:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Wenn Sie das zweite Argument zu **3** ändern, erhalten Sie stattdessen ein Drei‑Spalten‑Layout. Das ist das Kernprinzip von **wie man Spalten** on‑the‑fly erstellt, ohne manuelle Schleifen.

---

## Schritt 3: Arbeitsblatt neu berechnen (Sicherstellen, dass die Formel ausgewertet wird)

ClosedXML wertet Formeln nicht automatisch aus, wenn Sie sie schreiben. Sie müssen `Calculate()` auf der Arbeitsmappe (oder auf dem spezifischen Arbeitsblatt) aufrufen, um die Auswertung zu erzwingen.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Pro‑Tipp:** Wenn Sie mit großen Arbeitsmappen arbeiten, rufen Sie `Calculate()` nur für die Blätter auf, die tatsächlich geändert wurden. Das spart Speicher und beschleunigt die Verarbeitung.

Wenn Sie `WrapColsDemo.xlsx` öffnen, sehen Sie das Zwei‑Spalten‑Layout sauber befüllt in **A1:B3**. Kein zusätzlicher Code war nötig, um Zeilen oder Spalten zu durchlaufen – `WRAPCOLS` erledigte alles.

---

## Schritt 4: Ausgabe überprüfen (Was zu erwarten ist)

Nach dem Ausführen des Programms öffnen Sie die erzeugte Datei. Sie sollten sehen:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Wenn die Zahlen vertikal erscheinen (d. h. alle in Spalte A), prüfen Sie, ob Sie `worksheet.Calculate()` **nach** dem Setzen der Formel aufgerufen haben. Einige Engines benötigen außerdem `workbook.Calculate()`; das obige Snippet funktioniert für den integrierten Evaluator von ClosedXML.

---

## Häufige Variationen & Randfälle

### Ändern der Spaltenzahl

Um ein **Zwei‑Spalten‑Layout** mit einer anderen Zeilenanzahl zu erstellen, passen Sie einfach die Größe von `SEQUENCE` oder das zweite Argument von `WRAPCOLS` an:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Dies erzeugt einen 4‑Zeilen × 3‑Spalten‑Block (12 Zahlen, auf drei Spalten verteilt).

### Verwendung einer dynamischen Spaltenzahl

Wenn Ihre Spaltenzahl aus einer Variablen stammt, betten Sie sie mit String‑Interpolation ein:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Jetzt haben Sie **wie man eine Formel hinzufügt**, die zur Laufzeit angepasst wird.

### Leere Arbeitsblätter

Wenn das Arbeitsblatt leer ist, funktioniert `Calculate()` weiterhin – die Formel füllt die Zellen beginnend bei A1. Wenn Sie jedoch später Zeilen/Spalten löschen, die den Ausgabebereich überschneiden, können `#REF!`‑Fehler auftreten. Um das zu vermeiden, leeren Sie zuerst den Zielbereich:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Kompatibilität

`WRAPCOLS` und `SEQUENCE` sind Teil von Excels **Dynamic‑Array**‑Funktionen, eingeführt in Office 365. Wenn Sie ältere Excel‑Versionen anvisieren, existieren diese Funktionen nicht und Sie benötigen eine manuelle Schleife. Der Evaluator von ClosedXML spiegelt das aktuelle Excel‑Verhalten wider, sodass er für moderne Umgebungen sicher ist.

---

## Vollständiges funktionierendes Beispiel (Einfaches Kopieren‑Einfügen)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Erwartetes Ergebnis:** Beim Öffnen von *WrapColsDemo.xlsx* wird ein ordentliches Zwei‑Spalten‑Layout mit den Zahlen 1‑6 angezeigt, wie oben beschrieben.

---

## Fazit

Wir haben **wie man WRAPCOLS verwendet**, um **ein Zwei‑Spalten‑Layout zu erstellen**, gezeigt **wie man eine Formel** programmgesteuert hinzuzufügen und gesehen, wie `SEQUENCE` es ermöglicht, **Sequenz‑Array**‑Werte ohne Schleife zu **generieren**. Durch die Nutzung von Excels dynamischen Array‑Funktionen aus C# können Sie Ihren Code kompakt, lesbar und wartbar halten.

Als Nächstes könnten Sie erkunden:

- **Dynamische Zeilenzahlen erstellen** mit `ROWS` oder `COUNTA`.  
- **Ausgabe formatieren** (Rahmen, Zahlenformate) mit der Styling‑API von ClosedXML.  
- **Exportieren nach CSV** nach dem Aufbau des Layouts, für nachgelagerte Verarbeitung.

Probieren Sie es aus, passen Sie die Spaltenzahl an und sehen Sie, wie schnell Sie komplexe Tabellenkalkulationen prototypisieren können. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}