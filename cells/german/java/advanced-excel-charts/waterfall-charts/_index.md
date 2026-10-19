---
date: 2026-09-02
description: Erfahren Sie, wie Sie in Java mit Aspose.Cells ein Excel-Wasserfalldiagramm
  erstellen, den Datenbereich des Diagramms festlegen, Beschriftungen anpassen und
  in XLSX exportieren.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Wasserfalldiagramme
og_description: Erstellen Sie ein Excel-Wasserfalldiagramm mit Aspose.Cells für Java
  – legen Sie den Diagrammdatenbereich fest, fügen Sie Datenbeschriftungen hinzu und
  exportieren Sie in wenigen Schritten in XLSX.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Excel-Wasserfalldiagramm mit Aspose.Cells für Java erstellen
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Excel-Wasserfalldiagramm mit Aspose.Cells für Java erstellen
url: /de/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wasserfalldiagramme

## Einführung in Wasserfalldiagramme mit Aspose.Cells für Java

In diesem Tutorial lernen Sie, wie Sie mit Aspose.Cells für Java **create excel waterfall chart** und **set chart data range** erstellen. Wasserfalldiagramme verwandeln eine Reihe von positiven und negativen Zahlen in eine klare visuelle Geschichte und sind damit ideal für Finanzberichte, Verkaufsleistungsbewertungen und jede Situation, in der Sie sehen müssen, wie einzelne Elemente zu einem Gesamtergebnis beitragen.

## Schnelle Antworten
- **Was ist ein Wasserfalldiagramm?** Eine Visualisierung, die zeigt, wie ein Anfangswert durch eine Reihe von Zwischenschritten erhöht und verringert wird und schließlich zu einem Endwert führt.  
- **Welche Bibliothek wird verwendet?** Aspose.Cells für Java.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Datei als XLSX speichern?** Ja – verwenden Sie `workbook.save("FileName.xlsx")`.  
- **Ist es für Java-Datenvisualisierung geeignet?** Absolut; Aspose.Cells bietet umfangreiche Diagrammfunktionen ohne installierte Office-Anwendungen.

## Was ist ein Wasserfalldiagramm?
Ein Wasserfalldiagramm zeigt sequenzielle positive und negative Beiträge zu einem Ausgangswert und hilft Ihnen zu verstehen, wie jede Komponente das Gesamtergebnis beeinflusst. Durch die nebeneinander Darstellung von Gewinnen und Verlusten wird ein komplexer Finanzfluss sofort lesbar.

## Warum Aspose.Cells für Java verwenden, um ein Wasserfalldiagramm hinzuzufügen?
Aspose.Cells ermöglicht das Erzeugen von Excel‑Diagrammen auf jedem Server, in CI‑Pipelines oder auf dem Desktop, ohne dass Microsoft Excel benötigt wird. Es unterstützt **15+ output formats** (XLSX, PDF, HTML, CSV und mehr), verarbeitet Arbeitsmappen mit **500+ rows** in weniger als einer Sekunde und bietet programmgesteuerte Kontrolle über jedes Diagrammelement – von Farben bis zu Datenbeschriftungen.

## Voraussetzungen

