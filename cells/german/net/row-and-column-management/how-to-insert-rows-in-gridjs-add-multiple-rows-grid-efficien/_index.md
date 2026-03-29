---
category: general
date: 2026-03-29
description: Erfahren Sie, wie Sie schnell Zeilen in GridJs einfügen. Dieser Leitfaden
  behandelt auch, wie Sie Zeilen hinzufügen und mehrere Zeilen im Grid mit einer Batch‑Operation
  hinzufügen.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: de
og_description: Erfahren Sie, wie Sie schnell Zeilen in GridJs einfügen. Dieser Leitfaden
  zeigt, wie man Zeilen hinzufügt, mehrere Zeilen zum Grid hinzufügt und große Batch‑Einfügungen
  verarbeitet.
og_title: Wie man Zeilen in GridJs einfügt – Mehrere Zeilen effizient zum Grid hinzufügen
tags:
- GridJs
- C#
- data‑grid
title: So fügen Sie Zeilen in GridJs ein – Mehrere Zeilen effizient zum Grid hinzufügen
url: /de/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Zeilen in GridJs einfügt – Mehrere Zeilen im Grid effizient hinzufügen

Haben Sie sich jemals gefragt, **wie man Zeilen einfügt** in eine riesige GridJs‑Tabelle, ohne die Benutzeroberfläche zum Einfrieren zu bringen? Vielleicht sind Sie an eine Grenze gestoßen, wenn Sie versuchen, **Zeilen** einzeln hinzuzufügen, und die Leistung einfach zusammenbricht. Die gute Nachricht ist, dass GridJs eine Batch‑API bietet, die es Ihnen ermöglicht, **mehrere Zeilen im Grid** in einem einzigen Aufruf hinzuzufügen, sodass alles schnell bleibt, selbst wenn Sie mit Millionen von Einträgen arbeiten.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das genau zeigt, **wie man Zeilen einfügt** mit `InsertRowsBatch`. Sie sehen, warum Batching wichtig ist, wie das Ergebnis verifiziert wird und worauf Sie achten müssen, wenn der Ziel‑Index sehr groß ist. Am Ende können Sie mit Zuversicht tausend neue Datensätze in jede GridJs‑Instanz einfügen.

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie folgendes haben:

- .NET 6.0 oder höher (der Code kompiliert mit jedem aktuellen SDK)
- Eine Referenz auf das `GridJs` NuGet‑Paket (oder die DLL, wenn Sie eine benutzerdefinierte Build verwenden)
- Grundlegende C#‑Kenntnisse – Sie müssen kein Guru sein, nur mit Klassen und Methoden vertraut sein
- Eine IDE oder ein Editor Ihrer Wahl (Visual Studio, Rider, VS Code … alles funktioniert)

> **Pro‑Tipp:** Wenn Sie mit wirklich riesigen Grids (Zehntausenden von Millionen Zeilen) arbeiten wollen, aktivieren Sie `gridJs.EnableVirtualization = true;`, um das Rendering der UI leichtgewichtig zu halten.

## Schritt 1: Erstellen und Konfigurieren der GridJs‑Instanz

First things first: you need a live `GridJs` object. Think of it as the canvas on which you’ll paint rows.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Warum dieser Schritt wichtig ist:** Das Initialisieren des Grids und optionales Vorbefüllen mit Daten spiegelt ein real‑weltliches Szenario wider, in dem das Grid bereits eine große Menge an Informationen enthält. Der Batch‑Insert, den wir später ausführen, muss den nullbasierten Index respektieren, daher füllen wir vor, um den genauen Einfügepunkt zu veranschaulichen.

## Schritt 2: Verwenden Sie `InsertRowsBatch`, um **mehrere Zeilen im Grid** hinzuzufügen

Now the core of the tutorial – the call that actually **adds rows** in bulk. The method signature is `InsertRowsBatch(int startIndex, int count)`. In our example we’ll start at index 2 000 000 (which corresponds to the 2 000 001st row) and add ten rows.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Wie es funktioniert:** `InsertRowsBatch` reserviert intern die gewünschte Anzahl von Zeilen und verschiebt vorhandene Zeilen nach unten. Da die Operation in einer einzigen Transaktion durchgeführt wird, wird die UI nur einmal aktualisiert, weshalb diese Methode der empfohlene Weg ist, **wie man Zeilen effizient hinzufügt**.

