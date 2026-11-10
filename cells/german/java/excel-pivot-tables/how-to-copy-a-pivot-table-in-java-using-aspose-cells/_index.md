---
category: general
date: 2026-09-27
description: Pivot‑Tabelle in Java mit Aspose.Cells kopieren – eine Schritt‑für‑Schritt‑Anleitung,
  die zeigt, wie man einen Bereich kopiert und Pivot‑Definitionen beibehält.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: de
lastmod: 2026-09-27
og_description: Pivot-Tabelle in Java mit Aspose.Cells kopieren. Folgen Sie diesem
  vollständigen Tutorial, um einen Bereich mit Aspose.Cells zu kopieren und die Pivot-Definitionen
  unverändert zu lassen.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Kopieren einer Pivot‑Tabelle in Java – Aspose.Cells Schnellleitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Wie man eine Pivot‑Tabelle in Java mit Aspose.Cells kopiert
url: /de/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Pivot‑Tabelle in Java mit Aspose.Cells kopiert

Wenn Sie eine **Pivot‑Tabelle** von einer Arbeitsmappe in eine andere kopieren müssen, zeigt Ihnen dieser Leitfaden genau, wie Sie dies mit Aspose.Cells für Java tun können. Die Lösung funktioniert für jede erstellte Pivot‑Tabelle und bewahrt die Pivot‑Definition, ohne dass Sie sie manuell neu erstellen müssen.

Sie lernen, wie Sie die Quelldatei laden, den Bereich definieren, der die Pivot‑Tabelle enthält, diesen Bereich in eine neue Arbeitsmappe kopieren und schließlich das Ergebnis speichern. Das Tutorial behandelt außerdem häufige Stolperfallen, wie das Bewahren von Datenquellen und den Umgang mit großen Arbeitsmappen.

## Was Sie benötigen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Java 17 oder neuer (der Code kompiliert auch mit JDK 8+)
* Aspose.Cells für Java 23.9 oder neuer – die neueste Version bietet die zuverlässigste **copy range aspose cells**‑Unterstützung
* Eine Quell‑Excel‑Datei, die eine Pivot‑Tabelle enthält (z. B. `SourceWithPivot.xlsx`)
* Eine IDE oder ein Build‑Tool (Maven/Gradle), das die Aspose.Cells‑JAR referenzieren kann

## Schritt 1: Laden der Quellarbeitsmappe, die die Pivot‑Tabelle enthält

Der erste Schritt besteht darin, die Arbeitsmappe zu öffnen, die die zu duplizierende Pivot‑Tabelle enthält. Das Laden der Datei erzeugt eine In‑Memory‑Darstellung aller Arbeitsblätter, Zellen und Pivot‑Caches.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Warum das wichtig ist:**  
Aspose.Cells liest die gesamte Arbeitsmappe, einschließlich versteckter Pivot‑Cache‑Blätter. Wenn Sie diesen Schritt überspringen, würde die nachfolgende **Pivot‑Tabelle kopieren**‑Operation die zugrunde liegende Datenquelle verlieren.

## Schritt 2: Erstellen einer leeren Zielarbeitsmappe

Als Nächstes instanziieren Sie eine neue Arbeitsmappe, die die kopierte Pivot‑Tabelle erhalten soll. Das Beginnen mit einer leeren Arbeitsmappe verhindert versehentliche Überschreibungen.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tipp:** Die Standardarbeitsmappe enthält ein leeres Blatt, das sich perfekt für eine einfache Kopie eignet. Wenn Sie in ein bestimmtes Blatt kopieren möchten, benennen Sie `destWs` mit `destWs.setName("TargetSheet")` um.

## Schritt 3: Definieren des Quellbereichs, der die Pivot‑Tabelle enthält

Eine Pivot‑Tabelle belegt einen rechteckigen Zellblock. Sie müssen den genauen Bereich angeben; andernfalls werden nur Rohdaten kopiert. In diesem Beispiel gehen wir davon aus, dass die Pivot‑Tabelle **A1:G20** belegt, Sie können die Adresse jedoch an Ihre Datei anpassen.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Warum das funktioniert:**  
Wenn Sie `createRange` auf der `Cells`‑Sammlung des Arbeitsblatts aufrufen, schließt Aspose.Cells die Pivot‑Definition, deren Cache und sämtliche Formatierungen ein. Das ist das Kernstück, um **wie man eine Pivot‑Tabelle kopiert** korrekt umzusetzen.

## Schritt 4: Kopieren des definierten Bereichs in das Zielblatt

