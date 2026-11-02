---
category: general
date: 2026-10-07
description: Tìm hiểu cách tải JSON vào Excel và tạo tệp XLSX từ JSON bằng Aspose.Cells.
  Hướng dẫn từng bước này cũng chỉ cách điền dữ liệu từ JSON vào Excel và lưu sổ làm
  việc dưới dạng XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: vi
lastmod: 2026-10-07
og_description: Tải JSON vào Excel và tạo tệp XLSX từ JSON bằng Aspose.Cells cho Java.
  Hãy làm theo hướng dẫn này để đưa dữ liệu JSON vào Excel và lưu sổ làm việc dưới
  dạng XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Tải JSON vào Excel bằng Aspose.Cells – hướng dẫn Java đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cách tải JSON vào Excel bằng Aspose.Cells cho Java
url: /vi/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tải JSON vào Excel bằng Aspose.Cells cho Java

Nếu bạn cần **tải JSON vào Excel**, hướng dẫn này sẽ cho bạn một cách đáng tin cậy để thực hiện với Aspose.Cells cho Java. Bạn sẽ thấy cách tạo XLSX từ JSON, điền dữ liệu vào Excel từ JSON, và cuối cùng **lưu workbook dưới dạng XLSX**—tất cả trong một chương trình tự chứa duy nhất.

Làm việc với JSON trong bảng tính là điều phổ biến khi bạn xuất dữ liệu từ các dịch vụ web, API hoặc kho lưu trữ NoSQL. Khi kết thúc hướng dẫn này, bạn sẽ có một lớp Java sẵn sàng chạy tạo workbook từ JSON và ghi kết quả vào một tệp trên đĩa.

## Yêu cầu trước

