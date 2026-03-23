---
category: general
date: 2026-03-22
description: Wie man Lambda in C# verwendet, um mit Excel-Formeln zu arbeiten. Lernen
  Sie, Formeln in Zellen zu schreiben, Bereiche in ein Array zu konvertieren, das
  Array in der Konsole anzuzeigen und den Kotangens in Excel zu berechnen.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: de
og_description: Wie man Lambda in C# verwendet, um Excel‑Formeln zu manipulieren,
  einen Bereich in ein Array zu konvertieren, eine Formel in eine Zelle zu schreiben,
  ein Array in der Konsole anzuzeigen und den Kotangens in Excel zu berechnen.
og_title: Wie man Lambda in C# mit Excel‑Formeln verwendet – Schritt für Schritt
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Wie man Lambda in C# mit Excel-Formeln verwendet – Vollständiger Leitfaden
url: /de/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Lambda in C# mit Excel-Formeln verwendet – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man Lambda** verwendet, wenn Sie Excel aus C# automatisieren? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie die Leistungsfähigkeit der neuen dynamischen Array‑Funktionen von Excel mit der `LAMBDA`‑Fähigkeit von C# kombinieren müssen. Die gute Nachricht? Es ist eigentlich ziemlich einfach, sobald man sieht, wie die Teile zusammenpassen.

In diesem Tutorial führen wir Sie durch **das Schreiben einer Formel in eine Zelle**, **das Konvertieren eines Bereichs in ein Array**, **die Anzeige dieses Arrays in der Konsole** und sogar **die Berechnung des Kotangens in Excel** – und zeigen dabei **wie man Lambda** innerhalb eines `REDUCE`‑Aufrufs verwendet. Am Ende haben Sie ein ausführbares Snippet, das Sie in jedes .NET‑Projekt einbinden können, das Aspose.Cells (oder eine ähnliche Bibliothek) referenziert.

---

## Was Sie lernen werden

- Wie man **eine Formel in eine Zelle schreibt** mit C#.
- Wie man **einen Bereich in ein Array konvertiert** mit der `EXPAND`‑Funktion.
- Wie man **ein Array in der Konsole anzeigt** nach der Berechnung.
- Wie man **den Kotangens in Excel** mit `COT` und `COTH` berechnet.
- Die genaue Syntax für **wie man Lambda** innerhalb von Excels `REDUCE`‑Funktion aus C# verwendet.

> **Voraussetzung:** Sie benötigen eine aktuelle Version von .NET (Core 6+ oder .NET Framework 4.7+) und die Aspose.Cells für .NET‑Bibliothek, die über NuGet installiert wird.

---

## Schritt 1: Arbeitsmappe einrichten und Formel in Zelle schreiben

Das Erste, was wir tun, ist eine neue Arbeitsmappe zu erstellen und das erste Arbeitsblatt zu holen. Dann **schreiben wir eine Formel in eine Zelle** – in diesem Fall wird `A1` das Ergebnis eines `EXPAND`‑Aufrufs enthalten.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Warum das wichtig ist:** Das Schreiben der Formel direkt aus dem Code ermöglicht es Ihnen, komplexe Tabellenkalkulationen on the fly zu erzeugen, ohne Excel zu öffnen. Es legt auch die Grundlage für den nächsten Schritt, in dem wir **den Bereich in ein Array konvertieren**.

---

## Schritt 2: Bereich mit EXPAND in ein Array konvertieren

`EXPAND` ist Excels Methode, einen kleinen Bereich in eine größere Matrix zu verwandeln. Durch das Platzieren der Formel in `A1` wird Excel einen 4 × 5‑Block ausgehend von dieser Zelle ausgeben. Aus C# müssen wir die Werte nicht manuell kopieren – die Bibliothek übernimmt die schwere Arbeit, wenn wir `Calculate` aufrufen.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Wie man Lambda verwendet:** Noch nicht, aber bleiben Sie dran. Zuerst benötigen wir die Daten im Blatt, dann werden wir sie mit einem Lambda reduzieren.

