---
category: general
date: 2026-06-18
description: Tạo hướng dẫn Java tạo file Excel, trình bày cách đặt màu nền cho hàng,
  tạo Excel từ DataTable và lưu workbook dưới dạng XLSX với việc tô màu xen kẽ các
  hàng.
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: vi
og_description: Tạo tệp Excel bằng Java từng bước. Học cách đặt màu nền cho hàng,
  áp dụng tô màu xen kẽ cho các hàng, tạo Excel từ DataTable và lưu sổ làm việc dưới
  dạng XLSX.
og_title: Tạo tệp Excel bằng Java – Hướng dẫn toàn diện về định dạng và xuất
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: Tạo file Excel bằng Java – Hướng dẫn toàn diện với định dạng hàng và xuất XLSX
url: /vi/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo File Excel Java – Hướng Dẫn Toàn Diện với Định Dạng Hàng và Xuất XLSX

Bạn đã bao giờ tự hỏi làm thế nào để **create excel file java** trông chuyên nghiệp ngay từ đầu chưa? Bạn không đơn độc—các nhà phát triển thường cần một cách nhanh chóng để biến dữ liệu dạng bảng thành một bảng tính được định dạng đẹp mà không phải mở Excel thủ công. Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh: lấy dữ liệu từ một `DataTable`, áp dụng **alternating row shading excel**, và cuối cùng **save workbook as xlsx**. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ dự án Java nào.

Chúng tôi sẽ bao phủ mọi thứ bạn cần: thư viện bắt buộc (Aspose.Cells for Java), đoạn mã chính xác để **set row background color**, cách **generate excel from datatable**, và một vài mẹo thực tế để tránh những lỗi thường gặp. Không có phần thừa, chỉ có một ví dụ sẵn sàng chạy mà bạn có thể điều chỉnh ngay hôm nay.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- Java 17 hoặc mới hơn (mã chạy được với bất kỳ JDK gần đây nào)
- Maven hoặc Gradle để quản lý phụ thuộc
- Kiến thức cơ bản về các collection trong Java
- Quyền truy cập vào thư viện Aspose.Cells for Java (bản dùng thử miễn phí hoặc phiên bản có giấy phép)

Nếu bạn muốn một giải pháp mã nguồn mở, logic này có thể dễ dàng chuyển sang Apache POI—chỉ cần thay đổi các lời gọi API. Để ngắn gọn, chúng tôi sẽ dùng Aspose.Cells vì phương thức `importDataTable` của nó làm cho bước **generate excel from datatable** trở thành một dòng lệnh.

## Step 1: Set Up the Project and Add Aspose.Cells

Thêm phụ thuộc sau vào file `pom.xml` (Maven) hoặc `build.gradle` (Gradle). Điều này sẽ tải thư viện cốt lõi cho phép chúng ta thao tác với workbook, style và màu sắc.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

Sau khi làm mới dự án, bạn đã sẵn sàng viết mã Java theo phong cách **create excel file java**.

## Step 2: Create the Workbook and Load Your Data

Đầu tiên chúng ta khởi tạo một `Workbook` mới. Sau đó chúng ta lấy một `DataTable`—điều này có thể là kết quả của một truy vấn JDBC, một trình phân tích CSV, hoặc bất kỳ bảng dữ liệu trong bộ nhớ nào bạn đã có.

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

Tại thời điểm này chúng ta có một workbook sạch và một `DataTable` đã được điền dữ liệu. Bước tiếp theo là nơi phép màu về hình ảnh xảy ra.

## Step 3: Define Row Styles – Setting Row Background Color

Chúng ta muốn mỗi hàng có một nền riêng, xen kẽ giữa màu xanh nhạt và màu xám nhạt. Điều này cải thiện khả năng đọc, đặc biệt với các báo cáo lớn. Đoạn mã dưới tạo một mảng `Style`—một phần tử cho mỗi hàng dữ liệu—and assigns a **set row background color** dựa trên chỉ số hàng.

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

Lưu ý cách chúng ta sử dụng `Color.getLightBlue()` và `Color.getLightGray()`. Aspose.Cells cung cấp một bảng màu phong phú, nhưng bạn có thể thay thế các lời gọi này bằng bất kỳ `Color` nào bạn muốn—có thể là màu thương hiệu công ty của bạn.

## Step 4: Import the DataTable with Styling

Bây giờ chúng ta kết hợp dữ liệu và mảng style lại với nhau. Phương thức `importDataTable` chịu trách nhiệm sao chép các hàng, áp dụng style tương ứng, và thậm chí thêm tiêu đề cột nếu bạn truyền `true` cho tham số `importColumnNames`.

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

