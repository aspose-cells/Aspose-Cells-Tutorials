---
category: general
date: 2026-06-27
description: Tìm hiểu cách nhập DataTable vào Excel với các cột màu xen kẽ. Hướng
  dẫn từng bước về việc nhập dữ liệu kèm định dạng và thiết lập màu chữ cho cột bằng
  Java.
draft: false
keywords:
- alternating column colors
- import data with formatting
- import datatable to excel
- set column font color
- how to import datatable
language: vi
og_description: Làm chủ việc tạo màu cột xen kẽ khi nhập DataTable vào Excel. Hướng
  dẫn này chỉ cách nhập dữ liệu có định dạng và đặt màu phông chữ cho cột trong Java.
og_title: Màu cột xen kẽ trong Excel – Nhập DataTable với định dạng
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  headline: Alternating Column Colors in Excel – Import DataTable with Formatting
  type: TechArticle
- description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  name: Alternating Column Colors in Excel – Import DataTable with Formatting
  steps:
  - name: Prerequisites
    text: '- Java 8+ (the code works with newer releases as well). - Apache POI 5.x
      on your classpath – the library that talks to Excel files. - A `DataTable` implementation
      that offers `getColumns()` and `size()` (or adapt the example to a `ResultSet`).'
  - name: – Obtain the DataTable You Want to Export
    text: First, you need a source of rows and columns. In real projects this might
      be a database query, a CSV parser, or an in‑memory collection. The example assumes
      a helper method `getDataTable()` that returns a ready‑to‑use `DataTable`.
  - name: – Prepare a Style for Each Column
    text: We create a `Style[]` whose length matches the number of columns. Each entry
      will hold a font color that alternates between blue and green.
  - name: – Create Styles with Alternating Font Colors
    text: 'Now the fun part: loop through the array and assign a blue font to even‑indexed
      columns and a green font to odd‑indexed ones. This is where **alternating column
      colors** is implemented.'
  - name: – Import the DataTable with the Style Array
    text: Finally, we hand the `DataTable` and the `columnStyles` array to POI’s `importDataTable`
      method. The `true` flag tells POI to treat the first row as column headers.
  - name: – Save the Workbook (Optional but Recommended)
    text: After the import, you’ll probably want to write the workbook to disk or
      stream it to a client.
  type: HowTo
