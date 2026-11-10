---
category: general
date: 2026-10-23
description: Erfahren Sie, wie Sie ein Excel‑Blatt in Java duplizieren und dabei Pivot‑Tabellen
  erhalten. Dieser Leitfaden zeigt außerdem, wie man Pivot‑Tabellen kopiert, Excel‑Bereiche
  kopiert und ein Blatt mit Pivot‑Daten kopiert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: de
lastmod: 2026-10-23
og_description: Dupliziere ein Excel‑Blatt in Java und bewahre dabei Pivot‑Tabellen.
  Folge diesem vollständigen Tutorial, um Pivot‑Tabellen zu kopieren, Excel‑Bereiche
  zu kopieren und ein Blatt mit Pivot‑Daten zu duplizieren.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Ein Excel‑Blatt mit Pivot‑Tabellen in Java duplizieren – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Wie man ein Excel‑Blatt dupliziert und Pivot‑Tabellen in Java intakt hält
url: /de/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Excel-Blatt dupliziert und Pivot-Tabellen intakt hält in Java

Wenn Sie ein **Excel-Blatt duplizieren** möchten, während Sie jede Pivot-Tabelle erhalten, zeigt Ihnen dieser Leitfaden genau, wie es geht. Sie sehen eine prägnante Lösung, die ein Blatt kopiert, einen bestimmten Bereich kopiert und sogar eine Pivot-Tabelle in eine andere Arbeitsmappe kopiert – alles in reinem Java mit Aspose.Cells.

Das Duplizieren eines Excel-Blatts ist eine gängige Aufgabe, wenn Sie monatliche Berichte aus einer Vorlage erstellen oder eine Sandbox‑Kopie zum Testen benötigen. Der untenstehende Code funktioniert mit Aspose.Cells 25.11 oder neuer, das die Option `setCopyPivotTable(true)` eingeführt hat.

## Was Sie benötigen

- Java 17 (oder ein aktuelles JDK) installiert
- Aspose.Cells for Java 25.11 oder neuer in Ihrem Projekt (Maven‑Koordinate `com.aspose:aspose-cells:25.11`)
- Eine Quell‑Arbeitsmappe (`SourceWithPivot.xlsx`), die bereits eine Pivot‑Tabelle enthält
- Eine IDE oder ein Build‑Tool Ihrer Wahl (IntelliJ IDEA, Eclipse, Maven, Gradle usw.)

## Schritt 1: Laden Sie die Quell‑Arbeitsmappe, die die Pivot‑Tabelle enthält

Der erste Vorgang besteht darin, die Arbeitsmappe zu öffnen, die die Pivot enthält, die Sie erhalten möchten.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Warum dieser Schritt wichtig ist:** Das Laden der Quell‑Arbeitsmappe gibt Ihnen Zugriff auf die Arbeitsblatt‑Objekte, Zellen und die eingebetteten Pivot‑Tabellen. Ohne dies können Sie die Pivot‑Daten, die Sie kopieren möchten, nicht referenzieren.

## Schritt 2: Erstellen Sie eine leere Ziel‑Arbeitsmappe (oder laden Sie eine vorhandene)

Sie können entweder mit einer leeren Arbeitsmappe beginnen oder eine vorhandene Datei öffnen, die das duplizierte Blatt erhalten soll.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tipp:** Wenn Sie bereits eine Reporting‑Arbeitsmappe haben, ersetzen Sie die obige Zeile durch `new Workbook("ExistingReport.xlsx")`, um das duplizierte Blatt hinzuzufügen.

## Schritt 3: Kopieren Sie das gesamte Arbeitsblatt – die Pivot‑Tabelle wird automatisch erhalten

Das Kopieren des gesamten Arbeitsblatts ist der einfachste Weg, ein **Blatt mit Pivot zu kopieren**. Aspose.Cells kopiert die Pivot‑Definition und deren Cache automatisch.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Warum es funktioniert:** `addCopy` klont die Blattstruktur, Zellwerte, Stile und alle eingebetteten Pivot‑Tabellen. Das neue Arbeitsblatt in `dstWb` sieht dem Original identisch, einschließlich des Pivot‑Caches, aus.

## Schritt 4: (Optional) Kopieren Sie nur einen bestimmten Bereich, der die Pivot‑Tabelle enthält