---

## Schritt 3: LAMBDA innerhalb von REDUCE verwenden – Der Kern von „Wie man Lambda verwendet“

Excel 365 hat `REDUCE` eingeführt, das einen **Anfangswert**, einen **Bereich** und ein **LAMBDA** akzeptiert, das angibt, wie jedes Element kombiniert werden soll. Aus C# weisen wir einfach den Formel‑String zu; das Lambda befindet sich innerhalb der Excel‑Formel, nicht im C#‑Code.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Erklärung:**  
- `0` ist der Anfangs‑Accumulator (`acc`).  
- `A1:D4` ist der Bereich, den wir verarbeiten wollen (die ersten vier Spalten des Spill).  
- `LAMBDA(acc, x, acc + x)` weist Excel an, jede Zelle (`x`) zum Accumulator hinzuzufügen.  

Das ist das Wesentliche von **wie man Lambda** für Aggregationen in einem Tabellenkalkulations‑Kontext verwendet.

---

## Schritt 4: Kotangens in Excel berechnen – Von Grad zu hyperbolisch

Wenn Sie trigonometrische Ergebnisse benötigen, sind Excels Funktionen `COT` und `COTH` ein Kinderspiel. Wir werden sie jeweils in `G1` und `G2` platzieren.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Warum das praktisch ist:** Zu wissen, **wie man Kotangens in Excel berechnet**, kann Sie davor bewahren, eigenen mathematischen Code zu schreiben, besonders wenn die Arbeitsmappe mit Nicht‑Entwicklern geteilt wird.

---

## Schritt 5: Berechnung erzwingen und das erweiterte Array abrufen

Jetzt veranlassen wir die Arbeitsmappe, jede Formel zu berechnen, und holen dann das ausgegebene Array aus `A1`. Hier **zeigen wir das Array in der Konsole an**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Was Sie sehen werden:**  
- Eine schön formatierte 4 × 5‑Matrix, Zeile für Zeile ausgegeben.  
- Die von dem `REDUCE`‑Lambda berechnete Summe.  
- Die beiden Kotangens‑Werte.

Damit ist der Ablauf von **Formel in Zelle schreiben** bis **Array in der Konsole anzeigen** abgeschlossen.

---

## Vollständiges funktionierendes Beispiel (zum Kopieren‑Einfügen bereit)

Unten finden Sie das komplette Programm, das Sie in eine Konsolen‑App einfügen können. Denken Sie daran, zuerst das `Aspose.Cells`‑NuGet‑Paket hinzuzufügen (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Erwartete Konsolenausgabe (Werte können variieren, je nach dem Standardinhalt von B1:C2, die standardmäßig 0 sind):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Fühlen Sie sich frei, `B1:C2` vor dem Ausführen mit eigenen Zahlen zu füllen – die Matrix wird diese Werte widerspiegeln.

---

## Pro‑Tipps & häufige Fallstricke

- **Pro‑Tipp:** Wenn Sie möchten, dass der ausgegebene Bereich an einer anderen Stelle beginnt, ändern Sie einfach die Zielzelle (`A1`). Die `EXPAND`‑Funktion respektiert den Anker.
- **Achten Sie darauf:** Leere Zellen im Quellbereich werden im ausgegebenen Array zu `0`, was Ihre `REDUCE`‑Summe beeinflussen kann.
- **Randfall:** Wenn die Arbeitsmappe Formeln enthält, die von volatilen Funktionen abhängen (z. B. `NOW()`), rufen Sie `workbook.Calculate()` nach dem Setzen aller Formeln auf, um sicherzustellen, dass alles aktuell ist.
- **Leistungshinweis:** Bei sehr großen Spills sollten Sie die Größe im `EXPAND`‑Aufruf begrenzen; sonst könnten Sie mehr Speicher zuweisen als nötig.
- **Kompatibilität:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}