---
category: general
date: 2026-06-21
description: Wie man WRAPCOLS mit Aspose.Cells Java verwendet, um ein Array in Zeilen
  zu konvertieren, eine Formel in eine Zelle zu schreiben und Zellen mit der Formel
  zu füllen – Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: de
og_description: Wie man WRAPCOLS in Java mit Aspose.Cells verwendet, um ein Array
  in Zeilen zu konvertieren, eine Formel in eine Zelle zu schreiben und Zellen mit
  einer Formel zu füllen – alles in einem Leitfaden.
og_title: Wie man WRAPCOLS in Java verwendet – Vollständiges Excel‑WRAPCOLS‑Beispiel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Wie man WRAPCOLS in Java verwendet – Komplettes Excel‑WRAPCOLS‑Beispiel
url: /de/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man WRAPCOLS in Java verwendet – Komplettes Excel WRAPCOLS Beispiel

Haben Sie sich jemals gefragt, **wie man WRAPCOLS** verwendet, wenn Sie ein einfaches Array in eine übersichtliche Tabelle in Excel umwandeln müssen? Sie sind nicht der Einzige. Viele Entwickler stoßen an ihre Grenzen, wenn sie das `WRAPCOLS`‑Funktion zum ersten Mal sehen und denken: „Wie schreibe ich diese Formel eigentlich aus Java in eine Zelle?“ Die gute Nachricht? Es ist ziemlich einfach, sobald man die richtigen Schritte kennt.

In diesem Tutorial gehen wir ein vollständig ausführbares Aspose.Cells‑Java‑Beispiel durch, das **ein Array in Zeilen konvertiert**, die Formel direkt in eine Zelle schreibt und Ihnen zeigt, wie man **Zellen mit Formel füllt** für reale Szenarien. Am Ende haben Sie ein klares Bild des **excel wrapcols example** und können es an Ihre eigenen Projekte anpassen.

## Voraussetzungen

- Java 17 oder höher (der Code funktioniert mit jedem aktuellen JDK).
- Aspose.Cells für Java Bibliothek (Sie können das neueste JAR von Maven Central beziehen).
- Grundlegendes Verständnis von Java‑Syntax und Excel‑Formeln.
- Eine IDE oder ein einfacher Texteditor – keine spezielle Toolchain erforderlich.

Alles bereit? Großartig, lassen Sie uns beginnen.

## Schritt 1: Projekt einrichten und eine Arbeitsmappe laden

Zuerst – erstellen Sie ein neues Maven‑ (oder Gradle‑)Projekt und fügen Sie die Aspose.Cells‑Abhängigkeit hinzu:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Jetzt können wir eine vorhandene Arbeitsmappe laden (oder eine neue erstellen) und das erste Arbeitsblatt holen:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Warum wir eine Arbeitsmappe laden** – Aspose.Cells arbeitet mit einer In‑Memory‑Repräsentation einer Excel‑Datei. Durch das Laden (oder Erstellen) einer Arbeitsmappe erhalten wir Zugriff auf Zellen, Zeilen und Formeln, was für jede **write formula to cell**‑Operation unerlässlich ist.

## Schritt 2: WRAPCOLS‑Formel in eine Zelle einfügen

Das Herzstück des Tutorials liegt in der `WRAPCOLS`‑Funktion. Sie nimmt ein eindimensionales Array und „wrappt“ es in eine angegebene Anzahl von Spalten, wobei der Rest automatisch in neue Zeilen überläuft. Hier ist die Syntax, die wir verwenden werden:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Beachten Sie, dass die Formel ein einfacher String ist, der an `setFormula` übergeben wird. Aspose.Cells übernimmt die schwere Arbeit – das Parsen der Formel, deren Auswertung und das Überlaufen der Ergebnisse in das Arbeitsblatt. Dies ist der direkteste Weg, **Zellen mit Formel zu füllen**, ohne manuell über Zeilen und Spalten zu iterieren.

### Was die Formel macht

- `{1,2,3}` – ein wörtliches Array, das drei Zahlen enthält.
- `2` – die Anzahl der Spalten pro Zeile.
- Ergebnis:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (leer)

Wenn Sie stattdessen drei Spalten möchten, ändern Sie einfach das zweite Argument zu `3`, und das Array würde eine einzelne Zeile füllen.

## Schritt 3: Arbeitsmappe speichern und Ausgabe überprüfen

Da die Formel jetzt in **A1** steht, speichern wir die Arbeitsmappe auf die Festplatte, damit Sie sie in Excel öffnen und das Überlaufen sehen können:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Öffnen Sie `output.xlsx` und Sie sehen genau das, was der Kommentar beschrieben hat – zwei Spalten in der ersten Zeile und den verbleibenden Wert in der zweiten Zeile. Das ist das Wesentliche des **excel wrapcols example**.

