---
category: general
date: 2026-10-07
description: Datum aus Excel in Java mit Aspose.Cells lesen. Diese Anleitung zeigt,
  wie man japanische Ära-Daten parst, das Datum aus Excel‑Zellen liest und Datum‑Uhrzeit‑Werte
  aus Excel‑Zellen schnell extrahiert.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Datum aus Excel in Java mit Aspose.Cells lesen. Diese Anleitung zeigt,
  wie man japanische Ära-Daten parst, das Datum aus Excel‑Zellen liest und Datum‑Uhrzeit‑Werte
  aus Excel‑Zellen in nur wenigen Schritten extrahiert.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Datum aus Excel in Java mit Aspose.Cells lesen – vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
- read date from excel
- java excel date conversion
title: Datum aus Excel in Java mit Aspose.Cells lesen – vollständige Anleitung
url: /de/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum aus Excel in Java mit Aspose.Cells lesen – vollständige Anleitung

Wenn Sie **read date from Excel** Arbeitsblätter lesen müssen, die japanische Ära‑Zeichenketten enthalten, sind Sie hier genau richtig. In vielen alten Buchhaltungs‑ oder Regierungs‑Tabellen wird das Datum als „令和3年5月10日“ gespeichert, und die Umwandlung in ein standardmäßiges Gregorianisches `LocalDateTime` kann fehleranfällig sein. Dieses Tutorial zeigt Ihnen Schritt für Schritt, wie Sie die Ära‑bewusste Analyse aktivieren, den Zellenwert lesen und **extract datetime from Excel** mit Aspose.Cells für Java extrahieren.

## Schnelle Antworten
- **Welche Bibliothek verarbeitet japanische Ära‑Daten?** Aspose.Cells for Java.
- **Welche Java‑Version wird benötigt?** Java 17 oder neuer (Java 8 funktioniert ebenfalls).
- **Benötige ich eine Lizenz für Tests?** Eine kostenlose Testversion reicht für die Entwicklung aus.
- **Kann derselbe Code gregorianische Daten lesen?** Ja, die API erkennt das Format automatisch.
- **Werden Zeitinformationen erhalten?** Absolut – Stunden, Minuten und Sekunden bleiben bei der Umwandlung erhalten.

## Was ist read date from Excel?
Der Ausdruck „read date from Excel“ bezieht sich darauf, den Datumswert einer Zelle abzurufen und ihn in ein Java‑Datum‑Zeit‑Objekt wie `java.time.LocalDateTime` zu konvertieren. Aspose.Cells abstrahiert das Low‑Level‑Excel‑Binärformat, sodass Sie mit Datumsangaben arbeiten können, ohne manuell Zeichenketten zu parsen.

## Warum Aspose.Cells für die Verarbeitung japanischer Ära‑Daten verwenden?
Aspose.Cells unterstützt **50+ Eingabe‑ und Ausgabeformate** und kann mehrseitige Arbeitsmappen verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Sein integrierter Ära‑bewusster Parser konvertiert jede japanische Ära (Meiji, Taishō, Shōwa, Heisei, Reiwa) in gregorianische Daten in einem einzigen API‑Aufruf und eliminiert damit fehleranfälligen regulären Ausdruckscode.

## Voraussetzungen
- Java 17 (oder Java 8+) auf Ihrem Rechner installiert.
- Maven‑ oder Gradle‑Build‑System.
- Grundlegende Vertrautheit mit Excel‑Dateien.
- Aspose.Cells für Java Bibliothek (Testversion oder lizenziert).

Falls Ihnen etwas davon unbekannt ist, keine Sorge – Sie sehen im nächsten Schritt genau, wie Sie die Bibliothek hinzufügen.

## Wie liest man ein Datum aus Excel in Java?
Laden Sie Ihre Arbeitsmappe, aktivieren Sie die Ära‑bewusste Analyse und fragen Sie die Zelle nach ihrem `DateTime`‑Wert. Der gesamte Vorgang benötigt **zwei Zeilen funktionalen Code**, sobald die Bibliothek im Klassenpfad ist.

### Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Nachdem die Abhängigkeit aufgelöst ist, können Sie die API verwenden, um **read date from Excel** Zellen zu lesen.

### Schritt 2: Eine Arbeitsmappe erstellen und das erste Arbeitsblatt anvisieren

Die Klasse `Workbook` repräsentiert eine komplette Excel‑Datei im Speicher. Das Erstellen einer neuen Instanz garantiert eine saubere Umgebung für die nachfolgenden Analyse‑Schritte.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Schritt 3: Eine japanische Ära‑Datumszeichenkette in Zelle A1 einfügen

Zur Demonstration schreiben wir die Ära‑Zeichenkette selbst; in der Produktion würden Sie eine vorhandene `.xlsx` laden.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Der Text folgt dem konventionellen japanischen Muster: *Ära* + *Jahr* + *Monat* + *Tag*.

### Schritt 4: Ära‑bewusste Datum‑Analyse aktivieren

Teilen Sie Aspose.Cells mit, Ära‑Zeichenketten als Datum zu behandeln, indem Sie das Flag `ParseDateUsingJapaneseEra` setzen.  
`ParseDateUsingJapaneseEra` ist eine Eigenschaft, die bei `true` die automatische Umwandlung japanischer Ära‑Zeichenketten in gregorianische Daten aktiviert.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Ohne dieses Flag würde die Bibliothek „令和3年5月10日“ als Klartext behandeln, und die automatische Umwandlung würde verloren gehen.

### Schritt 5: Den geparsten DateTime‑Wert abrufen

