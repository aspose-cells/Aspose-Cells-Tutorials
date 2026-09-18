---
category: general
date: 2026-09-18
description: Wie man Pivot in Java mit Aspose.Cells dupliziert – eine Pivot‑Tabelle
  schnell und zuverlässig zwischen Arbeitsmappen kopiert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: de
lastmod: 2026-09-18
og_description: Wie man ein Pivot in Java mit Aspose.Cells dupliziert. Folgen Sie
  diesem vollständigen Tutorial, um eine Pivot‑Tabelle zwischen Arbeitsmappen mit
  sauberem Java‑Code zu kopieren.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Pivot‑Tabelle in Java duplizieren – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Wie man Pivot‑Tabellen in Java mit Aspose.Cells dupliziert
url: /de/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot‑Tabellen in Java mit Aspose.Cells dupliziert

Wenn Sie **wie man Pivot dupliziert** in einer Java‑Anwendung benötigen, zeigt Ihnen dieser Leitfaden die genauen Schritte. Durch das Laden einer Excel‑Arbeitsmappe, das Definieren des Zellbereichs des Pivot und das Kopieren dieses Bereichs in eine neue Arbeitsmappe können Sie eine Pivot‑Tabelle verschieben, ohne deren Definition oder Daten zu verlieren.

Das Kopieren einer Pivot‑Tabelle ist ein häufiges Bedürfnis, wenn Sie Berichte erstellen, Analysen archivieren oder eine große Arbeitsmappe in modulare Teile aufteilen. In diesem Tutorial lernen Sie, wie man **Bereich zwischen Arbeitsmappen kopiert**, wie man **Excel‑Arbeitsmappe in Java lädt** und die Feinheiten des **sicheren Kopierens von Pivot**.

Am Ende erhalten Sie ein sofort ausführbares Java‑Programm, das eine Pivot‑Tabelle von `Source.xlsx` nach `PivotCopied.xlsx` mit Aspose.Cells für Java dupliziert.

## Voraussetzungen

* JDK 8 oder neuer installiert.
* Maven (oder ein anderes Build‑Tool) zur Verwaltung von Abhängigkeiten.
* Aspose.Cells für Java Version 23.10 oder höher. Fügen Sie die folgende Maven‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Eine Quellarbeitsmappe (`Source.xlsx`), die eine Pivot‑Tabelle im Bereich **A1:H30** enthält.

## Wie man Pivot in Java dupliziert

Die Grundidee ist einfach:

1. **Laden der Quellarbeitsmappe** – das gibt Ihnen Zugriff auf das Arbeitsblatt, das die Pivot‑Tabelle enthält.
2. **Definieren des Zellbereichs**, der die Pivot‑Tabelle umschließt.
3. **Erstellen einer Zielarbeitsmappe** – eine leere Datei, die den kopierten Bereich erhalten wird.
4. **Kopieren des Bereichs** – Aspose.Cells dupliziert automatisch die Pivot‑Definition.
5. **Speichern der Zielarbeitsmappe** – Sie haben nun eine separate Datei mit derselben Pivot‑Tabelle.

Nachfolgend finden Sie ein vollständiges, ausführbares Java‑Programm, das diese Schritte ausführt.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Warum das funktioniert

* **Aspose.Cells** behandelt eine Pivot‑Tabelle als Teil der Zellsammlung des Arbeitsblatts. Wenn Sie `copyRange` aufrufen, kopiert die Bibliothek nicht nur Zellwerte, sondern auch den zugrunde liegenden Pivot‑Cache und die Definition, sodass die neue Arbeitsmappe ein voll funktionsfähiges Duplikat enthält.
* Das Objekt `CopyOptions` bewahrt standardmäßig Formeln, Formate und eingebettete Objekte. Sie können es anpassen (z. B. `setCopyColumnWidths(true)`), falls Sie zusätzliche Kontrolle benötigen.

## Bereich zwischen Arbeitsmappen kopieren – genauerer Blick

Während das obige Beispiel einen einzelnen zusammenhängenden Block kopiert, kann `copyRange` jeden rechteckigen Bereich verarbeiten. Wenn Ihre Pivot‑Tabelle nicht zusammenhängende Bereiche umfasst, können Sie `copyRange` mehrmals aufrufen oder `Worksheet.copy` verwenden, um das gesamte Blatt zu duplizieren.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tipp:** Beim Kopieren großer Arbeitsmappen aktivieren Sie `CopyOptions.setPreserveCellStyle(true)`, um unnötige Stilduplikationen zu vermeiden, was die Leistung verbessern kann.

