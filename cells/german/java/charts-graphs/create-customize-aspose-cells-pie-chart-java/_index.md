---
date: '2026-09-27'
description: Erfahren Sie, wie Sie ein Kreisdiagramm in Java mit Aspose.Cells erstellen.
  Schritt‑für‑Schritt‑Anleitung zum Anpassen von Excel‑Kreisdiagrammen, Einrichten
  der Maven‑Abhängigkeit und Erzeugen professioneller Diagramme.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Erstellen Sie ein Kreisdiagramm in Java mit Aspose.Cells für Java.
  Erfahren Sie, wie Sie Excel‑Kreisdiagramme anpassen, die Maven‑Abhängigkeit hinzufügen
  und in wenigen Minuten professionelle Diagramme erzeugen.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Kreisdiagramm in Java mit Aspose.Cells erstellen – Vollständiger Java‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Wie man ein Kreisdiagramm in Java mit Aspose.Cells erstellt
url: /de/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Tortendiagramm in Java mit Aspose.Cells erstellt

## Einleitung
Das programmatische Erstellen eines **pie chart** fühlt sich oft wie ein Rätsel an, besonders wenn Sie eine feinkörnige Kontrolle über Farben, Legenden und Titel benötigen. In diesem Leitfaden lernen Sie, wie Sie **create pie chart java** mit Aspose.Cells erstellen und anschließend das Excel‑Tortendiagramm an Ihre Marken‑ oder Berichtsstil anpassen. Wir gehen die Einrichtung der Umgebung, das Befüllen von Daten, die Diagrammerstellung und visuelle Anpassungen durch – alles ohne Ihre Java‑IDE zu verlassen.

**Was Sie lernen werden**
- Fügen Sie die **Maven dependency Aspose.Cells** zu Ihrem Projekt hinzu.
- Erstellen Sie ein Workbook, füllen Sie Zellen mit Daten und erzeugen Sie ein pie chart.
- Wenden Sie benutzerdefinierte Farben, Titel und Legenden auf das Diagramm an.
- Exportieren Sie das Workbook in eine XLSX‑Datei, die zum Teilen bereit ist.

Bevor Sie beginnen, sollten Sie mit grundlegender Java‑Syntax vertraut sein und Maven oder Gradle installiert haben.

## Schnelle Antworten
- **Welche Bibliothek erstellt pie charts in Java?** Aspose.Cells for Java.
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; eine kostenpflichtige Lizenz ist für die Produktion erforderlich.
- **Welche Maven-Koordinaten werden benötigt?** `com.aspose:aspose-cells:24.10`.
- **Kann ich die Segmentfarben ändern?** Ja, über die `setAreaColor`‑Methode jeder Serie.
- **Ist das Diagramm nach XLSX exportierbar?** Absolut — rufen Sie einfach `workbook.save("output.xlsx")` auf.

## Was ist ein pie chart in Excel?
Ein **pie chart** visualisiert eine einzelne Datenreihe als proportionale Segmente eines Kreises, wodurch es einfach wird, Teile eines Ganzen zu vergleichen. Der Winkel jedes Segments entspricht seinem Wert relativ zur Gesamtsumme und ermöglicht schnelle Einblicke in die Verteilung über Kategorien wie Marktanteil, Budgetzuweisung oder demografische Prozentsätze.

## Warum Aspose.Cells zum Erstellen eines pie chart java verwenden?
Aspose.Cells unterstützt mehr als 50 Diagrammtypen und kann Arbeitsblätter mit bis zu einer Million Zeilen verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Dieser Performance‑Vorteil ermöglicht es Ihnen, große Berichte auf bescheidener Hardware zu erzeugen, während Sie feinkörnige Kontrolle über das Aussehen des Diagramms, die Datenbindung und Exportformate haben, was es zu einer überlegenen Wahl gegenüber vielen Open‑Source‑Bibliotheken macht.

## Voraussetzungen
- **Java Development Kit (JDK)** 8 oder neuer.
- **IDE** wie IntelliJ IDEA oder Eclipse.
- **Maven** oder **Gradle** für das Dependency‑Management.
- Eine **Trial‑ oder gekaufte Aspose.Cells‑Lizenz**.