Fragen Sie nun die Zelle nach ihrer Datumsdarstellung. `cell.getDateTime()` gibt den Zellenwert als `java.util.Date`‑Objekt zurück. Die Methode liefert ein `java.util.Date`, das wir sofort in das moderne `java.time.LocalDateTime` konvertieren. `LocalDateTime` ist eine Java‑Klasse, die Datum und Zeit ohne Zeitzone repräsentiert.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Damit wird die Anforderung **extract datetime from Excel** typensicher erfüllt.

### Schritt 6: Das Ergebnis überprüfen

Geben Sie das gregorianische Datum aus, um die erfolgreiche Umwandlung zu bestätigen.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Wenn Sie das Programm ausführen, sollten Sie sehen:

```
2021-05-10T00:00
```

Die Ausgabe beweist, dass wir erfolgreich **read date from Excel** gelesen, die japanische Ära geparst und **extract datetime from Excel** in einem einzigen Ablauf extrahiert haben.

## Umgang mit realen Randfällen

### Mehrere Ären

Japan hat mehrere Ären (Meiji, Taishō, Shōwa, Heisei, Reiwa). Das Flag `setParseDateUsingJapaneseEra(true)` deckt alle automatisch ab, aber beachten Sie, dass ältere Daten außerhalb des von der Bibliothek unterstützten Bereichs liegen können (typischerweise 1868‑heute). Wenn Sie ein Datum wie „昭和45年12月31日“ finden, wird derselbe Code es in 1970‑12‑31 umwandeln.

### Leere oder ungültige Zellen

Wenn eine Zelle leer ist oder eine fehlerhafte Zeichenkette enthält, wirft `cell.getDateTime()` eine `CellsException`. Schützen Sie sich davor mit einer einfachen Prüfung:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Zeitkomponente

Das Beispiel enthält nur ein Datum, aber wenn Ihre Excel‑Datei auch die Zeit speichert (z. B. „令和3年5月10日 14:30“), wird Aspose.Cells den Zeitanteil erhalten. Das `LocalDateTime`, das Sie erhalten, enthält Stunden, Minuten und Sekunden.

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenführen, hier das vollständige, sofort kopier‑und‑einfüg‑bereite Programm:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Speichern Sie dies als `JapaneseEraDateParser.java`, kompilieren Sie mit `javac` und führen Sie es mit `java` aus. Wenn alles korrekt eingerichtet ist, wird das gregorianische Datum in der Konsole ausgegeben.

## Pro‑Tipps & häufige Stolperfallen

- **Pro tip:** Aktivieren Sie `setParseDateUsingJapaneseEra(true)` **vor** dem Lesen von Zellenwerten. Das spätere Ändern des Flags konvertiert bereits gelesene Zellen nicht retroaktiv.
- **Locale note:** Der Parser arbeitet direkt mit den Unicode‑Zeichen, sodass Sie nicht explizit ein japanisches Locale setzen müssen.
- **Performance:** Die Ära‑Analyse fügt nur einen vernachlässigbaren Overhead hinzu. Wenn Sie sie nur für wenige Zellen benötigen, schalten Sie das Flag nur für diese Lesevorgänge ein.
- **Testing:** Nutzen Sie die kostenlose Testversion von Aspose, um gegen eine reale Arbeitsmappe zu validieren, die gregorianische und Ära‑Daten mischt. Das stellt sicher, dass der Produktionscode wie erwartet funktioniert.

## Häufig gestellte Fragen

**Q: Kann ich diesen Ansatz mit einer bestehenden .xlsx‑Datei verwenden?**  
A: Ja. Laden Sie die Datei mit `new Workbook("path/to/file.xlsx")` und das gleiche Flag wird alle gefundenen Ära‑Zeichenketten parsen.

**Q: Was passiert, wenn die Zelle ein gregorianisches Datum enthält?**  
A: Die Bibliothek gibt den gregorianischen Wert unverändert zurück; die Ära‑Analyse wirkt nur auf Zeichenketten, die dem Ära‑Muster entsprechen.

**Q: Unterstützt Aspose.Cells Daten vor Meiji (1868)?**  
A: Nein. Daten vor 1868 liegen außerhalb des unterstützten Bereichs und werden als Klartext behandelt.

**Q: Wie gehe ich mit großen Arbeitsmappen um, ohne den Speicher zu erschöpfen?**  
A: Verwenden Sie den `Workbook`‑Konstruktor, der `LoadOptions` mit `setMemorySetting(MemorySetting.MemoryPreference)` akzeptiert, um Daten zu streamen, anstatt alles auf einmal zu laden.

**Q: Ist für den Produktionseinsatz eine kommerzielle Lizenz erforderlich?**  
A: Ja, eine gültige Aspose.Cells‑Lizenz entfernt Evaluationsbeschränkungen und ermöglicht volle Leistung.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Meistern Sie das 1904‑Datumssystem in Excel mit Aspose.Cells Java für effektive Zelloperationen](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Excel effizient in PDF mit benutzerdefinierten Datumsformaten konvertieren mit Aspose.Cells für Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Wie man Zellbereiche in Excel mit Aspose.Cells für Java auswählt (2023‑Leitfaden)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Zuletzt aktualisiert:** 2026-10-07  
**Getestet mit:** Aspose.Cells 24.12 for Java  
**Autor:** Aspose

## Verwandte Tutorials

- [Japanisches Ära‑Datum aus Excel in Java – Vollständige Anleitung](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Excel‑Datei in Java mit Aspose.Cells lesen – Vollständige Anleitung](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Excel‑Arbeitsmappe mit Aspose.Cells für Java speichern – Vollständige Anleitung](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}