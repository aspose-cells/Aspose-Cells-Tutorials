---
category: general
date: 2026-03-27
description: Wie man in C# mit Aspose.Cells eine Pivot‑Tabelle erstellt – lernen Sie,
  Daten hinzuzufügen, die Aktualisierung zu aktivieren und die Arbeitsmappe als xlsx
  zu speichern – in einem einzigen Tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: de
og_description: Wie man eine Pivot‑Tabelle in C# mit Aspose.Cells erstellt. Dieser
  Leitfaden zeigt, wie man Daten hinzufügt, die Aktualisierung aktiviert und die Arbeitsmappe
  als xlsx speichert.
og_title: Wie man Pivot‑Tabellen in C# erstellt – Komplettes Aspose.Cells‑Tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man Pivot in C# erstellt – Vollständiger Leitfaden mit Aspose.Cells
url: /de/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot-Tabellen in C# erstellt – Komplettes Aspose.Cells‑Tutorial

Haben Sie sich schon einmal gefragt, **wie man Pivot‑Tabellen** in C# erstellt, ohne sich mit COM‑Interop herumzuschlagen? Sie sind nicht allein. In vielen datengetriebenen Anwendungen benötigen wir eine schnelle Möglichkeit, rohe Verkaufszahlen in eine übersichtliche Zusammenfassung zu verwandeln, und Aspose.Cells macht das zum Kinderspiel.  

In diesem Tutorial gehen wir jeden Schritt durch: Daten hinzufügen, Pivot‑Tabelle erstellen, automatisches Aktualisieren aktivieren und schließlich **Arbeitsmappe als xlsx speichern**, damit Ihre Benutzer sie sofort in Excel öffnen können. Am Ende haben Sie eine einsatzbereite Datei `PivotRefresh.xlsx` und ein fundiertes Verständnis dafür, warum jede Zeile wichtig ist.

## Voraussetzungen

- .NET 6+ (oder .NET Framework 4.7.2 und neuer) – jede aktuelle Runtime funktioniert.
- Aspose.Cells für .NET – Sie können es über NuGet beziehen (`Install-Package Aspose.Cells`).
- Grundlegende Kenntnisse der C#‑Syntax – tiefgehendes Excel‑Wissen ist nicht nötig.

> **Pro‑Tipp:** Wenn Sie an einem Firmenrechner arbeiten, stellen Sie sicher, dass die Aspose‑Lizenz angewendet ist; sonst erhalten Sie ein Wasserzeichen in der erzeugten Datei.

## Schritt 1 – Wie man Daten zu einer neuen Arbeitsmappe hinzufügt

Bevor ein Pivot existieren kann, muss es eine Quelltabelle geben. Wir erstellen eine neue Arbeitsmappe, benennen das erste Arbeitsblatt *SalesData* und fügen ein paar Zeilen ein, die einen realen Verkaufs‑Dump nachahmen.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Warum das wichtig ist:**  
- Mit `PutValue` wird der Zellentyp automatisch gesetzt, sodass Sie sich später nicht um String‑/Zahlen‑Mismatches kümmern müssen.  
- Das Definieren von Kopfzeilen in Zeile 1 gibt der Pivot‑Engine etwas, worauf sie beim Zuordnen der Felder zurückgreifen kann.

## Schritt 2 – Ein Arbeitsblatt erstellen, das die Pivot‑Tabelle hostet

Eine Pivot‑Tabelle lebt auf einem eigenen Blatt, sodass die Quelldaten sauber bleiben und der Bericht übersichtlich ist.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Was, wenn Sie bereits ein Blatt haben?** Verweisen Sie einfach darauf über den Index (`workbook.Worksheets["MySheet"]`) anstatt ein neues hinzuzufügen.

## Schritt 3 – Quellbereich definieren (Wie man Daten → Bereich definiert)

Aspose.Cells benötigt ein `CellArea`‑Objekt oder einen Bereichs‑String, der sowohl Kopfzeilen als auch Daten umfasst. Hier gehen wir von maximal 100 Zeilen aus; passen Sie den Wert bei Bedarf an.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Randfall:** Wenn Ihr Datensatz dynamisch ist, können Sie die letzte benutzte Zeile mit `salesDataSheet.Cells.MaxDataRow` ermitteln und den Bereich entsprechend bauen.

## Schritt 4 – Wie man Pivot erstellt – Pivot‑Tabelle einfügen

