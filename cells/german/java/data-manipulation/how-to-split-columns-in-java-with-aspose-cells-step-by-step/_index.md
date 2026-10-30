---
category: general
date: 2026-10-07
description: Wie man Spalten mit Aspose.Cells für Java aufteilt. Erfahren Sie, wie
  Sie Zeichenketten in Spalten aufteilen, Excel‑Formeln automatisieren und Formeln
  in eine Zelle schreiben – in wenigen Codezeilen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: de
lastmod: 2026-10-07
og_description: Wie man Spalten in Java mit Aspose.Cells aufteilt. Dieses Tutorial
  zeigt, wie man einen String in Spalten aufteilt, die Auswertung von Excel‑Formeln
  automatisiert und eine Formel in eine Zelle schreibt.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Wie man Spalten in Java mit Aspose.Cells aufteilt – Schnelltutorial
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Wie man Spalten in Java mit Aspose.Cells aufteilt – Schritt‑für‑Schritt‑Anleitung
url: /de/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Spalten in Java mit Aspose.Cells aufteilt – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **Spalten aufteilen** in einem Excel-Arbeitsblatt programmgesteuert müssen, zeigt Ihnen diese Anleitung den kompletten Prozess mit Aspose.Cells für Java. Sie lernen außerdem, wie man **String in Spalten aufteilt**, **Excel‑Formeln automatisiert** auswertet und **eine Formel in eine Zelle schreibt** mit kompakt­em, produktionsreifem Code.

Programmgesteuertes Aufteilen von Spalten eliminiert manuelles Kopieren‑Einfügen, reduziert Fehler und ermöglicht groß­skalige Daten­transformationen. Am Ende dieses Tutorials können Sie Formeln on‑the‑fly erzeugen, ändern und auswerten, sodass Excel zu einem echten Teil Ihres Java‑Backends wird.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Java 17 oder neuer installiert.
* Maven 3.8+ (oder Gradle) für die Abhängigkeitsverwaltung.
* Eine Aspose.Cells for Java Lizenz (die kostenlose Evaluierungsversion funktioniert zum Lernen).
* Grundlegende Kenntnisse in Java‑Syntax und Excel‑Konzepten.

Falls eines dieser Elemente fehlt, installieren Sie es zuerst; die Code‑Beispiele gehen von einem Standard‑Maven‑Projekt aus.

## Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen

Fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu. Damit wird die neueste stabile Aspose.Cells‑Bibliothek eingebunden.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Warum dieser Schritt wichtig ist:** Die Bibliothek stellt die Klassen `Workbook`, `Worksheet` und `Cell` bereit, die zum Manipulieren von Excel‑Dateien ohne Microsoft Office erforderlich sind. Ohne die Abhängigkeit lässt sich der Code nicht kompilieren.

## Schritt 2: Erstellen Sie eine Arbeitsmappe und wählen Sie das erste Arbeitsblatt aus

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Das Objekt `Workbook` repräsentiert die gesamte Excel‑Datei. Das erste Arbeitsblatt zu öffnen sorgt für einen vorhersehbaren Ausgangspunkt für die Formel, die wir schreiben werden.

## Schritt 3: Schreiben Sie die WRAPCOLS‑Formel in eine Zielzelle

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Warum wir `WRAPCOLS` verwenden:** Die integrierte Excel‑Funktion `WRAPCOLS` bricht einen einzelnen Textwert automatisch in eine definierte Anzahl von Spalten auf und berücksichtigt dabei Wortgrenzen intelligent. Dies ist der zuverlässigste Weg, **String in Spalten aufzuteilen**, ohne eigene Parsing‑Logik zu schreiben.

## Schritt 4: Erzwingen Sie die Berechnung der Formel in der Arbeitsmappe

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Der Aufruf von `calculateFormula()` **automatisiert die Excel‑Formel**‑Auswertung auf der Serverseite. Ohne diesen Aufruf würde die Zelle weiterhin den Formel‑Text enthalten, nicht die berechneten Werte.

## Schritt 5: Ergebnis abrufen und anzeigen

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Wenn Sie das Programm ausführen, gibt die Konsole aus:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Die erzeugte Datei `SplitColumnsResult.xlsx` zeigt die drei Spalten, die mit dem aufgeteilten Text gefüllt sind.

## Verstehen der WRAPCOLS‑Funktion