Anchor `"A1"` cho Aspose biết bắt đầu ghi ở đâu—góc trên‑trái của sheet. Vì chúng ta đã cung cấp mảng `rowStyles`, mỗi hàng sẽ kế thừa màu nền mà chúng ta đã đặt trước, đạt được **alternating row shading excel** mà không cần vòng lặp sau khi import.

## Step 5: Save the Styled Workbook as XLSX

Cuối cùng, chúng ta lưu workbook xuống đĩa. Phương thức `save` tự động xác định định dạng dựa trên phần mở rộng file, vì vậy sử dụng `.xlsx` sẽ cho chúng ta một workbook Office Open XML hiện đại có thể mở trong Excel, Google Sheets, hoặc LibreOffice.

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

Chạy phương thức `main` sẽ tạo ra một file có tên `styledTable.xlsx` trong thư mục gốc của dự án. Mở nó lên, và bạn sẽ thấy một bảng được định dạng gọn gàng với các màu nền xen kẽ—đúng như những gì các bên liên quan kinh doanh mong đợi từ một báo cáo.

![Screenshot of styled Excel file created with Java](images/styled_excel_java.png "ví dụ tạo excel file java")

*Image alt text:* **create excel file java** screenshot showing alternating row shading

## Why This Approach Works Better Than Manual Cell‑by‑Cell Styling

Bạn có thể tự hỏi tại sao chúng ta lại dùng mảng style thay vì lặp qua từng hàng sau khi import. Câu trả lời có hai phần:

1. **Performance** – Áp dụng style trong quá trình import tránh một lượt duyệt thêm trên worksheet, điều này có thể tốn kém khi xử lý hàng ngàn dòng.
2. **Maintainability** – Logic style nằm trong một nơi duy nhất (`rowStyles`), giúp dễ dàng thay đổi màu, thêm viền, hoặc thay đổi mẫu mà không cần chạm vào mã import.

Nếu sau này bạn cần thêm các dấu hiệu trực quan (ví dụ: làm nổi bật các hàng có điểm dưới một ngưỡng), chỉ cần mở rộng khối `if` bên trong vòng lặp—không cần thay đổi gì khác.

## Common Variations and Edge Cases

### Exporting a Large DataTable

Khi làm việc với hơn 100k dòng, bạn có thể gặp giới hạn bộ nhớ. Aspose.Cells hỗ trợ chế độ **streaming**:

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

Đặt tùy chọn bộ nhớ trước khi tạo style, và thư viện sẽ ghi dữ liệu vào các file tạm thay vì giữ toàn bộ trong RAM.

### Using Apache POI Instead of Aspose.Cells

Nếu vấn đề giấy phép là mối quan tâm, bạn có thể thay thế logic import bằng các đối tượng `CellStyle` của POI. Khái niệm vẫn giữ nguyên: tạo hai `CellStyle`, lặp qua các hàng, và áp dụng `setFillForegroundColor` với `IndexedColors`. Nhược điểm duy nhất là mã sẽ hơi dài hơn.

### Adding Conditional Formatting

Giả sử bạn muốn làm nổi bật bất kỳ điểm nào trên 90 bằng màu xanh lá. Thêm đoạn này sau khi import:

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

Bây giờ worksheet không chỉ có shading xen kẽ mà còn có các highlight động.

## Recap: What We Accomplished

- **Create excel file java** từ một `DataTable` bằng Aspose.Cells.
- **Set row background color** một cách lập trình, đạt được **alternating row shading excel**.
- **Save workbook as xlsx**, đảm bảo tương thích với các công cụ bảng tính hiện đại.
- Thể hiện cách **generate excel from datatable** một cách hiệu quả và mở rộng.

Tất cả những điều này được gói gọn trong một lớp Java ngắn gọn, dễ đọc mà bạn có thể sao chép‑dán vào codebase của mình.

## Next Steps and Related Topics

Nếu bạn thích walkthrough này, bạn cũng có thể khám phá:

- **Exporting charts** từ Java sang Excel (API chart của Aspose.Cells).
- **Password‑protecting** workbook đã tạo (`workbook.protect(...)`).
- **Writing large datasets** với streaming để giữ mức sử dụng bộ nhớ thấp.
- **Integrating with Spring Boot** để phục vụ file đã tạo dưới dạng phản hồi tải xuống.

Mỗi chủ đề trên đều dựa trên nền tảng chúng ta đã xây dựng ở đây—vì vậy hãy tự do thử nghiệm và mở rộng.

---

*Happy coding! Nếu bạn gặp bất kỳ khó khăn nào hoặc có ý tưởng cải tiến, hãy để lại bình luận bên dưới. Hãy cùng nhau duy trì cuộc trò chuyện.*


## What Should You Learn Next?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ hoạt động cùng các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Set Excel Row Heights Using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}