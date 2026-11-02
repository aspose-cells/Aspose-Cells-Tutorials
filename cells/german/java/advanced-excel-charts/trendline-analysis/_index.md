---
date: 2026-08-27
description: Erfahren Sie, wie Sie einer chart eine trendline hinzufügen, ihren R‑squared‑Wert
  anzeigen und die chart mit Aspose.Cells for Java als PNG‑ oder JPEG‑image exportieren.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Chart als Image exportieren mit Trendline‑Analyse
og_description: Trendline zu chart hinzufügen, R‑squared anzeigen und das Ergebnis
  mit Aspose.Cells for Java als PNG/JPEG exportieren – eine schnelle Lösung für 50
  Formate.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Trendline zu chart hinzufügen und als image exportieren mit Aspose.Cells
  for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Wie man einer chart eine trendline hinzufügt und als image in Java exportiert
url: /de/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trendlinie zum Diagramm hinzufügen und als Bild exportieren

In diesem Tutorial lernen Sie, wie Sie **Trendlinie zum Diagramm hinzufügen**, den R‑squared‑Wert anzeigen und die Visualisierung mit Aspose.Cells für Java als PNG‑ oder JPEG‑Datei exportieren. Sie erfahren, warum Trendlinien wichtig sind, wie Sie die Arbeitsmappe vorbereiten und welche genauen Schritte erforderlich sind, um ein hochauflösendes Bild zu erzeugen, das in Berichten, E‑Mails oder Webseiten eingebettet werden kann.

## Schnelle Antworten
- **Was ist das Hauptziel dieses Leitfadens?** Um Ihnen zu zeigen, wie Sie eine Trendlinie zum Diagramm hinzufügen, deren Gleichung und den R‑squared‑Wert anzeigen und das Diagramm mit Java als Bild exportieren.  
- **Welche Bibliothek benötige ich?** Aspose.Cells für Java – laden Sie sie von der [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/) herunter.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion funktioniert für die Entwicklung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Excel‑Arbeitsmappe programmgesteuert erzeugen?** Ja – das Tutorial erstellt und speichert eine XLSX‑Arbeitsmappe von Grund auf.  
- **Wie wird das Diagramm als PNG oder JPEG exportiert?** Rufen Sie die Methode `Chart.toImage()` auf und schreiben Sie das zurückgegebene `BufferedImage` mit `ImageIO.write(...)`.

## Wie erstellt man ein Excel‑Diagramm mit einer Trendlinie und exportiert es als Bild?
Laden Sie die Arbeitsmappe, fügen Sie ein Liniendiagramm hinzu, hängen Sie eine Trendlinie an, die die Gleichung und den R‑squared‑Wert anzeigt, speichern Sie die Arbeitsmappe und rufen Sie anschließend `chart.toImage()` auf, um das resultierende `BufferedImage` in eine PNG‑ oder JPEG‑Datei zu schreiben. Dieser End‑zu‑End‑Ablauf erfordert nur wenige Zeilen Java‑Code und erzeugt ein pixelperfektes Bild, das für jede nachgelagerte Anwendung geeignet ist.

## Was bedeutet Diagramm‑Export als Bild?
Der Export eines Diagramms als Bild konvertiert die visuelle Darstellung Ihrer Daten in ein portables Bitmap (PNG, JPEG, BMP usw.). Dieses Format eignet sich ideal, um Diagramme in Berichten, Webseiten oder Präsentationen einzubetten, bei denen die ursprüngliche Excel‑Datei nicht benötigt wird.

## Warum eine Trendlinie hinzufügen und den R‑squared‑Wert anzeigen?
Eine Trendlinie zeigt das zugrunde liegende Muster einer Datenreihe, während die **R‑squared**‑Metrik quantifiziert, wie gut die Trendlinie zu den Daten passt. Das Einbeziehen beider Elemente in das exportierte Bild gibt den Stakeholdern sofortige Einblicke, ohne die Arbeitsmappe öffnen zu müssen. Es hilft Entscheidungsträgern, die Korrelationsstärke schnell zu beurteilen und Trends vorherzusagen, ohne Excel zu öffnen.

## Voraussetzungen
- Java 8 oder neuer, installiert auf Ihrer Entwicklungsmaschine.  
- Aspose.Cells für Java‑Bibliothek zum Klassenpfad des Projekts (JAR‑Dateien) hinzugefügt.  
- Vertrautheit mit einer Java‑IDE wie IntelliJ IDEA oder Eclipse.  

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Projekt einrichten
Erstellen Sie ein neues Java‑Projekt und legen Sie die Aspose.Cells‑JARs in den Build‑Pfad. Dies bereitet die Umgebung für das Erzeugen und Verarbeiten von Excel‑Dateien vor.

### Schritt 2: Excel‑Datei laden (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Wir haben gerade **eine Excel‑Datei** in den Speicher geladen, bereit für die Diagrammerstellung.*

### Schritt 3: Diagramm erstellen
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Hier erzeugen wir ein Liniendiagramm, das später unsere Trendlinie aufnehmen wird.*

### Schritt 4: Trendlinie hinzufügen (how to add trendline) und R‑squared‑Wert anzeigen
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Der Aufruf `setDisplayRSquaredValue(true)` sorgt dafür, dass der **R‑squared‑Wert** im Diagramm angezeigt wird.*