### Erforderliche Bibliotheken und Abhängigkeiten
Fügen Sie das Aspose.Cells Maven‑Artefakt zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Oder das Gradle‑Äquivalent:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Schritte zum Erwerb einer Lizenz
Aspose.Cells für Java ist kommerziell, aber Sie können mit einer kostenlosen Testversion beginnen. Besuchen Sie die [purchase page](https://purchase.aspose.com/buy), um einen temporären Lizenzschlüssel zu erhalten.

## Einrichtung von Aspose.Cells für Java
Stellen Sie zunächst sicher, dass die Bibliothek in Ihrem Klassenpfad liegt. Nachdem Sie die Abhängigkeit hinzugefügt haben, können Sie die API wie unten gezeigt initialisieren.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Implementierungs‑Leitfaden

### Workbook erstellen und konfigurieren
Die Klasse `Workbook` repräsentiert eine komplette Excel‑Datei im Speicher.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Schritt 1: Ein Workbook instanziieren
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Dies erstellt ein neues, leeres Workbook, das Sie sofort mit Daten füllen können.

### Zugriff auf oder Ändern von Arbeitsblattzellen
Ein `Worksheet` stellt ein einzelnes Blatt innerhalb des Workbooks dar und enthält Zellen, Zeilen und Spalten.  
Sie schreiben die Daten, die das pie chart antreiben, in ein Arbeitsblatt.

#### Schritt 2: Das erste Arbeitsblatt und seine Zellen abrufen
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Füllen Sie die Zellen mit Kategorienamen und Werten, die das Diagramm verwendet.

### Ein pie chart erstellen
`Chart`‑Objekte visualisieren Daten in einem Arbeitsblatt und unterstützen verschiedene Typen wie pie, column und line.

#### Schritt 3: Ein pie chart zum Arbeitsblatt hinzufügen
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### pie chart‑Serie und Daten konfigurieren
`Series` definiert den Datenbereich und die Formatierung für ein Diagramm und verknüpft Arbeitsblattzellen mit visuellen Elementen.

#### Schritt 4: Die Serie für das Diagramm festlegen
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Diagramm‑Legende und Titelgestaltung konfigurieren
Eine Diagramm‑`Legend` zeigt die Namen der Serien und Farben an und hilft den Lesern, jedes Segment zu identifizieren.

#### Schritt 5: Diagramm‑Legende und Titel anpassen
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Diagramm‑Serienfarben anpassen
`setAreaColor` legt die Füllfarbe eines Diagramm‑Seriensegments mit einem RGB‑Wert fest.

#### Schritt 6: Pie‑Segmentfarben ändern
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Spalten automatisch anpassen und Workbook speichern
`autoFitColumns` passt die Spaltenbreiten automatisch an den Zelleninhalt an.

#### Schritt 7: Spaltenbreiten anpassen und Datei speichern
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Häufige Anwendungsfälle
- **Demographic analysis:** Zeigt die Bevölkerungsverteilung über Regionen hinweg.
- **Market‑share reporting:** Visualisiert den Anteil jedes Konkurrenten auf einen Blick.
- **Budget allocation:** Hebt hervor, wie Mittel auf Abteilungen verteilt werden.

## Leistungs‑Überlegungen
- Geben Sie Objekte (`workbook.dispose()`) frei, wenn sie nicht mehr benötigt werden, um nativen Speicher freizugeben.
- Verwenden Sie für massive Datensätze `WorkbookDesigner`, um Daten zu streamen, anstatt alles auf einmal zu laden.
- Profilieren Sie mit Java Flight Recorder, um Engpässe bei der Diagrammerstellung zu erkennen.

## Häufig gestellte Fragen

**Q: Kann ich mehrere pie charts im selben Workbook erzeugen?**  
A: Ja, wiederholen Sie die Schritte zur Diagrammerstellung für jeden Datenbereich; jedes Diagramm ist unabhängig.

**Q: Unterstützt Aspose.Cells 3‑D pie charts?**  
A: Ja; setzen Sie beim Hinzufügen des Diagramms den Diagrammtyp auf `ChartType.PIE_3D`.

**Q: Wie wende ich ein benutzerdefiniertes Theme auf alle Diagramme an?**  
A: Verwenden Sie die Methode `Workbook.setDefaultTheme`, bevor Sie Diagramme erstellen.

**Q: In welche Dateiformate kann ich das Workbook exportieren?**  
A: Mehr als 30 Formate, darunter XLSX, CSV, PDF und HTML.

**Q: Wird für den kommerziellen Einsatz eine Lizenz benötigt?**  
A: Ja, eine gültige Lizenz entfernt Evaluations‑Wasserzeichen und schaltet die volle Funktionalität frei.

## Fazit
Sie haben nun ein vollständiges, durchgängiges Rezept für **create pie chart java** mit Aspose.Cells. Wenn Sie die obigen Schritte befolgen, können Sie hochwertige Excel‑pie charts erzeugen, Farben und Titel anpassen und sie in jede Reporting‑Pipeline einbetten. Erkunden Sie weitere Diagrammtypen – column, line, radar – um Ihr Datenvisualisierungs‑Toolkit zu erweitern.

---

**Zuletzt aktualisiert:** 2026-09-27  
**Getestet mit:** Aspose.Cells 24.10 for Java  
**Autor:** Aspose

## Verwandte Tutorials

- [Excel-Diagramm-Datenbeschriftungen mit Aspose.Cells für Java&#58; Eine Schritt‑für‑Schritt‑Anleitung](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Dynamische Excel-Diagramme mit Aspose.Cells Java erstellen&#58; Ein umfassender Leitfaden für Entwickler](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Excel-Workbooks mit Aspose.Cells Java erstellen und anpassen&#58; Eine Schritt‑für‑Schritt‑Anleitung](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}