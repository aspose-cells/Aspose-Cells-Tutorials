---
category: general
date: 2026-08-14
description: Kopieren Sie Bereiche zwischen Arbeitsmappen mit Java und Aspose.Cells.
  Erfahren Sie, wie Sie eine Pivot‑Tabellen‑Arbeitsmappe kopieren, ein Bild nach PowerPoint
  exportieren und den AutoFilter aus einer Excel‑Tabelle entfernen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: de
lastmod: 2026-08-14
og_description: Bereich zwischen Arbeitsmappen in Java kopieren. Dieser Leitfaden
  zeigt, wie man eine Pivot‑Tabellen‑Arbeitsmappe kopiert, ein Bild nach PowerPoint
  exportiert und den AutoFilter aus einer Excel‑Tabelle entfernt.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Bereich zwischen Arbeitsmappen in Java kopieren – vollständiges Aspose.Cells‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Bereich zwischen Arbeitsmappen in Java kopieren – Schritt‑für‑Schritt‑Anleitung
url: /de/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bereich zwischen Arbeitsmappen in Java kopieren – Schritt‑für‑Schritt‑Anleitung

Wenn Sie in Java **Bereich zwischen Arbeitsmappen kopieren** müssen, bietet Aspose.Cells eine saubere API, die komplexe Objekte wie Pivot‑Tabellen und Bilder verarbeitet. Dieses Tutorial zeigt, wie man **Pivot‑Tabellen‑Arbeitsmappe kopiert**, **Bild nach PowerPoint exportiert** und **AutoFilter aus einer Excel‑Tabelle entfernt**, während der Code leicht lesbar und wartbar bleibt.

Sie lernen, wie Sie:

* Eine Quell‑Arbeitsmappe laden und den Quell‑Bereich definieren.  
* Eine Ziel‑Arbeitsmappe erstellen und den Bereich so kopieren, dass die Pivot‑Tabelle intakt bleibt.  
* Das erste Bild auf dem Blatt als editierbares PowerPoint‑Objekt exportieren.  
* Einen AutoFilter aus der ersten Excel‑Tabelle entfernen.  
* Eine Arbeitsmappe mit `SmartMarkerOptions` laden, um JSON‑Arrays als einzelnen Zellenwert zu behandeln.

Das Beispiel verwendet Aspose.Cells 23.10 für Java, die Konzepte gelten jedoch auch für frühere Versionen.

---

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Java 17 oder neuer | Erforderlich für die neueste Aspose.Cells‑Laufzeit. |
| Aspose.Cells für Java (Maven‑Artefakt `com.aspose:aspose-cells`) | Stellt die im Code verwendeten Klassen `Workbook`, `Worksheet`, `Range` und verwandte Klassen bereit. |
| Eine Quell‑Excel‑Datei (`src.xlsx`), die eine Pivot‑Tabelle, ein Bild und eine Tabelle mit einem AutoFilter enthält. | Das Tutorial manipuliert diese Objekte, um jede Funktion zu demonstrieren. |

Fügen Sie die Maven‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Bereich zwischen Arbeitsmappen kopieren – Quelle und Ziel laden

Der erste Schritt besteht darin, die Quell‑Arbeitsmappe zu öffnen, den Bereich auszuwählen, der die zu kopierenden Daten enthält, und eine leere Ziel‑Arbeitsmappe zu erstellen.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Warum das wichtig ist:** Durch die Verwendung von `Range.copy` kopiert Aspose.Cells nicht nur rohe Zellwerte, sondern auch den zugrunde liegenden Pivot‑Cache, sodass die Pivot‑Tabelle im Ziel‑Workbook funktionsfähig bleibt.

---

## Pivot‑Tabellen‑Arbeitsmappe beim Kopieren des Bereichs kopieren

Jetzt kopieren Sie den definierten Bereich von der Quell‑Arbeitsmappe in die Ziel‑Arbeitsmappe. Die Pivot‑Tabelle wird automatisch erhalten, weil der Bereich den Pivot‑Cache einschließt.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Ergebnis:** Beim Öffnen von `destination.xlsx` wird das gleiche Pivot‑Tabellen‑Layout wie in `src.xlsx` angezeigt. Es ist kein zusätzlicher Code erforderlich, um den Pivot‑Cache neu zu erstellen.

---

## Bild nach PowerPoint exportieren

