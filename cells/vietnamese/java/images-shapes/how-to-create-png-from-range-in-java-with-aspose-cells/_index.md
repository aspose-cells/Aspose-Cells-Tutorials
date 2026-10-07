---
category: general
date: 2026-10-07
description: Tìm hiểu cách tạo PNG từ phạm vi và xuất dữ liệu dưới dạng PNG trong
  Java. Hướng dẫn này cho bạn biết cách lưu ảnh phạm vi Excel bằng Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: vi
lastmod: 2026-10-07
og_description: Tạo PNG từ vùng trong Java và xuất dữ liệu dưới dạng PNG bằng Aspose.Cells.
  Theo dõi hướng dẫn đầy đủ này để lưu ngay hình ảnh vùng Excel.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Tạo PNG từ phạm vi trong Java – hướng dẫn chi tiết Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cách tạo PNG từ phạm vi trong Java với Aspose.Cells
url: /vi/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo PNG từ phạm vi trong Java với Aspose.Cells

Nếu bạn cần **tạo PNG từ phạm vi** trong một workbook Excel, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Khi kết thúc hướng dẫn, bạn sẽ có thể **xuất dữ liệu dưới dạng PNG**, lưu hình ảnh phạm vi Excel và tái sử dụng tệp trong báo cáo hoặc trang web.

Bạn sẽ thấy một chương trình Java đầy đủ, có thể chạy được, tải workbook, chọn các ô mong muốn, kết xuất chúng dưới dạng PNG và lưu kết quả vào đĩa. Không cần công cụ bên ngoài—Aspose.Cells xử lý mọi thứ nội bộ.

## Nội dung hướng dẫn này

* Yêu cầu trước và cấu hình Maven cho Aspose.Cells
* Tải workbook chứa pivot table hoặc bất kỳ phạm vi dữ liệu nào
* Xác định phạm vi ô chính xác mà bạn muốn chuyển đổi
* Cấu hình tùy chọn hình ảnh cho đầu ra PNG
* Kết xuất phạm vi và lưu tệp PNG
* Các lỗi thường gặp và mẹo để có hình ảnh chất lượng cao

Sau khi hoàn thành các bước này, bạn sẽ có thể **chuyển đổi worksheet sang PNG** cho bất kỳ phạm vi nào, dù là bảng đơn giản hay biểu đồ pivot phức tạp.

## Yêu cầu trước

* Java 17 hoặc mới hơn (mã được biên dịch với JDK 11+)
* Maven 3.6+ (hoặc Gradle nếu bạn muốn)
* Aspose.Cells for Java 23.12 hoặc mới hơn – thêm phụ thuộc như dưới đây
* Một tệp Excel hiện có (`PivotWithStyle.xlsx`) chứa phạm vi bạn muốn chụp

> **Pro tip:** Nếu bạn không có giấy phép, bạn có thể yêu cầu một khóa đánh giá tạm thời từ Aspose. Thư viện hoạt động ở chế độ đánh giá mà không cần cấu hình bổ sung.

### Phụ thuộc Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Bước 1: Tải workbook chứa phạm vi mục tiêu

Hoạt động đầu tiên là mở tệp Excel. Aspose.Cells đọc tệp vào bộ nhớ mà không cần Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Why this matters*: Việc tải workbook cho phép bạn truy cập vào các worksheet, ô và các thuộc tính thiết lập trang cần thiết cho việc kết xuất.

## Bước 2: Truy cập worksheet chứa phạm vi

Hầu hết các workbook có một sheet mặc định ở chỉ mục 0, nhưng bạn cũng có thể sử dụng tên sheet.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Nếu dữ liệu của bạn nằm trên một sheet khác, thay `0` bằng chỉ mục phù hợp hoặc dùng `workbook.getWorksheets().get("SheetName")`.

## Bước 3: Xác định phạm vi ô bạn muốn chuyển đổi

Bạn có thể chỉ định bất kỳ khu vực hình chữ nhật nào bằng ký hiệu A1. Trong ví dụ này chúng tôi chụp `A1:D15`, có thể là một pivot table hoặc một khối dữ liệu thông thường.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Edge case*: Khi phạm vi bao gồm các ô đã hợp nhất, Aspose.Cells sẽ tự động mở rộng hình ảnh để bao gồm khu vực hợp nhất.

## Bước 4: Chuẩn bị tùy chọn hình ảnh PNG

`ImageOrPrintOptions` cho phép bạn kiểm soát định dạng, độ phân giải và các chi tiết kết xuất khác. Đặt định dạng lưu thành PNG đảm bảo chất lượng không mất dữ liệu.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Tăng DPI hữu ích khi các ô nguồn chứa phông chữ nhỏ hoặc biểu đồ chi tiết.

## Bước 5: Giới hạn khu vực kết xuất tới phạm vi đã chọn

