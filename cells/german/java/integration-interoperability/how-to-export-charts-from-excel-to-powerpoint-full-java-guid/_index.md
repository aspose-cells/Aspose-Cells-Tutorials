---
category: general
date: 2026-06-27
description: Wie man Diagramme aus Excel mit Java nach PowerPoint exportiert. Lernen
  Sie, Tabellenkalkulationen in PowerPoint zu konvertieren, PPTX‑Dateien zu speichern
  und Excel‑Daten mühelos nach PPT zu exportieren.
draft: false
keywords:
- how to export charts
- convert spreadsheet to powerpoint
- how to save pptx
- excel to powerpoint slide
- export excel data ppt
language: de
og_description: Wie man Diagramme aus Excel nach PowerPoint in Java exportiert. Diese
  Schritt‑für‑Schritt‑Anleitung zeigt Ihnen, wie Sie eine Tabelle nach PowerPoint
  konvertieren, PPTX‑Dateien speichern und Excel‑Daten nach PPT exportieren.
og_title: Wie man Diagramme von Excel nach PowerPoint exportiert – Java‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  headline: How to Export Charts from Excel to PowerPoint – Full Java Guide
  type: TechArticle
- description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  name: How to Export Charts from Excel to PowerPoint – Full Java Guide
  steps:
  - name: '**Load** the workbook you want to transform.'
    text: '**Load** the workbook you want to transform.'
  - name: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
    text: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
  - name: '**Save** the workbook using the `PPTX` format and the options you configured.'
    text: '**Save** the workbook using the `PPTX` format and the options you configured.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
title: Wie man Diagramme von Excel nach PowerPoint exportiert – Vollständiger Java‑Leitfaden
url: /de/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Diagramme von Excel nach PowerPoint exportiert – Vollständiger Java‑Leitfaden

Haben Sie sich jemals gefragt, **wie man Diagramme** aus einer Excel‑Arbeitsmappe direkt in eine PowerPoint‑Folien­seite exportiert? Sie sind nicht allein – Entwickler müssen häufig datengetriebene Tabellenkalkulationen in präsentationsfertige Decks umwandeln, ohne das lästige Kopieren‑und‑Einfügen. In diesem Tutorial führen wir Sie durch eine saubere, programmatische Lösung, mit der Sie **Spreadsheet zu PowerPoint konvertieren**, das Ergebnis als PPTX speichern und sogar die Diagramm‑Verarbeitung zur Laufzeit feinjustieren können.

Am Ende haben Sie ein sofort einsatzbereites Java‑Snippet, das jede Arbeitsmappe nimmt, ihre Diagramme (und OLE‑Objekte, falls gewünscht) extrahiert und eine polierte **excel to powerpoint slide**‑Datei ausgibt. Keine zusätzliche UI, kein umständliches VBA, nur reiner Java‑Code, den Sie noch heute in Ihr Projekt einbinden können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- **Java 17** oder neuer (die API funktioniert mit jedem aktuellen JDK)
- **Aspose.Cells for Java**‑Bibliothek (der Code verwendet `PresentationOptions` und `SaveFormat.PPTX`)
- Grundlegendes Verständnis von Java‑Projekt‑Setups (Maven/Gradle)
- Eine Excel‑Datei (`.xlsx`), die mindestens ein Diagramm enthält, das Sie exportieren möchten

Falls Ihnen das Aspose.Cells‑JAR fehlt, fügen Sie es via Maven hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Oder laden Sie das JAR direkt von der Aspose‑Website herunter und legen Sie es in Ihren Klassenpfad.

## Wie man Diagramme exportiert – Überblick

Auf hoher Ebene sieht der Prozess so aus:

1. **Laden** Sie die Arbeitsmappe, die Sie transformieren möchten.
2. **Konfigurieren** Sie eine `PresentationOptions`‑Instanz, um Aspose mitzuteilen, welche Elemente (Diagramme, OLE‑Objekte usw.) in das Folien‑Deck aufgenommen werden sollen.
3. **Speichern** Sie die Arbeitsmappe im `PPTX`‑Format mit den konfigurierten Optionen.

Das war’s. Die Bibliothek übernimmt die schwere Arbeit – jedes Diagramm wird als Vektorgrafik gerendert, das Layout bleibt erhalten und es wird eine PowerPoint‑Datei erzeugt, die PowerPoint selbst ohne Probleme öffnen kann.

Im Folgenden zerlegen wir jeden Schritt, erklären *warum* er wichtig ist und zeigen den genauen Code, den Sie benötigen.

## Schritt 1: Laden der Arbeitsmappe und Konfigurieren der Export‑Optionen

Zuerst müssen wir Aspose mitteilen, was beim Erstellen der PowerPoint‑Datei eingeschlossen werden soll. Die Klasse `PresentationOptions` bietet feinkörnige Kontrolle. Das Setzen von `setExportCharts(true)` sorgt dafür, dass jedes Diagramm zu einem Folienelement wird, während `setExportOleObjects(true)` eingebettete Objekte (wie Excel‑Tabellen) mit einbezieht.

