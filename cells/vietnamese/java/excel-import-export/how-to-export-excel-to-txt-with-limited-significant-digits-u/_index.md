---
category: general
date: 2026-08-17
description: Xuất Excel sang TXT đồng thời giới hạn số chữ số có nghĩa – tìm hiểu
  cách thiết lập số chữ số và chuyển đổi Excel sang văn bản trong Java với ví dụ đầy
  đủ về Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: vi
lastmod: 2026-08-17
og_description: Xuất Excel sang TXT trong khi giới hạn chữ số có nghĩa. Hướng dẫn
  này chỉ cách đặt số chữ số và chuyển đổi Excel sang văn bản bằng Aspose.Cells cho
  Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Xuất Excel sang TXT với số chữ số có nghĩa giới hạn – Hướng dẫn Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Cách xuất Excel sang TXT với số chữ số có giới hạn bằng Java
url: /vi/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Excel sang TXT với số chữ số có nghĩa giới hạn bằng Java

Nếu bạn cần **xuất Excel sang TXT** đồng thời kiểm soát số chữ số có nghĩa, hướng dẫn này cung cấp giải pháp đã sẵn sàng để chạy. Bạn sẽ thấy cách đặt số chữ số, chuyển đổi Excel sang văn bản và giữ cho đầu ra gọn gàng chỉ với một thay đổi cấu hình duy nhất.

Mẫu này sử dụng Aspose.Cells for Java 25.10, phiên bản giới thiệu tùy chọn `setSignificantDigits`. Khi kết thúc tutorial, bạn có thể tạo tệp TXT chỉ chứa những chữ số bạn muốn, mà không cần mã làm tròn bổ sung.

## Những gì bạn sẽ đạt được

- Tạo một workbook bằng chương trình.
- Chèn một giá trị số vào ô.
- Cấu hình tùy chọn lưu TXT để giới hạn chữ số có nghĩa.
- Lưu workbook dưới dạng tệp văn bản thuần.
- Hiểu cách hoạt động của cài đặt `significantDigits` và cách điều chỉnh cho các kịch bản khác.

### Yêu cầu trước