Bằng cách gán phạm vi làm khu vực in, Aspose.Cells chỉ kết xuất các ô đó và bỏ qua phần còn lại của sheet.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Nếu bỏ qua bước này, toàn bộ worksheet sẽ được raster hoá, gây lãng phí bộ nhớ và tạo ra hình ảnh lớn hơn.

## Bước 6: Kết xuất phạm vi và thêm hình ảnh vào worksheet (tùy chọn)

Nếu bạn muốn nhúng PNG đã tạo lại vào workbook (để xem trước), bạn có thể thêm nó như một hình ảnh. Bước này là tùy chọn cho các kịch bản chỉ xuất.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Why you might do this*: Một số quy trình làm việc yêu cầu hình ảnh là một phần của workbook trước khi phân phối, chẳng hạn như tạo báo cáo có thể in được kết hợp giữa các ô gốc và hình ảnh.

## Bước 7: Lưu tệp PNG vào đĩa

Cuối cùng, ghi hình ảnh vào tệp. Phương thức `save` tuân theo định dạng được chỉ định trong `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Khi chương trình kết thúc, `PivotImage.png` sẽ chứa một ảnh chụp pixel‑perfect của các ô `A1:D15`.

### Kết quả mong đợi

* Một tệp có tên `PivotImage.png` nằm trong `YOUR_DIRECTORY`.
* Hình ảnh hiển thị bố cục, phông chữ, màu sắc và viền chính xác từ phạm vi đã chọn.
* Nếu phạm vi nguồn chứa pivot table, hình ảnh được kết xuất sẽ bao gồm cùng kiểu dáng và giá trị đã tính như hiển thị trong Excel.

## Xử lý các kịch bản phổ biến

### Xuất phạm vi không liên tục

Aspose.Cells không kết xuất các phạm vi rời rạc trong một hình ảnh duy nhất. Để xuất nhiều khu vực, tạo các hình ảnh riêng cho mỗi phạm vi và sau đó kết hợp chúng bằng thư viện xử lý ảnh (ví dụ, ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Lưu worksheet lớn dưới dạng PNG

Kết xuất toàn bộ sheet có hàng ngàn dòng có thể tiêu tốn bộ nhớ đáng kể. Giảm thiểu bằng cách:

* Giảm DPI (`imageOptions.setResolution(72)`) để có tệp nhỏ hơn.
* Sử dụng `setPageCount` để giới hạn số trang được kết xuất.
* Xuất từng trang có thể in một lần qua `worksheet.getPageSetup().setPrintArea(...)`.

### Bảo tồn công thức ô

Một ảnh PNG là định dạng raster; công thức không được giữ lại. Nếu người dùng downstream cần dữ liệu thô, cũng hãy xuất phạm vi dưới dạng CSV hoặc JSON bằng `Range.exportDataTable()`.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là lớp Java hoàn chỉnh mà bạn có thể sao chép‑dán vào IDE. Thay `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối trên máy của bạn.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Chạy chương trình với `mvn compile exec:java` (hoặc công cụ xây dựng bạn ưa thích). Sau khi thực thi, mở `PivotImage.png` để kiểm tra kết quả.

## Kết luận

Bạn giờ đã biết cách **tạo PNG từ phạm vi** trong Java bằng Aspose.Cells, hiệu quả **xuất dữ liệu dưới dạng PNG** và **lưu hình ảnh phạm vi Excel** cho bất kỳ kịch bản báo cáo hoặc chia sẻ nào. Các bước—tải workbook, xác định phạm vi, cấu hình tùy chọn hình ảnh, đặt khu vực in và lưu tệp—bao quát toàn bộ quy trình cho **chuyển đổi worksheet sang PNG** và **lưu ô dưới dạng PNG**.

### Các bước tiếp theo

* Thử nghiệm các giá trị `Resolution` khác nhau để cân bằng chất lượng và kích thước tệp.
* Sử dụng `ImageOrPrintOptions.setTransparent(true)` nếu bạn cần PNG có nền trong suốt.
* Kết hợp nhiều hình ảnh phạm vi thành một PDF duy nhất bằng `PdfSaveOptions` cho báo cáo đa trang.
* Khám phá xuất sang các định dạng raster khác (JPEG, BMP) bằng cách thay đổi `setSaveFormat`.

Bạn có thể tự do điều chỉnh mẫu này cho biểu đồ, bảng hoặc thậm chí toàn bộ worksheet. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có ví dụ mã đầy đủ, hoạt động với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách xuất một worksheet Excel sang PNG bằng Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Chuyển đổi Excel sang PNG bằng Aspose.Cells cho Java: Hướng dẫn từng bước](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Tạo Union Range trong Excel bằng Aspose.Cells Java: Hướng dẫn toàn diện](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}