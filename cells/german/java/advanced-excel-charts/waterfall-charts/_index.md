---
date: 2026-02-16
description: Erfahren Sie, wie Sie den Datenbereich eines Diagramms festlegen und
  ein Wasserfalldiagramm in Java mit Aspose.Cells erstellen. Schritt‑für‑Schritt‑Anleitung
  zum Hinzufügen eines Datenreihen‑Diagramms, Anpassen und Exportieren nach XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Diagrammdatenbereich festlegen – Aspose.Cells für Java Wasserfalldiagramm
url: /de/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wasserfalldiagramme

## Einführung in Wasserfalldiagramme mit Aspose.Cells für Java

In diesem Tutorial lernen Sie, wie Sie **den Diagrammdatenbereich festlegen** und ein **Wasserfalldiagramm** mit Aspose.Cells für Java erstellen. Wasserfalldiagramme sind ein unverzichtbares Werkzeug in der Datenvisualisierung, weil sie die kumulative Wirkung einer Reihe von positiven und negativen Werten zeigen. Egal, ob Sie einen Finanzbericht, einen Vertriebsleistungsbericht oder eine andere datenbasierte Analyse vorbereiten – ein Wasserfalldiagramm kann Rohdaten in klare, umsetzbare Erkenntnisse verwandeln.

## Schnellantworten
- **Was ist ein Wasserfalldiagramm?** Eine Visualisierung, die zeigt, wie ein Anfangswert durch eine Reihe von Zwischenschritten erhöht und verringert wird und schließlich zu einem Endwert führt.  
- **Welche Bibliothek wird verwendet?** Aspose.Cells für Java.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Entwicklung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Datei als XLSX speichern?** Ja – verwenden Sie `workbook.save("FileName.xlsx")`.  
- **Eignet es sich für die Java‑Datenvisualisierung?** Absolut; Aspose.Cells bietet umfangreiche Diagrammfunktionen ohne installierte Office‑Software.

## Was ist ein Wasserfalldiagramm?
Ein Wasserfalldiagramm zeigt sequenzielle positive und negative Beiträge zu einem Ausgangswert und hilft Ihnen zu verstehen, wie jede Komponente das Gesamtergebnis beeinflusst.

## Warum Aspose.Cells für Java verwenden, um ein Wasserfalldiagramm hinzuzufügen?
- **Kein Microsoft Excel erforderlich** – Diagramme können auf jedem Server oder in jeder CI‑Pipeline erzeugt werden.  
- **Volle Kontrolle über das Layout** – Farben, Datenbeschriftungen und Achsen können programmgesteuert angepasst werden.  
- **Unterstützt mehrere Ausgabeformate** – XLSX, PDF, HTML und mehr.  
- **Hohe Leistung** – ideal für große Arbeitsmappen und automatisierte Berichte.

## Voraussetzungen

