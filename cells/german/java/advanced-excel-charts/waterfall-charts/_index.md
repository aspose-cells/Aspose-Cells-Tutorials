---
date: 2025-12-10
description: Erfahren Sie, wie Sie ein Wasserfalldiagramm in Java mit Aspose.Cells
  erstellen. Schritt‑für‑Schritt‑Anleitung zum Hinzufügen eines Diagramms zum Arbeitsblatt,
  Anpassen und Speichern der Arbeitsmappe als XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Wie man ein Wasserfalldiagramm mit Aspose.Cells für Java erstellt
url: /de/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wasserfalldiagramme

## Einführung in Wasserfalldiagramme mit Aspose.Cells für Java

In diesem Tutorial lernen Sie, wie Sie ein **Wasserfalldiagramm erstellen** mit Aspose.Cells für Java. Wasserfalldiagramme sind ein unverzichtbares Werkzeug in der Datenvisualisierung, weil sie Ihnen ermöglichen, die kumulative Wirkung einer Reihe von positiven und negativen Werten zu sehen. Egal, ob Sie einen Finanzbericht, einen Vertriebsleistungsbericht oder eine andere datenbasierte Analyse vorbereiten, ein Wasserfalldiagramm kann rohe Zahlen in klare, umsetzbare Erkenntnisse verwandeln.

## Schnellantworten
- **Was ist ein Wasserfalldiagramm?** Eine Visualisierung, die zeigt, wie ein Anfangswert durch eine Reihe von Zwischenschritten erhöht und verringert wird und schließlich zu einem Endwert führt.  
- **Welche Bibliothek wird verwendet?** Aspose.Cells für Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Datei als XLSX speichern?** Ja – verwenden Sie `workbook.save("FileName.xlsx")`.  
- **Ist es für Java‑Datenvisualisierung geeignet?** Absolut; Aspose.Cells bietet umfangreiche Diagrammfunktionen ohne installierte Office‑Software.

## Was ist ein Wasserfalldiagramm?
Ein Wasserfalldiagramm stellt sequenzielle positive und negative Beiträge zu einem Ausgangswert dar und hilft Ihnen zu verstehen, wie jede Komponente das Gesamtergebnis beeinflusst.

## Warum Aspose.Cells für Java verwenden, um ein Wasserfalldiagramm hinzuzufügen?
- **Kein Excel erforderlich** – Diagramme auf jedem Server oder CI‑Pipeline erzeugen.  
- **Vollständige Kontrolle über das Layout** – Farben, Datenbeschriftungen und Achsen können programmgesteuert angepasst werden.  
- **Unterstützt mehrere Ausgabeformate** – XLSX, PDF, HTML und mehr.  
- **Hohe Leistung** – ideal für große Arbeitsmappen und automatisierte Berichte.

## Voraussetzungen

Bevor wir in den Code eintauchen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Aspose.Cells für Java: Sie müssen Aspose.Cells für Java installiert haben. Sie können es von [hier](https://releases.aspose.com/cells/java/) herunterladen.

- Java‑Entwicklungsumgebung: Stellen Sie sicher, dass Java auf Ihrem System installiert ist.

Jetzt beginnen wir Schritt für Schritt mit dem Erstellen des Wasserfalldiagramms.

## Wie man ein Wasserfalldiagramm in Java erstellt

### Schritt 1: Aspose.Cells importieren

```java
import com.aspose.cells.*;
```

Zuerst müssen Sie die Aspose.Cells‑Bibliothek in Ihr Java‑Projekt importieren. Diese Bibliothek bietet umfangreiche Funktionen zum Arbeiten mit Excel‑Dateien, einschließlich der Diagrammerstellung.

### Schritt 2: Arbeitsmappe und Arbeitsblatt initialisieren

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Erstellen Sie eine neue Arbeitsmappe und fügen Sie ein Arbeitsblatt hinzu. Wir verwenden dieses Arbeitsblatt, um unsere Daten einzugeben und **Diagramm zum Arbeitsblatt hinzufügen**.

### Schritt 3: Daten eingeben

Jetzt füllen wir das Arbeitsblatt mit den Daten, die wir im Wasserfalldiagramm darstellen möchten.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

In diesem Beispiel haben wir Kategorien in Spalte A und die entsprechenden Werte in Spalte B. Sie können diese Daten durch Ihren eigenen Datensatz ersetzen.

### Schritt 4: Das Wasserfalldiagramm erstellen

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Wir haben ein Wasserfalldiagramm zu unserem Arbeitsblatt hinzugefügt, die Datenreihe und die Kategoriedaten angegeben. Dies ist der zentrale Schritt, der **Wasserfalldiagramm hinzufügt** zu Ihrem Blatt. Sie können das Erscheinungsbild des Diagramms (Farben, Datenbeschriftungen usw.) über die Eigenschaften des `Chart`‑Objekts weiter anpassen.

### Schritt 5: Die Arbeitsmappe speichern

```java
workbook.save("WaterfallChart.xlsx");
```

Speichern Sie die Arbeitsmappe in einer Datei. Das Beispiel verwendet das XLSX‑Format, aber Aspose.Cells ermöglicht auch den Export nach PDF, CSV und vielen anderen Formaten. Damit wird die Anforderung **save workbook xlsx** erfüllt.

## Häufige Probleme und Lösungen

- **Diagramm erscheint leer** – Prüfen Sie, ob die Datenbereichsreferenzen (`B2:B6` und `A2:A6`) mit den tatsächlichen Zellen übereinstimmen, die Ihre Werte und Kategorien enthalten.  
- **Negative Werte werden nicht korrekt angezeigt** – Stellen Sie sicher, dass der Diagrammtyp auf `ChartType.WATERFALL` gesetzt ist; andere Diagrammtypen behandeln Negative anders.  
- **Datei lässt sich in Excel nicht öffnen** – Vergewissern Sie sich, dass Sie eine aktuelle Version von Aspose.Cells (die neueste Veröffentlichung) verwenden und dass die Dateierweiterung zum Format passt (`.xlsx` für Excel).

## Häufig gestellte Fragen

### Wie kann ich das Erscheinungsbild meines Wasserfalldiagramms anpassen?

Sie können das Erscheinungsbild Ihres Wasserfalldiagramms anpassen, indem Sie Eigenschaften wie Farben, Datenbeschriftungen und Achsenbeschriftungen ändern Weitere Details finden Sie in der Aspose.Cells‑Dokumentation.

### Kann ich mehrere Wasserfalldiagramme im selben Arbeitsblatt erstellen?

Ja, Sie können mehrere Wasserfalldiagramme im selben Arbeitsblatt erstellen, indem Sie dieselben Schritte mit **verschiedenen Datenbereichen** wiederholen.

### Ist Aspose.Cells mit verschiedenen Java‑Entwicklungsumgebungen kompatibel?

Ja, Aspose.Cells für Java ist mit verschiedenen Java‑Entwicklungsumgebungen kompatibel, einschließlich Eclipse, IntelliJ IDEA und NetBeans.

### Kann ich zusätzliche Datenreihen zu meinem Wasserfalldiagramm hinzufügen?

Natürlich, Sie können weitere Datenreihen zu Ihrem Wasserfalldiagramm hinzufügen, um **komplexe Datenszenarien** effektiv darzustellen.

### Wo finde ich weitere Ressourcen und Beispiele für Aspose.Cells für Java?

Sie können die Dokumentation für Aspose.Cells für Java unter [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) für ausführliche Informationen und Codebeispiele einsehen.

---

**Zuletzt aktualisiert:** 2025-12-10  
**Getestet mit:** Aspose.Cells für Java 24.12 (neueste)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}