---
category: general
date: 2026-09-21
description: Erfahren Sie, wie Sie einen Bereich in Java kopieren und dabei die Pivot‑Tabelle
  erhalten. Diese Schritt‑für‑Schritt‑Anleitung zeigt Ihnen, wie Sie eine Pivot‑Tabelle
  sicher exportieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: de
lastmod: 2026-09-21
og_description: Wie man einen Bereich in Java kopiert und dabei die Pivot‑Tabelle
  beibehält. Folgen Sie dieser vollständigen Anleitung, um Pivot‑Tabellen sicher zu
  exportieren.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Wie man einen Bereich kopiert und eine Pivot‑Tabelle in Java beibehält
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Wie man einen Bereich kopiert und eine Pivot‑Tabelle in Java beibehält
url: /de/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man einen Bereich kopiert und eine Pivot‑Tabelle in Java beibehält

Wenn Sie **how to copy range** benötigen, das eine Pivot‑Tabelle enthält, zeigt Ihnen dieser Leitfaden einen zuverlässigen Weg, die Pivot‑Tabelle intakt zu halten. Viele Entwickler haben Schwierigkeiten, die Pivot‑Tabelle zu verlieren, wenn sie Daten exportieren, aber der untenstehende Ansatz ermöglicht es Ihnen, **copy pivot table**‑Daten zu kopieren, ohne die Funktionalität zu beeinträchtigen. Am Ende dieses Tutorials können Sie die Struktur der **preserve pivot table** beibehalten, **export pivot table**‑Dateien erstellen und **how to preserve pivot** in verschiedenen Szenarien verstehen.

Das Beispiel verwendet Aspose.Cells for Java, eine beliebte Bibliothek für die Excel‑Automatisierung. Es wird kein zusätzliches Werkzeug benötigt, außer einer Standard‑Java‑Entwicklungsumgebung.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Java 17 (oder neuer) installiert.
* Maven oder Gradle zur Verwaltung von Abhängigkeiten.
* Aspose.Cells for Java (Version 23.9 oder neuer). Fügen Sie die folgende Maven‑Abhängigkeit hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Eine Quellarbeitsmappe (`Source.xlsx`), die die Pivot‑Tabelle enthält, die Sie kopieren möchten.

## Wie man einen Bereich kopiert und die Pivot‑Tabelle intakt hält

Die Kernidee besteht darin, den **range** zu kopieren, der die gesamte Pivot‑Tabelle einschließlich ihrer Datenquelle umfasst, mittels `copyRange`. Diese Methode kopiert sowohl die Rohdaten als auch die Pivot‑Definition und stellt sicher, dass die Zielarbeitsmappe eine voll funktionsfähige Pivot‑Tabelle erhält.

### Schritt 1: Quellarbeitsmappe laden

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Warum dieser Schritt?*  
Das Laden der Arbeitsmappe gibt Ihnen Zugriff auf das Arbeitsblatt, das die Pivot‑Tabelle enthält. Die Klasse `Workbook` abstrahiert die gesamte Excel‑Datei, während `Worksheet` Zell‑Operationen bereitstellt.

### Schritt 2: Den Bereich definieren, der die Pivot‑Tabelle abdeckt

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Warum dieser Schritt?*  
Eine Pivot‑Tabelle ist nicht nur eine einzelne Zelle; sie erstreckt sich über einen Block, der Kopfzeilen, Datenzeilen und den Pivot‑Cache umfasst. Durch die Angabe eines Bereichs, der die Pivot‑Tabelle vollständig enthält, stellen Sie sicher, dass `copyRange` auch den zugrunde liegenden Cache kopiert, was für das Verhalten von **preserve pivot table** entscheidend ist.

### Schritt 3: Eine leere Zielarbeitsmappe erstellen

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Warum dieser Schritt?*  
Der Start mit einer leeren Arbeitsmappe verhindert versehentliche Konflikte mit vorhandenen Tabellenblättern oder benannten Bereichen. Die Zielarbeitsmappe erhält den kopierten Bereich und exportiert damit effektiv **export pivot table**‑Inhalte.

### Schritt 4: Den Bereich kopieren – die Pivot‑Tabelle bleibt erhalten

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Warum dieser Schritt?*  
`copyRange` führt eine Tiefenkopie durch: Zellwerte, Formatierungen und Pivot‑Metadaten werden übertragen. Dies ist die kritische Operation, die **copy pivot table** ermöglicht, ohne die Funktionalität zu verlieren. Das Objekt `CellArea` definiert, wo der Bereich im Zielblatt landet.

### Schritt 5: Zielarbeitsmappe speichern

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Warum dieser Schritt?*  
Das Speichern finalisiert den **export pivot table**‑Prozess. Die resultierende Datei (`DestWithPivot.xlsx`) enthält eine voll funktionsfähige Pivot‑Tabelle, die Sie in Excel, Google Sheets oder einem anderen Tabellenkalkulations‑Viewer öffnen können.

