---
category: general
date: 2026-06-08
description: Holen Sie das Datum und die Uhrzeit aus einer Zelle mit Aspose.Cells
  Java und lernen Sie, wie Sie in nur wenigen Schritten Werte in eine Excel‑Zelle
  schreiben.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: de
og_description: Datum und Uhrzeit aus einer Zelle mit Aspose.Cells Java abrufen. Dieses
  Tutorial zeigt außerdem, wie man Werte effizient in eine Excel‑Zelle schreibt.
og_title: Datum und Uhrzeit aus einer Zelle in Java Excel – Komplettanleitung
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Datum und Uhrzeit aus einer Zelle in Java‑Excel erhalten – Komplett‑Guide
url: /de/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum und Uhrzeit aus Zelle in Java Excel – Komplettanleitung

Haben Sie jemals **Datum und Uhrzeit aus Zelle** erhalten müssen, aber der Wert sieht wie ein japanischer Ära‑String aus? Sie sind nicht allein. In vielen alten Tabellenkalkulationen werden die Daten als „Reiwa 3/04/01“ gespeichert, und ein korrektes `java.time.LocalDateTime` daraus zu extrahieren kann sich anfühlen, als würde man eine Geheimnachricht entschlüsseln.  

Glücklicherweise kann Aspose.Cells for Java die Konvertierung für Sie übernehmen, und wir zeigen Ihnen außerdem, wie Sie **Wert in Excel‑Zelle schreiben** können, damit Sie Daten round‑tripen können, ohne die Logik des Blatts zu brechen.

In diesem Tutorial lernen Sie:

* Wie man ein Workbook erstellt und ein bestimmtes Arbeitsblatt anspricht.  
* Die genauen Schritte, um den japanischen Ära‑Kalender für das Parsen zu aktivieren.  
* Warum Sie Formeln neu berechnen müssen, bevor Sie das Datum auslesen.  
* Wie Sie einen neuen Wert wieder in eine Zelle schreiben, ohne die Formatierung zu verlieren.  

Keine externen Tools, kein Hokuspokus – einfach reiner Java‑Code, den Sie noch heute in jedes Maven‑Projekt einbinden können.

---

## Voraussetzungen

* **Java 8+** (das Beispiel verwendet die moderne `java.time`‑API).  
* **Aspose.Cells for Java** ≥ 23.9.0 – fügen Sie die Abhängigkeit via Maven oder Gradle hinzu.  
* Grundlegende Kenntnisse der Excel‑Konzepte (Arbeitsblätter, Zellen, Formeln).  

Falls Ihnen die Bibliothek fehlt, holen Sie sie aus dem offiziellen Aspose‑Repository:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Schritt 1: Erstelle ein neues Workbook und greife auf das erste Arbeitsblatt zu

Um zu beginnen, benötigen wir ein frisches `Workbook`‑Objekt. Denken Sie daran wie an das Öffnen einer neuen Excel‑Datei im Speicher.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Warum das wichtig ist:*  
Das programmatische Erstellen des Workbooks gibt Ihnen die volle Kontrolle über Einstellungen, bevor irgendwelche Daten das Dateisystem berühren. Das erste Arbeitsblatt (`Index 0`) ist dort, wo wir sowohl das Lesen als auch das Schreiben demonstrieren.

---

## Schritt 2: Schreibe einen japanischen Ära‑Datums‑String in Zelle A1

Jetzt **Wert in Excel‑Zelle schreiben** nach A1. Das spiegelt ein reales Szenario wider, bei dem ein Benutzer manuell „Reiwa 3/04/01“ eingegeben hat.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Schneller Tipp:* `putValue` ist vielseitig – es akzeptiert Strings, Zahlen, Daten und sogar Formeln. Wenn Sie einen reinen String übergeben, speichert Aspose ihn exakt so, was für unser Demo perfekt ist.

---

## Schritt 3: Aktiviere den japanischen Ära‑Kalender für das Datums‑Parsing

Standardmäßig verwendet Aspose.Cells den Gregorianischen Kalender. Um „Reiwa“ zu verstehen, schalten wir eine Einstellung um.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Warum aktivieren?*  
Der japanische Ära‑Kalender ordnet Ära‑Namen (Reiwa, Heisei, Showa) ihren gregorianischen Gegenstücken zu. Ohne dieses Flag würde die Bibliothek den String als reinen Text behandeln und Sie würden nie ein korrektes `DateTime`‑Objekt erhalten.

---

## Schritt 4: Berechne Formeln neu, damit der Ära‑String in ein gregorianisches Datum umgewandelt wird

