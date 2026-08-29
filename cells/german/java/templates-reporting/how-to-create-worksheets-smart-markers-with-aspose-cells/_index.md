---
category: general
date: 2026-08-20
description: Erstellen Sie Smart‑Marker für Arbeitsblätter in Java mit Aspose.Cells
  und steuern Sie die Benennung von Detailblättern mit SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: de
lastmod: 2026-08-20
og_description: Erstellen Sie Smart Marker für Arbeitsblätter in Java mit Aspose.Cells.
  Erfahren Sie, wie Sie Detailblätter dynamisch mit SmartMarkerOptions benennen.
og_image_alt: create worksheets smart markers example diagram
og_title: Arbeitsblätter mit Smart Markern erstellen – Java‑Leitfaden mit Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Wie man Arbeitsblätter mit Smart‑Markern in Aspose.Cells erstellt
url: /de/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# So erstellen Sie Arbeitsblätter Smart Markers mit Aspose.Cells

Wenn Sie **Arbeitsblätter Smart Markers** in einer Java-Arbeitsmappe erstellen müssen, zeigt Ihnen diese Anleitung die genauen Schritte, um dies mit Aspose.Cells zu tun. Sie sehen, wie Sie `SmartMarkerOptions` konfigurieren, sodass jedes Detailblatt einen eindeutigen, vorhersehbaren Namen erhält.

Das Erzeugen von Excel-Berichten, die eine Master‑Detail‑Vorlage erweitern, ist eine häufige Anforderung in Finanz-, Bestands- und Berichtssystemen. Durch die Verwendung von Smart Markern entfällt das manuelle Duplizieren von Arbeitsblättern, und Sie können sich auf die Daten statt auf die Infrastruktur konzentrieren.

## Was Sie lernen werden

* Wie man eine Master-Arbeitsmappe lädt, die Smart Marker enthält.  
* Wie man `SmartMarkerOptions` einstellt, um die Benennung der erzeugten Detailblätter zu steuern.  
* Wie man eine `DataTable` mit Beispieldaten bereitstellt und sie auf die Smart Marker anwendet.  
* Wie man das Ergebnis speichert, sodass jedes Detailarbeitsblatt einen eindeutigen Namen hat und doppelte Blattnamen vermieden werden.

**Voraussetzungen**  
* Java 17 oder höher (der Code kompiliert auch mit JDK 8+).  
* Aspose.Cells für Java 23.9 oder neuer – die Bibliothek stellt die Klassen `Workbook`, `SmartMarkerOptions` und verwandte Klassen bereit.  
* Eine IDE wie IntelliJ IDEA, Eclipse oder VS Code.

Weitere Konzepte, denen Sie begegnen, umfassen **Aspose.Cells Java**, **smart marker options** und den Umgang mit **duplicate sheet names**, wenn die Vorlage erweitert wird.

## Arbeitsblätter Smart Markers erstellen – Schritt‑für‑Schritt‑Anleitung

Die folgenden Abschnitte teilen den Prozess in einzelne, wiederverwendbare Schritte auf. Jeder Schritt enthält ein Code‑Snippet, eine Erklärung, warum er wichtig ist, und praktische Tipps, um häufige Fallstricke zu vermeiden.

### Schritt 1: Maven‑Projekt einrichten und Aspose.Cells hinzufügen

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Warum dieser Schritt wichtig ist** – Die Bibliothek liefert die Klasse `Workbook`, die Excel‑Dateien liest und schreibt, sowie die Smart‑Marker‑Engine, die Ihre Vorlage automatisch erweitert. Ohne die korrekte Abhängigkeit kann der Compiler die später verwendeten API‑Aufrufe nicht auflösen.

> **Pro Tipp:** Wenn Sie hinter einem Unternehmens‑Proxy arbeiten, konfigurieren Sie `settings.xml` von Maven, um das Aspose‑Repository sicher abzurufen.

### Schritt 2: Master‑Arbeitsmappe laden, die Smart Marker enthält

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Warum dieser Schritt wichtig ist** – Die Master‑Arbeitsmappe definiert das Layout, Formeln und Platzhalter‑Tags (`«SmartMarker»`), die die Engine ersetzen wird. Das einmalige Laden der Datei hält den Speicherverbrauch gering und ermöglicht die Wiederverwendung derselben Arbeitsmappe für mehrere Datensätze.

