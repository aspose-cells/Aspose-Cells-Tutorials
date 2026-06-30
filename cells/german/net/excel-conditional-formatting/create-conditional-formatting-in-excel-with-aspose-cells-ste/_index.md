---
category: general
date: 2026-06-30
description: Erstellen Sie bedingte Formatierung in einer Excel-Arbeitsmappe mit Aspose.Cells.
  Erfahren Sie, wie Sie den Zellenhintergrund festlegen, Zellen ranken und die Datei
  programmgesteuert erstellen.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: de
og_description: Erstellen Sie bedingte Formatierung in einer Excel‑Arbeitsmappe mit
  Aspose.Cells. Folgen Sie diesem umfassenden Tutorial, um den Zellhintergrund festzulegen,
  Zellen zu ranken und Excel zu automatisieren.
og_title: Bedingte Formatierung in Excel mit Aspose.Cells erstellen
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Bedingte Formatierung in Excel mit Aspose.Cells erstellen – Schritt‑für‑Schritt‑Anleitung
url: /de/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bedingte Formatierung in Excel mit Aspose.Cells erstellen – Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, wie man **conditional formatting** in einer Excel‑Datei erstellt, ohne die Benutzeroberfläche zu öffnen? Sie sind nicht allein. Viele Entwickler müssen **excel workbook**‑Dateien on the fly erstellen, und das programmgesteuerte Vorgehen spart Stunden manueller Arbeit. In diesem Tutorial zeigen wir Ihnen genau, wie man **conditional formatting** erstellt, Zellen formatiert und sogar die Top‑Werte rankt – alles mit der leistungsstarken Aspose.Cells‑Bibliothek für .NET.

Wir gehen ein praxisnahes Beispiel durch: ein Score‑Sheet erzeugen, hohe Scores in hellgrün hervorheben und den Top‑3‑Performern einen goldenen Hintergrund geben. Am Ende wissen Sie **how to set cell background**, **how to rank cells** und **how to use Aspose** für anspruchsvolle Excel‑Automatisierung. Keine Ausschweifungen, nur eine vollständige, ausführbare Lösung, die Sie in jedes C#‑Projekt einbinden können.

## Was Sie lernen werden

- Wie man **excel workbook** mit Aspose.Cells erstellt  
- Wie man einen Bereich mit zufälligen Daten (Scores) füllt  
- Wie man **set cell background** mit Vollfarben festlegt  
- Wie man eine formelbasierte Regel anwendet, um **rank cells** zu ranken und die besten drei hervorzuheben  
- Wie man das Ergebnis als .xlsx‑Datei speichert  

