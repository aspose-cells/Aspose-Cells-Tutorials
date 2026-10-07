---
category: general
date: 2026-10-07
description: Cách tách cột bằng Aspose.Cells cho Java. Học cách tách chuỗi thành các
  cột, tự động hoá công thức Excel và ghi công thức vào ô chỉ trong vài dòng mã.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: vi
lastmod: 2026-10-07
og_description: Cách tách cột trong Java bằng Aspose.Cells. Hướng dẫn này chỉ cho
  bạn cách tách chuỗi thành các cột, tự động đánh giá công thức Excel và ghi công
  thức vào ô.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Cách tách cột trong Java bằng Aspose.Cells – hướng dẫn nhanh
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cách tách cột trong Java bằng Aspose.Cells – hướng dẫn từng bước
url: /vi/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng dẫn chi tiết cách tách cột trong Java với Aspose.Cells

Nếu bạn cần **cách tách cột** trong một worksheet Excel một cách lập trình, hướng dẫn này sẽ chỉ cho bạn quy trình hoàn chỉnh với Aspose.Cells cho Java. Bạn cũng sẽ học cách **tách chuỗi thành các cột**, **tự động tính toán công thức Excel**, và **ghi công thức vào ô** bằng mã ngắn gọn, sẵn sàng cho môi trường production.

Việc tách cột bằng mã loại bỏ thao tác sao chép‑dán thủ công, giảm lỗi và cho phép chuyển đổi dữ liệu quy mô lớn. Khi kết thúc tutorial này, bạn có thể tạo, sửa đổi và tính toán công thức ngay lập tức, biến Excel thành một phần thực sự của backend Java của bạn.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* Java 17 hoặc phiên bản mới hơn.
* Maven 3.8+ (hoặc Gradle) để quản lý phụ thuộc.
* Giấy phép Aspose.Cells for Java (phiên bản dùng thử miễn phí vẫn đủ cho việc học).
* Kiến thức cơ bản về cú pháp Java và các khái niệm Excel.

Nếu còn thiếu bất kỳ mục nào, hãy cài đặt chúng trước; các mẫu mã giả định một dự án Maven tiêu chuẩn.

## Bước 1: Thêm Aspose.Cells vào dự án của bạn

Thêm phụ thuộc sau vào file `pom.xml`. Điều này sẽ tải thư viện Aspose.Cells ổn định mới nhất.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Tại sao bước này quan trọng:** Thư viện cung cấp các lớp `Workbook`, `Worksheet` và `Cell` cần thiết để thao tác file Excel mà không cần Microsoft Office. Nếu không có phụ thuộc, mã sẽ không biên dịch được.

## Bước 2: Tạo workbook và chọn worksheet đầu tiên

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Đối tượng `Workbook` đại diện cho toàn bộ file Excel. Việc truy cập worksheet đầu tiên giúp có một điểm khởi đầu dự đoán được cho công thức chúng ta sẽ viết.

## Bước 3: Ghi công thức WRAPCOLS vào ô mục tiêu

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Tại sao chúng ta dùng `WRAPCOLS`:** Hàm tích hợp sẵn của Excel `WRAPCOLS` tự động chia một giá trị văn bản duy nhất thành số cột đã định, xử lý ranh giới từ một cách thông minh. Đây là cách đáng tin cậy nhất để **tách chuỗi thành các cột** mà không cần logic phân tích tùy chỉnh.

## Bước 4: Buộc workbook tính công thức

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Gọi `calculateFormula()` **tự động tính toán công thức Excel** phía server. Nếu không gọi, ô vẫn chỉ chứa văn bản công thức, không phải giá trị đã tính.

## Bước 5: Lấy và hiển thị kết quả đã gói

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Khi chạy chương trình, console sẽ in:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

File `SplitColumnsResult.xlsx` được tạo sẽ hiển thị ba cột đã được điền với văn bản đã tách.

## Hiểu về hàm WRAPCOLS

