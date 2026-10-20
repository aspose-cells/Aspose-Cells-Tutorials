---
category: general
date: 2026-07-03
description: Datum mit Locale unter Verwendung von Javas java.time‑API parsen. Erfahren
  Sie, wie man das japanische Ära-Format verarbeitet, Datumsumwandlungen nach Locale
  durchführt und robuste Java‑Datum‑Parsing‑Techniken anwendet.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: de
og_description: Datum mit Locale in Java mithilfe der java.time‑API parsen. Dieser
  Leitfaden zeigt die Handhabung des japanischen Ära‑Formats, die Konvertierung von
  Datumsangaben nach Locale und bewährte Methoden für zuverlässiges Datum‑Parsing.
og_title: Datum mit Locale in Java parsen – Vollständiges Programmier‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: Datum mit Locale in Java parsen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum mit Locale in Java parsen – Vollständige Schritt‑für‑Schritt‑Anleitung

Schon einmal nötig gehabt, **Datum mit Locale zu parsen** in Java, aber nicht sicher gewesen, welche Klassen man dafür verwenden soll? Sie sind nicht allein – der Umgang mit nicht‑gregorianischen Kalendern oder regionalen Formaten kann sich anfühlen wie das Entschlüsseln einer Geheimsprache. In diesem Tutorial gehen wir ein reales Beispiel durch: einen japanischen Ära‑String wie `R5/04/01` in ein standardmäßiges gregorianisches `2023‑04‑01` `Date`‑Objekt umzuwandeln. Am Ende haben Sie ein wiederverwendbares Muster für jedes lokalspezifische Datumsformat.

Wir behandeln alles von den erforderlichen Imports bis zur Behandlung von Randfällen und streuen ein paar verwandte Konzepte ein – *java date parsing*, *japanese era format*, *locale date conversion* und die moderne *java time API* – damit Sie die Lösung an Ihre eigenen Projekte anpassen können. Keine externen Bibliotheken, nur reines Java 8+.

---

## Was dieses Tutorial abdeckt

- Einrichten des **Japanese era** (`Reiwa`) Format‑Strings.
- Verwendung von `DateTimeFormatter` mit `JapaneseChronology` und einem `Locale`.
- Umwandlung des resultierenden `JapaneseDate` in ein `LocalDate` (Gregorianisch).
- Ausgabe des finalen ISO‑8601‑Datums.
- Häufige Fallstricke wie nicht unterstützte Äras oder nicht passende Muster.
- Schnelle Varianten für andere Locales (Thai Buddhist, Islamic usw.).

**Voraussetzungen**  
Ein JDK 8 oder neuer, grundlegende Vertrautheit mit `java.time` und eine IDE oder CLI zum Ausführen von Java‑Code. Das war’s – keine zusätzlichen Maven‑Abhängigkeiten.

## Datum mit Locale parsen – Schritt‑für‑Schritt

Im Folgenden teilen wir die Lösung in drei natürliche Schritte auf. Jeder Schritt enthält den genauen Code, den Sie benötigen, eine kurze Erklärung, *warum* er wichtig ist, und einen Hinweis, den Sie in der offiziellen Dokumentation vielleicht nicht finden.

### Schritt 1: Definieren Sie den Ära‑Datums‑String

Zuerst speichern Sie den japanischen Ära‑String exakt so, wie Sie ihn erhalten (z. B. aus einer CSV‑Datei oder UI).

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Warum das wichtig ist:**  
> Das führende `R` steht für *Reiwa*, die aktuelle Ära Japans. Wenn Sie das Ära‑Symbol ignorieren, geht der Parser vom gregorianischen Kalender aus und liefert ein falsches Jahr.

### Schritt 2: Einen lokalisierungsbewussten Formatter erstellen

Die **java.time API** von Java ermöglicht es, einen `DateTimeFormatter` an eine bestimmte Chronologie (Kalendersystem) und ein `Locale` zu binden. Für die japanische Ära verwenden wir `JapaneseChronology`.

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**Wichtige Punkte**  
- `G` parst den Ära‑Text (`R` für Reiwa, `H` für Heisei, usw.).  
- `ResolverStyle.STRICT` zwingt den Parser, unmögliche Daten wie `R0/13/32` abzulehnen.  
- Durch das Setzen des `Locale` auf `Locale.JAPAN` wird sichergestellt, dass die Ära‑Symbole den japanischen Konventionen entsprechen.

> **Pro‑Tipp:** Wenn Sie *mehrere* Ära‑Formate unterstützen müssen (z. B. ausgeschriebenes `HEISEI`), fügen Sie `.parseCaseInsensitive()` wie gezeigt hinzu und erweitern Sie das Muster zu `Guuuu` für vollständige Namen.

### Schritt 3: Parsen und in ein gregorianisches `LocalDate` konvertieren

