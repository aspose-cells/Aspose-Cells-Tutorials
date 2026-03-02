---
category: general
date: 2026-03-01
description: Hoe een PDF te maken en een werkmap als PDF op te slaan, Excel naar HTML
  te exporteren en de expand-functie te gebruiken met Aspose.Cells voor Java. Stapsgewijze
  code inbegrepen.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: nl
og_description: Hoe maak je een PDF van een werkmap met Aspose.Cells voor Java. Leer
  hoe je een werkmap opslaat als PDF, Excel exporteert naar HTML en de EXPAND-functie
  gebruikt.
og_title: Hoe maak je een PDF van een werkmap – Java‑tutorial
tags:
- Aspose.Cells
- Java
- PDF generation
title: Hoe een PDF te maken vanuit een werkmap – Complete Java‑gids
url: /nl/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF te maken vanuit een Werkmap – Complete Java-gids

Heb je je ooit afgevraagd **hoe PDF** direct vanuit een Excel-werkmap kunt maken zonder met externe converters te jongleren? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een snelle PDF-export, een HTML-preview of geavanceerde array‑formules nodig hebben — allemaal in één keer.  

In deze tutorial lopen we een enkel, zelfstandig Java‑programma door dat precies dat doet. We zullen **werkmap opslaan als PDF**, je laten zien hoe je **Excel naar HTML exporteert** terwijl bevroren rijen behouden blijven, en de **gebruik van de expand‑functie** binnen een werkblad demonstreren. Aan het einde heb je een uitvoerbaar project dat je in elke Maven‑ of Gradle‑build kunt plaatsen.

> **Pro tip:** Alle onderstaande code werkt met Aspose.Cells 23.10 (of nieuwer). Als je een oudere versie gebruikt, kunnen sommige methodenamen iets anders zijn.

---

## Vereisten

- **Java 17** (of een andere LTS‑versie) geïnstalleerd en geconfigureerd.
- **Aspose.Cells for Java**‑bibliotheek. Voeg de volgende Maven‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Een IDE of teksteditor naar keuze (IntelliJ IDEA, VS Code, Eclipse…).

Geen externe API's, geen webservices — alleen pure Java en de Aspose.Cells SDK.

---

## Overzicht van de Oplossing

We splitsen de implementatie in **zeven logische stappen**:

1. Maak een werkmap en demonstreer de **EXPAND**‑functie.  
2. Schakel lettertype‑variatieselectors in en **sla de werkmap op als PDF**.  
3. Exporteer dezelfde werkmap naar HTML terwijl bevroren rijen behouden blijven.  
4. Gebruik een Smart Marker met een `IF`‑parameter om voorwaardelijke tekst in te voegen.  
5. Pas een master‑detail Smart Marker toe voor hiërarchische gegevens.  
6. Laad een Markdown‑bestand dat Base‑64‑gecodeerde afbeeldingen bevat.  
7. Configureer GridJs‑opties voor uitlijning en randen, en voeg vervolgens gegevens in.

Elke stap is ingekapseld in een eigen methode om de `main`‑methode overzichtelijk te houden en om te illustreren **waarom** we doen wat we doen, niet alleen **wat** we typen.

---

## Stap 1 – Maak een Werkmap en Gebruik de EXPAND‑functie

De **EXPAND**‑functie is een nieuwe dynamische‑array‑formule geïntroduceerd in Office 365. Hiermee kun je een bereik uitbreiden naar een groter gebied zonder handmatig cellen te kopiëren.

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

**Waarom dit belangrijk is:**  
- `EXPAND` vult het resultaat automatisch aan met lege cellen, wat perfect is wanneer je later **werkmap opslaat als PDF** — de PDF toont een nette, rechthoekige tabel.  
- Het aanroepen van `calculateFormula()` zorgt ervoor dat de formule‑engine wordt uitgevoerd voordat we iets exporteren.

---

## Stap 2 – Schakel Lettertype‑Variatieselectors in en **Sla Werkmap op als PDF**

Als je geavanceerde typografie wilt ondersteunen (bijv. emoji of CJK‑variatieselectors), moet je de functie **vóór** het opslaan inschakelen.

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

**Belangrijk punt:** Het primaire zoekwoord **hoe PDF te maken** wordt hier beantwoord — door `workbook.save(..., SaveFormat.PDF)` aan te roepen na het configureren van de instellingen.

---

## Stap 3 – **Excel naar HTML exporteren** terwijl bevroren rijen behouden blijven

Vaak vragen belanghebbenden om een snelle webpreview. Aspose.Cells kan exporteren naar HTML, en met `setPreserveFrozenRows(true)` behouden we dezelfde scrollervaring als in Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Waarom het belangrijk is:** Bevroren rijen zijn een gebruiksvriendelijkheid‑voordeel; zonder hen verdwijnen de koprijen wanneer gebruikers naar beneden scrollen op de pagina.

---

## Stap 4 – Smart Marker met een IF‑parameter

Smart Markers laten je gegevens in een sjabloon samenvoegen zonder loops te schrijven. De `if`‑parameter voegt voorwaardelijke logica direct binnen de marker toe.

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

De gegenereerde PDF zal **“VIP Customer: Acme Corp”** weergeven omdat `IsVIP` `true` is. Verander de vlag naar `false` en je krijgt **“Regular Customer: Acme Corp”** — zonder extra code.

---

## Stap 5 – Master‑Detail Smart Marker met een Hiërarchisch Bereik

Wanneer je ouder‑kind‑gegevens hebt (bijv. bestellingen en regelitems), bespaart een master‑detail‑marker je handmatige rij‑invoeging.

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

**Wat je wint:** De engine breidt de master‑rijen uit voor elke bestelling en nestelt automatisch de detail‑rijen eronder — perfect voor facturen of aankooprapporten.

---

## Stap 6 – Laad een Markdown‑document met ingebedde Base‑64‑afbeeldingen

Als je brongegevens zich in Markdown bevinden (veelvoorkomend in documentatie‑pijplijnen), kan Aspose.Cells het rechtstreeks in een werkmap renderen.

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

**Opmerking voor randgeval:** Als de Base‑64‑string onjuist is, zal Aspose de afbeelding overslaan maar de rest van het document blijven verwerken — geen crash.

---

## Stap 7 – Configureer GridJs‑opties en Voeg Gegevens In

GridJs is een lichtgewicht JavaScript‑grid die Aspose kan renderen naar HTML. Het uitlijnen van getallen en het toepassen van randen verbetert de leesbaarheid.

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

**Waarom het belangrijk is:** Juiste uitlijning en randen laten de gegenereerde HTML eruitzien als een gepolijste spreadsheet — nuttig voor dashboards.

---

## Alles Samenvoegen – De `main`‑methode

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