Bevor wir in den Code eintauchen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Aspose.Cells für Java: Sie müssen Aspose.Cells für Java installiert haben. Sie können es von der Aspose.Cells für Java Release‑Seite herunterladen: [Aspose.Cells für Java Releases](https://releases.aspose.com/cells/java/).
- Java‑Entwicklungsumgebung: Stellen Sie sicher, dass Java auf Ihrem System installiert ist und ein Build‑Tool (Maven/Gradle) bereitsteht.

Jetzt beginnen wir Schritt für Schritt mit der Erstellung des Wasserfalldiagramms.

## So setzen Sie den Diagrammdatenbereich für ein Wasserfalldiagramm in Java
Laden Sie eine neue Arbeitsmappe, füllen Sie sie mit Daten, fügen Sie ein `Chart`‑Objekt hinzu, definieren Sie den Serienbereich und speichern Sie schließlich die Datei. Dieser Prozess ist einfach: Sie erstellen eine Arbeitsmappe, füllen Zellen mit Kategorien und Werten, erstellen ein Diagramm, binden die Datenbereiche und exportieren dann die Arbeitsmappe. Das Ergebnis ist ein voll funktionsfähiges Wasserfalldiagramm, das in Berichten oder Dashboards verwendet werden kann.

### Schritt 1: import Aspose.Cells
Das Paket `com.aspose.cells` enthält alle Klassen, die für die Excel‑Manipulation erforderlich sind, einschließlich der Erstellung von Arbeitsmappen, der Verarbeitung von Arbeitsblättern und der Diagrammerstellung.

### Schritt 2: Arbeitsmappe und Arbeitsblatt initialisieren
Eine **Workbook** stellt eine Excel‑Datei dar, und ein **Worksheet** ist ein einzelnes Blatt innerhalb dieser Datei. Das Erzeugen dieser Objekte liefert die Grundlage sowohl für Rohdaten als auch für das Diagramm.

### Schritt 3: Daten eingeben
Spalte A enthält Kategorienamen, während Spalte B die numerischen Werte für das Wasserfalldiagramm enthält. Dieses Layout entspricht dem typischen Gewinn‑und‑Verlust‑Fluss, der in der Finanzanalyse verwendet wird.

### Schritt 4: Wasserfalldiagramm erstellen
Das **Chart**‑Objekt erzeugt eine visuelle Darstellung; das Setzen des Typs auf `ChartType.WATERFALL` konfiguriert es als Wasserfalldiagramm. Verwenden Sie die `add`‑Methode, um den Diagrammdatenbereich für die Serie (`"B2:B6"` ) festzulegen und die Kategorienachse mit `"A2:A6"` zu verknüpfen.

### Schritt 5: Arbeitsmappe speichern
Das Speichern der Arbeitsmappe schreibt das Diagramm und die Daten in das angegebene Dateiformat. Rufen Sie `workbook.save("WaterfallChart.xlsx")` auf, um eine XLSX‑Datei zu erzeugen, oder ändern Sie den Format‑Parameter, um nach PDF, CSV oder HTML zu exportieren.

## Häufige Probleme und Lösungen

- **Diagramm erscheint leer** – Prüfen Sie, ob die Datenbereichs‑Referenzen (`B2:B6` und `A2:A6`) mit den tatsächlichen Zellen übereinstimmen, die Ihre Werte und Kategorien enthalten.  
- **Negative Werte werden nicht korrekt angezeigt** – Stellen Sie sicher, dass der Serientyp auf `ChartType.WATERFALL` gesetzt ist; andere Diagrammtypen behandeln Negative anders.  
- **Datei öffnet sich nicht in Excel** – Verwenden Sie die neueste Aspose.Cells‑Version und stellen Sie sicher, dass die Dateierweiterung dem Format entspricht (`.xlsx` für Excel).

## Häufig gestellte Fragen

### Wie kann ich das Aussehen meines Wasserfalldiagramms anpassen?
Sie können Eigenschaften wie `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` ändern, um Balkenfarben zu ändern, Datenbeschriftungen mit `setShowDataLabels(true)` aktivieren und Achsentitel über `getCategoryAxis().setTitle("Stage")` anpassen. Die Aspose.Cells‑API‑Referenz bietet eine vollständige Liste anpassbarer Optionen.

### Kann ich mehrere Wasserfalldiagramme im selben Arbeitsblatt erstellen?
Ja. Nachdem Sie das erste Diagramm hinzugefügt haben, wiederholen Sie die Schritte zur Diagrammerstellung mit einem anderen Datenbereich und einem neuen `Chart`‑Objekt. Jedes Diagramm ist unabhängig und kann überall im Blatt positioniert werden.

### Ist Aspose.Cells mit verschiedenen Java‑Entwicklungsumgebungen kompatibel?
Absolut. Die Bibliothek funktioniert mit Eclipse, IntelliJ IDEA, NetBeans und jedem Build‑System, das Maven oder Gradle unterstützt. Es sind keine zusätzlichen Plugins erforderlich.

### Kann ich zusätzliche Datenreihen zu meinem Wasserfalldiagramm hinzufügen?
Sie können weitere Reihen hinzufügen, indem Sie `chart.getNSeries().add("C2:C6", true)` aufrufen und jede Reihe separat konfigurieren. So lassen sich mehrere Szenarien nebeneinander vergleichen.

### Wo finde ich weitere Ressourcen und Beispiele für Aspose.Cells für Java?
Entdecken Sie die vollständige Dokumentation in der Aspose.Cells Java API‑Referenz: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: Wie setze ich den Diagrammdatenbereich für ein finanzielles Wasserfalldiagramm?**  
A: Verwenden Sie die `add`‑Methode der Diagramm‑Serie und übergeben Sie den Zellbereich, der Ihre Werte enthält, z. B. `"B2:B6"`.

**Q: Kann ich die Arbeitsmappe statt XLSX als PDF exportieren?**  
A: Ja, rufen Sie `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` auf, um eine PDF‑Version zu erzeugen.

**Q: Was tun, wenn ich ein Wasserfalldiagramm mit mehr Kategorien erstellen muss?**  
A: Erweitern Sie den Datenbereich sowohl in der Wertespalte als auch in der Kategoriespalte und passen Sie anschließend die Aufrufe von `add` und `setCategoryData` entsprechend an.

**Q: Gibt es eine Möglichkeit, positive und negative Balken automatisch zu formatieren?**  
A: Durchlaufen Sie die `Series`‑Sammlung und setzen Sie die `FillFormat`‑Farbe basierend auf dem Vorzeichen jedes Wertes; Aspose.Cells ermöglicht die programmgesteuerte Anwendung von bedingter Formatierung.

**Q: Unterstützt Aspose.Cells dynamische Datenaktualisierungen für Diagramme?**  
A: Ja. Nach dem Ändern von Zellwerten speichern Sie die Arbeitsmappe einfach erneut – das Diagramm spiegelt die neuen Daten automatisch wider.

---

**Last Updated:** 2026-09-02  
**Tested with:** Aspose.Cells für Java (latest)  
**Author:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Verwandte Tutorials

- [Excel-Diagramm-Datenbeschriftungen mit Aspose.Cells für Java anpassen: Eine Schritt-für-Schritt-Anleitung](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Datenbeschriftungen zu Excel-Diagramm mit Aspose.Cells Java hinzufügen](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Wie man Diagramme in Java mit Aspose.Cells erstellt und exportiert: Ein vollständiger Leitfaden](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}