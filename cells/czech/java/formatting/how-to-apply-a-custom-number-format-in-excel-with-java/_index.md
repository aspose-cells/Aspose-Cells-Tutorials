---
category: general
date: 2026-11-22
description: Naučte se, jak pomocí vlastního formátu čísel formátovat sloupec jako
  měnu v Excelu pomocí Javy. Nastavte formát čísel v Excelu rychle pomocí jednoduchého
  stylu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: cs
lastmod: 2026-11-22
og_description: Použijte vlastní formát čísel v Excelu pomocí Javy. Tento tutoriál
  ukazuje, jak nastavit formát čísel v Excelu a stylovat první sloupec jako měnu.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Použijte vlastní formát čísel v Excelu pomocí Javy – krok za krokem
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
title: Jak použít vlastní číselný formát v Excelu pomocí Javy
url: /cs/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít vlastní formát čísel v Excelu pomocí Javy

Pokud potřebujete **vlastní formát čísel** sloupce v listu Excelu, tento průvodce vám přesně ukáže, jak to provést pomocí Javy. Ať už generujete finanční zprávy nebo exportujete účetní data, formátování prvního sloupce jako měny činí výstup okamžitě čitelným.

V níže uvedeném příkladu **naformátujeme sloupec jako měnu**, použijeme styl na první sloupec a poté importujeme `DataTable` do listu. Stejný přístup funguje pro jakýkoli číselný formát, který chcete zobrazit.

## Co se naučíte

* Jak vytvořit **vlastní formát čísel** pomocí objektu `Style` z Apache POI.  
* Jak **nastavit formát čísel v Excelu** pro konkrétní sloupec, včetně případu **nastavení formátu měny**.  
* Jak **stylovat první sloupec** při importu `DataTable`.  
* Jak uložit sešit a ověřit, že formátování je zobrazeno správně.

### Předpoklady

* Java 17 nebo novější.  
* Apache POI 5.x (knihovna, která poskytuje `Workbook`, `Worksheet` a `Style`).  
* Implementace `DataTable`, kterou lze iterovat podobně jako v ukázkovém kódu.  
* Základní znalost Javy a konceptů Excelu.

---

## Krok 1: Nastavení projektu a import dat

Nejprve přidejte Apache POI do svého projektu. Pokud používáte Maven, zahrňte následující závislost:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Dále získejte zdrojová data jako `DataTable`. V reálném scénáři může pocházet z databázového dotazu, CSV souboru nebo odpovědi API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Tip:** Ujistěte se, že sloupce `DataTable` mají správné typy v Javě (`Integer`, `Double`, atd.), protože formát čísla ovlivňuje jen číselné buňky.

---

## Krok 2: Vytvořte **vlastní formát čísel** pro první sloupec

**Vlastní formát čísel** říká Excelu, jak má zobrazovat číselné hodnoty. Pro zobrazení hodnot jako měny použijeme vestavěný formát `CURRENCY`, ale můžete také definovat vzory jako `"$#,##0.00"`.

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

**Proč to funguje:**  
* `createCellStyle()` vrací znovupoužitelný objekt stylu.  
* `setDataFormat()` připojí **nastavení formátu měny** ke stylu, který Excel následně použije na každou buňku s tímto stylem.  
* Uložením stylu do `columnStyles[0]` zaručujeme, že jen první sloupec získá formátování měny.

---

## Krok 3: Importujte `DataTable` při aplikaci stylů sloupců

Nyní importujeme data do listu. Metoda `importDataTable` přijímá pole stylů, což nám umožňuje **stylovat první sloupec** a nechat ostatní sloupce s výchozím formátováním.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Volání výše **nastavuje formát čísel v Excelu** pouze pro první sloupec. Všechny ostatní sloupce dědí výchozí styl sešitu, což udržuje kód jednoduchý a efektivní.

---

## Krok 4: Uložte sešit a ověřte výsledek

Nakonec zapíšete sešit do souboru a otevřete jej v Excelu, abyste potvrdili, že první sloupec zobrazuje měnové symboly.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Očekávaný výstup:**  
Když otevřete *FormattedReport.xlsx*, hodnoty ve sloupci A se zobrazí s příslušným měnovým symbolem (např. `$1,234.00`). Všechny ostatní sloupce si zachovají původní číselnou reprezentaci.

---

## Běžné varianty a okrajové případy

| Situace | Úprava |
|-----------|------------|
| **Jiná měna** (např. Euro) | Nahraďte `Style.CustomNumberFormat.CURRENCY` vlastním vzorcem: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Více než jeden stylovaný sloupec** | Vyplňte další položky v `columnStyles[]` vlastními objekty `CellStyle`. |
| **Velké datové sady** | Použijte `importDataTable` po dávkách nebo streamujte řádky, aby se předešlo `OutOfMemoryError`. |
| **Locale‑specifické oddělovače** | Použijte `java.text.NumberFormat` k vytvoření locale‑specifického vzorce a předávejte jej do `setDataFormat`. |

> **Pozor:** Opakované používání jednoho objektu `CellStyle` napříč mnoha sloupci může způsobit neočekávané formátování, protože Excel omezuje počet různých stylů na sešit. Vytvořte samostatný styl pro každý unikátní formát, který potřebujete.

---

## Kompletní spustitelný příklad

Níže je samostatný program, který demonstruje celý pracovní postup, od vytvoření dat až po uložení naformátovaného sešitu.

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

Spuštěním programu vznikne **FormattedReport.xlsx**, kde sloupec A (sloupec „Amount“) je zobrazen s **vlastním formátem čísel**, který ukazuje dolarový znak a dvě desetinná místa.

---

## Závěr

Nyní víte, jak **vlastní formát čísel** použít v Excelovém listu z Javy, **naformátovat sloupec jako měnu** a **stylovat první sloupec** při importu dat. Vytvořením znovupoužitelného `CellStyle` a předáním do `importDataTable` můžete **nastavit formát čísel v Excelu** pro libovolný sloupec, aniž byste museli ručně procházet každou buňku.

Dále vyzkoušejte:

* Použít `setDataFormat` s locale‑specifickými vzorci pro **nastavení formátu měny**

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Nastavení formátu čísel v Excelu v Javě – Kompletní průvodce](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Aplikace formátu čísel v Excelu v Javě – Kompletní průvodce Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Jak vytvořit Excel sešit s formátem měny a tučným písmem v Javě](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}