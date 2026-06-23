---
category: general
date: 2026-03-22
description: Erfahren Sie, wie Sie Pivot-Tabellen in C# mit Aspose.Cells duplizieren.
  Dieser Leitfaden zeigt außerdem, wie Sie Zeilen kopieren und eine Excel-Arbeitsmappe
  in C# laden, um eine nahtlose Excel‑Automatisierung beim Kopieren von Zeilen zu
  ermöglichen.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: de
og_description: Wie du eine Pivot-Tabelle in C# duplizierst? Folge diesem kurzen Tutorial,
  um eine Excel-Arbeitsmappe in C# zu laden, Zeilen zu kopieren und die Excel‑Automatisierung
  zum Kopieren von Zeilen zu meistern.
og_title: Wie man Pivot in C# dupliziert – Vollständiger Leitfaden
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Wie man Pivot in C# dupliziert – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot in C# dupliziert – Vollständige Schritt‑für‑Schritt-Anleitung

Haben Sie sich jemals gefragt, **wie man Pivot**‑Tabellen programmgesteuert dupliziert, ohne sie manuell in Excel zu ziehen? Sie sind nicht der Einzige. In vielen Reporting‑Pipelines wird das gleiche Pivot‑Layout auf einem neuen Satz von Zeilen benötigt, und es von Hand zu erledigen ist Zeitverschwendung.  

Die gute Nachricht? Mit ein paar Zeilen C# können Sie eine Excel‑Arbeitsmappe laden, den Bereich definieren, der das Pivot enthält, und **wie man Zeilen kopiert**, sodass das Pivot an einem neuen Ort erscheint – alles in einem automatisierten Durchlauf. In diesem Tutorial behandeln wir außerdem die Grundlagen von **load excel workbook c#** und geben Ihnen eine solide Grundlage für **excel automation copy rows**‑Aufgaben.

> **Was Sie am Ende wissen werden**  
> • Ein vollständiges, ausführbares Beispiel, das eine Pivot‑Tabelle dupliziert.  
> • Eine Erklärung, warum jede Zeile wichtig ist.  
> • Tipps zum Umgang mit Sonderfällen wie ausgeblendeten Arbeitsblättern oder mehreren Pivots.

---

## Voraussetzungen

- **.NET 6.0** (oder eine aktuelle .NET‑Version) installiert.  
- **Aspose.Cells for .NET** – die Bibliothek, die wir zur Manipulation von Excel‑Dateien verwenden. Sie können sie über NuGet beziehen:  

```bash
dotnet add package Aspose.Cells
```  

- Eine Quellarbeitsmappe (`Source.xlsx`), die bereits eine Pivot‑Tabelle im Bereich **A1:J20** enthält (der Bereich, den wir duplizieren werden).  
- Grundlegende Kenntnisse der C#‑Syntax – nichts Besonderes, nur die üblichen `using`‑Anweisungen und die `Main`‑Methode.

Falls Ihnen etwas davon unbekannt ist, machen Sie eine kurze Pause und installieren Sie das Paket; der Rest der Anleitung geht davon aus, dass die Bibliothek einsatzbereit ist.

