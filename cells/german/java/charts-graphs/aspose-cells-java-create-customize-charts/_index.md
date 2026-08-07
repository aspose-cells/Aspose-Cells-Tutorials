---
date: '2026-04-08'
description: Erfahren Sie, wie Sie ein Säulendiagramm in Java mit Aspose.Cells erstellen,
  einschließlich Diagramm in Java erzeugen, Diagrammblatt hinzufügen und Arbeitsmappe
  nach Excel exportieren.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Spaltendiagramm mit Aspose.Cells Java‑Tutorial erstellen
url: /de/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Spalten‑Diagramm mit Aspose.Cells Java generieren

In heutigen datengetriebenen Anwendungen kann das **Generieren eines Spalten‑Diagramms** schnell und programmgesteuert rohe Zahlen in klare visuelle Erkenntnisse verwandeln. Egal, ob Sie ein Reporting‑Dashboard, ein Analyse‑Tool oder eine einfache Export‑Funktion erstellen, Aspose.Cells für Java bietet Ihnen eine flüssige API, um **chart java**‑Projekte zu **create chart java** ohne die Excel‑Benutzeroberfläche zu verwenden. In diesem Tutorial lernen Sie, wie Sie die Bibliothek einrichten, **Excel‑Zellen befüllen**, ein **Diagrammblatt** hinzufügen, den **Diagrammtitel** anpassen und schließlich **workbook excel** in eine Datei **exportieren**.

## Schnellantworten
- **Was bedeutet „generate column chart“?** Es erstellt eine vertikale Balken‑Visualisierung aus tabellarischen Daten.  
- **Welche Bibliothek wird benötigt?** Aspose.Cells für Java (Kostenlose Testversion verfügbar).  
- **Benötige ich eine Excel‑Installation?** Nein, die Bibliothek funktioniert unabhängig von Microsoft Excel.  
- **Kann ich in andere Formate als XLS exportieren?** Ja – PDF, PNG, SVG usw. über `workbook.save()`.  
- **Ist eine Lizenz für die Produktion zwingend erforderlich?** Ja, eine erworbene oder temporäre Lizenz ist nötig.

## Was ist ein Spalten‑Diagramm?
Ein Spalten‑Diagramm stellt Datenreihen als vertikale Balken dar und erleichtert den Vergleich von Werten über Kategorien wie Regionen, Monate oder Produktlinien hinweg. Aspose.Cells ermöglicht es Ihnen, dieses Diagramm vollständig im Code zu erstellen und dabei volle Kontrolle über Daten, Styling und Ausgabeformat zu haben.

## Warum Aspose.Cells zum Erstellen von chart java verwenden?
- **Kein COM‑Interop** – funktioniert auf jedem OS mit einer JVM.  
- **Umfangreiche Styling‑Optionen** – Bilder, Verläufe, Legenden und benutzerdefinierte Schriften.  
- **Hohe Leistung** – geeignet für große Datensätze.  
- **Mehrere Exportformate** – XLS, XLSX, PDF, PNG und mehr.

## Voraussetzungen
- **Java Development Kit (JDK) 8+** installiert.  
- Grundkenntnisse in Java und Vertrautheit mit Excel‑Konzepten.  

### Erforderliche Bibliotheken
Fügen Sie Aspose.Cells Ihrem Projekt mit einem der nachstehenden Snippets hinzu.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Lizenzbeschaffung
Aspose bietet eine kostenlose Testversion und eine temporäre Lizenz für umfangreiche Tests.

