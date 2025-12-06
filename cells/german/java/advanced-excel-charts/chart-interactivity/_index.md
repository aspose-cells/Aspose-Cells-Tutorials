---
date: 2025-12-06
description: Erfahren Sie, wie Sie den Diagrammtyp in Excel ändern und interaktive
  Diagramme mit Java und Aspose.Cells erstellen. Fügen Sie dem Diagramm Tooltips,
  Datenbeschriftungen und Drill‑Down‑Funktionen für eine reichhaltigere Datenvisualisierung
  hinzu.
language: de
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Excel-Diagrammtyp mit Aspose.Cells Java ändern
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Diagrammtyp ändern und Interaktivität hinzufügen

## Einführung

Interaktive Diagramme verleihen Ihren Excel‑Berichten ein neues Maß an Erkenntnis, indem Benutzer über Datenpunkte fahren, klicken und sie direkt erkunden können. In diesem Tutorial **ändern Sie den Excel‑Diagrammtyp** und **erstellen interaktive Diagramm‑Java‑Lösungen** mit Aspose.Cells für Java. Wir zeigen, wie Sie Tooltips, Datenbeschriftungen und einen einfachen Drill‑Down‑Hyperlink zum Diagramm hinzufügen, damit Ihr Publikum tiefer in die Zahlen eintauchen kann.

## Schnellantworten
- **Welche Bibliothek wird verwendet?** Aspose.Cells für Java  
- **Kann ich den Diagrammtyp ändern?** Ja – ändern Sie einfach das `ChartType`‑Enum, wenn Sie das Diagramm erstellen.  
- **Wie füge ich Tooltips zu einem Diagramm hinzu?** Verwenden Sie die Datenbeschriftungs‑API (`setHasDataLabels(true)`) und aktivieren Sie die Anzeige des Werts.  
- **Wird Drill‑Down unterstützt?** Sie können Hyperlinks zu Datenpunkten hinzufügen, um ein einfaches Drill‑Down‑Verhalten zu erzielen.  
- **Voraussetzungen?** Java‑IDE, Aspose.Cells‑JAR und eine Excel‑Datei mit Beispieldaten.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Java‑Entwicklungsumgebung (JDK 8+ empfohlen)  
- Aspose.Cells für Java‑Bibliothek (Download [hier](https://releases.aspose.com/cells/java/))  
- Eine Beispielarbeitsmappe (`data.xlsx`) mit den Daten, die Sie visualisieren möchten  

## Schritt 1: Einrichten Ihres Java‑Projekts

1. Erstellen Sie ein neues Java‑Projekt in Ihrer bevorzugten IDE (IntelliJ IDEA, Eclipse usw.).  
2. Fügen Sie das Aspose.Cells‑JAR zu Ihrem Build‑Path oder zu den Maven/Gradle‑Abhängigkeiten hinzu.

## Schritt 2: Laden der Daten

Um mit Diagrammen zu arbeiten, müssen Sie zunächst eine Arbeitsmappe in den Speicher laden.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Schritt 3: Erstellen eines Diagramms (und Ändern seines Typs)

Sie können jeden Diagrammtyp wählen, der zu Ihrer Analyse passt. Im Folgenden erstellen wir ein **Säulendiagramm**, aber Sie können leicht zu einem Linien‑, Kreis‑ oder Balkendiagramm wechseln, indem Sie das `ChartType`‑Enum ändern.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro Tipp:** Um den **Excel‑Diagrammtyp zu ändern**, ersetzen Sie `ChartType.COLUMN` durch `ChartType.LINE`, `ChartType.PIE` usw.

## Schritt 4: Interaktivität hinzufügen

### 4.1. Tooltips hinzufügen (Tooltips zum Diagramm hinzufügen)

Tooltips erscheinen, wenn der Benutzer über einen Datenpunkt fährt. Der folgende Code aktiviert Datenbeschriftungen und zeigt den Wert als Tooltip an.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Datenbeschriftungen hinzufügen

Datenbeschriftungen bieten einen permanenten visuellen Hinweis direkt im Diagramm. Sie können sie als Callouts anzeigen, um die Lesbarkeit zu verbessern.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Drill‑Down implementieren (Hyperlink auf einen Datenpunkt)

Eine einfache Möglichkeit, Drill‑Down‑Funktionalität hinzuzufügen, besteht darin, einem bestimmten Punkt einen Hyperlink zuzuweisen. Ein Klick auf den Punkt öffnet eine Webseite mit detaillierten Informationen.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Schritt 5: Arbeitsmappe speichern

Nachdem Sie das Diagramm konfiguriert haben, speichern Sie die Arbeitsmappe, damit die interaktiven Funktionen in der Ausgabedatei erhalten bleiben.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Häufige Probleme & Lösungen

| Problem | Lösung |
|---------|--------|
| **Tooltips werden nicht angezeigt** | Stellen Sie sicher, dass `setHasDataLabels(true)` vor dem Aufruf von `setShowValue(true)` aufgerufen wird. |
| **Hyperlink ist nicht anklickbar** | Prüfen Sie, ob das Ausgabeformat Hyperlinks unterstützt (z. B. XLSX, nicht CSV). |
| **Diagrammtyp ändert sich nicht** | Vergewissern Sie sich, dass Sie das richtige `ChartType`‑Enum beim Hinzufügen des Diagramms geändert haben. |

## Häufig gestellte Fragen

**F: Wie kann ich den Diagrammtyp ändern, nachdem er erstellt wurde?**  
A: Sie müssen ein neues Diagramm mit dem gewünschten `ChartType` erstellen. Aspose.Cells bietet keine In‑Place‑Typkonvertierung, daher entfernen Sie das alte Diagramm und fügen ein neues hinzu.

**F: Kann ich das Aussehen von Tooltips anpassen?**  
A: Ja. Verwenden Sie die `DataLabel`‑Eigenschaften wie `setFontSize`, `setFontColor` und `setBackgroundColor`, um den Tooltip‑Text zu stylen.

**F: Wie gehe ich mit Benutzerinteraktionen in einer Webanwendung um?**  
A: Exportieren Sie die Arbeitsmappe in eine HTML‑ oder XLSX‑Datei und nutzen Sie JavaScript auf der Client‑Seite, um Klick‑Ereignisse auf Diagrammelemente zu erfassen.

**F: Wo finde ich weitere Beispiele und Dokumentation?**  
A: Besuchen Sie die [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) für eine vollständige Liste der diagrammbezogenen Klassen und Methoden.

## Fazit

Sie wissen jetzt, wie Sie den **Excel‑Diagrammtyp ändern**, **interaktive Diagramm‑Java‑Lösungen** erstellen und diese mit Tooltips, Datenbeschriftungen und Drill‑Down‑Hyperlinks mithilfe von Aspose.Cells für Java anreichern. Diese Erweiterungen machen Ihre Excel‑Berichte für Endbenutzer deutlich ansprechender und aufschlussreicher.

---

**Zuletzt aktualisiert:** 2025-12-06  
**Getestet mit:** Aspose.Cells für Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}