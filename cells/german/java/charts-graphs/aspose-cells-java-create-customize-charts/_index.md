---
"date": "2025-04-08"
"description": "Ein Code-Tutorial für Aspose.Words Java"
"title": "Aspose.Cells Java&#58; Diagramme erstellen und anpassen"
"url": "/de/java/charts-graphs/aspose-cells-java-create-customize-charts/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Diagrammerstellung und -anpassung mit Aspose.Cells Java meistern

In der heutigen datengetriebenen Welt ist die Visualisierung komplexer Datensätze entscheidend für fundierte Entscheidungen. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen: Die Erstellung überzeugender Diagramme in Ihren Anwendungen kann die Benutzerfreundlichkeit deutlich verbessern. Dieses Tutorial führt Sie durch die Verwendung von Aspose.Cells für Java, um mühelos Diagramme zu erstellen und anzupassen.

## Was Sie lernen werden

- So richten Sie Aspose.Cells für Java ein
- Erstellen und Benennen von Arbeitsblättern
- Zellen mit Daten füllen
- Hinzufügen eines Diagrammblatts und Erstellen eines Säulendiagramms
- Anpassen Ihres Diagramms mit Bildern, Titeln und Serienkonfigurationen
- Speichern der Arbeitsmappe

Mit diesen Schritten können Sie im Handumdrehen optisch ansprechende Diagramme erstellen.

## Voraussetzungen

Bevor Sie sich in Aspose.Cells für Java vertiefen, stellen Sie sicher, dass Sie über Folgendes verfügen:

- **Java Development Kit (JDK) 8 oder höher** auf Ihrem Computer installiert.
- Grundlegende Kenntnisse der Java-Programmierung und Vertrautheit mit Excel-Operationen.
  
### Erforderliche Bibliotheken

Um mit Aspose.Cells zu beginnen, fügen Sie die folgende Abhängigkeit in Ihr Projektmanagement-Tool ein.

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

### Lizenzerwerb

Aspose bietet eine kostenlose Testversion an, mit der Sie alle Funktionen der Bibliothek vor dem Kauf testen können. Sie können auch eine temporäre Lizenz für umfangreiche Tests erwerben.