Aspose parst den String nicht automatisch in ein Datum. Stattdessen wird die Zelle nach einem Berechnungslauf als Formel‑Ergebnis behandelt.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Wenn `calculateFormula()` ausgeführt wird, erkennt die Engine das Ära‑Muster, wendet den japanischen Kalender an und speichert das resultierende gregorianische Datum intern. Der Aufruf `getDateTime()` liefert dann ein `java.util.Date` (oder Sie können zu `java.time` konvertieren).

**Erwartete Ausgabe**

```
2021-04-01T00:00:00.000+00:00
```

---

## Schritt 5: Schreibe einen neuen Wert zurück in dieselbe Zelle (oder in eine andere Zelle)

Angenommen, Sie möchten den ursprünglichen String durch ein sauberes ISO‑8601‑Datum ersetzen. So **Wert in Excel‑Zelle schreiben** Sie sicher und erhalten dabei den Zellstil.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Was passiert?*  
`putValue` erkennt den Typ `LocalDateTime` und konvertiert ihn in Asposes interne Seriennummer‑Darstellung. Das Setzen des Zahlenformats stellt sicher, dass die Zelle das Datum exakt so anzeigt, wie Sie es in Excel erwarten.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier eine einzelne Java‑Klasse, die Sie kompilieren und ausführen können. Sie erstellt ein Workbook, schreibt einen Ära‑String, konvertiert ihn und speichert schließlich die Datei.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Führen Sie das mit `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` aus und öffnen Sie **output.xlsx**. Sie sehen, dass Zelle A1 das aktuelle Datum anzeigt, während die Konsole den konvertierten Wert „2021‑04‑01“ ausgibt.

---

## Sonderfälle & häufige Fragen

### Was, wenn die Zelle bereits ein echtes Excel‑Datum enthält?

Wenn `cell.getType()` `CellValueType.IS_DATE_TIME` zurückgibt, können Sie den Berechnungsschritt überspringen und den Wert direkt auslesen:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Wie verarbeite ich eine ganze Spalte von Ära‑Strings?

Durchlaufen Sie den genutzten Bereich und wenden Sie dieselben Einstellungen einmalig an:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Kann ich die japanische Ära‑Verarbeitung später deaktivieren?

Ja – schalten Sie das Flag einfach zurück:

```java
settings.setUseJapaneseEraCalendar(false);
```

Denken Sie daran, nach einer Änderung des Flags erneut zu berechnen.

---

## Pro‑Tipps & Stolperfallen

* **Performance:** Das Aktivieren des japanischen Ära‑Kalenders verursacht einen kleinen Overhead. Wenn Sie ihn nur für wenige Zellen benötigen, schalten Sie ihn ein, verarbeiten Sie, und schalten Sie ihn wieder aus.  
* **Sprachbewusstsein:** Der Ära‑String muss exakt dem Muster „EraName yy/MM/dd“ entsprechen. Ein Tippfehler bei „Reiwa“ (z. B. „Rewa“) lässt die Zelle als reinen Text stehen.  
* **Speicherformat:** `Workbook.save("output.xlsx")` schreibt eine XLSX‑Datei. Verwenden Sie `"output.xls"` für das ältere Binärformat, beachten Sie jedoch, dass einige Funktionen (wie Ära‑Parsing) dort eingeschränkt sein können.

---

## Fazit

Sie wissen jetzt, wie Sie **Datum und Uhrzeit aus Zelle** erhalten, wenn die Quelle eine japanische Ära‑Notation verwendet, und Sie haben gesehen, wie Sie **Wert in Excel‑Zelle schreiben** mit korrekter Formatierung. Durch das Setzen von `setUseJapaneseEraCalendar(true)` und das Erzwingen einer Formel‑Neuberechnung überbrückt Aspose.Cells die Lücke zwischen alten Ära‑Strings und modernen gregorianischen Daten – alles mit nur wenigen Zeilen Java.

Was kommt als Nächstes? Versuchen Sie, dieses Muster auf andere kulturelle Kalender (Thai, Hijri) auszuweiten oder große Workbooks stapelweise zu verarbeiten, indem Sie denselben Ansatz verwenden. Die gleichen Prinzipien – richtigen Kalender aktivieren, neu berechnen, dann lesen/schreiben – gelten überall.

Haben Sie ein kniffliges Datumsformat, das Sie nicht knacken können? Hinterlassen Sie einen Kommentar unten, und wir lösen das gemeinsam. Viel Spaß beim Coden!  

![Beispiel für Datum und Uhrzeit aus Zelle](https://example.com/images/get-datetime-from-cell.png "Beispiel für Datum und Uhrzeit aus Zelle")


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Features meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [How to Implement Recursive Cell Calculation in Aspose.Cells Java for Enhanced Excel Automation](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}