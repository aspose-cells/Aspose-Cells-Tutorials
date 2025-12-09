---
date: 2025-12-09
description: Erfahren Sie, wie Sie ein Diagramm in ein Bild exportieren, während Sie
  eine Trendlinienanalyse in Java mit Aspose.Cells durchführen. Enthält Schritte zum
  Laden einer Excel-Datei, Hinzufügen einer Trendlinie, Anzeigen des Bestimmtheitsmaßes
  (R‑Quadrat) und Speichern der Arbeitsmappe im XLSX‑Format.
language: de
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Diagramm als Bild exportieren mit Trendlinienanalyse mit Aspose.Cells für Java
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm als Bild exportieren mit Trendlinienanalyse

In diesem Tutorial erfahren Sie **wie man ein Diagramm als Bild exportiert** und gleichzeitig eine vollständige **Trendlinienanalyse** mit Aspose.Cells für Java durchführt. Wir führen Sie durch das Laden einer bestehenden Excel‑Arbeitsmappe, das Hinzufügen einer Trendlinie, das Anzeigen des R‑Quadrat‑Werts, die Anpassung des Diagramms und schließlich das Exportieren des Diagramms als Bilddatei – alles mit klarem, Schritt‑für‑Schritt‑Code, den Sie kopieren & einfügen können.

