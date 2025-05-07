---
"date": "2025-04-07"
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für Java Kreisdiagramme in Excel erstellen und anpassen. Folgen Sie dieser Schritt-für-Schritt-Anleitung, um Ihre Fähigkeiten zur Datenvisualisierung zu verbessern."
"title": "Erstellen Sie Kreisdiagramme in Excel mit Aspose.Cells für Java – Ein umfassender Leitfaden"
"url": "/de/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Erstellen Sie Kreisdiagramme in Excel mit Aspose.Cells für Java
## Einführung
Durch die Erstellung ansprechender und informativer Kreisdiagramme in Excel können Sie Rohdaten in aussagekräftige Erkenntnisse umwandeln und so schnell fundierte Geschäftsentscheidungen treffen. Sie haben Probleme mit den integrierten Funktionen von Microsoft Excel oder suchen eine skalierbare Lösung, die sich nahtlos in Ihre Java-Anwendungen integriert? Aspose.Cells für Java hilft Ihnen dabei.

Dieses Tutorial führt Sie durch die Erstellung und Anpassung von Kreisdiagrammen in Excel-Dateien mit Aspose.Cells für Java. Erfahren Sie, wie Sie effizient Daten hinzufügen, Diagrammelemente konfigurieren und Ihre Arbeitsmappe fertigstellen – alles einfach und präzise.

**Was Sie lernen werden:**
- Einrichten und Verwenden von Aspose.Cells für Java
- Erstellen einer neuen Arbeitsmappe und Auffüllen mit Beispieldaten
- Hinzufügen und Anpassen von Kreisdiagrammen in einem Excel-Arbeitsblatt
- Best Practices für die Diagrammkonfiguration und -optimierung