Bevor wir in den Code eintauchen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Aspose.Cells für Java: Sie benötigen Aspose.Cells für Java. Sie können es von [hier](https://releases.aspose.com/cells/java/) herunterladen.

- Java‑Entwicklungsumgebung: Stellen Sie sicher, dass Java auf Ihrem System installiert ist.

Jetzt können wir Schritt für Schritt das Wasserfalldiagramm erstellen.

## Wie man den Diagrammdatenbereich für ein Wasserfalldiagramm in Java festlegt

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

Erzeugen Sie eine neue Arbeitsmappe und fügen Sie ein Arbeitsblatt hinzu. Dieses Arbeitsblatt verwenden wir, um unsere Daten einzugeben und **ein Diagramm zum Arbeitsblatt hinzuzufügen**.

### Schritt 3: Daten eingeben

Jetzt füllen wir das Arbeitsblatt mit den Daten, die wir im Wasserfalldiagramm darstellen wollen.

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

In diesem Beispiel befinden sich die Kategorien in Spalte A und die zugehörigen Werte in Spalte B. Sie können diese Daten durch Ihren eigenen Datensatz ersetzen.

### Schritt 4: Das Wasserfalldiagramm erstellen

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Wir haben ein Wasserfalldiagramm zu unserem Arbeitsblatt hinzugefügt, die Datenreihe und die Kategoriedaten angegeben. Dies ist der zentrale Schritt, der **ein Wasserfalldiagramm** zu Ihrem Blatt **hinzufügt**. Beachten Sie, dass die `add`‑Methode den Bereich `"B2:B6"` verwendet – hier **setzen wir den Diagrammdatenbereich** für die Reihe. Sie können das Aussehen des Diagramms (Farben, Datenbeschriftungen usw.) über die Eigenschaften des `Chart`‑Objekts weiter anpassen.

### Schritt 5: Die Arbeitsmappe speichern

```java
workbook.save("WaterfallChart.xlsx");
```

Speichern Sie die Arbeitsmappe in einer Datei. Das Beispiel verwendet das XLSX‑Format, aber Aspose.Cells ermöglicht Ihnen auch das **export excel pdf java**‑kompatible Dateien wie PDF, CSV und viele weitere Formate zu erzeugen. Damit ist die Anforderung **save workbook xlsx** erfüllt.

## Häufige Probleme und Lösungen

- **Diagramm erscheint leer** – Prüfen Sie, ob die Datenbereichsreferenzen (`B2:B6` und `A2:A6`) mit den tatsächlichen Zellen übereinstimmen, die Ihre Werte und Kategorien enthalten.  
- **Negative Werte werden nicht korrekt angezeigt** – Stellen Sie sicher, dass der Diagrammtyp auf `ChartType.WATERFALL` gesetzt ist; andere Diagrammtypen behandeln Negative anders.  
- **Datei lässt sich nicht in Excel öffnen** – Vergewissern Sie sich, dass Sie eine aktuelle Version von Aspose.Cells (die neueste Veröffentlichung) verwenden und dass die Dateierweiterung zum Format passt (`.xlsx` für Excel).

## Häufig gestellte Fragen

### Wie kann ich das Aussehen meines Wasserfalldiagramms anpassen?

Sie können das Aussehen Ihres Wasserfalldiagramms ändern, indem Sie Eigenschaften wie Farben, Datenbeschriftungen und Achsenbeschriftungen modifizieren. Weitere Details finden Sie in der Aspose.Cells‑Dokumentation.

### Kann ich mehrere Wasserfalldiagramme im selben Arbeitsblatt erstellen?

Ja, Sie können mehrere Wasserfalldiagramme im selben Arbeitsblatt erzeugen, indem Sie dieselben Schritte mit unterschiedlichen Datenbereichen wiederholen.

### Ist Aspose.Cells mit verschiedenen Java‑Entwicklungsumgebungen kompatibel?

Ja, Aspose.Cells für Java ist mit verschiedenen Java‑Entwicklungsumgebungen kompatibel, einschließlich Eclipse, IntelliJ IDEA und NetBeans.

### Kann ich weitere Datenreihen zu meinem Wasserfalldiagramm hinzufügen?

Natürlich, Sie können weitere Datenreihen zu Ihrem Wasserfalldiagramm hinzufügen, um komplexe Datenszenarien effektiv darzustellen. Dies ist ein Beispiel, wie Sie **add data series chart** programmgesteuert **hinzufügen** können.

### Wo finde ich weitere Ressourcen und Beispiele für Aspose.Cells für Java?

Sie können die Dokumentation für Aspose.Cells für Java unter [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) für ausführliche Informationen und Code‑Beispiele durchsuchen.

## FAQ

**F: Wie lege ich den Diagrammdatenbereich für ein finanzielles Wasserfalldiagramm fest?**  
A: Verwenden Sie die `add`‑Methode der Diagrammreihe und übergeben Sie den Zellbereich, der Ihre Werte enthält, z. B. `"B2:B6"`.

**F: Kann ich die Arbeitsmappe statt als XLSX als PDF exportieren?**  
A: Ja, rufen Sie `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` auf, um **export excel pdf java**‑kompatiblen Output zu erzeugen.

**F: Was, wenn ich ein finanzielles Wasserfalldiagramm mit mehr Kategorien erstellen muss?**  
A: Erweitern Sie den Datenbereich sowohl in der Wertespalte als auch in der Kategoriespalte und passen Sie die Aufrufe von `add` und `setCategoryData` entsprechend an.

**F: Gibt es eine Möglichkeit, positive und negative Balken automatisch zu formatieren?**  
A: Sie können die `Series`‑Sammlung durchlaufen und das `FillFormat`‑Farbe basierend auf dem Vorzeichen jedes Wertes setzen.

**F: Unterstützt Aspose.Cells dynamische Datenaktualisierungen für Diagramme?**  
A: Ja, Sie können Zellwerte nach der Diagrammerstellung ändern; das Diagramm spiegelt die Änderungen beim Speichern der Arbeitsmappe wider.

---

**Zuletzt aktualisiert:** 2026-02-16  
**Getestet mit:** Aspose.Cells für Java (neueste)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}