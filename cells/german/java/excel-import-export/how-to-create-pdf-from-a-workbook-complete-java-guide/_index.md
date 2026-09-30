---
category: general
date: 2026-03-01
description: Wie man PDF erstellt und die Arbeitsmappe als PDF speichert, Excel nach
  HTML exportiert und die Expand‑Funktion mit Aspose.Cells für Java verwendet. Schritt‑für‑Schritt‑Code
  enthalten.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: de
og_description: Wie man mit Aspose.Cells für Java ein PDF aus einer Arbeitsmappe erstellt.
  Erfahren Sie, wie Sie die Arbeitsmappe als PDF speichern, Excel nach HTML exportieren
  und die EXPAND‑Funktion verwenden.
og_title: Wie man ein PDF aus einer Arbeitsmappe erstellt – Java‑Tutorial
tags:
- Aspose.Cells
- Java
- PDF generation
title: Wie man ein PDF aus einer Arbeitsmappe erstellt – Vollständiger Java-Leitfaden
url: /de/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF aus einer Arbeitsmappe erstellt – Vollständiger Java‑Leitfaden

Haben Sie sich jemals gefragt, **wie man PDF** direkt aus einer Excel‑Arbeitsmappe erstellt, ohne Drittanbieter‑Konverter zu jonglieren? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie einen schnellen PDF‑Export, eine HTML‑Vorschau oder ausgefallene Array‑Formeln benötigen – alles in einem Schritt.  

In diesem Tutorial führen wir Sie durch ein einzelnes, eigenständiges Java‑Programm, das genau das leistet. Wir **speichern die Arbeitsmappe als PDF**, zeigen Ihnen, wie Sie **Excel nach HTML exportieren** und dabei gefrorene Zeilen beibehalten, und demonstrieren die **Verwendung der EXPAND‑Funktion** innerhalb eines Arbeitsblatts. Am Ende haben Sie ein lauffähiges Projekt, das Sie in jede Maven‑ oder Gradle‑Umgebung einbinden können.

> **Pro Tipp:** Der gesamte nachfolgende Code funktioniert mit Aspose.Cells 23.10 (oder neuer). Wenn Sie eine ältere Version verwenden, können einige Methodennamen leicht abweichen.

---

## Voraussetzungen

- **Java 17** (oder jede andere LTS‑Version) installiert und konfiguriert.
- **Aspose.Cells for Java**‑Bibliothek. Fügen Sie die folgende Maven‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Eine IDE oder ein Text‑Editor Ihrer Wahl (IntelliJ IDEA, VS Code, Eclipse …).

Keine externen APIs, keine Web‑Services – nur reines Java und das Aspose.Cells‑SDK.

---

## Übersicht der Lösung

Wir teilen die Implementierung in **sieben logische Schritte** auf:

1. Erstellen einer Arbeitsmappe und Demonstration der **EXPAND**‑Funktion.  
2. Aktivieren von Schrift‑Variations‑Selektoren und **Arbeitsmappe als PDF speichern**.  
3. dieselbe Arbeitsmappe nach HTML exportieren und gefrorene Zeilen beibehalten.  
4. Einen Smart Marker mit einem `IF`‑Parameter verwenden, um bedingten Text einzufügen.  
5. Einen Master‑Detail‑Smart Marker für hierarchische Daten anwenden.  
6. Eine Markdown‑Datei laden, die Base‑64‑kodierte Bilder enthält.  
7. GridJs‑Optionen für Ausrichtung und Rahmen konfigurieren und dann Daten einfügen.

Jeder Schritt ist in einer eigenen Methode gekapselt, um die `main`‑Methode übersichtlich zu halten und zu verdeutlichen, **warum** wir etwas tun, nicht nur **was** wir tippen.

---

## Schritt 1 – Erstellen einer Arbeitsmappe und Verwenden der EXPAND‑Funktion

