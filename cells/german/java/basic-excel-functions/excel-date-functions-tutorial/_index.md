---
date: 2026-07-26
description: Erfahren Sie, wie Sie die Datumsdifferenz in Java mit den Aspose.Cells
  Excel Date Functions berechnen. Enthält Beispiele für end of month, TODAY und DATEDIF.
keywords:
- calculate date difference java
- end of month java
- add excel date formula
- implement excel date functions
- retrieve current date excel
lastmod: 2026-07-26
linktitle: Datumsdifferenz in Java berechnen – Excel Date Functions
og_description: Datumsdifferenz in Java mit den Aspose.Cells Excel Date Functions
  berechnen. Dieser Leitfaden zeigt, wie man Excel Date Formulas hinzufügt, current
  dates abruft und effizient end‑of‑month Werte erhält.
og_image_alt: 'Guide: calculate date difference in Java with Aspose.Cells Excel functions'
og_title: Datumsdifferenz in Java berechnen – Excel Date Functions
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  headline: Calculate Date Difference in Java – Excel Date Functions
  type: TechArticle
- description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  name: Calculate Date Difference in Java – Excel Date Functions
  steps:
  - name: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
    text: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
  - name: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
    text: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
  - name: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
    text: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
  - name: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
    text: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
  type: HowTo
- questions:
  - answer: Create a `Style` object, set its `Number` property to `"dd-MM-yyyy"`,
      and apply it to the target cell via `cell.setStyle(style)`. **`Style` defines
      formatting such as number format, font, and alignment for a cell.**
    question: How do I format a cell to display dates in `dd‑MM‑yyyy` format?
  - answer: Yes, you can retrieve the `Date` objects from two cells, convert them
      to `java.time.LocalDate`, and use `ChronoUnit.DAYS.between(start, end)` for
      precise control.
    question: Can I calculate date differences without using the DATEDIF formula?
  - answer: Absolutely. All built‑in Excel date functions, including DATEDIF and EOMONTH,
      correctly handle leap years according to the Gregorian calendar.
    question: Does Aspose.Cells support leap‑year calculations?
  - answer: Iterate through each `Worksheet` in the `Workbook`, set the required formulas,
      and call `calculateFormula()` once per workbook for optimal performance.
    question: Is it possible to batch‑process multiple worksheets for date calculations?
  - answer: All functions are available from **Aspose.Cells 23.9** onward; the latest
      release (as of 2026) adds performance optimizations for large datasets.
    question: What version of Aspose.Cells is required for these features?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- excel date functions
- aspose cells
- java excel processing
- date calculations
- java tutorial
title: Datumsdifferenz in Java berechnen – Excel Date Functions
url: /de/java/basic-excel-functions/excel-date-functions-tutorial/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Datumsfunktionen‑Tutorial

In diesem umfassenden Tutorial ist **calculate date difference java** unser Hauptfokus. Wir gehen durch, wie man Aspose.Cells für Java verwendet, um mit Excel-Datumsfunktionen zu arbeiten, vom Erstellen von Daten über das Abrufen des aktuellen Tages, das Berechnen von Differenzen bis zum Finden von Monatsenden. Egal, ob Sie eine Reporting-Engine verfeinern oder Tabellen automatisieren, diese Techniken sparen Zeit und reduzieren Fehler. Lassen Sie uns eintauchen!

## Schnelle Antworten
- **Wie berechne ich den Datumsunterschied in Java?** Verwenden Sie die DATEDIF‑Funktion über Aspose.Cells und geben Sie die Einheit an (Tage, Monate, Jahre).  
- **Wie kann ich das heutige Datum in Excel aus Java erhalten?** Rufen Sie die TODAY‑Funktion über Aspose.Cells auf oder setzen Sie den Zellenwert auf `new Date()`.  
- **Welche Methode gibt den letzten Tag eines Monats zurück?** Verwenden Sie die EOMONTH‑Funktion; Aspose.Cells wertet sie automatisch aus.  
- **Benötige ich eine Lizenz für Aspose.Cells?** Ja, eine gültige Lizenz entfernt Evaluationswasserzeichen und schaltet die volle Funktionalität frei.  
- **Welche Java‑Version wird unterstützt?** Aspose.Cells funktioniert mit Java 8 und neuer.

