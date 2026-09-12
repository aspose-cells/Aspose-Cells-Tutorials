---
category: general
date: 2026-09-11
description: Erstellen Sie ein neues Arbeitsblatt und kopieren Sie einen Excel‑Bereich
  mit Aspose.Cells. Erfahren Sie, wie Sie einen Bereich zwischen Arbeitsblättern kopieren
  und dabei Pivot‑Tabellen erhalten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: de
lastmod: 2026-09-11
og_description: Erstellen Sie ein neues Arbeitsblatt und kopieren Sie einen Excel‑Bereich
  mit Aspose.Cells. Dieses Tutorial zeigt die genauen Schritte zum Kopieren von Bereichen
  zwischen Arbeitsblättern und zum Beibehalten von Pivot‑Tabellen.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Neues Arbeitsblatt erstellen und Excel‑Bereich kopieren – Aspose.Cells‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Neues Arbeitsblatt erstellen und Excel‑Bereich mit Aspose.Cells kopieren
url: /de/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues Arbeitsblatt erstellen und Excel‑Bereich mit Aspose.Cells kopieren

Wenn Sie **ein neues Arbeitsblatt erstellen** und Daten in einer Excel‑Datei verschieben müssen, macht Aspose.Cells das unkompliziert. Dieser Leitfaden zeigt genau, wie Sie einen Excel‑Bereich von einem Blatt auf ein anderes kopieren, wobei alle Pivot‑Tabellen im Bereich erhalten bleiben.

Sie lernen, wie Sie **einen Excel‑Bereich kopieren**, wie Sie **einen Bereich zwischen Blättern kopieren** und warum die Aspose.Cells‑Methode `copy` Pivot‑Tabellendefinitionen unverändert lässt. Es werden keine externen Werkzeuge benötigt – nur ein Java‑Projekt mit der Aspose.Cells‑Bibliothek.

## Voraussetzungen

- Java 17 oder neuer installiert
- Aspose.Cells für Java (Version 23.12 oder neuer) zum Klassenpfad Ihres Projekts hinzugefügt
- Eine Quell‑Arbeitsmappe (`input.xlsx`), die eine Pivot‑Tabelle im zu kopierenden Bereich enthält
- Grundlegende Kenntnisse der Java‑Syntax sowie der Maven/Gradle‑Abhängigkeitsverwaltung

## Schritt 1: Projekt einrichten und Aspose.Cells importieren

Erstellen Sie ein einfaches Maven‑Projekt (oder Gradle, falls Sie das bevorzugen) und fügen Sie die Aspose.Cells‑Abhängigkeit hinzu:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Importieren Sie anschließend die benötigten Klassen in Ihrer Java‑Quelldatei:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Warum dieser Schritt wichtig ist*: Durch das Importieren der richtigen Klassen erhalten Sie Zugriff auf `Workbook`, `Worksheet`, `Range` und die `copy`‑Methode, die den Bereichstransfer übernimmt.

## Schritt 2: Quell‑Arbeitsmappe laden

Öffnen Sie die Arbeitsmappe, die die zu kopierenden Daten enthält. Der folgende Code lädt `input.xlsx` aus einem von Ihnen angegebenen Verzeichnis:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Erläuterung*: `Workbook` repräsentiert die gesamte Excel‑Datei. Durch einmaliges Laden erhalten Sie Lese‑/Schreibzugriff auf jedes Blatt und jede Zellsammlung.

## Schritt 3: Quell‑Bereich ermitteln, der die Pivot‑Tabelle enthält

Wählen Sie das Arbeitsblatt aus, das die Pivot‑Tabelle enthält, und definieren Sie den genauen Zellblock, den Sie kopieren möchten. In diesem Beispiel kopieren wir die Zellen A1 bis D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Warum das wichtig ist*: Durch das Erstellen eines `Range`‑Objekts teilen Sie Aspose.Cells genau mit, welche Zellen (einschließlich eingebetteter Objekte wie Pivot‑Tabellen) dupliziert werden sollen.

## Schritt 4: **Neues Arbeitsblatt erstellen**, das die kopierten Daten empfängt

Jetzt fügen wir dem selben Workbook ein neues Blatt hinzu. Hier erscheint das Haupt‑Keyword:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Erläuterung*: Das Hinzufügen eines neuen Blatts isoliert die kopierten Daten, sodass Sie leicht prüfen können, ob die **copy excel range**‑Operation erfolgreich war, ohne das Originalblatt zu beeinflussen.

## Schritt 5: Bereich kopieren – die Pivot‑Tabelle wird automatisch erhalten

