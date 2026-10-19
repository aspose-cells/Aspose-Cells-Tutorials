---
category: general
date: 2026-07-13
description: Erstelle eine Excel‑Arbeitsmappe in C# und lerne, wie man einen benannten
  Bereich hinzufügt, einer Tabelle einen Namen zuweist und Namenskonflikte behandelt
  – alles in einem klaren Beispiel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: de
lastmod: 2026-07-13
og_description: Erstellen Sie eine Excel-Arbeitsmappe in C# mit Aspose.Cells. Erfahren
  Sie, wie Sie benannte Bereiche hinzufügen, Tabellennamen festlegen und Namenskonflikte
  in einer prägnanten, ausführbaren Anleitung lösen.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Excel-Arbeitsmappe in C# erstellen – benannten Bereich hinzufügen & Tabellennamen
  festlegen
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Excel-Arbeitsmappe in C# erstellen – benannten Bereich hinzufügen & Tabellennamen
  festlegen
url: /de/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe in C# erstellen – Vollständige Anleitung zum Hinzufügen benannter Bereiche und Festlegen von Tabellennamen

Haben Sie jemals **eine Excel-Arbeitsmappe** von Grund auf erstellen müssen und sich gefragt, wo ein benannter Bereich platziert wird oder wie man einer Tabelle eine eigene Kennung gibt? Sie sind nicht allein. In vielen Reporting‑ oder Datenexport‑Szenarien jonglieren Sie mit Bereichen, Tabellen und gelegentlichen Namenskollisionen.  

In diesem Tutorial führen wir Sie durch ein vollständig ausführbares Beispiel, das **eine Excel-Arbeitsmappe erstellt**, **einen benannten Bereich hinzufügt** und anschließend **einer Tabelle einen Namen zuweist** – und zeigen Ihnen genau, was zu tun ist, wenn Namen kollidieren. Am Ende kennen Sie das „Wie“ und das „Warum“ jedes Schrittes sowie einige Tipps, um Ihren Code sauber zu halten.

> **Schneller Gewinn:** Der Code verwendet die **Aspose.Cells**‑Bibliothek, die mit .NET 6+ funktioniert und keine Excel‑Installation auf dem Server erfordert.

---

## Was Sie benötigen

- **.NET 6 SDK** (oder jede aktuelle .NET‑Version)  
- **Aspose.Cells for .NET** NuGet‑Paket  
- Eine brauchbare IDE (Visual Studio, Rider oder VS Code)  
- Grundkenntnisse in C# – nichts Besonderes, nur die üblichen `using`‑Anweisungen

Wenn Sie das haben, können wir direkt mit dem **Excel‑Arbeitsmappe erstellen**‑Prozess beginnen.

---

## ## Excel-Arbeitsmappe erstellen – Schritt‑für‑Schritt‑Übersicht

Unten finden Sie das vollständige, sofort kopier‑fertige Programm. Es demonstriert alles von der Erstellung der Arbeitsmappe bis zum Umgang mit einem Namenskonflikt, wenn Sie versuchen, **einer Tabelle einen Namen zuzuweisen**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Erwartete Ausgabe** beim Ausführen des Programms:

```
Naming conflict detected:
A name with the same text already exists.
```

Und wenn Sie *DemoWorkbook.xlsx* öffnen, sehen Sie eine Tabelle mit dem Namen **Table1** und einen benannten Bereich namens **MyRange** – genau das, was wir beabsichtigt haben, ohne die Kollision.

---

## ## Benannten Bereich hinzufügen – Warum das wichtig ist

Ein **benannter Bereich** ist im Wesentlichen ein Alias für einen Zellenblock. Anstatt ständig `A1:B5` zu referenzieren, können Sie `MyRange` in Formeln, Datenvalidierungen oder sogar im Code verwenden. Das verbessert die Lesbarkeit und reduziert die Wahrscheinlichkeit von Tippfehler‑bezogenen Fehlern.

