---
category: general
date: 2026-11-22
description: Lernen Sie, wie Sie wrapcols in Java verwenden, um einen Bereich in Spalten
  zu konvertieren, mithilfe von Aspose.Cells. Dieser Leitfaden führt Sie Schritt für
  Schritt durch die Wrap‑Columns‑Excel‑Funktion.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: de
lastmod: 2026-11-22
og_description: Wie man wrapcols in Java verwendet, um einen Bereich in Spalten umzuwandeln.
  Folgen Sie diesem Tutorial, um die Wrap‑Columns‑Excel‑Funktion mit Aspose.Cells
  zu meistern.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: Wie man wrapcols in Java verwendet – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Wie man wrapcols in Java mit Aspose.Cells verwendet
url: /de/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man wrapcols in Java mit Aspose.Cells verwendet

Wenn Sie **how to use wrapcols** benötigen, um Daten in einer Excel‑Arbeitsmappe neu zu strukturieren, zeigt dieses Tutorial den vollständigen Prozess. Sie sehen, wie die WRAPCOLS‑Formel einen vertikalen Bereich in eine Reihe von Spalten umwandelt, wodurch das nebeneinander‑Anzeigen von Listen erleichtert wird.

Der Leitfaden deckt alles ab, was Sie benötigen: Laden einer Arbeitsmappe, Anwenden der WRAPCOLS‑Formel und Speichern des Ergebnisses. Es sind keine externen Referenzen erforderlich, sodass Sie den Code kopieren und sofort ausführen können. Unterwegs erklären wir außerdem die *wrap columns excel function* und demonstrieren, wie man **convert range to columns** für gängige Reporting‑Szenarien durchführt.

## Was Sie benötigen

- Java 17 oder neuer  
- Aspose.Cells für Java (neueste Version)  
- Eine Java‑IDE (IntelliJ IDEA, Eclipse oder VS Code)  
- Eine Eingabe‑Excel‑Datei (`input.xlsx`) mit Daten in Spalte A  

## Wie man wrapcols in Java mit Aspose.Cells verwendet

Die folgenden vier Schritte implementieren den **how to use wrapcols**‑Workflow. Jeder Schritt enthält ein Code‑Snippet, eine Erklärung, warum er wichtig ist, und einen Tipp zur Vermeidung häufiger Fallstricke.

### Schritt 1: Arbeitsmappe laden

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Warum dieser Schritt wichtig ist*: `Workbook` ist der Einstiegspunkt für alle Excel‑Operationen in Aspose.Cells. Das Laden der Datei gibt Ihnen Zugriff auf Arbeitsblätter, Zellen und Formeln.  

**Pro‑Tipp**: Verwenden Sie während der Entwicklung einen absoluten Pfad, um `FileNotFoundException` zu vermeiden. Wechseln Sie zu einem relativen Pfad, sobald das Projekt verpackt ist.

### Schritt 2: Auf das erste Arbeitsblatt zugreifen

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Das erste Arbeitsblatt (`index 0`) enthält typischerweise die Daten, die Sie transformieren möchten. Wenn Ihre Daten sich auf einem anderen Blatt befinden, ändern Sie den Index oder verwenden Sie `get("SheetName")`.  

**Warum dieser Schritt wichtig ist**: Die Arbeit mit dem richtigen Arbeitsblatt stellt sicher, dass die WRAPCOLS‑Formel den beabsichtigten Bereich referenziert.