## Was sind Excel-Datumsfunktionen?
Excel-Datumsfunktionen sind integrierte Formeln, die Daten innerhalb eines Arbeitsblatts erstellen, manipulieren oder auswerten. Sie ermöglichen arithmetische Operationen, das Abrufen des aktuellen Datums oder das Berechnen von Monatsgrenzen ohne manuelle Berechnungen. Durch die Verwendung dieser Funktionen können Sie Tage, Monate oder Jahre hinzufügen oder subtrahieren, die Anzahl der Tage zwischen zwei Daten bestimmen und automatisch Schaltjahre sowie unterschiedliche Monatslängen berücksichtigen, wobei die Daten in einem Format bleiben, das Excel versteht und gemäß den regionalen Einstellungen anzeigen kann.

## Warum Aspose.Cells für Java verwenden, um Excel-Datumsfunktionen zu implementieren?
Aspose.Cells unterstützt **50+** Eingabe‑ und Ausgabeformate, verarbeitet Tabellen mit **bis zu 1 000 Seiten** ohne das gesamte Dokument in den Speicher zu laden, und führt Formelberechnungen mit **bis zu 3‑facher** Geschwindigkeit schneller aus als das native Excel auf derselben Hardware. Dieser Leistungszuwachs ist entscheidend für groß‑skalige Datenpipelines.

## Verständnis von Datumsfunktionen in Excel

Excel bietet ein umfangreiches Set an Datumsfunktionen, die komplexe Berechnungen vereinfachen. Im Folgenden heben wir die gebräuchlichsten hervor und zeigen, wie Aspose.Cells sie automatisch auswertet.

### DATE‑Funktion
Die `DATE`‑Funktion erzeugt einen Datumswert aus den Komponenten Jahr, Monat und Tag.  
**Direkte Antwort:** `=DATE(2023, 12, 31)` gibt die Seriennummer für den 31. Dezember 2023 zurück, die Excel als Datum formatiert. In Java können Sie die Formel einer Zelle auf diesen String setzen und Aspose.Cells berechnet das korrekte Datum, wenn die Arbeitsmappe gespeichert oder neu berechnet wird.

### TODAY‑Funktion
Die `TODAY`‑Funktion gibt das aktuelle Systemdatum ohne Zeitanteil zurück.  
**Direkte Antwort:** `=TODAY()` spiegelt stets den Tag wider, an dem die Arbeitsmappe geöffnet oder neu berechnet wird, und ist damit ideal für dynamische Berichte.

### DATEDIF‑Funktion
Die `DATEDIF`‑Funktion berechnet die Differenz zwischen zwei Daten in Tagen, Monaten oder Jahren.  
**Direkte Antwort:** `=DATEDIF(A1, B1, "d")` liefert die Anzahl der Tage zwischen den Daten in den Zellen A1 und B1. Dies ist der Kern unseres **calculate date difference java**‑Szenarios.

### EOMONTH‑Funktion
Die `EOMONTH`‑Funktion gibt den letzten Tag des Monats für ein gegebenes Startdatum zurück, versetzt um eine angegebene Anzahl von Monaten.  
**Direkte Antwort:** `=EOMONTH(A1, 0)` liefert den letzten Kalendertag des Monats, der das Datum in A1 enthält.

## Arbeiten mit Aspose.Cells für Java

Nachdem wir die Grundlagen behandelt haben, sehen wir uns an, wie man Aspose.Cells einrichtet und diese Funktionen programmgesteuert anwendet.

### Einrichtung von Aspose.Cells

Before coding, ensure your environment is ready:

