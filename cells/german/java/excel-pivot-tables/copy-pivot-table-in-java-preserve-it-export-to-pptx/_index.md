---
category: general
date: 2026-03-01
description: Pivot‑Tabelle in Java kopieren und dabei die Pivot beibehalten, dann
  Excel nach PPTX exportieren, den Excel‑AutoFilter deaktivieren und Smart Marker
  für JSON‑Arrays verwenden – vollständige Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: de
og_description: Pivot‑Tabelle in Java kopieren, Pivot‑Definition beibehalten, nach
  PPTX exportieren, AutoFilter deaktivieren und Smart Marker verwenden – vollständige
  Anleitung für Entwickler.
og_title: Pivot‑Tabelle in Java kopieren – beibehalten, nach PPTX exportieren
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Pivot‑Tabelle in Java kopieren – beibehalten, nach PPTX exportieren
url: /de/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot‑Tabelle in Java kopieren – beibehalten, nach PPTX exportieren

Haben Sie jemals eine **Pivot‑Tabelle** von einer Arbeitsmappe in eine andere kopieren müssen, ohne die zugrunde liegende Pivot‑Definition zu verlieren? Sie sind nicht der Einzige, der darüber nachdenkt. In vielen realen Projekten werden Sie Daten verschieben, und das Letzte, was Sie wollen, ist ein kaputter Pivot, der zur Laufzeit Fehler wirft.  

In diesem Tutorial führen wir Sie durch eine vollständige Lösung, die nicht nur **Pivot‑Tabelle kopieren** ermöglicht, sondern Ihnen auch zeigt, wie Sie beim Kopieren **Pivot‑Tabelle beibehalten**, **Excel nach PPTX exportieren**, **Excel‑AutoFilter deaktivieren** und **Smart Marker verwenden**, um ein JSON‑Array in eine einzelne Zelle zu schieben. Am Ende haben Sie ein einzelnes, ausführbares Java‑Programm, das alle vier Szenarien abdeckt.

## Voraussetzungen

- Java 8 oder neuer (der Code funktioniert auch mit Java 11)  
- Aspose.Cells für Java Bibliothek (Version 23.9 oder später) – Sie können sie von Maven Central beziehen  
- Grundlegende Kenntnisse der Excel‑Konzepte wie Pivot‑Tabellen, Tabellen und Textfelder  

Falls Ihnen das Aspose.Cells‑JAR fehlt, fügen Sie Folgendes zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Jetzt tauchen wir ein.

## Schritt 1: Pivot‑Tabelle kopieren – Pivot‑Definition beibehalten

Wenn Sie einfach den Zellbereich, der eine Pivot‑Tabelle enthält, kopieren, bleiben die Pivot‑Metadaten häufig zurück. Aspose.Cells bietet uns eine elegante Möglichkeit, die Definition intakt zu halten, indem `copyRange` mit einer `CopyOptions`‑Instanz verwendet wird.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Warum das funktioniert:** `CopyOptions` weist Aspose.Cells an, alles zu übernehmen, einschließlich des Pivot‑Cache und der Feldeinstellungen. Ohne diese Option erhalten Sie nur reine Werte und verlieren die Möglichkeit, die Pivot‑Tabelle zu aktualisieren.

**Randfall:** Falls Ihre Quell‑Pivot‑Tabelle größer ist als der fest codierte Bereich `A1:G20`, passen Sie den Bereich entsprechend an oder verwenden Sie `sourceSheet.getPivotTables().get(0).getDataRange()`, um ihn dynamisch abzurufen.

![Beispiel für das Kopieren einer Pivot‑Tabelle](image.png "Pivot‑Tabelle in Java kopieren")

*Bildbeschreibung: Diagramm zum Kopieren einer Pivot‑Tabelle in Java*

## Schritt 2: Ein Arbeitsblatt mit editierbarem Textfeld nach PPTX exportieren

Oft müssen Sie ein Excel‑Blatt in eine PowerPoint‑Folien umwandeln – denken Sie an wöchentliche Dashboards, die präsentiert werden müssen. Aspose.Cells kann ein Arbeitsblatt direkt als PPTX‑Datei speichern und dabei Formen wie Textfelder erhalten.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Was passiert:** Die `save`‑Methode mit `SaveFormat.PPTX` konvertiert das gesamte Blatt, einschließlich jedes editierbaren Textfeldes, in eine PowerPoint‑Folien. Der Text im Feld bleibt editierbar, wenn Sie die PPTX in PowerPoint öffnen.

**Tipp:** Falls Sie mehrere Blätter haben und nur ein bestimmtes benötigen, rufen Sie `wb.getWorksheets().removeAt(index)` für die anderen auf, bevor Sie speichern.

## Schritt 3: Excel‑AutoFilter in einer Tabelle deaktivieren

AutoFilter ist praktisch für Endbenutzer, aber manchmal müssen Sie ihn programmgesteuert ausschalten – vielleicht vor dem Export von Daten oder beim Erstellen eines sauberen Berichts. So **deaktivieren Sie den Excel‑AutoFilter** in einer Excel‑Tabelle.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Warum Sie das benötigen könnten:** Der Export in Formate, die AutoFilter nicht unterstützen (wie CSV oder PDF), kann verirrte Filter‑Icons erzeugen. Durch das Deaktivieren wird ein sauberes Ergebnis sichergestellt.

**Häufige Falle:** Falls das Blatt keine Tabellen enthält, wirft `getTables().get(0)` eine `IndexOutOfBoundsException`. Überprüfen Sie in Produktionscode immer zuerst `sheet.getTables().size()`.

## Schritt 4: Smart Marker verwenden – JSON‑Array als einzelnen Zellenwert einfügen

Smart Marker ist Asposes Templating‑Engine. Ein nützlicher Trick ist, ein komplettes JSON‑Array als einzelnen Zellenwert zu behandeln, was sich ideal zum Protokollieren oder Weitergeben strukturierter Daten eignet. Lassen Sie uns **Smart Marker verwenden**, um dies zu erreichen.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Wie es funktioniert:** Der `${json}`‑Marker im Arbeitsbuch wird durch den gesamten JSON‑String ersetzt, weil wir `ArrayAsSingle` gesetzt haben. Ohne diese Option würde Aspose versuchen, jedes Array‑Element in separate Zeilen zu expandieren.

**Variation:** Falls Sie das Array über mehrere Zeilen verteilt benötigen, lassen Sie einfach `ArrayAsSingle` weg und lassen Sie Smart Marker die Expansion automatisch übernehmen.

## Vollständiges funktionierendes Beispiel – Alle Schritte kombiniert

Unten steht eine einzelne Java‑Klasse, die alle behandelten Vorgänge zusammenführt. Führen Sie sie als reguläre `main`‑Methode aus; passen Sie lediglich die Dateipfade an Ihre Umgebung an.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}