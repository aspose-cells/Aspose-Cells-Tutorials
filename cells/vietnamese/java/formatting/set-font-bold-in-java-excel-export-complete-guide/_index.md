---
category: general
date: 2026-06-30
description: Đặt chữ đậm khi nhập DataTable vào Excel bằng Java. Tìm hiểu mã định
  dạng có điều kiện, nhập DataTable vào Excel và tạo kiểu cho bảng một cách dễ dàng.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: vi
og_description: Đặt chữ đậm trong Java khi xuất DataTable sang Excel. Hướng dẫn này
  bao gồm mã định dạng có điều kiện, nhập DataTable vào Excel và tạo kiểu cho bảng.
og_title: Đặt Font In Đậm trong Xuất Excel bằng Java – Hướng Dẫn Từng Bước
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Đặt Font Đậm Khi Xuất Excel trong Java – Hướng Dẫn Toàn Diện
url: /vi/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Font Đậm trong Xuất Excel bằng Java – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách đặt font đậm** cho các cột cụ thể khi **nhập tệp excel datatable** chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần một bảng tính được định dạng đẹp mà không phải chỉnh sửa từng ô một cách thủ công. Tin tốt là gì? Chỉ với vài dòng Java, bạn có thể nhập một `DataTable`, áp dụng font đậm, và thậm chí thêm một số **mã định dạng có điều kiện**—tất cả đều được thực hiện bằng chương trình.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ đầy đủ, có thể chạy ngay, cho thấy **cách nhập datatable** vào một workbook Excel, áp dụng **set font bold** cho mọi cột có chỉ số chẵn, và tùy chọn thêm một định dạng có điều kiện đơn giản. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy và hiểu rõ **import table with styles** cho bất kỳ dự án nào.

## Yêu cầu trước

- Java 8 hoặc mới hơn (mã cũng hoạt động trên Java 17)  
- Aspose.Cells for Java (phiên bản dùng thử miễn phí là đủ) – thêm dependency Maven hoặc JAR vào classpath của bạn.  
- Kiến thức cơ bản về chuyển đổi `java.sql` `ResultSet` → `DataTable` (chúng tôi sẽ mô phỏng một bảng để đơn giản).  
- Một IDE hoặc công cụ build như Maven/Gradle.

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng Maven, thêm đoạn này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Tổng quan về Giải pháp

1. **Tạo một `DataTable` mô phỏng** dữ liệu mà bạn thường lấy từ cơ sở dữ liệu.  
2. **Tạo một mảng `CellStyle`** trong đó mỗi cột chẵn sẽ có font đậm – đây là phần cốt lõi của **set font bold**.  
3. **Lấy worksheet đầu tiên** từ workbook.  
4. **Nhập `DataTable`** cùng tiêu đề cột, bắt đầu từ ô `A1`, và áp dụng các style đã chuẩn bị.  
5. (Tùy chọn) **Thêm một quy tắc định dạng có điều kiện** để minh họa từ khóa **conditional formatting code**.

Mỗi bước được giải thích bằng tiếng Anh đơn giản, và các khối mã đều tự chứa nên bạn có thể sao chép‑dán và chạy ngay lập tức.

---

## Bước 1: Lấy hoặc Xây dựng DataTable để Nhập

Trong các ứng dụng thực tế, bạn có thể sẽ gọi các tiện ích chuyển đổi `ResultSet` → `DataTable`. Đối với hướng dẫn này, chúng ta sẽ tạo một `DataTable` đơn giản bằng tay để bạn có thể tập trung vào phần Excel.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Tại sao điều này quan trọng:** Có một `DataTable` sẵn sàng cho phép chúng ta tập trung vào API **import datatable excel** và logic định dạng. Phương pháp trên có thể tái sử dụng—chỉ cần thay thế các hàng được mã hoá sẵn bằng truy vấn cơ sở dữ liệu khi đưa vào môi trường production.

---

## Bước 2: Chuẩn bị Styles – Đây là nơi chúng ta **Set Font Bold**

Bây giờ chúng ta sẽ xây dựng một mảng các đối tượng `CellStyle`, một cho mỗi cột. Quy tắc rất đơn giản: **set font bold** cho mọi cột có chỉ số chẵn (0, 2, 4,…). Các cột lẻ sẽ giữ nguyên.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Tại sao lại dùng Mảng Styles?

- **Hiệu suất:** Áp dụng một style cho mỗi cột nhanh hơn so với việc định dạng từng ô riêng lẻ.  
- **Nhất quán:** Mỗi ô trong một cột sẽ kế thừa cùng một định dạng, đảm bảo giao diện đồng nhất.  
- **Mở rộng:** Khi thêm cột mới, chỉ cần mở rộng mảng—không cần viết lại mã.

---

## Bước 3: Truy cập Worksheet Đầu tiên trong Workbook

Aspose.Cells tạo một worksheet mặc định cho chúng ta, nhưng việc lấy nó một cách rõ ràng là thực hành tốt. Điều này cũng minh họa **cách nhập datatable** vào một sheet cụ thể.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## Bước 4: Nhập DataTable với Styles – Hoạt động Cốt lõi **Import Table With Styles**

Phương thức `importDataTable` thực hiện phần công việc nặng. Nó sao chép dữ liệu, thêm tiêu đề cột, và áp dụng mảng style mà chúng ta đã tạo trước đó.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Khi bạn chạy ví dụ, bạn sẽ thấy **set font bold** được áp dụng cho các cột `ID` và `Score`, trong khi `Name` vẫn giữ dạng thường.

---

## Bước 5 (Tùy chọn): Thêm Định dạng Có Điều kiện – Một Ví dụ Nhanh **Conditional Formatting Code**

Nếu bạn muốn làm nổi bật các hàng có điểm số vượt quá 90, chỉ cần thêm vài dòng sẽ thực hiện được. Điều này cho thấy từ khóa **conditional formatting code** mà không làm rối luồng chính.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Lưu ý:** Đoạn mã trên là tùy chọn nhưng minh họa cách bạn có thể xếp lớp **conditional formatting code** lên bảng đã được định dạng sẵn.

---

## Kết hợp Tất Cả – Ví dụ Đầy Đủ, Có Thể Chạy



## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tự động Định dạng Có Điều kiện trong Excel bằng Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Cách triển khai Cài đặt Font tùy chỉnh trong Aspose.Cells Java cho Định dạng Excel](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Đặt Kích thước Font trong Excel bằng Aspose.Cells Java - Hướng Dẫn Toàn Diện](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}