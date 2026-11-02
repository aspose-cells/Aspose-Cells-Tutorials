---
category: general
date: 2026-06-18
description: Đặt định dạng số trong Excel bằng Java, học cách sử dụng ký hiệu khoa
  học trong Java, ghi giá trị vào ô, thiết lập số chữ số có ý nghĩa và xuất dữ liệu
  ra file xlsx trong vài phút.
draft: false
keywords:
- set number format excel
- scientific notation java
- write value to cell
- set significant digits
- export data to xlsx
language: vi
og_description: Đặt định dạng số Excel bằng Java. Tìm hiểu cách sử dụng ký hiệu khoa
  học trong Java, ghi giá trị vào ô, thiết lập số chữ số có nghĩa và xuất dữ liệu
  ra tệp xlsx một cách hiệu quả.
og_title: Đặt Định Dạng Số Excel trong Java – Hướng Dẫn Từng Bước
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  headline: Set Number Format Excel in Java – Complete Guide
  type: TechArticle
- description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  name: Set Number Format Excel in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '| A (Formatted) | |---------------| | 1.235E7 |'
  - name: How do I change the number of significant digits?
    text: Just edit the format string. For three digits use `"0.###E0"`; for six digits
      use `"0.######E0"`.
  - name: What if I need a different locale (comma as decimal separator)?
    text: Add a locale‑aware format, e.g., `df.getFormat("0,####E0")`. Excel respects
      the user’s regional settings, so the comma will appear only if the workbook
      is opened on a system that uses it.
  - name: Can I apply the same style to an entire column?
    text: Absolutely. Create the style once (as shown) and then loop through rows,
      applying `cell.setCellStyle(sciStyle)` each time. For large sheets, consider
      using `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – it’s faster and
      keeps the code tidy.
  - name: What if I’m stuck with an older Java version that doesn’t support `var`?
    text: Replace `var` with the explicit type (`Workbook workbook = new XSSFWorkbook();`).
      The rest of the code stays identical.
  type: HowTo
tags:
- Java
- Excel
- Data Export
title: Đặt Định Dạng Số Excel trong Java – Hướng Dẫn Toàn Diện
url: /vi/java/formatting/set-number-format-excel-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Định Dạng Số Excel trong Java – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi làm thế nào để **set number format Excel** từ một chương trình Java mà không phải rối rắm? Bạn không phải là người duy nhất. Dù bạn đang tạo các báo cáo tài chính hay xuất dữ liệu cảm biến, việc hiển thị những con số lớn một cách đẹp mắt trong tệp *.xlsx* là một kỹ năng cần thiết.

Trong hướng dẫn này, chúng ta sẽ đi qua một giải pháp thực tế, từ đầu đến cuối: tạo workbook, cấu hình **scientific notation java**, giới hạn **set significant digits**, ghi một giá trị vào ô, và cuối cùng **export data to xlsx**. Khi kết thúc, bạn sẽ có một đoạn mã tự chứa có thể chèn ngay vào dự án của mình.

## Những Điều Bạn Sẽ Học

- Cách khởi tạo một workbook bằng JExcel‑API (hoặc Apache POI) trong Java.  
- Các lệnh chính xác để **set number format excel** buộc hiển thị dạng khoa học.  
- Cách **write value to cell** đồng thời giữ độ chính xác.  
- Điều chỉnh cài đặt của workbook để **set significant digits** thành số tùy chỉnh.  
- Lưu tệp để có thể mở trong bất kỳ ứng dụng bảng tính hiện đại nào (**export data to xlsx**).  

Không có dịch vụ bên ngoài, không có phép màu. Chỉ là Java thuần và một vài lớp được tài liệu hoá tốt.

---

## Yêu Cầu Trước

- JDK 17 hoặc mới hơn (mã vẫn chạy trên các phiên bản cũ hơn, nhưng các ví dụ sử dụng cú pháp `var` hiện đại để ngắn gọn).  
- Maven hoặc Gradle để kéo vào phụ thuộc `org.apache.poi:poi-ooxml`.  
- Kiến thức cơ bản về các collection trong Java – nếu bạn đã viết một vòng lặp `for` trước đây, bạn đã ổn.

---

## Bước 1: Thêm Phụ Thuộc Apache POI

Nếu bạn đang dùng Maven, dán đoạn này vào file `pom.xml` của bạn. Người dùng Gradle có thể chuyển nó sang cú pháp `implementation`.

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

> **Mẹo:** Giữ POI luôn cập nhật. Nhánh 5.x cung cấp hỗ trợ tốt hơn cho định dạng số và các bảng tính lớn.

---

## Bước 2: Tạo Workbook và Truy Cập Cài Đặt  

Điều đầu tiên chúng ta cần là một đối tượng workbook mới. Apache POI không cung cấp lớp `WorkbookSettings` như JExcel, nhưng chúng ta có thể đạt được hiệu quả tương tự bằng cách tạo một `CellStyle` sau này.

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise a new workbook (this is where we "set number format excel")
        Workbook workbook = new XSSFWorkbook();   // XSSFWorkbook -> .xlsx format
        // No explicit WorkbookSettings, we'll configure a CellStyle later
```

