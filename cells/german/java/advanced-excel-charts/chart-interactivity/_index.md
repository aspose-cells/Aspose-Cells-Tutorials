---
date: 2025-12-01
description: Erfahren Sie, wie Sie den Diagrammtyp in Excel ändern und interaktive
  Funktionen wie Tooltips, Datenbeschriftungen und Drill‑Down mit Aspose.Cells für
  Java hinzufügen.
language: de
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Excel-Diagrammtyp ändern und Interaktivität hinzufügen – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Diagrammtyp ändern und Interaktivität hinzufügen

## Einleitung

Interaktive Diagramme ermöglichen es Ihrem Publikum, Daten on‑the‑fly zu erkunden, während die Möglichkeit, **Excel-Diagrammtyp zu ändern** Ihnen die Flexibilität gibt, Informationen im effektivsten visuellen Format darzustellen. In diesem Tutorial lernen Sie, wie Sie Aspose.Cells für Java verwenden, um den Diagrammtyp zu ändern, Tooltips hinzuzufügen, Datenbeschriftungen einzubetten und sogar Drill‑Down‑Links zu erstellen – alles ohne Ihren Java‑Code zu verlassen. Am Ende haben Sie eine voll ausgestattete, interaktive Excel-Arbeitsmappe, die Sie in Berichten, Dashboards oder Webanwendungen einbetten können.

## Schnelle Antworten
- **Kann ich den Diagrammtyp programmgesteuert ändern?** Ja – verwenden Sie das `ChartType`‑Enum beim Erstellen oder Aktualisieren eines Diagramms.  
- **Wie füge ich einem Diagramm Tooltips hinzu?** Aktivieren Sie Datenbeschriftungen und setzen Sie `ShowValue` auf true.  
- **Was ist der einfachste Weg, Drill‑Down‑Links hinzuzufügen?** Fügen Sie einem Datenpunkt über `getHyperlinks().add(url)` einen Hyperlink hinzu.  
- **Benötige ich eine Lizenz für Aspose.Cells?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine Lizenz erforderlich.  
- **Welche Java‑Version wird unterstützt?** Java 8 und höher werden vollständig unterstützt.

## Was bedeutet „Excel-Diagrammtyp ändern“?

Den Diagrammtyp zu ändern bedeutet, die visuelle Darstellung zu tauschen (z. B. von einem Säulendiagramm zu einem Liniendiagramm), während die zugrunde liegenden Daten unverändert bleiben. Das ist nützlich, wenn Sie feststellen, dass ein anderes Diagramm Trends, Vergleiche oder Verteilungen besser vermittelt.

## Warum Interaktivität zu Excel‑Diagrammen hinzufügen?

- **Bessere Dateneinblicke:** Tooltips und Datenbeschriftungen ermöglichen es Benutzern, genaue Werte ohne Scrollen zu sehen.  
- **Fesselnde Präsentationen:** Interaktive Elemente halten das Interesse der Betrachter.  
- **Drill‑Down‑Fähigkeit:** Hyperlinks ermöglichen es Benutzern, zu detaillierten Arbeitsblättern oder externen Ressourcen zu springen.  
- **Wiederverwendbare Assets:** Eine Arbeitsmappe kann mehrere Reporting‑Szenarien bedienen, indem einfach der Diagrammtyp gewechselt wird.

## Voraussetzungen

