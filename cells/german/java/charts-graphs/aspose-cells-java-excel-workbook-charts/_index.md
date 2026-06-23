---
date: '2026-04-11'
description: Lernen Sie Excel-Automatisierung mit Java und Aspose.Cells. Dieses Tutorial
  zeigt, wie man ein Excel-Arbeitsbuch mit Java erstellt, Excel-Daten mit Java befüllt
  und eine Excel-Datei mit Java und Diagrammen speichert.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Excel-Automatisierung Java: Arbeitsmappen und Diagramme mit Aspose erstellen'
url: /de/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Automatisierung mit Java: Arbeitsmappen & Diagramme mit Aspose

## Einführung

Die Automatisierung von Excel‑Aufgaben mit Java kann Stunden manueller Arbeit einsparen, insbesondere wenn Sie Berichte, Dashboards oder datenbasierte Diagramme on‑the‑fly erstellen müssen. **Excel automation java** mit Aspose.Cells bietet Ihnen eine saubere, hochleistungsfähige API, die alles von der Erstellung von Arbeitsmappen bis hin zu anspruchsvollen Diagrammformatierungen übernimmt. In diesem Tutorial lernen Sie, wie Sie Aspose.Cells einrichten, **create an Excel workbook java**, es mit Daten füllen, ein Diagramm hinzufügen, 3‑D‑Formatierung anwenden und schließlich **save the Excel file java**.

### Schnelle Antworten
- **Welche Bibliothek vereinfacht die Excel‑Automatisierung in Java?** Aspose.Cells for Java.  
- **Kann ich programmatisch 3‑D‑Diagramme hinzufügen?** Ja – die API unterstützt 3‑D‑Formatierung und Lichteffekte.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testlizenz ist verfügbar; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Welche Java‑Build‑Tools werden unterstützt?** Maven und Gradle werden beide vollständig unterstützt.  
- **Welche Dateiformate kann ich exportieren?** XLS, XLSX, CSV, PDF und viele weitere.

## Was ist Excel automation java?

Excel automation java bezeichnet den Prozess der programmgesteuerten Erstellung, Modifizierung und Speicherung von Excel‑Arbeitsmappen mittels Java‑Code. Es eliminiert manuelle Tabellenkalkulationsbearbeitung, sorgt für Konsistenz und ermöglicht die Integration mit anderen Systemen wie Datenbanken oder Webdiensten.

## Warum Aspose.Cells für Java verwenden?

- **Umfangreiches Funktionsset** – von einfachen Zellwerten bis hin zu komplexen Diagrammen, Pivot‑Tabellen und bedingter Formatierung.  
- **Keine Microsoft‑Office‑Abhängigkeit** – funktioniert in jeder serverseitigen Umgebung.  
- **Hohe Leistung** – optimiert für große Datenmengen und mehrthreadige Szenarien.  
- **Breite Formatunterstützung** – Lesen/Schreiben von XLS, XLSX, ODS, CSV, PDF, HTML und mehr.

## Voraussetzungen

- **Java Development Kit (JDK) 8+**  
- **Maven oder Gradle** für die Abhängigkeitsverwaltung  
- **Aspose.Cells for Java 25.3 oder höher** (Testversion oder lizenziert)  

## Einrichtung von Aspose.Cells für Java

Fügen Sie die Bibliothek zu Ihrem Projekt hinzu, indem Sie eine der folgenden Konfigurationen verwenden.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Lizenzbeschaffung

Fordern Sie eine kostenlose Testlizenz von der Aspose‑Website an oder erwerben Sie eine Voll‑Lizenz für den Produktionseinsatz. Platzieren Sie die Lizenzdatei in Ihrem Projekt und laden Sie sie zur Laufzeit.

## Grundlegende Initialisierung und Einrichtung

Sobald die Abhängigkeit aufgelöst ist, können Sie mit dem Codieren beginnen.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Wie man eine Excel‑Arbeitsmappe in Java erstellt

Erstellen Sie eine neue Arbeitsmappen‑Instanz, die alle Ihre Arbeitsblätter enthält.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Schritt 2: Arbeitsblätter hinzufügen (einschließlich eines Diagrammblatts)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Schritt 3: Wie man Excel‑Daten in Java befüllt

Fügen Sie Beispieldaten ein, auf die das Diagramm zugreifen wird.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Schritt 4: Ein Säulendiagramm zur Arbeitsmappe hinzufügen

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Schritt 5: Farbformatierung auf den Diagrammbereich anwenden

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Schritt 6: Legende und Datenreihen konfigurieren

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Schritt 7: 3D‑Formatierung auf die Reihen anwenden

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Schritt 8: Reihenfarben für bessere visuelle Unterscheidung festlegen

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Schritt 9: Wie man eine Excel‑Datei in Java speichert

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Praktische Anwendungen

- **Finanzberichterstattung** – Quartalsberichte mit dynamischen Diagrammen erstellen.  
- **Data‑Analysis‑Dashboards** – Interaktive Dashboards erstellen, die sich automatisch aktualisieren.  
- **Inventarverwaltung** – Lagerbestände und Trends nach Excel exportieren zur Überprüfung durch Stakeholder.  
- **Projektplanung** – Gantt‑ähnliche Diagramme direkt aus Java‑basierten Planungssystemen erstellen.

## Leistungstipps für Excel Automation Java

- **Workbook‑Objekte wiederverwenden** beim Verarbeiten mehrerer Blätter, um Speicherverbrauch zu reduzieren.  
- **Zell‑Updates stapeln** mit `Cells.importArray` für große Datensätze anstelle einzelner `putValue`‑Aufrufe.  
- **Ressourcen freigeben** durch Aufruf von `book.dispose()` nach dem Speichern großer Dateien.

## Häufig gestellte Fragen

**Q: Kann ich XLSX anstelle von XLS erzeugen?**  
A: Ja – ändern Sie einfach die Dateierweiterung in `book.save("output.xlsx")`; Aspose wählt automatisch das richtige Format.

**Q: Ist für die Entwicklung eine Lizenz erforderlich?**  
A: Eine kostenlose Testlizenz funktioniert für Entwicklung und Test. Für Produktionsbereitstellungen ist eine gekaufte Lizenz erforderlich.

**Q: Wie füge ich weitere Diagrammtypen hinzu?**  
A: Verwenden Sie das `ChartType`‑Enum (z. B. `ChartType.PIE`, `ChartType.LINE`) beim Aufruf von `charts.add(...)`.

**Q: Was, wenn ich die Arbeitsmappe schützen muss?**  
A: Rufen Sie `book.getSettings().setPassword("yourPassword")` vor dem Speichern auf.

**Q: Unterstützt Aspose.Cells makrofähige Dateien?**  
A: Ja – Sie können VBA‑Makros in XLSM‑Arbeitsmappen erstellen oder erhalten.

---

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}