- questions:
  - answer: Replace `setFontColor` with `setPatternForegroundColor` and call `setPattern(BackgroundType.SOLID)`
      on the style.
    question: What if I need background colors instead of font colors?
  - answer: 'Absolutely—just swap the loop logic: iterate over rows and assign a style
      per row index.'
    question: Can I apply the same color scheme to rows instead of columns?
  - answer: Excel caps at 16,384 columns (XFD). The code will throw an exception once
      you exceed that limit. Guard against it by checking `columnCount` against `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.
    question: What if the DataTable has more columns than the worksheet can handle?
  - answer: Yes, POI abstracts the format. However, the older binary format supports
      fewer colors, so you might see a fallback to the nearest palette entry.
    question: Does this work with .xls (Excel 97‑2003) files?
  type: FAQPage
tags:
- excel
- java
- datatable
- formatting
- apache-poi
title: Màu cột xen kẽ trong Excel – Nhập DataTable với định dạng
url: /vi/java/excel-import-export/alternating-column-colors-in-excel-import-datatable-with-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Màu Cột Xen Kẽ trong Excel – Nhập DataTable với Định Dạng

Bạn đã bao giờ tự hỏi làm sao để làm cho file Excel xuất ra của mình thêm phần bắt mắt mà không rời khỏi code? **Màu cột xen kẽ** là cách nhanh chóng giúp các bảng lớn dễ đọc hơn, và bạn có thể thực hiện điều này khi **import datatable to excel**. Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp Java hoàn chỉnh, không chỉ đưa dữ liệu của bạn vào worksheet mà còn áp dụng mẫu màu chữ xanh‑xanh cho từng cột.

Bạn sẽ thấy cách **import data with formatting**, đặt màu chữ cho mỗi cột, và trả lời câu hỏi “**how to import datatable**” một cách triệt để. Không cần công cụ bên ngoài, chỉ cần Java thuần và một thư viện bảng tính phổ biến.

## What You’ll Build

Kết thúc hướng dẫn này, bạn sẽ có một đoạn mã Java có thể chạy được, thực hiện:

1. Lấy một `DataTable` (hoặc bất kỳ collection kiểu `ResultSet` nào).  
2. Tạo một mảng `Style` trong đó các cột chẵn có màu xanh và các cột lẻ có màu xanh lá.  
3. Gọi `importDataTable` để đưa dữ liệu vào ô **A1** đồng thời áp dụng các style.  

Tất cả chỉ trong vài dòng code, nhưng kết quả trông như một báo cáo được thiết kế tỉ mỉ.

### Prerequisites

- Java 8+ (code cũng hoạt động với các phiên bản mới hơn).  
- Apache POI 5.x trên classpath – thư viện giao tiếp với file Excel.  
- Một triển khai `DataTable` cung cấp `getColumns()` và `size()` (hoặc điều chỉnh ví dụ cho `ResultSet`).  

Nếu bạn đã dùng POI cho các tác vụ Excel khác, bạn có thể chèn đoạn này ngay.

---

## Alternating Column Colors While Importing DataTable to Excel

Trái tim của giải pháp nằm trong bốn bước ngắn gọn. Hãy cùng phân tích.

### Step 1 – Obtain the DataTable You Want to Export

Đầu tiên, bạn cần một nguồn dữ liệu gồm các hàng và cột. Trong dự án thực tế, đây có thể là truy vấn cơ sở dữ liệu, trình phân tích CSV, hoặc một collection trong bộ nhớ. Ví dụ giả định có một phương thức trợ giúp `getDataTable()` trả về một `DataTable` đã sẵn sàng.

```java
// Step 1: Obtain the data to be imported
DataTable dataTable = getDataTable();   // your own method that fills the table
```

> **Why this matters:**  
> Lấy dữ liệu trước giúp bạn kiểm tra số lượng cột, từ đó xác định kích thước mảng style sau này. Nó cũng đảm bảo bước nhập có một đối tượng cụ thể để làm việc.

### Step 2 – Prepare a Style for Each Column

Chúng ta tạo một `Style[]` có độ dài bằng số cột. Mỗi phần tử sẽ chứa một màu chữ xen kẽ giữa xanh và xanh lá.

```java
// Step 2: Prepare a style for each column (same count as the number of columns)
int columnCount = dataTable.getColumns().size();
Style[] columnStyles = new Style[columnCount];
```

> **Pro tip:** Nếu `DataTable` của bạn có thể thay đổi cấu trúc tại thời gian chạy, hãy tính lại `columnCount` mỗi khi xuất. Điều này ngăn `ArrayIndexOutOfBoundsException`.

### Step 3 – Create Styles with Alternating Font Colors

Bây giờ là phần thú vị: lặp qua mảng và gán font màu xanh cho các cột có chỉ số chẵn, và màu xanh lá cho các cột có chỉ số lẻ. Đây là nơi **alternating column colors** được thực hiện.

```java
// Step 3: Create styles with alternating font colors for visual distinction
for (int i = 0; i < columnStyles.length; i++) {
    columnStyles[i] = workbook.createStyle();               // create a fresh style
    // Even columns → blue, odd columns → green
    columnStyles[i].setFontColor(
        (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
    );
}
```

> **Why alternating colors?**  
> Mắt người đọc sẽ quét các hàng dễ dàng hơn khi các cột liền kề nổi bật. Nhịp điệu xanh‑xanh giảm mỏi mắt, đặc biệt với các bảng rộng.

### Step 4 – Import the DataTable with the Style Array

Cuối cùng, chúng ta truyền `DataTable` và mảng `columnStyles` cho phương thức `importDataTable` của POI. Tham số `true` báo cho POI coi hàng đầu tiên là tiêu đề cột.

```java
// Step 4: Import the data table into the worksheet starting at cell A1, applying the styles
worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);
```

> **What happens under the hood?**  
> POI duyệt qua từng cột, lấy `Style` tương ứng từ mảng, và ghi mỗi ô bằng style đó. Vì chúng ta chỉ đặt màu chữ, các khía cạnh khác (đường viền, nền) vẫn giữ mặc định — bạn có thể mở rộng style nếu muốn thêm hiệu ứng.

### Step 5 – Save the Workbook (Optional but Recommended)

Sau khi nhập, bạn có thể muốn ghi workbook ra đĩa hoặc stream tới client.

```java
// Optional: write the workbook to a file
try (FileOutputStream fos = new FileOutputStream("ExportedReport.xlsx")) {
    workbook.save(fos);
}
```

> **Edge case:** Nếu file đích đã tồn tại, `FileOutputStream` sẽ ghi đè. Hãy bọc lệnh này trong một kiểm tra hoặc yêu cầu người dùng xác nhận trong ngữ cảnh UI.

---

## Common Questions & Gotchas

- **What if I need background colors instead of font colors?**  
  Thay `setFontColor` bằng `setPatternForegroundColor` và gọi `setPattern(BackgroundType.SOLID)` trên style.

- **Can I apply the same color scheme to rows instead of columns?**  
  Chắc chắn — chỉ cần đổi logic vòng lặp: duyệt qua các hàng và gán style theo chỉ số hàng.

- **What if the DataTable has more columns than the worksheet can handle?**  
  Excel giới hạn tối đa 16.384 cột (XFD). Code sẽ ném ngoại lệ khi vượt quá giới hạn này. Hãy kiểm tra `columnCount` so với `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.