Jetzt parsen wir tatsächlich den String und transformieren das Ergebnis in ein klassisches `LocalDate`, das jede Java‑Bibliothek verwenden kann.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**Erklärung**  
`JapaneseDate.from(...)` erzeugt ein Datumsobjekt, das im japanischen Kalender verankert ist. Durch Aufruf von `LocalDate.from(...)` entfernen wir die Ära‑Information und erhalten das entsprechende ISO‑8601‑Datum – ideal für Speicherung, Vergleich oder API‑Aufrufe.

> **Warum konvertieren?** Die meisten Datenbanken, REST‑Services und Drittanbieter‑Bibliotheken erwarten ein gregorianisches Datum. Die Konvertierung innerhalb Ihrer Parsing‑Routine verhindert später subtile Fehler.

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier ist eine einzelne, sofort ausführbare Java‑Klasse. Sie können sie gerne in `ParseDateWithLocale.java` kopieren und ausführen.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**Erwartete Konsolenausgabe**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

Führen Sie das Programm mit `javac ParseDateWithLocale.java && java ParseDateWithLocale` aus. Wenn Sie die beiden Zeilen oben sehen, haben Sie erfolgreich **Datum mit Locale geparst**.

## Umgang mit Randfällen & häufigen Fragen

### Was, wenn die Eingabe ein anderes Ära‑Symbol verwendet?

Japanische Äras ändern sich etwa alle paar Jahrzehnte. Der Formatter erkennt automatisch `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei) und `R` (Reiwa). Wenn Sie eine ältere Ära erhalten, die von der Standard‑`JapaneseChronology` nicht abgedeckt wird, erhalten Sie eine `DateTimeParseException`. In diesem Fall prüfen Sie die Quelldaten oder stellen eine benutzerdefinierte Zuordnung bereit.

### Wie unterstützt man andere nicht‑gregorianische Kalender?

Das Muster ist identisch; Sie tauschen lediglich die Chronologie und das Locale aus. Zum Beispiel sehen thailändische buddhistische Daten (`BuddhistChronology`) so aus:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Kann ich ohne ein Ära‑Symbol parsen (reines Jahr‑Monat‑Tag)?

Ja – lassen Sie einfach `G` im Muster weg und verwenden Sie den Standard‑Formatter `ISO_LOCAL_DATE`. Das ist der klassische *java date parsing*‑Weg für gregorianische Strings.

### Was ist mit nachgiebigem Parsen (z. B. fehlende führende Nullen)?

Wechseln Sie `ResolverStyle.STRICT` zu `ResolverStyle.LENIENT`. Beachten Sie, dass der nachgiebige Modus ungültige Daten stillschweigend überrollen kann (z. B. wird `R5/13/40` zu `2024‑02‑09`). Für Produktionscode ist der strikte Modus in der Regel sicherer.

## Pro‑Tipps für robuste Locale‑Datumskonvertierung

1. **Cache den Formatter** – Das Erstellen eines `DateTimeFormatter` ist relativ günstig, aber wenn Sie Tausende von Daten pro Sekunde parsen, speichern Sie ihn in einem static final Feld.  
2. **Validieren Sie die Eingabelänge** – Eine schnelle Prüfung `if (eraDateString.length() != 8)` kann unnötige Parsing‑Ausnahmen vermeiden.  
3. **Loggen Sie den Original‑String** – Beim Debuggen von Locale‑Problemen zeigt die rohe Eingabe oft unsichtbare Zeichen (Null‑Breiten‑Leerzeichen), die den Parser brechen.  
4. **Unit‑Testen Sie jede Ära** – Schreiben Sie JUnit‑Tests für `R`, `H`, `S` usw., um sicherzustellen, dass zukünftige Java‑Updates die Zuordnung nicht ändern.

## Fazit

Wir haben gerade gezeigt, wie man **Datum mit Locale** in Java parst, indem man die moderne *java time API*, einen lokalisierungsbewussten `DateTimeFormatter` und die `JapaneseChronology` nutzt. Das vollständige Beispiel zeigt den gesamten Ablauf – vom rohen japanischen Ära‑String bis zu einem sauberen gregorianischen `LocalDate` – und gibt Ihnen das Wissen, das Muster für andere Kalender, wie das thailändische buddhistische oder das islamische System, anzupassen.

Nächste Schritte? Versuchen Sie, die `JapaneseChronology` durch `ThaiBuddhistChronology` oder `HijrahChronology` zu ersetzen und sehen Sie, wie dieselbe Code‑Struktur völlig unterschiedliche kulturelle Kalender handhabt. Sie können auch das resultierende `LocalDate` zurück in einen lokalspezifischen String formatieren, indem Sie `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)` verwenden.

Haben Sie ein kniffliges Locale oder einen unerwarteten Parsing‑Fehler? Hinterlassen Sie unten einen Kommentar, und wir lösen das gemeinsam. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Meistern der Datenpräsentation in Excel: Zahlen- und benutzerdefinierte Datumsformatierung mit Aspose.Cells für Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Effizientes Konvertieren von Excel zu PDF mit benutzerdefinierten Datumsformaten mittels Aspose.Cells für Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Meistern des 1904‑Datumsystems in Excel mit Aspose.Cells Java für effektive Zelloperationen](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}