## Schritt 4: Beispiel erweitern – Größere Arrays konvertieren

Echte Projekte arbeiten selten nur mit drei Zahlen. Angenommen, Sie haben eine größere Sammlung, z. B. `{10,20,30,40,50,60,70}` und möchten drei Spalten pro Zeile. So würden Sie den Code anpassen:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Jetzt beginnt das Überlaufen bei **C5** und erzeugt:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Dies zeigt, wie Sie **convert array to rows** dynamisch durchführen können, indem Sie einfach den Formel‑String anpassen. Keine Schleifen, keine manuellen Zuweisungen von Zellen – Aspose.Cells erledigt den Rest.

## Schritt 5: Umgang mit Randfällen und häufigen Stolperfallen

### 1. Leere Arrays

Wenn das Array‑Literal leer ist (`{}`), gibt `WRAPCOLS` einen `#VALUE!`‑Fehler zurück. Um zu verhindern, dass Ihr Blatt beschädigt wird, schützen Sie die Formelerstellung:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Nicht‑numerische Daten

`WRAPCOLS` funktioniert auch mit Text. Zum Beispiel erzeugt `WRAPCOLS({"A","B","C","D"},2)` ein zweispaltiges Layout von Zeichenketten. Denken Sie nur daran, Zeichenketten im Array‑Literal zu quoten.

### 3. Kompatibilität

Die `WRAPCOLS`‑Funktion ist in Excel 365 und Excel 2019+ (Office 2019, Excel für das Web) verfügbar. Wenn Sie ältere Versionen unterstützen müssen, müssen Sie auf manuelles Schleifen zurückgreifen oder eine andere spill‑kompatible Funktion verwenden.

## Schritt 6: Praktische Tipps und Pro‑Tricks

- **Pro‑Tipp:** Verwenden Sie `Cell.setFormulaLocal`, wenn Sie einen lokalspezifischen Trennzeichen (Komma vs. Semikolon) je nach Regionseinstellungen des Benutzers benötigen.
- **Achten Sie auf:** Überschreiben vorhandener Daten. Der Spill‑Bereich ersetzt jeden Inhalt, der bereits im Zielbereich existiert.
- **Hinweis zur Leistung:** Das Setzen einer Formel ist günstig; die eigentliche Arbeit erfolgt, wenn Sie die Arbeitsmappe **speichern** oder **neu berechnen**. Wenn Sie Tausende von Formeln erzeugen, sollten Sie die automatische Berechnung deaktivieren (`wb.calculateFormula()` später), um die Verarbeitung zu beschleunigen.

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette, sofort ausführbare Java‑Klasse, die alles, was wir besprochen haben, integriert:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Erwartete Ausgabe:** Öffnen Sie `output.xlsx` und Sie sehen drei unterschiedliche Spill‑Bereiche:

- **A1:B2** – Zahlen 1‑3 in zwei Spalten gewrappt.
- **C5:E7** – Zahlen 10‑70 in drei Spalten gewrappt.
- **G1:H2** – Fruchtnamen in zwei Spalten gewrappt.

## Fazit

Wir haben gerade **wie man WRAPCOLS** mit Aspose.Cells für Java verwendet, gezeigt, wie man **convert array to rows**, **write formula to cell** und **populate cells with formula** auf eine saubere, wiederholbare Weise. Der Ansatz eliminiert mühsames Schleifen, nutzt das native Spill‑Verhalten von Excel und hält Ihren Code kompakt.

Bereit für die nächste Herausforderung? Versuchen Sie, `WRAPCOLS` mit dynamischen Datenquellen zu kombinieren – vielleicht Werte aus einer Datenbank zu holen, den Array‑String zur Laufzeit zu erstellen und Excel die Layout‑Arbeit erledigen zu lassen. Sie können auch mit anderen Spill‑Funktionen wie `SEQUENCE` oder `FILTER` experimentieren, um noch umfangreichere Berichte zu erstellen.

Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar oder stöbern Sie in der umfangreichen Dokumentation von Aspose. Viel Spaß beim Programmieren und genießen Sie die Leistungsfähigkeit moderner Excel‑Formeln direkt aus Java! 

![Beispiel für die Verwendung von wrapcols](/images/wrapcols-demo.png "wie man wrapcols in Java verwendet – Screenshot der überlaufenden Daten")

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält komplette funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Zellbereiche in Excel mit Aspose.Cells für Java auswählt (2023‑Leitfaden)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [Wie man eine aktive Zelle in Excel mit Aspose.Cells für Java festlegt: Ein vollständiger Leitfaden](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Wie man Zeilen in Excel‑Arbeitsmappen mit Aspose.Cells für Java einfügt](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}