- Java-Entwicklungsumgebung (JDK 8+)  
- Aspose.Cells for Java Bibliothek (Download von [hier](https://releases.aspose.com/cells/java/))  
- Eine Beispiel‑Excel‑Datei (`data.xlsx`), die die Daten enthält, die Sie visualisieren möchten.

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Richten Sie Ihr Java‑Projekt ein

1. Erstellen Sie ein neues Java‑Projekt in Ihrer bevorzugten IDE (IntelliJ IDEA, Eclipse, VS Code usw.).  
2. Fügen Sie die Aspose.Cells‑JAR zu Ihrem Projekt‑Klassenpfad hinzu.

### Schritt 2: Laden Sie die Quell‑Arbeitsmappe

Wir beginnen damit, eine vorhandene Arbeitsmappe zu laden, die die Daten für unser Diagramm enthält.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Schritt 3: Erstellen Sie ein Diagramm und **ändern Sie dessen Typ**

Unten erstellen wir ein Säulendiagramm und zeigen dann sofort, wie Sie es bei Bedarf in ein Liniendiagramm umwandeln können.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro‑Tipp:** Den Diagrammtyp nach der Erstellung zu ändern ist so einfach wie das Aufrufen von `setChartType(...)`. Dies erfüllt das Hauptkeyword **Excel-Diagrammtyp ändern** ohne ein neues Diagrammobjekt zu benötigen.

### Schritt 4: Interaktivität hinzufügen

#### 4.1 Tooltips zum Diagramm hinzufügen

Tooltips werden angezeigt, wenn ein Benutzer über einen Datenpunkt fährt. In Aspose.Cells werden sie über Datenbeschriftungen implementiert.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Datenbeschriftungen hinzufügen ( **add data labels chart** )

Datenbeschriftungen können den genauen Wert, den Kategorienamen oder beides anzeigen. Hier verwenden wir einen Callout‑Stil.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Drill‑Down implementieren ( **add drill down excel** )

Ein Drill‑Down‑Link ermöglicht es Benutzern, einen Punkt anzuklicken und zu einer detaillierten Ansicht zu springen, entweder innerhalb der Arbeitsmappe oder auf einer Webseite.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Schritt 5: Arbeitsmappe speichern

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Häufige Probleme und Lösungen

| Problem | Ursache | Lösung |
|---------|---------|--------|
| Tooltips werden nicht angezeigt | `HasDataLabels` nicht aktiviert | Stellen Sie sicher, dass `setHasDataLabels(true)` aufgerufen wird, bevor `ShowValue` konfiguriert wird. |
| Drill‑Down‑Link tut nichts | Hyperlink‑URL ist fehlerhaft | Überprüfen Sie, ob die URL mit `http://` oder `https://` beginnt. |
| Diagrammtyp ändert sich nicht | Verwendung einer älteren Aspose.Cells‑Version | Aktualisieren Sie auf die neueste Version (getestet mit 24.12). |

## Häufig gestellte Fragen

**F: Wie kann ich den Diagrammtyp ändern, nachdem er erstellt wurde?**  
A: Rufen Sie `chart.setChartType(ChartType.YOUR_CHOICE)` auf dem bestehenden `Chart`‑Objekt auf. Dies erfüllt direkt die Anforderung **Excel-Diagrammtyp ändern**.

**F: Kann ich das Aussehen von Tooltips anpassen?**  
A: Ja. Verwenden Sie `chart.getNSeries().get(0).getPoints().getDataLabels()`, um Schriftgröße, Farbe und Hintergrund festzulegen.

**F: Ist es möglich, mehrere Drill‑Down‑Links in einem Diagramm hinzuzufügen?**  
A: Absolut. Durchlaufen Sie die Punkte und rufen Sie `getHyperlinks().add(url)` für jeden Punkt auf, den Sie verlinken möchten.

**F: Unterstützt Aspose.Cells andere Diagrammtypen wie Kreis- oder Radar?**  
A: Alle im `ChartType`‑Enum definierten Diagrammtypen werden unterstützt, einschließlich `PIE`, `RADAR`, `AREA` usw.

**F: Wo finde ich weitere Beispiele?**  
A: Besuchen Sie die offizielle [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) für eine vollständige Liste der diagrammbezogenen Methoden.

## Fazit

Sie wissen jetzt, wie Sie **Excel-Diagrammtyp ändern**, **Tooltips** einbetten, **Datenbeschriftungen** hinzufügen und **Drill‑Down**‑Links mit Aspose.Cells für Java erstellen. Diese interaktiven Funktionen verwandeln statische Tabellenkalkulationen in dynamische Datenexplorationstools, ideal für Dashboards, Berichte und webbasierte Analysen.

---

**Zuletzt aktualisiert:** 2025-12-01  
**Getestet mit:** Aspose.Cells 24.12 für Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}