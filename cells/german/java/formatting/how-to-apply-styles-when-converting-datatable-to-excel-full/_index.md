---
category: general
date: 2026-06-21
description: Wie man beim Konvertieren einer DataTable nach Excel in Java Stile anwendet.
  Lernen Sie, eine DataTable nach Excel zu importieren, benutzerdefinierte Stile hinzuzufügen
  und die Arbeitsmappe in wenigen Minuten in einer Datei zu speichern.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: de
og_description: Wie man beim Konvertieren einer DataTable nach Excel in Java Stile
  anwendet. Dieser Leitfaden zeigt, wie man eine DataTable nach Excel importiert,
  benutzerdefinierte Stile hinzufügt und die Arbeitsmappe in einer Datei speichert.
og_title: Wie man beim Konvertieren einer DataTable in Excel Stile anwendet – Java‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  headline: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  type: TechArticle
- description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  name: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  steps:
  - name: 5.1 Conditional Formatting Instead of Fixed Styles
    text: If you need to highlight rows where `Score > 90`, you can add a `ConditionalFormattingCollection`
      after the import. This gives you dynamic coloring without hard‑coding extra
      styles.
  - name: 5.2 Merging Cells for Titles
    text: Sometimes a report needs a big title spanning multiple columns. Use `worksheet.getCells().merge(0,
      0, 1, 3)` and then apply a distinct style to that merged region.
  - name: 5.3 Large DataSets – Performance Considerations
    text: When dealing with >100k rows, set `ImportDataTableOptions` to `ImportDataTableOptions.NO_FORMATTING`
      first, then apply styles in a second pass. This avoids the overhead of styling
      each cell during import.
  - name: 5.4 Multi‑Sheet Export
    text: If you have several `DataTable`s, just create additional worksheets via
      `workbook.getWorksheets().add("Sheet2")` and repeat the **import datatable to
      excel** step for each sheet.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- DataTable
title: Wie man beim Konvertieren einer DataTable nach Excel Stile anwendet – Vollständiger
  Java‑Leitfaden
url: /de/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man beim Konvertieren von DataTable zu Excel Stile anwendet – Vollständiger Java‑Leitfaden

Haben Sie sich jemals gefragt, **wie man Stile anwendet**, wenn Sie **DataTable zu Excel konvertieren** müssen? Sie sind nicht allein. In vielen internen Tools holen wir Daten aus Datenbanken, stecken sie in ein `DataTable` und erwarten dann eine hübsch aussehende Tabelle, ohne zusätzlichen Aufwand. Spoiler: Sie müssen der Bibliothek *genau* sagen, was „hübsch“ bedeutet.

In diesem Tutorial gehen wir ein vollständiges, sofort ausführbares Beispiel durch, das **zeigt, wie man Stile anwendet** mit Aspose.Cells für Java, ein `DataTable` nach Excel importiert, **benutzerdefinierte Excel‑Stile hinzufügt** und schließlich **die Arbeitsmappe in eine Datei speichert**. Am Ende haben Sie einen wiederverwendbaren Code‑Snippet, den Sie in jedes Projekt einbinden können.

---

## Was Sie benötigen

- **Java 17** (oder ein aktuelles JDK) – der Code funktioniert auch mit Java 8+.  
- **Aspose.Cells for Java** JAR (die kostenlose Testversion funktioniert zum Testen).  
- Eine `DataTable`‑Quelle – wir simulieren eine einfache, Sie können aber jede reale Abfrage‑Ergebnis einsetzen.  
- Eine IDE Ihrer Wahl (IntelliJ, Eclipse, VS Code … Sie entscheiden).

Es werden keine zusätzlichen Build‑Tools benötigt; ein einfaches Maven `pom.xml` reicht aus, Sie können das JAR aber auch manuell hinzufügen.

---

## Schritt 1: Projekt und Abhängigkeiten einrichten

Zuerst einmal – wir bringen die Bibliothek in den Klassenpfad.

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- check the latest version -->
    </dependency>