* **Syntax:** `WRAPCOLS(text, columns, [delimiter])`
* **Parameter:**
  * `text` – der String, den Sie aufteilen möchten.
  * `columns` – die Anzahl der Spalten, über die der Text verteilt werden soll.
  * `delimiter` (optional) – das Zeichen, das zum Trennen des Strings verwendet wird; Standard ist ein Leerzeichen.
* **Rückgabewert:** Ein Array, das in benachbarte Zellen „ausläuft“, wobei jedes Element einen Teil des ursprünglichen Textes enthält.

Da die Funktion horizontal ausläuft, müssen Sie die Formel nur in die linkeste Zelle schreiben (A1 im Beispiel). Excel füllt automatisch B1, C1, … nach Bedarf.

## Häufige Variationen und Randfälle

| Situation | Empfohlene Anpassung |
|-----------|----------------------|
| **Variable Spaltenanzahl** | Ersetzen Sie die fest codierte `3` durch eine Variable: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Benutzerdefinierter Trenner** | Verwenden Sie das dritte Argument, z. B. `=WRAPCOLS(A2,4,",")` um an Kommas zu trennen. |
| **Leerer Quell‑String** | Die Funktion gibt leere Zellen zurück; prüfen Sie vor dem Setzen der Formel, dass der String nicht `null` oder leer ist. |
| **Große Datensätze** | Wenden Sie die Formel in einer Schleife für jede Zeile an und rufen Sie anschließend einmal `calculateFormula()` nach der Schleife auf, um die Leistung zu verbessern. |
| **Nicht‑ASCII‑Zeichen** | WRAPCOLS funktioniert mit Unicode; stellen Sie sicher, dass Ihre Java‑Quelldatei als UTF‑8 gespeichert ist. |

**Pro‑Tipp:** Wenn Sie viele Zeilen verarbeiten, speichern Sie die Formel in einer String‑Variablen und verwenden Sie sie wieder, um wiederholte String‑Verkettungen zu vermeiden.

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie direkt kopieren und einfügen können. Es enthält Import‑Anweisungen, Ausnahmebehandlung und einen optionalen Speicher‑Vorgang.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Wenn Sie dieses Programm ausführen, erhalten Sie dieselbe Konsolenausgabe wie oben und es wird eine Excel‑Datei geschrieben, die deutlich demonstriert, **wie man Spalten aufteilt**.

## Fehlerbehebung – Checkliste

* **Formel wird nicht ausgewertet** – Stellen Sie sicher, dass `workbook.calculateFormula()` nach dem Setzen der Formel aufgerufen wird.
* **Leere Zellen nach dem Aufteilen** – Vergewissern Sie sich, dass der Quell‑String nicht `null` oder leer ist und dass die Spaltenanzahl größer als null ist.
* **Lizenzausnahme** – Stellen Sie vor dem Erstellen der Arbeitsmappe eine gültige Aspose.Cells‑Lizenzdatei bereit (`License license = new License(); license.setLicense("Aspose.Total.lic");`), um Evaluierungs‑Wasserzeichen zu entfernen.
* **Leistungsprobleme bei großen Tabellen** – Rufen Sie `calculateFormula()` einmal nach dem Schreiben aller Formeln auf, nicht nach jeder einzelnen Zelle.

## Fazit

Sie wissen jetzt **wie man Spalten in Java mit Aspose.Cells aufteilt**, **wie man String in Spalten aufteilt** mit der `WRAPCOLS`‑Funktion, **wie man Excel‑Formeln automatisiert** auswertet und **wie man eine Formel programmgesteuert in eine Zelle schreibt**. Diese Technik eliminiert manuelle Datenvorbereitungsschritte und integriert die leistungsstarken Text‑Verarbeitungs‑Fähigkeiten von Excel direkt in Ihre Java‑Anwendungen.

### Nächste Schritte

* Untersuchen Sie weitere Textfunktionen wie `TEXTSPLIT` und `FILTERXML` für komplexere Parsing‑Szenarien.
* Kombinieren Sie `WRAPCOLS` mit `IFERROR`, um unerwartete Eingaben elegant zu behandeln.
* Integrieren Sie die Lösung in einen Spring Boot‑Service, der CSV‑Daten über REST empfängt und eine befüllte Excel‑Datei zurückgibt.

Durch das Beherrschen dieser Muster können Sie robuste, automatisierte Excel‑Workflows bauen, die mit den Anforderungen Ihres Unternehmens skalieren. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungs‑Ansätze in Ihren eigenen Projekten zu erkunden.

- [aspose cells java – Split Names into Columns](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [How to Delete Blank Columns in Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}