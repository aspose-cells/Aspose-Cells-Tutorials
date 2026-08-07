---
date: '2026-04-08'
description: Erfahren Sie, wie Sie mit Aspose.Cells für Java ein Liniendiagramm mit
  Markierungen erstellen, das Diagramm dem Arbeitsblatt hinzufügen und Excel‑Diagramme
  für die automatisierte Berichterstellung anpassen.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Liniendiagramm mit Markern mit Aspose.Cells für Java erstellen
url: /de/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen und Gestalten von Excel-Diagrammen mit Aspose.Cells Java

## Einleitung

In der heutigen datengetriebenen Welt ist ein **Liniendiagramm mit Markern** eine der effektivsten Methoden, um Trends und Ausreißer zu visualisieren. Egal, ob Sie automatisierte Berichte oder ein Dashboard erstellen, das täglich aktualisiert wird – die Möglichkeit, programmgesteuert ein Liniendiagramm mit Markern zu einem Arbeitsblatt hinzuzufügen, spart unzählige manuelle Schritte. Dieses Tutorial führt Sie durch die Verwendung von Aspose.Cells für Java zum Erstellen, Gestalten und Exportieren solcher Diagramme, sodass Sie sich auf Erkenntnisse statt auf mühsames Excel‑Herumfummeln konzentrieren können.

**Was Sie lernen werden**
- Initialisierung einer Arbeitsmappe und Befüllung mit Daten mithilfe von Aspose.Cells.  
- **Wie man ein Liniendiagramm mit Markern zu einem Arbeitsblatt hinzufügt** und dessen Aussehen konfiguriert.  
- Anpassung von Serienfarben, Markern und anderen Stiloptionen.  
- Speichern der Arbeitsmappe als Excel‑Datei, die Ihr gestaltetes Diagramm enthält.

## Schnelle Antworten
- **Welche Hauptklasse wird zu Beginn verwendet?** `Workbook` initialisiert eine neue Excel‑Datei.  
- **Welcher Diagrammtyp erzeugt ein Liniendiagramm mit Markern?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Wie setze ich benutzerdefinierte Farben für Serienpunkte?** Verwenden Sie `chart.getNSeries().setColorVaried(true)` und legen Sie die Farben der Marker‑Fläche fest.  
- **Benötige ich eine Lizenz für die volle Funktionalität?** Ja, eine kostenpflichtige oder temporäre Aspose.Cells‑Lizenz entfernt die Evaluationsbeschränkungen.  
- **Kann ich das Ergebnis als XLSX exportieren?** Absolut — `workbook.save("StyledChart.xlsx")` erzeugt eine XLSX‑Datei.

## Voraussetzungen

Bevor Sie Diagramme mit Aspose.Cells für Java erstellen und gestalten, stellen Sie sicher, dass die folgende Umgebung eingerichtet ist:

### Erforderliche Bibliotheken
Binden Sie Aspose.Cells als Abhängigkeit in Ihr Projekt ein. Hier finden Sie Anleitungen für Maven‑ und Gradle‑Benutzer:

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

### Umgebungsanforderungen
- Java Development Kit (JDK) auf Ihrem System installiert.  
- Eine integrierte Entwicklungsumgebung (IDE) wie IntelliJ IDEA oder Eclipse zum Schreiben und Testen des Codes.

### Vorkenntnisse
Grundlegende Kenntnisse der Java‑Programmierung sind erforderlich, ebenso wie Vertrautheit mit Excel‑Arbeitsmappen und Diagrammkonzepten. 

### Lizenzbeschaffung
Aspose.Cells ist ein kommerzielles Produkt, das für die volle Funktionalität eine Lizenz erfordert. Sie können eine kostenlose Testversion erhalten, um die Funktionen zu evaluieren, eine temporäre Lizenz für ausgedehnte Tests anfordern oder das Produkt für den langfristigen Einsatz erwerben.

- **Kostenlose Testversion:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporäre Lizenz:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Kauf:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Einrichten von Aspose.Cells für Java

Nachdem Sie die erforderlichen Abhängigkeiten installiert haben, richten Sie Ihre Entwicklungsumgebung ein, um Aspose.Cells zu verwenden. Importieren Sie die Bibliothek und initialisieren Sie ein `Workbook`‑Objekt in Ihrer Java‑Anwendung:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Implementierungsleitfaden

