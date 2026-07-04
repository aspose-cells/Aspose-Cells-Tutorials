---
category: general
date: 2026-07-03
description: Wie man Excel-Dateien mit Java gestaltet. Erfahren Sie, wie Sie das Datumsformat
  einer Spalte in Excel formatieren, Zahlenformat in Excel anwenden, DataTable nach
  XLSX exportieren und DataTable mit Aspose Cells in Excel importieren.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: de
og_description: Wie man Excel-Dateien in Java gestaltet. Dieses Tutorial zeigt, wie
  man das Datumsformat einer Spalte in Excel formatiert, das Zahlenformat in Excel
  anwendet, DataTable nach XLSX exportiert und DataTable in Excel importiert.
og_title: Wie man Excel gestaltet – Java-Leitfaden für benutzerdefinierte Spaltenformatierung
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Wie man Excel formatiert – DataTable mit benutzerdefinierter Formatierung in
  Java importieren
url: /de/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Excel stylt – DataTable mit benutzerdefiniertem Format in Java importieren

Haben Sie sich jemals gefragt, **wie man Excel**-Tabellen programmgesteuert stylt, ohne die Datei manuell zu öffnen? Sie sind nicht allein. Viele Entwickler müssen Berichte erzeugen, bei denen die erste Spalte fett, die zweite Spalte Datumswerte anzeigt und der Rest ein sauberes Layout hat. In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das **eine DataTable in Excel importiert**, eine fette Kopfzeile anwendet, eine Datumsspalte formatiert und schließlich **DataTable nach XLSX exportiert**.  

Wir verwenden Aspose.Cells für Java, aber die Konzepte lassen sich auf jede Bibliothek übertragen, die das Arbeiten mit Styles ermöglicht. Am Ende haben Sie ein wiederverwendbares Muster für **apply number format Excel** Zellen, **format column date Excel** und das Ausliefern einer professionell gestalteten Arbeitsmappe an Ihre Nutzer.

## Voraussetzungen

- Java 17 (oder ein aktuelles JDK)  
- Aspose.Cells für Java 23.9 oder neuer (die kostenlose Testversion reicht aus)  
- Eine `DataTable`‑ähnliche Struktur (das Beispiel verwendet ein einfaches Mock‑Objekt)  
- Ihre bevorzugte IDE (IntelliJ IDEA, Eclipse, VS Code…)

Keine zusätzlichen Maven‑Plugins sind erforderlich; fügen Sie einfach die Aspose.Cells‑JAR zu Ihrem Klassenpfad hinzu.

---

## Schritt 1: Die Quell‑DataTable beschaffen – Vorbereitung „Export DataTable to XLSX“

Bevor wir **datatable into excel importieren** können, benötigen wir ein `DataTable`‑Objekt, das die zu exportierenden Daten repräsentiert. In realen Projekten holen Sie diese möglicherweise aus einer Datenbank, einer CSV‑Datei oder einer API. Für dieses Tutorial mocken wir eine kleine Tabelle:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Warum das wichtig ist:** Wenn die Daten von Anfang an korrekt sind, kann sich die restliche Styling‑Logik ausschließlich auf die Präsentation konzentrieren und nicht auf Datenaufbereitung.

---

## Schritt 2: Ein Array für Style‑Definitionen jeder Spalte erstellen

Aspose.Cells ermöglicht das Übergeben eines **Style[]**‑Arrays beim Import einer `DataTable`. Jeder Eintrag entspricht einer Spalte und bestimmt, wie diese Spalte nach dem Import aussieht. Wir allozieren das Array basierend auf der Spaltenanzahl:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tipp:** Wenn Sie viele Spalten haben, bauen Sie das Array in einer Schleife auf und verwenden Sie ein einzelnes `Style`‑Objekt dort, wo das Format identisch ist. Das reduziert den Speicherverbrauch.

---

## Schritt 3: Die Styles definieren – fette Kopfzeile & Datumsformatierung

Jetzt beantworten wir die klassische **format column date excel**‑Frage und demonstrieren gleichzeitig **apply number format excel** für andere Spalten.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Was passiert hier?**  
- `StyleNumberFormat.DATE` weist Excel an, den Zellenwert als kurzes Datum zu behandeln (z. B. *31/01/2024*).  
- `StyleNumberFormat.CURRENCY_USD` fügt automatisch das `$`‑Symbol und zwei Dezimalstellen hinzu.  
- Das Setzen der Schriftart auf fett in der ersten Spalte lässt die Kopfzeile hervorstechen – ein häufiger Bedarf, wenn Sie **how to style excel**‑Tabellen für bessere Lesbarkeit gestalten.

> **Randfall:** Enthält Ihre Quelldaten bereits formatierte Zeichenketten, müssen Sie diese ggf. in `java.util.Date`‑Objekte konvertieren, bevor Sie importieren; sonst behandelt Excel sie als reinen Text.

---

