---
date: 2025-12-06
description: Erfahren Sie, wie Sie Datenreihen hinzufügen, kombinierte Diagrammtypen
  erstellen, die Excel-Arbeitsmappe speichern und das Diagramm mit Aspose.Cells für
  Java als PNG exportieren.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Datenreihen hinzufügen, um ein kombiniertes Diagramm mit Aspose.Cells zu erstellen
url: /de/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Datenreihen hinzufügen, um ein kombiniertes Diagramm mit Aspose.Cells zu erstellen

In diesem Tutorial **fügen Sie Datenreihen** zu einer Excel‑Arbeitsmappe hinzu und lernen, wie Sie **kombinierte Diagramm**‑Typen mit Aspose.Cells für Java **erstellen**. Wir gehen jeden Schritt durch – vom Einrichten der Arbeitsmappe, Hinzufügen von Reihen, Anpassen der Legende, bis zum **Speichern der Excel‑Arbeitsmappe** und dem Export des **Diagramms nach PNG**. Am Ende haben Sie ein einsatzbereites kombiniertes Diagramm, das Sie in Berichten oder Dashboards einbetten können.

## Schnellantworten
- **Welche Bibliothek erstellt kombinierte Diagramme?** Aspose.Cells für Java  
- **Wie füge ich eine Datenreihe hinzu?** Verwenden Sie `chart.getNSeries().add(...)`  
- **Kann ich das Diagramm als Bild exportieren?** Ja, mit `chart.toImage(...)` (PNG)  
- **In welchem Dateiformat kann ich die Arbeitsmappe speichern?** Standard‑`.xlsx` (Excel)  
- **Benötige ich eine Lizenz für die Produktion?** Eine gültige Aspose.Cells‑Lizenz ist erforderlich  

## Was bedeutet **Datenreihe hinzufügen** in Aspose.Cells?
Das Hinzufügen einer Datenreihe teilt dem Diagramm mit, welche Zellen die Werte enthalten, die Sie darstellen möchten. Jede Reihe kann eine Linie, Säule oder einen anderen Diagrammtyp repräsentieren, und Sie können sie mischen, um ein **kombiniertes Diagramm** zu erstellen.

## Warum ein **kombiniertes Diagramm** erstellen?
Ein kombiniertes Diagramm ermöglicht es, unterschiedliche Datensätze mit verschiedenen visuellen Darstellungen (z. B. eine Linienreihe über einer Säulereihe) in einer einzigen Ansicht anzuzeigen. Das ist ideal, um Trends gegenüber Gesamtsummen zu vergleichen, Korrelationen hervorzuheben oder reichhaltigere Erkenntnisse kompakt zu präsentieren.

## Voraussetzungen
- Java Development Kit (JDK) 8 oder höher  
- Aspose.Cells für Java‑Bibliothek (Download über den untenstehenden Link)  
- Grundkenntnisse in Java‑Syntax und Excel‑Konzepten  

## Erste Schritte

Laden Sie zunächst die Aspose.Cells für Java‑Bibliothek von der offiziellen Website herunter:

[Aspose.Cells für Java herunterladen](https://releases.aspose.com/cells/java/)

Nachdem die JAR‑Datei zu Ihrem Projekt‑Classpath hinzugefügt wurde, können Sie mit dem Aufbau des Diagramms beginnen.

### Schritt 1: Aspose.Cells‑Klassen importieren
```java
import com.aspose.cells.*;
```

### Schritt 2: Eine neue Arbeitsmappe erstellen
```java
Workbook workbook = new Workbook();
```

### Schritt 3: Auf das erste Arbeitsblatt zugreifen
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Schritt 4: Ein kombiniertes Diagramm‑Objekt hinzufügen  
Wir beginnen mit einem Liniendiagramm und fügen später weitere Reihen hinzu, um den **kombinierten Diagramm**‑Effekt zu erzielen.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Daten zum Diagramm hinzufügen

Jetzt, wo der Diagramm‑Container existiert, müssen wir ihn mit Daten füttern.

### Schritt 5: Datenbereiche definieren und **Datenreihe hinzufügen**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Profi‑Tipp:** Der erste Parameter (`"A1:A5"`) ist der Bereich für die erste Reihe, und der zweite (`"B1:B5"`) erzeugt eine zweite Reihe, die mit der ersten kombiniert wird.

### Schritt 6: Kategoriedaten (X‑Achse) festlegen
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Diagramm anpassen

Ein gutes Diagramm erzählt eine Geschichte. Geben wir ihm Titel, Achsenbeschriftungen und eine klare Legende.

### Schritt 7: Diagrammtitel und Achsenbeschriftungen setzen
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Schritt 8: **Legende zum Diagramm hinzufügen** und Position anpassen
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Arbeitsmappe speichern und Diagramm exportieren

Nach den Anpassungen möchten Sie die **Excel‑Arbeitsmappe speichern** und zudem ein Bild erzeugen.

### Schritt 9: Die Arbeitsmappe als Excel‑Datei speichern
```java
workbook.save("CombinedChart.xlsx");
```

### Schritt 10: **Diagramm nach PNG** exportieren
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Die Methode `chart.toImage` **erzeugt Excel‑Diagrammbilder**, die in Webseiten, Berichten oder E‑Mails verwendet werden können.

## Häufige Probleme & Fehlerbehebung

| Problem | Lösung |
|---------|--------|
| **Keine Daten sichtbar** | Stellen Sie sicher, dass die Zellbereiche (`A1:A5`, `B1:B5`, `C1:C5`) tatsächlich Daten enthalten, bevor Sie das Diagramm erstellen. |
| **Legende überlappt Diagramm** | Setzen Sie `chart.getLegend().setOverlay(false)` oder verschieben Sie die Legende an eine andere Position (z. B. `RIGHT`). |
| **Bilddatei ist leer** | Vergewissern Sie sich, dass das Diagramm mindestens eine Reihe enthält und dass `chart.toImage` nach allen Anpassungen aufgerufen wird. |
| **Speichern wirft eine Ausnahme** | Prüfen Sie, ob Sie Schreibrechte für das Zielverzeichnis besitzen und ob die Datei nicht bereits in Excel geöffnet ist. |

## Häufig gestellte Fragen

**F: Wie installiere ich Aspose.Cells für Java?**  
A: Laden Sie die JAR‑Datei von der offiziellen Website herunter und fügen Sie sie Ihrem Projekt‑Classpath hinzu. Der Download‑Link lautet: [Aspose.Cells für Java herunterladen](https://releases.aspose.com/cells/java/).

**F: Kann ich neben Linien‑ und Säulendiagrammen auch andere Diagrammtypen erstellen?**  
A: Ja, Aspose.Cells unterstützt Balken-, Kreis-, Streu‑, Flächen‑ und viele weitere Diagrammtypen. Siehe die API‑Dokumentation für die vollständige Liste.

**F: Wird für den Produktionseinsatz eine Lizenz benötigt?**  
A: Für den produktiven Einsatz ist eine gültige Aspose.Cells‑Lizenz erforderlich. Eine kostenlose Testversion ist für Evaluierungszwecke verfügbar.

**F: Wie kann ich die Farben jeder Reihe ändern?**  
A: Verwenden Sie `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (oder ähnlich) nach dem Hinzufügen der Reihen.

**F: Wo finde ich weitere Code‑Beispiele?**  
A: Umfangreiche Dokumentation und zusätzliche Beispiele stehen auf der Aspose‑Referenzseite zur Verfügung: [hier](https://reference.aspose.com/cells/java/).

---

**Zuletzt aktualisiert:** 2025-12-06  
**Getestet mit:** Aspose.Cells für Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
