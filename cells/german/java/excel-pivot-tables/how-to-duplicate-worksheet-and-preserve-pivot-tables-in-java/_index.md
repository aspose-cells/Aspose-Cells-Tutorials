---
category: general
date: 2026-08-17
description: Wie man ein Arbeitsblatt in Java mit Aspose.Cells dupliziert, die Pivot‑Tabelle
  beibehält, die Pivot‑Tabelle in eine neue Arbeitsmappe kopiert und eine Arbeitsmappe
  aus einem Blatt erstellt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: de
lastmod: 2026-08-17
og_description: Wie man ein Arbeitsblatt in Java mit Aspose.Cells dupliziert, die
  Pivot‑Tabelle beibehält, die Pivot‑Tabelle in eine neue Arbeitsmappe kopiert und
  eine Arbeitsmappe aus einem Blatt erstellt – alle Schritte erklärt.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Wie man ein Arbeitsblatt dupliziert und Pivot‑Tabellen beibehält – Java‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Wie man ein Arbeitsblatt dupliziert und Pivot-Tabellen in Java beibehält
url: /de/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Arbeitsblatt dupliziert und Pivot‑Tabellen in Java beibehält

Ein Arbeitsblatt zu duplizieren und dabei die Pivot‑Tabelle unverändert zu lassen, ist ein häufiges Bedürfnis, wenn Sie Excel‑Berichte automatisieren. Dieser Leitfaden zeigt Ihnen, wie Sie eine Pivot‑Tabelle in eine neue Arbeitsmappe mit Aspose.Cells für Java kopieren und erklärt außerdem, wie Sie die Pivot‑Tabelle beibehalten, wenn Sie eine Arbeitsmappe aus einem Blatt erstellen.

Sie lernen, wie Sie eine vorhandene Arbeitsmappe laden, das Arbeitsblatt, das eine Pivot‑Tabelle enthält, duplizieren und das Ergebnis als neue Datei speichern. Das Tutorial geht davon aus, dass Sie eine grundlegende Java‑Entwicklungsumgebung und eine gültige Aspose.Cells‑Lizenz besitzen (die kostenlose Evaluation funktioniert zum Testen). Keine externen Werkzeuge sind über das Aspose.Cells‑JAR hinaus erforderlich.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Java Development Kit (JDK) 8 oder neuer.
* Maven oder Gradle zur Verwaltung der Aspose.Cells‑Abhängigkeit.
* Eine Excel‑Datei (`source.xlsx`), die mindestens eine Pivot‑Tabelle im ersten Arbeitsblatt enthält.
* Ein Verzeichnis, in dem Sie die Quelldatei lesen und die duplizierte Arbeitsmappe schreiben können.

Fügen Sie die Aspose.Cells‑Abhängigkeit zu Ihrer `pom.xml` (Maven) oder `build.gradle` (Gradle) hinzu. Für Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Wie man ein Arbeitsblatt mit einer Pivot‑Tabelle dupliziert

Der Kernvorgang besteht aus einem dreistufigen Prozess: Laden, Kopieren und Speichern. Jeder Schritt wird unten erklärt.

### Schritt 1 – Laden der Arbeitsmappe, die die Pivot‑Tabelle enthält

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Warum dieser Schritt wichtig ist*: Das `Workbook`‑Objekt repräsentiert die gesamte Excel‑Datei. Durch das Abrufen des ersten Arbeitsblatts (`get(0)`) adressieren Sie das Blatt, das die Pivot‑Tabelle enthält, die Sie duplizieren möchten.

