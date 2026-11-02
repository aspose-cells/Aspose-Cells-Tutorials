---
category: general
date: 2026-08-08
description: Wie man eine Pivot‑Tabelle in Aspose.Cells kopiert und einen Bereich
  mit Java in eine Arbeitsmappe überträgt. Erfahren Sie die genauen Schritte, um eine
  Pivot‑Tabelle mit CopyOptions zu duplizieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: de
lastmod: 2026-08-08
og_description: Wie man eine Pivot‑Tabelle in Aspose.Cells kopiert und einen Bereich
  mit Java in eine Arbeitsmappe überträgt. Folgen Sie dieser vollständigen Anleitung,
  um eine Pivot‑Tabelle mithilfe von CopyOptions zu duplizieren.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Wie man Pivot in Aspose.Cells kopiert – Bereich in Arbeitsmappe kopieren
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Wie man Pivot in Aspose.Cells kopiert – Bereich in Arbeitsmappe kopieren
url: /de/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot in Aspose.Cells kopiert – Bereich in Arbeitsmappe kopieren

Wenn Sie **wie man Pivot kopiert** in einer Excel‑Datei mit Aspose.Cells benötigen, zeigt Ihnen diese Anleitung den genauen Vorgang. Am Ende des Tutorials können Sie **Bereich in Arbeitsmappe kopieren** durchführen, wobei die Definition der Pivot‑Tabelle erhalten bleibt.

Das Beispiel verwendet Java, aber dieselben Konzepte gelten für jede .NET‑Sprache, die mit Aspose.Cells arbeitet. Es werden keine externen Tools benötigt – nur die Aspose.Cells‑Bibliothek für Java und eine grundlegende Entwicklungsumgebung.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Java Development Kit (JDK) 8 oder höher.
* Maven oder Gradle zur Verwaltung von Abhängigkeiten (das Beispiel verwendet Maven).
* Aspose.Cells for Java 23.9 (oder die neueste Version) zu Ihrem Projekt hinzugefügt.
* Eine Eingabe‑Arbeitsmappe (`input.xlsx`), die mindestens eine Pivot‑Tabelle im ersten Arbeitsblatt enthält.

Wenn diese Elemente bereitstehen, werden Laufzeitfehler vermieden, wenn der Code auf die Arbeitsmappe zugreift.

## Wie man Pivot mit Aspose.Cells kopiert

Dieser Abschnitt führt Sie Schritt für Schritt durch das Vorgehen, um **wie man Pivot kopiert** von einem Teil eines Blatts zu einem anderen zu übertragen, wobei die Klasse `CopyOptions` verwendet wird.

### Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen

Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Warum dieser Schritt wichtig ist*: Die Bibliothek stellt die Klassen `Workbook`, `CopyOptions` und weitere bereit, die für **aspose.cells copy range**‑Operationen erforderlich sind. Ohne die Abhängigkeit kann der Compiler diese Typen nicht auflösen.

### Schritt 2: Die Quell‑Arbeitsmappe laden

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Das Laden der Datei erzeugt eine In‑Memory‑Darstellung der Tabelle. Das `Workbook`‑Objekt gibt Ihnen Zugriff auf Arbeitsblätter, Zellen und Pivot‑Tabellen.