Die **EXPAND**‑Funktion ist eine neue dynamische Array‑Formel, die in Office 365 eingeführt wurde. Sie ermöglicht es, einen Bereich in einen größeren Bereich zu „spill‑en“, ohne Zellen manuell zu kopieren.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Warum das wichtig ist:**  
- `EXPAND` füllt das Ergebnis automatisch mit Leerwerten auf, was ideal ist, wenn Sie später **die Arbeitsmappe als PDF speichern** – das PDF zeigt dann eine saubere, rechteckige Tabelle.  
- Der Aufruf von `calculateFormula()` stellt sicher, dass die Formelengine ausgeführt wird, bevor wir irgendetwas exportieren.

---

## Schritt 2 – Schrift‑Variations‑Selektoren aktivieren und **Arbeitsmappe als PDF speichern**

Wenn Sie erweiterte Typografie unterstützen müssen (z. B. Emoji‑ oder CJK‑Variations‑Selektoren), müssen Sie die Funktion **vor** dem Speichern aktivieren.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Wichtiger Hinweis:** Das zentrale Stichwort **how to create pdf** wird hier beantwortet – durch den Aufruf von `workbook.save(..., SaveFormat.PDF)` nach der Konfiguration der Einstellungen.

---

## Schritt 3 – **Excel nach HTML exportieren** und gefrorene Zeilen beibehalten

Oft verlangen Stakeholder eine schnelle Web‑Vorschau. Aspose.Cells kann nach HTML exportieren, und mit `setPreserveFrozenRows(true)` behalten wir das gleiche Scroll‑Verhalten wie in Excel bei.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Warum das für Sie relevant ist:** Gefrorene Zeilen sind ein Komfortmerkmal; ohne sie verschwinden die Kopfzeilen, wenn Benutzer die Seite nach unten scrollen.

---

## Schritt 4 – Smart Marker mit einem IF‑Parameter

Smart Marker ermöglichen das Einfügen von Daten in eine Vorlage, ohne Schleifen zu schreiben. Der `if`‑Parameter fügt bedingte Logik direkt im Marker hinzu.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

Das erzeugte PDF enthält **„VIP Customer: Acme Corp“**, weil `IsVIP` den Wert `true` hat. Ändern Sie die Flagge zu `false` und Sie erhalten **„Regular Customer: Acme Corp“** – ohne zusätzlichen Code.

---

## Schritt 5 – Master‑Detail‑Smart‑Marker mit einem hierarchischen Bereich

Wenn Sie Eltern‑Kind‑Daten haben (z. B. Aufträge und Positionen), spart ein Master‑Detail‑Marker das manuelle Einfügen von Zeilen.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Was Sie gewinnen:** Die Engine erweitert die Master‑Zeilen für jeden Auftrag und verschachtelt automatisch die Detail‑Zeilen darunter – ideal für Rechnungen oder Einkaufsberichte.

---

## Schritt 6 – Laden eines Markdown‑Dokuments mit eingebetteten Base‑64‑Bildern

Falls Ihre Quelldaten in Markdown vorliegen (häufig in Dokumentations‑Pipelines), kann Aspose.Cells sie direkt in eine Arbeitsmappe rendern.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Hinweis zum Randfall:** Wenn die Base‑64‑Zeichenkette fehlerhaft ist, überspringt Aspose das Bild, verarbeitet aber den Rest des Dokuments weiter – es kommt zu keinem Absturz.

---

## Schritt 7 – GridJs‑Optionen konfigurieren und Daten einfügen

GridJs ist ein leichtgewichtiges JavaScript‑Raster, das Aspose in HTML rendern kann. Zahlen auszurichten und Rahmen anzuwenden verbessert die Lesbarkeit.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Warum das wichtig ist:** Richtige Ausrichtung und Rahmen lassen das erzeugte HTML wie eine professionell aussehende Tabelle wirken – nützlich für Dashboards.

---

## Alles zusammenführen – Die `main`‑Methode

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}