```java
import com.aspose.cells.*;

public class ExcelToPowerPointExporter {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source Excel workbook
        // -------------------------------------------------
        String srcPath = "C:/data/sourceWorkbook.xlsx";
        Workbook workbook = new Workbook(srcPath);

        // -------------------------------------------------
        // 2️⃣ Configure presentation export options
        // -------------------------------------------------
        PresentationOptions presentationOptions = new PresentationOptions();
        presentationOptions.setExportCharts(true);          // <-- how to export charts
        presentationOptions.setExportOleObjects(true);     // include embedded OLE objects

        // The next lines are optional but often useful:
        presentationOptions.setExportFormulas(false);      // skip raw formulas if you only need visuals
        presentationOptions.setExportImages(true);         // grab any pictures as well
```

**Warum dieser Schritt wichtig ist:**  
Wenn Sie `setExportCharts(true)` weglassen, behandelt Aspose Diagramme wie normale Zellen und gibt deren Daten in die Folie aus, anstatt ein visuelles Diagramm zu erzeugen. Das verfehlt den Zweck einer Präsentation. Ebenso ermöglicht das Umschalten des OLE‑Exports, komplexe Objekte (wie Pivot‑Tabellen) ohne zusätzlichen Code beizubehalten.

> **Pro‑Tipp:** Bei sehr großen Arbeitsmappen sollten Sie `setExportFormulas` deaktivieren, um die Konvertierung zu beschleunigen. Das visuelle Ergebnis bleibt gleich, aber der Vorgang ist speicherschonender.

## Schritt 2: Speichern der Arbeitsmappe als PowerPoint‑Datei

Jetzt, wo die Optionen bereitstehen, besteht die eigentliche Konvertierung aus einer einzigen Zeile: Aufruf von `workbook.save(...)` mit dem Enum `SaveFormat.PPTX`. Hier beantworten wir **wie man pptx in Java speichert**.

```java
        // -------------------------------------------------
        // 3️⃣ Save the workbook as a PowerPoint file
        // -------------------------------------------------
        String outPath = "C:/output/slide.pptx";
        workbook.save(outPath, SaveFormat.PPTX, presentationOptions);

        System.out.println("✅ Conversion complete! Check " + outPath);
    }
}
```

**Was im Hintergrund passiert:**  
Aspose iteriert über jedes Arbeitsblatt, extrahiert jedes Diagramm, konvertiert es in eine PowerPoint‑Form (meist ein EMF‑Vektor) und platziert es auf einer neuen Folie. Wenn Sie mehrere Arbeitsblätter haben, erhält jedes standardmäßig eine eigene Folie. Sie können die Folien später mit Apache POI oder PowerPoint selbst umordnen.

### Erwartetes Ergebnis

Öffnen Sie `slide.pptx` in Microsoft PowerPoint, und Sie sollten sehen:

- Eine Folie pro Arbeitsblatt (oder pro Diagramm, je nach Quelle)
- Scharf gerenderte Diagramme, die Farben und Datenbeschriftungen beibehalten
- Alle OLE‑Objekte (wie eingebettete Excel‑Tabellen) erscheinen als editierbare Objekte

Falls kein Diagramm angezeigt wird, prüfen Sie, ob die Quell‑Arbeitsmappe tatsächlich ein Diagramm‑Objekt enthält und `setExportCharts(true)` nicht an anderer Stelle überschrieben wird.

## Alternative: Export eines einzelnen Diagramms in ein eigenständiges PPTX

Manchmal benötigen Sie nur **excel to powerpoint slide** für ein bestimmtes Diagramm, nicht die gesamte Arbeitsmappe. Das erreichen Sie, indem Sie eine temporäre Arbeitsmappe erstellen, die nur das gewünschte Diagramm enthält.

```java
        // -------------------------------------------------
        // 4️⃣ Export a single chart (optional)
        // -------------------------------------------------
        // Assume the chart is on the first worksheet, first chart
        Worksheet sheet = workbook.getWorksheets().get(0);
        int chartIndex = 0; // change if you have multiple charts
        Chart chart = sheet.getCharts().get(chartIndex);

        // Clone the chart into a new workbook
        Workbook singleChartWb = new Workbook();
        Worksheet newSheet = singleChartWb.getWorksheets().get(0);
        newSheet.getCharts().addCopy(chart);

        // Use the same PresentationOptions
        singleChartWb.save("C:/output/singleChart.pptx", SaveFormat.PPTX, presentationOptions);
```

