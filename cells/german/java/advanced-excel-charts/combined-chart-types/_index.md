---
date: 2026-09-02
description: Erfahren Sie, wie Sie ein Diagramm als PNG exportieren, Datenreihen hinzufügen,
  ein Linien‑ und Säulendiagramm kombinieren, die Arbeitsmappe als XLSX speichern
  und ein Legenden‑Diagramm mit Aspose.Cells for Java hinzufügen.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Diagramm als PNG exportieren und Datenreihe für kombiniertes Diagramm hinzufügen
og_description: Diagramm mit Aspose.Cells for Java als PNG exportieren, ein Linien‑
  und Säulendiagramm kombinieren, Datenreihen hinzufügen und die Arbeitsmappe als
  XLSX in einem einzigen Tutorial speichern.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Diagramm als PNG exportieren und Datenreihe für kombiniertes Diagramm hinzufügen
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Diagramm als PNG exportieren und Datenreihe für kombiniertes Diagramm hinzufügen
url: /de/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm als PNG exportieren und Datenreihen für kombiniertes Diagramm hinzufügen

In diesem Tutorial werden Sie **Datenreihen** zu einer Excel-Arbeitsmappe **hinzufügen**, **Linien‑ und Säulendiagramm**‑Elemente **kombinieren** und lernen, wie man **Diagramm als PNG exportiert** mit Aspose.Cells für Java. Wir gehen jeden Schritt durch – vom Einrichten der Arbeitsmappe, dem Hinzufügen des Diagramms zu einem Arbeitsblatt, dem Anpassen der Legende, bis zum **Speichern der Arbeitsmappe als XLSX** und dem Erzeugen eines PNG‑Bildes des Diagramms. Am Ende haben Sie ein einsatzbereites kombiniertes Diagramm, das Sie in Berichte oder Dashboards einbetten können.

## Schnelle Antworten
- **Which library creates combined charts?** Welche Bibliothek erstellt kombinierte Diagramme? Aspose.Cells for Java.  
- **How do I add a data series?** Wie füge ich eine Datenreihe hinzu? Call `chart.getNSeries().add(...)` with the appropriate range.  
- **How can I export chart to PNG?** Wie kann ich das Diagramm als PNG exportieren? Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **What file format can I save the workbook as?** In welchem Dateiformat kann ich die Arbeitsmappe speichern? Standard `.xlsx` (save workbook as XLSX).  
- **Do I need a license for production?** Benötige ich eine Lizenz für die Produktion? Yes – a valid Aspose.Cells license is required for production deployments.

## Was ist das Exportieren von Diagrammen als PNG in Aspose.Cells?
Das Exportieren eines Diagramms als PNG erzeugt ein Rasterbild des Excel‑Diagramms, das in Webseiten, Berichten oder E‑Mails angezeigt werden kann, ohne dass die Excel‑Anwendung erforderlich ist. Diese Methode erfasst das genaue visuelle Layout, die Farben und Datenmarker und erzeugt eine portable Bilddatei.

## Warum ein kombiniertes Linien‑Säulendiagramm erstellen?
Ein kombiniertes Linien‑Säulendiagramm ermöglicht es, verschiedene Datensätze mit unterschiedlichen visuellen Darstellungen (z. B. eine Linienreihe über einer Säulreihe) in einer einzigen Ansicht darzustellen. Dieser Ansatz ist ideal, um Trends mit Gesamtsummen zu vergleichen, Korrelationen hervorzuheben oder tiefere Einblicke zu liefern, während der visuelle Umfang klein bleibt.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder höher
- Aspose.Cells für Java Bibliothek (Download über den untenstehenden Link)
- Grundlegende Kenntnisse der Java‑Syntax und Excel‑Konzepte  

## Erste Schritte

Laden Sie zunächst die Aspose.Cells für Java Bibliothek von der offiziellen Seite herunter:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Sobald das JAR zu Ihrem Projekt‑Klassenpfad hinzugefügt wurde, können Sie mit dem Erstellen des Diagramms beginnen.

### Schritt 1: aspose.cells‑Klassen importieren
`Workbook` ist das Kernobjekt von Aspose.Cells, das eine gesamte Excel‑Datei im Speicher repräsentiert.  
```java
import com.aspose.cells.*;
```

### Schritt 2: neue Arbeitsmappe erstellen
`Worksheet` stellt ein einzelnes Blatt innerhalb einer `Workbook` dar und bietet Zugriff auf Zellen, Zeilen und Diagramme.  
```java
Workbook workbook = new Workbook();
```

### Schritt 3: erstes Arbeitsblatt zugreifen
`Chart` ist das Objekt, das alle diagrammbezogenen Einstellungen, Reihen und Rendering‑Optionen enthält.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Schritt 4: kombiniertes Diagramm‑Objekt zum Arbeitsblatt hinzufügen  
Wir beginnen mit einem Liniendiagramm und fügen später eine Säulreihe hinzu, um einen **kombinierten Linien‑Säulendiagramm**‑Effekt zu erzielen.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Daten zum Diagramm hinzufügen

