---
category: general
date: 2026-09-21
description: Chuyển đổi Excel sang PowerPoint với Aspose.Cells trong Java – tìm hiểu
  cách xuất biểu đồ sang PPTX và lưu workbook dưới dạng PPTX chỉ trong vài dòng mã.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: vi
lastmod: 2026-09-21
og_description: Chuyển đổi Excel sang PowerPoint bằng Aspose.Cells trong Java. Hướng
  dẫn này chỉ cách xuất biểu đồ ra PPTX và lưu sổ làm việc dưới dạng PPTX với các
  hộp văn bản có thể chỉnh sửa.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Chuyển đổi Excel sang PowerPoint với Aspose.Cells – Hướng dẫn Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Chuyển đổi Excel sang PowerPoint với Aspose.Cells trong Java
url: /vi/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi Excel sang PowerPoint với Aspose.Cells trong Java

Nếu bạn cần **chuyển đổi Excel sang PowerPoint**, hướng dẫn này sẽ cho bạn một cách ngắn gọn, sẵn sàng cho môi trường sản xuất. Bạn sẽ thấy cách xuất biểu đồ sang PPTX, giữ các hộp văn bản có thể chỉnh sửa, và **lưu workbook dưới dạng PPTX** chỉ trong ba dòng mã Java.

Nhiều nhà phát triển xuất dữ liệu sang PDF, nhưng PowerPoint thường phù hợp hơn cho các bài thuyết trình yêu cầu biểu đồ sống và các yếu tố có thể chỉnh sửa. Bài hướng dẫn này bao gồm mọi thứ bạn cần—từ cài đặt dự án đến xử lý các lỗi thường gặp—để bạn có thể tạo PowerPoint từ biểu đồ Excel mà không rời khỏi IDE Java của mình.

## Yêu cầu trước

* Java 17 hoặc mới hơn đã được cài đặt.  
* Maven (hoặc Gradle) để quản lý phụ thuộc.  
* Giấy phép Aspose.Cells for Java (bản dùng thử miễn phí đủ cho việc đánh giá).  
* Một tệp Excel (`ChartAndTextbox.xlsx`) chứa ít nhất một biểu đồ và một hộp văn bản.

## Bước 1: Thêm Aspose.Cells vào dự án của bạn

Bước đầu tiên là bao gồm thư viện Aspose.Cells. Sử dụng Maven, thêm phụ thuộc sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Nếu bạn sử dụng Gradle, tương đương là:  
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Việc bao gồm thư viện sẽ cho phép bạn truy cập vào `Workbook`, `PdfSaveOptions` và enum `SaveFormat` cần thiết cho quá trình chuyển đổi.

## Bước 2: Tải workbook chứa biểu đồ và hộp văn bản

Bây giờ tải tệp Excel. Lớp `Workbook` đọc toàn bộ workbook vào bộ nhớ, giữ nguyên biểu đồ, công thức và các hộp văn bản.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**Tại sao điều này quan trọng:** Việc tải workbook trước đảm bảo rằng tất cả các đối tượng nhúng (biểu đồ, hình ảnh, hộp văn bản) đã sẵn sàng cho quá trình xuất. Nếu không tìm thấy tệp, Aspose.Cells sẽ ném ra một `FileNotFoundException` rõ ràng, bạn có thể bắt để cải thiện trải nghiệm người dùng.

## Bước 3: Cấu hình tùy chọn xuất để giữ hộp văn bản có thể chỉnh sửa

Aspose.Cells sử dụng `PdfSaveOptions` để kiểm soát cách các đối tượng được ghi khi định dạng đích là PowerPoint. Bằng cách bật `setExportEditableTextBoxes(true)`, bất kỳ hộp văn bản nào trong sheet Excel sẽ vẫn có thể chỉnh sửa sau khi chuyển đổi.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **Tại sao sử dụng `PdfSaveOptions` cho PPTX?**  
> Nội bộ, Aspose.Cells tái sử dụng pipeline render PDF cho đầu ra PowerPoint, cho phép kiểm soát chi tiết các yếu tố có thể chỉnh sửa. Đặt cờ này là cách được khuyến nghị để bảo tồn khả năng chỉnh sửa hộp văn bản.

## Bước 4: Lưu workbook dưới dạng bản trình bày PowerPoint

