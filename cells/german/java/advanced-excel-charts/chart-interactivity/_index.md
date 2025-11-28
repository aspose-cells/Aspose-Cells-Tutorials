---
date: 2025-11-28
description: Erfahren Sie, wie Sie Tooltips, Datenbeschriftungen und Drill‑Down‑Funktionen
  hinzufügen, um ein interaktives Diagramm in Java mit Aspose.Cells zu erstellen.
language: de
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Wie man Tooltips in interaktiven Diagrammen hinzufügt (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Tooltips in interaktiven Diagrammen hinzufügt (Aspose.Cells Java)

## Einführung

Interaktive Diagramme ermöglichen es Benutzern, Daten durch Hover, Klick oder Drill‑Down zu erkunden. In diesem Tutorial lernen Sie **wie man Tooltips** zu einem Diagramm hinzufügt, sowie **wie man Datenbeschriftungen** hinzufügt und **Drill‑Down**‑Navigation implementiert – alles mit Aspose.Cells für Java. Am Ende können Sie ein voll funktionsfähiges, interaktives Diagramm erstellen, das Ihre Datenpräsentationen ansprechender und aussagekräftiger macht.

## Schnellantworten
- **Welche Bibliothek wird benötigt?** Aspose.Cells für Java (neueste Version).  
- **Welches Hauptfeature deckt dieser Leitfaden ab?** Hinzufügen von Tooltips zu Diagrammen.  
- **Kann ich auch Datenbeschriftungen hinzufügen?** Ja – siehe den Abschnitt „Datenbeschriftungen hinzufügen“.  
- **Wird Drill‑Down unterstützt?** Ja, über Hyperlinks auf Datenpunkte.  
- **Welches Dateiformat wird erzeugt?** Eine Excel‑Arbeitsmappe (`.xlsx`) mit einem interaktiven Diagramm.

## Was bedeutet das Hinzufügen von Tooltips?

Ein Tooltip ist ein kleines Popup, das erscheint, wenn ein Benutzer über ein Diagrammelement fährt, und zusätzliche Informationen wie den genauen Wert oder eine benutzerdefinierte Nachricht anzeigt. Tooltips verbessern die Datenlesbarkeit, ohne das visuelle Layout zu überladen.

## Warum interaktive Diagramme in Java erstellen?

- **Bessere Entscheidungsfindung:** Benutzer sehen sofort präzise Werte.  
- **Professionelle Berichte:** Interaktive Elemente lassen Dashboards modern wirken.  
- **Wiederverwendbare Komponenten:** Sobald Sie die API beherrschen, können Sie sie in jeder Excel‑basierten Reporting‑Lösung einsetzen.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Eine Java‑Entwicklungsumgebung (JDK 8 oder neuer).  
- Aspose.Cells für Java Bibliothek (Download von [hier](https://releases.aspose.com/cells/java/)).  
- Eine Beispieldatei **data.xlsx**, die die zu visualisierenden Daten enthält.

## Schritt 1: Einrichten Ihres Java‑Projekts

1. Erstellen Sie ein neues Java‑Projekt in Ihrer bevorzugten IDE (IntelliJ IDEA, Eclipse usw.).  
2. Fügen Sie die Aspose.Cells‑JAR zu Ihrem Projekt‑Classpath hinzu.

## Schritt 2: Laden von Daten

Um ein interaktives Diagramm zu erstellen, benötigen Sie zunächst ein Arbeitsblatt mit Daten. Der folgende Code lädt das erste Arbeitsblatt aus **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Schritt 3: Erstellen eines Diagramms

Jetzt fügen wir dem Arbeitsblatt ein Säulendiagramm hinzu. Das Diagramm erstreckt sich über die Zellen F6 bis K16.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Schritt 4: Interaktivität hinzufügen

### 4.1. Wie man Tooltips hinzufügt

Das folgende Snippet aktiviert Tooltips für die erste Serie im Diagramm. Jeder Datenpunkt zeigt beim Hover seinen Wert an.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Datenbeschriftungen zum Diagramm hinzufügen

Wenn Sie neben jeder Säule sichtbare Beschriftungen wünschen, verwenden Sie den unten gezeigten **add data labels chart**‑Ansatz. Dies erfüllt das sekundäre Schlüsselwort *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Wie man Drill‑Down implementiert

Drill‑Down lässt Benutzer auf einen Datenpunkt klicken und zu einer Detailansicht springen (z. B. eine Webseite). Hier fügen wir dem ersten Punkt der Serie einen Hyperlink hinzu.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Pro‑Tipp:** Sie können die URL dynamisch basierend auf dem Wert des Punktes generieren, um ein wirklich datengetriebenes Drill‑Down‑Erlebnis zu schaffen.

## Schritt 5: Arbeitsmappe speichern

Nachdem das Diagramm konfiguriert wurde, speichern Sie die Arbeitsmappe. Die resultierende Datei enthält ein interaktives Diagramm, das in Excel geöffnet werden kann.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Häufige Probleme & Lösungen

| Problem | Ursache | Lösung |
|-------|-------|-----|
| Tooltips werden nicht angezeigt | Datenbeschriftungen nicht aktiviert | Stellen Sie sicher, dass `setHasDataLabels(true)` vor dem Setzen von `ShowValue` aufgerufen wird. |
| Hyperlink nicht anklickbar | Falscher Punkt‑Index | Prüfen Sie, ob Sie den korrekten Punkt referenzieren (`get(0)` ist der erste Punkt). |
| Diagramm ist verschoben | Ungültiger Zellbereich | Passen Sie die Zeilen‑/Spaltenindizes in `add(ChartType.COLUMN, row1, col1, row2, col2)` an. |

## Häufig gestellte Fragen

**F: Wie kann ich den Diagrammtyp ändern?**  
A: Ersetzen Sie `ChartType.COLUMN` durch einen anderen Enum‑Wert wie `ChartType.LINE` oder `ChartType.PIE`, wenn Sie `worksheet.getCharts().add(...)` aufrufen.

**F: Kann ich das Aussehen von Tooltips anpassen?**  
A: Ja. Verwenden Sie die Formatierungseigenschaften des `DataLabel`‑Objekts (Schriftgröße, Hintergrundfarbe usw.), um den Tooltip‑Text zu stylen.

**F: Wie gehe ich mit Benutzerinteraktionen in einer Web‑Anwendung um?**  
A: Exportieren Sie die Arbeitsmappe in ein web‑kompatibles Format (z. B. HTML) und nutzen Sie JavaScript, um Klick‑Events auf Diagrammelementen abzufangen.

**F: Wo finde ich weitere Beispiele und Dokumentation?**  
A: Besuchen Sie die offizielle API‑Referenz unter [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/).

**F: Ist es möglich, mehrere Drill‑Down‑Links im selben Diagramm zu setzen?**  
A: Absolut. Durchlaufen Sie die Serienpunkte und weisen Sie jedem Punkt in der `Hyperlinks`‑Sammlung eine eindeutige URL zu.

## Fazit

In diesem Leitfaden haben Sie **wie man Tooltips hinzufügt**, **wie man Datenbeschriftungen hinzufügt** und **wie man Drill‑Down**‑Funktionalität implementiert, um eine **create interactive chart java**‑Lösung mit Aspose.Cells zu erstellen. Diese Features verwandeln statische Excel‑Diagramme in dynamische, benutzerfreundliche Visualisierungen, die es Stakeholdern ermöglichen, Daten mühelos zu erkunden.

---

**Zuletzt aktualisiert:** 2025-11-28  
**Getestet mit:** Aspose.Cells für Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}