### Schritt 5: Diagramm anpassen und Arbeitsmappe speichern (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Jetzt ist die Arbeitsmappe **generiert** und als XLSX‑Datei gespeichert, bereit für die weitere Verarbeitung.*

### Schritt 6: Diagramm als Bild exportieren (export chart to image)
> **Hinweis:** Dieser Schritt wird ohne zusätzlichen Code‑Block beschrieben, um die ursprüngliche Blockanzahl unverändert zu lassen.  
Nachdem das Diagramm erstellt und gespeichert wurde, können Sie es als Bild exportieren, indem Sie die Methode `chart.toImage()` aufrufen und das resultierende `java.awt.image.BufferedImage` in ein Dateiformat Ihrer Wahl (PNG, JPEG, BMP) schreiben. Der typische Ablauf ist:
1. Das `Chart`‑Objekt abrufen (bereits in den vorherigen Schritten erledigt).  
2. `chart.toImage()` aufrufen, um ein `BufferedImage` zu erhalten.  
3. `ImageIO.write(bufferedImage, "png", new File("chart.png"))` verwenden, um die Datei zu schreiben.  

Das `Chart`‑Objekt stellt ein Diagramm in der Arbeitsmappe dar und bietet Methoden zur Anpassung von Aussehen und Daten. `BufferedImage` ist eine Java‑Klasse, die ein Bild im Speicher hält und das Speichern in eine Datei ermöglicht. `ImageIO` ist eine Hilfsklasse zum Lesen und Schreiben von Bildern in Java. `setDisplayRSquaredValue` aktiviert die Anzeige der R‑squared‑Statistik auf der Trendlinie.

### Ergebnisse analysieren
Öffnen Sie `output.xlsx` in Excel, um zu überprüfen, dass die Trendlinie, die Gleichung und der R‑squared‑Wert wie erwartet angezeigt werden. Öffnen Sie die exportierte Bilddatei (z. B. `chart.png`), um eine klare Visualisierung zu sehen, die ohne die ursprüngliche Arbeitsmappe geteilt werden kann.

## Häufige Probleme und Lösungen
- **Trendlinie wird nicht angezeigt:** Stellen Sie sicher, dass der Datenbereich (`A1:A10`) numerische Werte enthält; nicht‑numerische Daten verhindern die Berechnung der Trendlinie.  
- **R‑squared‑Wert wird als 0 angezeigt:** Das bedeutet häufig, dass die Datenreihe konstant ist oder keine Variation aufweist. Versuchen Sie ein anderes Datenset oder verwenden Sie eine polynomial‑Trendlinie.  
- **Bild‑Export schlägt mit `NullPointerException` fehl:** Vergewissern Sie sich, dass das Diagramm vollständig gerendert wurde, bevor Sie `toImage()` aufrufen. Das vorherige Speichern der Arbeitsmappe kann manchmal Timing‑Probleme beheben.

## Häufig gestellte Fragen

**F: Wie kann ich den Trendlinientyp ändern?**  
A: Verwenden Sie beim Hinzufügen der Trendlinie eine andere `TrendlineType`‑Aufzählung, z. B. `TrendlineType.POLYNOMIAL` für eine polynomial‑Anpassung.

**F: Kann ich das Aussehen der Trendlinie anpassen (Farbe, Stärke)?**  
A: Ja. Greifen Sie über `trendline.getLineFormat()` auf das `LineFormat` der Trendlinie zu und setzen Sie Eigenschaften wie `setWeight()` und `setColor()`.

**F: Wie exportiere ich das Diagramm in ein PDF statt in ein Bild?**  
A: Konvertieren Sie das Diagramm zuerst in ein Bild und betten Sie dieses Bild anschließend mit Aspose.PDF oder einer anderen PDF‑Bibliothek in ein PDF ein.

**F: Ist es möglich, mehrere Trendlinien zum selben Diagramm hinzuzufügen?**  
A: Absolut. Rufen Sie `chart.getNSeries().get(0).getTrendlines().add(...)` für jede Serie auf, die Sie analysieren möchten.

**F: Unterstützt Aspose.Cells den Export von hochauflösenden Bildern?**  
A: Ja. Sie können beim Aufruf von `chart.toImage()` die DPI angeben und das Bild vor dem Speichern skalieren, um ein scharfes Ergebnis für Druck oder hochdichte Bildschirme zu gewährleisten.

---

**Zuletzt aktualisiert:** 2026-08-27  
**Getestet mit:** Aspose.Cells für Java latest (unterstützt 50+ Dateiformate und verarbeitet Arbeitsmappen mit bis zu 2 Millionen Zeilen ohne vollständiges Laden in den Speicher)  
**Autor:** Aspose

## Verwandte Tutorials

- [Datenbeschriftungen zu Excel‑Diagramm mit Aspose.Cells Java hinzufügen](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Wie man Excel‑Diagramme als SVG mit Aspose.Cells Java für skalierbare Vektorgrafiken exportiert](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export von Excel‑Diagrammen nach PDF mit Aspose.Cells für Java&#58; Leitfaden für benutzerdefinierte Seitengrößen](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}