---
date: 2026-02-09
description: Erfahren Sie, wie Sie Datenbeschriftungen zu einem Excel‑Diagramm hinzufügen
  und den Diagrammtyp mit Aspose.Cells für Java ändern, sowie Tooltips und Drill‑Down‑Interaktivität.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Datenbeschriftungen zu Excel-Diagramm mit Aspose.Cells Java hinzufügen
url: /de/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Datenbeschriftungen zu Excel-Diagramm hinzufügen und Diagrammtyp ändern – Aspose.Cells Java

Interaktive Diagramme verleihen Ihren Excel-Berichten ein neues Maß an Erkenntnissen, und **das Hinzufügen von Datenbeschriftungen zu Excel-Diagrammen** macht die Informationen sofort lesbar. In diesem Tutorial lernen Sie, wie Sie **Datenbeschriftungen zu Excel-Diagrammen hinzufügen**, den Diagrammtyp ändern und interaktive Java‑Lösungen mit Aspose.Cells erstellen. Außerdem zeigen wir Ihnen, wie Sie Tooltips und einen einfachen Drill‑Down‑Hyperlink hinzufügen, damit Ihr Publikum die Daten eingehend erkunden kann.

## Quick Answers
- **Welche Bibliothek wird verwendet?** Aspose.Cells for Java  
- **Kann ich den Diagrammtyp ändern?** Ja – ändern Sie einfach das `ChartType`‑Enum, wenn Sie das Diagramm erstellen.  
- **Wie füge ich einem Diagramm Tooltips hinzu?** Verwenden Sie die Data‑Label‑API (`setHasDataLabels(true)`) und aktivieren Sie die Anzeige des Wertes.  
- **Wird Drill‑Down unterstützt?** Sie können Hyperlinks an Datenpunkte anhängen, um ein einfaches Drill‑Down‑Verhalten zu erzielen.  
- **Voraussetzungen?** Java‑IDE, Aspose.Cells‑JAR und eine Excel‑Datei mit Beispieldaten.

## Prerequisites

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Java-Entwicklungsumgebung (JDK 8+ empfohlen)  
- Aspose.Cells for Java Bibliothek (Download von [here](https://releases.aspose.com/cells/java/))  
- Eine Beispielarbeitsmappe (`data.xlsx`) mit den Daten, die Sie visualisieren möchten  

## Schritt 1: Einrichten Ihres Java-Projekts

1. Erstellen Sie ein neues Java-Projekt in Ihrer bevorzugten IDE (IntelliJ IDEA, Eclipse usw.).  
2. Fügen Sie das Aspose.Cells-JAR dem Build-Pfad Ihres Projekts oder den Maven/Gradle-Abhängigkeiten hinzu.

## Schritt 2: Daten laden

Um mit Diagrammen zu arbeiten, benötigen Sie zunächst eine Arbeitsmappe, die im Speicher geladen ist.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Schritt 3: Erstellen eines Diagramms (und Ändern des Typs)

Sie können jeden Diagrammtyp wählen, der zu Ihrer Analyse passt. Im Folgenden erstellen wir ein **Säulendiagramm**, aber Sie können ganz einfach zu einem Linien-, Kreis- oder Balkendiagramm wechseln, indem Sie das `ChartType`‑Enum ändern.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Profi‑Tipp:** Um **den Excel-Diagrammtyp zu ändern**, ersetzen Sie `ChartType.COLUMN` durch `ChartType.LINE`, `ChartType.PIE` usw.

## Schritt 4: Interaktivität hinzufügen

### 4.1. Tooltips hinzufügen (Tooltips zum Diagramm hinzufügen)

Tooltips erscheinen, wenn der Benutzer über einen Datenpunkt fährt. Der folgende Code aktiviert Datenbeschriftungen und zeigt den Wert als Tooltip an.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Datenbeschriftungen hinzufügen – **Datenbeschriftungen zu Excel-Diagramm hinzufügen**

Datenbeschriftungen bieten einen dauerhaften visuellen Hinweis direkt im Diagramm. Sie können sie als Callouts anzeigen, um die Lesbarkeit zu verbessern.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Warum Datenbeschriftungen hinzufügen?** Das direkte Einfügen von Datenbeschriftungen in das Diagramm eliminiert die Notwendigkeit, dass Benutzer über das Diagramm fahren oder Werte erraten müssen, und verbessert die Klarheit des Berichts.

### 4.3. Drill‑Down implementieren (Hyperlink auf einem Datenpunkt)

Eine einfache Möglichkeit, Drill‑Down‑Funktionalität hinzuzufügen, besteht darin, einen Hyperlink an einen bestimmten Punkt anzuhängen. Durch Klicken auf den Punkt wird eine Webseite mit detaillierten Informationen geöffnet.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Schritt 5: Arbeitsmappe speichern

Nachdem Sie das Diagramm konfiguriert haben, speichern Sie die Arbeitsmappe, damit die interaktiven Funktionen in der Ausgabedatei gespeichert werden.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Häufige Probleme & Lösungen

| Problem | Lösung |
|-------|----------|
| **Tooltips werden nicht angezeigt** | Stellen Sie sicher, dass `setHasDataLabels(true)` vor der Konfiguration von `setShowValue(true)` aufgerufen wird. |
| **Hyperlink ist nicht anklickbar** | Überprüfen Sie, ob das Ausgabeformat Hyperlinks unterstützt (z. B. XLSX, nicht CSV). |
| **Diagrammtyp ändert sich nicht** | Überprüfen Sie, ob Sie beim Hinzufügen des Diagramms das richtige `ChartType`‑Enum geändert haben. |

## Häufig gestellte Fragen

**F: Wie kann ich den Diagrammtyp ändern, nachdem er erstellt wurde?**  
A: Sie müssen ein neues Diagramm mit dem gewünschten `ChartType` erstellen. Aspose.Cells bietet keine In‑Place‑Typkonvertierung, daher entfernen Sie das alte Diagramm und fügen ein neues hinzu.

**F: Kann ich das Aussehen von Tooltips anpassen?**  
A: Ja. Verwenden Sie die `DataLabel`‑Eigenschaften wie `setFontSize`, `setFontColor` und `setBackgroundColor`, um den Tooltip‑Text zu gestalten.

**F: Wie gehe ich mit Benutzerinteraktionen in einer Webanwendung um?**  
A: Exportieren Sie die Arbeitsmappe in eine HTML‑ oder XLSX‑Datei und verwenden Sie JavaScript auf der Client‑Seite, um Klick‑Ereignisse auf Diagrammelementen zu erfassen.

**F: Wo finde ich weitere Beispiele und Dokumentation?**  
A: Besuchen Sie die [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) für eine vollständige Liste der diagrammbezogenen Klassen und Methoden.

## Fazit

Sie wissen jetzt, wie Sie **Datenbeschriftungen zu Excel-Diagrammen hinzufügen**, **den Excel-Diagrammtyp ändern**, **interaktive Java-Diagrammlösungen erstellen** und diese mit Tooltips, Datenbeschriftungen und Drill‑Down‑Hyperlinks mithilfe von Aspose.Cells für Java anreichern. Diese Verbesserungen machen Ihre Excel-Berichte für Endbenutzer deutlich ansprechender und aufschlussreicher.

---

**Zuletzt aktualisiert:** 2026-02-09  
**Getestet mit:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}