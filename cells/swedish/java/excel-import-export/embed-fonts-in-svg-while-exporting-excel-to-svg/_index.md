---
category: general
date: 2026-08-14
description: Bädda in teckensnitt i SVG när du exporterar Excel till SVG med Aspose.Cells.
  Lär dig hur du anger utskriftsområde, ställer in utskriftsalternativ och använder
  WRAPCOLS‑funktionen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: sv
lastmod: 2026-08-14
og_description: Bädda in typsnitt i SVG när du exporterar Excel till SVG med Aspose.Cells.
  Denna guide visar hur du ställer in utskriftsområde, konfigurerar utskriftsalternativ
  och använder WRAPCOLS‑funktionen.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Bädda in teckensnitt i SVG vid export av Excel till SVG – steg för steg
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
title: Bädda in teckensnitt i SVG vid export av Excel till SVG
url: /sv/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bädda in typsnitt i SVG vid export av Excel till SVG

Om du behöver **embed fonts in SVG while exporting Excel to SVG**, visar den här handledningen exakt hur du gör det med Aspose.Cells for Java. Vi kommer också att gå igenom hur du **set print area**, **set print options**, och **use WRAPCOLS function** för att formatera data utan att förlora layout.

Du kommer att gå igenom ett komplett, körbart exempel som laddar en befintlig arbetsbok, tillämpar `WRAPCOLS`‑formeln, konfigurerar SVG‑specifika bildalternativ, definierar utskriftsområdet och slutligen sparar filen som en SVG med inbäddade typsnitt. Ingen extern dokumentation krävs—kopiera bara koden, kör den och inspektera den resulterande SVG‑filen.

## Bädda in typsnitt i SVG – konfigurering av ImageOrPrintOptions

Att bädda in typsnitt säkerställer att SVG‑filen renderas exakt som den ser ut i Excel, även på maskiner som inte har de ursprungliga teckensnitten installerade.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Varför detta är viktigt*: När `setEmbedFonts(true)` är aktiverat skriver Aspose.Cells typsnittsdata direkt in i `<defs>`‑sektionen i SVG‑filen. Resultatet blir en självständig fil som ser identisk ut i alla webbläsare och på alla plattformar.

## Exportera Excel till SVG – fullständigt arbetsflöde

Följande steg illustrerar hela processen, från att ladda arbetsboken till att spara SVG‑filen.

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

**Förväntad output**: `output.svg` visas i `YOUR_DIRECTORY`. När du öppnar den i en webbläsare visas kalkylbladet med alla typsnitt inbäddade, data omslagna i tre kolumner (tack vare `WRAPCOLS`), och endast cellerna inom `A1:H30` renderas.

## Ställ in utskriftsområde för kalkylbladet

Att definiera ett utskriftsområde begränsar den exporterade SVG‑filen till ett specifikt område, vilket minskar filstorleken och fokuserar betraktaren på den relevanta datan.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tips*: Intervallet följer Excels A1‑notation. Om du behöver ett dynamiskt område kan du beräkna det programatiskt med `ws.getCells().getMaxDisplayRange()`.

## Ställ in utskriftsalternativ för SVG‑output

Utskriftsalternativ styr hur Aspose.Cells översätter kalkylbladet till en bild. Förutom att bädda in typsnitt kan du justera upplösning, skalning och sidlayout.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Varför du bör ställa in utskriftsalternativ*: Utan explicita alternativ använder Aspose.Cells standardinställningar som kan utelämna inbäddning av typsnitt eller tillämpa en oönskad skalningsfaktor, vilket leder till suddiga eller felaktigt stylade SVG‑filer.

## Använd WRAPCOLS‑funktionen för att omsluta kolumndata

`WRAPCOLS` är en Excel‑formel som fördelar ett vertikalt område i ett angivet antal kolumner. Den är praktisk när du vill visa en lång lista i ett kompakt rutnät.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

När arbetsboken sparas utvärderar Aspose.Cells formeln och skapar en tre‑kolumns layout inom det definierade utskriftsområdet. Denna teknik fungerar för alla storlekar på områden—justera bara det andra argumentet till önskat antal kolumner.

## Fullständigt körbart exempel

Nedan är hela Java‑programmet som du kan klistra in i vilken IDE som helst. Se till att du har Aspose.Cells for Java‑biblioteket på din classpath.

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

**Verifieringssteg**

1. Kör programmet.  
2. Öppna `output.svg` i en webbläsare.  
3. Bekräfta att texten använder samma teckensnitt som den ursprungliga Excel‑filen (typsnitt är inbäddade).  
4. Verifiera att endast cellerna inom `A1:H30` visas och att data från `A2:A10` visas i tre kolumner.

## Vanliga fallgropar och hur du undviker dem

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Typsnitt saknas i SVG | `setEmbedFonts(false)` eller så är typsnittsfilen inte åtkomlig | Se till att `setEmbedFonts(true)` och att typsnittet är installerat på maskinen som kör koden |
| WRAPCOLS utvärderas inte | Beräkningsmotorn är inaktiverad | Anropa `workbook.calculateFormula()` innan export, eller låt Aspose.Cells utvärdera under sparning |
| Exporterad SVG är tom | Utskriftsområdet inkluderar ingen data | Dubbelkolla intervallet som skickas till `setPrintArea` |
| SVG‑filen är enorm | Ingen skalning tillämpad, hög bildupplösning | Justera `imgOptions.setResolution(96)` eller liknande för att kontrollera DPI |

## Proffstips: återanvänd ImageOrPrintOptions för flera kalkylblad

Om din arbetsbok innehåller flera blad som behöver identiska SVG‑inställningar, skapa en enda `ImageOrPrintOptions`‑instans och tilldela den till varje kalkylblads `PageSetup`. Detta minskar minnesanvändningen och garanterar konsekvent inbäddning av typsnitt i alla exporterade filer.

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

## Nästa steg

* **Exportera till andra vektorformat** – Ändra `ImageFormat.SVG` till `ImageFormat.PDF` för högkvalitativa PDF‑filer.  
* **Batch‑bearbetning** – Loopa igenom en mapp med `.xlsx`‑filer och generera SVG‑filer automatiskt.  
* **Anpassad typsnittshantering** – Använd `FontSettings` för att ladda typsnitt från en specifik katalog när systemtypsnitten är otillräckliga.  

Genom att behärska **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options**, och **use WRAPCOLS function** kan du automatisera högkvalitativ SVG‑generering för rapporter, instrumentpaneler och webbvisualiseringar direkt från Excel‑data. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man ställer in ett utskriftsområde i Excel med Aspose.Cells för .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Ställ in utskriftsområde Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Ställ in utskriftsområde Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}