Da der Diagramm‑Container nun existiert, müssen wir ihn mit Daten versorgen.

### Schritt 5: Datenbereiche definieren und Datenreihe hinzufügen
`NSeries` ist die Sammlung, die jede Datenreihe für ein Diagramm speichert. Das Hinzufügen einer Reihe verknüpft einen Zellbereich mit dem Diagramm.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro Tipp:** Der erste Parameter (`"A1:A5"`) ist der Bereich für die erste Reihe, und der zweite (`"B1:B5"`) erstellt eine zweite Reihe, die mit der ersten kombiniert wird.

### Schritt 6: Kategoriedaten (X‑Achse) festlegen
`CategoryAxis` stellt die horizontale Achse des Diagramms dar und steuert die entlang der X‑Achse angezeigten Beschriftungen.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Diagramm anpassen

Ein gutes Diagramm erzählt eine Geschichte. Geben wir ihm Titel, Achsenbeschriftungen und eine klare Legende.

### Schritt 7: Diagrammachsen‑Beschriftungen und Titel festlegen
`Title` legt den Haupttitel des Diagramms fest, und `Axis`‑Objekte repräsentieren die X‑ und Y‑Achsen.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Schritt 8: Legende zum Diagramm hinzufügen und Position anpassen
`Legend` steuert die Platzierung und das Aussehen der Serienlegende im Diagramm.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Diagramm speichern und exportieren

Nach dem Anpassen möchten Sie **die Arbeitsmappe als XLSX speichern** und zudem ein Bild erzeugen.

### Schritt 9: Arbeitsmappe als Excel‑Datei (XLSX) speichern
`Workbook.save` schreibt die im Speicher befindliche Arbeitsmappe in eine Datei im angegebenen Format.  
```java
workbook.save("CombinedChart.xlsx");
```

### Schritt 10: Diagramm als PNG exportieren
`Chart.toImage` rendert das Diagramm als Bilddatei im gewählten Format.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Die Methode `chart.toImage` **erzeugt Excel‑Diagrammbilder**, die in Webseiten, Berichten oder E‑Mails verwendet werden können.

## Häufige Probleme & Fehlersuche

| Problem | Lösung |
|-------|----------|
| **Keine Daten angezeigt** | Stellen Sie sicher, dass die Zellbereiche (`A1:A5`, `B1:B5`, `C1:C5`) tatsächlich Daten enthalten, bevor Sie das Diagramm erstellen. |
| **Legende überlappt Diagramm** | Setzen Sie `chart.getLegend().setOverlay(false)` oder verschieben Sie die Legende an eine andere Position (z. B. `RIGHT`). |
| **Bilddatei ist leer** | Stellen Sie sicher, dass das Diagramm mindestens eine Reihe hat und dass `chart.toImage` nach allen Anpassungen aufgerufen wird. |
| **Speichern wirft eine Ausnahme** | Prüfen Sie, ob Sie Schreibrechte für das Zielverzeichnis haben und dass die Datei nicht in Excel geöffnet ist. |

## Häufig gestellte Fragen

**Q: Wie installiere ich Aspose.Cells für Java?**  
A: Laden Sie das JAR von der offiziellen Seite herunter und fügen Sie es dem Klassenpfad Ihres Projekts hinzu. Der Download‑Link ist: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kann ich andere Diagrammtypen außer Linie und Säule erstellen?**  
A: Ja, Aspose.Cells unterstützt Balken-, Kreis-, Streu‑, Flächen‑ und viele weitere Diagrammtypen. Siehe die API‑Dokumentation für die vollständige Liste.

**Q: Wird für den Produktionseinsatz eine Lizenz benötigt?**  
A: Eine gültige Aspose.Cells‑Lizenz ist für Produktionseinsätze erforderlich. Eine kostenlose Testversion ist zur Evaluierung verfügbar.

**Q: Wie kann ich die Farben jeder Reihe ändern?**  
A: Verwenden Sie `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (oder Ähnliches) nach dem Hinzufügen der Reihe.

**Q: Wo finde ich weitere Code‑Beispiele?**  
A: Umfassende Dokumentation und weitere Beispiele finden Sie auf der Aspose‑Referenzseite: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Zuletzt aktualisiert:** 2026-09-02  
**Getestet mit:** Aspose.Cells für Java neueste Version  
**Autor:** Aspose

## Verwandte Tutorials

- [Wie man Beschriftungen zu Excel‑Diagrammen mit Aspose.Cells für Java hinzufügt](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Wie man ein Excel‑Diagramm mit Trendlinie erstellt und als Bild exportiert mit Aspose.Cells für Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Excel‑Diagramme als PDF exportieren mit Aspose.Cells für Java: Leitfaden für benutzerdefinierte Seitengrößen](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}