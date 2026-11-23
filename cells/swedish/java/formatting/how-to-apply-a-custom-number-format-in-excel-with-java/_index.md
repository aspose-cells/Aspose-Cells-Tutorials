---
category: general
date: 2026-11-22
description: Lär dig hur du använder ett anpassat talformat för att formatera en kolumn
  som valuta i Excel med Java. Ställ in Excels talformat snabbt med en enkel stil.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: sv
lastmod: 2026-11-22
og_description: Använd ett anpassat talformat i Excel med Java. Denna handledning
  visar hur du ställer in Excel‑talformat och formaterar den första kolumnen som valuta.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Använd ett anpassat talformat i Excel med Java – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Hur man använder ett anpassat talformat i Excel med Java
url: /sv/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur du tillämpar ett anpassat talformat i Excel med Java

Om du behöver **custom number format** en kolumn i ett Excel‑blad visar den här guiden exakt hur du gör det med Java. Oavsett om du genererar finansiella rapporter eller exporterar bokföringsdata gör formatering av den första kolumnen som valuta att resultatet blir omedelbart läsbart.

I exemplet nedan kommer vi att **format column as currency**, applicera stilen på den första kolumnen och sedan importera en `DataTable` till bladet. Samma tillvägagångssätt fungerar för alla numeriska format du vill visa.

## Vad du kommer att lära dig

* Hur du skapar ett **custom number format** med Apache POI:s `Style`‑objekt.  
* Hur du **set Excel number format** för en specifik kolumn, inklusive fallet **set currency format**.  
* Hur du **style first column** när du importerar en `DataTable`.  
* Hur du sparar arbetsboken och verifierar att formateringen visas korrekt.

### Förutsättningar

* Java 17 eller nyare.  
* Apache POI 5.x (biblioteket som tillhandahåller `Workbook`, `Worksheet` och `Style`).  
* En `DataTable`‑implementation som kan itereras på samma sätt som i kodexemplet.  
* Grundläggande kunskap om Java‑ och Excel‑koncept.

---

## Steg 1: Ställ in projektet och importera data

Först, lägg till Apache POI i ditt projekt. Om du använder Maven, inkludera följande beroende:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Därefter, hämta källdata som en `DataTable`. I ett verkligt scenario kan detta komma från en databasfråga, en CSV‑fil eller ett API‑svar.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Se till att `DataTable`‑kolumnerna har rätt Java‑typer (`Integer`, `Double` osv.) eftersom talformatet endast påverkar numeriska celler.

---

## Steg 2: Skapa ett **custom number format** för den första kolumnen

Ett **custom number format** talar om för Excel hur numeriska värden ska visas. För att visa värden som valuta använder vi det inbyggda `CURRENCY`‑formatet, men du kan också definiera mönster som `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Varför detta fungerar:**  
* `createCellStyle()` returnerar ett återanvändbart stilobjekt.  
* `setDataFormat()` fäster **set currency format** till stilen, vilket Excel sedan applicerar på varje cell som använder denna stil.  
* Genom att lagra stilen i `columnStyles[0]` säkerställer vi att endast den första kolumnen får valutaformateringen.

---

## Steg 3: Importera `DataTable` samtidigt som du applicerar kolumnstilarna

Nu importerar vi data till bladet. Metoden `importDataTable` accepterar stil‑arrayen, vilket gör att vi kan **style first column** och låta de återstående kolumnerna behålla standardformateringen.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Anropet ovan **sets Excel number format** endast för den första kolumnen. Alla andra kolumner ärver arbetsbokens standardstil, vilket gör koden enkel och effektiv.

---

## Steg 4: Spara arbetsboken och verifiera resultatet

Slutligen, skriv arbetsboken till en fil och öppna den i Excel för att bekräfta att den första kolumnen visar valutasymboler.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Förväntat resultat:**  
När du öppnar *FormattedReport.xlsx* visas värdena i kolumn A med rätt valutasymbol (t.ex. `$1,234.00`). Alla andra kolumner behåller sin ursprungliga numeriska representation.

---

## Vanliga variationer och kantfall

| Situation | Justering |
|-----------|------------|
| **Olika valuta** (t.ex. Euro) | Byt ut `Style.CustomNumberFormat.CURRENCY` mot ett eget mönster: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Mer än en stylad kolumn** | Fyll i ytterligare poster i `columnStyles[]` med egna `CellStyle`‑objekt. |
| **Stora datamängder** | Använd `importDataTable` i batcher eller strömma rader för att undvika `OutOfMemoryError`. |
| **Locale‑specifika avgränsare** | Använd `java.text.NumberFormat` för att generera ett locale‑medvetet mönster och skicka det till `setDataFormat`. |

> **Watch out for:** Återanvändning av ett enda `CellStyle`‑objekt över många kolumner kan orsaka oväntad formatering eftersom Excel begränsar antalet distinkta stilar per arbetsbok. Skapa en separat stil för varje unikt format du behöver.

---

## Fullt körbart exempel

Nedan är ett fristående program som demonstrerar hela arbetsflödet, från dataskapande till att spara den formaterade arbetsboken.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

När programmet körs skapas **FormattedReport.xlsx** där kolumn A (kolumnen “Amount”) visas med ett **custom number format** som visar en dollartecken och två decimaler.

---

## Slutsats

Du vet nu hur du **custom number format** ett Excel‑blad från Java, **format column as currency**, och **style first column** när du importerar data. Genom att skapa ett återanvändbart `CellStyle` och skicka det till `importDataTable` kan du **set Excel number format** för vilken kolumn som helst utan att loopa över varje cell manuellt.

Next, try:

* Använd `setDataFormat` med locale‑specifika mönster för att **set currency format**

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Ställ in talformat i Excel med Java – Komplett guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Applicera talformat i Excel med Java – Komplett Aspose.Cells‑guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Hur man skapar Excel‑arbetsbok med valutformat och fet stil i Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}