## Überprüfen, ob die Pivot‑Tabelle erhalten blieb

Öffnen Sie `DestWithPivot.xlsx` in Excel und prüfen Sie Folgendes:

1. Die Pivot‑Tabelle erscheint an derselben Position (A1:G20) wie in der Quelle.
2. Das Aktualisieren der Pivot‑Tabelle aktualisiert die Daten korrekt, was beweist, dass der Cache kopiert wurde.
3. Alle Formatierungen (Spaltenbreiten, Zahlenformate) entsprechen dem Original.

Falls einer dieser Checks fehlschlägt, überprüfen Sie, ob der Quellbereich die Pivot‑Tabelle und ihre Datenquelle vollständig umschließt. Ein häufiger Fehler ist die Auswahl eines Bereichs, der den Daten‑Cache nicht vollständig einschließt, was zu einer defekten Pivot‑Tabelle führt.

## Zusätzliche Überlegungen

### Pivot‑Tabelle über verschiedene Arbeitsmappen‑Versionen kopieren

Aspose.Cells unterstützt sowohl ältere `.xls`‑Dateien als auch das neuere `.xlsx`‑Format. Der gleiche Code funktioniert unabhängig von der Dateierweiterung und stellt eine universelle Lösung für **how to preserve pivot** über verschiedene Versionen hinweg dar.

### Pivot‑Tabelle beim Einsatz einer gefilterten Quelle erhalten

Wenn die Quell‑Pivot‑Tabelle gefiltert ist, wird der Filterzustand ebenfalls kopiert. Sollten Sie die Filter im Ziel zurücksetzen müssen, rufen Sie nach dem Kopieren `PivotTable.refreshData()` auf:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Pivot‑Tabelle als statischen Schnappschuss exportieren

Manchmal möchten Sie eine statische Kopie (nur Werte) statt einer Live‑Pivot‑Tabelle. Ersetzen Sie `copyRange` durch `copyRange` gefolgt von `pt.setEnableRefresh(false)`, um weitere Berechnungen zu deaktivieren.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Umgang mit großen Arbeitsmappen

Bei Arbeitsmappen mit vielen Arbeitsblättern begrenzen Sie die Kopier‑Operation auf das jeweilige Blatt, um den Speicherverbrauch zu reduzieren. Verwenden Sie `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, um die Leistung fein abzustimmen.

## Vollständiges ausführbares Beispiel

Unten finden Sie das vollständige Programm, das Sie kopieren, einfügen und ausführen können. Passen Sie die Dateipfade an Ihre Umgebung an.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Erwartete Ausgabe**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Wenn Sie `DestWithPivot.xlsx` öffnen, sollten Sie die originale Pivot‑Tabelle voll funktionsfähig sehen, was bestätigt, dass Sie erfolgreich **how to copy range** durchgeführt haben, während Sie die **preserve pivot table** beibehalten haben.

## Häufige Stolperfallen und Pro‑Tipps

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Pivot erscheint, zeigt aber `#REF!`‑Fehler | Der kopierte Bereich ließ das versteckte Cache‑Blatt aus | Erweitern Sie den Quellbereich, um den gesamten Cache einzuschließen (in der Regel die Zeilen unterhalb der Pivot‑Tabelle) |
| Zielarbeitsmappe ist größer als erwartet | `copyRange` kopiert auch Formatierungen | Verwenden Sie `CopyOptions`, um Formatierungen auszuschließen, falls die Größe ein Problem darstellt |
| Aktualisierung schlägt mit „Datenquelle nicht gefunden“ fehl | Quellarbeitsmappe nutzte externe Datenverbindungen | Replizieren Sie die Verbindung im Ziel oder kopieren Sie zuerst das Datenquellen‑Blatt |

**Pro‑Tipp:** Führen Sie nach dem Kopieren immer eine schnelle Prüfung `destWs.getPivotTables().size()` durch. Wenn die Anzahl Null ist, hat der Bereich die Pivot‑Definition nicht enthalten und Sie müssen ihn erweitern.

## Fazit

In diesem Tutorial haben wir gezeigt, wie man **how to copy range** durchführt, das eine Pivot‑Tabelle enthält, und garantiert, dass das Verhalten von **preserve pivot table** intakt bleibt. Durch das Laden der Quellarbeitsmappe, das Definieren eines umfassenden Bereichs, die Verwendung von `copyRange` und das Speichern der Zieldatei können Sie zuverlässig **export pivot table**‑Daten exportieren und die Frage **how to preserve pivot** in Java‑Projekten beantworten.

Weitere Schritte, die Sie erkunden könnten, umfassen:

* Die Automatisierung des Kopierens für mehrere Tabellenblätter (verwenden Sie das sekundäre Schlüsselwort **copy pivot table** in einer Schleife).
* Das konvertieren der exportierten Arbeitsmappe in CSV, während Rohdaten erhalten bleiben (immer noch **preserve pivot table**‑Logik für die Quelle).

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}