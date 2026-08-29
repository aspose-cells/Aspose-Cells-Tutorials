---
date: 2026-08-21
description: Erfahren Sie, wie Sie Tooltips, Datenbeschriftungen hinzufügen und den
  Diagrammtyp in Excel-Diagrammen mit Aspose.Cells für Java ändern – Schritt‑für‑Schritt‑Anleitung
  mit interaktiven Beispielen.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Excel-Diagrammtyp ändern
og_description: Erfahren Sie, wie Sie Tooltips, Datenbeschriftungen hinzufügen und
  den Diagrammtyp in Excel-Diagrammen mit Aspose.Cells für Java ändern – Schritt‑für‑Schritt‑Anleitung
  mit interaktiven Beispielen.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: So fügen Sie Tooltips und Datenbeschriftungen zu Excel-Diagrammen in Java
  hinzu
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: So fügen Sie Tooltips und Datenbeschriftungen zu Excel-Diagrammen in Java hinzu
url: /de/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Datenbeschriftungen zu Excel-Diagramm hinzufügen und Diagrammtyp ändern – Aspose.Cells Java

Interaktive Diagramme verleihen Ihren Excel‑Berichten ein neues Maß an Erkenntnis, und **wie man Tooltips hinzufügt** macht die Informationen sofort lesbar. In diesem Tutorial lernen Sie, wie Sie **Datenbeschriftungen zu Excel‑Diagramm hinzufügen**, **den Diagrammtyp ändern** und interaktive Java‑Lösungen mit Aspose.Cells erstellen. Wir zeigen Ihnen außerdem, wie Sie Tooltips und einen einfachen Drill‑Down‑Hyperlink hinzufügen, damit Ihr Publikum die Daten tiefgehend erkunden kann.

## Schnelle Antworten
- **Welche Bibliothek wird verwendet?** Aspose.Cells für Java  
- **Kann ich den Diagrammtyp ändern?** Ja – ändern Sie einfach das `ChartType`‑Enum, wenn Sie das Diagramm erstellen.  
- **Wie füge ich Tooltips zu einem Diagramm hinzu?** Verwenden Sie die Daten‑Label‑API (`setHasDataLabels(true)`) und aktivieren Sie die Anzeige des Werts.  
- **Wird Drill‑Down unterstützt?** Sie können Hyperlinks zu Datenpunkten hinzufügen, um ein einfaches Drill‑Down‑Verhalten zu erzielen.  
- **Voraussetzungen?** Java‑IDE, Aspose.Cells‑JAR und eine Excel‑Datei mit Beispieldaten.

## Was bedeutet „how to add tooltips“?
**How to add tooltips** bezieht sich auf den Vorgang, Hover‑Text zu aktivieren, der den Wert eines Datenpunkts oder benutzerdefinierte Informationen in einem Excel‑Diagramm anzeigt. In Aspose.Cells wird dies über die Daten‑Label‑Einstellungen des Diagramms erreicht. Tooltips helfen Benutzern, Daten schnell zu verstehen, ohne das Diagramm zu überladen, und sie können für Schriftart, Farbe und Format angepasst werden.

