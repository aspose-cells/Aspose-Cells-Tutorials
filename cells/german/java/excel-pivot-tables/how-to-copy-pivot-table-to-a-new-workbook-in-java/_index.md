---
category: general
date: 2026-10-26
description: Erfahren Sie, wie Sie eine Pivot‑Tabelle mit Java in eine neue Arbeitsmappe
  kopieren, dabei die Formatierung und die Pivot‑Definition beibehalten, während Sie
  einen Excel‑Bereich mit Formatierung über Aspose.Cells kopieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: de
lastmod: 2026-10-26
og_description: Pivot‑Tabelle in ein neues Arbeitsbuch in Java mit Aspose.Cells kopieren.
  Dieser Leitfaden zeigt, wie man einen Excel‑Bereich kopiert, die Formatierung beibehält
  und effizient ein leeres Arbeitsbuch erstellt.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Pivot‑Tabelle in ein neues Arbeitsbuch in Java kopieren – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Wie man eine Pivot‑Tabelle in eine neue Arbeitsmappe in Java kopiert
url: /de/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot‑Tabelle in ein neues Arbeitsbuch in Java kopiert

Wenn Sie eine **Pivot‑Tabelle** von einer Excel‑Datei in eine andere **kopieren** müssen, zeigt Ihnen diese Anleitung eine vollständige, ausführbare Lösung. Sie sehen, wie Sie die Pivot‑Definition erhalten, alle Formatierungen beibehalten und häufige Fallstricke beim Kopieren eines Excel‑Bereichs vermeiden.

Das Kopieren einer Pivot‑Tabelle wirft oft Fragen auf, wie *wie man Pivot kopiert*, ohne die Datenquelle zu beschädigen oder Stile zu verlieren. Am Ende dieses Tutorials besitzen Sie ein eigenständiges Java‑Programm, das ein leeres Arbeitsbuch erstellt, den gewünschten Bereich kopiert und das Ergebnis mit intakter Pivot‑Tabelle speichert.

## Was Sie erreichen werden

* Laden eines Quell‑Arbeitsbuchs, das eine Pivot‑Tabelle enthält.  
* **Leeres Arbeitsbuch erstellen**, das die kopierten Daten empfängt.  
* **Excel‑Bereich kopieren**, der die Pivot‑Tabelle enthält, mit Optionen, die Pivot und Formatierung erhalten.  
* Das Ziel‑Datei speichern und prüfen, dass die Pivot‑Tabelle exakt wie das Original funktioniert.

### Voraussetzungen

* Java 17 oder höher.  
* Aspose.Cells für Java (Version 23.10 oder neuer).  
* Grundlegende Kenntnisse von Java‑IDEs (IntelliJ IDEA, Eclipse usw.).  

> **Profi‑Tipp:** Verwenden Sie die kostenlose Aspose.Cells‑Evaluierungslizenz für schnelle Tests; ersetzen Sie sie vor dem Produktionseinsatz durch eine Voll‑Lizenz.

## Pivot‑Tabelle in ein neues Arbeitsbuch kopieren

Der erste Schritt besteht darin, das Quell‑ und Ziel‑Arbeitsbuch einzurichten. Das Ziel‑Arbeitsbuch entsteht dabei durch einen **Leeres Arbeitsbuch erstellen**‑Aufruf, der Ihnen eine saubere Datei mit einem einzigen Arbeitsblatt liefert.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Warum das funktioniert

* `new Workbook()` **erstellt leeres Arbeitsbuch** mit einem Standard‑Blatt und vermeidet das Löschen vorhandener Daten.  
* `CopyOptions` weist Aspose.Cells an, **Pivot‑Tabellen**‑Metadaten zu kopieren, nicht nur Rohwerte. Der Modus `PASTE_ALL` überträgt zudem Zellstile, Zahlenformate und bedingte Formatierungen – erfüllt also die Anforderung **Bereich mit Formatierung kopieren**.  
* `copyRange` führt eine **Excel‑Bereich kopieren**‑Operation aus, die die internen Strukturen der Quelle respektiert, sodass die Pivot‑Tabelle nach dem Kopieren weiterhin funktionstüchtig bleibt.

## Wie man Pivot kopiert, ohne die Formatierung zu verlieren

