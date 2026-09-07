---
date: 2026-02-14
description: Erfahren Sie, wie Sie ein Diagramm als PNG exportieren, Datenreihen hinzufügen,
  ein Linien‑Säulendiagramm kombinieren, die Arbeitsmappe als XLSX speichern und eine
  Legende zum Diagramm hinzufügen, indem Sie Aspose.Cells für Java verwenden.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Diagramm nach PNG exportieren und Datenreihen für kombiniertes Diagramm hinzufügen
url: /de/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm als PNG exportieren und Datenreihen für kombiniertes Diagramm hinzufügen

In diesem Tutorial werden Sie **Datenreihen** zu einer Excel‑Arbeitsmappe **hinzufügen**, **Linien‑ und Säulendiagramm**‑Elemente **kombinieren** und lernen, wie man **Diagramm als PNG exportiert** mit Aspose.Cells for Java. Wir gehen jeden Schritt durch – vom Einrichten der Arbeitsmappe, dem Hinzufügen des Diagramms zu einem Arbeitsblatt, dem Anpassen der Legende, bis zum **Speichern der Arbeitsmappe als xlsx** und dem Erzeugen eines PNG‑Bildes des Diagramms. Am Ende haben Sie ein einsatzbereites kombiniertes Diagramm, das Sie in Berichte oder Dashboards einbetten können.

## Schnelle Antworten
- **Welche Bibliothek erstellt kombinierte Diagramme?** Aspose.Cells for Java  
- **Wie füge ich eine Datenreihe hinzu?** Use `chart.getNSeries().add(...)`  
- **Wie kann ich das Diagramm als PNG exportieren?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **In welchem Dateiformat kann ich die Arbeitsmappe speichern?** Standard `.xlsx` (save workbook as xlsx)  
- **Benötige ich eine Lizenz für die Produktion?** A valid Aspose.Cells license is required  

## Was ist **export chart to PNG** in Aspose.Cells?
Das Exportieren eines Diagramms als PNG erzeugt ein Rasterbild des Excel‑Diagramms, das in Webseiten, Berichten oder E‑Mails angezeigt werden kann, ohne dass die Excel‑Anwendung erforderlich ist.

## Warum ein **combined line column chart** erstellen?
Ein kombiniertes Diagramm ermöglicht es, verschiedene Datensätze mit unterschiedlichen visuellen Darstellungen (z. B. eine Linienreihe über einer Säulereihe) in einer einzigen Ansicht darzustellen. Das ist ideal, um Trends mit Gesamtsummen zu vergleichen, Korrelationen hervorzuheben oder reichhaltigere Erkenntnisse in einem kompakten Format zu liefern.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder höher  
- Aspose.Cells for Java Bibliothek (Download über den untenstehenden Link)  
- Grundlegende Kenntnisse der Java‑Syntax und Excel‑Konzepte  

## Erste Schritte

Laden Sie zunächst die Aspose.Cells for Java Bibliothek von der offiziellen Website herunter:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Sobald das JAR zu Ihrem Projekt‑Classpath hinzugefügt wurde, können Sie mit dem Erstellen des Diagramms beginnen.

### Schritt 1: Aspose.Cells‑Klassen importieren
```java
import com.aspose.cells.*;
```

### Schritt 2: Eine neue Arbeitsmappe erstellen
```java
Workbook workbook = new Workbook();
```

### Schritt 3: Auf das erste Arbeitsblatt zugreifen
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Schritt 4: Kombiniertes Diagramm‑Objekt zum Arbeitsblatt hinzufügen  
Wir beginnen mit einem Liniendiagramm und fügen später eine Säulereihe hinzu, um einen **combined line column chart**‑Effekt zu erzielen.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Daten zum Diagramm hinzufügen

Da der Diagramm‑Container jetzt existiert, müssen wir ihn mit Daten füttern.

### Schritt 5: Datenbereiche definieren und **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro Tipp:** Der erste Parameter (`"A1:A5"`) ist der Bereich für die erste Reihe, und der zweite (`"B1:B5"`) erzeugt eine zweite Reihe, die mit der ersten kombiniert wird.

### Schritt 6: Kategoriedaten (X‑Achse) festlegen
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Diagramm anpassen

Ein gutes Diagramm erzählt eine Geschichte. Geben wir ihm Titel, Achsenbeschriftungen und eine klare Legende.

### Schritt 7: **Set chart axis labels** und Titel
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Schritt 8: **Add legend chart** und Position anpassen
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Diagramm speichern und exportieren

Nach der Anpassung möchten Sie **save workbook as xlsx** und zudem ein Bild erzeugen.

### Schritt 9: Die Arbeitsmappe als Excel‑Datei (xlsx) speichern
```java
workbook.save("CombinedChart.xlsx");
```

### Schritt 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Die Methode `chart.toImage` **generates excel chart** Bilder, die in Webseiten, Berichten oder E‑Mails verwendet werden können.

## Häufige Probleme & Fehlerbehebung

| Problem | Lösung |
|-------|----------|
| **Keine Daten angezeigt** | Stellen Sie sicher, dass die Zellbereiche (`A1:A5`, `B1:B5`, `C1:C5`) tatsächlich Daten enthalten, bevor Sie das Diagramm erstellen. |
| **Legende überlappt Diagramm** | Setzen Sie `chart.getLegend().setOverlay(false)` oder verschieben Sie die Legende an eine andere Position (z. B. `RIGHT`). |
| **Bilddatei ist leer** | Stellen Sie sicher, dass das Diagramm mindestens eine Reihe enthält und dass `chart.toImage` nach allen Anpassungen aufgerufen wird. |
| **Speichern wirft eine Ausnahme** | Prüfen Sie, ob Sie Schreibrechte für das Zielverzeichnis haben und ob die Datei nicht in Excel geöffnet ist. |

## Häufig gestellte Fragen

**Q: Wie installiere ich Aspose.Cells for Java?**  
A: Laden Sie das JAR von der offiziellen Website herunter und fügen Sie es dem Klassenpfad Ihres Projekts hinzu. Der Download‑Link ist: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kann ich andere Diagrammtypen außer Linie und Säule erstellen?**  
A: Ja, Aspose.Cells unterstützt Balken-, Kreis-, Streu‑, Flächen‑ und viele weitere Diagrammtypen. Siehe die API‑Dokumentation für die vollständige Liste.

**Q: Ist eine Lizenz für den Produktionseinsatz erforderlich?**  
A: Eine gültige Aspose.Cells‑Lizenz ist für den Produktionseinsatz erforderlich. Eine kostenlose Testversion steht zur Evaluierung bereit.

**Q: Wie kann ich die Farben jeder Reihe ändern?**  
A: Verwenden Sie `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (oder Ähnliches) nach dem Hinzufügen der Reihen.

**Q: Wo finde ich weitere Code‑Beispiele?**  
A: Umfassende Dokumentation und weitere Beispiele sind auf der Aspose‑Referenzseite verfügbar: [hier](https://reference.aspose.com/cells/java/).

---

**Zuletzt aktualisiert:** 2026-02-14  
**Getestet mit:** Aspose.Cells for Java neueste Version  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}