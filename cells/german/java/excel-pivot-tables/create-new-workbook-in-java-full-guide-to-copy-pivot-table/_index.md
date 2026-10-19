---
category: general
date: 2026-07-23
description: Erstellen Sie ein neues Arbeitsbuch in Java und lernen Sie, wie Sie Pivot‑Tabellen
  kopieren, Excel‑Bereiche kopieren und Pivot‑Tabellen mit Aspose.Cells in wenigen
  Minuten exportieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: de
lastmod: 2026-07-23
og_description: Erstellen Sie ein neues Arbeitsbuch in Java, kopieren Sie sofort die
  Pivot‑Tabelle, kopieren Sie den Excel‑Bereich und exportieren Sie dann die Pivot‑Tabelle
  mit Aspose.Cells. Folgen Sie diesem vollständigen Tutorial.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Neues Arbeitsbuch in Java erstellen – Pivot‑Tabelle Schritt für Schritt
  kopieren
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Neues Arbeitsbuch in Java erstellen – Vollständige Anleitung zum Kopieren von
  Pivot‑Tabellen
url: /de/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues Arbeitsbuch in Java erstellen – Vollständige Anleitung zum Kopieren von Pivot-Tabellen

Haben Sie sich jemals gefragt, wie man **create new workbook** in Java erstellt, während man eine komplexe Pivot‑Tabelle beibehält? Sie sind nicht der Einzige, der darüber nachdenkt. In vielen Reporting‑Apps müssen Sie eine Pivot‑Tabelle aus einer Quelldatei in ein neues Arbeitsbuch verschieben, vielleicht um sie an einen Kunden zu senden oder weitere Berechnungen durchzuführen. Die gute Nachricht? Mit ein paar Zeilen können Sie genau das tun – ohne manuelles Kopieren‑und‑Einfügen.

In diesem Tutorial führen wir Sie durch den gesamten Prozess: Laden der Quelldatei, Definieren des Bereichs, der die Pivot‑Tabelle enthält, **copying the Excel range**, Erstellen eines **new workbook**, und schließlich **exporting the pivot table** in eine neue Datei. Am Ende haben Sie ein eigenständiges, ausführbares Java‑Programm, das die Frage „**how to copy pivot**“ ohne Rätselraten beantwortet.

## Voraussetzungen

- Java 17 oder höher (der Code funktioniert mit jedem aktuellen JDK)
- Aspose.Cells for Java Bibliothek (Kostenlose Testversion oder lizenzierte Version)
- Eine Beispiel‑Datei `source.xlsx`, die eine Pivot‑Tabelle im Bereich `A1:G20` enthält
- Eine IDE oder ein Build‑Tool (Maven/Gradle) zur Verwaltung der Aspose.Cells‑JAR

Haben Sie das? Großartig – lassen Sie uns loslegen.

## Schritt 1: Projekt einrichten und Aspose.Cells importieren

Zuerst müssen Sie Aspose.Cells zu Ihrem Projekt hinzufügen. Wenn Sie Maven verwenden, fügen Sie diese Abhängigkeit in Ihre `pom.xml` ein:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Wenn Sie Gradle bevorzugen, lautet das Äquivalent:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Sobald die Bibliothek im Klassenpfad ist, importieren Sie die benötigten Klassen:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro Tipp:** Aspose.Cells ist eine kommerzielle Bibliothek, bietet aber eine voll funktionsfähige 30‑tägige Evaluation, die ein Wasserzeichen auf die Ausgabe setzt – perfekt, um es auszuprobieren.

## Schritt 2: Quell‑Arbeitsbuch laden

Jetzt werden wir **create new workbook** Objekte erstellen, aber zuerst benötigen wir die Quelle, die die Pivot‑Tabelle enthält. Dieser Schritt ist die Grundlage für jede **copy excel range**‑Operation, da das Bereichsobjekt genau weiß, welche Zellen (einschließlich des Pivot‑Caches) übertragen werden müssen.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Warum nicht einfach den Bereich direkt lesen? Weil die Metadaten der Pivot‑Tabelle im Pivot‑Cache des Arbeitsblatts gespeichert sind und Aspose.Cells diese automatisch bündelt, wenn Sie den Bereich kopieren.

## Schritt 3: Den Bereich definieren, der die Pivot‑Tabelle enthält

In vielen realen Dateien belegt die Pivot‑Tabelle ein rechteckiges Block. Für dieses Beispiel gehen wir davon aus, dass sie in `A1:G20` liegt. Sie können die Adresse natürlich an Ihr tatsächliches Layout anpassen.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Wenn Sie sich über die genaue Adresse nicht sicher sind, können Sie `sourceSheet.getCells().getMaxDataRow()` und `getMaxDataColumn()` verwenden, um die Grenzen dynamisch zu berechnen. Das ist ein praktischer Trick, wenn sich die Größe der Pivot‑Tabelle im Laufe der Zeit ändert.

## Schritt 4: **Create New Workbook** und Ziel‑Arbeitsblatt

Hier ist der Moment, in dem wir tatsächlich **create new workbook** erstellen, das den kopierten Inhalt erhalten wird. Denken Sie daran als die leere Leinwand, auf die Sie die Pivot‑Tabelle einfügen.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Warum mit einem leeren Arbeitsbuch beginnen? Es garantiert, dass keine versteckten Stile oder vorherigen Pivot‑Tabellen die Kopie beeinträchtigen, und liefert ein sauberes Ergebnis, bereit für **export pivot table**.