### Schritt 3: WRAPCOLS‑Formel festlegen

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` ist die **wrap columns excel function**, die die Werte aus `range` über die angegebene Anzahl von Spalten verteilt. In diesem Beispiel nehmen wir die Werte aus `A1:A10` und wickeln sie in drei Spalten, beginnend bei `A1`.  

**Warum dieser Schritt wichtig ist**: Die Formel übernimmt die schwere Arbeit – kein manuelles Durchlaufen oder Array‑Handling ist erforderlich.  

**Tipp für convert range to columns**: Passen Sie das zweite Argument (`3`) an die benötigte Spaltenzahl an. Wenn die Länge des Bereichs kein Vielfaches der Spaltenanzahl ist, enthält die letzte Spalte die verbleibenden Elemente.

### Schritt 4: Arbeitsmappe speichern

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Beim Speichern wird die WRAPCOLS‑Formel in `output.xlsx` geschrieben. Wenn Sie die Datei in Excel öffnen, wird die Formel ausgewertet und die Daten werden in Spalten angezeigt.  

**Warum dieser Schritt wichtig ist**: Das Persistieren der Arbeitsmappe ermöglicht es Ihnen, das Ergebnis zu überprüfen und die Datei mit Nicht‑Java‑Benutzern zu teilen.

![Wrapcols formula applied in Excel](wrapcols-example.png){: .align-center alt="Wie man wrapcols in Excel verwendet Screenshot"}

### Erwartete Ausgabe

Wenn Sie `output.xlsx` öffnen, enthalten die Zellen `A1:C4` (oder so viele Zeilen, wie nötig) die ursprüngliche Liste aus `A1:A10`, verteilt auf drei Spalten. Das Layout sieht folgendermaßen aus:

| A | B | C |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
| Item 10 |   |   |

Die **wrap columns excel function** füllt leere Zellen automatisch mit Leerzeichen, sodass Sie keinen zusätzlichen Aufräumcode benötigen.

## Verständnis der wrap columns excel function

Die WRAPCOLS‑Formel ist Teil der dynamischen Array‑Funktionen von Excel, die in Excel 365 eingeführt wurden. Sie funktioniert ähnlich wie `TEXTSPLIT`, konzentriert sich jedoch auf die spaltenweise Verteilung.  

- **Syntax**: `=WRAPCOLS(source_range, columns)`  
- **Parameter**:  
  - `source_range` – der vertikale Bereich, den Sie neu strukturieren möchten.  
  - `columns` – die Anzahl der Spalten, in die die Daten gewickelt werden sollen.  

Wenn Sie `=WRAPCOLS(A1:A10, 3)` aufrufen, behandelt Excel die Quelle als ein eindimensionales Array und füllt zuerst die erste Spalte, dann die zweite usw., bis alle Werte platziert sind. Das macht **how to use wrapcols** zu einem perfekten Werkzeug, um eine einspaltige Liste in einen mehrspaltigen Bericht zu konvertieren, ohne VBA.

## Convert range to columns ohne Formeln (optional)

Wenn Sie die **convert range to columns**‑Operation vollständig in Java durchführen möchten – ohne die Berechnungs‑Engine von Excel zu nutzen – können Sie die Quellwerte einlesen, ein zweidimensionales Array erstellen und es manuell zurückschreiben:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

Dieses Snippet zeigt eine alternative Methode, **convert range to columns** durchzuführen, wenn Sie die volle Kontrolle über die Ausgabe benötigen (z. B. benutzerdefinierte Formatierung pro Spalte anwenden). Die Verwendung der **wrap columns excel function** über WRAPCOLS ist jedoch in der Regel knapper und lässt Excel die Neuberechnung automatisch übernehmen.

## Randfälle und bewährte Methoden

- **Leere Zellen**: WRAPCOLS behandelt leere Zellen als Leerzeichen. Wenn Ihr Quellbereich Lücken enthält, werden diese im Ergebnis beibehalten.  
- **Dynamische Bereiche**: Verwenden Sie einen benannten Bereich oder einen Tabellenbezug (`Table1[Column]`), damit die Formel sich anpasst, wenn Zeilen hinzugefügt werden.  
- **Leistung**: Das Anwenden der Formel ist O(1), da Excel sie lazy auswertet. Die oben gezeigte programmatische Umwandlung ist O(n) und kann bei sehr großen Bereichen langsamer sein.  
- **Versionskompatibilität**: Die WRAPCOLS‑Funktion erfordert Excel 365 oder neuer. Wenn Sie ältere Versionen unterstützen müssen, verwenden Sie die Java‑seitige Umwandlungsmethode.

## Wie man wrapcols in anderen Szenarien verwendet

- **Reporting‑Dashboards**: Wandeln Sie eine vertikale Liste von KPI‑Namen in eine kompakte Tabelle mit drei Spalten pro Zeile um.  
- **Daten‑Eingabeformulare**: Konvertieren Sie eine Spalte von Benutzereingaben in ein nebeneinander‑Layout für einen leichteren visuellen Vergleich.  
- **Export nach CSV**: Nach Anwendung von WRAPCOLS speichern Sie die Arbeitsmappe als CSV, um eine durch Trennzeichen getrennte Ansicht zu erhalten, die dem Spaltenlayout entspricht.

Jeder dieser Fälle folgt dem gleichen **how to use wrapcols**‑Muster: Laden, Referenzieren, Formel setzen, Speichern.

## Fazit

Sie wissen jetzt, **how to use wrapcols** in Java mit Aspose.Cells zu **convert range to columns** effizient zu nutzen. Durch das Anwenden der `WRAPCOLS`‑Formel nutzen Sie die native *wrap columns excel function*, halten Ihren Code kompakt und geben Excel die volle Kontrolle über Berechnung und Anzeige.  

Experimentieren Sie mit unterschiedlichen Spaltenzahlen, dynamischen Bereichen oder der optionalen reinen Java‑Umwandlung, um den Anforderungen Ihres Projekts gerecht zu werden. Wenn Sie diese Technik beherrschen, wird das Umformen von Daten in Excel zu einer Ein‑Zeilen‑Operation statt zu einer manuellen Aufgabe.

---


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man wrapcols verwendet, um eine Liste in mehrere Spalten in Java zu konvertieren](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [Wie man WRAPCOLS in Java verwendet – Vollständiger Leitfaden zu Excel‑Array‑Formeln](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [Wie man WRAPCOLS in Java verwendet – Vollständiges Excel‑WRAPCOLS‑Beispiel](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}