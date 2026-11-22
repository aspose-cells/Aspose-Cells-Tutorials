---
category: general
date: 2026-11-22
description: Erfahren Sie, wie Sie das Locale in einer Java-Arbeitsmappe festlegen,
  die Sprache der Arbeitsmappe ändern und den Kalender auf Japanisch einstellen, mit
  klaren Codebeispielen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: de
lastmod: 2026-11-22
og_description: Wie man das Locale in einer Java‑Arbeitsmappe schnell einstellt. Folgen
  Sie diesem Tutorial, um die Sprache der Arbeitsmappe zu ändern, das Locale auf Japanisch
  zu setzen und den japanischen Kalender zu konfigurieren.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Wie man das Locale in einer Java-Arbeitsmappe einstellt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Wie man das Gebietsschema in einer Java-Arbeitsmappe mit Aspose.Cells festlegt
url: /de/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man das Gebietsschema in einer Java-Arbeitsmappe mit Aspose.Cells festlegt

Das Festlegen des Gebietsschemas in einer Java-Arbeitsmappe ist ein häufiges Bedürfnis, wenn Sie Ihre Tabelle an verschiedene Regionen anpassen müssen. In diesem Leitfaden lernen Sie, wie Sie das Gebietsschema festlegen, die Sprache der Arbeitsmappe ändern und den Kalender auf Japanisch einstellen, mithilfe der Aspose.Cells API.

Die Internationalisierung einer Arbeitsmappe geht über das Übersetzen von Text hinaus; sie beeinflusst auch Zahlenformate, Datumsparsing und das Standardsystem des Kalenders. Am Ende dieses Tutorials werden Sie in der Lage sein:

* Das Gebietsschema der Arbeitsmappe auf Japanisch (Japan) konfigurieren – **set locale to japanese**.  
* Die Sprache der Arbeitsmappe ändern, sodass Formeln und UI‑Zeichenketten die Zielkultur berücksichtigen – **change workbook language**.  
* Den Kalender auf den japanischen Kaiserkalender umstellen – **how to set calendar**.  

Die Schritte funktionieren mit jeder aktuellen Version von Aspose.Cells für Java (v23.9 oder höher) und erfordern nur eine Standard‑Java‑Entwicklungsumgebung.

## Voraussetzungen

| Anforderung | Grund |
|-------------|-------|
| Java 8 or higher | Die Bibliothek zielt auf Java 8+ ab. |
| Aspose.Cells for Java (v23.9+) | Stellt `Workbook`, `WorkbookSettings` und Gebietsschema‑Hilfsprogramme bereit. |
| IDE (IntelliJ IDEA, Eclipse, or VS Code) | Zum Kompilieren und Ausführen des Beispiels. |
| Basic knowledge of Java | Erforderlich, um die Code‑Snippets zu verstehen. |

Fügen Sie die Aspose.Cells Maven‑Abhängigkeit zu Ihrer `pom.xml` hinzu (oder laden Sie die JAR manuell herunter):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Wie man das Gebietsschema und den Kalender in einer Arbeitsmappe festlegt

Der erste Schritt besteht darin, eine Arbeitsmappen‑Instanz zu erstellen und ihr Settings‑Objekt zu erhalten. Das Settings‑Objekt stellt die Gebietsschema‑ und Kalender‑APIs bereit.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Warum jede Zeile wichtig ist

* **`new Workbook()`** – Instanziiert eine leere Arbeitsmappe, die Sie vor dem Speichern manipulieren können.  
* **`getSettings()`** – Gibt ein `WorkbookSettings`‑Objekt zurück; alle regionalen Optionen befinden sich hier.  
* **`setCalendar(...)`** – Ersetzt den standardmäßigen Gregorianischen Kalender durch den japanischen Kaiserkalender und beeinflusst, wie Daten dargestellt und geparst werden.  
* **`setLocale(new Locale("ja","JP"))`** – Ändert die Sprache und regionale Konventionen (z. B. Monate, Dezimaltrennzeichen). Dies ist der Kern von **how to set locale** für die Arbeitsmappe.  

Das Ausführen des Programms erzeugt `LocaleDemo.xlsx`. Öffnen Sie es in Excel oder LibreOffice und Sie werden japanische Monatsnamen, das japanische Yen‑Währungssymbol und nach dem japanischen Kalender formatierte Daten sehen.

## Arbeitsmappensprache ändern (Gebietsschema auf Japanisch setzen)

Wenn Ihr Hauptziel ist, **die Arbeitsmappensprache zu ändern**, können Sie sich ausschließlich auf den Aufruf von `setLocale` konzentrieren. Das folgende Snippet isoliert diesen Schritt:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Was ändert sich?**  
* Zellformatierungszeichenketten wechseln zu Japanisch (z. B. `#,##0.00` wird zu `#,##0.00` mit einem Yen‑Symbol).  
* Eingebaute Funktionsnamen (wie `SUM`) bleiben Englisch, weil das Funktions‑Gebietsschema von Excel unabhängig ist, aber Datumszeichenketten und Fehlermeldungen folgen japanischen Konventionen.  