Jetzt kommt der spaßige Teil: Wir sagen Aspose.Cells, dass es ein Pivot erstellen soll, das mit dem gerade definierten Bereich verknüpft ist.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Beachten Sie die Formel‑ähnliche Referenz (`=SalesData!A1:D100`). Das ist dieselbe Syntax, die Sie in Excel eingeben würden, wodurch die API intuitiv wirkt.

## Schritt 5 – Zeilen‑, Spalten‑ und Datenfelder konfigurieren (Wie man Daten → Felder hinzufügt)

Wir platzieren *Region* in den Zeilen, *Product* in den Spalten und summieren sowohl *Units* als auch *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Warum diese Indizes?**  
Aspose.Cells indiziert Spalten beginnend bei 0, sodass `0` auf *Region* zeigt. Die Methode `DataFields.Add` ermöglicht es Ihnen, das Feld umzubenennen (z. B. „Sum of Units“) und einen Aggregationstyp zu wählen – `Sum` ist für numerische Daten am gebräuchlichsten.

## Schritt 6 – Wie man das Aktualisieren aktiviert – Pivot beim Öffnen automatisch aktualisieren

Ändert sich die Quelldaten später, möchten Sie wahrscheinlich, dass das Pivot diese Änderungen automatisch widerspiegelt. Hier kommt `RefreshDataOnOpen` ins Spiel.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Hinweis:** Dieses Flag funktioniert nur, wenn die Arbeitsmappe in Excel geöffnet wird; innerhalb von Aspose.Cells wird nicht neu berechnet, es sei denn, Sie rufen `pivotTable.RefreshData()` manuell auf.

## Schritt 7 – Arbeitsmappe als XLSX speichern (Wie man Arbeitsmappe als XLSX speichert)

Zum Schluss schreiben wir die Datei auf die Festplatte. Das `.xlsx`‑Format ist der moderne, zip‑basierte Excel‑Dateityp, der überall funktioniert.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Beim Ausführen des Programms entsteht eine Datei namens **PivotRefresh.xlsx** im Ausführungsordner. Öffnen Sie sie in Excel und Sie sehen ein sauber aufgebautes Pivot mit *Region*-Zeilen, *Product*-Spalten und summierten *Units*- und *Revenue*-Werten. Da wir das Aktualisieren aktiviert haben, werden alle Änderungen am Blatt *SalesData* das Pivot beim nächsten Öffnen der Arbeitsmappe automatisch aktualisieren.

### Erwartete Ausgabe

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Die Zahlen variieren je nach den von Ihnen hinzugefügten Zeilen.)*

---

## Häufige Fragen & Varianten

### Was, wenn ich mehrere Pivot‑Tabellen brauche?

Sie können **Schritt 4** mit einem anderen Namen und einer anderen Position wiederholen. Jeder Aufruf von `PivotTables.Add` liefert einen neuen Index, den Sie zum Abrufen des Tabellenobjekts verwenden können.

### Wie ändere ich die Aggregation von *Sum* zu *Average*?

Ersetzen Sie `PivotTableDataAggregationType.Sum` durch `PivotTableDataAggregationType.Average` in den `DataFields.Add`‑Aufrufen.

### Kann ich das Pivot formatieren (Schriftarten, Farben)?

Ja. Nach dem Erstellen des Pivots können Sie auf dessen `Style`‑Eigenschaft zugreifen oder Zellformatierungen auf den Bereich anwenden, der das Pivot enthält. Beispiel:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Ist es möglich, nach dem Speichern der Arbeitsmappe weitere Zeilen hinzuzufügen?

Absolut. Laden Sie die Datei mit `new Workbook("PivotRefresh.xlsx")`, hängen Sie Zeilen an das Blatt *SalesData* an und rufen Sie `pivotTable.RefreshData()` auf, bevor Sie erneut speichern.

---

## Vollständiges Beispiel (Einfaches Kopieren & Einfügen)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Speichern Sie die Datei, führen Sie sie aus und öffnen Sie die erzeugte **PivotRefresh.xlsx** – Sie haben gerade **wie man Pivot‑Tabellen** in C# erstellt.

---

## Fazit

Wir haben behandelt, **wie man Pivot‑Tabellen** programmgesteuert erstellt, wie man **Daten hinzufügt**, wie man **das Aktualisieren aktiviert** und schließlich, wie man **die Arbeitsmappe als xlsx speichert** mit Aspose.Cells. Der Code

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}