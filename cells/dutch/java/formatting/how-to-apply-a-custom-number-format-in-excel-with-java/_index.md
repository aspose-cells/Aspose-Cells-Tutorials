---
category: general
date: 2026-11-22
description: Leer hoe je een aangepast getalformaat gebruikt om een kolom als valuta
  te formatteren in Excel met Java. Stel het Excel‑getalformaat snel in met een eenvoudige
  stijl.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: nl
lastmod: 2026-11-22
og_description: Pas een aangepast getalformaat toe in Excel met Java. Deze tutorial
  laat zien hoe je het Excel‑getalformaat instelt en de eerste kolom als valuta opmaakt.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Pas een aangepast getalformaat toe in Excel met Java – stapsgewijze handleiding
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
title: Hoe een aangepast getalformaat in Excel toepassen met Java
url: /nl/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een custom number format toe te passen in Excel met Java

Als je een **custom number format** moet toepassen op een kolom in een Excel-werkblad, laat deze gids je precies zien hoe je dat doet met Java. Of je nu financiële rapporten genereert of boekhoudgegevens exporteert, het formatteren van de eerste kolom als valuta maakt de output direct leesbaar.

In het voorbeeld hieronder zullen we **format column as currency** toepassen, de stijl op de eerste kolom toepassen, en vervolgens een `DataTable` in het werkblad importeren. Dezelfde aanpak werkt voor elk numeriek formaat dat je wilt weergeven.

## Wat je zult leren

* Hoe je een **custom number format** maakt met het `Style`-object van Apache POI.  
* Hoe je **set Excel number format** instelt voor een specifieke kolom, inclusief het geval **set currency format**.  
* Hoe je **style first column** toepast tijdens het importeren van een `DataTable`.  
* Hoe je de werkmap opslaat en verifieert dat de opmaak correct wordt weergegeven.

### Vereisten

* Java 17 of nieuwer.  
* Apache POI 5.x (de bibliotheek die `Workbook`, `Worksheet` en `Style` levert).  
* Een `DataTable`-implementatie die kan worden doorlopen zoals in het code‑voorbeeld.  
* Basiskennis van Java en Excel-concepten.

---

## Stap 1: Het project opzetten en de gegevens importeren

Eerst voeg je Apache POI toe aan je project. Als je Maven gebruikt, neem dan de volgende afhankelijkheid op:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Vervolgens verkrijg je de brongegevens als een `DataTable`. In een real‑world scenario kan dit afkomstig zijn van een database‑query, een CSV‑bestand of een API‑respons.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Zorg ervoor dat de `DataTable`-kolommen de juiste Java‑types hebben (`Integer`, `Double`, etc.) omdat het getalformaat alleen numerieke cellen beïnvloedt.

---

## Stap 2: Maak een **custom number format** voor de eerste kolom

Een **custom number format** vertelt Excel hoe numerieke waarden moeten worden weergegeven. Om waarden als valuta te tonen gebruiken we het ingebouwde `CURRENCY`-formaat, maar je kunt ook patronen definiëren zoals `"$#,##0.00"`.

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

**Waarom dit werkt:**  
* `createCellStyle()` retourneert een herbruikbaar stijlobject.  
* `setDataFormat()` koppelt de **set currency format** aan de stijl, die Excel vervolgens toepast op elke cel die deze stijl gebruikt.  
* Door de stijl op te slaan in `columnStyles[0]` garanderen we dat alleen de eerste kolom de valutavormgeving krijgt.

---

## Stap 3: Importeer de `DataTable` terwijl je de kolomstijlen toepast

Nu importeren we de gegevens in het werkblad. De `importDataTable`-methode accepteert de stijl‑array, waardoor we **style first column** kunnen toepassen en de overige kolommen met de standaardopmaak laten.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

De bovenstaande oproep **sets Excel number format** alleen voor de eerste kolom. Alle andere kolommen erven de standaardstijl van de werkmap, wat de code eenvoudig en efficiënt houdt.

---

## Stap 4: Sla de werkmap op en controleer het resultaat

Tot slot schrijf je de werkmap naar een bestand en open je deze in Excel om te bevestigen dat de eerste kolom valutatekens toont.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Verwachte output:**  
Wanneer je *FormattedReport.xlsx* opent, verschijnen de waarden in kolom A met het juiste valutateken (bijv. `$1,234.00`). Alle andere kolommen behouden hun oorspronkelijke numerieke weergave.

---

## Veelvoorkomende variaties en randgevallen

| Situatie | Aanpassing |
|-----------|------------|
| **Different currency** (e.g., Euro) | Replace `Style.CustomNumberFormat.CURRENCY` with a custom pattern: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **More than one styled column** | Populate additional entries in `columnStyles[]` with their own `CellStyle` objects. |
| **Large data sets** | Use `importDataTable` in batches or stream rows to avoid `OutOfMemoryError`. |
| **Locale‑specific separators** | Use `java.text.NumberFormat` to generate a locale‑aware pattern and pass it to `setDataFormat`. |

> **Let op:** Het hergebruiken van één `CellStyle`‑object over veel kolommen kan onverwachte opmaak veroorzaken omdat Excel het aantal verschillende stijlen per werkmap beperkt. Maak een aparte stijl voor elk uniek formaat dat je nodig hebt.

---

## Volledig uitvoerbaar voorbeeld

Hieronder staat een zelfstandig programma dat de volledige workflow demonstreert, van het maken van gegevens tot het opslaan van de opgemaakte werkmap.

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

Het uitvoeren van het programma maakt **FormattedReport.xlsx** waarin kolom A (de “Amount”-kolom) wordt weergegeven met een **custom number format** dat een dollarteken en twee decimalen toont.

---

## Conclusie

Je weet nu hoe je een Excel‑werkblad vanuit Java **custom number format**, **format column as currency** en **style first column** kunt toepassen tijdens het importeren van gegevens. Door een herbruikbare `CellStyle` te maken en deze door te geven aan `importDataTable`, kun je **set Excel number format** voor elke kolom instellen zonder handmatig over elke cel te itereren.

Probeer nu:

* Gebruik `setDataFormat` met locale‑specifieke patronen om **set currency format** toe te passen.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Getalopmaak instellen in Excel met Java – Complete gids](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Getalopmaak toepassen in Excel met Java – Complete Aspose.Cells gids](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Hoe een Excel-werkmap te maken met valutavormaat en vet lettertype in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}