## Warum interaktive Diagramme mit Aspose.Cells verwenden?
Aspose.Cells unterstützt **50+ Eingabe‑ und Ausgabeformate** – darunter XLSX, CSV, PDF und HTML – und kann Arbeitsmappen mit **über 1 000 Blättern** verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Das ermöglicht schnelle serverseitige Diagrammerstellung für Unternehmensberichte. Interaktive Diagramme erlauben zudem das Einbetten von Hyperlinks, dynamische Datenaktualisierungen und den Export in web‑freundliche Formate, was sie ideal für Dashboards und Reporting‑Portale macht.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Java‑Entwicklungsumgebung (JDK 8+ empfohlen)  
- Aspose.Cells für Java‑Bibliothek (Download von der [Aspose.Cells for Java download page](https://releases.aspose.com/cells/java/))  
- Eine Beispielarbeitsmappe (`data.xlsx`) mit den Daten, die Sie visualisieren möchten  

## Schritt 1: Einrichtung Ihres Java‑Projekts

1. Erstellen Sie ein neues Java‑Projekt in Ihrer bevorzugten IDE (IntelliJ IDEA, Eclipse usw.).  
2. Fügen Sie das Aspose.Cells‑JAR zu Ihrem Build‑Path oder zu den Maven/Gradle‑Abhängigkeiten hinzu.

## Schritt 2: Laden von Daten

Um mit Diagrammen zu arbeiten, benötigen Sie zunächst eine Arbeitsmappe, die im Speicher geladen ist.

Die Klasse `Workbook` repräsentiert eine Excel‑Datei, und `Worksheet` steht für ein einzelnes Blatt innerhalb dieser Datei.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Wie man den Diagrammtyp in Aspose.Cells ändert

Erstellen Sie ein neues Diagramm mit dem gewünschten `ChartType`‑Enum; Aspose.Cells ändert den Typ eines bestehenden Diagramms nicht in‑Place, daher müssen Sie ein frisches Diagramm des korrekten Typs hinzufügen und optional das alte entfernen. Dieser Ansatz stellt sicher, dass alle Serien und Achsen korrekt für die neue visuelle Darstellung neu aufgebaut werden.

## Schritt 3: Erstellen eines Diagramms (und Ändern seines Typs)

Sie können jeden Diagrammtyp wählen, der zu Ihrer Analyse passt. Im Folgenden erstellen wir ein **Säulendiagramm**, Sie können jedoch leicht zu einem Linien‑, Kreis‑ oder Balkendiagramm wechseln, indem Sie das `ChartType`‑Enum ändern.

Das `Chart`‑Objekt bietet Methoden zur Konfiguration der visuellen Darstellung von Daten im Arbeitsblatt.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro‑Tipp:** Um **den Excel‑Diagrammtyp zu ändern**, ersetzen Sie `ChartType.COLUMN` durch `ChartType.LINE`, `ChartType.PIE` usw.

## Wie man Tooltips zu einem Excel‑Diagramm hinzufügt

Laden Sie Ihr Diagramm, aktivieren Sie Datenbeschriftungen und setzen Sie das Flag `showValue`. Der Tooltip zeigt dann den zugrunde liegenden Zellenwert an, sobald ein Benutzer über einen Datenpunkt in der gerenderten Excel‑Datei oder HTML‑Ansicht hovert. Sie können zudem Schriftart, Farbe und Hintergrund des Tooltips an den Stil Ihres Berichts anpassen.

Die Klasse `DataLabel` steuert das Aussehen und den Inhalt von Datenbeschriftungen, die zugleich als Tooltips fungieren.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Schritt 4: Interaktivität hinzufügen

### 4.1. Tooltips hinzufügen (add tooltips to chart)

Tooltips erscheinen, wenn der Benutzer über einen Datenpunkt hovert. Der folgende Code aktiviert Datenbeschriftungen und zeigt den Wert als Tooltip an.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Datenbeschriftungen hinzufügen – **add data labels to excel chart**

Datenbeschriftungen bieten einen permanenten visuellen Hinweis direkt im Diagramm. Sie können sie als Callouts anzeigen, um die Lesbarkeit zu verbessern.

Die Klasse `DataLabel` steuert das Aussehen der Beschriftungen jeder Serie. Durch Aufruf von `setHasDataLabels(true)` und Konfiguration von Eigenschaften wie `setShowValue(true)` betten Sie den numerischen Wert direkt in das Diagramm ein, sodass er sofort sichtbar ist, ohne dass eine Interaktion erforderlich ist. Weitere Optionen ermöglichen das Anzeigen von Seriennamen, Prozentsätzen oder benutzerdefiniertem Text für einen reichhaltigeren Kontext.

> **Warum Datenbeschriftungen hinzufügen?** Das direkte Einbinden von Datenbeschriftungen in das Diagramm eliminiert die Notwendigkeit, zu hovern oder Werte zu schätzen, und verbessert die Klarheit des Berichts.

### 4.3. Drill‑Down implementieren (Hyperlink auf einen Datenpunkt)

Eine einfache Möglichkeit, Drill‑Down‑Funktionalität hinzuzufügen, besteht darin, einem bestimmten Punkt einen Hyperlink zuzuweisen. Ein Klick auf den Punkt öffnet eine Webseite mit detaillierten Informationen.

Die Klasse `Hyperlink` fügt einem Diagrammelement einen anklickbaren Link hinzu und ermöglicht so die Drill‑Down‑Navigation.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Wie man Datenbeschriftungen zu einem Excel‑Diagramm hinzufügt

Die Klasse `DataLabel` steuert das Aussehen der Beschriftungen jeder Serie. Durch Aufruf von `setHasDataLabels(true)` und Konfiguration von Eigenschaften wie `setShowValue(true)` betten Sie den numerischen Wert direkt in das Diagramm ein, sodass er sofort sichtbar ist, ohne dass eine Interaktion erforderlich ist. Weitere Optionen ermöglichen das Anzeigen von Seriennamen, Prozentsätzen oder benutzerdefiniertem Text für einen reichhaltigeren Kontext.

## Schritt 5: Arbeitsmappe speichern

Nachdem Sie das Diagramm konfiguriert haben, speichern Sie die Arbeitsmappe, damit die interaktiven Funktionen im Ausgabedokument erhalten bleiben.

Der Aufruf von `workbook.save` schreibt die modifizierte Arbeitsmappe in eine Datei im gewählten Format.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Häufige Probleme & Lösungen

| Problem | Lösung |
|---------|--------|
| **Tooltips werden nicht angezeigt** | Stellen Sie sicher, dass `setHasDataLabels(true)` vor der Konfiguration von `setShowValue(true)` aufgerufen wird. |
| **Hyperlink ist nicht anklickbar** | Prüfen Sie, ob das Ausgabeformat Hyperlinks unterstützt (z. B. XLSX, nicht CSV). |
| **Diagrammtyp ändert sich nicht** | Vergewissern Sie sich, dass Sie das richtige `ChartType`‑Enum beim Hinzufügen des Diagramms geändert haben. |

## Häufig gestellte Fragen

**F: Wie kann ich den Diagrammtyp ändern, nachdem er erstellt wurde?**  
A: Sie müssen ein neues Diagramm mit dem gewünschten `ChartType` erstellen. Aspose.Cells bietet keine In‑Place‑Typumwandlung, also entfernen Sie das alte Diagramm und fügen Sie ein neues hinzu.

**F: Kann ich das Aussehen von Tooltips anpassen?**  
A: Ja. Verwenden Sie die `DataLabel`‑Eigenschaften wie `setFontSize`, `setFontColor` und `setBackgroundColor`, um den Tooltip‑Text zu stylen.

**F: Wie gehe ich mit Benutzerinteraktionen in einer Web‑Anwendung um?**  
A: Exportieren Sie die Arbeitsmappe in eine HTML‑ oder XLSX‑Datei und nutzen Sie JavaScript auf der Client‑Seite, um Klick‑Ereignisse auf Diagrammelemente zu erfassen.

**F: Wo finde ich weitere Beispiele und Dokumentation?**  
A: Besuchen Sie die [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) für eine vollständige Liste der diagrammbezogenen Klassen und Methoden.

## Fazit

Sie wissen jetzt, wie Sie **Datenbeschriftungen zu Excel‑Diagramm hinzufügen**, **den Excel‑Diagrammtyp ändern**, **interaktive Java‑Diagrammlösungen erstellen** und diese mit Tooltips, Datenbeschriftungen und Drill‑Down‑Hyperlinks mithilfe von Aspose.Cells für Java anreichern. Diese Erweiterungen machen Ihre Excel‑Berichte für Endbenutzer deutlich ansprechender und aussagekräftiger.

---

**Zuletzt aktualisiert:** 2026-08-21  
**Getestet mit:** Aspose.Cells für Java 24.12  
**Autor:** Aspose

## Verwandte Tutorials

- [Wie man Excel‑Diagramme und Datenbeschriftungen mit Aspose.Cells für Java ändert](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Excel‑Diagramm‑Achsenbeschriftungen mit Aspose.Cells Java extrahieren: Ein umfassender Leitfaden](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Blasendiagramme in Excel mit Aspose.Cells für Java erstellen: Schritt‑für‑Schritt‑Anleitung](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}