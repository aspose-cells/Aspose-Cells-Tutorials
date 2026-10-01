---
category: general
date: 2026-10-01
description: Tìm hiểu cách xuất hình dạng bằng ShapeExportOptions trong Java, giữ
  cho hình dạng có thể chỉnh sửa khi chuyển đổi sang PPTX bằng Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: vi
lastmod: 2026-10-01
og_description: Xuất hình dạng bằng ShapeExportOptions trong Java để tạo các tệp PPTX
  có thể chỉnh sửa. Hướng dẫn này sẽ đưa bạn qua toàn bộ quá trình sử dụng Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Xuất hình dạng bằng ShapeExportOptions trong Java – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Cách xuất hình dạng bằng ShapeExportOptions trong Java
url: /vi/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất shape với ShapeExportOptions trong Java

Nếu bạn cần **export shape with ShapeExportOptions** từ một workbook Excel, hướng dẫn này sẽ chỉ cho bạn các bước chính xác. Bạn sẽ thấy cách giữ shape có thể chỉnh sửa khi chuyển đổi sang tệp PPTX, điều này rất quan trọng cho việc chỉnh sửa tiếp theo trong PowerPoint.

Xuất shape là một nhiệm vụ phổ biến khi bạn tạo bộ slide từ bảng tính—bất kể bạn đang xây dựng bộ slide bán hàng, bảng điều khiển báo cáo, hay các bản trình bày tự động. Bài hướng dẫn này bao gồm mọi thứ bạn cần, từ cài đặt dự án đến việc xác minh tệp đã xuất, và nó sử dụng thư viện **Aspose.Cells for Java**.

## Những gì bạn cần

- Java 17 hoặc mới hơn (mã sẽ biên dịch với bất kỳ JDK gần đây nào)
- Maven hoặc Gradle để quản lý phụ thuộc
- Một tệp Excel (`Shapes.xlsx`) chứa ít nhất một textbox hoặc shape khác
- Kiến thức cơ bản về Aspose.Cells APIs

## Bước 1: Thêm Aspose.Cells vào dự án của bạn (Aspose Cells export shape)

Nếu bạn sử dụng Maven, thêm phụ thuộc sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Đối với Gradle, đặt đoạn này vào `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Mẹo:** Đăng ký giấy phép sớm để tránh watermark đánh giá.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Bước 2: Tải workbook chứa shape

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

Đối tượng `Workbook` đại diện cho toàn bộ tệp Excel. Việc tải nó là điều kiện tiên quyết đầu tiên cho bất kỳ thao tác nào với shape.

## Bước 3: Truy cập worksheet và lấy shape mong muốn (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Tại sao điều này quan trọng:** Shapes được lưu theo worksheet, vì vậy bạn phải chuyển đến sheet đúng trước khi có thể xuất một shape cụ thể.

## Bước 4: Cấu hình **ShapeExportOptions** để giữ shape có thể chỉnh sửa (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

Đặt `ExportAsEditable` thành `true` cho Aspose.Cells biết giữ lại dữ liệu vector của shape, cho phép người dùng PowerPoint chỉnh sửa shape sau khi nhập.

## Bước 5: Xuất shape trực tiếp ra tệp PPTX (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

Phương thức `exportToImage` hoạt động cho một số định dạng ảnh; khi tên tệp đích kết thúc bằng `.pptx`, Aspose.Cells sẽ ghi một slide PowerPoint chứa shape.

### Kết quả mong đợi

- `textbox.pptx` xuất hiện trong thư mục đã chỉ định.
- Mở tệp trong PowerPoint sẽ hiển thị một slide duy nhất với textbox gốc.
- textbox có thể chỉnh sửa hoàn toàn (bạn có thể thay đổi văn bản, phông chữ, kích thước, v.v.).

## Bước 6: Xác minh đầu ra và xử lý các trường hợp biên thường gặp

### Xác minh bằng chương trình

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

Nếu `slideCount` bằng `1`, việc xuất đã thành công.

### Trường hợp biên: Nhiều shape

Nếu worksheet chứa nhiều shape và bạn chỉ muốn một shape cụ thể, hãy tìm nó theo tên:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Trường hợp biên: Không tìm thấy shape

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Trường hợp biên: Xuất sang định dạng khác

`ShapeExportOptions` cũng hỗ trợ PNG, JPEG, SVG và EMF. Thay đổi phần mở rộng tệp và tùy chọn đặt `exportOptions.setImageFormat(ImageFormat.PNG)`.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các phần lại với nhau sẽ cho bạn một chương trình tự chứa mà bạn có thể sao chép‑dán vào IDE của mình:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

Chạy chương trình sẽ tạo `textbox.pptx`. Mở nó trong PowerPoint, nhấp chuột phải vào textbox, và bạn sẽ thấy các công cụ chỉnh sửa thường—xác nhận rằng **export shape with ShapeExportOptions** đã giữ được khả năng chỉnh sửa.

## Câu hỏi thường gặp

| Câu hỏi | Trả lời |
|----------|--------|
| *Tôi có thể xuất shape biểu đồ không?* | Có. Lệnh `exportToImage` tương tự hoạt động cho biểu đồ, hình ảnh và SmartArt. |
| *Nếu tôi cần PNG độ phân giải cao hơn thì sao?* | Đặt `options.setImageFormat(ImageFormat.PNG)` và điều chỉnh `options.setResolution(300)` trước khi xuất. |
| *PPTX đã xuất có tương thích với các phiên bản PowerPoint cũ không?* | Thư viện ghi Office Open XML (PPTX) được hỗ trợ bởi PowerPoint 2007 trở lên. |
| *Tôi có cần giấy phép để tính năng này hoạt động không?* | Phiên bản đánh giá miễn phí hoạt động nhưng sẽ thêm watermark. Đăng ký giấy phép để loại bỏ nó. |

## Các bước tiếp theo

- Khám phá **Aspose.Slides for Java** nếu bạn cần kết hợp nhiều shape đã xuất vào một bộ slide duy nhất.
- Sử dụng **ShapeExportOptions.setExportAsEditable(false)** khi bạn muốn hình raster (PNG/JPEG) để render nhanh hơn.
- Tự động xử lý hàng loạt: lặp qua tất cả worksheets và xuất mỗi shape ra các tệp PPTX riêng.

---

### Kết luận

Bạn bây giờ đã biết cách **export shape with ShapeExportOptions** trong Java, giữ được khả năng chỉnh sửa khi chuyển đổi textbox (hoặc bất kỳ shape nào khác) sang tệp PPTX. Bằng cách làm theo các bước trên—cài đặt thư viện, tải workbook, cấu hình `ShapeExportOptions`, và gọi `exportToImage`—bạn có thể tích hợp việc xuất shape vào bất kỳ quy trình báo cáo tự động nào.

Hãy tự do thử nghiệm với các shape khác nhau, định dạng đầu ra và cài đặt độ phân giải. Nếu bạn thấy hướng dẫn này hữu ích, hãy chia sẻ với đồng nghiệp hoặc lưu lại để tham khảo sau. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách điều chỉnh lề Shape trong Excel bằng Aspose.Cells cho Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [Cách áp dụng định dạng Shape 3D trong Excel bằng Aspose.Cells cho Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Hướng dẫn sao chép Shape trong Workbook Aspose Cells Java](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}