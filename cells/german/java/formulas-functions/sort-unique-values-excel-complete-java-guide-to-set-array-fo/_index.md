---
category: general
date: 2026-06-30
description: Sortieren Sie eindeutige Werte in Excel mit Java. Erfahren Sie, wie Sie
  Formeln festlegen, Formeln neu berechnen und eine eindeutige Liste in Excel mit
  Aspose.Cells erzeugen.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: de
og_description: Einzigartige Werte in Excel mit Java sortieren. Dieser Leitfaden zeigt,
  wie man Formeln festlegt, Formeln neu berechnet und in wenigen Minuten eine eindeutige
  Liste in Excel erstellt.
og_title: Einzigartige Werte sortieren in Excel – Java‑Tutorial für Array‑Formeln
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Eindeutige Werte sortieren in Excel – Vollständiger Java‑Leitfaden zum Setzen
  von Array‑Formeln
url: /de/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sort Unique Values Excel – Komplett‑Java‑Leitfaden zum Setzen von Array‑Formeln

Haben Sie sich jemals gefragt, wie man **sort unique values Excel** ohne das Ziehen von Formeln erledigt? Sie sind nicht der Einzige. In vielen Reporting‑Szenarien benötigen Sie eine saubere, alphabetisch sortierte Liste eindeutiger Einträge, und das manuell zu erledigen ist mühsam.  

Die gute Nachricht? Mit ein paar Zeilen Java‑Code können Sie **set array formula** auf einem Arbeitsblatt setzen und anschließend **recalculate formulas**, sodass der ausgegebene Bereich sich automatisch füllt. In diesem Tutorial führen wir Sie durch alles – vom Erstellen einer Arbeitsmappe bis zum Erzeugen einer eindeutigen Liste im Excel‑Stil – sodass Sie die Lösung direkt in Ihre Anwendung einbetten können.

## Was dieses Tutorial abdeckt

- Einrichtung eines Java‑Projekts mit Aspose.Cells (der Bibliothek, die den Code‑Snippet antreibt).  
- Verwendung der Funktionen `SORT` und `UNIQUE` zusammen, um **generate unique list Excel** Ergebnisse zu erzeugen.  
- Programmgesteuertes Anwenden einer **array formula** auf eine Zelle.  
- Auslösen eines Berechnungslaufs, damit der Schritt **how to recalculate formulas** sofort erfolgt.  
- Überprüfung der Ausgabe und Anpassung der Lösung für Sonderfälle wie leere Zellen oder nicht zusammenhängende Bereiche.

Am Ende dieses Leitfadens können Sie eine einsatzbereite Methode in jeden Java‑Service einbinden, der saubere Excel‑Tabellen exportieren muss.

> **Pro tip:** Wenn Sie bereits Maven verwenden, spart das Hinzufügen von Aspose.Cells als Abhängigkeit Ihnen das manuelle Verwalten von JAR‑Dateien.

---

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Java 8 oder neuer | Aspose.Cells zielt auf Java 8+ ab. |
| Maven (oder Gradle) | Vereinfacht das Verwalten von Abhängigkeiten. |
| Aspose.Cells für Java | Stellt die `Workbook`, `Worksheet` und Formel‑APIs bereit, die wir verwenden. |
| Grundlegende Kenntnisse der Excel‑Funktionen | Das Verständnis von `SORT` und `UNIQUE` hilft Ihnen, den Code anzupassen. |

> *Wenn Sie Aspose.Cells noch nicht haben, fügen Sie dies zu Ihrer `pom.xml` hinzu*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Schritt 1: Erstellen einer neuen Arbeitsmappe (How to Set Formula Begins Here)

Zuerst benötigen wir eine leere Arbeitsmappe. Denken Sie daran als leere Leinwand, auf der wir später **set array formula** in Zelle `A1` setzen.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Warum eine neue Arbeitsmappe erstellen?*  
> Sie garantiert eine saubere Umgebung und verhindert versteckte Formeln, die unsere Testdaten beeinträchtigen könnten.

---

## Schritt 2: Beispieldaten einfügen (Optional aber hilfreich)

Um das Ergebnis klar zu sehen, füllen wir Spalte **B** mit einigen doppelten Einträgen.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Warum Spalte B verwenden?*  
> Die Formel, die wir schreiben, bezieht sich auf `B1:B10`, sodass die Daten dort das klassische Excel‑Beispiel widerspiegeln.

---

## Schritt 3: Setzen einer Array‑Formel, die **Sort Unique Values Excel** erzeugt

Jetzt passiert die Magie. Wir kombinieren `UNIQUE` (um Duplikate zu entfernen) mit `SORT` (um sie alphabetisch zu ordnen). Der resultierende Ausdruck ist eine **array formula**, das heißt, er „spillt“ automatisch in benachbarte Zellen.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Wie es funktioniert

- `UNIQUE(B1:B10)` scannt den Bereich und gibt ein vertikales Array eindeutiger Zeichenketten zurück.  
- `SORT(...)` nimmt dieses Array und sortiert es aufsteigend.  
- Das gesamte in `=` einbetten und `setFormulaArray` aufrufen veranlasst Aspose.Cells, das Ergebnis als **spilled array** zu behandeln, genau wie Excel.

