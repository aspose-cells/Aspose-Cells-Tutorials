---
category: general
date: 2026-02-26
description: Wenden Sie das Zahlenformat in Excel schnell an und lernen Sie, wie Sie
  eine Spalte als Währung formatieren, das Zahlenformat einer Spalte festlegen und
  die Schriftfarbe einer Spalte in nur wenigen Zeilen C# einstellen.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: de
og_description: Wenden Sie das Zahlenformat in Excel mit C# in einfachen Schritten
  an. Lernen Sie, eine Spalte als Währung zu formatieren, das Zahlenformat einer Spalte
  festzulegen und die Schriftfarbe einer Spalte für professionelle Tabellenkalkulationen
  zu setzen.
og_title: Zahlenformat in Excel anwenden – Vollständiger Leitfaden zur Spaltenformatierung
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Zahlenformat in Excel anwenden – Schritt‑für‑Schritt‑Anleitung zum Formatieren
  von Spalten
url: /de/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

– Wie man Excel‑Spalten in C# formatiert". Keep "apply number format excel" maybe keep original phrase? Let's translate: "Zahlenformat in Excel anwenden – Wie man Excel‑Spalten in C# formatiert". Good.

Now paragraph.

We'll translate.

Proceed.

Make sure to keep markdown formatting.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zahlenformat in Excel anwenden – Wie man Excel‑Spalten in C# formatiert

Haben Sie sich schon einmal gefragt, wie man **Zahlenformat in Excel anwenden** kann, während man bereits durch eine `DataTable` iteriert? Sie sind nicht allein. Die meisten Entwickler stoßen auf ein Problem, wenn sie gleichzeitig einen blauen Header‑Text *und* eine währungsformatierte Spalte im selben Importvorgang benötigen. Die gute Nachricht? Mit ein paar Zeilen C# und den richtigen Style‑Objekten lässt sich das erledigen, ohne das Blatt nachträglich zu bearbeiten.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, wie man **Spalte als Währung formatiert**, **Spaltenzahlenformat festlegt** für jede andere Spalte und sogar **Spalten‑Schriftfarbe festlegt** für Header. Am Ende haben Sie ein wiederverwendbares Muster, das Sie in jedes Aspose‑Cells‑ (oder ähnliches) Projekt einbinden können.

## Was Sie lernen werden

- Wie man eine `DataTable` abruft und jeder Spalte ein bestimmtes `Style` zuweist.
- Die genauen Schritte, um **Zahlenformat in Excel anzuwenden** mit `Worksheet.Cells.ImportDataTable`.
- Warum das Vorab‑Erstellen von Styles effizienter ist, als Zellen einzeln zu formatieren.
- Sonderfall‑Behandlung, wenn die Quelltabelle mehr Spalten hat, als Sie gestylt haben.
- Ein vollständiges, copy‑and‑paste‑fertiges Code‑Beispiel, das Sie noch heute ausführen können.

> **Voraussetzung:** Dieser Leitfaden geht davon aus, dass Sie Aspose.Cells für .NET (oder eine Bibliothek, die `Workbook`, `Worksheet`, `Style`‑APIs bereitstellt) in Ihrem Projekt referenziert haben. Wenn Sie eine andere Bibliothek verwenden, lassen sich die Konzepte direkt übertragen – ersetzen Sie einfach die Typnamen.

---

## Schritt 1: Die Quelldaten als DataTable abrufen

Bevor irgendeine Formatierung stattfinden kann, benötigen Sie die Rohdaten. In den meisten realen Szenarien stammen die Daten aus einer Datenbank, einer CSV‑Datei oder einer API. Der Übersicht halber mocken wir eine einfache `DataTable` mit zwei Spalten: *Product* (string) und *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Warum das wichtig ist:** Das Laden der Daten in eine `DataTable` liefert Ihnen eine tabellarische In‑Memory‑Darstellung, die `ImportDataTable` direkt verarbeiten kann, wodurch ein manuelles Einfügen Zelle‑für‑Zelle entfällt.

## Schritt 2: Ein Array von Styles erstellen – eins pro Spalte

Die `ImportDataTable`‑Überladung, die wir verwenden, akzeptiert ein Array von `Style`‑Objekten. Jeder Eintrag entspricht einem Spaltenindex. Wenn Sie einen Eintrag auf `null` lassen, erbt die Spalte den Standard‑Workbook‑Style.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro‑Tipp:** Das Deklarieren des Arrays *nach* dem Erstellen der `DataTable` stellt sicher, dass die Größe exakt passt und verhindert später `IndexOutOfRangeException`.

## Schritt 3: Schriftfarbe (Blau) für die erste Spalte festlegen

Eine häufige Anforderung ist, Header‑ oder Schlüsselspalten mit einer auffälligen Schriftfarbe zu versehen. Hier machen wir den Text der ersten Spalte blau.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Warum ein Style‑Objekt?** Styles sind wiederverwendbar und können in einem Rutsch angewendet werden, was weitaus schneller ist, als jede Zelle nach dem Import zu iterieren. Das Workbook cached den Style einmal und nutzt ihn für jede Zelle dieser Spalte wieder.

