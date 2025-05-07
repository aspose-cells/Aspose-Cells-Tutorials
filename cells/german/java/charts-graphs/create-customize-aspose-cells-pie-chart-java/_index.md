---
"date": "2025-04-08"
"description": "Erfahren Sie, wie Sie Kreisdiagramme mit Aspose.Cells für Java erstellen und anpassen. Eine Schritt-für-Schritt-Anleitung mit Codebeispielen für Entwickler."
"title": "Aspose.Cells meistern&#58; Kreisdiagramme in Java erstellen und anpassen"
"url": "/de/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells meistern: Kreisdiagramme in Java erstellen und anpassen

## Einführung
Die Erstellung optisch ansprechender Diagramme ist eine häufige Anforderung bei der Datenvisualisierung in Excel. Ob Sie demografische Informationen präsentieren oder Markttrends analysieren – Kreisdiagramme bieten eine übersichtliche Möglichkeit, proportionale Daten darzustellen. Die programmgesteuerte Erstellung dieser Diagramme kann jedoch komplex sein. Dieses Tutorial führt Sie durch die Erstellung und Anpassung eines Aspose.Cells-Kreisdiagramms mit Java und vereinfacht den Prozess für Entwickler.

**Was Sie lernen werden:**
- Richten Sie Ihre Umgebung mit Aspose.Cells für Java ein.
- Erstellen Sie eine neue Arbeitsmappe und greifen Sie auf die Arbeitsblattzellen zu.
- Füllen Sie zur Vorbereitung der Diagrammerstellung bestimmte Zellen mit Daten auf.
- Erstellen Sie aus diesen Daten ein Kreisdiagramm.
- Passen Sie das Erscheinungsbild Ihres Kreisdiagramms an, einschließlich Farben, Titeln und Legenden.

Bevor Sie loslegen, sollten Sie über Grundkenntnisse in Java-Programmierung und Maven- oder Gradle-Abhängigkeitsmanagement verfügen. Lassen Sie uns unsere Umgebung einrichten!

## Voraussetzungen
Um diesem Tutorial folgen zu können, benötigen Sie:
- **Java Development Kit (JDK)**: Version 8 oder höher.
- **Integrierte Entwicklungsumgebung (IDE)**: Wie IntelliJ IDEA oder Eclipse.
- **Abhängigkeitsverwaltung**: Verwenden Sie Maven oder Gradle, um Ihre Abhängigkeiten zu verwalten.

