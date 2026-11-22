---
category: general
date: 2026-11-22
description: Tìm hiểu cách sử dụng định dạng số tùy chỉnh để định dạng một cột dưới
  dạng tiền tệ trong Excel bằng Java. Thiết lập định dạng số Excel nhanh chóng với
  một kiểu đơn giản.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: vi
lastmod: 2026-11-22
og_description: Áp dụng định dạng số tùy chỉnh trong Excel bằng Java. Hướng dẫn này
  chỉ cách thiết lập định dạng số trong Excel và định dạng cột đầu tiên dưới dạng
  tiền tệ.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Áp dụng định dạng số tùy chỉnh trong Excel bằng Java – hướng dẫn từng bước
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
title: Cách áp dụng định dạng số tùy chỉnh trong Excel bằng Java
url: /vi/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách áp dụng định dạng số tùy chỉnh trong Excel bằng Java

Nếu bạn cần **định dạng số tùy chỉnh** cho một cột trong bảng tính Excel, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng Java. Dù bạn đang tạo báo cáo tài chính hay xuất dữ liệu kế toán, việc định dạng cột đầu tiên dưới dạng tiền tệ sẽ giúp kết quả ngay lập tức dễ đọc.

Trong ví dụ dưới đây, chúng ta sẽ **định dạng cột dưới dạng tiền tệ**, áp dụng kiểu cho cột đầu tiên, và sau đó nhập một `DataTable` vào bảng tính. Cách tiếp cận này cũng hoạt động cho bất kỳ định dạng số nào bạn muốn hiển thị.

## Những gì bạn sẽ học

* Cách tạo **định dạng số tùy chỉnh** bằng đối tượng `Style` của Apache POI.  
* Cách **đặt định dạng số Excel** cho một cột cụ thể, bao gồm trường hợp **đặt định dạng tiền tệ**.  
* Cách **định dạng cột đầu tiên** khi nhập một `DataTable`.  
* Cách lưu workbook và xác minh rằng định dạng hiển thị đúng.

### Yêu cầu trước

* Java 17 hoặc mới hơn.  
* Apache POI 5.x (thư viện cung cấp `Workbook`, `Worksheet` và `Style`).  
* Một triển khai `DataTable` có thể được lặp lại giống như trong mẫu mã.  
* Kiến thức cơ bản về Java và các khái niệm Excel.

---

## Bước 1: Thiết lập dự án và nhập dữ liệu

Đầu tiên, thêm Apache POI vào dự án của bạn. Nếu bạn sử dụng Maven, bao gồm phụ thuộc sau:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Tiếp theo, lấy dữ liệu nguồn dưới dạng `DataTable`. Trong thực tế, dữ liệu này có thể đến từ truy vấn cơ sở dữ liệu, tệp CSV, hoặc phản hồi API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Mẹo:** Đảm bảo rằng các cột của `DataTable` có kiểu Java đúng (`Integer`, `Double`, v.v.) vì định dạng số chỉ ảnh hưởng đến các ô số.

---

## Bước 2: Tạo **định dạng số tùy chỉnh** cho cột đầu tiên

Một **định dạng số tùy chỉnh** cho Excel biết cách hiển thị các giá trị số. Để hiển thị giá trị dưới dạng tiền tệ, chúng ta sử dụng định dạng tích hợp `CURRENCY`, nhưng bạn cũng có thể định nghĩa các mẫu như `"$#,##0.00"`.

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

**Tại sao cách này hoạt động:**  
* `createCellStyle()` trả về một đối tượng style có thể tái sử dụng.  
* `setDataFormat()` gắn **định dạng tiền tệ** vào style, và Excel sẽ áp dụng cho mọi ô sử dụng style này.  
* Bằng cách lưu style vào `columnStyles[0]`, chúng ta đảm bảo chỉ cột đầu tiên nhận định dạng tiền tệ.

---

## Bước 3: Nhập `DataTable` trong khi áp dụng các style cho cột

Bây giờ chúng ta nhập dữ liệu vào worksheet. Phương thức `importDataTable` nhận mảng style, cho phép chúng ta **định dạng cột đầu tiên** và để các cột còn lại với định dạng mặc định.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Lệnh gọi trên **đặt định dạng số Excel** chỉ cho cột đầu tiên. Tất cả các cột khác kế thừa style mặc định của workbook, giúp mã đơn giản và hiệu quả.

---

## Bước 4: Lưu workbook và xác minh kết quả

Cuối cùng, ghi workbook ra file và mở trong Excel để xác nhận rằng cột đầu tiên hiển thị ký hiệu tiền tệ.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Kết quả mong đợi:**  
Khi bạn mở *FormattedReport.xlsx*, các giá trị trong cột A sẽ xuất hiện với ký hiệu tiền tệ phù hợp (ví dụ, `$1,234.00`). Tất cả các cột khác giữ nguyên biểu diễn số gốc.

---

## Các biến thể phổ biến và trường hợp đặc biệt

| Situation | Adjustment |
|-----------|------------|
| **Tiền tệ khác** (ví dụ, Euro) | Thay thế `Style.CustomNumberFormat.CURRENCY` bằng một mẫu tùy chỉnh: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Nhiều hơn một cột được định dạng** | Điền các mục bổ sung vào `columnStyles[]` với các đối tượng `CellStyle` riêng của chúng. |
| **Bộ dữ liệu lớn** | Sử dụng `importDataTable` theo lô hoặc truyền dòng để tránh `OutOfMemoryError`. |
| **Dấu phân cách theo locale** | Sử dụng `java.text.NumberFormat` để tạo mẫu phù hợp với locale và truyền nó vào `setDataFormat`. |

> **Cảnh báo:** Việc tái sử dụng một đối tượng `CellStyle` duy nhất cho nhiều cột có thể gây ra định dạng không mong muốn vì Excel giới hạn số lượng style riêng biệt trong mỗi workbook. Tạo một style riêng cho mỗi định dạng duy nhất bạn cần.

---

## Ví dụ đầy đủ có thể chạy

Dưới đây là một chương trình tự chứa minh họa toàn bộ quy trình, từ tạo dữ liệu đến lưu workbook đã định dạng.

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

Chạy chương trình sẽ tạo **FormattedReport.xlsx** trong đó cột A (cột “Amount”) được hiển thị với **định dạng số tùy chỉnh** có dấu đô la và hai chữ số thập phân.

---

## Kết luận

Bạn đã biết cách **định dạng số tùy chỉnh** một worksheet Excel từ Java, **định dạng cột dưới dạng tiền tệ**, và **định dạng cột đầu tiên** khi nhập dữ liệu. Bằng cách tạo một `CellStyle` có thể tái sử dụng và truyền nó vào `importDataTable`, bạn có thể **đặt định dạng số Excel** cho bất kỳ cột nào mà không cần lặp qua từng ô một cách thủ công.

Tiếp theo, hãy thử:

* Sử dụng `setDataFormat` với các mẫu theo locale để **đặt định dạng tiền tệ**

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Đặt Định dạng Số Excel trong Java – Hướng dẫn đầy đủ](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Áp dụng Định dạng Số Excel trong Java – Hướng dẫn đầy đủ Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Cách tạo workbook Excel với định dạng tiền tệ và phông chữ đậm trong Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}