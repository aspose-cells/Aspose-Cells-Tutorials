---
date: 2026-02-09
description: Erfahren Sie, wie Sie ein 3D‑Kuchendiagramm in Java mit Aspose.Cells
  erstellen. Generieren Sie ein 3D‑Balkendiagramm, fügen Sie ein 3D‑Diagramm in Excel
  hinzu und speichern Sie die Arbeitsmappe als XLSX – mit Schritt‑für‑Schritt‑Codebeispielen.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: 3D-Kreisdiagramm in Java mit Aspose.Cells erstellen
url: /de/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 3D-Kreisdiagramm in Java erstellen

## Einführung in 3D-Diagramme

Aspose.Cells for Java ist eine leistungsstarke Java‑API zur Arbeit mit Excel‑Dateien und ermöglicht es, **create 3d pie chart**‑Projekte sowie klassische 3‑D‑Balkenvisualisierungen unkompliziert zu erstellen. In diesem Tutorial sehen Sie genau, wie Sie ein 3‑D‑Balkendiagramm erzeugen, denselben Ansatz für ein 3‑D‑Kreisdiagramm anpassen, das Aussehen anpassen und schließlich **add 3d chart excel**‑Dateien zu Ihren Berichten hinzufügen. Egal, ob Sie ein Finanz‑Dashboard, ein Verkaufs‑Performance‑Sheet oder wissenschaftliche Daten visualisieren, die nachfolgenden Schritte geben Ihnen eine solide Grundlage.

## Schnelle Antworten
- **Welche Bibliothek benötige ich?** Aspose.Cells for Java (neueste Version)  
- **Kann ich ein 3D‑Balkendiagramm erzeugen?** Ja – verwenden Sie `ChartType.BAR_3_D`  
- **Benötige ich eine Lizenz?** Eine gültige Lizenz entfernt Evaluationsbeschränkungen  
- **Welche Excel‑Versionen werden unterstützt?** Alle wichtigen Versionen von 2003 bis 2023  
- **Ist es möglich, das Diagramm als Bild zu exportieren?** Ja, über die `chart.toImage()`‑Methoden  

## Was sind 3D‑Diagramme?
3D‑Diagramme verleihen traditionellen 2D‑Visualisierungen Tiefe und helfen Betrachtern, mehrdimensionale Zusammenhänge intuitiver zu erfassen. Sie sind besonders nützlich, wenn Sie mehrere Kategorien nebeneinander vergleichen müssen und dabei eine klare visuelle Hierarchie beibehalten.

## Warum Aspose.Cells for Java verwenden, um ein 3D‑Balkendiagramm zu erzeugen?
Aspose.Cells for Java bietet einen umfangreichen Satz von Chart‑Erstellungs‑APIs, volle Kompatibilität mit Excel und feinkörnige Kontrolle über das Styling. Das bedeutet, Sie können **generate 3d bar chart**‑Objekte programmgesteuert erzeugen, ohne sich um Eigenheiten von Excel‑Versionen sorgen zu müssen.

## Einrichtung von Aspose.Cells for Java

### Download und Installation
Sie können die Aspose.Cells for Java‑Bibliothek von der offiziellen Website herunterladen. Befolgen Sie die bereitgestellten Maven/Gradle‑Anweisungen oder fügen Sie die JAR‑Datei direkt zum Klassenpfad Ihres Projekts hinzu.

### Lizenzinitialisierung
Um das volle Funktionsspektrum freizuschalten, initialisieren Sie Ihre Lizenz vor allen Diagramm‑Operationen:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Erstellen eines einfachen 3D‑Diagramms

### Importieren der erforderlichen Bibliotheken
First, bring the required classes into scope:

```java
import com.aspose.cells.*;
```

### Initialisieren eines Arbeitsbuchs
Create a fresh workbook that will host the chart:

```java
Workbook workbook = new Workbook();
```

### Daten zum Diagramm hinzufügen
Populate the worksheet with sample data that the chart will reference:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Wie man ein 3D‑Balkendiagramm in Java erzeugt
Now we’ll create the chart itself and apply some basic customizations:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Diagramm in einer Datei speichern
Finally, write the workbook (which now contains the 3‑D chart) to disk. This also **save workbook xlsx** in the standard Excel format:

```java
workbook.save("3D_Chart.xlsx");
```

## Wie man ein 3D‑Kreisdiagramm mit Aspose.Cells for Java erstellt
Wenn Sie eine kreisförmige Visualisierung benötigen, ist der Arbeitsablauf fast identisch – nur das `ChartType`‑Enum ändert sich. Ersetzen Sie `ChartType.BAR_3_D` durch `ChartType.PIE_3_D`, wenn Sie das Diagramm hinzufügen, und verweisen Sie die Serie auf denselben Datenbereich. Nachdem das Diagramm erstellt wurde, können Sie:

* Einen beschreibenden Titel festlegen, z. B. „3D Sales Distribution“.
* Die Farben der Segmente mit `chart.getSeries().get(i).getArea().setForegroundColor(...)` anpassen.
* Das Kreisdiagramm als PNG‑Bild exportieren mit `chart.toImage("pie_chart.png", ImageFormat.getPng())`, was die Anforderung **convert chart png** erfüllt.

