---
category: general
date: 2026-06-21
description: Hur man applicerar stilar när man konverterar DataTable till Excel i
  Java. Lär dig att importera datatabellen till Excel, lägga till anpassade stilar
  i Excel och spara arbetsboken till en fil på några minuter.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: sv
og_description: Hur man applicerar stilar vid konvertering av DataTable till Excel
  i Java. Denna guide visar hur du importerar en datatabell till Excel, lägger till
  anpassade stilar i Excel och sparar arbetsboken till en fil.
og_title: Hur du applicerar stilar när du konverterar DataTable till Excel – Java‑handledning
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
title: Hur man tillämpar stilar vid konvertering av DataTable till Excel – Fullständig
  Java‑guide
url: /sv/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man tillämpar stilar när man konverterar DataTable till Excel – Fullständig Java‑guide

Har du någonsin undrat **hur man tillämpar stilar** när du behöver **konvertera DataTable till Excel**? Du är inte ensam. I många interna verktyg hämtar vi data från databaser, placerar den i en `DataTable`, och förväntar oss sedan ett snyggt kalkylblad utan extra arbete. Spoilern: du måste tala om för biblioteket *exakt* vad “snyggt” betyder.

I den här handledningen går vi igenom ett komplett, färdigt‑att‑köra exempel som visar **hur man tillämpar stilar** med Aspose.Cells för Java, importerar en `DataTable` till Excel, **lägger till anpassade stilar i Excel‑stil**, och slutligen **sparar arbetsboken till fil**. I slutet har du ett återanvändbart kodsnutt som du kan lägga in i vilket projekt som helst.

---

## Vad du behöver

- **Java 17** (eller någon nyare JDK) – koden fungerar även på Java 8+.
- **Aspose.Cells for Java** JAR (gratis provversion fungerar bra för testning).
- En `DataTable`‑källa – vi kommer att simulera en enkel, men du kan byta ut den mot vilket riktigt frågeresultat som helst.
- En IDE du gillar (IntelliJ, Eclipse, VS Code… du bestämmer).

Inga extra byggverktyg krävs; en enkel Maven `pom.xml` räcker, men du kan också lägga till JAR‑filen manuellt.

## Steg 1: Ställ in projektet och beroenden

Först och främst—låt oss få biblioteket på classpath.

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

Om du inte använder Maven, släng bara `aspose-cells-24.9.jar` i din `libs`‑mapp och lägg till den i byggsökvägen.

> **Proffstips:** Aspose levereras med en `License`‑klass. Registrera din licens tidigt, annars får du vattenstämplar i utdatafilen.

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

Nu är vi redo att prata om **hur man tillämpar stilar**.

## Steg 2: Skapa anpassade stilar för Excel

Magin i ett polerat kalkylblad ligger i dess cellstilar. Aspose låter dig definiera ett `Style`‑objekt, justera teckensnitt, färger, kanter och sedan återanvända det var du vill. Nedan är ett kompakt sätt att **lägga till anpassade stilar i Excel**‑omfattning.

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

Lägg märke till hur vi skapade **två distinkta stilar**—en för kolumnrubriker och en för dataraderna. Du kan utöka den här arrayen med så många stilar du behöver; Aspose kommer att tillämpa dem i ordning när du anropar `importDataTable`.

## Steg 3: Importera DataTable till arbetsbladet

Nu kommer delen som faktiskt **importerar datatable till excel**. Metoden `importDataTable` tar käll‑`DataTable`, en flagga för kolumnrubriker, startrad/kolumn, och stil‑arrayen vi just byggde.

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

En snabb sidnotering: argumentet `true` talar om för Aspose att **bevara kolumnrubriker**—det är det vanliga fallet när du vill ha en läsbar rapport. Om du sätter det till `false` blir den första dataraden rubriken.

## Steg 4: Sätt ihop allt – ett minimalt fungerande exempel

Nedan är en självständig `main`‑metod som skapar en dummy‑`DataTable`, anropar exportrutinen och skriver `output.xlsx` till mappen `./results`.

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

**Förväntat resultat:** Öppna `output.xlsx` så ser du en fet, grå rubrikrad, tunna kantade dataceller och kolumner som automatiskt anpassas efter innehållet. Det är exakt **hur man tillämpar stilar** för att få bladet att se professionellt ut.

![Hur man tillämpar stilar i Excel‑arbetsbok](/images/excel-styles.png){alt="hur man tillämpar stilar i Excel‑arbetsbok"}

*(Skärmdumpen visar rubriken i fet grå färg och datarader med tunna kanter.)*

## Steg 5: Avancerade tips & kantfall

### 5.1 Villkorsstyrd formatering istället för fasta stilar  
Om du behöver markera rader där `Score > 90`, kan du lägga till en `ConditionalFormattingCollection` efter importen. Detta ger dig dynamisk färgning utan att hårdkoda extra stilar.

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Sammanfoga celler för titlar  
Ibland behöver en rapport en stor titel som sträcker sig över flera kolumner. Använd `worksheet.getCells().merge(0, 0, 1, 3)` och tillämpa sedan en distinkt stil på det sammanslagna området.

### 5.3 Stora dataset – prestandaöverväganden  
När du hanterar >100 000 rader, sätt `ImportDataTableOptions` till `ImportDataTableOptions.NO_FORMATTING` först, och tillämpa sedan stilar i ett andra pass. Detta undviker overheaden av att formatera varje cell under import.

### 5.4 Export av flera blad  
Om du har flera `DataTable`s, skapa bara ytterligare arbetsblad via `workbook.getWorksheets().add("Sheet2")` och upprepa steget **importera datatable till excel** för varje blad.

## Slutsats

Vi har gått igenom **hur man tillämpar stilar** från början till slut: att sätta upp Aspose.Cells, bygga **anpassade stilar i Excel**, **importera datatable till excel**, och slutligen **spara arbetsboken till fil**. Det kompletta kodexemplet är redo att kopieras och klistras in, och de extra tipsen ger dig en färdplan för mer sofistikerade rapporter.

Nästa steg kan vara att utforska **lägga till anpassade stilar i Excel** för diagram, eller experimentera med **konvertera datatable till excel** i en Spring Boot REST‑endpoint. Oavsett har du nu en solid grund för att förvandla råa tabeller till polerade kalkylblad—ingen manuell formatering behövs.

Har du frågor

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man tillämpar stilar på Excel‑celler med Aspose.Cells för Java – Komplett guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Sammanfoga celler & tillämpa stilar i Excel med Aspose.Cells för Java – En komplett guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Hur man importerar DataTable till Excel med Aspose.Cells för .NET (Steg‑för‑steg‑guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}