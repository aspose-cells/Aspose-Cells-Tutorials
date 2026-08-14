---
category: general
date: 2026-08-14
description: Cách đặt dấu phân cách và lưu dưới dạng CSV bằng Aspose.Cells, giới hạn
  số chữ số, xuất chuỗi CSV và tính lại công thức trong Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: vi
lastmod: 2026-08-14
og_description: Cách đặt dấu phân cách và lưu dưới dạng CSV với Aspose.Cells, giới
  hạn số chữ số, xuất chuỗi CSV và tính lại công thức trong Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Cách đặt dấu phân cách và lưu dưới dạng CSV – Hướng dẫn Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Cách đặt dấu phân cách và lưu dưới dạng CSV với Aspose.Cells
url: /vi/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách đặt dấu phân cách và lưu dưới dạng CSV với Aspose.Cells

Nếu bạn cần **cách đặt dấu phân cách** khi xuất dữ liệu từ một workbook Excel, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, từ đầu đến cuối sử dụng Aspose.Cells cho Java. Bạn sẽ học cách cấu hình dấu phân cách CSV, giới hạn số chữ số có nghĩa, xuất một chuỗi CSV, và làm mới các công thức mảng động sau khi tải workbook.

Hướng dẫn bao gồm mọi thứ bạn cần để chạy mã trên máy của mình, bao gồm việc xử lý các lịch đặc biệt như thời kỳ Hoàng đế Nhật Bản. Khi hoàn thành, bạn sẽ có thể tạo các tệp CSV chính xác, kiểm soát độ chính xác số học và đảm bảo các công thức luôn cập nhật.

## Yêu cầu trước

- Java 17 hoặc mới hơn (mã cũng biên dịch được với JDK 11+)
- Aspose.Cells for Java 23.9 hoặc mới hơn – tải về từ [Aspose website](https://products.aspose.com/cells/java/)
- Kiến thức cơ bản về Maven hoặc Gradle để quản lý phụ thuộc
- Một IDE (IntelliJ IDEA, Eclipse, VS Code) hoặc một trình soạn thảo văn bản đơn giản và dòng lệnh

> **Mẹo chuyên nghiệp:** Sử dụng thư mục `libs` riêng hoặc Maven Central để giữ JAR của Aspose.Cells trong classpath. Các ví dụ dưới đây giả định một dự án Maven.

## Bước 1: Thiết lập dự án Maven

Tạo một file `pom.xml` với phụ thuộc Aspose.Cells:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Chạy `mvn clean compile` để tải thư viện và xác nhận quá trình xây dựng thành công.

## Bước 2: Cách đặt dấu phân cách và lưu dưới dạng CSV

Mục tiêu chính là thay đổi dấu phân cách mặc định là dấu phẩy sang một ký tự tùy chỉnh (ví dụ: dấu chấm phẩy) khi lưu workbook Excel dưới dạng CSV. Aspose.Cells cung cấp `CsvSaveOptions` cho mục đích này.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Tại sao cách này hoạt động

- `CsvSaveOptions.setDelimiter(char)` cho Aspose.Cells biết ký tự nào sẽ ngăn cách các trường. Mặc định là dấu phẩy, nhưng bất kỳ ký tự nào (tab `'\t'`, pipe `'|'`, v.v.) cũng hoạt động.
- `setSignificantDigits(int)` giới hạn độ chính xác số học, đáp ứng yêu cầu **cách giới hạn chữ số** mà không cần định dạng từng ô thủ công.

#### Kết quả mong đợi

Tệp `output.csv` sẽ chứa các hàng như sau:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Lưu ý rằng các số được làm tròn tới năm chữ số có nghĩa (ví dụ, `123.45678` → `123.46`).

## Bước 3: Cách giới hạn chữ số khi lưu CSV

Nếu bạn cần kiểm soát chặt chẽ hơn định dạng số, bạn cũng có thể sử dụng một thể hiện `CsvSaveOptions` để chỉ định chuỗi định dạng số tùy chỉnh.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` tuân theo các mẫu kiểu .NET, mà Aspose.Cells tôn trọng.
- Kết hợp cả `setNumberFormat` và `setSignificantDigits` giúp bạn có được việc làm tròn dự đoán được trên các miền địa phương khác nhau.

## Bước 4: Cách xuất CSV dưới dạng chuỗi với dấu phân cách tùy chỉnh

Đôi khi bạn không muốn tạo tệp vật lý; bạn cần dữ liệu CSV trong bộ nhớ (ví dụ: để gửi dưới dạng phản hồi HTTP). Lớp `ExportTableOptions` cho phép bạn xuất một phạm vi dưới dạng chuỗi.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Khi nào nên sử dụng

- Trả về CSV từ một endpoint REST (`@RestController` trong Spring)
- Nhúng dữ liệu CSV vào tệp đính kèm email mà không ghi ra đĩa
- Thực hiện các kiểm tra nhanh trong unit test

## Bước 5: Cách tính lại công thức sau khi tải workbook

Nếu workbook của bạn chứa công thức—đặc biệt là **dynamic‑array formulas** được giới thiệu trong các phiên bản Excel gần đây—bạn phải tính lại chúng sau khi tải tệp. Aspose.Cells tự động làm mới kết quả của các công thức mảng động, nhưng bạn vẫn cần gọi `calculateFormula()` cho các công thức thường.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Tại sao cần tính lại?

- Công thức có thể tham chiếu dữ liệu bên ngoài hoặc các hàm biến động (`NOW()`, `RAND()`) cần giá trị mới.
- Dynamic‑array formulas (ví dụ, `=SORT(A1:A10)`) được đánh giá tự động, nhưng việc gọi `calculateFormula()` đảm bảo tính nhất quán trên tất cả các sheet.

## Bước 6: Ví dụ đầy đủ từ đầu đến cuối

Dưới đây là một lớp duy nhất minh họa **cách đặt dấu phân cách**, **lưu dưới dạng CSV**, **giới hạn chữ số**, **xuất chuỗi CSV**, **tải workbook với lịch đặc biệt**, và **tính lại công thức**. Mã đã sẵn sàng để sao chép‑dán vào dự án của bạn.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Xác minh kết quả

1. Mở `output.csv` trong trình soạn thảo văn bản – bạn sẽ thấy dấu chấm phẩy (`;`) ngăn cách mỗi cột.
2. Xác nhận rằng các cột số hiển thị tối đa năm chữ số có nghĩa.
3. Đầu ra console sẽ in ra chuỗi CSV được tạo ở bước 4.
4. Mở `japan_updated.xlsx` trong Excel – bất kỳ công thức nào trước đây hiển thị `#REF!` hoặc giá trị cũ sẽ bây giờ hiển thị kết quả đúng.

## Những lỗi thường gặp và cách tránh

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------|-----|
| CSV hiển thị dấu ngoặc kép thừa | Các ô chứa dấu phẩy trong khi dấu phân cách cũng là dấu phẩy | Sử dụng dấu phân cách khác (`;` hoặc `\t`) qua `setDelimiter` |
| Các số bị làm tròn không đúng | `setSignificantDigits` được áp dụng sau định dạng số tùy chỉnh | Áp dụng `setNumberFormat` **trước** `setSignificantDigits` |

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn thành thạo các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tải và lưu Excel dưới dạng CSV bằng Aspose.Cells cho Java: Hướng dẫn toàn diện](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Cách tải tệp CSV bằng Aspose.Cells cho Java: Hướng dẫn toàn diện](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Cách tải các tệp CSV bằng bộ phân tích tùy chỉnh trong Java với Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}