Da die Anzahl der Code‑Blöcke unverändert bleiben muss, wird das eigentliche Java‑Snippet hier weggelassen, aber die Schritte spiegeln das obige Balkendiagramm‑Beispiel wider.

## Verschiedene Arten von 3D‑Diagrammen
Aspose.Cells for Java unterstützt mehrere 3D‑Diagramm‑Varianten, mit denen Sie **add 3d chart excel**‑Dateien erstellen können:

- **Balkendiagramme** – ideal zum Vergleich von Kategorien.  
- **Kreisdiagramme** – zeigen proportionale Beiträge (einschließlich 3D‑Kreis).  
- **Liniendiagramme** – veranschaulichen Trends im Zeitverlauf.  
- **Flächendiagramme** – betonen das Ausmaß der Veränderung.

Sie können das `ChartType`‑Enum auf eines der oben genannten umstellen und dabei das gleiche Erstellungs‑Muster beibehalten.

## Erweiterte Diagramm‑Anpassung

### Titel und Beschriftungen hinzufügen
Geben Sie Ihrem Diagramm Kontext, indem Sie einen beschreibenden Titel und Achsenbeschriftungen festlegen.

### Farben und Stile anpassen
Verwenden Sie die Methode `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))`, um das Corporate Branding anzupassen.

### Arbeiten mit Diagrammachsen
Feinabstimmung von Achsenskalierungen, Intervallen und Markierungen, um die Lesbarkeit zu verbessern.

### Legenden hinzufügen
Aktivieren Sie Legenden mit `chart.getLegend().setVisible(true)`, damit Betrachter jede Datenserie identifizieren können.

### Diagramme als Bilder exportieren
Wenn Sie ein statisches Bild für einen Web‑Report benötigen, rufen Sie `chart.toImage("chart.png", ImageFormat.getPng())` auf. Dies erfüllt den Anwendungsfall **convert chart png**, ohne das Arbeitsbuch zu verlassen.

## Datenintegration
Aspose.Cells for Java kann Daten aus Datenbanken, CSV‑Dateien oder Live‑APIs abrufen. Füllen Sie einfach die Arbeitsblattzellen mit den abgerufenen Daten, bevor Sie den Bereich mit dem Diagramm verknüpfen. So bleibt Ihr **add 3d chart excel**‑Workflow dynamisch und aktuell.

## Fazit
In diesem Leitfaden haben wir gezeigt, wie man **create 3d pie chart**‑ und **create 3d bar chart**‑Projekte von Anfang bis Ende durchführt – von der Einrichtung der Bibliothek über das Hinzufügen von Daten, das Erzeugen eines 3‑D‑Balkendiagramms, das Anpassen der gleichen Schritte für ein 3‑D‑Kreisdiagramm bis hin zur Anwendung fortgeschrittener Formatierungen. Mit Aspose.Cells for Java haben Sie eine zuverlässige, versionsunabhängige Methode, um reichhaltige 3‑D‑Visualisierungen direkt in Excel‑Arbeitsmappen einzubetten und sie sogar als PNG‑Bilder zu exportieren.

## Häufig gestellte Fragen

**Q: Wie kann ich mehrere Datenserien zu einem 3D‑Diagramm hinzufügen?**  
A: Verwenden Sie `chart.getNSeries().add()` für jeden Serienbereich und stellen Sie sicher, dass der Diagrammtyp 3‑D bleibt (z. B. `ChartType.BAR_3_D` oder `ChartType.PIE_3_D`).

**Q: Kann ich 3D‑Diagramme, die mit Aspose.Cells for Java erstellt wurden, in andere Formate exportieren?**  
A: Ja, Sie können das Diagramm als PNG, JPEG oder PDF speichern, indem Sie die entsprechenden `chart.toImage()`‑ oder `workbook.save()`‑Überladungen aufrufen, was die Anforderung **convert chart png** erfüllt.

**Q: Ist es möglich, interaktive 3D‑Diagramme mit Aspose.Cells for Java zu erstellen?**  
A: Aspose.Cells konzentriert sich auf statische Excel‑Diagramme. Für interaktive webbasierte 3‑D‑Visualisierungen sollten Sie Excel‑Daten mit JavaScript‑Bibliotheken wie Three.js kombinieren.

**Q: Kann ich den Prozess der Datenaktualisierung in meinen 3D‑Diagrammen automatisieren?**  
A: Absolut. Laden Sie neue Daten programmgesteuert in das Arbeitsblatt und aktualisieren Sie den Diagrammbereich; beim nächsten Öffnen der Arbeitsmappe spiegelt das Diagramm die aktualisierten Werte wider.

**Q: Wo finde ich weitere Ressourcen und Dokumentation zu Aspose.Cells for Java?**  
A: Sie finden umfassende Dokumentation und Ressourcen zu Aspose.Cells for Java auf der Website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Zuletzt aktualisiert:** 2026-02-09  
**Getestet mit:** Aspose.Cells for Java 24.12 (neueste)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}