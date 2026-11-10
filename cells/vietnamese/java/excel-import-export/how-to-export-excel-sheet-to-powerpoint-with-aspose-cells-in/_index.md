---
category: general
date: 2026-09-27
description: Cách xuất sheet Excel sang PowerPoint bằng Aspose.Cells trong Java –
  hướng dẫn từng bước cũng cho thấy cách chuyển đổi workbook Excel sang bản trình
  bày PowerPoint.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: vi
lastmod: 2026-09-27
og_description: Cách xuất sheet Excel sang PowerPoint bằng Aspose.Cells trong Java.
  Tìm hiểu cách chuyển đổi workbook Excel sang bản trình chiếu PowerPoint với mã đầy
  đủ.
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: Cách xuất bảng tính Excel sang PowerPoint – Hướng dẫn Java với Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: Cách xuất bảng Excel sang PowerPoint bằng Aspose.Cells trong Java
url: /vi/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất sheet Excel sang PowerPoint bằng Aspose.Cells trong Java

Nếu bạn cần **cách xuất sheet Excel sang PowerPoint**, hướng dẫn này cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy chính xác cách **chuyển đổi workbook Excel sang bản trình bày PowerPoint** trong khi giữ nguyên các hộp văn bản có thể chỉnh sửa và định dạng cơ bản.

Hướng dẫn giả định bạn đã có môi trường phát triển Java hoạt động và một giấy phép Aspose.Cells for Java hợp lệ. Khi kết thúc bài viết, bạn sẽ có một chương trình Java tải workbook Excel, xuất worksheet đầu tiên và ghi file `.pptx` có thể mở và chỉnh sửa trong Microsoft PowerPoint.

## Prerequisites

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Java 17 hoặc mới hơn | Aspose.Cells hỗ trợ các runtime Java hiện đại và cung cấp hiệu năng tốt hơn. |
| Aspose.Cells for Java (phiên bản 23.10 hoặc mới hơn) | Thư viện chứa overload `Workbook.save(..., SaveFormat.PPTX)` được dùng để chuyển đổi. |
| Bản sao có giấy phép của Aspose.Cells | Không có giấy phép, thư viện chạy ở chế độ đánh giá và sẽ thêm watermark. |
| File Excel chứa ít nhất một textbox có thể chỉnh sửa | Quá trình chuyển đổi sẽ giữ lại textbox dưới dạng shape có thể chỉnh sửa trong PowerPoint. |
| IDE hoặc công cụ xây dựng (ví dụ: Maven, Gradle) | Để biên dịch và chạy mã mẫu. |

## Step 1: Add Aspose.Cells to your project

Nếu bạn dùng Maven, thêm dependency sau vào `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Đối với Gradle, đặt đoạn mã này vào `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Mẹo:** Khai báo dependency trong scope `provided` nếu bạn chỉ cần thư viện ở thời gian chạy trên máy chủ.

## Step 2: Prepare the Excel workbook

Tạo một file Excel (`WorkbookWithTextbox.xlsx`) chứa một textbox có thể chỉnh sửa trên worksheet đầu tiên. Bạn có thể chèn textbox trong Excel bằng **Insert → Text Box**. Lưu file vào thư mục mà bạn có thể tham chiếu từ Java, ví dụ `src/main/resources`.

## Step 3: Write the conversion code

Tạo một lớp Java có tên `ExportEditableTextbox`. Mã dưới đây bao gồm đầy đủ import, xử lý lỗi và các chú thích giải thích từng thao tác.

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### Why this works

* `Workbook` đại diện cho toàn bộ file Excel. Khi tải nó, tất cả các worksheet, chart và shape sẽ được phân tích.
* `workbook.save(..., SaveFormat.PPTX)` kích hoạt engine chuyển đổi tích hợp của Aspose.Cells. Engine này ánh xạ các ô, hàng và shape của Excel sang các slide PowerPoint, giữ lại các textbox có thể chỉnh sửa dưới dạng shape PowerPoint.
* Phương thức này ghi một slide cho mỗi worksheet. Trong ví dụ này, worksheet đầu tiên trở thành slide duy nhất.

## Step 4: Run the program

Biên dịch và thực thi lớp bằng công cụ xây dựng của bạn:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

hoặc, nếu bạn dùng Gradle:

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

Sau khi chương trình kết thúc, mở `Worksheet.pptx` trong Microsoft PowerPoint. Bạn sẽ thấy một slide phản ánh chính xác sheet Excel, và textbox bạn tạo trong Excel xuất hiện dưới dạng shape có thể chỉnh sửa (double‑click để sửa).

## Step 5: Handling multiple worksheets (optional)

Nếu bạn muốn xuất **tất cả** các worksheet trong workbook, thay lời gọi một worksheet bằng một vòng lặp:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

Mỗi vòng lặp sẽ tạo một file PowerPoint riêng (`Worksheet_0.pptx`, `Worksheet_1.pptx`, …). Đối với một bản trình bày duy nhất chứa nhiều slide, Aspose.Cells tự động thêm một slide cho mỗi worksheet khi bạn gọi `save` một lần; không cần viết thêm code.

## Edge cases and best practices

| Tình huống | Cách tiếp cận đề xuất |
|-----------|----------------------|
| Workbook lớn (hàng trăm MB) | Tăng heap JVM (`-Xmx4g`) và cân nhắc xuất từng worksheet riêng để tránh lỗi out‑of‑memory. |
| Workbook được bảo vệ bằng mật khẩu | Sử dụng `LoadOptions` để cung cấp mật khẩu trước khi tải: `new LoadOptions(LoadFormat.XLSX, "pwd")`. |
| Cần giữ lại công thức Excel | PowerPoint không hỗ trợ công thức; chúng sẽ được render thành giá trị tĩnh trong quá trình chuyển đổi. |
| Yêu cầu layout slide tùy chỉnh | Sau khi chuyển đổi, dùng Aspose.Slides for Java để điều chỉnh master slide hoặc thêm animation. |
| Chạy trong dịch vụ web | Stream đầu ra trực tiếp tới HTTP response thay vì ghi file: `workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## Expected output

Chạy ví dụ sẽ tạo ra một file có tên `Worksheet.pptx`. Mở file này trong PowerPoint sẽ hiển thị:

* Một slide khớp về mặt hình ảnh với worksheet Excel đầu tiên.
* Một textbox có thể chỉnh sửa được đặt chính xác ở vị trí đã có trong Excel.
* Định dạng ô cơ bản (cỡ chữ, màu, viền) được giữ nguyên.

Console sẽ in ra:

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## Conclusion

Bây giờ bạn đã biết **cách xuất sheet Excel sang PowerPoint** bằng Aspose.Cells for Java, và bạn cũng hiểu cách **chuyển đổi workbook Excel sang bản trình bày PowerPoint** trong các tình huống thực tế. Giải pháp này hoạt động cho việc xuất worksheet đơn, workbook đa worksheet, và có thể mở rộng bằng Aspose.Slides để tùy chỉnh slide thêm.

---

### Next steps

* Khám phá **Aspose.Slides for Java** để thêm animation, chart, hoặc master slide tùy chỉnh sau khi chuyển đổi.  
* Thử chuyển đổi các workbook có chứa chart; Aspose.Cells sẽ render chart dưới dạng đối tượng chart gốc của PowerPoint.  
* Nghiên cứu xử lý batch bằng cách đọc một thư mục các file Excel và tạo một PowerPoint cho mỗi file.

Feel free to experiment with the code, adapt the file paths, and integrate the conversion into larger Java applications such as reporting services or automated document pipelines. Happy coding!

## What Should You Learn Next?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}