1. **Aspose.Cells herunterladen und installieren:** Besuchen Sie [Aspose.Cells for Java](https://releases.aspose.com/cells/java/) und laden Sie die neueste Version herunter.  
2. **Bibliothek zu Ihrem Projekt hinzufügen:** Fügen Sie die JAR‑Datei Ihrem Build‑Pfad hinzu oder ergänzen Sie die Maven‑Abhängigkeit.  
3. **Lizenzkonfiguration:** Platzieren Sie Ihre Lizenzdatei (`Aspose.Cells.lic`) in den Projektressourcen und laden Sie sie zur Laufzeit, um alle Funktionen freizuschalten.  
4. **Laden Sie die Bibliothek [hier](https://releases.aspose.com/cells/java/) herunter.**

### Wie berechnet man den Datumsunterschied in Java mit Aspose.Cells?

Ein `Workbook` repräsentiert eine komplette Excel‑Datei im Speicher und enthält Arbeitsblätter, Zellen und Stile.  
Laden Sie Ihre Arbeitsmappe, setzen Sie die DATEDIF‑Formel und werten Sie sie aus.  
**Direkte Antwort:** Erstellen Sie ein `Workbook`, weisen Sie einer Zelle `=DATEDIF(A2,B2,"d")` zu, rufen Sie `calculateFormula()` auf und lesen Sie dann den resultierenden numerischen Wert. Dies liefert die genaue Tagesanzahl zwischen zwei Daten in einem einzigen API‑Aufruf.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set the date using the DATE function
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// Get the calculated date value
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Calculated Date: " + calculatedDate);
```

### Verwendung der DATE‑Funktion mit Aspose.Cells

Sie können die `DATE`‑Formel direkt in eine Zelle einbetten, um Daten aus separaten Jahres‑, Monats‑ und Tageswerten zu erstellen.

**Direkte Antwort:** Setzen Sie die Formel einer Zelle auf `=DATE(2024, 5, 15)`; nach dem Aufruf von `calculateFormula()` zeigt die Zelle `15‑May‑2024` gemäß dem Locale der Arbeitsmappe an.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Use the TODAY function to get the current date
worksheet.getCells().get("A1").setFormula("=TODAY()");

// Get the current date value
String currentDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Current Date: " + currentDate);
```

### Arbeiten mit der TODAY‑Funktion

Das programmgesteuerte Abrufen des aktuellen Datums ist unkompliziert.

**Direkte Antwort:** Weisen Sie einer Zelle `=TODAY()` zu, rufen Sie `calculateFormula()` auf, und die Zelle enthält jedes Mal das heutige Datum, wenn die Arbeitsmappe geöffnet oder neu berechnet wird.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set two date values
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// Calculate the difference using DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

// Get the difference in days
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// Print the result
System.out.println("Days Difference: " + daysDifference);
```

### Berechnung von Datumsdifferenzen mit DATEDIF

Für die Kernaufgabe **calculate date difference java** verwenden Sie DATEDIF.

**Direkte Antwort:** Setzen Sie `=DATEDIF(C2,D2,"m")` in eine Zelle, um die Monatsdifferenz zu erhalten, oder ersetzen Sie `"m"` durch `"y"` bzw. `"d"` für Jahre bzw. Tage. Nach der Berechnung lesen Sie das numerische Ergebnis über `cell.getIntValue()` aus.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set a date value
worksheet.getCells().get("A1").putValue("2023-09-07");

// Calculate the end of the month using EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// Get the end-of-month date
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// Print the result
System.out.println("End of Month: " + endOfMonth);
```

### Ermittlung des Monatsendes

Die EOMONTH‑Funktion hilft Ihnen, Monatsenddaten für Abrechnungszyklen oder Berichtszeiträume zu ermitteln.

**Direkte Antwort:** Setzen Sie die Formel einer Zelle auf `=EOMONTH(E2,0)`; nach der Formelauswertung enthält die Zelle den letzten Tag des Monats des Datums in E2.

## Häufige Fallstricke und Tipps
- **Formel‑Neuberechnung:** Rufen Sie stets `workbook.calculateFormula()` auf, nachdem Sie Formeln gesetzt oder geändert haben; andernfalls behalten die Zellen alte Werte bei.  
- **Datums‑Seriennummern:** Excel speichert Daten als Seriennummern; beim Lesen von Werten verwenden Sie `cell.getDateValue()`, um ein `java.util.Date`‑Objekt zu erhalten.  
- **Locale‑Probleme:** Die Datumsformatierung richtet sich nach dem Locale der Arbeitsmappe. Setzen Sie den Stil explizit, wenn Sie ein bestimmtes Anzeigeformat benötigen.  
- **Große Arbeitsmappen:** Für Dateien mit **Hunderten von Tausenden Zeilen** aktivieren Sie `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, um den Speicherverbrauch gering zu halten.  
- `WorkbookSettings` konfiguriert Speicher‑ und Berechnungsoptionen für ein `Workbook`.

## Häufig gestellte Fragen

**Q: Wie formatiere ich eine Zelle, um Daten im Format `dd‑MM‑yyyy` anzuzeigen?**  
A: Erstellen Sie ein `Style`‑Objekt, setzen Sie dessen `Number`‑Eigenschaft auf `"dd-MM-yyyy"` und wenden Sie es mit `cell.setStyle(style)` auf die Zielzelle an.  
**`Style` definiert Formatierungen wie Zahlenformat, Schriftart und Ausrichtung für eine Zelle.**

**Q: Kann ich Datumsdifferenzen berechnen, ohne die DATEDIF‑Formel zu verwenden?**  
A: Ja, Sie können die `Date`‑Objekte aus zwei Zellen abrufen, sie in `java.time.LocalDate` konvertieren und `ChronoUnit.DAYS.between(start, end)` für präzise Steuerung verwenden.

**Q: Unterstützt Aspose.Cells Schaltjahr‑Berechnungen?**  
A: Absolut. Alle integrierten Excel‑Datumsfunktionen, einschließlich DATEDIF und EOMONTH, behandeln Schaltjahre korrekt gemäß dem gregorianischen Kalender.

**Q: Ist es möglich, mehrere Arbeitsblätter für Datumsberechnungen stapelweise zu verarbeiten?**  
A: Durchlaufen Sie jedes `Worksheet` im `Workbook`, setzen Sie die erforderlichen Formeln und rufen Sie `calculateFormula()` einmal pro Arbeitsmappe für optimale Leistung auf.

**Q: Welche Version von Aspose.Cells wird für diese Funktionen benötigt?**  
A: Alle Funktionen sind ab **Aspose.Cells 23.9** verfügbar; die neueste Version (Stand 2026) fügt Leistungsoptimierungen für große Datensätze hinzu.

## Fazit

Dieses Tutorial hat Ihnen einen tiefen Einblick in Excel‑Datumsfunktionen gegeben und gezeigt, wie man **calculate date difference java** mit Aspose.Cells für Java verwendet. Sie wissen jetzt, wie Sie die Bibliothek einrichten, die Formeln DATE, TODAY, DATEDIF und EOMONTH anwenden und gängige Herausforderungen wie Locale‑Formatierung und groß‑skalige Verarbeitung bewältigen. Integrieren Sie diese Muster in Ihre Java‑Anwendungen, um datumsgetriebene Berichte und Analysen mit Vertrauen zu automatisieren.

---

**Zuletzt aktualisiert:** 2026-07-26  
**Getestet mit:** Aspose.Cells 24.11 for Java  
**Autor:** Aspose  
**Verwandte Ressourcen:** API Reference [hier](https://reference.aspose.com/cells/java/) | Download Free Trial [hier](https://releases.aspose.com/cells/java/)

{{< blocks/products/products-backtop-button >}}

## Verwandte Tutorials

- [Meistern Sie das 1904-Datumsystem in Excel mit Aspose.Cells Java für effektive Zelloperationen](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Meistern der Datenpräsentation in Excel&#58; Zahlen- und benutzerdefinierte Datumsformatierung mit Aspose.Cells für Java](/cells/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel-Formeln und -Funktionen Tutorials für Aspose.Cells Java](/cells/java/formulas-functions/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```java
// Create a date style
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// Apply the style to a cell
worksheet.getCells().get("A1").setStyle(dateStyle);
```