In diesem Abschnitt zerlegen wir die Implementierung in einzelne Funktionen: Arbeitsmappeninitialisierung und Datenbefüllung, Diagrammerstellung und -konfiguration, Serienanpassung sowie Speichern der Arbeitsmappe.

### Funktion 1: Arbeitsmappeninitialisierung und Datenbefüllung

**Übersicht:** Diese Funktion konzentriert sich darauf, eine neue Arbeitsmappe zu erstellen, das erste Arbeitsblatt zu öffnen und es mit Daten für die Diagrammerstellung zu befüllen.

#### Schritt 1: Arbeitsmappe initialisieren
Instanziieren Sie ein `Workbook`‑Objekt:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Schritt 2: Spaltentitel festlegen und Daten befüllen
Definieren Sie die Spaltenüberschriften und füllen Sie Zeilen mit Beispieldaten:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funktion 2: Diagrammerstellung und -konfiguration

**Übersicht:** Diese Funktion demonstriert, wie ein Diagramm zum Arbeitsblatt hinzugefügt, dessen Stil festgelegt und grundlegende Eigenschaften konfiguriert werden.

#### Schritt 3: Diagramm zum Arbeitsblatt hinzufügen
Fügen Sie ein Liniendiagramm mit Datenmarkern hinzu:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funktion 3: Serienkonfiguration und -anpassung

**Übersicht:** Verbessern Sie die visuelle Attraktivität Ihrer Diagramme, indem Sie Serieneinstellungen wie variierte Farben und Marker‑Stile anpassen.

#### Schritt 4: Serieneinstellungen anpassen
Konfigurieren Sie die Seriendaten, wenden Sie benutzerdefinierte Formatierungen an und passen Sie Marker an:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funktion 4: Arbeitsmappe speichern

**Übersicht:** Speichern Sie schließlich die Arbeitsmappe, um Ihre Änderungen zu übernehmen und sicherzustellen, dass das Diagramm in der Excel‑Datei enthalten ist.

#### Schritt 5: Arbeitsmappe speichern
Speichern Sie Ihre Arbeitsmappe mit den neu erstellten Diagrammen:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Häufige Probleme und Fehlersuche

- **Diagramm erscheint leer:** Stellen Sie sicher, dass die Zellbereiche, die in `setXValues` und `setValues` verwendet werden, korrekt auf befüllte Zellen verweisen.  
- **Farben werden nicht angewendet:** Vergewissern Sie sich, dass `chart.getNSeries().setColorVaried(true)` vor der individuellen Anpassung der Serien aufgerufen wird.  
- **Lizenzfehler:** Eine Testlizenz kann die Anzahl der Diagramme einschränken; installieren Sie eine Voll‑Lizenz, um Beschränkungen zu entfernen.

## Häufig gestellte Fragen

**F: Kann ich mit Aspose.Cells andere Diagrammtypen (z. B. Balken, Kreis) erstellen?**  
A: Ja, Aspose.Cells unterstützt eine breite Palette von Diagrammtypen; ersetzen Sie einfach `ChartType.LINE_WITH_DATA_MARKERS` durch den gewünschten Enum‑Wert.

**F: Muss ich die Arbeitsmappe schließen oder Ressourcen freigeben?**  
A: Die Klasse `Workbook` verwaltet Ressourcen automatisch, Sie können jedoch in langlaufenden Anwendungen `workbook.dispose()` aufrufen, um Speicher freizugeben.

**F: Ist es möglich, mehrere Diagramme in dasselbe Arbeitsblatt einzufügen?**  
A: Absolut — rufen Sie `worksheet.getCharts().add(...)` für jedes Diagramm auf, das Sie einfügen möchten.

**F: Wie exportiere ich die Datei in ein älteres Excel‑Format (XLS)?**  
A: Verwenden Sie `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**F: Behält das Diagramm sein Styling bei, wenn es in Microsoft Excel geöffnet wird?**  
A: Ja, Aspose.Cells schreibt native Excel‑Diagrammobjekte, sodass alle Stile, Farben und Marker exakt wie definiert erscheinen.

---

**Zuletzt aktualisiert:** 2026-04-08  
**Getestet mit:** Aspose.Cells 25.3 für Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}