Tại sao chúng ta bắt đầu với một **new workbook**? Hãy nghĩ nó như một tấm vải trống; mọi quyết định định dạng chúng ta thực hiện sau sẽ được áp dụng lên tấm vải này.  

---

## Bước 3: Định Nghĩa CellStyle cho Định Dạng Khoa Học và Số Chữ Số Đáng Kể  

Apache POI cho phép bạn tạo một chuỗi định dạng dữ liệu. Để áp dụng **scientific notation java** và giới hạn số chữ số, chúng ta sử dụng mẫu `"0.####E0"` – các ký tự `#` kiểm soát số chữ số đáng kể sẽ hiển thị.

```java
import org.apache.poi.ss.usermodel.CellStyle;
import org.apache.poi.ss.usermodel.DataFormat;

// Inside main(), after workbook creation:
DataFormat df = workbook.createDataFormat();
CellStyle sciStyle = workbook.createCellStyle();

// "0.####E0" -> 0 before the decimal, up to 4 significant digits after, exponent part
sciStyle.setDataFormat(df.getFormat("0.####E0"));
```

*Điều gì đang xảy ra ở đây?* Định dạng này nói với Excel: “Hiển thị số ở dạng khoa học, nhưng chỉ giữ tối đa bốn chữ số đáng kể.” Nếu bạn cần độ chính xác khác, chỉ cần thêm hoặc bớt các ký tự `#`.  

---

## Bước 4: Ghi Một Số Lớn Vào Ô  

Bây giờ chúng ta sẽ **write value to cell** *A1* bằng kiểu chúng ta vừa tạo. Các đối tượng `Sheet` và `Row` nhẹ, vì vậy việc tạo chúng ngay lập tức là rẻ tiền.

```java
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Cell;

// Continue inside main():
Sheet sheet = workbook.createSheet("Numbers");

// Row 0 (first row), Cell 0 (column A)
Row row = sheet.createRow(0);
Cell cell = row.createCell(0);
cell.setCellValue(12345678.9);   // The raw value we want to store
cell.setCellStyle(sciStyle);    // Apply our scientific notation style
```

Lưu ý chúng ta không cần ép kiểu số; POI tự động xử lý `double`. Khi gắn `sciStyle`, chúng ta đảm bảo rằng khi người dùng mở tệp, Excel sẽ hiển thị `1.235E7` (làm tròn tới bốn chữ số đáng kể) thay vì chuỗi thô 8 chữ số.  

---

## Bước 5: Lưu Workbook – Export Data to XLSX  

Bước cuối cùng là **export data to xlsx**. Chúng ta sẽ ghi workbook vào một tệp trong thư mục hiện tại, nhưng bạn có thể chỉ định bất kỳ vị trí nào bạn muốn.

