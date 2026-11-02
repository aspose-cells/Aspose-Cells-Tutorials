---
category: general
date: 2026-08-14
description: Schriften in SVG einbetten beim Exportieren von Excel nach SVG mit Aspose.Cells.
  Erfahren Sie, wie Sie den Druckbereich festlegen, Druckoptionen einstellen und die
  WRAPCOLS‑Funktion verwenden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: de
lastmod: 2026-08-14
og_description: Schriften in SVG einbetten beim Exportieren von Excel nach SVG mit
  Aspose.Cells. Dieser Leitfaden zeigt Ihnen, wie Sie den Druckbereich festlegen,
  Druckoptionen konfigurieren und die WRAPCOLS‑Funktion anwenden.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Schriftarten in SVG einbetten beim Exportieren von Excel nach SVG – Schritt
  für Schritt
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Schriftarten in SVG einbetten beim Exportieren von Excel nach SVG
url: /de/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schriftarten in SVG einbetten beim Exportieren von Excel nach SVG

Wenn Sie **Schriftarten in SVG einbetten beim Exportieren von Excel nach SVG** müssen, zeigt Ihnen dieses Tutorial genau, wie Sie das mit Aspose.Cells für Java erledigen. Wir behandeln außerdem, wie Sie **den Druckbereich festlegen**, **Druckoptionen setzen** und die **WRAPCOLS‑Funktion** verwenden, um Daten zu formatieren, ohne das Layout zu verlieren.

Sie gehen Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das eine vorhandene Arbeitsmappe lädt, die `WRAPCOLS`‑Formel anwendet, SVG‑spezifische Bildoptionen konfiguriert, den Druckbereich definiert und schließlich die Datei als SVG mit eingebetteten Schriftarten speichert. Keine externe Dokumentation nötig – einfach den Code kopieren, ausführen und das resultierende SVG prüfen.

## Schriftarten in SVG einbetten – Konfiguration von ImageOrPrintOptions

Das Einbetten von Schriftarten stellt sicher, dass das SVG exakt so gerendert wird, wie es in Excel aussieht, selbst auf Rechnern, auf denen die Original‑Schriftarten nicht installiert sind.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Warum das wichtig ist*: Wenn `setEmbedFonts(true)` aktiviert ist, schreibt Aspose.Cells die Schriftartdaten direkt in den `<defs>`‑Abschnitt des SVG. Das Ergebnis ist eine eigenständige Datei, die in allen Browsern und auf allen Plattformen identisch aussieht.

## Excel nach SVG exportieren – kompletter Workflow

Die folgenden Schritte zeigen den End‑zu‑End‑Prozess, vom Laden der Arbeitsmappe bis zum Speichern der SVG‑Datei.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Erwartete Ausgabe**: `output.svg` erscheint in `YOUR_DIRECTORY`. Öffnet man die Datei im Browser, sieht man das Arbeitsblatt mit allen eingebetteten Schriftarten, die Daten, die dank `WRAPCOLS` in drei Spalten umgebrochen wurden, und nur die Zellen innerhalb von `A1:H30` werden gerendert.

## Druckbereich für das Arbeitsblatt festlegen

Durch die Definition eines Druckbereichs wird das exportierte SVG auf einen bestimmten Bereich beschränkt, was die Dateigröße reduziert und den Betrachter auf die relevanten Daten fokussiert.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tipp*: Der Bereich folgt der Excel‑A1‑Notation. Wenn Sie einen dynamischen Bereich benötigen, können Sie ihn programmgesteuert mit `ws.getCells().getMaxDisplayRange()` ermitteln.

## Druckoptionen für die SVG‑Ausgabe setzen

Druckoptionen steuern, wie Aspose.Cells das Arbeitsblatt in ein Bild übersetzt. Zusätzlich zum Einbetten von Schriftarten können Sie Auflösung, Skalierung und Seitenlayout anpassen.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Warum Sie Druckoptionen setzen sollten*: Ohne explizite Optionen verwendet Aspose.Cells Standardwerte, die das Einbetten von Schriftarten weglassen oder einen unerwünschten Skalierungsfaktor anwenden können, was zu unscharfen oder falsch gestylten SVGs führt.

