---
category: general
date: 2026-11-16
description: Tìm hiểu cách xuất hình dạng từ Excel sang PowerPoint bằng Java, chuyển
  biểu đồ Excel thành tệp PPTX và lưu hình dạng PPTX bằng Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: vi
lastmod: 2026-11-16
og_description: Cách xuất hình dạng từ Excel sang PowerPoint bằng Java. Theo dõi hướng
  dẫn đầy đủ này để chuyển đổi biểu đồ Excel, lưu hình dạng dưới dạng PPTX và nhúng
  một hình dạng vào tệp PowerPoint.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: Cách xuất hình dạng từ Excel sang PowerPoint trong Java – hướng dẫn từng
  bước
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: Cách xuất hình dạng từ Excel sang PowerPoint bằng Java
url: /vi/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất shape từ Excel sang PowerPoint bằng Java

Nếu bạn cần **how to export shape** từ một workbook Excel vào một slide PowerPoint, hướng dẫn này sẽ cho bạn các bước chính xác. Bạn sẽ thấy cách **convert Excel chart** các đối tượng, chuyển chúng thành một **shape to PowerPoint**, và cuối cùng **save shape PPTX** với các tùy chọn xuất đúng.

Xuất một shape là yêu cầu phổ biến khi bạn tạo báo cáo một cách tự động. Khi kết thúc tutorial này, bạn sẽ có một chương trình Java tự chứa tạo ra tệp `shape.pptx` sẵn sàng cho bài thuyết trình. Không cần script bên ngoài, và mã hoạt động với Aspose.Cells 2024‑R2 hoặc mới hơn.

## Yêu cầu trước

* Java 17 hoặc mới hơn (mã biên dịch với bất kỳ JDK 8+ nào)
* Thư viện Aspose.Cells cho Java (tải xuống từ trang web Aspose hoặc thêm phụ thuộc Maven)
* Tệp Excel (`chart.xls`) chứa ít nhất một shape (biểu đồ, textbox hoặc SmartArt)
* Kiến thức cơ bản về xử lý ngoại lệ trong Java

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## Cách xuất shape từ Excel sang PowerPoint (luồng tổng thể)

Quá trình bao gồm bốn phần logic:

1. **Load the workbook** chứa shape.  
2. **Locate the shape** trên worksheet đầu tiên.  
3. **Configure export options** để shape trở thành đối tượng PowerPoint có thể chỉnh sửa.  
4. **Save the shape as a PPTX file**.

Mỗi phần được giải thích chi tiết bên dưới, và chương trình chạy được đầy đủ sẽ theo sau các giải thích.

## Bước 1: Tải workbook chứa shape

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*Why this step?*  
`Workbook` là điểm vào cho tất cả các thao tác Aspose.Cells. Việc tải tệp cho phép bạn truy cập vào worksheets, cells và bộ sưu tập shape. Nếu tệp không tìm thấy, Aspose.Cells sẽ ném `FileNotFoundException`, mà chúng ta sẽ bắt sau.

## Bước 2: Truy cập worksheet đầu tiên và lấy shape mục tiêu

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*Why this step?*  
Worksheets được lưu trong một collection bắt đầu từ chỉ số 0, vì vậy `get(0)` trả về sheet đầu tiên. Shapes cũng được đánh chỉ số; `get(0)` lấy shape đầu tiên, thường là biểu đồ bạn muốn xuất. Nếu workbook của bạn chứa nhiều shape, bạn có thể lặp qua collection hoặc dùng `shape.getName()` để chọn một shape cụ thể.

## Bước 3: Chuẩn bị tùy chọn xuất – chúng ta muốn shape dưới dạng đối tượng PPTX có thể chỉnh sửa

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*Why this step?*  
`ImageOrPrintOptions` kiểm soát cách shape được render. Bằng cách chọn `SaveFormat.PPTX`, thư viện chuyển đồ họa Excel thành shape PowerPoint dựa trên vector, vẫn có thể chỉnh sửa sau khi nhập. Điều này là cần thiết cho việc chuyển đổi **shape to PowerPoint** thực sự; dùng PNG hoặc JPEG sẽ khóa đồ họa.

## Bước 4: Xuất shape ra tệp PowerPoint

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*Why this step?*  
Phương thức `save` ghi shape bằng các tùy chọn đã định nghĩa trước. `shape.pptx` tạo ra chứa một slide duy nhất, trong đó shape xuất hiện chính xác như trong Excel, nhưng bây giờ bạn có thể chỉnh sửa nó trong PowerPoint (thay đổi màu, thay đổi kích thước, thêm hoạt ảnh, v.v.). Điều này đáp ứng yêu cầu **save shape PPTX**.