**Warum Sie das wollen könnten:**  
Wenn Sie ein Folien‑Deck on‑the‑fly erzeugen (z. B. einen Reporting‑Service, der pro E‑Mail ein Diagramm sendet), reduziert ein minimales Arbeitsblatt den Speicherverbrauch und beschleunigt den Vorgang.

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Symptom | Lösung |
|---------|---------|--------|
| Diagramme verschwinden | Folien sind leer oder enthalten nur Datentabellen | Stellen Sie sicher, dass `presentationOptions.setExportCharts(true)` **vor** `workbook.save` aufgerufen wird. |
| Große Dateigröße | PPTX > 30 MB für wenige Diagramme | Deaktivieren Sie den Bild‑Export (`setExportImages(false)`) oder komprimieren Sie Bilder in PowerPoint nach der Erstellung. |
| Fehlende OLE‑Objekte | Eingebettete Excel‑Tabellen werden zu statischen Bildern | Setzen Sie `setExportOleObjects(true)`; prüfen Sie zudem, dass die Quell‑OLE‑Objekte nicht geschützt sind. |
| Kompatibilitätsfehler | PowerPoint meldet, die Datei sei beschädigt | Verwenden Sie die neueste Aspose.Cells‑Version; ältere Versionen können Bugs bei der PPTX‑Erstellung haben. |

## Diagramme in einer CI/CD‑Pipeline exportieren

Wenn Sie die Berichtserstellung als Teil eines Builds automatisieren, können Sie den obigen Code in ein Maven‑Plugin oder einen Gradle‑Task einbetten. Achten Sie nur darauf, dass die JVM genug Heap hat (z. B. `-Xmx2g`), wenn Sie riesige Arbeitsmappen verarbeiten.

```groovy
task exportCharts(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = 'com.example.ExcelToPowerPointExporter'
    args = []
    jvmArgs = ['-Xmx2g']
}
```

Der Aufruf `./gradlew exportCharts` erzeugt das PPTX ohne manuelles Eingreifen – ideal für nächtliche Reporting‑Jobs.

## Vollständiges, lauffähiges Beispiel (Copy‑Paste‑bereit)

Unten finden Sie die komplette, eigenständige Java‑Klasse, die Sie in jede IDE einfügen können. Sie enthält alle Importe, Fehlerbehandlung und Kommentare, die jede Zeile erklären.

```java
// FullExample.java
import com.aspose.cells.*;

public class FullExample {
    public static void main(String[] args) {
        try {
            // 👉 1️⃣ Load the Excel workbook you want to convert
            String srcFile = "C:/data/analysis.xlsx";
            Workbook wb = new Workbook(srcFile);

            // 👉 2️⃣ Set up export options – this is the core of how to export charts
            PresentationOptions opts = new PresentationOptions();
            opts.setExportCharts(true);          // include every chart
            opts.setExportOleObjects(true);     // keep OLE objects (tables, etc.)
            opts.setExportImages(true);         // optionally keep pictures
            opts.setExportFormulas(false);      // skip formulas for speed

            // 👉 3️⃣ Choose where the PPTX will be saved – answer to how to save pptx
            String outFile = "C:/output/analysis.pptx";

            // 👉 4️⃣ Perform the conversion
            wb.save(outFile, SaveFormat.PPTX, opts);

            System.out.println("✅ Excel file converted to PowerPoint successfully!");
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

Führen Sie die Klasse aus, öffnen Sie `analysis.pptx`, und Sie sehen jedes Diagramm Ihrer ursprünglichen Tabelle nun glücklich in einem PowerPoint‑Deck. Das ist das Wesentliche von **export excel data ppt** – keine manuellen Schritte, keine Kopier‑und‑Einfüge‑Fehler.

## Visuelle Zusammenfassung

![Diagramm, das zeigt, wie Diagramme von Excel nach PowerPoint mit Aspose.Cells exportiert werden](/images/export-charts-diagram.png "Wie man Diagramme von Excel nach PowerPoint exportiert")

*Die obige Abbildung stellt den Ablauf von einer Excel‑Arbeitsmappe → PresentationOptions → PPTX‑Datei dar.*

## Fazit

Wir haben **wie man Diagramme** von Excel nach PowerPoint mit Java exportiert, den genauen Code gezeigt, den Sie benötigen, um **Spreadsheet zu PowerPoint zu konvertieren**, und erklärt, **wie man pptx** zuverlässig speichert. Durch Anpassen von `PresentationOptions` können Sie alles steuern – von der Diagrammeinbindung bis zum OLE‑Objekt‑Handling – und erhalten eine flexible Brücke zwischen Datenanalyse und Präsentationsschicht.

Nächste Schritte? Kombinieren Sie diese Konvertierung mit **Apache POI**, um Folien programmgesteuert neu anzuordnen, oder betten Sie die Routine in einen Spring‑Boot‑Microservice ein, der PPTX‑Reports on‑demand bereitstellt. Sie können auch das Exportieren nach **PDF** oder **HTML** mit derselben Bibliothek erkunden – Aspose.Cells macht das unkompliziert.

Haben Sie Fragen zu Randfällen,

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Wie man Diagramme in Java mit Aspose.Cells erstellt und exportiert : Ein vollständiger Leitfaden](/cells/english/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Wie man Excel‑Diagramme als SVG mit Aspose.Cells Java für skalierbare Vektorgrafiken exportiert](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Excel‑Diagramme nach PDF exportieren mit Aspose.Cells für Java : Leitfaden für benutzerdefinierte Seitengrößen](/cells/english/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}