</dependencies>
```

Wenn Sie kein Maven verwenden, legen Sie einfach das `aspose-cells-24.9.jar` in Ihren `libs`‑Ordner und fügen es dem Build‑Pfad hinzu.

> **Pro‑Tipp:** Aspose liefert eine `License`‑Klasse. Registrieren Sie Ihre Lizenz frühzeitig, sonst sehen Sie Wasserzeichen in der Ausgabedatei.

```java
import com.aspose.cells.*;

public class ExcelExporter {
    static {
        try {
            License license = new License();
            license.setLicense("Aspose.Cells.lic"); // place your license file in resources
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
    }
    // …rest of the class
}
```

Jetzt können wir darüber sprechen, **wie man Stile anwendet**.

---

## Schritt 2: Benutzerdefinierte Stile für Excel erstellen

Die Magie einer professionellen Tabelle liegt in den Zell‑Stilen. Aspose ermöglicht das Definieren eines `Style`‑Objekts, das Anpassen von Schriftarten, Farben, Rahmen und das anschließende Wiederverwenden überall. Unten finden Sie eine kompakte Methode, um **benutzerdefinierte Excel‑Stile global hinzuzufügen**.

```java
/**
 * Builds an array of two custom styles:
 * 1. Header style – bold, gray background, centered.
 * 2. Data style   – thin borders, left‑aligned.
 */
private static Style[] buildImportStyles(Workbook workbook) {
    // Header style
    Style headerStyle = workbook.createStyle();
    Font headerFont = headerStyle.getFont();
    headerFont.setBold(true);
    headerFont.setColor(Color.getWhite());
    headerStyle.setPattern(BackgroundType.SOLID);
    headerStyle.setBackgroundColor(Color.getGray25());
    headerStyle.setHorizontalAlignment(TextAlignmentType.CENTER);
    headerStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    // Data style
    Style dataStyle = workbook.createStyle();
    dataStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setHorizontalAlignment(TextAlignmentType.LEFT);
    dataStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    return new Style[] { headerStyle, dataStyle };
}
```

Beachten Sie, dass wir **zwei unterschiedliche Stile** erstellt haben – einen für Spaltenüberschriften und einen für die Datenzeilen. Sie können dieses Array mit beliebig vielen Stilen erweitern; Aspose wendet sie in der Reihenfolge an, wenn Sie `importDataTable` aufrufen.

---

## Schritt 3: DataTable in das Arbeitsblatt importieren

Jetzt kommt der Teil, der tatsächlich **DataTable nach Excel importiert**. Die Methode `importDataTable` nimmt das Quell‑`DataTable`, ein Flag für Spaltenüberschriften, die Start‑Zeile/Spalte und das gerade erstellte Stil‑Array.

```java
public static void exportDataTableToExcel(DataTable dataTable, String outputPath) throws Exception {
    // 1️⃣ Create a new workbook and grab the first worksheet
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.getWorksheets().get(0);

    // 2️⃣ Build the custom styles (header + data)
    Style[] importStyles = buildImportStyles(workbook);

    // 3️⃣ Import the DataTable – start at A1 (0,0), keep column names, apply styles
    worksheet.getCells().importDataTable(dataTable, true, 0, 0, importStyles);

    // 4️⃣ Auto‑fit columns for a tidy look
    worksheet.autoFitColumns();

    // 5️⃣ Finally, **save workbook to file**
    workbook.save(outputPath);
}
```

Ein kurzer Hinweis: Das Argument `true` weist Aspose an, **Spaltenüberschriften zu erhalten** – das ist der typische Fall, wenn Sie einen lesbaren Bericht wollen. Wenn Sie es auf `false` setzen, wird die erste Datenzeile zur Überschrift.

---

## Schritt 4: Alles zusammenführen – ein minimal funktionierendes Beispiel

Unten finden Sie eine eigenständige `main`‑Methode, die ein Dummy‑`DataTable` erstellt, die Export‑Routine aufruft und `output.xlsx` in den Ordner `./results` schreibt.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExporter {

    // (License block omitted for brevity – see Step 1)

    public static void main(String[] args) throws Exception {
        // Mock a DataTable – replace this with your real DB call
        DataTable dataTable = createSampleDataTable();

        // Define where the Excel file should land
        String outputPath = "results/output.xlsx";

        // Perform the conversion and styling
        exportDataTableToExcel(dataTable, outputPath);

        System.out.println("Excel file generated at: " + outputPath);
    }

    /** Helper that builds a simple DataTable with three columns */
    private static DataTable createSampleDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", CellValueType.INTEGER);
        dt.getColumns().add("Name", CellValueType.STRING);
        dt.getColumns().add("Score", CellValueType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[] {1, "Alice", 85.5});
        dt.getRows().add(new Object[] {2, "Bob", 92.0});
        dt.getRows().add(new Object[] {3, "Charlie", 78.3});
        return dt;
    }

    // (Style builder and export method from Steps 2‑3 go here)
}
```

**Erwartete Ausgabe:** Öffnen Sie `output.xlsx` und Sie sehen eine fette, graue Kopfzeile, dünn gerahmte Datenzellen und automatisch an den Inhalt angepasste Spaltenbreiten. Das ist genau **wie man Stile anwendet**, um das Blatt professionell aussehen zu lassen.

![Wie man Stile in einer Excel-Arbeitsmappe anwendet](/images/excel-styles.png){alt="Wie man Stile in einer Excel-Arbeitsmappe anwendet"}

*(Der Screenshot zeigt die Kopfzeile in fett‑grau und die Datenzeilen mit dünnen Rahmen.)*

---

## Schritt 5: Fortgeschrittene Tipps & Sonderfälle

### 5.1 Bedingte Formatierung statt fester Stile  
Wenn Sie Zeilen hervorheben müssen, bei denen `Score > 90` gilt, können Sie nach dem Import eine `ConditionalFormattingCollection` hinzufügen. Das ermöglicht dynamische Farbgebung ohne das harte Kodieren zusätzlicher Stile.

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Zellen für Titel zusammenführen  
Manchmal benötigt ein Bericht einen großen Titel, der sich über mehrere Spalten erstreckt. Verwenden Sie `worksheet.getCells().merge(0, 0, 1, 3)` und wenden dann einen eigenen Stil auf diesen zusammengeführten Bereich an.

### 5.3 Große Datensätze – Leistungsüberlegungen  
Bei mehr als 100 k Zeilen setzen Sie zuerst `ImportDataTableOptions` auf `ImportDataTableOptions.NO_FORMATTING` und wenden die Stile dann in einem zweiten Durchlauf an. Das vermeidet den Aufwand, jede Zelle beim Import zu formatieren.

### 5.4 Multi‑Sheet‑Export  
Wenn Sie mehrere `DataTable`s haben, erstellen Sie einfach zusätzliche Arbeitsblätter über `workbook.getWorksheets().add("Sheet2")` und wiederholen den **DataTable nach Excel importieren**‑Schritt für jedes Blatt.

---

## Fazit

Wir haben **wie man Stile anwendet** von Anfang bis Ende behandelt: Einrichtung von Aspose.Cells, Erstellung **benutzerdefinierter Excel‑Stile**, **Import von DataTable nach Excel** und schließlich **Speichern der Arbeitsmappe in eine Datei**. Das vollständige Code‑Beispiel ist bereit zum Kopieren‑Einfügen, und die zusätzlichen Tipps bieten Ihnen eine Roadmap für anspruchsvollere Berichte.

Als Nächstes könnten Sie **benutzerdefinierte Excel‑Stile für Diagramme hinzufügen** oder mit **DataTable nach Excel konvertieren** in einem Spring‑Boot‑REST‑Endpoint experimentieren. So oder so haben Sie jetzt eine solide Grundlage, um rohe Tabellen in professionelle Tabellenkalkulationen zu verwandeln – ohne manuelle Formatierung.

Fragen?

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Stile auf Excel‑Zellen mit Aspose.Cells für Java anwendet – Vollständige Anleitung](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Zellen zusammenführen & Stile in Excel mit Aspose.Cells für Java anwenden – Eine vollständige Anleitung](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Wie man DataTable in Excel mit Aspose.Cells für .NET importiert (Schritt‑für‑Schritt‑Anleitung)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}