### Schritt 3: Kopieroptionen konfigurieren, um die Pivot‑Tabelle einzuschließen

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` teilt Aspose.Cells mit, dass die Operation die Pivot‑Tabellen‑Metadaten erhalten soll. Wenn Sie dieses Flag weglassen, wird die Pivot‑Tabelle zu statischen Daten reduziert und verliert ihre Interaktivität.

### Schritt 4: Den gewünschten Bereich mit der Pivot‑Tabelle kopieren

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Die Methode `copyRange` kopiert Zellen, Formatierungen und – dank der im vorherigen Schritt gesetzten Optionen – alle Pivot‑Tabellen, die den Bereich berühren. Dies ist das Kernstück der **copy range to workbook**‑Funktionalität.

### Schritt 5: Die geänderte Arbeitsmappe speichern

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Das Speichern schreibt die Änderungen in eine neue Datei (`output.xlsx`). Sie können diese Datei nun in Excel öffnen und sehen, dass die Pivot‑Tabelle exakt dort dupliziert wurde, wo der Bereich kopiert wurde.

## Vollständiges, ausführbares Beispiel

Wenn alle Teile zusammengefügt werden, sieht das komplette Programm, das Sie kompilieren und ausführen können, folgendermaßen aus:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Erwartetes Ergebnis

* `output.xlsx` enthält dieselben Daten wie `input.xlsx`.
* Die Pivot‑Tabelle, die ursprünglich den Quellbereich belegte, erscheint in den Zielzellen und ist vollständig funktionsfähig (Filter, Aktualisierungs‑Möglichkeit usw.).
* Alle Zellformatierungen, Formeln und Spaltenbreiten bleiben erhalten, weil `copyRange` den gesamten Zellblock kopiert.

## Häufige Fragen und Sonderfälle

**Was passiert, wenn sich der Zielbereich mit einer bestehenden Pivot‑Tabelle überschneidet?**  
Aspose.Cells überschreibt die Zielzellen. Um Datenverlust zu vermeiden, stellen Sie sicher, dass der Zielbereich leer ist oder verschieben Sie die vorhandene Pivot‑Tabelle zuerst.

**Kann ich eine Pivot‑Tabelle über Arbeitsblätter hinweg kopieren?**  
Ja. Verwenden Sie `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);`, wobei `targetSheetIndex` auf das Zielarbeitsblatt verweist.

**Kopiert `setCopyPivotTable(true)` die zugrunde liegende Datenquelle?**  
Die Methode kopiert nur die Referenz auf den Pivot‑Cache. Wenn die Quelldaten in derselben Arbeitsmappe liegen, verweist die Ziel‑Pivot‑Tabelle auf denselben Cache. Um den Cache zu duplizieren, müssen Sie einen neuen Pivot‑Cache manuell erstellen.

**Wie kopiere ich einen großen Bereich effizient?**  
Bei sehr großen Bereichen sollten Sie nur `CopyOptions.setCopyFormula(true)` und `setCopyDataValidation(true)` aktivieren, wenn sie wirklich benötigt werden. Das Reduzieren der Optionen kann die Leistung verbessern.

## Tipps für eine zuverlässige **aspose.cells copy range**‑Verwendung

* **Pro‑Tipp:** Rufen Sie nach dem Kopieren stets `workbook.calculateFormula()` auf, wenn der Bereich Formeln enthält, die vom Pivot‑Cache abhängen.
* **Achten Sie auf:** Versteckte Arbeitsblätter. `copyRange` funktioniert nur auf sichtbaren Arbeitsblättern, es sei denn, Sie referenzieren das versteckte Blatt explizit per Index.
* **Versions‑Check:** Das Flag `setCopyPivotTable` ist ab Aspose.Cells 20.9 verfügbar. Stellen Sie sicher, dass Ihre Bibliotheksversion es unterstützt.

## Fazit

Sie wissen jetzt, **wie man Pivot in Aspose.Cells kopiert** und **wie man Bereich in Arbeitsmappe kopiert**, wobei die volle Pivot‑Funktionalität erhalten bleibt. Die Schritte – Bibliothek hinzufügen, Arbeitsmappe laden, `CopyOptions` konfigurieren, den Kopiervorgang ausführen und speichern – bilden ein wiederholbares Muster, das Sie auf andere Kopier‑und‑Einfüge‑Szenarien anwenden können.

Als Nächstes können Sie verwandte Themen wie **aspose.cells copy range** für Diagramme, bedingte Formatierungen und Datenvalidierung erkunden. Experimentieren Sie mit dem Kopieren zwischen verschiedenen Dateiformaten (XLSX → XLS), um Ihre Automatisierungsmöglichkeiten zu erweitern. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Pivot‑Tabellen in Excel mit Aspose.Cells für Java&#58; Ein umfassender Leitfaden](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Wie man die Datenquelle einer Excel‑Pivot‑Tabelle mit Aspose.Cells für Java&#58; Ein umfassender Leitfaden](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Wie man Slicer in Pivot‑Tabellen mit Aspose.Cells für Java&#58; Ein umfassender Leitfaden](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}