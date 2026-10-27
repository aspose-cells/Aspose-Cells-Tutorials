---
category: general
date: 2026-10-07
description: Erfahren Sie, wie Sie Pivot‑Tabellen in Excel mit Java und Aspose.Cells
  duplizieren. Kopieren Sie eine Pivot‑Tabelle, indem Sie ihren Bereich schnell zwischen
  Arbeitsmappen kopieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: de
lastmod: 2026-10-07
og_description: Wie man Pivot‑Tabellen in Excel mit Java und Aspose.Cells dupliziert.
  Folgen Sie dieser Anleitung, um eine Pivot‑Tabelle zu kopieren, indem Sie ihren
  Bereich zwischen Arbeitsmappen kopieren.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Wie man Pivot-Tabellen in Excel mit Java dupliziert – vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Wie man Pivot‑Tabellen in Excel mit Java dupliziert – Schritt‑für‑Schritt‑Anleitung
url: /de/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot-Tabellen in Excel mit Java dupliziert – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **Pivot‑Tabellen duplizieren** müssen in einer Excel-Arbeitsmappe, zeigt Ihnen dieses Tutorial eine vollständige, sofort ausführbare Lösung. Mit Aspose.Cells für Java können Sie eine Pivot-Tabelle zusammen mit ihren Quelldaten kopieren, indem Sie den zugrunde liegenden Bereich kopieren und das Ergebnis dann als neue Arbeitsmappe speichern.

Das Duplizieren einer Pivot-Tabelle wirkt oft knifflig, weil der Pivot-Cache im Blatt versteckt ist. Durch das Kopieren des gesamten Bereichs, der die Pivot-Tabelle enthält, erstellt Aspose.Cells den Cache im Zielarbeitsbuch automatisch neu, sodass Sie eine voll funktionsfähige Kopie erhalten, ohne manuelles XML‑Herumfummeln.

In diesem Leitfaden werden Sie:

* Eine Quellarbeitsmappe laden, die eine Pivot-Tabelle enthält.  
* Den genauen Bereich definieren, der die Pivot enthält.  
* Diesen Bereich in eine neue Arbeitsmappe kopieren und die Pivot-Definition beibehalten.  
* Die neue Datei speichern und überprüfen, dass die Pivot funktioniert.  

Die Schritte funktionieren mit jeder von Aspose.Cells unterstützten Excel-Version (2007‑2024) und erfordern nur wenige Zeilen Java‑Code.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **Java 8 or newer** | Aspose.Cells ist für Java 8+ entwickelt. |
| **Aspose.Cells for Java** (latest version) | Stellt die in dem Beispiel verwendeten APIs `Workbook`, `Range` und `CopyRange` bereit. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Die Pivot, die Sie duplizieren möchten. |
| **Write permission** to the target directory | Erforderlich, um `CopyWithPivot.xlsx` zu speichern. |

Fügen Sie die Aspose.Cells Maven‑Abhängigkeit zu Ihrer `pom.xml` hinzu (oder laden Sie das JAR manuell herunter):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Wie man Pivot-Tabellen dupliziert – vollständige Implementierung

Unten finden Sie ein eigenständiges Java‑Programm, das **wie man Pivot‑Tabellen dupliziert** demonstriert, indem es den Bereich kopiert, der die Pivot enthält. Der Code beinhaltet Fehlerbehandlung, Kommentare und einen Verifizierungsschritt.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Erklärung jedes Schrittes

