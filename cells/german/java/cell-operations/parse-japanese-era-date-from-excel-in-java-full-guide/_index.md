---
category: general
date: 2026-06-18
description: Japanisches Ära‑Datum in Java mit Aspose.Cells parsen. Erfahren Sie,
  wie Sie ein Datum aus einer Excel‑Zelle lesen und das Datum/Uhrzeit schnell aus
  einer Excel‑Zelle extrahieren.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: de
og_description: Japanisches Jahreszahlen‑Datum in Java mit Aspose.Cells parsen. Dieser
  Leitfaden zeigt Ihnen, wie Sie ein Datum aus einer Excel‑Zelle lesen und das Datum/Zeit
  aus einer Excel‑Zelle in nur wenigen Schritten extrahieren.
og_title: Japanisches Ära-Datum aus Excel in Java parsen – Komplettes Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
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
title: Japanisches Ära‑Datum aus Excel in Java parsen – Vollständiger Leitfaden
url: /de/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanisches Ära‑Datum aus Excel in Java parsen – Vollständige Anleitung

Haben Sie jemals **parse Japanese era date** in einer Excel‑Arbeitsmappe gespeichert, aber waren sich nicht sicher, wie Sie sie in ein reguläres gregorianisches `DateTime` umwandeln können? Sie sind nicht allein – viele Entwickler stoßen auf dieses Problem, wenn sie mit alten japanischen Buchhaltungsblättern oder Regierungsformularen arbeiten. Die gute Nachricht ist, dass Sie mit wenigen Zeilen Java und der richtigen Bibliothek **read date from Excel cell** und **extract datetime from Excel cell** ohne manuelle String‑Manipulationen durchführen können.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das genau zeigt, wie man **parse Japanese era date**‑Zeichenketten wie „令和3年5月10日“ in ein Java `java.time.LocalDateTime` konvertiert. Wir behandeln die erforderliche Maven‑Abhängigkeit, erklären, warum Sie era‑aware parsing aktivieren müssen, und weisen auf häufige Stolperfallen hin. Am Ende haben Sie ein robustes, produktionsreifes Snippet, das Sie in jedes Java‑Projekt einbinden können.

## Voraussetzungen

- Java 17 oder neuer (der Code funktioniert auch mit Java 8+)
- Maven‑ oder Gradle‑Buildsystem
- Grundlegende Kenntnisse im Umgang mit Excel‑Dateien
- Die **Aspose.Cells for Java**‑Bibliothek (kostenlose Testversion funktioniert zum Testen)

Wenn Ihnen das irgendeiner dieser Punkte unbekannt ist, keine Sorge – ich zeige Ihnen genau, wie Sie die Bibliothek hinzufügen und loslegen.

## Schritt 1: Aspose.Cells zu Ihrem Projekt hinzufügen

Zuerst benötigen Sie die Bibliothek, die japanische Ära‑Daten versteht. Aspose.Cells übernimmt die schwere Arbeit für Sie.

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

Sobald die Abhängigkeit aufgelöst ist, können Sie Code schreiben, der *reads date from Excel cell* und *extracts datetime from Excel cell*.

## Schritt 2: Ein Workbook erstellen und das erste Arbeitsblatt anvisieren

Wir beginnen damit, ein neues Workbook im Speicher zu erstellen und das erste Blatt zu holen. Das entspricht den ersten beiden Zeilen des Originalbeispiels.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Warum mit einem frischen Workbook beginnen? Es garantiert eine saubere Umgebung, in der wir jede Einstellung kontrollieren können – entscheidend, wenn Sie später era‑aware parsing aktivieren.

## Schritt 3: Einen japanischen Ära‑Datums‑String in Zelle A1 einfügen

Jetzt simulieren wir eine Excel‑Datei, die bereits ein japanisches Ära‑Datum enthält. Im echten Leben würden Sie wahrscheinlich eine vorhandene `.xlsx` laden, aber zur Veranschaulichung **schreiben** wir den Wert selbst.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Der String folgt der üblichen japanischen Notation: *Era* + *Year* + *Month* + *Day*. Ohne zusätzliche Konfiguration würde Aspose.Cells dies als reinen Text und nicht als Datum behandeln.

## Schritt 4: Era‑Aware‑Datums‑Parsing aktivieren