- **Kostenlose Testversion**: [Kostenloser Download](https://releases.aspose.com/cells/java/)
- **Temporäre Lizenz**: [Hier anfordern](https://purchase.aspose.com/temporary-license/)

## Einrichten von Aspose.Cells für Java

Sobald Ihre Umgebung bereit ist, initialisieren Sie die Bibliothek, indem Sie eine neue `Workbook` Instanz. Dies dient als Grundlage für unsere Diagrammerstellung.

```java
import com.aspose.cells.Workbook;

// Initialisieren einer neuen Arbeitsmappe
Workbook workbook = new Workbook();
```

## Implementierungshandbuch

### 1. Erstellen und Benennen eines Arbeitsblatts

#### Überblick
Beginnen Sie mit der Einrichtung Ihres Datenblatts, das alle erforderlichen Daten für das Diagramm enthält.

#### Schritte:

**Erstellen einer neuen Arbeitsmappe**
```java
import com.aspose.cells.Worksheet;

// Erstellen einer neuen Arbeitsmappeninstanz
Workbook workbook = new Workbook();
```

**Benennen Sie das Arbeitsblatt**

```java
// Greifen Sie auf das erste Arbeitsblatt zu und legen Sie seinen Namen auf „Daten“ fest.
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Zellen mit Daten füllen

#### Überblick
Das Einfügen von Daten in Ihr Arbeitsblatt ist für die Erstellung aussagekräftiger Diagramme von entscheidender Bedeutung.

#### Schritte:

**Access Cells-Sammlung**

```java
import com.aspose.cells.Cells;

// Holen Sie sich die Zellensammlung aus dem Datenblatt
Cells cells = sheet.getCells();
```

**Daten einfügen**

```java
// Fügen Sie Regionsnamen und Verkaufszahlen ein
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Hinzufügen eines Diagrammblatts

#### Überblick
Fügen Sie ein spezielles Diagrammblatt hinzu, um Ihre Daten und Visualisierung getrennt zu halten.

#### Schritte:

**Diagrammblatt erstellen**

```java
import com.aspose.cells.SheetType;

// Hinzufügen eines neuen Diagrammblatts
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Nennen Sie das Arbeitsblatt „Diagramm“
chartSheet.setName("Chart");
```

### 4. Erstellen eines Diagramms

#### Überblick
Erstellen Sie ein Säulendiagramm, um Verkaufsdaten nach Region zu visualisieren.

#### Schritte:

**Säulendiagramm erstellen**

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Fügen Sie dem Blatt „Diagramm“ ein neues Säulendiagramm hinzu
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Bild als Hintergrund festlegen Diagramm-Plotbereich ausfüllen

#### Überblick
Verbessern Sie die visuelle Attraktivität Ihres Diagramms, indem Sie ein Hintergrundbild hinzufügen.

#### Schritte:

**Bilddaten festlegen**

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

### 6. Konfigurieren von Diagrammtitel und -serie

#### Überblick
Passen Sie Ihr Diagramm mit einem Titel, Seriendaten und Legendenpositionierung an.

#### Schritte:

**Diagrammtitel festlegen**

```java
// Konfigurieren der Titeleigenschaften des Diagramms
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

**Seriendaten konfigurieren**

```java
// Festlegen von Serien- und Kategoriedaten für das Diagramm
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Positionieren Sie die Legende oben im Diagramm
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 7. Speichern der Arbeitsmappe

#### Überblick
Stellen Sie sicher, dass Ihre gesamte harte Arbeit gespeichert wird, indem Sie die Arbeitsmappe exportieren.

#### Schritte:

**Arbeitsmappe speichern**

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Praktische Anwendungen

- **Geschäftsberichte**: Erstellen Sie dynamische Verkaufs- und Leistungsberichte.
- **Datenanalyse-Tools**: Verbessern Sie die Datenvisualisierung in Analysesoftware.
- **Dashboard-Integrationen**: Integrieren Sie Diagramme in Dashboards für Echtzeit-Updates.

## Überlegungen zur Leistung

- Optimieren Sie, indem Sie die Anzahl der Vorgänge bei großen Datensätzen minimieren.
- Verwalten Sie den Speicher effektiv, indem Sie nicht verwendete Objekte umgehend entsorgen.

## Abschluss

Sie beherrschen nun das Erstellen und Anpassen von Diagrammen mit Aspose.Cells in Java. Entdecken Sie weitere Funktionen wie dynamische Datenbereiche und verschiedene Diagrammtypen. 

## FAQ-Bereich

1. **Wie füge ich einem Diagramm mehrere Reihen hinzu?**
   - Verwenden Sie die `add` Methode auf `NSeries` mit mehreren Bereichen.

2. **Kann ich die Achsenbeschriftungen des Diagramms anpassen?**
   - Ja, Zugriff und Konfiguration der Achsen über `chart.getCategoderyAxis()` or `chart.getValueAxis()`.

3. **Was ist, wenn meine Bilddatei im Plotbereich nicht richtig angezeigt wird?**
   - Stellen Sie sicher, dass der Dateipfad korrekt ist und das Bildformat von Aspose.Cells unterstützt wird.

4. **Wie gehe ich effizient mit großen Datensätzen um?**
   - Erwägen Sie, Daten in Blöcken zu lesen und Zellen inkrementell zu aktualisieren.

5. **Ist es möglich, Diagramme in andere Formate wie PDF oder PNG zu exportieren?**
   - Ja, verwenden `workbook.save()` mit der entsprechenden Dateierweiterung für verschiedene Formate.

## Ressourcen

- [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/java/)
- [Laden Sie Aspose.Cells herunter](https://releases.aspose.com/cells/java/)
- [Erwerben Sie eine Lizenz](https://purchase.aspose.com/buy)
- [Kostenlose Testversion](https://releases.aspose.com/cells/java/)
- [Antrag auf eine temporäre Lizenz](https://purchase.aspose.com/temporary-license/)
- [Support-Forum](https://forum.aspose.com/c/cells/9)

Mit dieser Anleitung können Sie mit Aspose.Cells problemlos Diagramme in Java-Anwendungen erstellen und anpassen. Viel Spaß beim Programmieren!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}