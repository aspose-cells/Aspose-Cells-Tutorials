---
date: 2025-12-04
description: Erfahren Sie, wie Sie interaktive Diagramme in Java mit Aspose.Cells
  erstellen, Tooltips zum Diagramm hinzufügen und ein Drill‑Down-Diagramm für eine
  reichhaltigere Datenvisualisierung einbinden.
language: de
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Interaktives Diagramm in Java mit Aspose.Cells erstellen
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Interaktives Diagramm in Java erstellen

## Einführung

Interaktive Diagramme geben Ihren Benutzern die Möglichkeit, Datenpunkte zu erkunden, Details beim Überfahren anzuzeigen und sogar in tiefere Datensätze zu drillen – alles, ohne das Tabellenkalkulationsdokument zu verlassen. In diesem Tutorial lernen Sie **wie man interactive chart Java** Anwendungen mit Aspose.Cells. Wir gehen Schritt für Schritt auf das Hinzufügen von Tooltips, Datenbeschriftungen und die Implementierung einer Drill‑Down‑Funktion ein, damit Ihre Diagramme ansprechender und informativer werden.

## Schnelle Antworten
- **Welche Bibliothek wird verwendet?** Aspose.Cells for Java  
- **Kann ich Tooltips zum Diagramm hinzufügen?** Ja, über die NSeries Data‑label API  
- **Wird Drill‑Down unterstützt?** Ja, durch Anfügen von Hyperlinks an Datenpunkte  
- **Welches Dateiformat wird erzeugt?** Standard‑XLSX‑Arbeitsmappe mit eingebetteten Diagrammen  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Evaluierung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich  

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Eine Java‑Entwicklungsumgebung (JDK 8+ empfohlen)  
- Aspose.Cells for Java Bibliothek (Download von der offiziellen [Aspose release page](https://releases.aspose.com/cells/java/))  
- Eine Beispiel‑Excel‑Datei namens **data.xlsx**, die die zu visualisierenden Daten enthält  

## Schritt 1: Einrichten Ihres Java‑Projekts

1. Erstellen Sie ein neues Java‑Projekt in Ihrer bevorzugten IDE (IntelliJ IDEA, Eclipse, VS Code usw.).  
2. Fügen Sie die Aspose.Cells‑JAR zu Ihrem Klassenpfad hinzu – entweder indem Sie die JAR in den `libs`‑Ordner legen oder die Maven/Gradle‑Abhängigkeit hinzufügen.

## Schritt 2: Laden von Daten

Um ein interaktives Diagramm zu erstellen, benötigen Sie zunächst ein Arbeitsblatt mit Daten. Das folgende Snippet öffnet eine vorhandene Arbeitsmappe und greift auf das erste Arbeitsblatt zu.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Profi‑Tipp:** Stellen Sie sicher, dass der Datenbereich, den Sie diagrammieren möchten, zusammenhängend ist; Aspose.Cells erkennt den Bereich automatisch, wenn Sie die Serie binden.

## Schritt 3: Erstellen eines Diagramms

Jetzt erstellen wir ein Säulendiagramm und positionieren es im Arbeitsblatt. Sie können `ChartType.COLUMN` zu einem anderen Typ ändern (z. B. `ChartType.LINE`), wenn Sie einen anderen visuellen Stil bevorzugen.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Warum das wichtig ist:** Das programmatische Hinzufügen des Diagramms gibt Ihnen die volle Kontrolle über Größe, Position und Datenquelle, was für interaktive Erlebnisse entscheidend ist.

## Schritt 4: Hinzufügen von Interaktivität

### So fügen Sie Tooltips zum Diagramm hinzu

Tooltips (oder Datenbeschriftungen, die Werte anzeigen) helfen Benutzern, sofort die genaue Zahl hinter jedem Balken zu sehen. Der folgende Code aktiviert Datenbeschriftungen und konfiguriert sie so, dass der Wert angezeigt wird.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### So fügen Sie Datenbeschriftungen (Callouts) hinzu

Wenn Sie möchten, dass die Beschriftungen als Callouts statt einfachem Text erscheinen, ändern Sie die Eigenschaft `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### So fügen Sie ein Drill‑Down‑Diagramm hinzu

Drill‑Down ermöglicht es einem Benutzer, einen Datenpunkt anzuklicken und zu einer zugehörigen Detailansicht zu springen – häufig über einen Hyperlink umgesetzt. Unten hängen wir der ersten Punkt in der Serie eine URL an.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Häufiger Fehler:** Denken Sie daran, das Hyperlink‑Ziel auf eine Seite zu setzen, die die Detaildaten rendern kann (z. B. ein Web‑Report oder ein weiteres Excel‑Blatt). Andernfalls führt der Klick zu einem toten Link.

## Schritt 5: Speichern der Arbeitsmappe

Nachdem das Diagramm konfiguriert wurde, speichern Sie die Arbeitsmappe. Die resultierende Datei enthält das interaktive Diagramm, das in Excel oder einem kompatiblen Viewer geöffnet werden kann.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Fazit

In diesem Leitfaden haben Sie **wie man interactive chart Java** Lösungen mit Aspose.Cells erstellt, und zwar folgendes:

- Laden von Daten aus einer vorhandenen Arbeitsmappe  
- Programmatisches Erstellen eines Säulendiagramms  
- Hinzufügen von Tooltips und Callout‑Datenbeschriftungen  
- Implementierung von Drill‑Down‑Funktionalität über Hyperlinks  
- Speichern der finalen Arbeitsmappe  

Diese Techniken verwandeln statische Tabellenkalkulationen in dynamische, benutzerfreundliche Dashboards, die das Datenverständnis und die Entscheidungsfindung verbessern.

## Häufig gestellte Fragen

**F: Wie kann ich den Diagrammtyp ändernA: Ändern Sie das `ChartType`‑Enum in der `add`‑Methode (z. B. `ChartType.LINE` für ein Liniendiagramm).

**F: Kann ich das Aussehen von Tooltips anpassen?**  
A: Ja, Sie können Schriftgröße, Farbe, Hintergrund und weitere Stil‑Eigenschaften über das `DataLabels`‑Objekt anpassen.

**F: Wie gehe ich mit Diagramm‑Interaktivität in einer Web‑Anwendung um?**  
A: Exportieren Sie die Arbeitsmappe nach XLSX und verwenden Sie dann eine JavaScript‑Chart‑Bibliothek (z. B. Highcharts), um die Daten clientseitig darzustellen, oder betten Sie die Excel‑Datei in einen Office Web Viewer ein, der Hyperlinks berücksichtigt.

**F: Wo finde ich weitere Beispiele?**  
A: Besuchen Sie die offizielle [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) für eine vollständige Liste der diagrammbezogenen Klassen und Methoden.

**F: Benötige ich eine Lizenz für den Produktionseinsatz?**  
A: Ja, für den Einsatz ist eine kommerzielle Lizenz erforderlich; eine kostenlose Evaluationslizenz steht zum Testen bereit.

**Last Updated:** 2025-12-04  
**Tested With:** Aspose.Cells for Java 24.12 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}