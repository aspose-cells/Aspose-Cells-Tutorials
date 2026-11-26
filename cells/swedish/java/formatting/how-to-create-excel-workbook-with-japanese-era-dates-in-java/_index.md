---
category: general
date: 2026-11-25
description: Lär dig hur du skapar en Excel‑arbetsbok, formaterar cellen generellt,
  tillämpar stil på Excel‑cellen och sparar arbetsboken som XLSX med Java och Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- format cell general
- apply style excel cell
- save workbook xlsx
language: sv
lastmod: 2026-11-25
og_description: Skapa en Excel-arbetsbok i Java, formatera cellen som allmän, tillämpa
  stil på Excel-cellen och spara arbetsboken som XLSX samtidigt som du hanterar japanska
  era‑datum.
og_image_alt: Screenshot of a Java IDE showing code that creates an Excel workbook
  with a formatted date cell
og_title: Skapa Excel‑arbetsbok med japanska era‑datum – steg‑för‑steg Java‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create Excel workbook, format cell general, apply style
    Excel cell, and save workbook XLSX using Java and Aspose.Cells.
  headline: How to create Excel workbook with Japanese era dates in Java
  type: TechArticle
tags:
- Java
- Excel automation
- Aspose.Cells
title: Hur man skapar en Excel‑arbetsbok med japanska era‑datum i Java
url: /sv/java/formatting/how-to-create-excel-workbook-with-japanese-era-dates-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du en Excel-arbetsbok med japanska era‑datum i Java

Om du behöver **skapa en Excel-arbetsbok** som lagrar japanska era‑datum, visar den här guiden de exakta stegen. Du kommer att se hur du formaterar cellen som General, applicerar stil på Excel-cellen och slutligen **sparar arbetsboken som XLSX** så att datumet tolkas korrekt.

Att arbeta med japanska era‑strängar (som “R3‑04‑01”) kan vara knepigt eftersom Excel förväntar sig ett riktigt `DateTime`‑värde, inte bara text. I slutet av den här tutorialen har du en fullt fungerande `.xlsx`‑fil som visar rätt gregorianskt datum samtidigt som den ursprungliga era‑notationen bevaras.

## Förutsättningar

- Java 17 eller senare (koden kompileras även med tidigare versioner)
- Aspose.Cells för Java‑biblioteket (`aspose-cells-xx.x.jar`) – biblioteket är gratis för utvärdering och fullt utrustat för produktion
- Grundläggande kunskap om Java och Maven/Gradle (eller förmågan att lägga till en JAR i din classpath)
- En IDE som IntelliJ IDEA, Eclipse eller VS Code (någon av dem fungerar)

## Steg 1 – Skapa en Excel-arbetsbok

Den första operationen är att instansiera ett nytt workbook‑objekt. Detta objekt representerar hela Excel‑filen i minnet och ger dig åtkomst till kalkylblad, celler och stilar.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (an empty .xlsx file in memory)
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Varför detta är viktigt:**  
Att skapa arbetsboken programatiskt eliminerar behovet av en mallfil och garanterar att den resulterande filen startar i ett rent tillstånd. `Workbook`‑konstruktorn skapar automatiskt ett standardblad, som vi hämtar för vidare manipulation.

## Steg 2 – Formatera cellen som General

Excel lagrar tal med olika format. För ett datum som vi senare konverterar från en japansk era‑sträng, sätter vi först cellens talformat till *General* så att Excel inte försöker tolka texten för tidigt.

```java
        // Step 2: Get the target cell (A1) where the era date will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Write the raw Japanese era string (e.g., "R3-04-01")
        targetCell.putValue("R3-04-01");

        // Ensure the cell uses the General number format
        Style cellStyle = targetCell.getStyle();
        cellStyle.setNumber(0); // 0 = General format in Aspose.Cells
        targetCell.setStyle(cellStyle);
```

**Varför detta är viktigt:**  
Att **format cell general** förhindrar att Excel automatiskt formaterar era‑strängen som text med ett anpassat format, vilket skulle blockera senare konvertering till ett riktigt `DateTime`. Anropet `setNumber(0)` är Aspose.Cells‑motsvarigheten till Excels “General”-format.

## Steg 3 – Applicera stil på Excel-cellen

Även om huvudmålet är att lagra ett datum kan du vilja att cellen ser enhetlig ut med resten av bladet – kanske en tunn ram eller ett specifikt teckensnitt. Att applicera en stil visar också hur man manipulerar cellens estetik programatiskt.

```java
        // Step 3: Apply additional styling (optional but common)
        // Example: add a thin border around the cell
        cellStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN);

        // Set a light gray background to highlight the date cell
        cellStyle.setPattern(BackgroundType.SOLID);
        cellStyle.setBackgroundColor(Color.getGray());

        // Apply the updated style back to the cell
        targetCell.setStyle(cellStyle);
```

**Varför detta är viktigt:**  
Steget **apply style excel cell** visar hur du förbättrar den visuella presentationen utan att påverka den underliggande datan. Ramar och bakgrundsfärger lagras som en del av cellens stil‑objekt, vilket säkerställer att den färdiga arbetsboken ser polerad ut när den öppnas i Excel.

## Steg 4 – Konvertera den japanska era‑strängen till ett DateTime‑objekt