* Java 8 hoặc mới hơn đã được cài đặt (mã sử dụng các tính năng chuẩn của Java).
* Thư viện Aspose.Cells cho Java (phiên bản 23.10 hoặc mới hơn). Bạn có thể tải nó từ [Aspose website](https://downloads.aspose.com/cells/java) hoặc qua Maven Central.
* Một IDE hoặc một trình soạn thảo văn bản đơn giản và một terminal để biên dịch và chạy mã Java.
* Kiến thức cơ bản về cú pháp JSON và các khái niệm Excel.

> **Mẹo chuyên nghiệp:** Nếu bạn sử dụng Maven, thêm phụ thuộc sau vào `pom.xml` của bạn để tránh việc quản lý JAR thủ công:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Bước 1: Thiết lập dự án và nhập các lớp cần thiết

Tạo một lớp Java mới có tên `JsonToExcelDemo`. Nhập các lớp Aspose.Cells mà bạn sẽ cần cho việc tạo workbook, xử lý worksheet và xử lý Smart Marker.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*​Tại sao bước này quan trọng:* Việc nhập đúng các lớp đảm bảo trình biên dịch có thể tìm thấy các API của Aspose.Cells. Lớp `Workbook` đại diện cho tệp Excel, trong khi `SmartMarkerProcessor` điều khiển quá trình chuyển đổi JSON‑to‑Excel.

## Bước 2: Xác định nguồn JSON sẽ được tải vào Excel

Trong ví dụ này, chúng ta sử dụng một mảng JSON nhỏ chứa hai đối tượng. Trong thực tế, bạn có thể đọc JSON từ tệp, endpoint REST hoặc cơ sở dữ liệu.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*​Tại sao bước này quan trọng:* Chuỗi JSON là nguồn dữ liệu cho thao tác **điền Excel từ JSON**. Giữ JSON trong biến `String` giúp dễ dàng truyền cho `SmartMarkerProcessor`.

## Bước 3: Tạo một workbook mới và lấy worksheet đầu tiên

Một workbook mới cung cấp cho bạn một bảng trắng. Worksheet đầu tiên (chỉ mục 0) là nơi chúng ta sẽ chèn Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*​Tại sao bước này quan trọng:* Aspose.Cells làm việc với đối tượng `Workbook` có thể được lưu sau này dưới dạng tệp XLSX. Truy cập `Worksheet` đầu tiên cho phép chúng ta đặt marker tại một địa chỉ ô đã biết.

## Bước 4: Chèn Smart Marker để chỉ định cách Aspose.Cells xử lý JSON

Smart Markers là các placeholder mà Aspose.Cells thay thế bằng dữ liệu từ một nguồn. Marker `&=JSONData.ArrayAsSingle` chỉ thị cho thư viện xử lý toàn bộ mảng JSON như một giá trị ô duy nhất.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*​Tại sao bước này quan trọng:* Sử dụng `ArrayAsSingle` tránh hành vi mặc định mở rộng mỗi phần tử mảng thành các hàng riêng biệt. Điều này hữu ích khi bạn muốn văn bản JSON hiển thị nguyên văn trong một ô, hoặc khi bạn dự định tách nó sau này bằng công thức.

## Bước 5: Cấu hình SmartMarkerProcessor với nguồn dữ liệu JSON

Bây giờ gắn chuỗi JSON với tên logic `JSONData`. Bộ xử lý sẽ thay thế marker bằng dữ liệu thực tế.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*​Tại sao bước này quan trọng:* `setDataSource` liên kết tên được sử dụng trong marker (`JSONData`) với payload JSON thực tế. `process()` thực hiện công việc nặng: phân tích JSON, áp dụng logic marker và ghi kết quả vào worksheet.

## Bước 6: Lưu workbook đã tạo thành tệp XLSX

Cuối cùng, ghi workbook ra đĩa. Hằng số `SaveFormat.XLSX` đảm bảo định dạng Office Open XML đúng.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*​Tại sao bước này quan trọng:* Lưu tệp hoàn thành quy trình **tạo XLSX từ JSON**. Tệp được tạo có thể mở trong Excel, LibreOffice hoặc bất kỳ chương trình bảng tính nào hỗ trợ XLSX.

### Mã nguồn đầy đủ

Kết hợp tất cả các phần lại, đây là chương trình hoàn chỉnh, có thể chạy được mà **tạo workbook từ JSON**, **điền Excel từ JSON**, và **lưu workbook dưới dạng XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Kết quả mong đợi

Khi bạn mở `JsonSingleCell.xlsx` bạn sẽ thấy mảng JSON hiển thị trong ô **A1** chính xác như chuỗi gốc:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Nếu bạn muốn mỗi đối tượng trên một hàng riêng, thay thế marker bằng `&=JSONData` (không có `.ArrayAsSingle`). Bộ xử lý sẽ mở rộng mảng thành các hàng riêng lẻ, minh họa một kỹ thuật **điền Excel từ JSON** khác.

## Các biến thể phổ biến và trường hợp đặc biệt

| Situation | Adjustment |
|-----------|------------|
| **Payload JSON lớn ( > 10 MB )** | Tăng kích thước heap JVM (`-Xmx2g`) và cân nhắc streaming JSON để tránh `OutOfMemoryError`. |
| **Đối tượng lồng nhau** | Sử dụng các marker phân cấp như `&=JSONData.Name` và `&=JSONData.Age` trong bảng để ánh xạ mỗi thuộc tính vào một cột. |
| **Tệp JSON thay vì chuỗi** | Đọc tệp vào một `String` bằng `java.nio.file.Files.readString(Path.of("data.json"))` và truyền nó cho `setDataSource`. |
| **Cần giữ nguyên định dạng JSON gốc** | Giữ hậu tố `.ArrayAsSingle`, hoặc bọc JSON trong CDATA nếu bạn dự định sử dụng công thức Excel để phân tích JSON sau này. |
| **Nhiều worksheet** | Tạo các worksheet bổ sung (`workbook.getWorksheets().add("Sheet2")`) và lặp lại việc chèn marker trên mỗi sheet. |

> **Cảnh báo:** Smart Markers phân biệt chữ hoa và chữ thường. Đảm bảo tên logic (`JSONData`) khớp chính xác giữa marker và `setDataSource`.

## Kiểm thử giải pháp

1. Biên dịch chương trình:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Chạy chương trình:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Xác minh rằng `JsonSingleCell.xlsx` xuất hiện trong thư mục làm việc và mở mà không có lỗi.

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ, có hướng dẫn từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Workbook Excel từ JSON – Hướng dẫn đầy đủ Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Tạo Workbook Excel C# – Chèn JSON và Lưu dưới dạng XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Lưu Workbook Excel từ JSON – Hướng dẫn đầy đủ](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}