## WRAPCOLS‑Funktion zum Umbruch von Spaltendaten verwenden

`WRAPCOLS` ist eine Excel‑Formel, die einen vertikalen Bereich in eine festgelegte Anzahl von Spalten verteilt. Praktisch, wenn Sie eine lange Liste kompakt in einem Raster anzeigen möchten.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Beim Speichern der Arbeitsmappe wertet Aspose.Cells die Formel aus und erzeugt ein dreispaltiges Layout innerhalb des definierten Druckbereichs. Diese Technik funktioniert für jeden Bereich – passen Sie einfach das zweite Argument an die gewünschte Spaltenanzahl an.

## Vollständiges, ausführbares Beispiel

Nachfolgend das komplette Java‑Programm, das Sie in jede IDE einfügen können. Stellen Sie sicher, dass die Aspose.Cells‑Bibliothek für Java im Klassenpfad liegt.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Verifizierungsschritte**

1. Programm ausführen.  
2. `output.svg` in einem Webbrowser öffnen.  
3. Bestätigen, dass der Text dieselbe Schriftart wie die ursprüngliche Excel‑Datei verwendet (Schriftarten sind eingebettet).  
4. Prüfen, dass nur die Zellen innerhalb von `A1:H30` angezeigt werden und dass die Daten aus `A2:A10` in drei Spalten dargestellt werden.

## Häufige Stolperfallen und wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Schriftarten fehlen im SVG | `setEmbedFonts(false)` oder die Schriftdatei ist nicht zugänglich | `setEmbedFonts(true)` setzen und sicherstellen, dass die Schrift auf dem ausführenden Rechner installiert ist |
| WRAPCOLS wird nicht ausgewertet | Berechnungs‑Engine deaktiviert | `workbook.calculateFormula()` vor dem Export aufrufen oder Aspose.Cells die Auswertung beim Speichern überlassen |
| Exportiertes SVG ist leer | Druckbereich enthält keine Daten | Den an `setPrintArea` übergebenen Bereich überprüfen |
| SVG‑Datei ist riesig | Keine Skalierung angewendet, hohe Bildauflösung | `imgOptions.setResolution(96)` oder ähnliches anpassen, um DPI zu steuern |

## Pro‑Tipp: ImageOrPrintOptions für mehrere Arbeitsblätter wiederverwenden

Enthält Ihre Arbeitsmappe mehrere Tabellen, die identische SVG‑Einstellungen benötigen, erstellen Sie eine einzige `ImageOrPrintOptions`‑Instanz und weisen Sie sie jedem Arbeitsblatt‑`PageSetup` zu. Das reduziert den Speicherverbrauch und garantiert ein konsistentes Einbetten von Schriftarten in allen exportierten Dateien.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Nächste Schritte

* **Export in andere Vektorformate** – Ändern Sie `ImageFormat.SVG` zu `ImageFormat.PDF` für hochwertige PDFs.  
* **Batch‑Verarbeitung** – Durchlaufen Sie einen Ordner mit `.xlsx`‑Dateien und erzeugen Sie automatisch SVGs.  
* **Benutzerdefinierte Schriftartverwaltung** – Verwenden Sie `FontSettings`, um Schriftarten aus einem bestimmten Verzeichnis zu laden, wenn die Systemschriftarten nicht ausreichen.  

Durch das Beherrschen von **Schriftarten in SVG einbetten**, **Excel nach SVG exportieren**, **Druckbereich festlegen**, **Druckoptionen setzen** und **WRAPCOLS‑Funktion verwenden** können Sie die hochpräzise SVG‑Erstellung für Berichte, Dashboards und Web‑Visualisierungen direkt aus Excel‑Daten automatisieren. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man einen Druckbereich in Excel mit Aspose.Cells für .NET festlegt](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Druckbereich in Excel mit Aspose.Cells für .NET festlegen](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Définir une zone d’impression dans Excel avec Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}