Beginnen wir mit der Klärung der Voraussetzungen.
## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
### Erforderliche Bibliotheken, Versionen und Abhängigkeiten
Stellen Sie sicher, dass Aspose.Cells für Java Version 25.3 oder höher mit Maven oder Gradle in Ihr Projekt eingebunden ist.
**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### Anforderungen für die Umgebungseinrichtung
- Ein auf Ihrem System installiertes Java Development Kit (JDK).
- Eine integrierte Entwicklungsumgebung (IDE) wie IntelliJ IDEA, Eclipse oder NetBeans.
### Voraussetzungen
Grundlegende Kenntnisse der Java-Programmierung und Vertrautheit mit Excel-Dateistrukturen sind von Vorteil.
## Einrichten von Aspose.Cells für Java
Aspose.Cells ist eine leistungsstarke Bibliothek, mit der Entwickler Excel-Tabellen in Java-Anwendungen erstellen, bearbeiten und rendern können. So richten Sie sie ein:
1. **Installation**: Fügen Sie die Maven- oder Gradle-Abhängigkeit wie oben gezeigt hinzu.
2. **Lizenzerwerb**:
   - Erhalten Sie eine kostenlose Testlizenz für erste Tests von [Kostenlose Aspose-Testversion](https://releases.aspose.com/cells/java/).
   - Beantragen Sie eine temporäre Lizenz, um alle Funktionen ohne Einschränkungen zu testen über [Temporäre Lizenz](https://purchase.aspose.com/temporary-license/).
3. **Grundlegende Initialisierung**: Beginnen Sie mit der Erstellung einer Instanz des `Workbook` Klasse, die Ihre Excel-Datei darstellt.
```java
import com.aspose.cells.Workbook;
// Erstellen und Initialisieren einer neuen Arbeitsmappe
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## Implementierungshandbuch
Lassen Sie uns nun jede Funktion Schritt für Schritt implementieren, um eine Excel-Arbeitsmappe mit einem Kreisdiagramm zu erstellen.
### 1. Erstellen und Initialisieren der Arbeitsmappe
**Überblick**: Wir beginnen mit der Initialisierung unseres `Workbook` Objekt und greifen auf sein erstes Arbeitsblatt zu, wo wir Daten und Diagramme hinzufügen.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// Erstellen einer neuen Arbeitsmappeninstanz
Workbook workbook = new Workbook();
// Greifen Sie auf das erste Arbeitsblatt in der Arbeitsmappe zu
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. Hinzufügen von Beispieldaten zu Zellen
**Überblick**: Füllen Sie Ihr Arbeitsblatt mit Beispieldaten, die im Kreisdiagramm dargestellt werden.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// Fügen Sie Ländernamen in Spalte A hinzu
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// Weiter für andere Länder...
// Ergänzen Sie die entsprechenden Verkaufsdaten in Spalte B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// Fahren Sie für die restlichen Daten fort ...
```
### 3. Hinzufügen eines Kreisdiagramms zum Arbeitsblatt
**Überblick**Fügen Sie mithilfe vordefinierter Datenbereiche ein Kreisdiagramm in das Arbeitsblatt ein.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// Fügen Sie ein Kreisdiagramm an der angegebenen Stelle und in der angegebenen Größe hinzu
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. Konfigurieren der Diagrammserie
**Überblick**: Definieren Sie den Datenbereich für Verkaufs- und Kategoriedaten (Ländernamen), um sicherzustellen, dass das Kreisdiagramm Ihren Datensatz genau darstellt.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// Legen Sie die Verkaufsdaten als Datenquelle des Diagramms fest
serieses.add("B1:B8", true);
// Kategoriedaten angeben (Ländernamen)
serieses.setCategoryData("A1:A8");
// Aktivieren Sie verschiedene Farben für jedes Tortenstück
serieses.setColorVaried(true);

// Zeigen Sie zur besseren Übersicht eine Datentabelle im Diagramm an
chart.setShowDataTable(true);
```
### 5. Festlegen von Diagrammtitel und -stil
**Überblick**: Passen Sie den Titel Ihres Diagramms an, um die Lesbarkeit und Präsentation zu verbessern.
```java
import com.aspose.cells.Color;

// Legen Sie den Diagrammtitel mit Stiloptionen fest
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. Konfigurieren von Datenbeschriftungen für Diagrammreihen
**Überblick**: Fügen Sie jedem Kreissegment Datenbeschriftungen hinzu, um eine klare Aufschlüsselung der Werte zu ermöglichen.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // Positionieren Sie die Beschriftungen innerhalb der Basis jedes Tortenstücks
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // Konfigurieren von Beschriftungsanzeigeoptionen
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. Speichern der Arbeitsmappe
**Überblick**Finalisieren Sie Ihre Excel-Datei mit allen auf der Festplatte gespeicherten Daten und Diagrammen.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// Speichern Sie die Arbeitsmappe in einer Excel-Datei
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## Praktische Anwendungen
- **Geschäftsanalysen**: Verwenden Sie Kreisdiagramme in Verkaufsberichten, um Marktanteile oder Umsatzverteilungen über Regionen hinweg zu visualisieren.
- **Lehrmittel**: Erstellen Sie interaktive Lernmodule, die statistische Datenverteilungen anzeigen.
- **Projektmanagement**: Stellen Sie den Stakeholdern die Ressourcenzuweisung und Budgetnutzung visuell dar.
## Überlegungen zur Leistung
So optimieren Sie die Leistung:
- Minimieren Sie die Speichernutzung durch effizientes Verwalten der Arbeitsmappengröße.
- Nutzen Sie die Funktionen von Aspose.Cells wie das Streamen großer Dateien, wenn Sie mit umfangreichen Datensätzen arbeiten.
- Befolgen Sie die Best Practices von Java zur Speicherverwaltung und stellen Sie sicher, dass Ressourcen nach der Verwendung ordnungsgemäß freigegeben werden.
## Abschluss
In dieser Anleitung haben Sie gelernt, Kreisdiagramme in Excel mit Aspose.Cells für Java zu erstellen, zu konfigurieren und anzupassen. Diese leistungsstarke Bibliothek ermöglicht Entwicklern die nahtlose Integration erweiterter Tabellenkalkulationsfunktionen in ihre Java-Anwendungen.
Um die Möglichkeiten noch weiter zu erkunden, können Sie sich auch mit anderen Diagrammtypen befassen oder Ihre Möglichkeiten zur Datenbearbeitung mit den zusätzlichen Funktionen von Aspose.Cells erweitern.
## FAQ-Bereich
1. **Kann ich Aspose.Cells kostenlos nutzen?**
   - Ja, eine kostenlose Testversion ist verfügbar. Für den uneingeschränkten Zugriff auf alle Funktionen können Sie eine temporäre Lizenz beantragen.
2. **Ist es möglich, mit Aspose.Cells andere Diagrammtypen zu erstellen?**
   - Absolut! Sie können Balkendiagramme, Liniendiagramme und mehr erstellen, indem Sie die `ChartType`.
3. **Wie verarbeite ich große Datensätze in Excel mit Java?**
   - Verwenden Sie effiziente Datenladetechniken und ziehen Sie Streaming für sehr große Dateien in Betracht.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}