## Schritt 3: Überprüfen Sie die Einfügung – Landeten die Zeilen an der erwarteten Stelle?

After the batch operation you’ll want to be sure the rows are where you think they are. The following helper reads the first and last rows of the newly added block and prints them to the console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Erwartete Ausgabe**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Die leeren Zellen zeigen an, dass die Zeilen Platzhalter sind, die auf Daten warten. Sie können sie nun einzeln befüllen oder ein weiteres Batch‑Update ausführen.

> **Hinweis zu Randfällen:** Wenn `startIndex` die aktuelle Zeilenanzahl überschreitet, fügt GridJs die neuen Zeilen automatisch am Ende ein. Ein negativer Index löst hingegen eine `ArgumentOutOfRangeException` aus, daher sollten Sie immer benutzereingebene Indizes validieren.

## Schritt 4: Neue Zeilen befüllen (optional aber üblich)

Often you don’t just want empty rows; you need to fill them with meaningful values. You can loop over the newly created range and call `SetCell` or a similar API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Sie könnten `PopulateNewRows(gridJs, startIndex, rowsToAdd);` direkt nach dem Batch‑Insert aufrufen, wenn die Zeilen sofort zur Anzeige bereit sein sollen.

## Schritt 5: Leistungstipps für sehr große Grids

When you’re dealing with **add multiple rows grid** in the millions, keep these tricks in mind:

1. **Batch size matters** – Inserting 10 000 rows at once can be faster than ten separate 1 000‑row batches because each batch incurs a single UI refresh.  
   **Die Batch‑Größe ist entscheidend** – Das Einfügen von 10 000 Zeilen auf einmal kann schneller sein als zehn separate 1 000‑Zeilen‑Batches, weil jeder Batch nur eine UI‑Aktualisierung verursacht.

2. **Turn off UI updates** – Some GridJs versions expose `grid.SuspendLayout()` / `grid.ResumeLayout()`. Wrap your batch inside these calls if you notice lag.  
   **Deaktivieren Sie UI‑Updates** – Einige GridJs‑Versionen stellen `grid.SuspendLayout()` / `grid.ResumeLayout()` bereit. Verpacken Sie Ihren Batch in diese Aufrufe, wenn Sie Verzögerungen bemerken.

3. **Use virtualization** – As shown earlier, `EnableVirtualization` dramatically reduces memory consumption and rendering time.  
   **Verwenden Sie Virtualisierung** – Wie bereits gezeigt, reduziert `EnableVirtualization` den Speicherverbrauch und die Renderzeit erheblich.

4. **Avoid deep copies** – Pass simple value types or lightweight objects to the grid; heavy objects force the grid to clone data, hurting performance.  
   **Vermeiden Sie tiefe Kopien** – Übergeben Sie einfache Werttypen oder leichte Objekte an das Grid; schwere Objekte zwingen das Grid, Daten zu klonen, was die Leistung beeinträchtigt.

## Vollständiges funktionierendes Beispiel

Putting everything together, here’s the complete program you can copy‑paste into a new console project:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Run the program, and you’ll see the console output confirming that the ten rows were inserted at the correct location and then populated.

## Fazit

We’ve covered **how to insert rows** in GridJs using the batch API, demonstrated **how to add rows** efficiently, and explored ways to **add multiple rows grid** without choking the UI. The key takeaways are:

- Use `InsertRowsBatch(startIndex, count)` for any bulk operation.
- Validate indices and consider virtualization for massive datasets.
- Populate rows after the batch if you need immediate content.

Next, you might want to explore **how to delete rows**, implement **undo/redo** for batch edits, or integrate GridJs with a back‑end service that streams data on demand. All of those topics build directly on the concepts you’ve just learned.

Feel free to experiment—change the batch size, try inserting at the very beginning of the grid, or combine multiple batches in a single transaction. The more you play, the more comfortable you’ll become with großen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}