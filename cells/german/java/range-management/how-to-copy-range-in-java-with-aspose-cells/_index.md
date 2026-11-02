---
category: general
date: 2026-09-08
description: Wie man einen Bereich in Java mit Aspose.Cells kopiert – lernen Sie,
  Pivot‑Tabellen zu kopieren, Pivot‑Tabellen zu duplizieren und Pivot‑Tabellen zu
  exportieren, wobei die Formatierung erhalten bleibt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: de
lastmod: 2026-09-08
og_description: Wie man einen Bereich in Java mit Aspose.Cells kopiert. Dieses Tutorial
  zeigt Ihnen, wie Sie eine Pivot‑Tabelle kopieren, eine Pivot‑Tabelle duplizieren
  und eine Pivot‑Tabelle exportieren, wobei die Formatierung erhalten bleibt.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Wie man einen Bereich in Java kopiert – vollständiger Aspose.Cells-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Wie man einen Bereich in Java mit Aspose.Cells kopiert
url: /de/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man einen Bereich in Java mit Aspose.Cells kopiert

Wenn Sie **wie man einen Bereich kopiert** in Java benötigen, macht Aspose.Cells die Aufgabe unkompliziert. Egal, ob Sie einen regulären Zellblock oder eine voll ausgestattete Pivot‑Tabelle verschieben, die Bibliothek übernimmt den Kopiervorgang und behält Formeln, Stile und Pivot‑Cache bei. In diesem Leitfaden lernen Sie, **Pivot‑Tabelle kopieren**, **Pivot‑Tabelle duplizieren** und sogar **Pivot‑Tabelle exportieren** in eine neue Arbeitsmappe mit voller Formatierung.

Das Tutorial deckt alles von der Projekt‑Einrichtung bis zum abschließenden Verifizierungsschritt ab, sodass Sie den Code sofort nach dem Lesen ausführen können. Keine externen Tools sind erforderlich, außer dem Aspose.Cells for Java JAR.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- Java 17 (oder ein unterstütztes JDK) installiert und in Ihrer IDE konfiguriert.
- Maven oder Gradle für das Dependency‑Management (die Beispiele verwenden Maven).
- Eine Quell‑Excel‑Datei (`source.xlsx`), die eine Pivot‑Tabelle im Bereich `A1:H20` enthält.
- Grundlegende Kenntnisse in Java‑Programmierung.

## Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen

Aspose.Cells ist eine kommerzielle Bibliothek, aber eine kostenlose Evaluierungsversion ist verfügbar. Fügen Sie die Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Profi‑Tipp:** Wenn Sie Gradle bevorzugen, lautet der entsprechende Eintrag:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Durch das Hinzufügen des JAR erhalten Sie Zugriff auf die Klassen `Workbook`, `Worksheet`, `Range` und `CopyOptions`, die in diesem Leitfaden verwendet werden.

## Schritt 2: Die Quell‑Arbeitsmappe laden und das erste Arbeitsblatt auswählen

Der erste Teil von **wie man einen Bereich kopiert** besteht darin, die Arbeitsmappe zu öffnen, die die zu verschiebenden Daten enthält.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Warum das wichtig ist:** Das Öffnen der Arbeitsmappe erzeugt eine In‑Memory‑Repräsentation, die die API manipulieren kann, ohne die Originaldatei auf der Festplatte zu berühren.

## Schritt 3: Den Bereich definieren, der die Pivot‑Tabelle enthält

Eine Pivot‑Tabelle befindet sich innerhalb eines rechteckigen Blocks. Sie müssen diesen Block angeben, damit Aspose.Cells weiß, was kopiert werden soll.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Hinweis:** Die Methode `createRange` kopiert noch nichts; sie erstellt lediglich ein `Range`‑Objekt, das auf die Zellen zeigt, die Sie duplizieren möchten.

## Schritt 4: Eine neue Arbeitsmappe erstellen und ihr erstes Arbeitsblatt holen

Erstellen Sie nun die Ziel‑Arbeitsmappe, in der der kopierte Bereich abgelegt wird.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Warum ein neues Arbeitsbuch?** Die Verwendung einer frischen Datei garantiert, dass keine versteckten Stile oder benannten Bereiche den Kopiervorgang beeinträchtigen, was besonders wichtig ist, wenn Sie **Pivot‑Tabelle exportieren** in eine separate Datei.

## Schritt 5: Den Bereich (inklusive der Pivot‑Tabelle) in das Ziel‑Blatt kopieren

Dies ist der Kern von **wie man einen Bereich mit Formatierung kopiert**. Das `CopyOptions`‑Objekt weist Aspose.Cells an, alles zu erhalten: Werte, Formeln, Stile und Pivot‑Cache.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Pivot‑Tabelle kopieren:** Da der Quell‑Bereich die Pivot‑Tabelle enthält, dupliziert die API automatisch den Pivot‑Cache, sodass das neue Arbeitsblatt eine voll funktionsfähige Pivot‑Tabelle enthält, die sich exakt wie das Original verhält.

