---
category: general
date: 2026-07-06
description: Wie man Pivot‑Tabellen in Java mit Aspose.Cells kopiert – Schritt‑für‑Schritt‑Anleitung
  zum programmgesteuerten Duplizieren von Excel‑Pivot‑Tabellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: de
lastmod: 2026-07-06
og_description: Wie man Pivot‑Tabellen in Java mit Aspose.Cells kopiert, lässt Sie
  Excel‑Pivot‑Tabellen schnell und zuverlässig duplizieren.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Wie man Pivot-Tabellen in Java kopiert – Vollständiger Aspose.Cells-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Wie man Pivot‑Tabellen in Java mit Aspose.Cells kopiert
url: /de/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot‑Tabellen in Java mit Aspose.Cells kopiert

Haben Sie sich jemals gefragt, **wie man Pivot**‑Tabellen in einer Excel‑Datei kopiert, ohne die Arbeitsmappe manuell zu öffnen? Sie sind nicht allein. In vielen Reporting‑Pipelines müssen Sie **Excel‑Pivot**‑Tabellen on‑the‑fly duplizieren – vielleicht um einen Schnappschuss zu erstellen, sie in ein neues Blatt zu verschieben oder eine Vorlage für nachgelagerte Benutzer zu erzeugen.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das genau das zeigt. Mit der Aspose.Cells‑Bibliothek für Java laden wir eine Arbeitsmappe, ermitteln den Quell‑Pivot‑Bereich, kopieren ihn an einen neuen Ort und speichern das Ergebnis. Keine vagen Verweise, sondern eine konkrete Lösung, die Sie noch heute in Ihr Projekt übernehmen können.

---

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

* **Java Development Kit (JDK) 8+** – der Code kompiliert mit jedem aktuellen JDK.
* **Aspose.Cells for Java** Version 25.11 oder neuer – die `Range.copy`‑Methode, die Pivot‑Tabellen unterstützt, wurde in diesem Release eingeführt.
* Eine **input.xlsx**‑Datei, die bereits eine Pivot‑Tabelle enthält (Sie können zum Testen eine in Excel erstellen).
* Ein Build‑Tool Ihrer Wahl (Maven, Gradle oder reines `javac`). Wir zeigen die Maven‑Abhängigkeit für den schnellen Einstieg.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Schritt 1: Laden der Quell‑Arbeitsmappe

Das Erste, was wir tun, ist die Excel‑Datei zu öffnen, die die ursprüngliche Pivot‑Tabelle enthält. Aspose.Cells behandelt die Arbeitsmappe als In‑Memory‑Objekt, sodass Sie sie manipulieren können, ohne Excel zu starten.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Warum das wichtig ist:** Das Laden der Arbeitsmappe gibt uns Zugriff auf Arbeitsblätter, Zellen und, entscheidend, den Pivot‑Cache, der die Pivot‑Tabelle unterstützt. Ohne diesen Schritt hat die Bibliothek nichts zu kopieren.

---

## Schritt 2: Das Arbeitsblatt mit dem Pivot ermitteln

Falls Ihre Arbeitsmappe mehrere Blätter enthält, müssen Sie das richtige auswählen. Hier holen wir uns einfach das erste Blatt, Sie können aber auch `get("SheetName")` für eine benannte Suche verwenden.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro‑Tipp:** Wenn Sie mit vielen Blättern arbeiten, speichern Sie den Index oder Namen in einer Konfigurationsdatei, um hartkodierte Zahlen zu vermeiden.

---

## Schritt 3: Den Quell‑Bereich definieren, der die Pivot‑Tabelle enthält

Ab Version 25.11 erlaubt Aspose.Cells, eine Pivot‑Tabelle wie einen normalen Zellbereich zu behandeln. Geben Sie die Zelle oben‑links und unten‑rechts an, die die gesamte Pivot‑Tabelle umschließen.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Randfall:** Wenn sich Ihre Pivot‑Tabelle dynamisch erweitert (z. B. später Zeilen hinzugefügt werden), verwenden Sie `worksheet.getPivotTables().get(0).getDataRange()`, um den genauen Bereich programmgesteuert zu ermitteln.

---

## Schritt 4: Den Ziel‑Bereich festlegen, in den die Pivot‑Tabelle kopiert werden soll

Wählen Sie eine leere Zelle, an der die duplizierte Pivot‑Tabelle erscheinen soll. In diesem Demo‑Beispiel beginnen wir bei **F1**, sodass zwischen Original und Kopie ein Abstand entsteht.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Warum nicht ein neues Blatt?** Sie können auch ein frisches Arbeitsblatt erstellen (`workbook.getWorksheets().add("Copy")`) und dessen Zellen als Ziel verwenden. Die gleiche `copy`‑Methode funktioniert bereichsübergreifend.

