---
category: general
date: 2026-08-17
description: Nhập danh sách vào Excel trong Java bằng Aspose.Cells, học cách định
  dạng cột, xuất dữ liệu sang định dạng xlsx và tạo workbook Excel một cách lập trình.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import list to excel
- how to style column
- export data to xlsx
- import data with header
- create excel workbook java
language: vi
lastmod: 2026-08-17
og_description: Nhập danh sách vào Excel trong Java bằng Aspose.Cells, định dạng tiêu
  đề cột, xuất dữ liệu ra xlsx và tạo sổ làm việc Excel một cách hiệu quả.
og_image_alt: Screenshot of a Java‑generated Excel file showing bold column headers
og_title: Nhập danh sách vào Excel trong Java – hướng dẫn đầy đủ với định dạng cột
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  headline: How to import list to Excel and style columns in Java
  type: TechArticle
- description: Import list to Excel in Java using Aspose.Cells, learn how to style
    column, export data to xlsx, and create an Excel workbook programmatically.
  name: How to import list to Excel and style columns in Java
  steps:
  - name: Why this works
    text: '* **`importDataTable`** reads the keys of each map (`"Name"` and `"Score"`)
      as column headers when the `true` flag is set. This satisfies the **import data
      with header** requirement. * The **style array** aligns with the column order.
      By setting `columnStyles[1].getFont().setBold(true)`, we answer t'
  - name: Null values and type safety
    text: 'If a map contains `null` or mixed‑type values, Aspose.Cells automatically
      writes an empty cell. To guarantee consistent typing, you can pre‑process the
      list:'
  - name: Mismatched column counts
    text: '`importDataTable` expects the style array length to match the number of
      columns. If you add a new column later, remember to expand `columnStyles` accordingly,
      otherwise Aspose.Cells throws `IndexOutOfBoundsException`.'
  - name: Large data sets
    text: For more than 10 000 rows, consider using the **`importArray`** overload,
      which streams data directly to the worksheet and reduces memory consumption.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Data export
title: Cách nhập danh sách vào Excel và định dạng cột trong Java
url: /vi/java/excel-import-export/how-to-import-list-to-excel-and-style-columns-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách nhập danh sách vào Excel và định dạng cột trong Java

Nếu bạn cần **nhập danh sách vào Excel** từ một ứng dụng Java, hướng dẫn này sẽ cung cấp cho bạn một giải pháp hoàn chỉnh, có thể chạy ngay. Bạn sẽ thấy cách tạo một workbook Excel, nhập một danh sách các map dưới dạng bảng dữ liệu, áp dụng kiểu chữ đậm cho một cột cụ thể, và lưu kết quả dưới dạng tệp **xlsx**.

Làm việc với bảng tính là một yêu cầu phổ biến cho báo cáo, trao đổi dữ liệu, hoặc tự động hoá. Khi kết thúc tutorial này, bạn sẽ có thể **xuất dữ liệu ra xlsx** với định dạng cột tùy chỉnh mà không rời khỏi mã Java của mình.

## Những gì bạn cần chuẩn bị

* Java 17 hoặc mới hơn (mã cũng hoạt động với Java 8+)
* Thư viện Aspose.Cells for Java – phiên bản 23.10 (hoặc phiên bản mới nhất)
* Môi trường phát triển như IntelliJ IDEA hoặc Eclipse
* Kiến thức cơ bản về các collection của Java (`List`, `Map`)

> **Mẹo chuyên nghiệp:** Thêm phụ thuộc Maven của Aspose.Cells để giữ thư viện luôn cập nhật:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Nhập danh sách vào Excel bằng Aspose.Cells

