---
category: general
date: 2026-10-10
description: Tìm hiểu cách xuất phạm vi Excel thành hình ảnh trong Java bằng Aspose.Cells.
  Hướng dẫn cũng bao gồm việc xuất các ô đã chọn thành hình ảnh và lưu worksheet Excel
  dưới dạng ảnh.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: vi
lastmod: 2026-10-10
og_description: Xuất phạm vi Excel dưới dạng hình ảnh trong Java với giải pháp từng
  bước. Bao gồm xuất các ô đã chọn dưới dạng hình ảnh và lưu bảng tính Excel dưới
  dạng ảnh.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Xuất vùng Excel thành hình ảnh trong Java – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Cách xuất vùng Excel thành hình ảnh trong Java với Aspose.Cells
url: /vi/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất vùng Excel thành hình ảnh trong Java với Aspose.Cells

Nếu bạn cần **xuất vùng Excel thành hình ảnh**, hướng dẫn này sẽ chỉ cho bạn cách thực hiện giải pháp Java hoàn chỉnh bằng thư viện Aspose.Cells. Bạn cũng sẽ học cách **xuất các ô đã chọn thành hình ảnh** và cách **lưu worksheet Excel dưới dạng ảnh** cho mục đích báo cáo hoặc tài liệu.

Việc xuất một phần của workbook thành ảnh loại bỏ nhu cầu dùng các công cụ chụp màn hình của bên thứ ba và đảm bảo kết quả pixel‑perfect. Khi hoàn thành hướng dẫn này, bạn sẽ có một phương thức có thể tái sử dụng để ghi PNG (hoặc bất kỳ định dạng nào được hỗ trợ) trực tiếp vào đĩa, sẵn sàng để chèn vào PDF, email hoặc trang web.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* Java 17 hoặc mới hơn được cài đặt.
* Maven 3.8+ (hoặc công cụ xây dựng khác có thể xử lý các phụ thuộc Maven).
* Giấy phép Aspose.Cells for Java (bản đánh giá miễn phí vẫn hoạt động nhưng sẽ có watermark).
* Một tệp Excel mẫu (`input.xlsx`) đặt trong thư mục đã biết.

Các phần sau đây giả định bạn đã quen với phát triển Java cơ bản và cấu hình dự án Maven.

## Bước 1: Thêm Aspose.Cells vào dự án của bạn

Thêm phụ thuộc Aspose.Cells Maven vào file `pom.xml` của bạn. Thư viện này cung cấp các lớp `Workbook`, `Worksheet` và `ImageOrPrintOptions` được sử dụng trong ví dụ mã.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Giữ cho số phiên bản luôn cập nhật; các bản phát hành mới hơn bổ sung hỗ trợ định dạng và cải thiện hiệu năng.

## Bước 2: Tạo phương thức tiện ích để xuất một vùng

Việc đóng gói logic xuất ra trong một phương thức giúp bạn dễ dàng tái sử dụng trong các dự án và xử lý các trường hợp đặc biệt như ô hợp nhất hoặc hàng ẩn.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Tại sao phương thức này quan trọng

* **Tách biệt trách nhiệm:** Tải dữ liệu, cấu hình tùy chọn và xuất ảnh được chia rõ ràng.
* **Linh hoạt:** Bạn có thể thay đổi định dạng ảnh hoặc DPI mà không cần chỉnh sửa logic cốt lõi.
* **Xử lý lỗi:** Ném `Exception` cho phép người gọi quyết định ghi log, thử lại hoặc dừng lại.

## Bước 3: Gọi phương thức với các tham số thực tế

Dưới đây là một phương thức `main` tối thiểu minh họa cách **xuất các ô đã chọn thành hình ảnh** và cách **lưu worksheet Excel dưới dạng ảnh** bằng cách sử dụng toàn bộ phạm vi sheet.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Kết quả mong đợi

Chạy chương trình sẽ tạo hai tệp PNG:

* `range.png` – ảnh chỉ chứa các ô **A1:G20**.
* `full_sheet.png` – ảnh của toàn bộ vùng đã sử dụng của worksheet đầu tiên, thực chất là **lưu worksheet Excel dưới dạng ảnh**.

Bạn có thể mở các tệp này bằng bất kỳ trình xem ảnh nào để xác nhận bố cục trực quan khớp với giao diện Excel, bao gồm viền ô, màu sắc và các ô hợp nhất.

## Bước 4: Xử lý các trường hợp đặc biệt thường gặp

### 1. Ô hợp nhất

Aspose.Cells tự động giữ nguyên giao diện của các ô hợp nhất, nhưng nếu bạn cần kiểm soát việc render, hãy đặt `options.setOnePagePerSheet(true)` để buộc toàn bộ sheet vào một trang duy nhất trước khi xuất.

### 2. Hàng hoặc cột ẩn

Mặc định, các hàng/cột ẩn sẽ không được render. Để bao gồm chúng, bật:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Vùng lớn và tiêu thụ bộ nhớ

Xuất các vùng rất lớn có thể tiêu tốn đáng kể bộ nhớ. Nếu gặp `OutOfMemoryError`, hãy cân nhắc:

* Giảm DPI (`options.setHorizontalResolution(150)`).
* Xuất vùng thành các đoạn nhỏ hơn và ghép các ảnh lại bằng thư viện đồ họa.

## Bước 5: Xác minh kết quả bằng chương trình (tùy chọn)

Nếu quy trình hạ nguồn của bạn cần xác nhận rằng ảnh đã được tạo đúng, bạn có thể tải PNG bằng `javax.imageio.ImageIO` và kiểm tra kích thước:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Chiều rộng và chiều cao khác 0 cho thấy việc xuất ảnh thành công.

## Kết luận

Bây giờ bạn đã biết cách **xuất vùng Excel thành hình ảnh** trong Java, cách **xuất các ô đã chọn thành hình ảnh**, và cách **lưu worksheet Excel dưới dạng ảnh** bằng Aspose.Cells. Phương thức `exportRangeAsImage` có thể tái sử dụng giúp trừu tượng hoá độ phức tạp, cho phép bạn kiểm soát chất lượng ảnh và hoạt động với bất kỳ chỉ số worksheet hoặc phạm vi ô nào.

Các bước tiếp theo bạn có thể khám phá:

* Chuyển PNG sang PDF bằng Aspose.PDF để báo cáo.
* Xử lý hàng loạt nhiều workbook trong một thư mục.
* Tích hợp xuất ảnh vào endpoint REST Spring Boot để khách hàng có thể yêu cầu ảnh theo nhu cầu.

Hãy thoải mái thử nghiệm các định dạng ảnh khác (`ImageFormat.JPEG`, `ImageFormat.BMP`) và các thiết lập DPI để đáp ứng yêu cầu hình ảnh của dự án. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Xuất Workbook Excel thành hình ảnh bằng Aspose.Cells cho Java: Hướng dẫn từng bước](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Cách tạo biểu đồ Excel với đường xu hướng và xuất ra hình ảnh bằng Aspose.Cells cho Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Xuất các ô Excel thành hình ảnh bằng Aspose.Cells .NET: Hướng dẫn từng bước](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}