---

## Schritt 5: Die Pivot‑Tabelle an den neuen Ort kopieren

Jetzt passiert die Magie. Die `copy`‑Methode klont die Pivot, ihren Cache, das Format und sogar zugehörige Slicer (seit der neuesten Version).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Wichtig:** Der Kopiervorgang ist *tief*; er erzeugt **keine** Referenz zurück zur ursprünglichen Pivot. Sie können die neue Pivot unabhängig vom Original ändern, ohne das Quell‑Objekt zu beeinflussen.

---

## Schritt 6: Die Arbeitsmappe mit der duplizierten Pivot speichern

Abschließend schreiben wir die modifizierte Arbeitsmappe zurück auf die Festplatte. Sie können die Originaldatei überschreiben oder eine neue Datei erzeugen; hier wählen wir Letzteres, um das Original unverändert zu lassen.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Wenn Sie **output.xlsx** in Excel öffnen, sehen Sie die ursprüngliche Pivot in den Spalten A‑D und eine perfekte Kopie, beginnend bei Spalte F. Beide Pivot‑Tabellen können separat aktualisiert werden.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier die komplette Java‑Klasse, die Sie direkt kompilieren und ausführen können:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Erwartetes Ergebnis:** Beim Öffnen von `output.xlsx` wird die ursprüngliche Pivot (A1:D20) und eine identische Pivot, beginnend bei F1, angezeigt. Beide Tabellen behalten ihre Filter, Stile und berechneten Felder bei.

---

## Umgang mit gängigen Varianten

| Situation | Was anzupassen |
|-----------|----------------|
| **Mehrere Pivots** im selben Blatt | Durchlaufen Sie `worksheet.getPivotTables()` und kopieren Sie jede mit einem eigenen Zielbereich. |
| **Dynamischer Datenbereich** | Verwenden Sie `worksheet.getPivotTables().get(0).getDataRange()`, um den Quellbereich automatisch zu ermitteln. |
| **Kopieren in eine andere Arbeitsmappe** | Laden Sie eine zweite `Workbook`‑Instanz, erstellen Sie ein Ziel‑Arbeitsblatt und rufen Sie `sourceRange.copy(destWorksheet.getCells().createRange("A1"))` auf. |
| **Slicer erhalten** | Ab Version 25.12 werden Slicer automatisch kopiert, wenn der Bereich sie einschließt. Prüfen Sie nach dem Speichern in Excel. |

---

## Pro‑Tipps & Stolperfallen

* **Versions‑Check:** Die `copy`‑Methode, die Pivot‑Tabellen unterstützt, wurde in **Aspose.Cells 25.11** eingeführt. Bei einer älteren Version erhalten Sie eine Ausnahme. Überprüfen Sie stets die `aspose-cells`‑Version in Ihrer `pom.xml`.
* **Performance:** Das Kopieren großer Pivots kann speicherintensiv sein. Wenn Sie nur die Daten benötigen, exportieren Sie die Pivot lieber in eine flache Tabelle, anstatt das gesamte Objekt zu klonen.
* **Aktualisierungs‑Verhalten:** Die duplizierte Pivot behält ihren eigenen Cache. Wenn Sie die zugrunde liegenden Daten ändern, rufen Sie `pivotTable.refresh()` auf der neuen Pivot auf, um sie neu zu berechnen.
* **Formatierungs‑Eigenheiten:** Einige benutzerdefinierte Zahlenformate überleben den Kopiervorgang nicht in sehr alten Excel‑Versionen (<2007). Testen Sie mit der Excel‑Version Ihrer Zielgruppe.

---

## Fazit

Sie haben nun eine solide, durchgängige Lösung, **wie man Pivot‑Tabellen** mit Aspose.Cells für Java kopiert, und gesehen, **wie man Excel‑Pivot‑Tabellen** in wenigen Code‑Zeilen dupliziert. Der Ansatz funktioniert für einzelne oder mehrere Pivots, über Arbeitsblätter hinweg und sogar zwischen Arbeitsmappen.

Nächste Schritte könnten sein:

* Die Kopie für jede Pivot in einem Batch‑Job automatisieren.
* Code hinzufügen, um die duplizierte Pivot umzubenennen (z. B. `pivotTable.setName("Copy_of_Sales")`).
* Die Routine in einen größeren Reporting‑Service integrieren, der PDFs oder CSV‑Exporte erzeugt.

Probieren Sie es aus, passen Sie die Bereiche an Ihre realen Daten an und lassen Sie die Bibliothek die schwere Arbeit übernehmen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}