---
date: '2026-08-16'
description: Erfahren Sie, wie Sie Globalisierung in Java mit Aspose.Cells hinzufügen,
  Excel-Fehlermeldungen anpassen und die Maven-Abhängigkeit einrichten.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Erfahren Sie, wie Sie Globalisierung in Java mit Aspose.Cells hinzufügen,
  Excel-Fehlermeldungen anpassen und die Maven-Abhängigkeit einrichten. Folgen Sie
  der Schritt-für-Schritt-Anleitung.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Wie man Globalisierung in Java mit Aspose.Cells hinzufügt
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Wie man Globalisierung in Java mit Aspose.Cells hinzufügt
url: /de/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Globalisierung in Java mit Aspose.Cells hinzufügt

## Einführung

Das Hinzufügen von Globalisierung zu Ihrer Java‑Arbeitsmappe ermöglicht es Ihnen, Fehlermeldungen, boolesche Werte und andere lokalspezifische Zeichenketten in der Sprache anzuzeigen, die Ihre Benutzer erwarten. In diesem Tutorial lernen Sie **wie man Globalisierung** für Russisch hinzufügt, aber dasselbe Muster funktioniert für jede Sprache. Am Ende der Anleitung können Sie:

- Standard‑Fehlertexte und boolesche Darstellungen überschreiben.
- Ihre benutzerdefinierten Einstellungen auf jede `Workbook`‑Instanz anwenden.
- Die Lösung in ein typisches Maven‑basiertes Java‑Projekt integrieren.

Bereit, Ihre Excel‑Dateien wirklich mehrsprachig zu machen? Lassen Sie uns zunächst prüfen, ob Ihre Entwicklungsumgebung die Voraussetzungen erfüllt.

## Schnelle Antworten
- **Was ist Globalisierung in Aspose.Cells?** Es ist ein Satz lokalisierter Zeichenketten (Fehler, Booleans usw.), die Sie durch benutzerdefinierten Text ersetzen können.  
- **Welches Maven‑Artefakt wird benötigt?** `com.aspose:aspose-cells:25.3`.  
- **Kann ich andere Sprachen als Russisch anvisieren?** Ja – erweitern Sie `GlobalizationSettings` und überschreiben Sie die benötigten Methoden für jedes Locale.  
- **Benötige ich eine Lizenz für die Entwicklung?** Eine kostenlose Testversion funktioniert für Tests; eine permanente Lizenz entfernt Evaluations‑Wasserzeichen.  
- **Ist die Lösung thread‑sicher?** Einstellungen pro Arbeitsmappe anwenden; das `GlobalizationSettings`‑Objekt selbst ist nach der Erstellung unveränderlich.

## Was ist Globalisierung in Aspose.Cells?

`GlobalizationSettings` ist das Konfigurationsobjekt von Aspose.Cells, das lokalspezifische Zeichenketten wie Fehlermeldungen, boolesche Werte, Währungssymbole und Datumsformate steuert. Indem Sie Ihre eigene Unterklasse bereitstellen, teilen Sie der Bibliothek mit, welcher Text für jede Kultur angezeigt werden soll, sodass Sie die standardmäßigen englischen Zeichenketten durch Übersetzungen ersetzen können, die der Sprache und den regionalen Konventionen des Endbenutzers entsprechen.

## Warum benutzerdefinierte Globalisierung hinzufügen?

Aspose.Cells unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate** – darunter XLSX, CSV, PDF und ODS – und kann Arbeitsmappen mit **bis zu 200 000 Zeilen** verarbeiten, ohne die gesamte Datei in den Speicher zu laden. Die Anpassung der Globalisierung stellt sicher, dass Endbenutzer Nachrichten in ihrer Muttersprache sehen, wodurch die Anzahl der Support‑Tickets bei multinationalen Einsätzen um geschätzte **30 %** reduziert wird.

## Voraussetzungen

- **Java Development Kit** 8 oder neuer.
- **IDE** wie IntelliJ IDEA oder Eclipse.
- **Aspose.Cells for Java** Version 25.3 (oder neuer) über Maven oder Gradle hinzugefügt.

### Einrichtung von Aspose.Cells für Java