Hier kommt der entscheidende Teil: dem Workbook mitteilen, **parse Japanese era date**‑Zeichenketten zu verarbeiten, wenn es sie findet. Das geschieht über das Flag `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Warum ist das nötig? Standardmäßig geht Aspose.Cells vom gregorianischen Kalender aus, sodass „令和3年5月10日“ als Zeichenkette erhalten bleibt. Durch das Aktivieren des Flags wird die Engine angewiesen, es im Hintergrund in ein `java.util.Date` (oder das entsprechende `java.time`‑Äquivalent) zu konvertieren.

## Schritt 5: Den geparsten DateTime‑Wert abrufen

Jetzt, da das Workbook weiß, wie es die Ära interpretieren soll, können wir die Zelle nach ihrer `DateTime`‑Darstellung fragen.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Beachten Sie, dass wir **read date from Excel cell** mit `cell.getDateTime()` verwenden. Die Methode liefert ein `java.util.Date`, das wir sofort in `LocalDateTime` umwandeln für bessere Typsicherheit. Das erfüllt die Anforderung **extract datetime from excel cell** auf saubere, idiomatische Weise.

## Schritt 6: Ergebnis überprüfen

Zum Schluss geben wir das gregorianische Datum aus, um die erfolgreiche Konvertierung zu bestätigen.

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

Diese Ausgabe beweist, dass wir erfolgreich **parse Japanese era date**, **read date from Excel cell** und **extract datetime from Excel cell** in einem einzigen Ablauf durchgeführt haben.

## Umgang mit realen Sonderfällen

### Mehrere Ären

Japan hatte mehrere Ären (Meiji, Taishō, Shōwa, Heisei, Reiwa). Das Flag `setParseDateUsingJapaneseEra(true)` deckt alle automatisch ab, aber beachten Sie, dass ältere Daten außerhalb des von der Bibliothek unterstützten Bereichs liegen können (typischerweise 1868‑heute). Wenn Sie ein Datum wie „昭和45年12月31日“ finden, konvertiert derselbe Code es zu 1970‑12‑31.

### Leere oder ungültige Zellen

Wenn eine Zelle leer ist oder eine fehlerhafte Zeichenkette enthält, wirft `cell.getDateTime()` eine `CellsException`. Schützen Sie sich dagegen mit einer einfachen Prüfung:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Zeitkomponente

Das Beispiel enthält nur ein Datum, aber wenn Ihre Excel‑Datei auch eine Uhrzeit speichert (z. B. „令和3年5月10日 14:30“), wird Aspose.Cells den Zeitanteil beibehalten. Das `LocalDateTime`, das Sie erhalten, enthält Stunden, Minuten und Sekunden.

## Vollständiges funktionierendes Beispiel

Hier ist das komplette, copy‑and‑paste‑bereite Programm:

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

Speichern Sie dies als `JapaneseEraDateParser.java`, kompilieren Sie mit `javac` und führen Sie mit `java` aus. Wenn alles korrekt eingerichtet ist, wird das gregorianische Datum in der Konsole ausgegeben.

## Profi‑Tipps & häufige Stolperfallen

- **Pro‑Tipp:** Setzen Sie `setParseDateUsingJapaneseEra(true)` immer **vor** dem Auslesen von Zellenwerten. Das Ändern des Flags nach dem Lesen einer Zelle konvertiert den Wert nicht rückwirkend.
- **Achten Sie auf das Locale:** Die Bibliothek parst Ära‑Zeichenketten basierend auf Unicode‑Zeichen, sodass Sie kein japanisches Locale explizit setzen müssen.
- **Hinweis zur Performance:** Das Aktivieren des Era‑Parsens fügt einen kleinen Overhead hinzu. Wenn Sie es nur für einige Zellen benötigen, können Sie das Flag temporär umschalten, die Zellen lesen und es anschließend wieder deaktivieren.
- **Testing:** Verwenden Sie die kostenlose Testversion von Aspose, um gegen eine echte Excel‑Datei mit mehreren Ära‑Daten zu validieren. So stellen Sie sicher, dass Ihr Produktionscode wie erwartet funktioniert.

## Fazit

Wir haben gerade gezeigt, wie man **parse Japanese era date**‑Werte direkt aus einem Excel‑Workbook mit Java und Aspose.Cells verarbeitet. Durch das Aktivieren von era‑aware parsing können Sie **read date from Excel cell** und **extract datetime from Excel cell** auf saubere, typsichere Weise durchführen. Der Ansatz funktioniert für jede moderne japanische Ära, verarbeitet Zeitkomponenten und geht elegant mit ungültigen Daten um.

Bereit für die nächste Herausforderung? Versuchen Sie, eine echte `.xlsx`‑Datei zu laden, die eine Mischung aus gregorianischen und japanischen Ära‑Daten enthält, oder experimentieren Sie damit, das resultierende `LocalDateTime` in Zeichenketten zu formatieren, die Ihrem Locale entsprechen. Sie können auch erkunden, die konvertierten Daten zurück nach Excel zu schreiben für nachgelagerte Systeme, die nur gregorianische Daten verstehen.

Haben Sie Fragen oder sind Sie auf einen seltsamen Sonderfall gestoßen? Hinterlassen Sie unten einen Kommentar, und happy coding!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Meistern Sie das 1904‑Datumsystem in Excel mit Aspose.Cells Java für effektive Zelloperationen](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Effizientes Konvertieren von Excel zu PDF mit benutzerdefinierten Datumsformaten mittels Aspose.Cells für Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Wie man Zellbereiche in Excel mit Aspose.Cells für Java auswählt (2023‑Leitfaden)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}