Manchmal möchten Sie nicht das gesamte Blatt – vielleicht benötigen Sie nur einen Teil, der die Pivot enthält. Hierbei **kopieren Sie einen Excel‑Bereich** und fordern explizit an, dass die Pivot kopiert wird.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Wie es hilft:** `setCopyPivotTable(true)` zwingt die Engine, die Pivot‑Definition zu duplizieren, selbst wenn Sie einen begrenzten Bereich kopieren. Ohne dieses Flag würden nur die Rohdaten kopiert und die Pivot würde verloren gehen.

## Schritt 5: Speichern Sie die Ziel‑Arbeitsmappe

Schließlich schreiben Sie den duplizierten Inhalt in eine neue Datei.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Erwartete Ausgabe

Das Ausführen des Programms erzeugt `DuplicatedWithPivot.xlsx` im Zielverzeichnis. Öffnen Sie die Datei in Excel und Sie sehen:

- Ein neues Arbeitsblatt mit dem Namen `Sheet1 (Copy)` (oder den Originalnamen mit angehängtem „Copy“)
- Die Pivot‑Tabelle erscheint exakt wie im Quellblatt, voll funktionsfähig
- Wenn Sie die optionale Bereichskopie verwendet haben, sind nur die Zellen A1:G30 vorhanden, aber die Pivot funktioniert weiterhin, weil ihr Cache kopiert wurde

## Häufige Fragen und Sonderfälle

### Wie kopiere ich eine Pivot in eine andere Arbeitsmappe, ohne das gesamte Blatt zu kopieren?

Wenn Sie nur die Pivot und deren zugrunde liegende Daten benötigen, kopieren Sie den Bereich, der sowohl die Quelldaten als auch die Pivot enthält, und verwenden Sie dann `setCopyPivotTable(true)`. Der gleiche Code aus **Schritt 4** gilt; stellen Sie lediglich sicher, dass der Bereich die Datenquelle abdeckt.

### Was ist, wenn die Quell‑Arbeitsmappe mehrere Arbeitsblätter mit Pivot‑Tabellen hat?

Wiederholen Sie **Schritt 3** für jedes Arbeitsblatt, das Sie duplizieren möchten:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Funktioniert das mit geschützten Arbeitsblättern?

Aspose.Cells kann geschützte Blätter kopieren, aber Sie müssen sie zuerst unprotecten, wenn Sie die Pivot nach dem Kopieren ändern müssen:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Kann ich eine Pivot‑Tabelle in eine bestehende Arbeitsmappe kopieren, die bereits ein Blatt mit demselben Namen enthält?

Ja. Verwenden Sie `addCopy` mit einem eindeutigen Namen:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Profi‑Tipp: Überprüfen Sie den Pivot‑Cache

Nach dem Kopieren können Sie programmgesteuert bestätigen, dass der Pivot‑Cache existiert:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Wenn die Cache‑ID eine nicht‑negative Zahl ausgibt, wurde die Pivot erfolgreich dupliziert.

## Fazit

Sie wissen jetzt, wie man ein **Excel‑Blatt** in Java dupliziert und dabei jede Pivot‑Tabelle erhält, wie man **Pivot‑Tabellen** direkt kopiert, wie man einen **Excel‑Bereich** kopiert, der eine Pivot enthält, und wie man **Blatt mit Pivot** oder **Pivot in Arbeitsmappe** mit Aspose.Cells 25.11+ kopiert. Wenden Sie diese Muster an, um die Berichtserstellung zu automatisieren, Vorlagenklone zu erstellen oder Testumgebungen aufzubauen, die identische, pivot‑gesteuerte Analysen benötigen.

Bereit, mehr zu erkunden? Versuchen Sie, die duplizierte Arbeitsmappe nach PDF zu exportieren oder den Pivot‑Cache nach dem Kopieren programmgesteuert zu aktualisieren, um sicherzustellen, dass die neuesten Daten angezeigt werden. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man ein Arbeitsblatt dupliziert und Pivot-Tabellen in Java bewahrt](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Wie man Pivot-Tabellen in Java kopiert – Vollständiger Aspose.Cells‑Leitfaden](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Wie man einen Bereich kopiert und eine Pivot‑Tabelle in Java bewahrt](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}