**Wann sollte man das verwenden?**  
* Wenn Sie eine Tabelle benötigen, die Zahlen und Daten für ein japanisches Publikum anzeigt, der zugrunde liegende Kalender jedoch Gregorianisch bleiben kann.  
* Für Berichte, die als PDF exportiert oder gedruckt werden, um sicherzustellen, dass die visuelle Sprache dem Zielmarkt entspricht.

## Wie man den Kalender auf den japanischen Kalender einstellt

Manchmal ist die Anforderung **how to set calendar** getrennt vom Gebietsschema. Für Altsysteme, die Daten in der japanischen Kaiserära speichern, müssen Sie den Kalender explizit setzen, wobei Sie optional das Standard‑Gebietsschema beibehalten können.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Wichtige Punkte:**

* `Calendar.getInstance(Locale.JAPAN)` gibt ein `java.util.Calendar` zurück, das für die japanische Ära konfiguriert ist.  
* Die Arbeitsmappe wird nun Daten mit Ärasymbolen (R für Reiwa, H für Heisei usw.) darstellen.  
* Diese Einstellung wirkt sich **nicht** auf Zahlenformatierung oder UI‑Sprache aus; kombinieren Sie sie mit `setLocale`, wenn Sie beides benötigen.

## Vollständiges End‑zu‑End‑Beispiel

Unten finden Sie ein vollständiges, ausführbares Programm, das **how to set locale**, **change workbook language** und **set the calendar** in einem zusammenhängenden Ablauf demonstriert. Es fügt außerdem eine Beispielzelle hinzu, um die Wirkung zu veranschaulichen.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Erwartete Ausgabe:**  
Beim Öffnen von `FullJapaneseLocale.xlsx` wird die erste Zelle ein Datum wie `R3/04/01` (Reiwa 3) anzeigen und die zweite Zelle ist als `¥1,234,567.89` formatiert. Dies bestätigt, dass **how to set locale**, **change workbook language** und **how to set calendar** zusammen funktionieren.

## Häufige Fallstricke und wie man sie vermeidet

| Fallstrick | Warum es passiert | Lösung |
|------------|-------------------|--------|
| Verwendung von `Locale.CHINA` anstelle von `new Locale("ja","JP")` | `Locale.CHINA` setzt die chinesische Sprache, nicht Japanisch. | Instanziieren Sie immer `Locale` mit `"ja", "JP"` für Japanisch. |
| Vergessen, `settings.setCalendar(...)` nach `setLocale` aufzurufen | Der Kalender ist standardmäßig Gregorianisch, sodass Daten in der falschen Ära erscheinen. | Rufen Sie `setCalendar` **nach** dem Setzen des Gebietsschemas auf, oder setzen Sie beide zusammen wie gezeigt. |
| Speichern der Arbeitsmappe vor dem Anwenden der Einstellungen | Einstellungen werden auf das In‑Memory‑Objekt angewendet; ein frühes Speichern schreibt das Standard‑Gebietsschema. | Wenden Sie alle Gebietsschema‑/Kalender‑Änderungen **vor** dem Aufruf von `workbook.save()` an. |
| Verwendung einer veralteten Aspose.Cells‑Version | Ältere Versionen besitzen keine `setCalendar`‑Überladungen. | Aktualisieren Sie auf v23.9+ oder prüfen Sie die Release‑Notes für Gebietsschema‑Unterstützung. |

## Testen Ihrer Konfiguration

1. Führen Sie die Klasse **FullLocaleExample** aus.  
2. Öffnen Sie die erzeugte `FullJapaneseLocale.xlsx` in Excel.  
3. Überprüfen Sie, dass:  
   * Die Datumsspalte japanische Ärasymbole (`R`, `H` usw.) anzeigt.  
   * Die Zahlenspalte das Yen‑Symbol und Komma‑Trennzeichen verwendet.  
   * Alle eingebauten Fehlermeldungen (z. B. `#DIV/0!`) auf Japanisch erscheinen, falls die Arbeitsmappe Fehler enthält.  

Falls einer dieser Checks fehlschlägt, überprüfen Sie erneut, dass das `WorkbookSettings`‑Objekt, das Sie geändert haben, dieselbe Instanz ist, die beim Speichern verwendet wird.

## Nächste Schritte

* **Formeln lokalisieren** – Während das Gebietsschema die Formatierung steuert, können Sie auch benutzerdefinierte Funktionsnamen mit `FormulaParser` übersetzen.  
* **Gebietsschema auf bestehende Arbeitsmappen anwenden** – Laden Sie eine Arbeitsmappe mit `new Workbook

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}