## Ví dụ đầy đủ, có thể chạy

Sao chép toàn bộ lớp vào một tệp có tên `ExportShapeDemo.java`, thay thế `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối, và chạy `javac ExportShapeDemo.java && java ExportShapeDemo`. Sau khi thực thi, bạn sẽ thấy `shape.pptx` trong thư mục đích.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### Kết quả mong đợi

```
Export completed. File saved as shape.pptx
```

Mở `shape.pptx` trong Microsoft PowerPoint. Bạn sẽ thấy một slide duy nhất chứa biểu đồ Excel gốc (hoặc textbox) dưới dạng shape PowerPoint hoàn toàn có thể chỉnh sửa.

## Các biến thể phổ biến và trường hợp đặc biệt

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Multiple shapes** | Lặp qua `worksheet.getShapes()` và gọi `save` cho mỗi shape, hoặc chọn bằng `shape.getName()`. |
| **Shape is a chart with data series** | Sử dụng `exportOptions.setExportChartAsEditable(true)` để giữ series có thể chỉnh sửa. |
| **Need a specific slide layout** | Sau khi lưu, mở PPTX bằng Aspose.Slides và chèn shape vào layout tùy chỉnh. |
| **Large workbook** | Chỉ tải worksheet cần thiết bằng `Workbook(String, LoadOptions)` để giảm tiêu thụ bộ nhớ. |
| **Different output format (PDF, PNG)** | Thay đổi `exportOptions.setSaveFormat(SaveFormat.PDF)` hoặc `SaveFormat.PNG`. Điều này hữu ích khi bạn **convert Excel chart** thành hình ảnh tĩnh thay vì shape PowerPoint. |

**Mẹo:** Luôn kiểm tra chỉ số shape (`get(0)`) có khớp với phần tử trực quan bạn muốn xuất không. Thứ tự trong collection shape phản ánh thứ tự chèn trong Excel, có thể khác với thứ tự xếp chồng trực quan.

## Cách xuất shape từ Excel sang PowerPoint – danh sách kiểm tra khắc phục sự cố

* **File not found** – Đảm bảo đường dẫn trong `new Workbook()` trỏ tới tệp `.xls` hoặc `.xlsx` tồn tại.  
* **No shapes returned** – Xác nhận worksheet thực sự chứa shape; bạn có thể gọi `worksheet.getShapes().getCount()` để debug.  
* **Exported file is empty** – Kiểm tra rằng `exportOptions.setSaveFormat(SaveFormat.PPTX)` đã được đặt; sử dụng định dạng hình ảnh sẽ tạo ra một bức ảnh thay vì shape.  
* **Compatibility issues** – Aspose.Cells 24.9+ hỗ trợ xuất PPTX trên tất cả các nền tảng chính. Nâng cấp nếu gặp `UnsupportedOperationException`.

## Kết luận

Bây giờ bạn đã biết **how to export shape** từ một workbook Excel và nhúng nó vào bản thuyết trình PowerPoint bằng Java. Tutorial đã bao gồm việc tải workbook, tìm shape, cấu hình các tùy chọn **export shape from Excel**, và cuối cùng **save shape PPTX**. Với nền tảng này, bạn có thể tự động tạo báo cáo, xây dựng dashboard, hoặc tích hợp hình ảnh Excel vào các slide mà không cần sao chép‑dán thủ công.

### Các bước tiếp theo

* Khám phá **convert Excel chart** sang các định dạng Office khác như PDF hoặc DOCX.  
* Kết hợp kỹ thuật này với Aspose.Slides để đặt nhiều shape trên một slide duy nhất.  
* Thử nghiệm các thuộc tính của `ImageOrPrintOptions` (ví dụ, `setResolution`, `setTransparent`) để tinh chỉnh chất lượng hình ảnh của shape đã xuất.

Bạn có thể tự do điều chỉnh mã cho xử lý hàng loạt hoặc tích hợp vào dịch vụ báo cáo lớn hơn. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách xuất shape với ShapeExportOptions trong Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [Cách xuất sheet Excel sang PowerPoint với Aspose.Cells trong Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [Cách xuất biểu đồ từ Excel sang PowerPoint – Hướng dẫn Java đầy đủ](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}