### Schritt 3: SmartMarkerOptions für benutzerdefinierte Detailblattnamen konfigurieren

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Warum dieser Schritt wichtig ist** – Standardmäßig erstellt Aspose.Cells Detailblätter mit generischen Namen wie „DetailSheet“. Wenn die Vorlage für viele Zeilen erweitert wird, kollidieren diese Namen, was zu **duplicate sheet names** und einer Laufzeit‑Ausnahme führt. Das Muster `"DetailSheet_{0}"` garantiert einen eindeutigen Namen pro Zeile und löst das Duplikationsproblem.

### Schritt 4: DataTable erstellen, die zu den Smart‑Marker‑Feldern passt

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Warum dieser Schritt wichtig ist** – Die `DataTable` liefert die tatsächlichen Werte, die die Smart‑Marker‑Platzhalter ersetzen. Spaltennamen müssen mit den Markernamen in der Vorlage übereinstimmen; andernfalls überspringt die Engine die Ersetzung stillschweigend.

> **Häufiger Fehler:** Die Verwendung eines Spaltennamens, der sich nur in der Groß‑/Kleinschreibung unterscheidet (z. B. „id“ vs „Id“), führt zu fehlenden Daten in den erzeugten Arbeitsblättern.

### Schritt 5: Daten mit den Namensoptionen auf die Smart Marker anwenden

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Warum dieser Schritt wichtig ist** – Die Methode `apply` löst die Smart‑Marker‑Engine aus. Sie liest jede Zeile, erstellt ein neues Detailblatt anhand des Namensmusters aus `SmartMarkerOptions` und füllt das Blatt mit den Daten der jeweiligen Zeile. Dieser einzelne Aufruf ersetzt Dutzende von Zeilen manuellem Kopieren von Blättern und Befüllen von Zellen.

### Schritt 6: Arbeitsmappe speichern und Ergebnis überprüfen

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Nach der Ausführung öffnen Sie `MasterDetailDuplicatedNames.xlsx`. Sie sollten sehen:

* Das ursprüngliche Master‑Blatt bleibt unverändert.  
* Zwei neue Arbeitsblätter mit den Namen `DetailSheet_1` und `DetailSheet_2`.  
* Jedes Detailblatt enthält die Werte aus der entsprechenden Zeile der `DataTable`.

**Warum dieser Schritt wichtig ist** – Das Persistieren der Arbeitsmappe finalisiert die Smart‑Marker‑Erweiterung. Die Datei kann nun an nachgelagerte Systeme gesendet, an E‑Mails angehängt oder in Excel für weitere Analysen geöffnet werden.

## Umgang mit Randfällen und Variationen

### Mehrere Master‑Blätter

Wenn Ihre Vorlage mehr als ein Master‑Blatt enthält, iterieren Sie über die Smart‑Marker jedes Blatts:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Benutzerdefinierte Benennung über den Zeilenindex hinaus

Sie können jede Daten­spalte in den Blattnamen einbetten, indem Sie Platzhalter wie `{ColumnName}` verwenden:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Stellen Sie sicher, dass die Spalte `OrderId` in der bereitgestellten `DataTable` vorhanden ist.

### Verhindern zu langer Blattnamen

Excel begrenzt Blattnamen auf 31 Zeichen. Wenn Ihr Namensmuster diese Grenze überschreiten könnte, kürzen Sie den Wert oder erzeugen Sie einen Hash:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Verarbeiten Sie den erzeugten Namen anschließend mit `StringUtils.abbreviate`, bevor Sie ihn an Aspose übergeben.

## Vollständiges ausführbares Beispiel

Unten finden Sie die vollständige Quelldatei, die Sie kopieren, die Dateipfade anpassen und direkt ausführen können:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Erwartete Ausgabe**

* `MasterDetailDuplicatedNames.xlsx` enthält:

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Aspose.Cells Java meistern: Smart Marker für dynamische Daten in Arbeitsblättern verwenden](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Dynamische Diagramme mit Smart Markern in Aspose.Cells für Java erstellen | Schritt‑für‑Schritt‑Anleitung](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Arbeitsblätter](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}