> **Hinweis:** Wenn Sie eine ältere Excel‑Version verwenden, die `SORT` oder `UNIQUE` nicht unterstützt, können Sie auf `SORT(UNIQUE(...))` mit der **LET**‑Funktion zurückgreifen oder klassische Array‑Formeln (`=INDEX(...)`) nutzen. Das Tutorial konzentriert sich auf den modernen Dynamic‑Array‑Ansatz, weil er der sauberste Weg ist, **generate unique list Excel** heute zu erzeugen.

---

## Schritt 4: Formeln neu berechnen, damit der ausgegebene Bereich gefüllt wird

Nachdem die Formel gesetzt ist, wertet die Arbeitsmappe sie nicht automatisch aus. Hier kommt der Schritt **how to recalculate formulas** ins Spiel.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Der Aufruf von `calculateFormula()` zwingt Aspose.Cells, die Excel‑Engine auszuführen und füllt die Zellen `A1`, `A2`, … mit den sortierten eindeutigen Werten.

> *Warum nicht auf lazy evaluation vertrauen?*  
> In einem serverseitigen Kontext benötigen Sie die Daten oft sofort für den Export (CSV, PDF usw.) nach der Berechnung, sodass ein expliziter Aufruf Konsistenz garantiert.

---

## Schritt 5: Ergebnis überprüfen (Optionales Debugging)

Es ist immer sinnvoll, die ausgegebenen Werte in der Konsole auszugeben – besonders wenn Sie sich selbst eine neue API beibringen.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Das Ausführen des Programms gibt aus:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Öffnen Sie `SortedUniqueValues.xlsx` und Sie sehen dieselben Daten, die ab `A1` nach unten „spillen“.

---

## Umgang mit Sonderfällen

### Leere Zellen im Quellbereich

Enthält `B1:B10` leere Zellen, behandelt `UNIQUE` diese als eigenen Eintrag. Um leere Zellen zu ignorieren, wickeln Sie den Bereich mit `FILTER` ein:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Nicht zusammenhängende Daten

Wenn Ihre Daten in mehreren Spalten stehen, können Sie sie vor dem Anwenden von `UNIQUE` mit `CHOOSE` oder `TEXTJOIN` verbinden. Beispiel:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Diese Anpassungen zeigen die Flexibilität von **how to set formula** für komplexere Szenarien.

---

## Vollständiges funktionierendes Beispiel (Alle Schritte kombiniert)

Unten finden Sie das komplette, ausführbare Java‑Programm. Kopieren Sie es in Ihre IDE, fügen Sie die Aspose.Cells‑Abhängigkeit hinzu und starten Sie *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Erwartete Ausgabe** (in der Konsole angezeigt) entspricht der sortierten, deduplizierten Liste, die wir zuvor besprochen haben. Öffnet man die erzeugte Excel‑Datei, sieht man dieselben Werte, die ab `A1` nach unten „spillen“.

---

## Häufig gestellte Fragen

**F: Funktioniert das mit älteren Excel‑Versionen (vor Office 365)?**  
A: Die Funktionen `SORT` und `UNIQUE` gehören zur Dynamic‑Array‑Engine, die in Excel 365 eingeführt wurde. Für Legacy‑Dateien müssten Sie klassische Array‑Formeln wie `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}` verwenden. Aspose.Cells kann diese zwar auswerten, aber die Syntax ist umfangreicher.

**F: Kann ich die Array‑Formel auf einen anderen Bereich als `A1` setzen?**  
A: Absolut. Ändern Sie einfach die Adresse in `cells.get("A1")`. Das ausgegebene Array beginnt immer an der von Ihnen angegebenen Zelle und erweitert sich nach rechts und unten nach Bedarf.

**F: Was, wenn meine Quelldaten größer sind als `B1:B10`?**  
A: Ersetzen Sie den statischen Bereich durch einen dynamischen, z. B. `B:B` oder einen benannten Bereich. Die Formel wird zu `=SORT(UNIQUE(B:B))`. Seien Sie vorsichtig bei Ganzspalten‑Referenzen in sehr großen Tabellen; sie können die Performance beeinträchtigen.

---

## Fazit

Wir haben gerade **how to set formula** in Java behandelt, um **sort unique values Excel** zu erreichen, **how to recalculate formulas** auszuführen und **generate unique list Excel** mithilfe der leistungsstarken API von Aspose.Cells zu erzeugen. Die Schritte sind simpel: Arbeitsmappe erstellen, Daten füllen, eine Array‑Formel anwenden, Berechnung auslösen und das Ergebnis prüfen.  

Ab hier können Sie weiter ausbauen – bedingte Formatierung hinzufügen, nach PDF exportieren oder die Methode in einen Web‑Service integrieren, der fertige Berichte liefert. Der Kern bleibt gleich: Lassen Sie Excel‑Funktionen die schwere Arbeit erledigen und steuern Sie den Prozess mit Java.

Bereit, Ihre Excel‑Automatisierung auf das nächste Level zu heben? Probieren Sie `SORT` gegen `SORTBY` aus, um nach einer zweiten Spalte zu sortieren, oder experimentieren Sie mit `FILTER`, um Zeilen auszuschließen, die nicht den Geschäftsregeln entsprechen. Die Möglichkeiten sind praktisch unbegrenzt.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}