| Schritt | Was der Code macht | Warum es wichtig ist für **Pivot‑Tabelle kopieren** |
|---------|-------------------|---------------------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` liest `Source.xlsx`. | Die Quelldatei ist der einzige Ort, an dem die ursprüngliche Pivot existiert. |
| **2️⃣ Define the range** | `createRange("A1:G20")` erstellt ein `Range`‑Objekt, das die Pivot und ihre Daten abdeckt. | Eine Pivot‑Tabelle wird zusammen mit ihrem Cache gespeichert; das Kopieren des gesamten Bereichs stellt sicher, dass der Cache ebenfalls übertragen wird. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` schreibt den Bereich in das Ziel‑Blatt. | Dies ist der Kern von **Bereich zwischen Arbeitsmappen kopieren** – die API verarbeitet versteckte Objekte automatisch. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` zwingt die Pivot, neu zu berechnen. | Stellt sicher, dass die duplizierte Pivot dieselben Werte wie das Original anzeigt, insbesondere nach Änderungen. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` schreibt die Datei auf die Festplatte. | Erzeugt das endgültige Ergebnis **Excel‑Bereich kopieren**, das Sie in Excel öffnen können. |

#### Erwartete Ausgabe

Nach dem Ausführen des Programms öffnen Sie `CopyWithPivot.xlsx`. Sie sehen ein Arbeitsblatt, das identisch zum Quellblatt aussieht, und die Pivot‑Tabelle funktioniert exakt wie das Original – Sie können Zeilen erweitern, Felder filtern und Daten ohne Fehler aktualisieren.

## Häufige Varianten und Sonderfälle

### 1️⃣ Kopieren einer Pivot, die sich über mehrere Blätter erstreckt

Wenn die Quelldaten der Pivot auf einem anderen Blatt als die Pivot‑Tabelle selbst liegen, schließen Sie beide Blätter in den Kopiervorgang ein. Der einfachste Ansatz ist, zuerst das gesamte Quellblatt zu kopieren und anschließend das Pivot‑Blatt:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Umgang mit benannten Bereichen

Aspose.Cells bewahrt benannte Bereiche beim Kopieren eines Bereichs. Wenn das Zielarbeitsbuch jedoch bereits einen Namen mit derselben Kennung enthält, wird eine `CellsException` ausgelöst. Lösen Sie dies, indem Sie den konfligierenden Namen vor dem Kopieren umbenennen:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Große Arbeitsmappen und Leistung

Das Kopieren sehr großer Bereiche (Hunderttausende von Zeilen) kann speicherintensiv sein. Aktivieren Sie **Speicheroptimierung**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Formeln unverändert behalten

Wenn der Quellbereich Formeln enthält, die auf Zellen außerhalb des kopierten Bereichs verweisen, werden diese Verweise nach dem Kopieren ungültig. Um dies zu vermeiden, erweitern Sie den Bereich, um alle abhängigen Zellen einzuschließen, oder verwenden Sie `copyRange` mit dem `CopyOptions`‑Flag `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Profi‑Tipps für ein zuverlässiges **Bereich zwischen Arbeitsmappen kopieren**

* **Immer absolute Adressen** (`$A$1:$G$20`) verwenden, wenn das Quellblatt umbenannt werden könnte.  
* **Nach dem Kopieren aktualisieren** – obwohl Aspose.Cells den Cache neu erstellt, beseitigt das Aufrufen von `refresh()` gelegentliche Warnungen über veraltete Caches in Excel.  
* **Pivot validieren**: Nach dem Speichern die Datei programmgesteuert öffnen und `pivotTable.validate()` aufrufen, um sicherzustellen, dass keine fehlerhaften Verweise vorhanden sind.  
* **Versionskompatibilität**: Der Code funktioniert mit Excel‑2007‑2024‑Dateien (`.xlsx`, `.xlsm`). Für ältere `.xls`‑Dateien setzen Sie `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Vollständige Quellcode‑Auflistung (bereit zum Kompilieren)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Pivot‑Tabelle in Java kopiert – Vollständige Aspose.Cells‑Anleitung](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Wie man Pivot‑Tabellen in Excel mit Aspose.Cells für Java erstellt: Ein umfassender Leitfaden](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Wie man die Quelle einer Excel‑Pivot‑Tabelle mit Aspose.Cells für Java aktualisiert: Ein umfassender Leitfaden](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}