### Schritt 2 – Erstellen einer neuen Arbeitsmappe und Duplizieren des gesamten Arbeitsblatts

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` klont das Arbeitsblatt **einschließlich** aller eingebetteten Objekte, Formeln und Pivot‑Caches. Dies ist der empfohlene Weg, **wie man Pivot kopiert**, weil die Pivot‑Definition und ihre Datenquelle zusammen übertragen werden.

### Schritt 3 – Speichern der neuen Arbeitsmappe

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Nach der Ausführung enthält `copy_with_pivot.xlsx` eine exakte Kopie des Originalblatts, und die Pivot‑Tabelle funktioniert ohne zusätzliche Konfiguration.

**Erwartetes Ergebnis**: Das Öffnen von `copy_with_pivot.xlsx` in Excel zeigt das duplizierte Arbeitsblatt mit derselben Pivot‑Anordnung, denselben Filtern und berechneten Feldern wie die Quelldatei.

## Wie man eine Pivot‑Tabelle in eine andere Arbeitsmappe kopiert

Wenn Sie eine Pivot‑Tabelle verschieben möchten, ohne das gesamte Blatt zu kopieren, können Sie den Pivot‑Cache extrahieren und an ein neues Arbeitsblatt anhängen. Das folgende Snippet demonstriert diesen Ansatz:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Dieser Code beantwortet **wie man Pivot kopiert**, indem nur das Pivot‑Objekt und nicht das gesamte Arbeitsblatt kopiert wird. Die Methode `addCopy` in der `PivotTables`‑Sammlung sorgt dafür, dass der Pivot‑Cache dupliziert wird, was die Anforderungen **wie man Pivot beibehält** erfüllt.

## Wie man Pivot beibehält, wenn man eine Arbeitsmappe aus einem Blatt erstellt

Manchmal beginnen Sie mit einem Blatt, das nicht zu einer Arbeitsmappe gehört (z. B. erzeugen Sie ein Blatt im Speicher). Um **eine Arbeitsmappe aus einem Blatt zu erstellen** und dabei die Pivot‑Tabelle zu erhalten, folgen Sie diesen Schritten:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Indem Sie das Arbeitsblatt nach vollständiger Definition der Pivot‑Tabelle zu einer frischen `Workbook`‑Instanz hinzufügen, stellen Sie sicher, dass **wie man Pivot beibehält** funktioniert, selbst wenn das Arbeitsblatt außerhalb einer bestehenden Datei entstanden ist.

## Praktische Tipps und häufige Fallstricke

| Tipp | Warum er wichtig ist |
|-----|----------------------|
| Verwenden Sie `addCopy` statt `copy` | `addCopy` klont den zugrunde liegenden Pivot‑Cache; ein einfaches `copy` kann die Verbindung zur Datenquelle verlieren. |
| Halten Sie Quell‑ und Ziel‑Dateien im selben Dateisystem | Relative Pfade in der Datenquelle der Pivot‑Tabelle werden korrekt aufgelöst, wodurch „source not found“-Fehler reduziert werden. |
| Überprüfen Sie den Pivot‑Cache nach dem Kopieren | Rufen Sie `pivot.refresh()` auf, wenn sich die Quelldaten zwischen Kopieren und Speichern geändert haben. |
| Entsorgen Sie Arbeitsmappen nach Gebrauch | `sourceWorkbook.dispose();` gibt native Ressourcen frei, was bei großen Dateien wichtig ist. |

## Sonderfälle, denen Sie begegnen könnten

* **Mehrere Arbeitsblätter mit voneinander abhängigen Pivot‑Tabellen** – Kopieren Sie jedes Arbeitsblatt einzeln; gemeinsam genutzte Caches werden automatisch dupliziert, aber Sie müssen ggf. externe Datenverbindungen neu zuweisen.
* **Pivot‑Tabellen, die auf externen SQL‑Abfragen basieren** – Stellen Sie sicher, dass die Zielumgebung dieselbe Datenbank erreichen kann; sonst zeigt die Pivot‑Tabelle „#REF!“‑Fehler.
* **Große Arbeitsmappen (>100 MB)** – Verwenden Sie `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, um den Speicherverbrauch während des Kopiervorgangs zu reduzieren.

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das alle besprochenen Schritte integriert. Speichern Sie es als `CopyPivotTable.java`, passen Sie die Dateipfade an und führen Sie es mit Ihrer bevorzugten IDE oder über `javac`/`java` aus.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);

        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving the pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);

        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");

        // Optional: copy only the pivot table to a separate workbook
        PivotTable pivot = sourceWorksheet.getPivotTables().get(0);
        Workbook pivotOnlyWorkbook = new Workbook();
        Worksheet pivotSheet = pivotOnlyWorkbook.getWorksheets().add("PivotOnly");
        pivotSheet.getPivotTables().addCopy(pivot);
        pivotOnlyWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");

        // Optional: create a new workbook from a freshly built sheet with a pivot
        Worksheet tempSheet = new Worksheet();
        PivotTable newPivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");
        // Configure newPivot (data source, rows, columns, etc.) here...

        Workbook createdFromSheet =


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}