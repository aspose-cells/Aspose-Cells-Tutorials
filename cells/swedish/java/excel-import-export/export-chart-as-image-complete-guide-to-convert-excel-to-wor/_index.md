---
category: general
date: 2026-06-30
description: Exportera diagram som bild och lär dig hur du exporterar diagram, sparar
  Excel som Word, konverterar Excel till Word och konverterar XLSX till DOCX i några
  enkla steg.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: sv
og_description: Exportera diagram som bild och konvertera snabbt Excel till Word.
  Följ den här guiden för att spara Excel som Word, exportera diagram och konvertera
  XLSX till DOCX.
og_title: Exportera diagram som bild – Steg‑för‑steg konvertering från Excel till
  Word
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Exportera diagram som bild – Komplett guide för att konvertera Excel till Word
url: /sv/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera diagram som bild – Komplett guide för att konvertera Excel till Word

Har du någonsin undrat hur man exporterar diagram som bild från en Excel-arbetsbok och placerar den direkt i ett Word-dokument? Du är inte ensam—utvecklare frågar ständigt, “Hur exporterar jag diagram från XLSX och bäddar in det i DOCX utan att förlora kvalitet?”

Den goda nyheten är att med några rader Java‑kod kan du **exportera diagram som bild**, sedan **spara Excel som Word** i ett sömlöst flöde. I den här handledningen går vi igenom hela processen, från att ladda arbetsboken till att konfigurera sparalternativen som omvandlar dina diagram till skarpa PNG‑bilder i en DOCX‑fil.

Vi kommer också att beröra relaterade uppgifter som **convert Excel to Word**, **save Excel as Word**, och **convert XLSX to DOCX**—allt medan koden hålls tydlig och körbar. Inga onödiga detaljer, bara en praktisk lösning du kan kopiera‑klistra in idag.

---

## Vad du behöver

- **Java Development Kit (JDK) 8+** – koden körs på vilken modern JDK som helst.
- **Aspose.Cells for Java**-biblioteket (version 23.10 eller nyare). Du kan hämta det från Maven Central eller ladda ner JAR‑filen direkt.
- En **Excel‑fil** (`charts.xlsx`) som innehåller minst ett diagram du vill exportera.
- En **Java‑IDE** (IntelliJ IDEA, Eclipse eller VS Code) – vilken som helst fungerar.
- Grundläggande kunskap om Java och Maven/Gradle (valfritt men hjälpsamt).

Det är allt. Inga extra plugins, ingen COM‑interop, bara ren Java.

## Steg 1: Ladda Excel‑arbetsboken och hitta diagrammet

Det första vi måste göra är att öppna arbetsboken som innehåller diagrammet. Aspose.Cells gör detta enkelt—ange bara filvägen.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Varför detta är viktigt:** Att ladda arbetsboken ger oss åtkomst till diagramobjektet, som vi senare kommer att be Aspose rendera som en bild. Om arbetsboken innehåller flera blad eller diagram kan du justera indexen eller loopa igenom dem.

## Steg 2: Konfigurera DOCX‑sparalternativ för att exportera diagram som bilder

Aspose.Cells tillhandahåller en `DocxSaveOptions`‑klass som låter dig styra hur konverteringen beter sig. Att sätta `setExportChartAsImage(true)` instruerar biblioteket att rasterisera varje diagram till en bild innan det bäddas in i Word‑filen.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Proffstips:** Om du föredrar vektorgrafik (EMF/WMF) kan du låta detta flagga vara avstängt, men rasterbilder renderas vanligtvis mer konsekvent över olika Word‑versioner.

## Steg 3: Spara arbetsboken som en DOCX‑fil

Nu när alternativen är satta sparar vi helt enkelt arbetsboken. Biblioteket tar hand om att konvertera alla kalkylblad, tabeller och—tack vare flaggan vi satte—diagram som bilder.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Vad du får:** En `charts.docx`‑fil där det ursprungliga Excel‑diagrammet visas som en högupplöst PNG (eller JPEG, beroende på dina inställningar) i Word‑dokumentet. Öppna den i Microsoft Word för att se resultatet.