## Schritt 4: Die zweite Spalte als Währung formatieren

Excel‑interne Zahlenformate werden über einen Index identifiziert. `14` entspricht dem Standard‑Währungsformat (z. B. `$1,234.00`). Wenn Sie ein benutzerdefiniertes Format benötigen, können Sie stattdessen einen Format‑String zuweisen.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Sonderfall:** Verwendet Ihr Workbook ein Gebietsschema, in dem das Währungssymbol nicht `$` ist, passt sich derselbe Index automatisch an (z. B. `€` für deutsche Locale).

## Schritt 5: Die DataTable mit den definierten Styles importieren

Jetzt fügen wir alles zusammen. Die Methode `ImportDataTable` fügt die Daten ab Zelle `A1` (Zeile 0, Spalte 0) ein und wendet die zuvor vorbereiteten Styles an.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Der zweite Parameter `true` weist Aspose.Cells an, die erste Zeile der `DataTable` als Spalten‑Header zu behandeln.
- Die Koordinaten `0, 0` geben die linke obere Ecke an, an der der Import beginnt.
- `columnStyles` ordnet jeder Spalte den jeweiligen Style zu.

## Schritt 6: Das Workbook speichern (optional, aber praktisch zum Prüfen)

Wenn Sie das Ergebnis in Excel sehen möchten, speichern Sie das Workbook einfach auf die Festplatte. Dieser Schritt ist für die Formatierungslogik nicht zwingend nötig, aber für das Debugging sehr hilfreich.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Erwartete Ausgabe

| **Produkt** (blaue Schrift) | **Preis** (Währung) |
|------------------------------|----------------------|
| Apfel                        | $1.25                |
| Banane                       | $0.75                |
| Kirsche                      | $2.10                |

- Die *Produkt*‑Spalte erscheint in Blau und fällt dadurch hervor.
- Die *Preis*‑Spalte zeigt Werte mit dem Standard‑Währungssymbol und zwei Dezimalstellen.

---

## Häufig gestellte Fragen & Varianten

### Wie lege ich **Spaltenzahlenformat fest** für mehr als zwei Spalten fest?

Erweitern Sie einfach das `columnStyles`‑Array. Zum Beispiel, um in der dritten Spalte einen Prozentsatz anzuzeigen:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Was, wenn ich ein *benutzerdefiniertes* Währungsformat benötige, z. B. „USD 1,234.00“?

Ersetzen Sie die `Number`‑Eigenschaft durch einen Format‑String:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Kann ich **Spalten‑Schriftfarbe festlegen** für eine numerische Spalte, ohne das Zahlenformat zu beeinflussen?

Absolut. Styles sind kombinierbar. Sie können sowohl `Font.Color` als auch `Number` auf derselben `Style`‑Instanz setzen:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Was passiert, wenn die `DataTable` mehr Spalten hat als Styles?

Jede Spalte ohne expliziten Style (`null`‑Eintrag) erbt den Standard‑Style des Workbooks. Um versehentliche `null`s zu vermeiden, können Sie das gesamte Array zunächst mit einem Basis‑Style initialisieren:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Anschließend überschreiben Sie nur die Spalten, die Sie wirklich anpassen möchten.

### Funktioniert dieser Ansatz bei großen Datenmengen (10 k+ Zeilen)?

Ja. Da die Formatierung *einmal pro Spalte* vor dem Import erfolgt, bleibt die Operation O(N) bezüglich der Zeilen und der Speicherverbrauch gering. Das Durchlaufen jeder Zelle nach dem Import würde die Performance stark beeinträchtigen.

---

## Vollständiges, funktionierendes Beispiel (Copy‑Paste‑bereit)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Führen Sie das Programm aus, öffnen Sie `StyledReport.xlsx` und Sie sehen das Ergebnis von **Zahlenformat in Excel anwenden** sofort.

---

## Fazit

Wir haben gerade gezeigt, wie man **Zahlenformat in Excel anwenden** für eine importierte `DataTable` sauber und effizient umsetzt. Durch das Vorab‑Erstellen eines `Style[]`‑Arrays können Sie **Spalte als Währung formatieren**, **Spaltenzahlenformat festlegen** und **Spalten‑Schriftfarbe festlegen** in einem einzigen Aufruf – ohne nachträgliche Verarbeitung.

Erweitern Sie das Muster gern: bedingte Formatierung hinzufügen, Zellen für Überschriften zusammenführen oder Formeln einbetten. Die gleichen Prinzipien gelten und halten Ihren Code übersichtlich, während Ihre Tabellen professionell aussehen.

---

### Was kommt als Nächstes?

- Erkunden Sie **bedingte Formatierung**, um Werte hervorzuheben, die einen Schwellenwert überschreiten.
- Kombinieren Sie diese Technik mit **Pivot‑Tabellen‑Erstellung** für dynamische Berichte.
- Probieren Sie **Spaltenzahlenformat festlegen** für Datumsangaben, Prozentsätze oder benutzerdefinierte wissenschaftliche Notation.

Haben Sie eine eigene Variante ausprobiert? Teilen Sie sie in den Kommentaren – lassen Sie uns gemeinsam weiterentwickeln.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}