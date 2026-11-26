---
category: general
date: 2026-11-25
description: Erstellen Sie ein Java‑Codebeispiel für eine Excel‑Arbeitsmappe, das
  Aspose.Cells‑Smart‑Markers verwendet, um JSON‑Arrays als Einzelwerte zu binden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: de
lastmod: 2026-11-25
og_description: Erstellen Sie ein Excel‑Arbeitsbuch in Java mit Aspose.Cells, um JSON‑Arrays
  einfach als einzelne Zellen zu exportieren. Folgen Sie der Schritt‑für‑Schritt‑Anleitung.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Excel-Arbeitsmappe in Java erstellen – Aspose.Cells Smart‑Marker‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Wie man ein Excel‑Arbeitsbuch in Java mit Aspose.Cells‑Markern erstellt
url: /de/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Excel‑Arbeitsbuch in Java mit Aspose.Cells‑Markern erstellt

Wenn Sie **Excel‑Arbeitsbuch Java**‑Code benötigen, der ein JSON‑Array in eine einzelne Zelle schreibt, zeigt Ihnen dieses Tutorial genau, wie es geht. Mit den Smart‑Markers von Aspose.Cells können Sie ein komplettes Array als einen einzigen Wert behandeln und so manuelle Schleifen sowie Zell‑für‑Zell‑Schreibvorgänge vermeiden.

Sie lernen, wie Sie ein Arbeitsbuch einrichten, einen Smart‑Marker definieren, eine `Map`‑Datenquelle binden, die ein JSON‑ähnliches Array enthält, und schließlich die Datei speichern. Das Beispiel funktioniert mit Java 17+, Maven und der kostenlosen Aspose.Cells‑für‑Java‑Testbibliothek.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers"}

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Java 17 oder höher | Die neuesten Sprachfeatures und Sicherheitsupdates |
| Maven 3.6+ | Vereinfacht das Verwalten von Abhängigkeiten |
| Aspose.Cells for Java (v23.12 oder neuer) | Stellt die `Workbook`, `Worksheet` und Smart‑Marker‑APIs bereit, die im Beispiel verwendet werden |
| Grundkenntnisse von Java‑Collections | Sie erstellen eine `Map<String, Object>`, die als Datenquelle dient |

Fügen Sie die Aspose.Cells‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Excel‑Arbeitsbuch Java erstellen – vollständiges Beispiel

Das folgende Programm ist eine **komplette, ausführbare** Lösung. Kopieren Sie es in eine Datei namens `ExcelSmartMarkerDemo.java`, kompilieren und führen Sie sie aus.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Was der Code macht

1. **Erstellt ein frisches Arbeitsbuch** – `new Workbook()` liefert Ihnen ein Excel‑Datei‑Objekt im Speicher mit einem Standard‑Blatt.  
2. **Platziert einen Smart‑Marker in Zelle A1** – `{{jsonArray:ArrayAsSingle}}` weist Aspose.Cells an, den Marker durch das *gesamte* Array zu ersetzen, durch Kommas getrennt.  
3. **Erstellt eine `Map`‑Datenquelle** – Der Schlüssel `"jsonArray"` entspricht dem Markernamen; der Wert ist ein `String[]`.  
4. **Ruft `setSmartMarkerData` auf** – Bindet die Map an den Marker und führt den Ersetzungsvorgang aus.  
5. **Speichert die Datei** – `workbook.save(...)` schreibt `JsonSingleValue.xlsx` auf die Festplatte.

Wenn Sie die erzeugte Excel‑Datei öffnen, enthält Zelle **A1**:

```
One, Two, Three
```

Das Array wird als einzelner, kommagetrennter String dargestellt, weil die Option `ArrayAsSingle` verwendet wurde.

---

## Aspose.Cells‑Smart‑Marker zum Binden von JSON‑Daten verwenden

Aspose.Cells‑Smart‑Marker sind ein leistungsstarkes Mittel, um komplexe Objekte (einschließlich JSON‑ähnlicher Strukturen) direkt auf Arbeitsblätter abzubilden. Die Syntax `{{fieldName:Option}}` funktioniert ähnlich wie eine Template‑Engine:

* **fieldName** – der Schlüssel in Ihrer Datenquelle (`Map`, POJO oder `DataTable`).  
* **Option** – steuert, wie Sammlungen behandelt werden. `ArrayAsSingle` behandelt die gesamte Sammlung als einen Wert; andere Optionen wie `Array` würden das Array über Zeilen hinweg ausdehnen.

**Warum einen Smart‑Marker statt einer Schleife verwenden?**  
Eine Schleife erfordert manuelle Berechnungen von Zelladressen, fehleranfällige Indizierung und zusätzlichen Code für das Styling. Smart‑Marker ermöglichen deklarative Platzhalter, halten Ihren Java‑Code kurz und überlassen der Bibliothek die Layout‑Details.

---

## Die Java‑Map‑Datenquelle einrichten

Die `Map<String, Object>` ist der einfachste Datencontainer für Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*Der Schlüssel (`jsonArray`) muss exakt mit dem Markernamen übereinstimmen.*  
Sie können auch eine `List<String>`, ein benutzerdefiniertes POJO oder sogar eine verschachtelte `Map` für komplexere JSON‑Strukturen verwenden. Aspose.Cells traversiert den Objektgraphen automatisch.

**Tipp:** Wenn Sie den zusammengefügten String anders formatieren möchten (z. B. mit Semikolons), verarbeiten Sie das Array in Java, bevor Sie es der Map zuweisen:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Das Arbeitsbuch speichern und die Ausgabe prüfen

```java
workbook.save("JsonSingleValue.xlsx");
```

Die `save`‑Methode unterstützt viele Formate (`.xlsx`, `.xls`, `.csv`, `.pdf`). Für dieses Tutorial bleiben wir beim Standard‑Excel‑Open‑XML‑Format.

**Verifizierungsschritte**

1. Öffnen Sie `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc oder Google Sheets.  
2. Stellen Sie sicher, dass Zelle **A1** den Text `One, Two, Three` enthält.  
3. Prüfen Sie, dass keine zusätzlichen Zeilen oder Spalten hinzugefügt wurden – der Smart‑Marker hat die Ersetzung an Ort und Stelle durchgeführt.

Falls die Zelle den rohen Marker‑Text (`{{jsonArray:ArrayAsSingle}}`) anzeigt, überprüfen Sie Folgendes:

* Der Markenname stimmt exakt (Groß‑/Kleinschreibung) mit dem Map‑Schlüssel überein.  
* `setSmartMarkerData` wird **nach** dem Platzieren des Markers aufgerufen.  
* Die verwendete Aspose.Cells‑Version unterstützt die Option `ArrayAsSingle` (verfügbar seit v20.3).

---

## Häufige Varianten und Sonderfälle

| Szenario | Anpassung |
|----------|-----------|
| **Anderer Trenner** | Verwenden Sie `ArrayAsSingle` zusammen mit einem benutzerdefinierten Join in Java (siehe Tipp oben). |
| **Mehrere Arrays in einem Blatt** | Platzieren Sie zusätzliche Marker wie `{{anotherArray:ArrayAsSingle}}` in anderen Zellen und fügen Sie entsprechende Einträge zur Map hinzu. |
| **Verschachtelte JSON‑Objekte** | Stellen Sie eine verschachtelte `Map<String, Object>` bereit; referenzieren Sie Felder mit Punktnotation (`{{parent.child}}`). |
| **Große Datenmengen** | Für tausende Zeilen bevorzugen Sie die Option `Array`, damit Aspose.Cells die Zeilen automatisch erweitert, was |

## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}