Verwenden Sie die `copy`‑Methode, um den Bereich vom Quell‑Blatt zum Ziel‑Blatt zu verschieben. Aspose.Cells kopiert Formeln, Formatierungen und Pivot‑Tabellendefinitionen:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Warum das funktioniert*: Die `copy`‑Methode führt eine tiefe Kopie der Quellzellen durch. Sie kopiert nicht nur Werte, sondern repliziert die gesamte Zellstruktur, einschließlich des Pivot‑Caches. Deshalb können Sie **copy range aspose.cells** ausführen und auf dem neuen Blatt eine funktionierende Pivot‑Tabelle sehen.

## Schritt 6: Arbeitsmappe mit dem neuen Arbeitsblatt speichern

Schließlich schreiben Sie die modifizierte Arbeitsmappe auf die Festplatte:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Ergebnis*: `output.xlsx` enthält nun das Originalblatt plus ein neues Blatt namens **Copy**, das exakt denselben Bereich inklusive Pivot‑Tabelle enthält.

## Vollständiges funktionierendes Beispiel

Alle Teile zusammengefügt, hier das vollständige, ausführbare Programm:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Erwartete Ausgabe**: Öffnen Sie `output.xlsx` in Excel. Sie sehen ein Blatt namens **Copy**, dessen Zellen A1:D20 dieselben Daten, dieselbe Formatierung und eine aktive Pivot‑Tabelle enthalten, die der Original‑Pivot‑Tabelle entspricht.

## Häufige Fragen und Sonderfälle

- **Was ist, wenn der Quell‑Bereich zusammengeführte Zellen enthält?**  
  Die `copy`‑Methode kopiert ebenfalls die Zusammenführungsinformationen, sodass zusammengeführte Zellen im Zielblatt unverändert bleiben.

- **Kann ich in eine andere Arbeitsmappe kopieren?**  
  Ja. Laden Sie eine zweite `Workbook`‑Instanz, erstellen Sie einen Ziel‑Bereich in dieser Arbeitsmappe und rufen Sie `sourceRange.copy(destinationRange)` auf. Die Methode übernimmt das Kopieren über Arbeitsmappen hinweg automatisch.

- **Was ist, wenn das Ziel‑Blatt bereits Daten enthält?**  
  Der Kopiervorgang überschreibt alle vorhandenen Zellen, die mit dem Ziel‑Bereich überschneiden. Um Datenverlust zu vermeiden, stellen Sie sicher, dass der Zielbereich leer ist, oder verwenden Sie eine andere Startzelle (z. B. `"B2"`).

- **Wird der Pivot‑Cache dupliziert?**  
  Aspose.Cells verwendet den ursprünglichen Pivot‑Cache erneut, was bedeutet, dass die neue Pivot‑Tabelle weiterhin mit denselben Quelldaten verknüpft ist. Wenn Sie einen unabhängigen Cache benötigen, müssen Sie die Pivot‑Tabelle nach dem Kopieren neu erstellen.

## Tipps und bewährte Vorgehensweisen

- **Pro‑Tipp**: Verwenden Sie `Workbook.setForceFormulaRecalculation(true)` vor dem Speichern, wenn Ihr Bereich Formeln enthält, die von Daten außerhalb des kopierten Blocks abhängen.
- **Achten Sie auf** große Bereiche: Das Kopieren riesiger Blätter kann viel Speicher verbrauchen. Ziehen Sie in Betracht, in kleineren Abschnitten zu kopieren, falls Sie `OutOfMemoryError` erhalten.
- **Performance‑Tipp**: Deaktivieren Sie die Bildschirmaktualisierung (`workbook.getSettings().setCalculateFormulaOnOpen(false)`), wenn Sie mit sehr großen Dateien arbeiten, um den Kopiervorgang zu beschleunigen.

## Fazit

Sie wissen jetzt, wie Sie **ein neues Arbeitsblatt erstellen** und **einen Excel‑Bereich** zwischen Blättern mit Aspose.Cells kopieren, wobei Pivot‑Tabellen und alle Zelleigenschaften erhalten bleiben. Diese Technik ermöglicht es Ihnen, Datenblöcke programmgesteuert zu duplizieren, Berichtsvorlagen zu erstellen oder Arbeitsmappen neu zu strukturieren, ohne manuelles Kopieren‑Einfügen.

Als Nächstes können Sie verwandte Themen wie **copy range aspose.cells** für Cross‑Workbook‑Operationen, die Automatisierung von Pivot‑Tabellen‑Aktualisierungen oder das Exportieren des kopierten Blatts nach PDF erkunden. Experimentieren Sie mit verschiedenen Quell‑Bereichen und Blattnamen, um sie an Ihr konkretes Automatisierungsszenario anzupassen. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu beherrschen und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Formen zwischen Excel‑Blättern mit Aspose.Cells für .NET kopieren: Ein vollständiger Leitfaden](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Bilder zwischen Blättern in Excel mit Aspose.Cells für Java kopieren: Ein umfassender Leitfaden](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET: Bereichsdaten kopieren](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}