Bước quan trọng đầu tiên là chuyển đổi một `List<Map<String,Object>>` của Java thành một worksheet Excel. Aspose.Cells cung cấp phương thức `importDataTable`, nhận một collection, cờ header, vị trí bắt đầu dòng/cột, và một mảng style tùy chọn.

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcel {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Prepare the source data (simulating a DataTable)
        List<Map<String, Object>> dataRows = new ArrayList<>();
        dataRows.add(Map.of("Name", "Alice", "Score", 95));
        dataRows.add(Map.of("Name", "Bob",   "Score", 82));
        dataRows.add(Map.of("Name", "Charlie", "Score", 78));

        // 2️⃣ Create style objects – make the "Score" column bold
        Style[] columnStyles = new Style[2];               // two columns: Name, Score
        Workbook styleWorkbook = new Workbook();           // temporary workbook for style creation
        columnStyles[0] = styleWorkbook.createStyle();    // default style for "Name"
        columnStyles[1] = styleWorkbook.createStyle();    // custom style for "Score"
        columnStyles[1].getFont().setBold(true);          // **how to style column** – bold font

        // 3️⃣ Import the list into a worksheet using the style array
        Workbook workbook = new Workbook();                // **create excel workbook java**
        Worksheet sheet = workbook.getWorksheets().get(0);
        // true → include column headers from the map keys
        sheet.getCells().importDataTable(dataRows, true, 0, 0, columnStyles);

        // 4️⃣ Save the workbook to an .xlsx file
        String outputPath = "output/datatable_with_style.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved to: " + outputPath);
    }
}
```

### Tại sao cách này hoạt động

* **`importDataTable`** đọc các key của mỗi map (`"Name"` và `"Score"`) làm tiêu đề cột khi cờ `true` được đặt. Điều này đáp ứng yêu cầu **import data with header**.
* **Mảng style** được sắp xếp theo thứ tự cột. Bằng cách đặt `columnStyles[1].getFont().setBold(true)`, chúng ta trả lời câu hỏi **how to style column** mà không ảnh hưởng tới các cột khác.
* Sử dụng một `Workbook` tạm thời chỉ để tạo style giúp tránh làm bẩn workbook cuối cùng bằng các ô không cần thiết.

## Xuất dữ liệu ra xlsx – xử lý các trường hợp biên phổ biến

### Giá trị null và an toàn kiểu dữ liệu
Nếu một map chứa `null` hoặc các giá trị có kiểu hỗn hợp, Aspose.Cells sẽ tự động ghi một ô trống. Để đảm bảo kiểu dữ liệu nhất quán, bạn có thể tiền xử lý danh sách:

```java
for (Map<String, Object> row : dataRows) {
    row.replaceAll((k, v) -> v == null ? "" : v);
}
```

### Số cột không khớp
`importDataTable` yêu cầu độ dài của mảng style phải bằng số cột. Nếu bạn thêm một cột mới sau này, nhớ mở rộng `columnStyles` cho phù hợp, nếu không Aspose.Cells sẽ ném `IndexOutOfBoundsException`.

### Bộ dữ liệu lớn
Đối với hơn 10 000 hàng, hãy cân nhắc sử dụng overload **`importArray`**, nó sẽ stream dữ liệu trực tiếp vào worksheet và giảm tiêu thụ bộ nhớ.

## Cách định dạng thêm các cột

Bạn có thể định dạng bất kỳ cột nào bằng cách mở rộng mảng `columnStyles`. Dưới đây là ví dụ làm cho cả “Name” và “Score” đều in đậm và thêm màu nền cho cột “Score”.

```java
// Extend to three columns (Name, Score, Date)
Style[] extendedStyles = new Style[3];
Workbook tmp = new Workbook();
extendedStyles[0] = tmp.createStyle(); // Name – bold
extendedStyles[0].getFont().setBold(true);

extendedStyles[1] = tmp.createStyle(); // Score – bold + yellow background
extendedStyles[1].getFont().setBold(true);
extendedStyles[1].getPattern().setBackgroundColor(Color.getYellow());

extendedStyles[2] = tmp.createStyle(); // Date – default
```

Thay thế `columnStyles` gốc bằng `extendedStyles` và điều chỉnh nguồn dữ liệu cho phù hợp. Điều này minh họa **how to style column** cho nhiều kịch bản.

## Kiểm tra kết quả

Mở `output/datatable_with_style.xlsx` trong Microsoft Excel, Google Sheets, hoặc LibreOffice Calc. Bạn sẽ thấy:

| **Name**   | **Score** |
|------------|----------|
| Alice      | **95**   |
| Bob        | **82**   |
| Charlie    | **78**   |

Tiêu đề **Score** và các ô của nó hiển thị in đậm, xác nhận style đã được áp dụng đúng.

## Ví dụ hoàn chỉnh từ đầu đến cuối (sẵn sàng copy‑paste)

```java
import com.aspose.cells.*;
import java.util.*;

public class ImportListToExcelFull {
    public static void main(String[] args) throws Exception {
        // ----- Prepare sample data -----
        List<Map<String, Object>> rows = new ArrayList<>();
        rows.add(Map.of("Name", "Alice",   "Score", 95));
        rows.add(Map.of("Name", "Bob",     "Score", 82));
        rows.add(Map.of("Name", "Charlie", "Score", 78));

        // ----- Create column styles (Score column bold) -----
        Style[] styles = new Style[2];
        Workbook styleWB = new Workbook();                // temporary workbook for style objects
        styles[0] = styleWB.createStyle();                // Name – default
        styles[1] = styleWB.createStyle();                // Score – custom
        styles[1].getFont().setBold(true);                // apply bold font

        // ----- Build the workbook and import the list -----
        Workbook wb = new Workbook();                     // **create excel workbook java**
        Worksheet ws = wb.getWorksheets().get(0);
        ws.getCells().importDataTable(rows, true, 0, 0, styles); // true = import header row

        // ----- Save as XLSX -----
        String outFile = "output/datatable_with_style.xlsx";
        wb.save(outFile, SaveFormat.XLSX);

        System.out.println("Excel file created at: " + outFile);
    }
}
```

Chạy chương trình này sẽ tạo ra workbook chính xác như đã mô tả ở trên.

## Kết luận

Bây giờ bạn đã biết cách **nhập danh sách vào Excel**, áp dụng định dạng tùy chỉnh cho một cột cụ thể, và **xuất dữ liệu ra xlsx** bằng Aspose.Cells for Java. Tutorial đã bao phủ:

* Tạo một workbook Excel trong Java (`create excel workbook java`)
* Nhập danh sách các map với tiêu đề cột (`import data with header`)
* Định dạng một cột (`how to style column`) thông qua mảng style
* Lưu kết quả dưới dạng tệp XLSX

Từ đây, bạn có thể khám phá các định dạng nâng cao hơn (viền, định dạng số), thêm biểu đồ, hoặc tạo nhiều worksheet trong cùng một workbook. Hãy thử với các nguồn dữ liệu khác nhau—tệp CSV, cơ sở dữ liệu, hoặc phản hồi API REST—để mở rộng mẫu đã trình bày trong hướng dẫn này.

Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ và các giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)
- [Excel Data Import and Export Tutorials for Aspose.Cells Java](/cells/english/java/import-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}