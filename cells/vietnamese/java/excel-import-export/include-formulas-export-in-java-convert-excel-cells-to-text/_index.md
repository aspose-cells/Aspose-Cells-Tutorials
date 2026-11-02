---
category: general
date: 2026-07-03
description: Bao gồm xuất công thức trong Java để chuyển các ô Excel thành văn bản
  bằng Aspose.Cells. Tìm hiểu cách in phạm vi Excel và lấy chuỗi giá trị ô một cách
  hiệu quả.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: vi
og_description: Bao gồm xuất công thức trong Java để chuyển đổi ô Excel thành văn
  bản. Hướng dẫn từng bước cách in phạm vi Excel và lấy giá trị ô dưới dạng chuỗi.
og_title: Bao gồm xuất công thức trong Java – Chuyển các ô Excel thành văn bản
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Bao gồm xuất công thức trong Java – Chuyển các ô Excel thành văn bản
url: /vi/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bao gồm xuất công thức trong Java – Chuyển đổi ô Excel thành Văn bản

Bạn đã bao giờ cần **include formulas export** khi trích xuất dữ liệu từ một workbook Excel chưa? Có thể bạn đang xây dựng một dịch vụ báo cáo phải giữ nguyên các công thức gốc trong khi vẫn cung cấp một khối văn bản gọn gàng. Trong trường hợp đó, bạn đã đến đúng nơi. Hướng dẫn này sẽ chỉ cho bạn cách chuyển đổi các ô Excel thành văn bản thuần—*bao gồm* bất kỳ công thức nào được nhúng—sử dụng Aspose.Cells for Java.

Chúng tôi cũng sẽ đề cập đến cách **print Excel range**, tinh chỉnh **export table options**, và cuối cùng **get cell values string** mà bạn có thể ghi log, gửi qua API, hoặc lưu vào cơ sở dữ liệu. Khi kết thúc, bạn sẽ có một đoạn mã có thể chạy ngay và hiểu rõ lý do đằng sau mỗi lời gọi.

## Những gì bạn sẽ nhận được

- Một chương trình Java hoàn chỉnh, sẵn sàng copy‑paste, đọc file `.xlsx`, chọn một vùng và xuất nó dưới dạng chuỗi đã định dạng.  
- Hiểu rõ lớp `ExportTableOptions` và tại sao việc bật/tắt `setExportAsString` và `setIncludeFormula` lại quan trọng.  
- Các mẹo xử lý worksheets lớn, làm việc với các kiểu dữ liệu khác nhau, và tùy chỉnh định dạng đầu ra.  
- Một danh sách kiểm tra nhanh cho các lỗi thường gặp (như ô hợp nhất, hàng ẩn, và định dạng số theo locale).

### Yêu cầu trước

- Java 17 hoặc mới hơn (mã có thể biên dịch với các phiên bản cũ hơn nhưng chúng tôi sẽ dùng LTS mới nhất).  
- Aspose.Cells for Java 23.10 (hoặc bất kỳ bản phát hành gần đây nào) — bạn có thể tải từ Maven Central.  
- Một file mẫu `input.xlsx` đặt trong thư mục bạn kiểm soát (đường dẫn được mã cứng trong ví dụ để dễ hiểu).

Nếu bạn đã có những thứ trên, hãy bắt đầu.

## Bước 1: Thiết lập dự án và thêm phụ thuộc

Đầu tiên, tạo một dự án Maven (hoặc Gradle, nếu bạn thích). Thêm phụ thuộc Aspose.Cells vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Nếu bạn đang sử dụng proxy công ty, hãy chắc chắn rằng repository có thể truy cập được; nếu không quá trình build sẽ thất bại với lỗi “Could not resolve dependencies”.

Khi Maven hoàn tất việc tải về, bạn đã sẵn sàng viết một chút Java.

## Bước 2: Tải Workbook và Lấy Worksheet Mong Muốn

Dòng đầu tiên của ví dụ mã cho thấy cách mở một workbook hiện có:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Thay thế `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối tới file của bạn. Hàm khởi tạo `Workbook` sẽ tự động phát hiện định dạng file (XLS, XLSX, CSV, v.v.), vì vậy bạn không cần chỉ định nó.

Tiếp theo, chúng ta lấy sheet đầu tiên:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Tại sao lại là sheet đầu tiên? Trong nhiều mẫu, dữ liệu nằm trên tab đầu tiên, nhưng bạn có thể truyền bất kỳ chỉ số nào hoặc thậm chí dùng `get("SheetName")` nếu muốn cách tiếp cận dựa trên tên.

## Bước 3: Xác Định Vùng Muốn Xuất

Bây giờ là phần cốt lõi của thao tác **convert excel cells text**. Bạn cho Aspose.Cells biết những ô nào cần lấy bằng cách tạo một đối tượng `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Chuỗi `"A1:C3"` là địa chỉ kiểu A1 truyền thống. Nó cũng có thể được tạo lập bằng chương trình:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Sự linh hoạt này hữu ích khi kích thước vùng thay đổi—ví dụ, bạn đọc dòng cuối cùng đã dùng bằng `ws.getCells().getMaxDataRow()`.