Im obigen Ausschnitt rufen wir auf:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Das erste Argument ist der **Name**, den Sie später verwenden.  
- Das zweite Argument ist die **Adresse** (relativ zum Arbeitsblatt).  

Falls Sie jemals **einen Bereich dynamisch hinzufügen** müssen, können Sie die Adresszeichenkette mit `Cell.GetRefersTo()` erstellen oder `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)` verwenden.

---

## ## Namen einer Tabelle zuweisen – Konflikte behandeln

Tabellen (auch *ListObjects* genannt) besitzen bereits eine eingebaute Namenseigenschaft. Standardmäßig benennt Aspose.Cells sie `Table1`, `Table2` usw. Wenn Sie einer Tabelle dieselbe Kennung wie einem bestehenden benannten Bereich zuweisen, wirft die Bibliothek eine Ausnahme – genau wie Excel.

Warum passiert das?

- Der Namensbereich von Excel ist **arbeitsmappenweit** für sowohl Bereiche als auch Tabellen.  
- Doppelte Namen würden Formeln mehrdeutig machen, daher blockiert die Engine sie.

### Profi‑Tipp

Wenn Sie wirklich benötigen, dass eine Tabelle einen logischen Namen mit einem Bereich teilt, sollten Sie **einen Präfix** für einen von beiden verwenden, z. B.:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Oder benennen Sie zuerst den Bereich um:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Beide Ansätze halten den Namensraum übersichtlich und vermeiden Laufzeitfehler.

---

## ## Tabellennamen festlegen – Best Practices

Wenn Sie **den Tabellennamen** programmgesteuert festlegen, beachten Sie folgende Richtlinien:

1. **Verwenden Sie ein konsistentes Präfix** (`tbl_`, `rng_` usw.) – es sagt sofort, um welches Objekt es sich handelt.  
2. **Bleiben Sie innerhalb von 255 Zeichen** – das Limit von Excel für Namen.  
3. **Vermeiden Sie Leerzeichen und Sonderzeichen** – nur Buchstaben, Zahlen und Unterstriche sind sicher.  
4. **Validieren Sie vor der Zuweisung** – eine schnelle Prüfung `if (!sheet.Names.Contains(name))` verhindert die von uns demonstrierte Kollision.  

Hier ist eine Hilfsmethode, die Sie in jedes Projekt einbinden können:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Der Aufruf `SafeSetTableName(sheet, table, "MyRange")` wandelt `MyRange` automatisch in `MyRange_1` um, falls ein Konflikt besteht, und stellt sicher, dass der **Excel‑Arbeitsmappe‑Erstellungs**‑Vorgang nie unerwartet abbricht.

---

## ## Voll funktionsfähiges Beispiel – Alles zusammenführen

Unten finden Sie eine kompakte Version, die Sie direkt in eine Konsolen‑App kopieren können. Sie enthält die Sicherheitsroutine und demonstriert den End‑zu‑End‑Ablauf.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Das Ausführen dieses Skripts erzeugt `FinalDemo.xlsx`, wobei die Tabelle `MyRange_1` (oder ein anderer eindeutiger Anhang) heißt und der Bereich `MyRange` bleibt. Keine Ausnahme, kein Rätsel – nur saubere, deterministische Benennung.

---

## ## Häufig gestellte Fragen (FAQ)

**Q: Kann ich einen benannten Bereich hinzufügen, der sich über mehrere Arbeitsblätter erstreckt?**  
A: Ja, aber Sie müssen die Adresse mit dem Blattnamen qualifizieren, z. B. `"Sheet1!A1:B5"`. Die Methode `Names.Add` akzeptiert dieses Format.

**Q: Unterstützt Aspose.Cells dynamische benannte Bereiche (wie OFFSET‑Formeln)?**  
A: Absolut. Sie können einen Formelfragment‑String anstelle einer statischen Adresse übergeben, z. B. `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: Was, wenn ich eine bestehende Tabelle umbenennen muss?**  
A: Setzen Sie einfach `table.Name = "` 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}