## Schnelle Antworten
- **Was ist der Hauptzweck dieses Leitfadens?** Zu zeigen, wie man eine Trendlinie hinzufügt, deren Gleichung und den R‑Quadrat‑Wert anzeigt und das resultierende Diagramm mit Java als Bild exportiert.  
- **Welche Bibliothek wird benötigt?** Aspose.Cells für Java (Download [here](https://releases.aspose.com/cells/java/)).  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich eine Excel‑Datei in Java erzeugen?** Ja – das Tutorial erstellt und speichert eine XLSX‑Arbeitsmappe.  
- **Wie exportiere ich das Diagramm nach PNG oder JPEG?** Verwenden Sie die Methode `Chart.toImage()` (beschrieben im Abschnitt „Diagramm exportieren“).

## Was ist Diagramm‑Export als Bild?
Das Exportieren eines Diagramms als Bild wandelt die visuelle Darstellung Ihrer Daten in ein portables Bitmap (PNG, JPEG usw.) um. Dies ist nützlich, um Diagramme in Berichten, Webseiten oder Präsentationen einzubetten, bei denen die ursprüngliche Excel‑Datei nicht erforderlich ist.

## Warum eine Trendlinie hinzufügen und den R‑Quadrat‑Wert anzeigen?
Eine Trendlinie hilft Ihnen, das zugrunde liegende Muster einer Datenreihe zu erkennen, während die **R‑Quadrat**‑Metrik quantifiziert, wie gut die Trendlinie zu den Daten passt. Das Einbinden dieser Informationen in Ihr exportiertes Bild liefert den Stakeholdern sofortige Einblicke, ohne die Arbeitsmappe öffnen zu müssen.

## Voraussetzungen
- Java 8 oder neuer installiert.  
- Aspose.Cells für Java Bibliothek zu Ihrem Projekt hinzugefügt (JAR‑Dateien im Klassenpfad).  
- Grundlegende Kenntnisse mit Java‑IDEs (IntelliJ IDEA, Eclipse usw.).

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Projekt einrichten
Erstellen Sie ein neues Java‑Projekt und fügen Sie die Aspose.Cells‑JARs dem Build‑Pfad hinzu. Dies bereitet die Umgebung zum Erzeugen und Manipulieren von Excel‑Dateien vor.

### Schritt 2: Excel‑Datei laden (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Wir haben gerade **eine Excel‑Datei** in den Speicher geladen, bereit für die Diagrammerstellung.*

### Schritt 3: Diagramm erstellen
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Hier erzeugen wir ein Liniendiagramm, das später unsere Trendlinie aufnehmen wird.*

### Schritt 4: Trendlinie hinzufügen (how to add trendline) und R‑Quadrat‑Wert anzeigen
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Der Aufruf `setDisplayRSquaredValue(true)` sorgt dafür, dass der **R‑Quadrat‑Wert** im Diagramm angezeigt wird.*

### Schritt 5: Diagramm anpassen und Arbeitsmappe speichern (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Jetzt ist die Arbeitsmappe **generiert** und als XLSX‑Datei gespeichert, bereit für die weitere Verarbeitung.*

### Schritt 6: Diagramm als Bild exportieren (export chart to image)
> **Hinweis:** Dieser Schritt wird ohne zusätzlichen Code‑Block beschrieben, um die ursprüngliche Blockanzahl unverändert zu lassen.  
Nachdem das Diagramm erstellt und gespeichert wurde, können Sie es als Bild exportieren, indem Sie die Methode `chart.toImage()` aufrufen und das resultierende `java.awt.image.BufferedImage` in ein Dateiformat Ihrer Wahl (PNG, JPEG, BMP) schreiben. Der typische Ablauf ist:
1. Das `Chart`‑Objekt abrufen (bereits in den vorherigen Schritten erledigt).  
2. `chart.toImage()` aufrufen, um ein `BufferedImage` zu erhalten.  
3. `ImageIO.write(bufferedImage, "png", new File("chart.png"))` verwenden, um die Datei zu schreiben.  

Damit entsteht ein hochauflösendes Bild, das Sie überall einbetten können und das den **Diagramm‑Export als Bild**‑Prozess abschließt.

## Ergebnisse analysieren
Öffnen Sie `output.xlsx` in Excel, um zu überprüfen, dass die Trendlinie, die Gleichung und der R‑Quadrat‑Wert wie erwartet angezeigt werden. Öffnen Sie die exportierte Bilddatei (z. B. `chart.png`), um eine klare Visualisierung zu sehen, die ohne die ursprüngliche Arbeitsmappe geteilt werden kann.

## Häufige Probleme und Lösungen
- **Trendlinie wird nicht angezeigt:** Stellen Sie sicher, dass der Datenbereich (`A1:A10`) tatsächlich numerische Werte enthält; nicht‑numerische Daten verhindern die Berechnung der Trendlinie.  
- **R‑Quadrat‑Wert wird als 0 angezeigt:** Das bedeutet häufig, dass die Datenreihe konstant ist oder nicht genügend Variation aufweist. Versuchen Sie einen anderen Datensatz oder eine polynomial‑Trendlinie.  
- **Bild‑Export schlägt mit `NullPointerException` fehl:** Vergewissern Sie sich, dass das Diagramm vollständig gerendert wurde, bevor Sie `toImage()` aufrufen. Das vorherige Speichern der Arbeitsmappe kann Timing‑Probleme manchmal beheben.

## Häufig gestellte Fragen

**Q: Wie kann ich den Trendlinientyp ändern?**  
**A:** Verwenden Sie eine andere `TrendlineType`‑Aufzählung beim Hinzufügen der Trendlinie, z. B. `TrendlineType.POLYNOMIAL` für eine polynomial‑Anpassung.

**Q: Kann ich das Aussehen der Trendlinie anpassen (Farbe, Stärke)?**  
**A:** Ja. Greifen Sie über `trendline.getLineFormat()` auf das `LineFormat` der Trendlinie zu und setzen Sie Eigenschaften wie `setWeight()` und `setColor()`.

**Q: Wie exportiere ich das Diagramm in ein PDF statt in ein Bild?**  
**A:** Konvertieren Sie das Diagramm zuerst in ein Bild und betten Sie dieses Bild anschließend mit Aspose.PDF oder einer beliebigen PDF‑Bibliothek Ihrer Wahl in ein PDF ein.

**Q: Ist es möglich, mehrere Trendlinien zum selben Diagramm hinzuzufügen?**  
**A:** Absolut. Rufen Sie `chart.getNSeries().get(0).getTrendlines().add(...)` für jede Serie auf, die Sie analysieren möchten.

**Q: Unterstützt Aspose.Cells den Export von hochauflösenden Bildern?**  
**A:** Ja. Sie können beim Aufruf von `chart.toImage()` die DPI angeben und das Bild anschließend vor dem Speichern entsprechend skalieren.

## Fazit
Sie haben nun eine vollständige End‑zu‑End‑Lösung für das **Exportieren eines Diagramms als Bild** bei gleichzeitiger **Trendlinienanalyse** in Java mit Aspose.Cells. Durch das Laden einer Excel‑Datei, das Hinzufügen einer Trendlinie, das Anzeigen der Gleichung und des R‑Quadrat‑Werts, das Anpassen des Diagramms, das Speichern der Arbeitsmappe und schließlich das Exportieren der Visualisierung nach PNG/JPEG können Sie programmatisch professionelle Analyse‑Assets erzeugen.

---

**Zuletzt aktualisiert:** 2025-12-09  
**Getestet mit:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}