Cuối cùng, gọi `workbook.save` với `SaveFormat.PPTX`. Bước này hoàn thành quy trình **tạo PowerPoint từ biểu đồ Excel**.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

Kết hợp lại, chương trình đầy đủ trông như sau:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in ra:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

Khi bạn mở `Result.pptx` trong Microsoft PowerPoint, bạn sẽ thấy:

* Biểu đồ Excel gốc được hiển thị dưới dạng biểu đồ PowerPoint gốc (có thể chỉnh sửa trong trình chỉnh sửa biểu đồ của PowerPoint).  
* Hộp văn bản từ Excel xuất hiện dưới dạng hình dạng có thể chỉnh sửa, cho phép bạn thay đổi văn bản trực tiếp trên slide.

## Xử lý các trường hợp góc cạnh thường gặp

| Tình huống | Cách tiếp cận đề xuất |
|-----------|----------------------|
| **File not found** | Bao bọc hàm khởi tạo `Workbook` trong khối `try‑catch` và hiển thị thông báo rõ ràng. |
| **Workbook has no chart** | Kiểm tra sheet có chứa biểu đồ (`worksheet.getCharts().getCount() > 0`) trước khi chuyển đổi; nếu không, bỏ qua bước hoặc thêm một placeholder. |
| **Large Excel files** | Tăng kích thước heap JVM (`-Xmx2g`) để tránh `OutOfMemoryError` trong quá trình render. |
| **License not set** | Gọi `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` trước khi tải workbook để loại bỏ watermark đánh giá. |

## Câu hỏi thường gặp

**Q: Tôi có thể chuyển đổi nhiều worksheet thành các slide PowerPoint riêng biệt không?**  
A: Có. Lặp qua từng worksheet, xuất biểu đồ của nó vào một slide mới bằng `PdfSaveOptions`, sau đó lưu workbook một lần sau khi xử lý xong tất cả các sheet.

**Q: Phương pháp này có giữ định dạng ô không?**  
A: Chỉ các đối tượng biểu đồ và hộp văn bản được chuyển sang PowerPoint. Định dạng ô vẫn ở trong tệp Excel; nó sẽ không xuất hiện trong PPTX.

**Q: Nếu tôi muốn xuất ra PDF thay vì PPTX thì sao?**  
A: Sử dụng `SaveFormat.PDF` và cùng `PdfSaveOptions`. Cờ `setExportEditableTextBoxes` cũng hoạt động cho PDF.

## Các bước tiếp theo

Bây giờ bạn đã biết cách **lưu workbook dưới dạng PPTX** và **xuất biểu đồ sang PPTX**, bạn có thể khám phá:

* Thêm nhiều biểu đồ vào các slide khác nhau (`create powerpoint from excel chart` với vòng lặp).  
* Tùy chỉnh bố cục slide bằng Aspose.Slides for Java để có phong cách trình bày phong phú hơn.  
* Nhúng hình ảnh từ các ô Excel vào PowerPoint bằng lớp `Picture`.

Các mở rộng này cho phép bạn xây dựng quy trình báo cáo tự động hoàn toàn, tạo ra các bản trình bày chuyên nghiệp trực tiếp từ dữ liệu Excel.

---

**Tóm tắt:** Bài hướng dẫn này đã trình bày cách đáng tin cậy để **chuyển đổi Excel sang PowerPoint** bằng Aspose.Cells cho Java. Bằng việc tải workbook, cấu hình `PdfSaveOptions` để giữ hộp văn bản có thể chỉnh sửa, và lưu với `SaveFormat.PPTX`, bạn sẽ có một tệp PowerPoint chứa các biểu đồ sống và các hình dạng có thể chỉnh sửa—hoàn hảo cho các bài thuyết trình kinh doanh động. Hãy tự do điều chỉnh mã cho xử lý hàng loạt hoặc tích hợp vào các giải pháp báo cáo lớn hơn.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo biểu đồ Excel với Trendline và xuất ra hình ảnh bằng Aspose.Cells cho Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Cách chuyển đổi biểu đồ Excel sang SVG bằng Aspose.Cells trong Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [Cách chuyển đổi Excel sang PDF trong Java bằng Aspose.Cells&#58; Hướng dẫn từng bước](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}