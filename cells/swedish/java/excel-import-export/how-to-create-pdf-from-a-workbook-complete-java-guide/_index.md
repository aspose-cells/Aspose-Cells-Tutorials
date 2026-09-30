---
category: general
date: 2026-03-01
description: Hur man skapar PDF och sparar arbetsbok som PDF, exporterar Excel till
  HTML och använder expand‑funktionen med Aspose.Cells för Java. Steg‑för‑steg‑kod
  inkluderad.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: sv
og_description: Hur man skapar PDF från en arbetsbok med Aspose.Cells för Java. Lär
  dig att spara arbetsboken som PDF, exportera Excel till HTML och använda EXPAND‑funktionen.
og_title: Hur man skapar PDF från en arbetsbok – Java‑handledning
tags:
- Aspose.Cells
- Java
- PDF generation
title: Hur man skapar PDF från en arbetsbok – Komplett Java‑guide
url: /sv/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar PDF från en arbetsbok – Komplett Java‑guide

Har du någonsin undrat **how to create PDF** direkt från en Excel‑arbetsbok utan att jonglera med tredjeparts‑konverterare? Du är inte ensam. Många utvecklare stöter på problem när de behöver en snabb PDF‑export, en HTML‑förhandsgranskning eller avancerade array‑formler — allt i ett svep.  

I den här handledningen går vi igenom ett enda, självständigt Java‑program som gör exakt det. Vi kommer att **save workbook as PDF**, visa dig hur du **export Excel to HTML** samtidigt som du behåller frysta rader, och demonstrera **use expand function** i ett kalkylblad. I slutet har du ett körbart projekt som du kan lägga in i vilken Maven‑ eller Gradle‑byggnad som helst.

> **Pro tip:** All kod nedan fungerar med Aspose.Cells 23.10 (eller nyare). Om du använder en äldre version kan vissa metodnamn skilja sig något.

---

## Förutsättningar

- **Java 17** (eller någon LTS‑version) installerad och konfigurerad.
- **Aspose.Cells for Java**‑biblioteket. Lägg till följande Maven‑beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- En IDE eller textredigerare efter eget val (IntelliJ IDEA, VS Code, Eclipse…).

Inga externa API:er, inga webbtjänster — bara ren Java och Aspose.Cells‑SDK.

---

## Översikt av lösningen

Vi delar upp implementeringen i **seven logical steps**:

1. Skapa en arbetsbok och demonstrera **EXPAND**‑funktionen.  
2. Aktivera teckensnittets variationsväljare och **save the workbook as PDF**.  
3. Exportera samma arbetsbok till HTML samtidigt som frysta rader bevaras.  
4. Använd en Smart Marker med en `IF`‑parameter för att infoga villkorlig text.  
5. Tillämpa en master‑detail Smart Marker för hierarkiska data.  
6. Ladda en Markdown‑fil som innehåller Base‑64‑kodade bilder.  
7. Konfigurera GridJs‑alternativ för justering och ramar, och sedan infoga data.

Varje steg är inbäddat i sin egen metod för att hålla `main`‑metoden prydlig och för att illustrera **why** vi gör vad vi gör, inte bara **what** vi skriver.

---

## Steg 1 – Skapa en arbetsbok och använd EXPAND‑funktionen

**EXPAND**‑funktionen är en ny dynamisk‑array‑formel som introducerades i Office 365. Den låter dig sprida ett område till ett större område utan att manuellt kopiera celler.

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

**Varför detta är viktigt:**  
- `EXPAND` fyller automatiskt resultatet med tomma celler, vilket är perfekt när du senare **save workbook as PDF** — PDF‑filen visar en ren, rektangulär tabell.  
- Att anropa `calculateFormula()` säkerställer att formelmotorn körs innan vi exporterar något.

---

## Steg 2 – Aktivera teckensnittets variationsväljare och **Save Workbook as PDF**

Om du behöver stödja avancerad typografi (t.ex. emoji eller CJK‑variationsväljare) måste du slå på funktionen **before** sparandet.

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

**Viktigt:** Det primära nyckelordet **how to create pdf** besvaras här — genom att anropa `workbook.save(..., SaveFormat.PDF)` efter att inställningarna konfigurerats.

---

## Steg 3 – **Export Excel to HTML** samtidigt som frysta rader bevaras

Ofta begär intressenter en snabb webb‑förhandsgranskning. Aspose.Cells kan exportera till HTML, och med `setPreserveFrozenRows(true)` behåller vi samma rullningsupplevelse som i Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Varför du bryr dig:** Frysta rader är en användbarhetssnutt; utan dem försvinner rubrikraderna när användare scrollar ner på sidan.

---

## Steg 4 – Smart Marker med en IF‑parameter

Smart Markers låter dig slå samman data i en mall utan att skriva loopar. `if`‑parametern lägger till villkorlig logik direkt i markören.

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

Den genererade PDF‑filen kommer att visa **“VIP Customer: Acme Corp”** eftersom `IsVIP` är `true`. Ändra flaggan till `false` så får du **“Regular Customer: Acme Corp”** — ingen extra kod behövs.

---

## Steg 5 – Master‑Detail Smart Marker med ett hierarkiskt område

När du har förälder‑barn‑data (t.ex. beställningar och radposter) sparar en master‑detail‑markör dig från manuell radinfogning.

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

**Vad du får:** Motorn expanderar master‑raderna för varje beställning och nästar automatiskt detaljraderna under — perfekt för fakturor eller inköpsrapporter.

---

## Steg 6 – Ladda ett Markdown‑dokument med inbäddade Base‑64‑bilder

Om dina källdata finns i Markdown (vanligt i dokumentations‑pipelines) kan Aspose.Cells rendera det direkt till en arbetsbok.

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

**Edge case‑anteckning:** Om Base‑64‑strängen är felaktig kommer Aspose att hoppa över bilden men fortsätta bearbeta resten av dokumentet — ingen krasch.

---

## Steg 7 – Konfigurera GridJs‑alternativ och infoga data

GridJs är ett lättviktigt JavaScript‑rutnät som Aspose kan rendera till HTML. Justering av siffror och applicering av ramar förbättrar läsbarheten.

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

**Varför vi bryr oss:** Korrekt justering och ramar får den genererade HTML‑koden att se ut som ett polerat kalkylblad — användbart för instrumentpaneler.

---

## Sätt ihop allt — `main`‑metoden

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