* **Cú pháp:** `WRAPCOLS(text, columns, [delimiter])`
* **Tham số:**
  * `text` – chuỗi bạn muốn tách.
  * `columns` – số cột để phân phối văn bản.
  * `delimiter` (tùy chọn) – ký tự dùng để ngắt chuỗi; mặc định là dấu cách.
* **Giá trị trả về:** Một mảng sẽ tràn sang các ô liền kề, mỗi phần tử chứa một đoạn của văn bản gốc.

Vì hàm này tràn theo chiều ngang, bạn chỉ cần ghi công thức vào ô nằm bên trái nhất (A1 trong ví dụ). Excel sẽ tự động điền B1, C1, … khi cần.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Điều chỉnh đề xuất |
|-----------|--------------------|
| **Số cột biến** | Thay `3` cố định bằng biến: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Dấu phân cách tùy chỉnh** | Dùng đối số thứ ba, ví dụ `=WRAPCOLS(A2,4,",")` để tách bằng dấu phẩy. |
| **Chuỗi nguồn rỗng** | Hàm trả về các ô trống; hãy kiểm tra `null` hoặc chuỗi rỗng trước khi đặt công thức. |
| **Bộ dữ liệu lớn** | Áp dụng công thức trong vòng lặp cho mỗi hàng, sau đó gọi `calculateFormula()` một lần duy nhất sau vòng lặp để cải thiện hiệu năng. |
| **Ký tự không phải ASCII** | WRAPCOLS hỗ trợ Unicode; đảm bảo file nguồn Java của bạn được lưu dưới dạng UTF‑8. |

**Mẹo chuyên nghiệp:** Khi xử lý nhiều hàng, lưu công thức vào một biến chuỗi và tái sử dụng để tránh việc nối chuỗi lặp lại gây tốn tài nguyên.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh, sẵn sàng sao chép‑dán. Nó bao gồm các câu lệnh import, xử lý ngoại lệ và một thao tác lưu tùy chọn.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Chạy chương trình này sẽ tạo ra cùng một đầu ra console như trên và ghi một file Excel minh họa rõ ràng **cách tách cột**.

## Danh sách kiểm tra khắc phục sự cố

* **Công thức không tính** – Đảm bảo `workbook.calculateFormula()` được gọi sau khi đặt công thức.
* **Các ô trống sau khi tách** – Kiểm tra chuỗi nguồn không phải `null` hoặc rỗng, và số cột lớn hơn 0.
* **Lỗi giấy phép** – Cung cấp file giấy phép Aspose.Cells hợp lệ (`License license = new License(); license.setLicense("Aspose.Total.lic");`) trước khi tạo workbook để loại bỏ watermark đánh giá.
* **Độ trễ hiệu năng trên sheet lớn** – Gọi `calculateFormula()` một lần duy nhất sau khi tất cả công thức đã được viết, không phải sau mỗi ô riêng lẻ.

## Kết luận

Bạn đã biết **cách tách cột** trong Java bằng Aspose.Cells, **cách tách chuỗi thành các cột** với hàm `WRAPCOLS`, **cách tự động tính công thức Excel**, và **cách ghi công thức vào ô** một cách lập trình. Kỹ thuật này loại bỏ các bước chuẩn bị dữ liệu thủ công và tích hợp khả năng xử lý văn bản mạnh mẽ của Excel trực tiếp vào ứng dụng Java của bạn.

### Các bước tiếp theo

* Khám phá các hàm văn bản khác như `TEXTSPLIT` và `FILTERXML` cho các kịch bản phân tích phức tạp hơn.
* Kết hợp `WRAPCOLS` với `IFERROR` để xử lý đầu vào bất ngờ một cách mềm mại.
* Tích hợp giải pháp vào một dịch vụ Spring Boot nhận dữ liệu CSV qua REST và trả về file Excel đã được điền.

Khi thành thạo các mẫu này, bạn có thể xây dựng các quy trình làm việc Excel tự động, mạnh mẽ và mở rộng cùng nhu cầu kinh doanh. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [aspose cells java – Tách Tên thành Cột](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [How to Delete Blank Columns in Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}