Verwenden Sie nun die Methode `copy`, um den Bereich zu duplizieren. Die Methode kopiert alles innerhalb des Bereichs, einschließlich der Pivot‑Definition, Formeln und Stile.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Wichtiger Hinweis:**  
Wenn Sie nur die Daten ohne die Pivot‑Tabelle benötigen, könnten Sie `srcRange.copyData` verwenden. Für ein echtes **Pivot‑Tabelle kopieren** müssen Sie jedoch den gesamten Bereich wie oben gezeigt kopieren.

## Schritt 5: Speichern der Zielarbeitsmappe

Abschließend schreiben Sie die neue Arbeitsmappe auf die Festplatte. Die resultierende Datei enthält eine voll funktionsfähige Pivot‑Tabelle, die der Quelle identisch ist.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Das Ausführen des Programms erzeugt `CopyPivotResult.xlsx` mit derselben Pivot‑Layout, denselben Filtern und denselben Berechnungen wie die Originaldatei.

## Erwartete Ausgabe

Wenn Sie `CopyPivotResult.xlsx` in Excel öffnen:

* Die Pivot‑Tabelle erscheint bei **A1:G20** im ersten Blatt.
* Alle Zeilen‑/Spaltenfelder, Filter und Wertefelder sind intakt.
* Das Aktualisieren der Pivot‑Tabelle aktualisiert dieselbe Datenquelle wie die Quellarbeitsmappe (sofern die Quelldaten eingebettet sind).

## Randfälle und praktische Tipps

| Situation | Wie man damit umgeht |
|-----------|----------------------|
| **Pivot erstreckt sich über mehr Spalten als erwartet** | Verwenden Sie `srcWs.getPivotTables().get(0).getPivotTableArea()`, um die genaue Adresse programmgesteuert zu erhalten. |
| **Quellarbeitsmappe enthält mehrere Pivots** | Durchlaufen Sie `srcWs.getPivotTables()` und kopieren Sie jeden Bereich einzeln, wobei Sie die Zieladressen anpassen. |
| **Große Arbeitsmappen verursachen Speicherbelastung** | Aktivieren Sie `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` bevor Sie die Quelle laden. |
| **Sie müssen nur die Pivot‑Definition kopieren, nicht die Daten** | Löschen Sie nach dem Kopieren die Quell‑Datenzeilen im Ziel mit `destWs.getCells().deleteRows(startRow, count)`. |
| **Zieldatei muss das ursprüngliche Format beibehalten** | Setzen Sie `CopyOptions` mit `options.setPasteType(PasteType.ALL)` für eine Kopie mit voller Treue. |

**Profi‑Tipp:** Überprüfen Sie immer die kopierte Pivot‑Tabelle, indem Sie programmgesteuert `destWs.getPivotTables().get(0).refresh()` aufrufen. Das stellt sicher, dass der Cache aktuell ist, insbesondere wenn die Quelldaten in einer externen Verbindung liegen.

## Vollständiges ausführbares Beispiel

Unten finden Sie das gesamte Programm, das Sie in Ihre IDE kopieren‑und‑einfügen können. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad auf Ihrem Rechner.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Das Ausführen dieses Codes wird die **Pivot‑Tabelle kopieren** exakt wie beschrieben und demonstriert den unkompliziertesten Weg, **copy range aspose cells** zu nutzen, während die Pivot‑Funktionalität erhalten bleibt.

## Fazit

Sie wissen jetzt, wie Sie **Pivot‑Tabelle kopieren** in Java mit Aspose.Cells, vom Laden der Quellarbeitsmappe bis zum Speichern der Zieldatei. Der Leitfaden hat die wesentlichen Schritte behandelt, erklärt, warum jeder Schritt wichtig ist, und häufige Randfälle adressiert.  

Als Nächstes könnten Sie erkunden:

* **wie man Pivot‑Tabellen** über verschiedene Arbeitsblätter derselben Arbeitsmappe hinweg kopiert
* Verwendung von **copy range aspose cells**, um Diagramme oder bedingte Formatierungen zu duplizieren
* Automatisierung der Pivot‑Aktualisierung nach dem Kopieren, um Daten aktuell zu halten

Experimentieren Sie gern mit größeren Bereichen, mehreren Pivots oder der Integration dieser Logik in eine umfangreichere Excel‑Verarbeitungspipeline. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Pivot‑Tabelle in Java kopieren – erhalten, nach PPTX exportieren](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Wie man die Datenquelle einer Excel‑Pivot‑Tabelle mit Aspose.Cells für Java aktualisiert: Ein umfassender Leitfaden](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel‑Pivot‑Tabellen‑Manipulation mit Aspose.Cells Java: Ein umfassender Leitfaden](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}