- **Does this work with .xls (Excel 97‑2003) files?**  
  Có, POI trừu tượng hoá định dạng. Tuy nhiên, định dạng nhị phân cũ hỗ trợ ít màu hơn, vì vậy bạn có thể thấy màu được thay thế bằng màu gần nhất trong bảng màu.

---

## Full Working Example

Dưới đây là một lớp tự chứa mà bạn có thể dán vào dự án Maven đã có `org.apache.poi:poi-ooxml:5.2.3`. Điều chỉnh `getDataTable()` để trả về nguồn dữ liệu thực tế của bạn.

```java
import com.aspose.cells.*;
import java.io.FileOutputStream;

public class ExcelAlternatingColorsExport {

    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 1️⃣ Obtain the data to be imported
        DataTable dataTable = getDataTable(); // implement this method

        // 2️⃣ Prepare a style for each column
        int columnCount = dataTable.getColumns().size();
        Style[] columnStyles = new Style[columnCount];

        // 3️⃣ Create alternating font colors (blue for even, green for odd)
        for (int i = 0; i < columnStyles.length; i++) {
            columnStyles[i] = workbook.createStyle();
            columnStyles[i].setFontColor(
                (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
            );
        }

        // 4️⃣ Import the data with formatting
        worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);

        // 5️⃣ Save the file
        try (FileOutputStream fos = new FileOutputStream("AlternatingColorsReport.xlsx")) {
            workbook.save(fos);
        }

        System.out.println("Export complete – open AlternatingColorsReport.xlsx to see the result.");
    }

    // Dummy implementation – replace with real data retrieval
    private static DataTable getDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID");
        dt.getColumns().add("Name");
        dt.getColumns().add("Score");
        dt.getRows().add(new DataRow(new Object[]{1, "Alice", 85}));
        dt.getRows().add(new DataRow(new Object[]{2, "Bob", 92}));
        dt.getRows().add(new DataRow(new Object[]{3, "Carol", 78}));
        return dt;
    }
}
```

**Expected output:** Mở `AlternatingColorsReport.xlsx`. Cột A và C (chỉ số chẵn) hiển thị văn bản màu xanh, trong khi cột B (chỉ số lẻ) hiển thị màu xanh lá. Hàng đầu tiên được in đậm làm tiêu đề vì `importDataTable` xử lý nó như vậy.

---

## Conclusion

Chúng ta vừa bao quát mọi thứ bạn cần để **import datatable to excel** đồng thời áp dụng **alternating column colors** và **set column font color** một cách lập trình. Cách tiếp cận nhẹ, chỉ dựa vào Apache POI, và có thể mở rộng cho các nhu cầu định dạng khác như viền hoặc nền ô.

Tiếp theo, bạn có thể thử:

- **Import data with formatting** cho các hàng (màu hàng xen kẽ).  
- Thêm **conditional formatting** để làm nổi bật các điểm cao.  
- Xuất trực tiếp tới phản hồi HTTP cho các ứng dụng web.

Hãy tự do điều chỉnh mẫu này cho quy trình báo cáo của mình — một khi đã nắm vững nền tảng, khả năng mở rộng là vô hạn. Chúc bạn coding vui!

## What Should You Learn Next?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Sort Excel Data by Column Color Using Aspose.Cells Java: A Complete Guide](/cells/english/java/formatting/sort-excel-data-by-column-color-aspose-cells-java/)
- [Master Excel Column Protection Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/security-protection/excel-column-protection-aspose-cells-java/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}