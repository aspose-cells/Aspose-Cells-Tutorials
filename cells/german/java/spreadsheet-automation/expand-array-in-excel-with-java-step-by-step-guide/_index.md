---
category: general
date: 2026-07-03
description: Erfahren Sie, wie Sie ein Array in Excel mit Java erweitern. Dieses Tutorial
  behandelt das Erweitern von Arrays in Zeilen, die Anwendung von Expand und das effiziente
  Einfügen von Formeln.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: de
og_description: Array in Excel mit Java erweitern. Folgen Sie dieser Anleitung, um
  zu lernen, wie man expand verwendet, eine Formel in einer Zelle setzt und das Array
  sofort auf Zeilen erweitert.
og_title: Array in Excel mit Java erweitern – Vollständiger Programmierleitfaden
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Array in Excel mit Java erweitern – Schritt‑für‑Schritt‑Anleitung
url: /de/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Array in Excel mit Java erweitern – Vollständiger Programmierleitfaden

Haben Sie sich jemals gefragt, wie man **array in Excel** erweitert, ohne die Zellen manuell zu ziehen? Sie sind nicht allein. Viele Entwickler stoßen auf ein Problem, wenn sie programmgesteuert einen dynamischen Bereich erzeugen müssen – besonders, da die neue Excel‑`EXPAND`‑Funktion noch frisch ist. In diesem Leitfaden zeigen wir Ihnen genau **wie man EXPAND verwendet**, die Formel in ein Arbeitsblatt einfügt und das Ergebnis in die gewünschten Zeilen ausbreitet. Am Ende können Sie **array in Zeilen erweitern** mit einer einzigen Zeile Java‑Code.

Wir gehen ein vollständiges, ausführbares Beispiel mit der Aspose.Cells for Java Bibliothek durch. Keine vagen Verweise, nur konkreter Code, den Sie copy‑paste, kompilieren und ausführen können. Unterwegs erklären wir, warum jeder Schritt wichtig ist, behandeln Sonderfälle wie nicht zusammenhängende Arrays und streuen ein paar Profi‑Tipps ein, die Sie in der offiziellen Dokumentation nicht finden. Bereit? Dann legen wir los.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

* Java 17 (oder ein aktuelles JDK) installiert.
* Maven oder Gradle zur Verwaltung von Abhängigkeiten.
* Eine gültige Aspose.Cells for Java Lizenz (die kostenlose Testversion funktioniert zum Testen).
* Grundlegende Kenntnisse von Excel‑Formeln – wenn Sie bereits `VLOOKUP` oder `SUMIF` verwendet haben, sind Sie startklar.

Wenn Ihnen irgendeiner dieser Punkte unbekannt ist, pausieren Sie und richten Sie ihn zuerst ein; der Rest des Tutorials geht davon aus, dass sie bereit sind.

## Schritt 1: Ihr Maven‑Projekt einrichten und Aspose.Cells hinzufügen

Um alles übersichtlich zu halten, erstellen Sie ein neues Maven‑Projekt namens `ExpandArrayDemo`. Fügen Sie die Aspose.Cells‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro‑Tipp:** Wenn Sie Gradle verwenden, sieht die gleiche Abhängigkeit so aus: `implementation 'com.aspose:aspose-cells:23.12'`.

Sobald Maven das Herunterladen abgeschlossen hat, können Sie Java‑Code schreiben, der **Formel in Zelle setzt**.

## Schritt 2: Ein Workbook erstellen und das erste Arbeitsblatt öffnen

Der erste Code‑Abschnitt spiegelt das Snippet wider, das Sie bereits gesehen haben, aber wir fügen einige Sicherheitsprüfungen und Kommentare hinzu, damit Sie das *Warum* hinter jeder Zeile verstehen.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*Warum das wichtig ist:* Das Instanziieren von `Workbook` reserviert die internen Strukturen, die Aspose zum Verwalten von Zellen, Formeln und Stilen benötigt. Der Zugriff auf das erste Arbeitsblatt ist der häufigste Einstiegspunkt, besonders wenn Sie gerade experimentieren.

## Schritt 3: Die EXPAND‑Formel einfügen – „Wie man Formel einfügt“

Jetzt kommt das Herzstück des Tutorials: **wie man Formel einfügt**, die ein Array erweitert. Die Excel‑`EXPAND`‑Funktion nimmt drei Argumente – Quell‑Array, benötigte Zeilen und benötigte Spalten. In unserem Fall wollen wir `{1,2,3}` zu **5 Zeilen** und **1 Spalte** erweitern.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

Beachten Sie, dass wir `putFormula` statt `putValue` verwendet haben. Das weist Aspose an, den String als echte Excel‑Formel zu behandeln, nicht als reinen Text. Die Methode `putFormula` analysiert den String automatisch und speichert den Formelbbaum intern.

### Warum EXPAND verwenden?

`EXPAND` eliminiert den mühsamen Schritt, den Ausfüll‑Handle zu ziehen. Es funktioniert zudem mit dynamischen Arrays, das heißt, wenn sich Ihr Quell‑Array ändert, aktualisiert sich der ausgegebene Bereich automatisch. Das ist besonders praktisch, wenn Sie Berichte programmgesteuert erzeugen.

## Schritt 4: Berechnung erzwingen – Ergebnis materialisieren

