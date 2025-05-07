---
"date": "2025-04-07"
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für Java Diagramme in Excel erstellen und anpassen. Automatisieren Sie die Diagrammerstellung, verbessern Sie die Datenvisualisierung und sparen Sie Zeit mit dieser ausführlichen Anleitung."
"title": "Erstellen und Gestalten von Excel-Diagrammen mit Aspose.Cells Java – Ein umfassender Leitfaden"
"url": "/de/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Erstellen und Gestalten von Excel-Diagrammen mit Aspose.Cells Java

## Einführung

In der heutigen datengetriebenen Welt ist eine effektive Informationsvisualisierung für Analysen und Entscheidungen entscheidend. Oftmals ist es notwendig, dynamische Diagramme in Excel-Arbeitsmappen programmgesteuert zu erstellen – insbesondere bei großen Datensätzen oder automatisierten Berichtssystemen. Dieses Tutorial zeigt, wie Sie mit Aspose.Cells für Java Diagramme in Excel nahtlos erstellen und anpassen. Durch die Integration von Aspose.Cells in Ihre Java-Anwendungen können Sie die Diagrammerstellung automatisieren, die Datenpräsentation verbessern und Zeit sparen.

**Was Sie lernen werden:**
- Initialisieren einer Arbeitsmappe und Auffüllen mit Daten mithilfe von Aspose.Cells.
- Erstellen und Konfigurieren von Liniendiagrammen mit Datenmarkierungen.
- Anpassen des Erscheinungsbilds und der Farben der Serie zur besseren Visualisierung.
- Speichern der Arbeitsmappe mit dem neu erstellten Diagramm in einem Excel-Format.

Lassen Sie uns zunächst die Voraussetzungen besprechen, die für den Einstieg erforderlich sind.

## Voraussetzungen

Bevor Sie Diagramme mit Aspose.Cells für Java erstellen und gestalten, stellen Sie sicher, dass Sie über die folgende Konfiguration verfügen:

### Erforderliche Bibliotheken
Fügen Sie Aspose.Cells als Abhängigkeit in Ihr Projekt ein. Hier finden Sie Anweisungen für Maven- und Gradle-Benutzer:

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
- Auf Ihrem System ist das Java Development Kit (JDK) installiert.
- Eine integrierte Entwicklungsumgebung (IDE) wie IntelliJ IDEA oder Eclipse zum Codieren und Testen.

### Voraussetzungen
Erforderlich sind grundlegende Kenntnisse der Java-Programmierung sowie Kenntnisse im Umgang mit Excel-Arbeitsmappen und Diagrammkonzepten. 

### Lizenzerwerb
Aspose.Cells ist ein kommerzielles Produkt, für dessen volle Funktionalität eine Lizenz erforderlich ist. Sie können eine kostenlose Testversion erhalten, um die Funktionen zu testen, eine temporäre Lizenz für längere Tests anfordern oder das Produkt für die langfristige Nutzung erwerben.

- **Kostenlose Testversion:** [Kostenlose Testversion herunterladen](https://releases.aspose.com/cells/java/)
- **Temporäre Lizenz:** [Temporäre Lizenz anfordern](https://purchase.aspose.com/temporary-license/)
- **Kaufen:** [Aspose.Cells kaufen](https://purchase.aspose.com/buy)

## Einrichten von Aspose.Cells für Java

Nachdem Sie die erforderlichen Abhängigkeiten installiert haben, richten Sie Ihre Entwicklungsumgebung für die Verwendung von Aspose.Cells ein. Importieren Sie zunächst die Bibliothek und initialisieren Sie ein Workbook-Objekt in Ihrer Java-Anwendung:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialisieren einer neuen Arbeitsmappeninstanz
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Implementierungshandbuch

In diesem Abschnitt unterteilen wir die Implementierung in einzelne Funktionen: Initialisierung und Datenauffüllung der Arbeitsmappe, Erstellung und Konfiguration von Diagrammen, Serienanpassung und Speichern der Arbeitsmappe.

### Funktion 1: Initialisierung der Arbeitsmappe und Datenauffüllung

**Überblick:** Bei dieser Funktion geht es darum, eine neue Arbeitsmappe zu erstellen, auf das erste Arbeitsblatt zuzugreifen und es mit Daten für die Diagrammerstellung zu füllen.

#### Schritt 1: Initialisieren der Arbeitsmappe
Beginnen Sie mit der Instanziierung eines `Workbook` Objekt:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instanziieren einer Arbeitsmappe
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Schritt 2: Spaltentitel festlegen und Daten eintragen
Definieren Sie die Spaltenüberschriften und füllen Sie die Zeilen mit Beispieldaten:

```java
        // Spaltentitel festlegen 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Erstellen Sie Zufallsdaten für Serie 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Erstellen Sie Zufallsdaten für Serie 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funktion 2: Diagrammerstellung und -konfiguration

**Überblick:** Diese Funktion zeigt, wie Sie dem Arbeitsblatt der Arbeitsmappe ein Diagramm hinzufügen, seinen Stil festlegen und grundlegende Eigenschaften konfigurieren.

#### Schritt 3: Dem Arbeitsblatt ein Diagramm hinzufügen
Fügen Sie ein Liniendiagramm mit Datenmarkierungen hinzu:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instanziieren einer Arbeitsmappe
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Diagramm zum Arbeitsblatt hinzufügen
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Zugriff auf und Konfiguration des Diagramms
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Festlegen eines vordefinierten Stils
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funktion 3: Serienkonfiguration und -anpassung

**Überblick:** Verbessern Sie die visuelle Attraktivität Ihrer Diagramme, indem Sie Serieneinstellungen wie verschiedene Farben und Markierungsstile anpassen.

#### Schritt 4: Serieneinstellungen anpassen
Konfigurieren Sie Seriendaten, wenden Sie benutzerdefinierte Formatierungen an und passen Sie Markierungen an:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instanziieren einer Arbeitsmappe
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Hinzufügen von Reihen zum Diagramm
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Aktivieren Sie verschiedene Farben für Serienpunkte
        chart.getNSeries().setColorVaried(true);

        // Passen Sie die Stile und Farben der Markierungen der ersten Serie an
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Legen Sie die X- und Y-Werte für die erste Serie fest
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Passen Sie Stile und Farben der Markierungen der zweiten Serie an
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Legen Sie die X- und Y-Werte für die zweite Reihe fest
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funktion 4: Arbeitsmappen speichern

**Überblick:** Speichern Sie abschließend die Arbeitsmappe, um Ihre Änderungen beizubehalten und sicherzustellen, dass das Diagramm in die Excel-Datei aufgenommen wird.

#### Schritt 5: Speichern der Arbeitsmappe
Speichern Sie Ihre Arbeitsmappe mit den neu erstellten Diagrammen:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instanziieren einer Arbeitsmappe
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu und fügen Sie Daten und Diagrammkonfiguration wie in den vorherigen Schritten hinzu …
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Die Implementierung zum Hinzufügen von Daten und Konfigurieren des Diagramms erfolgt hier.)

        // Speichern Sie die Arbeitsmappe in einer Excel-Datei
        workbook.save("StyledChart.xlsx");
    }
}
```

**Keyword-Empfehlungen:**
- „Aspose.Cells für Java“
- „Excel-Diagrammerstellung mit Java“
- „Java-Programmierung für Excel-Automatisierung“

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}