## Wie man Pivot in eine Arbeitsmappe kopiert – Umgang mit mehreren Pivots

Wenn das Quellblatt mehr als einen Pivot enthält, können Sie über die Pivot‑Tabellen des Arbeitsblatts iterieren und jede einzeln kopieren:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Dieser Ansatz stellt sicher, dass jeder Pivot seinen ursprünglichen Namen und seine Datenquelle beibehält.

## Excel‑Arbeitsmappe in Java laden – häufige Fallstricke

* **Dateipfad‑Trennzeichen:** Verwenden Sie Vorwärtsschrägstriche (`/`) oder `File.separator`, um den Code plattformunabhängig zu halten.
* **Fehlende Lizenz:** Aspose.Cells arbeitet im Evaluierungsmodus, aber die Ausgabe enthält ein Wasserzeichen. Registrieren Sie eine Lizenz mit `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` bevor Sie die Arbeitsmappe laden, um das Wasserzeichen zu entfernen.
* **Große Dateien:** Für Arbeitsmappen größer als 100 MB sollten Sie `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` mit Streaming‑Optionen verwenden, um den Speicherverbrauch zu reduzieren.

## Vollständige End‑zu‑Ende‑Beispiel‑Zusammenfassung

Wenn wir alles zusammenführen, hier das endgültige Programm, das Sie in Ihre IDE kopieren‑und‑einfügen können:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Erwartete Ausgabe:** Nach der Ausführung erscheint `PivotCopied.xlsx` im angegebenen Verzeichnis. Öffnet man sie in Excel, wird das gleiche Pivot‑Tabellen‑Layout, dieselben Filter und Daten wie in `Source.xlsx` angezeigt. Alle berechneten Felder und Formatierungen bleiben erhalten.

## Häufig gestellte Fragen

* **Funktioniert das mit älteren Excel‑Formaten (.xls)?**  
  Ja. Aspose.Cells erkennt das Format automatisch. Verwenden Sie `new Workbook("file.xls")` und dieselbe Kopierlogik gilt.

* **Was ist, wenn der Pivot externe Datenquellen referenziert?**  
  Die Kopie behält die ursprüngliche Datenquellen‑Referenz bei. Wenn die Zielumgebung diese Quelle nicht erreichen kann, zeigt der Pivot `#REF!`‑Fehler an. Um dies zu vermeiden, aktualisieren Sie den Pivot nach dem Kopieren oder ändern Sie seine Datenquelle über `PivotTable.setDataSource(...)`.

* **Kann ich einen Pivot zu einem bestimmten Blattnamen kopieren?**  
  Natürlich. Nachdem Sie das Zielarbeitsblatt erstellt haben, benennen Sie es um:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Fazit

Sie wissen jetzt, **wie man Pivot‑Tabellen** in Java mit Aspose.Cells dupliziert, wie man **Bereich zwischen Arbeitsmappen kopiert** und die besten Praktiken für **Excel‑Arbeitsmappe in Java laden**. Durch das Befolgen des Fünf‑Schritte‑Prozesses – Laden, Definieren, Ziel erstellen, Kopieren und Speichern – können Sie die Berichtserstellung automatisieren, Analysen archivieren oder komplexe Arbeitsmappen aufteilen, ohne die Pivot‑Funktionalität zu verlieren.

Als Nächstes erkunden Sie verwandte Themen wie **Pivot in Arbeitsmappe kopieren** mit mehreren Blättern oder integrieren Sie den duplizierten Pivot in eine größere Datenverarbeitungspipeline mithilfe von Apache POI für Nicht‑Aspose‑Szenarien. Experimentieren Sie mit verschiedenen `CopyOptions`‑Einstellungen, um die Leistung für sehr große Arbeitsmappen zu optimieren.

Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Pivot‑Tabellen in Excel mit Aspose.Cells für Java erstellt: Ein umfassender Leitfaden](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Wie man die Datenquelle einer Excel‑Pivot‑Tabelle mit Aspose.Cells für Java aktualisiert: Ein umfassender Leitfaden](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Pivot‑Felder in Excel‑Arbeitsmappen mit Aspose.Cells für Java gruppieren – umfassender Leitfaden](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}