### Erforderliche Bibliotheken und Abhängigkeiten
Stellen Sie sicher, dass Sie Aspose.Cells für Java mit Maven oder Gradle in Ihr Projekt einbinden.

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Schritte zum Lizenzerwerb
Aspose.Cells für Java ist eine kommerzielle Bibliothek, Sie können jedoch mit einer kostenlosen Testversion beginnen oder eine temporäre Lizenz beantragen. Besuchen Sie die [Kaufseite](https://purchase.aspose.com/buy) um Lizenzierungsoptionen zu erkunden.

## Einrichten von Aspose.Cells für Java
Stellen Sie zunächst sicher, dass Ihre Projektumgebung die erforderlichen Bibliotheken enthält, indem Sie diese wie oben gezeigt über Maven oder Gradle hinzufügen. Nach der Einbindung können Sie Aspose.Cells initialisieren:

```java
import com.aspose.cells.Workbook;

// Initialisieren einer neuen Arbeitsmappeninstanz
Workbook workbook = new Workbook();
```

## Implementierungshandbuch

### Erstellen und Konfigurieren einer Arbeitsmappe
Das Erstellen einer Arbeitsmappe ist der erste Schritt, in dem Sie Ihre Daten einrichten.

#### Bibliotheken importieren
Stellen Sie sicher, dass diese Importe oben in Ihrer Datei enthalten sind:

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

#### Schritt 1: Erstellen einer Arbeitsmappeninstanz
```java
// Erstellt eine leere Arbeitsmappeninstanz zum Arbeiten.
Workbook workbook = new Workbook();
```
Dieser Schritt initialisiert Ihre Excel-Datei programmgesteuert und ermöglicht Ihnen, sie mithilfe der Aspose.Cells-Funktionen zu bearbeiten.

### Zugreifen auf oder Ändern von Arbeitsblattzellen
Als Nächstes füllen Sie die Arbeitsblattzellen mit Daten aus, die für das Kreisdiagramm verwendet werden.

#### Schritt 2: Zugriff auf ein Arbeitsblatt und seine Zellen
```java
// Greifen Sie auf das erste Arbeitsblatt in der Arbeitsmappe zu.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Tragen Sie Beispielwerte, die für ein Kreisdiagramm verwendet werden, in bestimmte Zellen ein.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Tragen Sie Prozentwerte für ein Kreisdiagramm in bestimmte Zellen ein.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Hier füllen Sie das Arbeitsblatt mit Daten, die verschiedene Segmente eines Kreisdiagramms darstellen.

### Erstellen eines Kreisdiagramms

#### Schritt 3: Fügen Sie dem Arbeitsblatt ein Kreisdiagramm hinzu
```java
// Erstellen Sie im Arbeitsblatt ein Kreisdiagramm.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Dieser Schritt fügt Ihrem Arbeitsblatt an den angegebenen Positionen und mit den angegebenen Abmessungen ein neues Kreisdiagramm hinzu.

### Kreisdiagrammreihen und Daten konfigurieren

#### Schritt 4: Legen Sie die Serie für das Diagramm fest
```java
// Konfigurieren Sie den Datenbereich der Serie für das Diagramm.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Verknüpfen Sie den Titel des Kreisdiagramms mit einer Zelle, die den Titeltext enthält.
pie.getTitle().setLinkedSource("D2");
```
Dieser Code verknüpft Ihren Datenbereich und richtet die Reihe für das Kreisdiagramm ein.

### Konfigurieren der Darstellung von Diagrammlegende und -titel

#### Schritt 5: Diagrammlegende und -titel anpassen
```java
// Legen Sie die Legendenposition am unteren Rand des Diagramms fest.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Legen Sie die Schrifteigenschaften für den Diagrammtitel fest.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Durch die Anpassung des Erscheinungsbilds werden die Lesbarkeit und die optische Attraktivität verbessert.

### Farben von Diagrammreihen anpassen

#### Schritt 6: Farben der Kreissegmente ändern
```java
import com.aspose.cells.Color;

// Greifen Sie auf die Farben einzelner Kreisdiagrammsegmente zu und passen Sie diese an.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Diese Einstellungen personalisieren Ihr Diagramm, damit es zu bestimmten Farbschemata passt.

### Spalten automatisch anpassen und Arbeitsmappe speichern

#### Schritt 7: Spaltenbreiten anpassen und Datei speichern
```java
// Alle Spalten automatisch anpassen.
worksheet.autoFitColumns();

// Definieren Sie den Platzhalterpfad des Ausgabeverzeichnisses zum Speichern der Arbeitsmappe.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Speichern Sie die geänderte Arbeitsmappe als Excel-Datei im angegebenen Verzeichnis.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Passen Sie abschließend die Spalten automatisch an und speichern Sie Ihre Arbeitsmappe.

## Praktische Anwendungen
1. **Demografische Analyse**: Verwenden Sie Kreisdiagramme, um die Bevölkerungsverteilung in verschiedenen Ländern oder Regionen anzuzeigen.
2. **Marktanteilsberichte**: Veranschaulichen Sie die Marktanteile verschiedener Unternehmen in einem Sektor.
3. **Budgetzuweisung**: Visualisieren Sie, wie Budgets auf verschiedene Abteilungen innerhalb einer Organisation verteilt werden.

Diese Anwendungen demonstrieren die Vielseitigkeit und Nützlichkeit von Aspose.Cells in realen Szenarien.

## Überlegungen zur Leistung
So optimieren Sie die Leistung bei der Verwendung von Aspose.Cells:
- Minimieren Sie die Speichernutzung, indem Sie nicht mehr benötigte Objekte entsorgen.
- Verwenden Sie effiziente Datenstrukturen zur Verarbeitung großer Datensätze.
- Erstellen Sie ein Profil Ihrer Anwendung, um Engpässe zu identifizieren.

Durch die Einhaltung bewährter Methoden wird ein reibungsloser und reaktionsschneller Betrieb der Anwendungen gewährleistet.

## Abschluss
Dieses Tutorial führte Sie durch die Schritte zum Erstellen und Anpassen eines Kreisdiagramms mit Aspose.Cells in Java. Mit diesem Wissen können Sie diese Techniken nun auf verschiedene Datenvisualisierungsaufgaben in Ihren Projekten anwenden. Für weitere Informationen können Sie sich mit den zusätzlichen Diagrammtypen und erweiterten Anpassungsmöglichkeiten von Aspose.Cells befassen.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}