Nu ersätter vi den råa texten med ett riktigt `DateTime`‑värde. Aspose.Cells kan tolka en sträng med en specifik `CultureInfo`. Genom att ange den japanska kulturen (`ja-JP`) tolkar biblioteket korrekt “R3‑04‑01” som det tredje året av Reiwa‑eran, vilket motsvarar 2021‑04‑01 i den gregorianska kalendern.

```java
        // Step 4: Convert the era string to a DateTime using Japanese culture
        // The fromString method respects the culture’s calendar (Japanese Imperial)
        DateTime japaneseDate = DateTime.fromString(
                "R3-04-01", // era string
                CultureInfo.createSpecificCulture("ja-JP") // Japanese locale
        );

        // Overwrite the cell value with the parsed DateTime
        targetCell.setValue(japaneseDate);
```

**Varför detta är viktigt:**  
Utan att specificera kulturen skulle “R3‑04‑01” behandlas som vanlig text och förlora sin datumsemantik. `CultureInfo`‑objektet talar om för Aspose.Cells att använda det japanska kalendersystemet och hanterar automatiskt era‑konverteringen. Den resulterande cellen innehåller nu ett riktigt Excel‑datum, vilket möjliggör sortering, filtrering och datum‑aritmetik.

## Steg 5 – Spara arbetsboken som XLSX

Till sist skriver vi den minnes‑lagrade arbetsboken till en fysisk fil. Genom att använda `.xlsx`‑formatet garanteras kompatibilitet med moderna versioner av Excel, Google Sheets och andra kalkylbladsverktyg.

```java
        // Step 5: Save the workbook to the desired location
        String outputPath = "JapaneseEra.xlsx"; // adjust the path as needed
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

**Varför detta är viktigt:**  
Operationen **save workbook xlsx** slutför alla ändringar. Aspose.Cells skriver arbetsboken i Open XML‑formatet och bevarar både data och de stilar som applicerades i tidigare steg. Den resulterande filen kan öppnas direkt i Excel, där cellen visar `2021‑04‑01` (det gregorianska motsvarigheten) men den ursprungliga era‑strängen fortfarande kan återfås via Excels “Format Cells → Number → Custom” om så behövs.

## Förväntat resultat

När du öppnar `JapaneseEra.xlsx` i Microsoft Excel:

- Cell **A1** visar datumet `2021‑04‑01` (Excels standard datumformat).  
- Cellens ram är en tunn grå linje och bakgrunden ljusgrå, vilket bekräftar att steget **apply style excel cell** lyckades.  
- Om du ändrar cellformatet till “General” förblir det underliggande värdet ett riktigt datum, inte den ursprungliga strängen.

Konsolen kommer att skriva ut:

```
Workbook saved successfully to JapaneseEra.xlsx
```

## Vanliga variationer och specialfall

| Situation | Vad som ska ändras |
|-----------|--------------------|
| **Olika era (t.ex. Heisei)** | Använd lämplig era‑prefix (`H` för Heisei) i inmatningssträngen. Samma `CultureInfo` hanterar konverteringen. |
| **Flera datum** | Loopa över ett intervall av celler och tillämpa samma konverteringslogik på varje. |
| **Anpassat datumformat** | Efter `setValue(japaneseDate)`, anropa `cellStyle.setNumber(14)` (eller något Excel‑nummerformat‑ID) för att visa datum som `yyyy/MM/dd`. |
| **Stora arbetsböcker** | Återanvänd ett enda `Style`‑objekt för prestanda, eller använd `StyleFlag` för att endast ändra nödvändiga attribut. |
| **Spara till en ström** | Ersätt `workbook.save(outputPath, SaveFormat.XLSX)` med `workbook.save(outputStream, SaveFormat.XLSX)` när du skickar filen via HTTP. |

## Tips från praktiken

- **Proffstips:** Sätt alltid cellens nummerformat *innan* du tilldelar ett `DateTime`. Att ändra formatet i efterhand kan få Excel att visa fel visuell representation.
- **Se upp för:** Att använda `CultureInfo("ja-JP")` utan `createSpecificCulture` kan falla tillbaka till den gregorianska kalendern, vilket leder till felaktiga datum.
- **Prestanda‑notering:** När du skapar många stylade celler, klona ett befintligt `Style` istället för att anropa `getStyle()` för varje cell; detta minskar intern kopieringskostnad.

## Slutsats

I den här tutorialen har du lärt dig hur du **skapar en Excel-arbetsbok** i Java, **formaterar cellen som General**, **applicerar stil på Excel-cellen** och **sparar arbetsboken som XLSX** samtidigt som du korrekt hanterar japanska era‑datum. Det kompletta kodexemplet är redo att kopieras, klistras in och köras, vilket ger dig en pålitlig grund för all Excel‑automatisering som involverar icke‑gregorianska kalendrar.

Nästa steg, du kan utforska:

- Lägga till formler som refererar till de konverterade datumen (t.ex. `=YEAR(A1)`).
- Exportera arbetsboken till PDF med `workbook.save("output.pdf", SaveFormat.PDF)`.
- Integrera denna logik i en Spring Boot REST‑endpoint för att generera rapporter på begäran.

Känn dig fri att experimentera med olika kulturer, anpassade talformat eller massimport av data. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

De följande tutorialerna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Excel-arbetsbokinitialisering och cellformatering med Aspose.Cells Java: En omfattande guide](/cells/english/java/formatting/excel-workbook-initialization-cell-styling-aspose-cells-java/)
- [Hur man skapar och sparar en Excel-arbetsbok som SVG med Aspose.Cells för Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Hur man skapar och sparar en Excel-arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}