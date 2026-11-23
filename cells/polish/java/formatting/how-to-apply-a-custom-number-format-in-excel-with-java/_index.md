---
category: general
date: 2026-11-22
description: Naucz się, jak używać własnego formatu liczbowego, aby sformatować kolumnę
  jako walutę w Excelu przy użyciu Javy. Szybko ustaw format liczbowy w Excelu za
  pomocą prostego stylu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: pl
lastmod: 2026-11-22
og_description: Zastosuj niestandardowy format liczbowy w Excelu przy użyciu Javy.
  Ten samouczek pokazuje, jak ustawić format liczbowy w Excelu i sformatować pierwszą
  kolumnę jako walutę.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Zastosuj niestandardowy format liczbowy w Excelu przy użyciu Javy – przewodnik
  krok po kroku
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
title: Jak zastosować własny format liczbowy w Excelu przy użyciu Javy
url: /pl/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zastosować własny format liczbowy w Excelu przy użyciu Javy

Jeśli potrzebujesz **custom number format** kolumny w arkuszu Excel, ten przewodnik pokazuje dokładnie, jak to zrobić przy użyciu Javy. Niezależnie od tego, czy generujesz raporty finansowe, czy eksportujesz dane księgowe, formatowanie pierwszej kolumny jako waluty sprawia, że wynik jest od razu czytelny.

W poniższym przykładzie **format column as currency**, zastosujemy styl do pierwszej kolumny, a następnie zaimportujemy `DataTable` do arkusza. To samo podejście działa dla dowolnego formatu liczbowego, który chcesz wyświetlić.

## Co się nauczysz

* Jak utworzyć **custom number format** przy użyciu obiektu `Style` z Apache POI.  
* Jak **set Excel number format** dla konkretnej kolumny, w tym przypadek **set currency format**.  
* Jak **style first column** podczas importowania `DataTable`.  
* Jak zapisać skoroszyt i zweryfikować, że formatowanie wyświetla się poprawnie.

### Wymagania wstępne

* Java 17 lub nowsza.  
* Apache POI 5.x (biblioteka dostarczająca `Workbook`, `Worksheet` i `Style`).  
* Implementacja `DataTable`, którą można iterować podobnie jak w przykładzie kodu.  
* Podstawowa znajomość Javy i koncepcji Excela.

---

## Krok 1: Konfiguracja projektu i import danych

Najpierw dodaj Apache POI do swojego projektu. Jeśli używasz Mavena, dołącz następującą zależność:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Następnie uzyskaj dane źródłowe jako `DataTable`. W rzeczywistym scenariuszu może to pochodzić z zapytania do bazy danych, pliku CSV lub odpowiedzi API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Upewnij się, że kolumny `DataTable` mają odpowiednie typy Javy (`Integer`, `Double` itp.), ponieważ format liczbowy wpływa tylko na komórki numeryczne.

---

## Krok 2: Utwórz **custom number format** dla pierwszej kolumny

**custom number format** określa, jak Excel ma wyświetlać wartości liczbowe. Aby wyświetlić wartości jako walutę, używamy wbudowanego formatu `CURRENCY`, ale możesz także zdefiniować wzorce, takie jak `"$#,##0.00"`.

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

**Dlaczego to działa:**  
* `createCellStyle()` zwraca wielokrotnego użytku obiekt stylu.  
* `setDataFormat()` dołącza **set currency format** do stylu, który Excel następnie stosuje do każdej komórki używającej tego stylu.  
* Przechowując styl w `columnStyles[0]`, zapewniamy, że tylko pierwsza kolumna otrzymuje formatowanie walutowe.

---

## Krok 3: Importuj `DataTable` z zastosowaniem stylów kolumn

Teraz importujemy dane do arkusza. Metoda `importDataTable` przyjmuje tablicę stylów, co pozwala nam **style first column** i pozostawić pozostałe kolumny z domyślnym formatowaniem.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Powyższe wywołanie **sets Excel number format** tylko dla pierwszej kolumny. Wszystkie pozostałe kolumny dziedziczą domyślny styl skoroszytu, co utrzymuje kod prostym i wydajnym.

---

## Krok 4: Zapisz skoroszyt i zweryfikuj wynik

Na koniec zapisz skoroszyt do pliku i otwórz go w Excelu, aby potwierdzić, że pierwsza kolumna wyświetla symbole waluty.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Oczekiwany wynik:**  
Kiedy otworzysz *FormattedReport.xlsx*, wartości w kolumnie A pojawią się z odpowiednim symbolem waluty (np. `$1,234.00`). Wszystkie pozostałe kolumny zachowują pierwotną reprezentację liczbową.

---

## Typowe warianty i przypadki brzegowe

| Sytuacja | Dostosowanie |
|-----------|------------|
| **Inna waluta** (np. Euro) | Zastąp `Style.CustomNumberFormat.CURRENCY` własnym wzorcem: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Więcej niż jedna stylowana kolumna** | Wypełnij dodatkowe pozycje w `columnStyles[]` własnymi obiektami `CellStyle`. |
| **Duże zestawy danych** | Użyj `importDataTable` w partiach lub strumieniuj wiersze, aby uniknąć `OutOfMemoryError`. |
| **Separatory zależne od lokalizacji** | Użyj `java.text.NumberFormat` do wygenerowania wzorca zależnego od lokalizacji i przekaż go do `setDataFormat`. |

> **Watch out for:** Ponowne użycie jednego obiektu `CellStyle` w wielu kolumnach może powodować nieoczekiwane formatowanie, ponieważ Excel ogranicza liczbę różnych stylów w skoroszycie. Utwórz osobny styl dla każdego unikalnego formatu, którego potrzebujesz.

---

## Pełny przykład do uruchomienia

Poniżej znajduje się samodzielny program, który demonstruje cały przepływ pracy, od tworzenia danych po zapisanie sformatowanego skoroszytu.

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

Uruchomienie programu tworzy **FormattedReport.xlsx**, w którym kolumna A (kolumna „Amount”) jest wyświetlana z **custom number format**, który pokazuje znak dolara i dwie miejsca po przecinku.

---

## Podsumowanie

Teraz wiesz, jak **custom number format** arkusz Excel z Javy, **format column as currency**, oraz **style first column** podczas importowania danych. Tworząc wielokrotnego użytku `CellStyle` i przekazując go do `importDataTable`, możesz **set Excel number format** dla dowolnej kolumny bez ręcznego iterowania po każdej komórce.

Next, try:

* Użycie `setDataFormat` z wzorcami zależnymi od lokalizacji, aby **set currency format**

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Ustaw format liczbowy w Excelu w Javie – Kompletny przewodnik](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Zastosuj format liczbowy w Excelu w Javie – Kompletny przewodnik Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Jak stworzyć skoroszyt Excel z formatem waluty i pogrubioną czcionką w Javie](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}