Verwendet man nur die Standard‑`CopyOptions`, können bei älteren Aspose.Cells‑Versionen einige Stil‑Informationen fehlen. Durch explizites Setzen des Einfügetyps wird garantiert, dass **Bereich mit Formatierung kopieren** beachtet wird.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Das Hinzufügen von `setPasteSpecialType` sorgt dafür, dass Spaltenbreiten, Zeilenhöhen und sogar Datenvalidierungsregeln mit dem Bereich übertragen werden. Das ist besonders nützlich, wenn die Pivot‑Tabelle mehrere Spalten mit benutzerdefinierten Breiten umfasst.

## Leeres Arbeitsbuch vor dem Kopieren erstellen

Manchmal versuchen Entwickler, in ein bereits vorhandenes Arbeitsbuch zu kopieren, das bereits Daten enthält. Das kann zu überlappenden Bereichen oder unerwarteten Überschreibungen führen. Ein **Leeres Arbeitsbuch erstellen**‑Aufruf isoliert den Vorgang:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Falls Sie im Ziel‑Arbeitsbuch mehr als ein Blatt benötigen, können Sie diese nach dem Kopieren hinzufügen:

```java
destWb.getWorksheets().add("Summary");
```

## Excel‑Bereich mit Formatierung mithilfe von CopyOptions kopieren

Über Pivot‑Tabellen hinaus funktioniert das gleiche Muster für jeden **Excel‑Bereich kopieren**, bei dem die Formatierung erhalten bleiben muss – Diagramme, Tabellen oder bedingte Formate.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

Die `CopyOptions`‑Instanz bleibt unverändert, sodass Sie ein konsistentes Verhalten über verschiedene Bereiche hinweg erhalten.

### Randfälle, die zu beachten sind

| Situation                              | Empfohlene Vorgehensweise |
|----------------------------------------|---------------------------|
| Quell‑Arbeitsbuch enthält mehrere Pivot‑Tabellen | Jede Pivot‑Tabelle separat kopieren oder das gesamte Blatt kopieren. |
| Ziel‑Arbeitsbuch enthält bereits Daten | Beim Aufruf von `copyRange` eine nicht kollidierende Startzelle wählen (z. B. „H1“). |
| Pivot‑Datenquelle ist extern (z. B. DB) | Sicherstellen, dass das Ziel‑Arbeitsbuch auf dieselbe externe Datenquelle verweist, oder die Pivot nach dem Kopieren aktualisieren. |
| Großes Arbeitsbuch ( > 10 MB )         | Java‑Heap‑Größe erhöhen (`-Xmx2g`), um `OutOfMemoryError` zu vermeiden. |

## Ergebnis überprüfen

Nach dem Ausführen des Programms öffnen Sie `destination.xlsx`. Sie sollten sehen:

* Das gleiche Pivot‑Tabellen‑Layout wie in `source.xlsx`.  
* Alle Zellfarben, Zahlenformate und Spaltenbreiten sind erhalten.  
* Die Datenquelle der Pivot‑Tabelle verweist weiterhin auf den ursprünglichen Datenbereich innerhalb der neuen Datei, sodass ein Aktualisieren der Pivot die Werte korrekt aktualisiert.

Falls die Pivot‑Tabelle als statische Tabelle erscheint, prüfen Sie, ob `CopyOptions.setPasteType(PasteType.PASTE_ALL)` gesetzt ist. Ohne diese Option behandelt Aspose.Cells die Pivot als reine Daten.

## Fazit

Sie wissen jetzt, wie man **Pivot‑Tabelle** in ein neues Arbeitsbuch in Java kopiert und dabei Formatierung, Datenverbindungen und Blattlayout beibehält. Die vollständige Lösung demonstriert das Laden einer Quelldatei, **Leeres Arbeitsbuch erstellen**, das Konfigurieren von **Excel‑Bereich kopieren**‑Optionen und das Speichern des Ergebnisses.  

Von hier aus können Sie verwandte Themen erkunden, etwa **wie man Pivot über verschiedene Arbeitsblätter kopiert**, Diagramme neben Pivot‑Tabellen einbetten oder die Stapelverarbeitung mehrerer Arbeitsbücher automatisieren. Experimentieren Sie mit den `CopyOptions`‑Einstellungen, um Ihre spezifischen Automatisierungsanforderungen zu erfüllen, und Sie verfügen über ein robustes Excel‑Manipulations‑Toolkit.

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}