## Schritt 5: Pivot‑Tabelle kopieren (und ihren zugrunde liegenden Bereich)

Jetzt zum Kern des Tutorials: **copy pivot table**. Aspose.Cells behandelt das Kopieren eines Bereichs als Deep‑Copy, d.h. der Pivot‑Cache wird mit den Zellen übertragen. Deshalb erledigt diese eine Zeile die schwere Arbeit.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Falls Sie sich jemals gefragt haben, **how to copy pivot** ohne Funktionsverlust zu kopieren, das ist die Antwort. Das Ziel‑Blatt enthält jetzt eine voll funktionsfähige Pivot‑Tabelle, die Sie aktualisieren, ändern oder einfach exportieren können.

### Sonderfall: Beibehalten der Aktualisierungseinstellungen

Manchmal ist die Quell‑Pivot so eingestellt, dass sie beim Öffnen aktualisiert wird. Um dieses Verhalten beizubehalten, können Sie die Optionen der Pivot‑Tabelle explizit kopieren:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Dieses Snippet stellt sicher, dass die kopierte Pivot‑Tabelle sich exakt wie das Original verhält.

## Schritt 6: Ziel‑Arbeitsbuch speichern – **Export Pivot Table**

Abschließend **export pivot table**, indem wir das neue Arbeitsbuch auf die Festplatte speichern. Sie können jedes von Aspose unterstützte Format wählen: XLSX, XLS, CSV, PDF usw. Für diese Anleitung bleiben wir bei XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Wenn Sie die Datei über einen Web‑Service senden müssen, können Sie sie in einen `ByteArrayOutputStream` schreiben anstatt in einen Dateipfad – Aspose macht das trivial.

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier ein komplettes, sofort ausführbares Programm. Sie können es gerne kopieren, einfügen und in Ihrer IDE ausführen.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Erwartete Ausgabe

Wenn Sie das Programm ausführen, gibt die Konsole aus:

```
Pivot table copied successfully!
```

Und die Datei `copied_with_pivot.xlsx` erscheint in `YOUR_DIRECTORY`. Öffnen Sie sie in Excel, und Sie sehen die Pivot‑Tabelle unverändert, bereit zum Aktualisieren oder Bearbeiten.

## Häufige Fragen & Fehlersuche

- **Was, wenn die Quell‑Pivot über mehr als ein Arbeitsblatt verteilt ist?**  
  Sie müssen jeden relevanten Bereich separat kopieren und dann die Pivot‑Tabelle auf dem Ziel‑Blatt mit den `PivotTable`‑APIs neu erstellen.

- **Kann ich nur das Pivot‑Layout ohne die Daten kopieren?**  
  Setzen Sie vor dem Kopieren `sourceRange.setCopyDataOnly(false)`. Das weist Aspose an, den Cache zu behalten, aber nicht die zugrunde liegenden Quelldaten.

- **Gibt es eine Möglichkeit, die Pivot‑Tabelle in eine CSV‑Datei zu kopieren?**  
  CSV unterstützt keine Pivot‑Tabellen, aber Sie können das *Ergebnis* der Pivot‑Tabelle exportieren, indem Sie `pivotTable.calculate()` aufrufen und das Blatt dann als CSV speichern.

- **Warum verliert die kopierte Pivot‑Tabelle ihr Format?**  
  Das Format befindet sich in der Stil‑Sammlung. Nach dem Kopieren können Sie `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` aufrufen, um die Stile zu übertragen.

## Fazit

Wir haben Ihnen gerade gezeigt, wie Sie **create new workbook** in Java, **copy pivot table** und **export pivot table** – alles mit einem sauberen, reproduzierbaren Code‑Beispiel. Durch das Definieren des genauen **copy excel range**, die Nutzung der Deep‑Copy‑Semantik von Aspose.Cells und das Beibehalten optionaler Einstellungen können Sie praktisch jede Pivot‑Migrationsaufgabe automatisieren.

Bereit für den nächsten Schritt? Versuchen Sie, das Ausgabeformat zu PDF zu ändern oder durch mehrere Quelldateien zu iterieren, um Dutzende von Pivot‑Tabellen im Batch zu verarbeiten. Das gleiche Muster gilt – passen Sie einfach die Dateipfade und Bereichsadressen an.

Wenn Sie auf ein Problem stoßen, hinterlassen Sie unten einen Kommentar oder prüfen Sie die Aspose.Cells‑Dokumentation für erweiterte Pivot‑Manipulationen. Viel Spaß beim Programmieren und genießen Sie die Zeit, die Sie durch die Automatisierung dieser lästigen Kopier‑ und Einfüge‑Aufgaben gespart haben!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Pivot‑Tabellen in Excel mit Aspose.Cells für Java erstellt: Ein umfassender Leitfaden](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Wie man die Quelle einer Excel‑Pivot‑Tabelle mit Aspose.Cells für Java aktualisiert: Ein umfassender Leitfaden](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Wie man Excel nach HTML exportiert und erstellt mit Aspose.Cells Java | Workbook‑Operations‑Leitfaden](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}