Add the Maven dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Or, if you prefer Gradle, insert the following into `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Lizenzbeschaffung

Aspose offers several licensing options:

- **Free trial** – vollständige Funktionsbewertung für 30 Tage.  
- **Temporary license** – unbegrenzte Evaluierung ohne Wasserzeichen.  
- **Commercial license** – produktionsreif, mit Prioritäts‑Support.

After obtaining a license file, set it once at application startup:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Wie fügt man Globalisierung für Russisch hinzu?

Ein `Workbook`‑Objekt repräsentiert eine Excel‑Datei, die im Speicher geladen ist, und bietet Zugriff auf ihre Tabellen, Zellen und Einstellungen. Laden Sie Ihre Arbeitsmappe, erstellen Sie eine Unterklasse von `GlobalizationSettings` und hängen Sie sie an die Arbeitsmappe an. Die direkte Antwort lautet: **eine benutzerdefinierte `GlobalizationSettings`‑Klasse instanziieren, `getErrorValueString` und `getBooleanValueString` überschreiben und dann `workbook.setGlobalizationSettings(customSettings)` aufrufen**. Dieser zweistufige Ansatz ersetzt die standardmäßigen russischen Zeichenketten durch Ihre eigenen.

### Definition der benutzerdefinierten Einstellungen

Das erste Mal, dass Sie in diesem Leitfaden `GlobalizationSettings` erwähnen, beachten Sie die Definition:

`GlobalizationSettings` ist die Basisklasse, die Aspose.Cells verwendet, um lokalspezifische Zeichenketten abzurufen.  

Erstellen Sie nun eine Unterklasse, die russisch‑spezifischen Text zurückgibt:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Anwenden der Einstellungen auf eine Arbeitsmappe

Nachdem Sie die Unterklasse definiert haben, hängen Sie sie an jede `Workbook`‑Instanz an:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Praktische Anwendungen

- **Finanzberichterstattung** – Fehlermeldungen in der Muttersprache des Buchhalters anzeigen, Missinterpretationen reduzieren.  
- **Unternehmensweite Werkzeuge** – dieselbe Globalisierungslogik in Dutzenden interner Excel‑basierter Hilfsprogramme einbetten.  
- **Automatisierte Datenpipelines** – sicherstellen, dass nachgelagerte Systeme lokalisierte Werte erhalten, ohne zusätzliche Übersetzungsschritte.

## Leistungsüberlegungen

Wenn Sie benutzerdefinierte Globalisierung aktivieren, verarbeitet Aspose.Cells weiterhin Formeln und I/O mit derselben hohen Leistung. Um den Speicherverbrauch niedrig zu halten:

- Arbeitsmappen‑Referenzen (`wb.dispose()`) nach dem Speichern freigeben.  
- `CalculationOptions.setEnableIterativeCalculation(true)` nur bei Bedarf verwenden.  
- Den JVM‑Heap (`-Xmx2g`) für Arbeitsmappen größer als 100 MB anpassen.

## Häufig gestellte Fragen

**F: Kann ich dieselben Globalisierungseinstellungen gleichzeitig auf mehrere Arbeitsmappen anwenden?**  
**A:** Ja. Erstellen Sie eine einzelne `RussianGlobalization`‑Instanz und übergeben Sie sie jeder Arbeitsmappe über `setGlobalizationSettings`.

**F: Was ist, wenn ich eine Sprache unterstützen muss, die ein Rechts‑nach‑Links‑Schriftsystem verwendet?**  
**A:** Überschreiben Sie zusätzliche Methoden wie `getCurrencySymbol` und `getDatePattern` in Ihrer Unterklasse, um geeignete RTL‑Symbole zurückzugeben.

**F: Ist für die Testversion eine Lizenz erforderlich, um benutzerdefinierte Globalisierung zu verwenden?**  
**A:** Nein. Die Testversion unterstützt `GlobalizationSettings` vollständig; nur Evaluations‑Wasserzeichen erscheinen bei bestimmten Ausgabeformaten.

**F: Wie kann ich falsche Fehlermeldungen debuggen?**  
**A:** Fügen Sie `System.out.println`‑Anweisungen in Ihren überschriebenen Methoden ein, um zu prüfen, ob der Eingabewert `err` mit Ihren Switch‑Fällen übereinstimmt.

**F: Beeinflusst dies die Berechnungsgeschwindigkeit von Formeln?**  
**A:** Vernachlässigbar. Die Bibliothek sucht die Zeichenkette nur beim Rendern von Zellwerten, nicht während Zwischenschritten der Berechnung.

## Zusätzliche Ressourcen

- **Dokumentation**: Detaillierte Anleitungen finden Sie unter [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Download**: Greifen Sie auf die neuesten Releases zu unter [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Kauf**: Kaufen Sie eine Lizenz für die kommerzielle Nutzung unter [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Kostenlose Testversion**: Beginnen Sie mit einer kostenlosen Testversion von [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporäre Lizenz**: Erhalten Sie eine temporäre Lizenz über [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support**: Holen Sie sich Hilfe von der Community im [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Zuletzt aktualisiert:** 2026-08-16  
**Getestet mit:** Aspose.Cells 25.3 für Java  
**Autor:** Aspose

## Verwandte Tutorials

- [Aspose.Cells Java: Leitfaden für benutzerdefinierte Berechnungs-Engine](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Wie man Aspose Cells verwendet – Excel‑Engine‑Tutorials für Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven‑Abhängigkeit – Excel‑Datenverbindungen mit Aspose.Cells in Java verwalten](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}