```java
import java.io.FileOutputStream;

// Still inside main():
try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
    workbook.write(out);
}
workbook.close();   // Free resources
System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Khi bạn nhấp đúp vào `sigDigits.xlsx`, bạn sẽ thấy cột **A** hiển thị `1.235E7` – chính xác như chúng ta yêu cầu.

### Kết Quả Mong Đợi

| A (Formatted) |
|---------------|
| 1.235E7       |

Nếu bạn mở tệp và thay đổi định dạng ô thủ công, bạn sẽ thấy giá trị gốc vẫn là `12345678.9`. Đó là phép màu của **set number format excel**: hiển thị thay đổi, dữ liệu vẫn nguyên vẹn.

---

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Làm sao để thay đổi số chữ số đáng kể?

Chỉ cần chỉnh sửa chuỗi định dạng. Đối với ba chữ số dùng `"0.###E0"`; đối với sáu chữ số dùng `"0.######E0"`.

### Nếu tôi cần một locale khác (dấu phẩy làm dấu thập phân) thì sao?

Thêm định dạng có hỗ trợ locale, ví dụ `df.getFormat("0,####E0")`. Excel sẽ tôn trọng cài đặt khu vực của người dùng, vì vậy dấu phẩy sẽ xuất hiện chỉ khi workbook được mở trên hệ thống sử dụng dấu phẩy.

### Tôi có thể áp dụng cùng một style cho toàn bộ cột không?

Chắc chắn. Tạo style một lần (như đã minh họa) rồi lặp qua các hàng, áp dụng `cell.setCellStyle(sciStyle)` mỗi lần. Đối với các sheet lớn, cân nhắc dùng `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – nhanh hơn và giữ code gọn gàng.

### Nếu tôi bị kẹt với phiên bản Java cũ không hỗ trợ `var` thì sao?

Thay `var` bằng kiểu rõ ràng (`Workbook workbook = new XSSFWorkbook();`). Phần còn lại của mã vẫn giống nhau.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.*;

import java.io.FileOutputStream;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (set number format excel)
        Workbook workbook = new XSSFWorkbook();

        // Define a style for scientific notation with 4 significant digits
        DataFormat df = workbook.createDataFormat();
        CellStyle sciStyle = workbook.createCellStyle();
        sciStyle.setDataFormat(df.getFormat("0.####E0")); // set significant digits

        // Access the first worksheet and write a large number into cell A1
        Sheet sheet = workbook.createSheet("Numbers");
        Row row = sheet.createRow(0);
        Cell cell = row.createCell(0);
        cell.setCellValue(12345678.9);   // write value to cell
        cell.setCellStyle(sciStyle);    // apply scientific notation

        // Save the workbook – export data to xlsx
        try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
            workbook.write(out);
        }
        workbook.close();

        System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Chạy lớp, mở `sigDigits.xlsx`, và bạn sẽ thấy số được hiển thị ở dạng khoa học với đúng bốn chữ số đáng kể. Đó là toàn bộ quy trình **set number format excel** trong Java.

---

## Kết Luận

Chúng ta vừa trình bày mọi thứ bạn cần để **set number format excel** từ Java: tạo workbook, tạo style dạng khoa học mà **set significant digits**, **write value to cell**, và cuối cùng **export data to xlsx**. Cách tiếp cận này nhẹ, chỉ dùng Apache POI và hoạt động trên bất kỳ nền tảng nào hỗ trợ Java.

Tiếp theo, bạn có thể muốn:

- Thêm định dạng có điều kiện để làm nổi bật các giá trị ngoài phạm vi.  
- Tạo nhiều sheet với các kiểu số khác nhau (ví dụ: tiền tệ vs. khoa học).  
- Dòng dữ liệu lớn bằng `SXSSFWorkbook` để xuất hiệu quả về bộ nhớ.  

Hãy thử những gợi ý này, và bạn sẽ trở thành người được tin cậy cho việc tự động hoá Excel trong đội của mình. Có câu hỏi hoặc trường hợp sử dụng lạ? Để lại bình luận bên dưới—chúc lập trình vui! 

*Hình ảnh minh họa quy trình (alt text: “set number format excel workflow diagram showing Java code, scientific notation, and export to xlsx”)*


## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều có ví dụ mã hoàn chỉnh kèm giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Đặt Ô Hoạt Động trong Excel Sử Dụng Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Đặt Ô Hoạt Động Excel](/cells/german/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Đặt Ô Hoạt Động Excel](/cells/french/java/cell-operations/aspose-cells-java-set-active-cell-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}