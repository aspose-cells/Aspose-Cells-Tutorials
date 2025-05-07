---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für Java Pivot-Tabellen in Excel erstellen. Automatisieren Sie die Datengruppierung und -analyse mit Quellcodebeispielen."
"linktitle": "Gruppieren von Daten in Pivot-Tabellen"
"second_title": "Aspose.Cells Java Excel-Verarbeitungs-API"
"title": "Gruppieren von Daten in Pivot-Tabellen"
"url": "/de/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gruppieren von Daten in Pivot-Tabellen


Pivot-Tabellen sind ein leistungsstarkes Tool zum Analysieren und Zusammenfassen von Daten in Tabellenkalkulationen. Sie ermöglichen das Gruppieren und Kategorisieren von Daten, um wertvolle Erkenntnisse zu gewinnen. In diesem Artikel erfahren Sie, wie Sie Daten in Pivot-Tabellen mithilfe von Aspose.Cells für Java effektiv gruppieren und erhalten Quellcodebeispiele.

## Einführung

Pivot-Tabellen bieten eine flexible Möglichkeit, Daten aus großen Datensätzen zu organisieren und zusammenzufassen. Sie ermöglichen Ihnen die Erstellung individueller Ansichten Ihrer Daten durch die Gruppierung in Kategorien oder Hierarchien. So können Sie Trends, Muster und Ausreißer in Ihren Daten leichter erkennen.

## Schritt 1: Erstellen Sie eine Pivot-Tabelle

Beginnen wir mit der Erstellung einer Pivot-Tabelle mit Aspose.Cells für Java. Unten sehen Sie ein Beispiel für die Erstellung einer Pivot-Tabelle aus einer Excel-Beispieldatei.

```java
// Laden Sie die Excel-Datei
Workbook workbook = new Workbook("sample.xlsx");

// Greifen Sie auf das Arbeitsblatt mit den Daten zu
Worksheet worksheet = workbook.getWorksheets().get(0);

// Geben Sie den Datenbereich an
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Angenommen, 20 Datenzeilen
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Angenommen, 4 Datenspalten

// Erstellen Sie eine Pivot-Tabelle basierend auf dem Datenbereich
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Holen Sie sich die Pivot-Tabelle nach Index
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Hinzufügen von Feldern zu Zeilen und Spalten
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Werte hinzufügen und Aggregation anwenden
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Speichern Sie die geänderte Excel-Datei
workbook.save("output.xlsx");
```

## Schritt 2: Daten gruppieren

In Aspose.Cells für Java können Sie Daten innerhalb der Pivot-Tabelle gruppieren, indem Sie `PivotField` Klasse. Hier ist ein Beispiel für die Gruppierung eines Felds in der Pivot-Tabelle:

```java
// Greifen Sie auf das Feld „Produkt“ in der Pivot-Tabelle zu
PivotField productField = pivotTable.getPivotFields().get("Product");

// Gruppieren Sie das Feld "Produkt" nach einem bestimmten Kriterium, z. B. nach dem Anfangsbuchstaben
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Speichern Sie die geänderte Excel-Datei mit gruppierten Daten
workbook.save("output_grouped.xlsx");
```

## Schritt 3: Gruppierung anpassen

Sie können die Gruppierungseinstellungen weiter anpassen, z. B. durch die Angabe datumsbasierter Gruppierungsintervalle oder benutzerdefinierter Gruppierungsregeln. Hier ist ein Beispiel für die Anpassung der datumsbasierten Gruppierung:

```java
// Greifen Sie auf das Feld „Datum“ in der Pivot-Tabelle zu (vorausgesetzt, es handelt sich um ein Datumsfeld).
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Gruppieren Sie Daten nach Monaten
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Speichern Sie die geänderte Excel-Datei mit benutzerdefinierter Datumsgruppierung
workbook.save("output_custom_grouping.xlsx");
```

## Abschluss

Das Gruppieren von Daten in Pivot-Tabellen ist eine wertvolle Technik zur Analyse und Zusammenfassung von Daten in Excel. Aspose.Cells für Java vereinfacht die Automatisierung dieses Prozesses. Mit den bereitgestellten Quellcodebeispielen können Sie Pivot-Tabellen erstellen, die Gruppierung anpassen und effizient Erkenntnisse aus Ihren Daten gewinnen.

## FAQs

### 1. Was ist der Zweck von Pivot-Tabellen in Excel?

Pivot-Tabellen in Excel dienen zum Zusammenfassen und Analysieren großer Datensätze. Sie ermöglichen die Erstellung individueller Ansichten Ihrer Daten und erleichtern so das Erkennen von Mustern und Trends.

### 2. Wie kann ich die Gruppierung von Daten in einer Pivot-Tabelle anpassen?

Sie können die Gruppierung der Daten in einer Pivot-Tabelle anpassen, indem Sie die `PivotField` Klasse in Aspose.Cells für Java. Damit können Sie Gruppierungskriterien wie datumsbasierte Intervalle oder benutzerdefinierte Regeln angeben.

### 3. Kann ich die Erstellung von Pivot-Tabellen mit Aspose.Cells für Java automatisieren?

Ja, Sie können die Erstellung von Pivot-Tabellen in Excel mit Aspose.Cells für Java automatisieren, wie in den bereitgestellten Quellcodebeispielen gezeigt.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}