---
category: general
date: 2026-10-16
description: Wie man Pivot-Tabellen in Java mit Aspose.Cells kopiert – lernen Sie,
  Bereiche in ein anderes Blatt zu kopieren und Bereiche zwischen Arbeitsblättern
  effizient zu kopieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: de
lastmod: 2026-10-16
og_description: Wie man Pivot‑Tabellen in Java mit Aspose.Cells kopiert. Dieses Tutorial
  zeigt Ihnen, wie Sie einen Bereich in ein anderes Blatt und zwischen Arbeitsblätter
  mit vollständigem Code kopieren.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Wie man eine Pivot‑Tabelle zwischen Arbeitsblättern in Java kopiert – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Wie man eine Pivot‑Tabelle zwischen Arbeitsblättern in Java kopiert
url: /de/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Pivot‑Tabelle zwischen Arbeitsblättern in Java kopiert

Wenn Sie **how to copy pivot table** von einem Blatt zu einem anderen im selben Arbeitsbuch kopieren müssen, bietet dieser Leitfaden eine komplette, sofort einsatzbereite Lösung. Sie sehen, wie Sie den Quellbereich, der die Pivot‑Tabelle enthält, kopieren, ihre Funktionalität erhalten und das Ergebnis überprüfen – alles mit Aspose.Cells für Java.

Das Kopieren einer Pivot‑Tabelle ist eine häufige Aufgabe, wenn Sie Berichte programmgesteuert erstellen, und wenn es korrekt durchgeführt wird, vermeiden Sie den Verlust des Pivot‑Caches oder das Brechen von Formeln. Am Ende dieses Tutorials können Sie **copy range to another sheet** und **copy range between worksheets** ohne manuelle Schritte ausführen.

## Was Sie lernen werden

* Eine vorhandene Excel‑Datei mit einer Pivot‑Tabelle laden.
* Den Quellbereich definieren, der die Pivot‑Tabelle enthält.
* Einen Zielbereich auf einem anderen Arbeitsblatt definieren.
* `CopyOptions` verwenden, um die Pivot‑Tabelle unverändert zu behalten.
* Überprüfen, dass die kopierte Pivot‑Tabelle wie erwartet funktioniert.

**Voraussetzungen**

* Java 17 oder höher.
* Aspose.Cells für Java (Version 23.12 oder neuer).  
* Eine Excel‑Datei (`input.xlsx`), die auf dem ersten Blatt eine Pivot‑Tabelle enthält.

---

## Pivot‑Tabelle mit Aspose.Cells kopieren

Der Kern der Operation ist ein vierstufiger Prozess: Arbeitsmappe laden, Quellbereich finden, Zielbereich festlegen und den Kopiervorgang ausführen. Nachfolgend wird jeder Schritt im Detail erklärt.

### Schritt 1: Arbeitsmappe laden

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Warum dieser Schritt?*  
Das Laden der Arbeitsmappe bringt die gesamte Datei in den Speicher, sodass Sie Zugriff auf Arbeitsblätter, Zellen und den Pivot‑Cache erhalten. Aspose.Cells liest das Dateiformat automatisch, sodass Sie sich nicht um `.xls` vs `.xlsx` kümmern müssen.

### Schritt 2: Quellbereich finden, der die Pivot‑Tabelle enthält

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Warum dieser Schritt?*  
Eine Pivot‑Tabelle wird in einem Zellblock gespeichert, der ebenfalls auf einen versteckten Cache verweist. Durch die Auswahl des genauen Bereichs (`A1:G20` in diesem Beispiel) stellen Sie sicher, dass der Cache beim Kopieren des Bereichs verknüpft bleibt.

### Schritt 3: Zielbereich auf einem anderen Blatt definieren

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Warum dieser Schritt?*  
Die Auswahl eines Ziels auf einem anderen Arbeitsblatt ermöglicht Ihnen **copy range to another sheet**. Die Zelle oben links (`A1`) ist ein gängiger Ausgangspunkt, Sie können sie jedoch überall platzieren, indem Sie die Adresse ändern.

### Schritt 4: Quellbereich kopieren und dabei die Pivot‑Tabelle erhalten

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Warum dieser Schritt?*  
`CopyOptions` steuert, was übertragen wird. Die Verwendung von `PasteType.PASTE_ALL` garantiert, dass die Pivot‑Tabelle, ihre Formatierung und die zugrunde liegenden Formeln dupliziert werden. Ohne diese Optionen könnten nur Rohwerte kopiert werden, was die Pivot‑Funktionalität zerstört.