Wenn Sie *Formel in Zelle setzen* über die API, berechnet das Workbook nicht automatisch neu. Sie müssen einen Berechnungsdurchlauf auslösen, damit das Array **in Zeilen erweitert** wird und die Werte im Blatt erscheinen.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

Wenn Sie diesen Schritt überspringen, zeigt Excel beim Öffnen der erzeugten `.xlsx`‑Datei nur die Formel, nicht aber die ausgegebenen Werte, bis Sie **F9** drücken. Durch Aufruf von `calculate()` stellen Sie sicher, dass das Workbook sofort einsatzbereit ist.

## Schritt 5: Das Workbook speichern und Ausgabe prüfen

Schließlich schreiben Sie das Workbook in eine Datei und geben optional die ausgegebenen Werte zur Kontrolle auf der Konsole aus.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Wenn Sie das Programm ausführen, sollte die Konsolenausgabe wie folgt aussehen:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel füllt die restlichen Zeilen mit Nullen, weil das Quell‑Array nur drei Elemente hatte. Das ist das Standardverhalten von `EXPAND`. Wenn Sie lieber leere Zellen statt Nullen möchten, können Sie das Array in `IFERROR` einbetten oder `CHOOSE`‑Tricks verwenden – mehr dazu im Abschnitt „Erweiterte Variationen“ weiter unten.

## Erweiterte Variationen & Sonderfälle

### 1. Ein horizontales Array auf mehrere Spalten erweitern

Wenn Sie **array in Zeilen** *und* Spalten erweitern müssen, ändern Sie einfach das dritte Argument:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

Jetzt erstreckt sich der Bereich auf ein 5 × 3‑Block und füllt fehlende Zellen mit Nullen.

### 2. Einen benannten Bereich als Quelle verwenden

Statt eines literalen `{1,2,3}` können Sie einen benannten Bereich referenzieren, der zur Laufzeit geändert werden kann:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

Stellen Sie sicher, dass `MySourceRange` existiert (Sie können ihn über `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")` erstellen).

### 3. Umgang mit nicht‑numerischen Daten

`EXPAND` funktioniert auch mit Text. Zum Beispiel:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

Die zusätzliche Zeile erscheint als leerer String, nicht als Null.

### 4. Null‑Füllung mit `IFERROR` vermeiden

Wenn Sie lieber leere Zellen statt Nullen sehen möchten, wickeln Sie `EXPAND` in `IFERROR` ein:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

Jetzt werden die Zeilen 4 und 5 wirklich leer sein.

## Häufige Stolperfallen und wie man sie umgeht

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Formel wird nicht neu berechnet** | Vergessen von `ws.getCells().calculate()` | Immer `calculate()` nach `putFormula` aufrufen. |
| **Null‑Werte dort, wo Leere erwartet werden** | `EXPAND` füllt standardmäßig mit Nullen | `IFERROR(..., "")` verwenden oder mit `CHOOSE` einbetten. |
| **Falsche Zelladresse** | Verwendung von `"A0"` oder `"1A"` | Excel‑Adressen beginnen bei 1; Aspose erwartet den Stil `"A1"`. |
| **Bibliotheks‑Versionskonflikt** | Verwendung einer alten Aspose.Cells‑Version, die `EXPAND` nicht unterstützt | Auf die neueste Version (23.12 zum Zeitpunkt des Schreibens) aktualisieren. |

## Vollständiges Beispiel (Alle Schritte kombiniert)

Unten finden Sie das komplette, copy‑paste‑bereite Programm. Speichern Sie es als `ExpandArrayDemo.java`, kompilieren und führen Sie es aus.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Wenn Sie dieses Programm ausführen, entsteht eine Excel‑Datei, in der **Zelle A1** nun die `EXPAND`‑Formel enthält und die Zeilen 1‑5 der Spalte A `1, 2, 3, 0, 0` anzeigen. Öffnen Sie die Datei in Excel, um dasselbe Ergebnis sofort zu sehen – kein manuelles Ziehen erforderlich.

## Fazit

Sie haben gerade gelernt, wie man **array in Excel** mit Java erweitert, **wie man EXPAND verwendet** und die genauen Schritte, um **Formel in Zelle zu setzen** und **array in Zeilen** programmgesteuert zu erweitern. Durch die Nutzung von Aspose.Cells umgehen Sie umständliche UI‑Tricks und lassen den Code die schwere Arbeit übernehmen. Egal, ob Sie eine Reporting‑Engine, ein automatisiertes Dateneingabetool oder einen eigenen Spreadsheet‑Generator bauen – diese Technik spart Ihnen unzählige Stunden.

Was kommt als Nächstes? Versuchen Sie, das statische Array durch einen dynamischen Bereich aus einem anderen Blatt zu ersetzen, experimentieren Sie mit mehrspaltigen Ausgaben oder kombinieren Sie `EXPAND` mit `FILTER` für leistungsstarke Daten­transformationen. Der Himmel ist die Grenze, und jetzt haben Sie ein solides Fundament, auf dem Sie weiter aufbauen können.

Haben Sie Fragen oder möchten Sie einen coolen Anwendungsfall teilen? Hinterlassen Sie ein

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Zeilen in Excel‑Arbeitsmappen mit Aspose.Cells für Java einfügt](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [Wie man eine Spalte in Excel mit Aspose.Cells für Java einfügt – Ein umfassender Leitfaden](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [Wie man Zellbereiche in Excel mit Aspose.Cells für Java auswählt (2023 Leitfaden)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}