Voraussetzungen: .NET 6+ (oder .NET Framework 4.6+), Visual Studio (oder jede C#‑IDE) und ein Verweis auf das Aspose.Cells‑NuGet‑Paket. Wenn Sie Aspose noch nie verwendet haben, keine Sorge – wir decken **how to use Aspose** von Grund auf ab.

---

![Beispiel für bedingte Formatierung in einer mit Aspose.Cells erzeugten Excel‑Arbeitsmappe](https://example.com/images/create-conditional-formatting.png "Screenshot, der die bedingte Formatierung in der erzeugten Excel‑Datei zeigt")

*Image alt text: Beispiel für bedingte Formatierung in einer mit Aspose.Cells erzeugten Excel‑Arbeitsmappe.*

## Wie man ein Excel‑Workbook mit Aspose.Cells erstellt

Zuerst das Wichtigste: Sie benötigen ein Workbook‑Objekt, mit dem Sie arbeiten können. Aspose.Cells macht das zu einem Einzeiler.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Warum benennen wir das Blatt um? Ein klarer Name (wie **Scores**) erleichtert das spätere Referenzieren, besonders wenn Sie die Datei mit nicht‑technischen Benutzern teilen.  

Jetzt, wo das Workbook existiert, füllen wir Spalte A mit zufälligen Scores.

## Wie man Daten füllt – Zufällige Scores erzeugen

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Ein kurzer Hinweis: `PutValue` erkennt den Datentyp automatisch, sodass Sie nicht zu `int` casten müssen. Die Schleife startet bei `i = 0`, schreibt aber in Zeile `i + 1`, weil Excel‑Zeilen 1‑basiert sind, während die `Cells`‑Collection 0‑basiert ist.

## Wie man den Zellenhintergrund für hohe Scores setzt

Jetzt **create conditional formatting**, das jeden Score ≥ 80 in einem hellgrünen Farbton färbt.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Die Eigenschaft `ForegroundColor` steuert die Füllfarbe, während `Pattern = BackgroundType.Solid` Excel anweist, eine einheitliche Füllung statt eines Farbverlaufs oder Musters zu verwenden. Das ist der Kern von **how to set cell background** basierend auf einem numerischen Schwellenwert.

## Wie man Zellen rankt und die Top‑3 hervorhebt

Das Ranking ist etwas kniffliger, weil wir eine Formel benötigen, die jede Zelle gegen den gesamten Bereich evaluiert. Aspose.Cells lässt Sie dieselbe Excel‑Formelsyntax verwenden, die Sie in der UI eingeben würden.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Warum `A2` in der Formel? Aspose evaluiert die Formel relativ zu jeder Zelle im Bereich, sodass `A2` automatisch zu `A3`, `A4` usw. wird, wenn die Regel zeilenweise angewendet wird. Die Funktion `RANK` liefert die Position eines Wertes innerhalb des angegebenen Bereichs, und der Teil `<=3` sorgt dafür, dass nur die drei höchsten Scores die goldene Füllung erhalten.

## Wie man das Workbook speichert

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Ersetzen Sie `YOUR_DIRECTORY` durch einen absoluten oder relativen Pfad, in den Ihre Anwendung schreiben darf. Nach dem Ausführen der Methode öffnen Sie die Datei in Excel und sehen:

- Hellgrüne Zellen für jeden Score ≥ 80  
- Goldene Zellen für die drei höchsten Scores, unabhängig davon, ob sie ebenfalls ≥ 80 sind  

Das ist die komplette **create conditional formatting**‑Pipeline.

---

## Vollständiges, ausführbares Beispiel

Hier ist die gesamte Methode noch einmal, bereit zum Kopieren‑Einfügen in eine Konsolen‑App oder jede C#‑Klasse:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Erwartetes Ergebnis

Wenn Sie `Scores_ConditionalFormatting.xlsx` öffnen:

- Zellen mit Werten **80** oder höher leuchten hellgrün.  
- Die drei höchsten Zahlen (auch wenn sie unter 80 liegen) erscheinen mit einem **gold**‑Hintergrund.  
- Alle anderen Zellen behalten den standardmäßigen weißen Hintergrund bei.

Dieser visuelle Hinweis zeigt einem Manager sofort, wer die Top‑Performer sind, ohne manuelles Sortieren.

---

## Häufige Fragen & Sonderfälle

**Was ist, wenn ich mehr als drei Top‑Scores benötige?**  
Ändern Sie einfach den Teil `<=3` der Formel zu `<=5` (oder einer beliebigen Zahl). Die Regel passt sich automatisch an.

**Kann ich mehrere Formatierungsbereiche anwenden?**  
Absolut. Rufen Sie `sheet.ConditionalFormattings.Add` erneut mit einem anderen Bereich auf und fügen Sie dann Bedingungen zu diesem neuen `ConditionalFormatting`‑Objekt hinzu.

**Was ist mit älteren Excel‑Versionen?**  
Aspose.Cells speichert standardmäßig im modernen `.xlsx`‑Format, das mit Excel 2007 und neuer kompatibel ist. Wenn Sie `.xls` benötigen, übergeben Sie `SaveFormat.Excel97To2003` an die `Save`‑Methode.

**Gibt es Performance‑Auswirkungen bei großen Tabellen?**  
Bedingte Formatierung wird als Metadaten gespeichert und beeinflusst die Dateigröße nicht wesentlich. Das Erzeugen von Hunderttausenden von Zeilen kann jedoch den Speicherverbrauch erhöhen – erwägen Sie die Verarbeitung in Batches.

---

## Nächste Schritte

Jetzt, wo Sie **how to create conditional formatting** gemeistert haben, könnten Sie folgendes erkunden:

- **How to create Excel charts** programmgesteuert (ein weiteres Aspose.Cells‑Juwel)  
- **How to set cell background** basierend auf Textwerten (z. B. „Pass/Fail“)  
- **How to use Aspose.Cells for data validation** und Dropdown‑Listen  

Jedes dieser Themen baut auf denselben Grundlagen auf, die Sie gerade gelernt haben, sodass Sie sich sofort zu Hause fühlen.

---

## Zusammenfassung

Wir haben ein komplettes End‑to‑End‑Beispiel durchlaufen, wie man **create conditional formatting** in einer Excel‑Arbeitsmappe mit Aspose.Cells erstellt. Vom Initialisieren des Workbooks, Befüllen der Daten, **setting cell background**, Ranken der Top‑Performer bis zum finalen Speichern der Datei – jeder Schritt wurde sowohl im Hinblick auf **how to rank cells** als auch **how to use Aspose** behandelt.  

Probieren Sie den Code aus, passen Sie die Schwellenwerte an und sehen Sie, wie schnell Sie polierte Berichte für jedes Geschäftsszenario erzeugen können. Haben Sie eine eigene Variante, die Sie teilen möchten? Hinterlassen Sie einen Kommentar unten – happy coding!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Automatisieren der Excel‑Bedingten Formatierung mit Aspose.Cells für Java: Ein vollständiger Leitfaden](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Wie man Excel‑Zellen erstellt & formatiert mit Aspose.Cells für Java: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Erstellen einer Excel‑Arbeitsmappe mit Aspose.Cells in Java: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}