- **Kostenlose Testversion**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Temporäre Lizenz**: [Request Here](https://purchase.aspose.com/temporary-license/)

## Einrichtung von Aspose.Cells für Java

Zuerst erstellen Sie eine `Workbook`‑Instanz – diese dient als Canvas für unsere Daten und das Diagramm.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Schritt‑für‑Schritt‑Anleitung

### 1. Arbeitsblatt erstellen und benennen
Wir speichern die Rohdaten in einem Blatt namens **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Excel‑Zellen füllen
Fügen Sie Regionsnamen und Verkaufszahlen ein, die das Spalten‑Diagramm visualisieren soll.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Diagrammblatt hinzufügen
Das Trennen des Diagramms von den Rohdaten hält die Arbeitsmappe übersichtlich.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Spalten‑Diagramm erstellen
Jetzt erzeugen wir tatsächlich **generate column chart**‑Objekte.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Bild als Hintergrundfüllung im Plot‑Bereich festlegen
Ein Hintergrundbild kann das Diagramm hervorheben.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Diagrammtitel festlegen
Die **set chart title**‑Anpassung verbessert die Lesbarkeit.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Serien‑Daten und Legende konfigurieren
Verknüpfen Sie den Datenbereich mit dem Diagramm und positionieren Sie die Legende.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Arbeitsmappe exportieren
Abschließend **export workbook excel** in eine XLS‑Datei (oder ein beliebiges unterstütztes Format).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Praktische Anwendungen
- **Business‑Reports** – Automatisches Erzeugen von Verkaufs‑Diagrammen für monatliche PDFs.  
- **Datenanalyse‑Tools** – Einbetten dynamischer Diagramme in benutzerdefinierte Analyse‑Dashboards.  
- **Enterprise‑Dashboards** – Diagrammbilder on‑the‑fly für Echtzeit‑Monitoring aktualisieren.

## Leistungsüberlegungen
- Batch‑Updates von Zellen bei großen Datensätzen durchführen, um Overhead zu reduzieren.  
- Ressourcen freigeben (`workbook.dispose()`), wenn Sie viele Arbeitsmappen in einer Schleife verarbeiten.  

## Häufige Probleme und Lösungen
- **Bild wird nicht angezeigt** – Pfad prüfen und sicherstellen, dass das Bildformat (PNG, JPEG) unterstützt wird.  
- **Diagramm erscheint leer** – Sicherstellen, dass die Datenbereichs‑Referenzen (`Data!B2:B8`) den befüllten Zellen entsprechen.  
- **Out‑of‑memory‑Fehler** – Daten in Teilen verarbeiten und nach großen Saves `System.gc()` aufrufen.

## Häufig gestellte Fragen

**Q: Wie füge ich mehrere Serien zu einem Spalten‑Diagramm hinzu?**  
A: Rufen Sie `chart.getNSeries().add()` wiederholt mit unterschiedlichen Datenbereichen auf, z. B. `"Data!C2:C8"` für eine zweite Serie.

**Q: Kann ich die Achsenbeschriftungen ändern?**  
A: Ja. Verwenden Sie `chart.getCategoryAxis().setTitle("Regions")` und `chart.getValueAxis().setTitle("Sales")`.

**Q: Welche Formate kann ich neben XLS exportieren?**  
A: Verwenden Sie `workbook.save("chart.pdf")`, `workbook.save("chart.png")` oder `workbook.save("chart.xlsx")` für PDF, PNG bzw. XLSX.

**Q: Wird für Entwicklungs‑Builds eine Lizenz benötigt?**  
A: Eine kostenlose Testversion reicht für die Evaluation, aber für Produktions‑Deployments ist eine permanente oder temporäre Lizenz erforderlich.

**Q: Wie kann ich die Render‑Geschwindigkeit bei tausenden Zeilen verbessern?**  
A: Zellen mit `cells.importArray()` befüllen und Diagramm‑Neuzeichnungen minimieren, indem Sie das Diagramm erst nach dem Laden aller Daten erstellen.

---

**Zuletzt aktualisiert:** 2026-04-08  
**Getestet mit:** Aspose.Cells 25.3 für Java  
**Autor:** Aspose  

## Ressourcen

- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Purchase a License](https://purchase.aspose.com/buy)
- [Free Trial](https://releases.aspose.com/cells/java/)
- [Temporary License Request](https://purchase.aspose.com/temporary-license/)
- [Support Forum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}