## Schritt 4: Eine neue Arbeitsmappe erstellen und das erste Arbeitsblatt öffnen

Eine frische Arbeitsmappe gibt uns eine saubere Leinwand. Wir holen das erste Arbeitsblatt, in das der Import erfolgen wird.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Warum eine neue Arbeitsmappe?** Der Start von Grund auf stellt sicher, dass keine verbliebenen Styles oder versteckten Zeilen das Endergebnis beeinflussen – entscheidend, wenn Sie **how to style excel**‑Dateien konsistent über mehrere Durchläufe hinweg erzeugen.

---

## Schritt 5: Die DataTable mit den Spalten‑Styles importieren

Hier ist das Herzstück: Die `DataTable` in das Blatt einlesen und dabei das zuvor erstellte Style‑Array anwenden.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Erklärung:**  
- `importDataTable` kopiert sowohl die Kopfzeile als auch die Datenzeilen.  
- Das `columnStyles`‑Array ist spaltenweise ausgerichtet, sodass die Kopfzeile der ersten Spalte fett wird, die zweite Spalte Datumswerte zeigt und die dritte Spalte als Währung erscheint.  
- Diese eine Zeile ersetzt dutzende manuelle Zell‑für‑Zell‑Formatierungen und zeigt, wie man **apply number format excel** programmatisch umsetzt.

---

## Schritt 6: Die formatierte Arbeitsmappe speichern – Abschluss „Export DataTable to XLSX“

Zum Schluss speichern wir die Arbeitsmappe auf dem Datenträger. Passen Sie den Pfad an einen beschreibbaren Ordner auf Ihrem Rechner an.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Öffnen Sie die Datei in Excel und Sie sollten sehen:

- Spaltenkopf **ID** fett dargestellt.  
- Spalte **OrderDate** im Datumsformat (z. B. *27/04/2024*).  
- Spalte **Total** mit Dollar‑Zeichen und zwei Dezimalstellen.

> **Pro‑Tipp:** Wenn Sie ältere Excel‑Versionen unterstützen müssen, rufen Sie `workbook.save(outputPath, SaveFormat.XLS)` anstelle des Standard‑XLSX auf.

---

## Schritt 7: Ergebnis prüfen & optionale Anpassungen

Es ist gute Praxis, die erzeugte Datei zu überprüfen, besonders wenn Sie Berichte automatisiert für Stakeholder bereitstellen.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Wenn `isBold` `true` ausgibt, hat Ihre **how to style excel**‑Routine wie gewünscht funktioniert. Von hier aus können Sie:

- Bedingte Formatierung hinzufügen (z. B. Totale > $200 hervorheben).  
- Die oberste Zeile fixieren, um das Scrollen zu erleichtern.  
- Ein Diagramm einfügen, das auf die importierten Daten verweist.

All diese Erweiterungen folgen demselben Muster: `Style` definieren, anwenden und speichern.

---

## Häufige Fragen & Randfälle

| Frage | Antwort |
|----------|--------|
| **Kann ich mehr als eine Spalte auf dieselbe Weise stylen?** | Ja – verwenden Sie eine einzelne `Style`‑Instanz für alle Spalten, die das gleiche Format teilen. |
| **Was passiert, wenn meine DataTable mehr Spalten als Styles hat?** | Jede Spalte ohne entsprechenden Eintrag im `columnStyles`‑Array erhält den Standard‑Style. |
| **Wie ändere ich das Datumsformat zu „dd‑MMM‑yyyy“?** | Verwenden Sie `columnStyles[1].setCustom("#dd-MMM-yyyy#");` anstelle des eingebauten `DATE`. |
| **Gibt es eine Möglichkeit, Spalten nach dem Import automatisch zu skalieren?** | Rufen Sie `worksheet.autoFitColumns();` nach `importDataTable` auf. |
| **Funktioniert das unter Linux/macOS?** | Absolut – Aspose.Cells ist plattformunabhängig, solange ein kompatibles JDK vorhanden ist. |

---

## Fazit

Sie haben nun ein solides End‑zu‑Ende‑Beispiel, wie man **how to style Excel**‑Arbeitsmappen durch **importing datatable into excel**, **format column date excel** und **apply number format excel** mit Java erstellt. Der Code zeigt den kompletten Ablauf vom **export datatable to xlsx** bis zum Öffnen der Datei in Excel und erklärt sowohl das *Was* als auch das *Warum* jedes Schrittes.  

Probieren Sie es aus: Passen Sie das Style‑Array an, fügen Sie weitere Spalten hinzu oder binden Sie eine echte Datenbankabfrage ein. Das gleiche Muster ermöglicht Ihnen, professionelle Berichte per Knopfdruck zu erzeugen – ohne manuelle Nachbearbeitung.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Bild‑Alt‑Text: „Styled Excel worksheet created using Java and Aspose.Cells, showing bold header and formatted date column.“*


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}