- Java 17 hoặc mới hơn (mã cũng biên dịch được với Java 8).
- Aspose.Cells for Java 25.10 trở lên. Tải JAR từ [trang web Aspose](https://products.aspose.com/cells/java) và thêm vào classpath của dự án.
- Một IDE hoặc trình soạn thảo văn bản đơn giản và công cụ xây dựng dòng lệnh (Maven/Gradle).

## Bước 1: Thiết lập dự án và nhập Aspose.Cells

Tạo một dự án Java mới và thêm JAR Aspose.Cells vào đường dẫn biên dịch. Nếu bạn dùng Maven, thêm phụ thuộc sau vào `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Mẹo:** Sử dụng bộ phân loại `jdk17` cho môi trường Java mới nhất; nó giảm nguy cơ cảnh báo tương thích.

## Bước 2: Tạo workbook và ghi một giá trị

Workbook đại diện cho một tệp Excel trong bộ nhớ. Bạn có thể thêm dữ liệu vào bất kỳ ô nào bằng phương thức `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Số `123.456789` sẽ là nguồn cho việc xuất TXT của chúng ta. Mặc định Aspose.Cells sẽ ghi tất cả các chữ số thập phân, thường tạo ra các tệp văn bản ồn ào.

## Bước 3: Cấu hình tùy chọn lưu TXT để giới hạn chữ số có nghĩa

Aspose.Cells cung cấp `TxtSaveOptions` để kiểm soát chi tiết đầu ra văn bản thuần. Phương thức `setSignificantDigits` cho trình xuất biết cần giữ bao nhiêu chữ số **tổng cộng**, không chỉ sau dấu thập phân.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Khi `significantDigits` được đặt thành `4`, trình xuất sẽ làm tròn giá trị `123.456789` thành `123.5`. Hành vi này phù hợp với định nghĩa toán học của các chữ số có nghĩa: bốn chữ số khác 0 đầu tiên được giữ lại.

### Cách cài đặt này khác với “giới hạn thập phân”

- **giới hạn thập phân** (`setDecimalPlaces`) cắt bớt các chữ số *sau* dấu thập phân, bất kể phần nguyên.
- **chữ số có nghĩa** (`setSignificantDigits`) đếm chữ số từ chữ số khác 0 đầu tiên, hữu ích khi các số có độ lớn khác nhau.

Nếu bạn cần một số lượng chữ số thập phân cố định, thay thế dòng trên bằng:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Bước 4: Lưu workbook dưới dạng tệp TXT

Bây giờ ghi workbook ra đĩa bằng các tùy chọn đã cấu hình.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Chạy chương trình sẽ tạo `significant_digits.txt` trong thư mục làm việc. Tệp chứa một dòng duy nhất:

```
123.5
```

### Đầu ra dự kiến

| Ô   | Giá trị gốc   | Xuất (4 chữ số có nghĩa) |
|-----|---------------|---------------------------|
| A1  | 123.456789    | 123.5                     |

Nếu bạn thay `setSignificantDigits(4)` thành `6`, đầu ra sẽ là `123.457`. Thử các giá trị khác để xem cách làm tròn thay đổi.

## Bước 5: Các biến thể phổ biến và trường hợp đặc biệt

### Xuất toàn bộ vùng dữ liệu

Nếu muốn xuất hơn một ô, chỉ cần điền vùng trước khi lưu:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Cài đặt `significantDigits` giống nhau sẽ áp dụng cho mọi ô số, đảm bảo độ chính xác đồng nhất trong tệp.

### Xử lý dấu phân cách thập phân theo locale

Aspose.Cells tuân theo locale hệ thống khi ghi văn bản. Để buộc dấu chấm (`.`) làm dấu phân cách thập phân, đặt culture cho `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Điều này hữu ích khi ứng dụng đích yêu cầu định dạng cụ thể, chẳng hạn các bộ phân tích CSV chỉ chấp nhận `.`.

### Ghi đè tệp hiện có

Phương thức `save` mặc định sẽ ghi đè tệp đích. Nếu bạn muốn tránh mất dữ liệu ngoài ý muốn, hãy kiểm tra sự tồn tại của tệp trước:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Workbook lớn và tiêu thụ bộ nhớ

Khi xuất các worksheet rất lớn, hãy cân nhắc stream đầu ra:

```java
saveOptions.setEnableMemorySaving(true);
```

Tùy chọn này giảm tiêu thụ heap bằng cách ghi từng hàng một cách tuần tự.

## Ví dụ hoàn chỉnh

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép, dán và chạy ngay:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Chạy đoạn mã này sẽ tạo `significant_digits.txt` với nội dung sau (các cột cách nhau bằng tab):

```
123.5	0.001235	98770
```

Mỗi số đều tuân theo quy tắc **4 chữ số có nghĩa**, chứng minh rằng cài đặt hoạt động trên các độ lớn khác nhau.

## Kết luận

Bây giờ bạn đã biết cách **xuất Excel sang TXT** đồng thời kiểm soát số chữ số có nghĩa. Bằng cách sử dụng `TxtSaveOptions.setSignificantDigits`, bạn có thể **đặt số chữ số**, **giới hạn thập phân**, và **giới hạn chữ số có nghĩa** chỉ với một dòng mã duy trì. Cách tiếp cận này hoạt động cho ô đơn, toàn bộ vùng và cả workbook lớn.

### Các bước tiếp theo

- Khám phá các thuộc tính khác của `TxtSaveOptions` như `setDelimiter('\t')` để tùy chỉnh dấu phân cách cột.
- Kết hợp trình xuất với `CsvSaveOptions` nếu bạn cần giá trị phân tách bằng dấu phẩy thay vì văn bản thuần.
- Tích hợp quy trình này vào dịch vụ web nhận tệp Excel tải lên và trả về đầu ra TXT đã cắt giảm ngay lập tức.

Hãy thoải mái thử nghiệm với các giới hạn chữ số và locale khác nhau. Nếu gặp trường hợp tùy chọn tích hợp không đáp ứng yêu cầu đặc biệt, bạn luôn có thể xử lý hậu kỳ tệp TXT bằng các tiện ích I/O chuẩn của Java.

Chúc lập trình vui vẻ!


## Bạn nên học gì tiếp theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách chuyển đổi Văn bản thành Số trong Excel bằng Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Cách Tạo và Xuất Excel sang HTML bằng Aspose.Cells Java | Hướng dẫn Thao tác Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cách Xuất Thuộc tính Excel Tùy chỉnh sang PDF bằng Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}