Aspose.Cells kann ein Bild markieren, damit es als editierbares PowerPoint‑Objekt exportiert wird. Der folgende Code wählt das erste Bild auf dem Ziel‑Blatt aus und setzt das Export‑Flag.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Was Sie sehen:** Beim Öffnen von `destination.pptx` in PowerPoint wird das Bild als native Form angezeigt, die Sie bearbeiten, skalieren oder animieren können.

---

## AutoFilter aus Excel‑Tabelle entfernen

Wenn das Quell‑Blatt eine Tabelle mit einem AutoFilter enthält, möchten Sie diesen nach dem Kopieren möglicherweise entfernen. Der untenstehende Code greift auf die erste Tabelle zu und entfernt deren Filter.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Auswirkung:** Die Tabelle bleibt in der Arbeitsmappe, aber die Dropdown‑Filter‑Pfeile verschwinden, sodass Sie eine saubere Datenansicht erhalten.

---

## Arbeitsmappe mit SmartMarker‑Optionen laden – JSON‑Arrays als einzelne Zelle behandeln

Wenn Sie einen Bericht aus JSON generieren, kann Aspose.Cells ein ganzes Array als einzelnen Zellenwert behandeln. Das ist nützlich, um JSON‑Strings in eine Vorlage einzubetten, ohne sie in mehrere Zellen zu expandieren.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Warum Sie das verwenden könnten:** Wenn Ihre JSON‑Payload ein Array enthält, das als JSON‑String in einer einzelnen Zelle erscheinen soll, verhindert `setArrayAsSingle(true)`, dass Aspose.Cells das Array in separate Zeilen oder Spalten aufteilt.

![Bereich zwischen Arbeitsmappen in Java – Aspose.Cells Codebeispiel](copy-range-workbooks.png)

*Bild‑Alt‑Text:* **Bereich zwischen Arbeitsmappen in Java – Aspose.Cells Codebeispiel** (entspricht dem primären Schlüsselwort).

---

## Erwartete Ausgabe

| Dateiname                | Enthält |
|--------------------------|----------|
| `destination.xlsx`       | Kopierter Bereich mit funktionierender Pivot‑Tabelle. |
| `destination.pptx`       | Exportiertes Bild als editierbare PowerPoint‑Form. |
| `final_output.xlsx`      | Tabelle ohne AutoFilter‑Pfeile. |
| `template_filled.xlsx`   | JSON‑Array als einzelner Zellenwert gespeichert. |

Öffnen Sie jede Datei in der jeweiligen Anwendung (Excel oder PowerPoint), um zu überprüfen, ob die Vorgänge erfolgreich waren.

---

## Fazit

Sie wissen jetzt, wie Sie **Bereich zwischen Arbeitsmappen kopieren** in Java mit Aspose.Cells, dabei eine Pivot‑Tabelle erhalten, ein Bild nach PowerPoint exportieren und einen AutoFilter aus einer Excel‑Tabelle entfernen. Das gleiche Muster lässt sich erweitern, um jeden Excel‑Bereich in eine neue Arbeitsmappe zu kopieren, SmartMarker‑JSON‑Arrays zu verarbeiten oder weitere Transformationen zu verketten.

Nächste Schritte, die Sie erkunden könnten:

* **Excel‑Bereich in neue Arbeitsmappe kopieren** mit mehreren Arbeitsblättern.  
* Verwenden Sie **Bild nach PowerPoint exportieren** für die stapelweise Bildextraktion.  
* **AutoFilter aus Excel‑Tabelle entfernen** in größeren Reporting‑Pipelines anwenden.  
* Kombinieren Sie diese Techniken mit Aspose.Slides für eine vollständige Excel‑zu‑PowerPoint‑Automatisierung.

Experimentieren Sie gern mit unterschiedlichen Bereichsadressen, mehreren Pivot‑Tabellen oder benutzerdefinierten Bildformaten. Die Aspose.Cells‑API ist für programmatische Flexibilität konzipiert, sodass Sie die hier gezeigten Muster an jede Unternehmens‑Excel‑Automatisierungssituation anpassen können.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Bilder zwischen Arbeitsblättern in Excel mit Aspose.Cells für Java kopieren: Ein umfassender Leitfaden](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Seitenlayout‑Einstellungen zwischen Arbeitsblättern in Excel mit Aspose.Cells Java kopieren](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel‑Arbeitsblätter zwischen Arbeitsmappen kopieren](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}