![Illustration of how to duplicate pivot in C# using Aspose.Cells](https://example.com/duplicate-pivot.png "how to duplicate pivot in C# illustration")

*Bildbeschreibung: "how to duplicate pivot in C# example showing source and duplicated pivot rows".*

## Schritt 1: Excel‑Arbeitsmappe laden C# – Öffnen der Datei

Das allererste, was Sie tun müssen, wenn Sie **load excel workbook c#** ausführen möchten, ist, eine `Workbook`‑Instanz zu erstellen, die auf Ihre Datei zeigt. Dieses Objekt gibt Ihnen Zugriff auf jedes Arbeitsblatt, jede Zelle und jedes Pivot in der Datei.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Warum das wichtig ist:**  
`Workbook` abstrahiert die gesamte Excel‑Datei in ein In‑Memory‑Modell. Ohne sie zuerst zu laden, können Sie den Ort des Pivots nicht untersuchen oder Zeilen kopieren. Außerdem erkennt der Konstruktor automatisch das Dateiformat (XLS, XLSX, CSV usw.), sodass Sie keinen zusätzlichen Code zur Format­erkennung benötigen.

## Schritt 2: Wie man Zeilen kopiert – Definieren des Pivot‑Bereichs

Jetzt, wo die Arbeitsmappe im Speicher ist, müssen wir Aspose.Cells mitteilen, welche Zeilen das Pivot enthalten. In unserem Beispiel befindet sich das Pivot in **A1:J20**, was den Zeilen **0‑19** (nullbasierte Indizierung) entspricht. Wir packen das in eine `CellArea`‑Struktur.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Warum wir `CellArea` verwenden:**  
Es ist eine leichtgewichtige Methode, um einen rechteckigen Block zu beschreiben. Wenn Sie später `CopyRows` aufrufen, liest die Methode dieses Objekt, um genau zu wissen, welche Zeilen dupliziert werden sollen. Wenn Sie den Bereich jemals anpassen müssen (z. B. das Pivot wächst bis Spalte K), ändern Sie nur den Wert von `endColumn`.

## Schritt 3: Zugriff auf das Ziel‑Arbeitsblatt

Die meisten Arbeitsmappen haben ein einzelnes Blatt, aber die API funktioniert genauso bei mehreren Blättern. Holen Sie sich das erste Arbeitsblatt (Index 0) – dort befindet sich das ursprüngliche Pivot.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro‑Tipp:**  
Wenn Sie benannte Blätter haben, können Sie diese auch per Name abrufen: `workbook.Worksheets["Sheet1"]`. Das hilft, harte Index‑Kodierungen zu vermeiden, wenn sich die Struktur der Arbeitsmappe ändert.

## Schritt 4: Wie man Zeilen kopiert – Duplizieren der Pivot‑Tabelle

Hier ist das Kernstück von **how to duplicate pivot**: Wir kopieren die Zeilen, die das Pivot enthalten, an einen neuen Ort. In unserem Fall beginnen wir bei Zeile 31 (nullbasierter Index 30). Die Methode `CopyRows` kopiert *sowohl* die Daten als auch den zugrunde liegenden Pivot‑Cache, sodass die neuen Zeilen sich exakt wie das Original verhalten.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Was passiert im Hintergrund?**  
`CopyRows` klont jede Zeile und bewahrt Formeln, Formatierungen und Pivot‑Definitionen. Da der Pivot‑Cache auf Arbeitsmappen‑Ebene liegt, verweist das duplizierte Pivot automatisch auf dieselbe Datenquelle – keine zusätzliche Konfiguration nötig.

**Sonderfall – ausgeblendete Zeilen:**  
Wenn eine der Zeilen im Quellbereich ausgeblendet ist, bleibt sie nach dem Kopieren ausgeblendet. Wenn Sie sie einblenden möchten, rufen Sie nach dem Kopieren `worksheet.Rows[destRow].IsHidden = false` auf.

## Schritt 5: Arbeitsmappe speichern – Duplikat überprüfen

Schließlich schreiben Sie die Änderungen zurück auf die Festplatte. Sie können die Originaldatei überschreiben oder, sicherer, unter einem neuen Namen speichern, um Vorher/Nachher vergleichen zu können.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Ergebnis, das Sie sehen sollten:**  
Öffnen Sie `CopyWithPivot.xlsx`. Sie finden das ursprüngliche Pivot bei **A1:J20** und eine identische Kopie, die bei **A31:J50** beginnt. Beide Pivots können unabhängig aktualisiert werden, und alle an das Original angehängten Slicer funktionieren weiterhin für die Kopie, da sie denselben Cache teilen.

## Häufige Fragen & Variationen

### Kann ich mehrere Pivots gleichzeitig duplizieren?

Absolut. Durchlaufen Sie alle Pivot‑Tabellen (`worksheet.PivotTables`) und kopieren Sie den Bereich jeder einzelnen an ein anderes Ziel. Achten Sie nur darauf, dass sich die Zielbereiche nicht überschneiden.

### Was, wenn die Quellarbeitsmappe passwortgeschützt ist?

Aspose.Cells lässt Sie eine geschützte Datei öffnen, indem Sie das Passwort an den `Workbook`‑Konstruktor übergeben:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Wie kopiere ich Zeilen, ohne Formeln zu beeinflussen?

Wenn Sie nur die *Werte* (keine Formeln) benötigen, verwenden Sie `CopyRows` mit dem `CopyOptions`‑Flag:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Gibt es eine Möglichkeit, Zeilen in eine *andere* Arbeitsmappe zu kopieren?

Ja. Nachdem Sie Zeilen im Quellblatt kopiert haben, können Sie das Arbeitsblatt in eine andere `Workbook`‑Instanz klonen über `targetWorkbook.Worksheets.AddCopy(worksheet)`.

## Pro‑Tipps für zuverlässige Excel‑Automation‑Copy‑Rows

- **Validieren Sie den Bereich** vor dem Kopieren. Ein kurzer `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` verhindert Out‑of‑Range‑Fehler.  
- **Deaktivieren Sie die Berechnung**, während Sie große Bereiche kopieren: `workbook.Settings.CalcMode = CalcMode.Manual;` – das beschleunigt den Vorgang erheblich.  
- **Entsorgen Sie Objekte** (`workbook.Dispose()`), wenn Sie viele Dateien in einer Schleife verarbeiten, um native Ressourcen freizugeben.  
- **Protokollieren Sie den Vorgang** – besonders in Produktions‑Pipelines – damit Sie nachverfolgen können, welche Dateien verarbeitet wurden, und Fehler frühzeitig erkennen.

## Fazit

Sie wissen jetzt, **how to duplicate pivot**‑Tabellen in C# mit Aspose.Cells zu duplizieren, und Sie haben den kompletten Workflow von **load excel workbook c#** über **excel automation copy rows** bis zum finalen Speichern des Ergebnisses gesehen. Das Beispiel ist eigenständig, läuft sofort und kann erweitert werden, um mehrere Pivots, geschützte Dateien oder das Kopieren zwischen Arbeitsmappen zu handhaben.

Nächste Schritte? Versuchen Sie, das Skript anzupassen, um:

- Das duplizierte Pivot programmgesteuert zu aktualisieren (`pivotTable.RefreshData();`).  
- Den duplizierten Bereich in eine CSV für die Weiterverarbeitung zu exportieren.  
- Den Code in eine ASP.NET Core‑API zu integrieren, sodass Benutzer eine Datei hochladen und sofort eine duplizierte‑Pivot‑Version erhalten können.

Viel Spaß beim Coden, und möge Ihre Excel‑Automation stets reibungslos laufen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}