## Bước 4: Cấu Hình Export Table Options để Bao Gồm Công Thức

Đây là nơi **include formulas export** thực sự hoạt động. Mặc định, Aspose.Cells trả về giá trị *hiển thị*. Nếu một ô chứa `=SUM(A1:A3)`, bạn sẽ nhận được số đã tính, không phải chuỗi công thức. Để thay đổi điều này, hãy thiết lập `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Tại sao cần cả hai cờ? `setExportAsString(true)` báo cho API nối các ô lại với nhau bằng dấu phân cách mặc định (tab cho cột, newline cho hàng). `setIncludeFormula(true)` chuyển nguồn giá trị từ “giá trị hiển thị” sang “công thức thô”. Nếu bạn chỉ muốn giá trị, để `false`.

### Tinh chỉnh tùy chọn

- `eto.setExportHiddenRows(true);` – bao gồm các hàng bị ẩn trong Excel.  
- `eto.setExportHiddenColumns(true);` – tương tự cho cột.  
- `eto.setExportAsHTML(true);` – nhận HTML thay vì văn bản thuần.

Hãy thoải mái thử nghiệm; lớp options là một **export table options** playground.

## Bước 5: Lấy Vùng Dưới Dạng Chuỗi Định Dạng

Bây giờ chúng ta kéo dữ liệu:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Chuỗi `txt` trả về trông giống như sau (giả sử A1:C3 chứa hỗn hợp giá trị và công thức):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Lưu ý dấu tab (`\t`) ngăn cách các cột và dấu newline (`\n`) ngăn cách các hàng. Bạn có thể tách chuỗi này sau này nếu cần một mảng 2‑D:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Bước 6: In Kết Quả – “Print Excel Range” Đơn Giản

Cuối cùng, chúng ta đổ chuỗi ra console:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Chạy chương trình sẽ in ra chính xác đầu ra như trên. Từ đây bạn có thể ghi chuỗi vào file log, gửi qua HTTP, hoặc lưu vào tài liệu NoSQL.

## Ví dụ Đầy Đủ, Sẵn Sàng Chạy

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh. Sao chép, dán và nhấn **Run**—không thiếu import nào.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Đầu ra Dự Kiến (mẫu)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Nếu workbook của bạn chứa các số được định dạng dưới dạng ngày, chúng sẽ xuất hiện theo định dạng locale‑specific (ví dụ, `2026‑07‑03`). Để ép ngày sang định dạng ISO, bạn có thể tinh chỉnh `ExportTableOptions` với một `NumberFormat` tùy chỉnh.

## Xử Lý Các Trường Hợp Đặc Biệt và Câu Hỏi Thường Gặp

### Nếu vùng chứa ô hợp nhất thì sao?

Các ô hợp nhất được xử lý như giá trị của ô trên‑trái. Phần còn lại của vùng hợp nhất sẽ xuất hiện dưới dạng chuỗi rỗng. Nếu bạn cần địa chỉ của vùng hợp nhất, hãy truy vấn `Cell.getMergedRange()` trước khi xuất.

### Tôi có thể xuất một sheet khổng lồ (hàng chục nghìn) không?

Có, nhưng hãy chú ý tới việc tiêu thụ bộ nhớ. Sử dụng `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` để cho Aspose.Cells stream dữ liệu ra đĩa. Ngoài ra, cân nhắc xuất theo từng khối (ví dụ, 10 000 hàng một lần) để chuỗi đầu ra không quá lớn.

### Làm sao thay đổi dấu phân cách cột?

`ExportTableOptions` cung cấp `setSeparator(char separator)`. Đối với đầu ra kiểu CSV, đặt nó thành `','`:

```java
eto.setSeparator(',');
```

### Công thức có tôn trọng tham chiếu ngoại vi không?

Nếu một công thức trỏ tới workbook khác, Aspose.Cells sẽ giữ nguyên văn bản tham chiếu (`='[Other.xlsx]Sheet1'!A1`). Nó sẽ không tính giá trị ngoại vi trừ khi bạn tải workbook đó lên.

## Pro Tips cho Mã Sẵn Sàng Sản Xuất

- **Cache workbook** nếu bạn đang đọc ...

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Tạo và Xuất Excel ra HTML bằng Aspose.Cells Java | Hướng Dẫn Thao Tác Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cách Chuyển Đổi Excel sang PDF trong Java Sử Dụng Aspose.Cells&#58; Hướng Dẫn Từng Bước](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Xuất Workbook Excel dưới dạng Hình Ảnh bằng Aspose.Cells for Java&#58; Hướng Dẫn Từng Bước](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}