## Schritt 6: Die Ziel‑Arbeitsmappe speichern

Schließlich schreiben Sie das Ergebnis auf die Festplatte.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Wenn Sie `dest.xlsx` öffnen, sehen Sie eine exakte Kopie der ursprünglichen Pivot‑Tabelle, inklusive ihrer Formatierung, Slicer und berechneten Felder.

## Erwartete Ausgabe

- `dest.xlsx` enthält ein Arbeitsblatt mit dem Namen **Sheet1**.
- Die Zellen `A1:H20` enthalten dieselben Daten und dieselbe Pivot‑Tabelle wie die Quelle.
- Alle Zellstile (Schriftarten, Farben, Rahmen) bleiben erhalten.
- Die Pivot‑Tabelle ist vollständig interaktiv; ein Aktualisieren spiegelt die zugrunde liegenden Daten im kopierten Bereich wider.

## Wie man einen Bereich mit Formatierung kopiert – tieferer Einblick

Das vorherige Beispiel zeigt das einfachste Szenario, aber Sie können auf Varianten stoßen, die einen leicht anderen Ansatz erfordern.

### Pivot‑Tabelle in ein vorhandenes Arbeitsbuch kopieren

Wenn Sie **Pivot‑Tabelle duplizieren** in einer Arbeitsmappe, die bereits Daten enthält, verwenden Sie denselben `copyRange`‑Aufruf, aber verweisen Sie auf eine andere Zieladresse:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Nur Pivot‑Tabelle exportieren (ohne umgebende Daten)

Manchmal möchten Sie nur die Pivot‑Tabelle, nicht die Quelldaten. Ermitteln Sie den Anzeigebereich der Pivot‑Tabelle über die Methode `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Bedingte Formatierung beibehalten

Bedingte Formatierungsregeln sind Teil der Stilsammlung. Das Flag `PasteType.ALL` kopiert sie bereits, Sie können es jedoch explizit angeben:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Randfälle und Fehlersuche

| Situation | Worauf zu achten ist | Empfohlene Lösung |
|-----------|----------------------|-------------------|
| Quell‑ und Ziel‑Arbeitsmappen verwenden unterschiedliche Excel‑Versionen | Einige neuere Pivot‑Funktionen (z. B. Datenmodell) werden möglicherweise nicht korrekt dargestellt | Verwenden Sie die neueste Aspose.Cells‑Version und setzen Sie `Workbook.setFileFormatType(FileFormatType.XLSX)` für beide Arbeitsmappen |
| Sehr große Pivot‑Tabellen ( > 10 000 Zeilen) verursachen Speicherbelastung | Out‑of‑Memory‑Fehler während des Kopierens | Aktivieren Sie `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` vor dem Laden |
| Ziel‑Blatt enthält bereits einen benannten Bereich mit demselben Namen wie die Quelle | Namenskollision führt zu einem Fehler von `CopyOptions` | Rufen Sie `copyOptions.setIgnoreNameConflicts(true)` auf |

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie in eine Java‑Klasse kopieren‑und‑einfügen können. Es enthält alle Importe, Fehlerbehandlung und Kommentare.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Führen Sie das Programm aus und öffnen Sie anschließend `dest.xlsx`, um zu prüfen, dass die Pivot‑Tabelle exakt wie das Original funktioniert.

## Fazit

Sie wissen jetzt, **wie man einen Bereich** in Java mit Aspose.Cells kopiert, einschließlich **Pivot‑Tabelle kopieren**, **Pivot‑Tabelle duplizieren** und **Pivot‑Tabelle exportieren**, wobei sämtliche Formatierung erhalten bleibt. Die Bibliothek abstrahiert die Low‑Level‑Details der Excel‑XML‑Struktur, sodass Sie sich auf die Geschäftslogik konzentrieren können.

### Nächste Schritte

- Erkunden Sie **Bereich mit Formatierung kopieren** für Diagramme und Bilder (verwenden Sie `PasteType.PICTURES`).
- Automatisieren Sie die Batch‑Verarbeitung: Schleifen Sie über mehrere Quelldateien und konsolidieren Sie deren Pivot‑Tabellen in einer Zusammenfassungs‑Arbeitsmappe.
- Kombinieren Sie diese Technik mit Aspose.Slides, um PowerPoint‑Berichte zu erzeugen, die die kopierte Pivot‑Tabelle einbetten.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man die Excel‑Pivot‑Tabellenquelle mit Aspose.Cells für Java aktualisiert: Ein umfassender Leitfaden](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Pivot‑Tabellen‑Laden in Java mit Aspose.Cells optimieren – Ein umfassender Leitfaden](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Wie man Pivot‑Tabellen in C# kopiert – Excel nach PPTX konvertieren, Bereich kopieren & Textfeld erstellen](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}