## Steg 4: Verifiera resultatet (valfritt men rekommenderat)

Det är alltid en bra idé att programatiskt verifiera att konverteringen lyckades, särskilt när du automatiserar batch‑processer.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Om du kör kodsnutten och ser framgångsmeddelandet har du effektivt **convert XLSX to DOCX** samtidigt som du bevarar diagrammets visuella som bilder.

## Fullt fungerande exempel

Nedan är det kompletta, färdiga Java‑programmet som sätter ihop alla stegen. Byt bara ut `YOUR_DIRECTORY` mot den faktiska sökvägen på din maskin.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Förväntat utdata när du kör programmet:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Öppna `charts.docx` i Microsoft Word, så ser du diagrammet renderat som en ren bild, perfekt placerad där det ursprungliga Excel‑diagrammet skulle ha varit.

## Vanliga frågor & specialfall

### Vad händer om min arbetsbok har flera diagram?

Du behöver inte ändra något—att sätta `setExportChartAsImage(true)` gäller för **alla** diagram i arbetsboken. Om du bara vill ha specifika diagram som bilder måste du exportera dem manuellt med `chart.toImage()` och sedan själv infoga dem i Word‑filen.

### Kan jag styra bildformatet (PNG vs JPEG)?

Aspose.Cells använder PNG som standard för export av diagram‑som‑bild. För att byta till JPEG kan du justera `ImageOrPrintOptions` innan du sparar:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Fungerar detta med äldre Excel‑filer (.xls)?

Absolut. Samma kod fungerar för både `.xls` och `.xlsx`. Aspose.Cells upptäcker automatiskt formatet, så du kan **save Excel as Word** oavsett källversion.

### Hur skiljer sig detta från “convert Excel to Word” med inbyggd Office‑interop?

Inbyggd interop kräver ofta en Windows‑maskin med Office installerat, och diagram kan förlora kvalitet. Att använda Aspose.Cells är plattformsoberoende, fungerar på Linux/macOS, och bevarar diagramkvaliteten genom att rasterisera dem.

## Tips för produktionsklara implementationer

- **Batch‑behandling:** Loopa igenom en katalog med XLSX‑filer och tillämpa samma `DocxSaveOptions`. Omge konverteringen med ett try‑catch‑block för att hantera korrupta filer på ett smidigt sätt.
- **Minneshantering:** För mycket stora arbetsböcker, anropa `workbook.dispose()` efter sparning för att frigöra inhemska resurser.
- **Anpassning:** Du kan också sätta `saveOptions.setPreserveCellFormatting(true)` om du behöver behålla cellformaten intakt vid konvertering.
- **Loggning:** Integrera ett loggningsramverk (SLF4J, Log4j) för att fånga konverteringsstatistik—användbart för revisionsspår.

## Slutsats

Du har nu en solid, helhetslösning som **export chart as image**, **save Excel as Word**, och **convert XLSX to DOCX** med bara ett fåtal Java‑satser. Den viktigaste insikten är att Aspose.Cells `DocxSaveOptions` gör diagramhantering enkel—ingen manuell bildextraktion, ingen COM‑interop, och fullt stöd för flera plattformar.

Känn dig fri att experimentera: prova att exportera flera kalkylblad, justera bildupplösningar, eller kombinera detta tillvägagångssätt med andra Aspose‑bibliotek (som Aspose.Words) för ännu rikare Word‑dokument. Himlen är gränsen när du vet hur du exporterar diagram korrekt.

Har du fler frågor om att konvertera Excel‑filer, bädda in bilder eller optimera prestanda? Lämna en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Konvertera Excel‑diagram till bild med Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [Hur man skapar Excel‑diagram med trendlinje och exporterar till bild med Aspose.Cells för Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Konvertera Excel‑cirkeldiagram till bild med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}