### Schritt 5: Arbeitsmappe speichern und Ergebnis überprüfen

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Öffnen Sie `output.xlsx` in Excel und bestätigen Sie, dass:

* Das zweite Blatt eine voll funktionsfähige Pivot‑Tabelle enthält, die mit der Originalidentisch ist.
* Durch Aktualisieren der Pivot‑Tabelle die Daten aktualisiert werden, was beweist, dass der Cache intakt ist.

---

## Bereich mit Java in ein anderes Blatt kopieren

Wenn Ihr Ziel einfach **copy range to another sheet** ohne Pivot‑Tabelle ist, funktioniert derselbe Code mit einem regulären Zellbereich. Die einzige Änderung ist die Quelladresse. Die `CopyOptions`‑Konfiguration bleibt gleich und stellt sicher, dass Formeln und Formatierungen erhalten bleiben.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Dieses Snippet demonstriert die Flexibilität der API für sowohl Pivot‑ als auch Nicht‑Pivot‑Szenarien.

---

## Bereich zwischen Arbeitsblättern kopieren, ohne Formeln zu verlieren

Wenn Sie **copy range between worksheets** ausführen, können Formeln, die andere Blätter referenzieren, beschädigt werden, wenn sich relative Bezüge ändern. Um dies zu vermeiden:

1. Verwenden Sie `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`, wenn Sie nur Formeln benötigen.
2. Halten Sie das Zielblatt im selben Arbeitsbuch, damit interne Verweise gültig bleiben.
3. Rufen Sie nach dem Kopieren `workbook.calculateFormula();` auf, um eine Neuberechnung zu erzwingen.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Diese zusätzlichen Schritte stellen sicher, dass ein kopierter Bereich sich exakt wie das Original verhält, selbst wenn er sich über mehrere Arbeitsblätter erstreckt.

---

## Profi‑Tipps und häufige Fallstricke

| Situation | Tipp |
|-----------|------|
| **Pivot cache not updating** | After copying, call `destSheet.getPivotTables().get(0).refresh();` to refresh the cache. |
| **Copying to a different workbook** | Use `Workbook destWorkbook = new Workbook();` and then `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Remember to copy the pivot cache separately if needed. |
| **Large pivot tables** | Increase the Java heap size (`-Xmx2g`) to avoid `OutOfMemoryError` during the copy. |
| **Preserving styles** | Set `copyOptions.setPasteType(PasteType.PASTE_ALL)`; otherwise, only values are copied. |

## Erwartete Ausgabe

Das Ausführen des vollständigen Programms erzeugt `output.xlsx`. Beim Öffnen in Excel:

* **Sheet2!A1:G20** zeigt dieselbe Pivot‑Tabelle wie **Sheet1!A1:G20** an.
* Die Pivot‑Feldliste, Zeilen‑/Spalten‑Bezeichnungen und Datenwerte stimmen mit der Quelle überein.
* Durch Aktualisieren der Pivot‑Tabelle werden die Zahlen aktualisiert, was bestätigt, dass der Cache funktionstüchtig ist.

Die Konsole gibt aus:

```
Pivot table copied successfully.
```

---

## Fazit

In diesem Tutorial haben Sie **how to copy pivot table** von einem Arbeitsblatt zu einem anderen mit Aspose.Cells für Java gelernt. Durch das Laden der Arbeitsmappe, das Auswählen des richtigen Quellbereichs, das Definieren eines Ziels und das Konfigurieren von `CopyOptions` können Sie zuverlässig **copy range to another sheet** und **copy range between worksheets** kopieren, während Sie die gesamte Pivot‑Funktionalität erhalten.  

Als Nächstes könnten Sie erkunden:

* Exportieren der kopierten Pivot‑Tabelle nach PDF oder HTML.
* Automatisieren von Pivot‑Tabellen‑Aktualisierungen über mehrere Arbeitsmappen hinweg.
* Verwenden von `CopyOptions`, um nur bestimmte Elemente zu kopieren (z. B. Werte, Formate).

Fühlen Sie sich frei, mit verschiedenen Bereichsadressen, Arbeitsmappen‑Strukturen oder sogar Kopien über Arbeitsmappen hinweg zu experimentieren. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Bereich in Java kopiert – Pivot‑Tabelle mit Aspose.Cells kopieren](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Wie man Pivot‑Tabelle in Java kopiert – Vollständiger Aspose.Cells‑Leitfaden](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Pivot‑Tabelle in Excel kopieren – Schritt‑für‑Schritt‑Anleitung mit Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}