---
category: general
date: 2026-11-25
description: Tìm hiểu cách xuất Excel sang PPTX với các hình dạng có thể chỉnh sửa.
  Hướng dẫn này cũng chỉ cách thiết lập khu vực in và chuyển đổi biểu đồ Excel cho
  các bài thuyết trình.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: vi
lastmod: 2026-11-25
og_description: Cách xuất Excel sang PPTX với các hình dạng có thể chỉnh sửa bằng
  Aspose.Cells, kèm các mẹo thiết lập vùng in và chuyển đổi biểu đồ Excel cho bản
  trình bày.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Cách xuất Excel sang PPTX với các hình dạng có thể chỉnh sửa
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Cách xuất Excel sang PPTX với các hình dạng có thể chỉnh sửa
url: /vi/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất Excel sang PPTX với các hình dạng có thể chỉnh sửa

Nếu bạn cần **how to export Excel** tệp tin sang PowerPoint trong khi giữ nguyên các hộp văn bản và hình dạng có thể chỉnh sửa, hướng dẫn này sẽ đưa bạn qua toàn bộ quá trình. Bạn cũng sẽ học cách **set print area** cho một slide tập trung và cách **convert Excel chart** các đối tượng sao cho chúng vẫn có thể chỉnh sửa hoàn toàn sau khi xuất.

Xuất Excel sang PPTX là phổ biến khi xây dựng bộ trình chiếu từ các báo cáo dựa trên dữ liệu. Bằng cách sử dụng Aspose.Cells cho Java, bạn tránh việc sao chép‑dán thủ công, giữ nguyên định dạng và có được kiểm soát lập trình đối với kết quả.

## Những gì bạn sẽ học

* Tải một workbook XLSX hiện có chứa hộp văn bản hoặc biểu đồ.  
* Cấu hình các tùy chọn xuất để tệp PPTX kết quả chứa **editable shapes**.  
* **Set the print area** để giới hạn phạm vi xuất chỉ các ô bạn cần.  
* Lưu worksheet dưới dạng tệp PPTX và xác minh rằng các hộp văn bản và biểu đồ có thể được chỉnh sửa trong PowerPoint.  

**Yêu cầu trước**

* Java 17 hoặc mới hơn đã được cài đặt.  
* Maven hoặc Gradle để quản lý phụ thuộc.  
* Kiến thức cơ bản về workbook Excel và lập trình Java.

---

## Cách xuất Excel sang PPTX với các hình dạng có thể chỉnh sửa

Phần này cung cấp mã cốt lõi thực hiện việc xuất. Ví dụ sử dụng Aspose.Cells 23.9 (phiên bản mới nhất tại thời điểm viết) và trình bày mọi bước cần thiết.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### Tại sao mỗi dòng lại quan trọng

1. **Dependency** – Aspose.Cells cung cấp lớp `ImageOrPrintOptions` có thể render các worksheet thành slide PPTX. Thêm nó qua Maven đảm bảo thư viện có trong classpath.  
2. **Imports** – Nhập các lớp đúng giúp mã sạch sẽ và tránh việc dùng tên đầy đủ.  
3. **Loading the workbook** – Bạn phải chỉ đến tệp chính xác chứa các đối tượng muốn xuất. Đường dẫn có thể là tuyệt đối hoặc tương đối so với thư mục gốc của dự án.  
4. **Export options** – Thiết lập `setEditable(true)` là chìa khóa để **how to export Excel** sao cho các hình dạng PowerPoint kết quả vẫn có thể chỉnh sửa. Nếu không bật cờ này, hộp văn bản sẽ trở thành hình ảnh tĩnh.  
5. **Print area** – Lệnh `setPrintArea` giới hạn việc xuất chỉ trong vùng bạn quan tâm, giảm kích thước tệp và loại bỏ các hàng/cột không cần. Điều này trực tiếp đáp ứng yêu cầu **set print area excel**.  
6. **Saving** – Hằng số `SaveFormat.PPTX` thông báo cho Aspose.Cells tạo tệp PowerPoint thay vì hình ảnh hay PDF.  

#### Kết quả mong đợi

Sau khi chạy chương trình, mở `EditableShapes.pptx` trong PowerPoint. Bạn sẽ thấy một slide phản ánh phạm vi Excel đã chọn, và bất kỳ hộp văn bản hay chú giải biểu đồ nào cũng có thể nhấp đúp và chỉnh sửa giống như các đối tượng PowerPoint gốc.

---

## Đặt vùng in (print area) trong Excel

Khi bạn chỉ cần một phần của worksheet, việc xác định **print area** cải thiện cả hiệu năng và độ rõ hình ảnh.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* Nếu sau này bạn thay đổi phạm vi dữ liệu, hãy gọi lại `setPrintArea` trước khi xuất. Việc xuất sẽ tuân theo cài đặt mới nhất.

---

## Chuyển đổi biểu đồ XLSX thành biểu đồ PowerPoint có thể chỉnh sửa

Aspose.Cells coi biểu đồ là các đối tượng vẽ. Bằng cách bật `setEditable(true)`, biểu đồ sẽ được chuyển thành biểu đồ PowerPoint gốc có thể chỉnh sửa (ví dụ: thay đổi series, tiêu đề trục).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

Nếu bạn cần **how to convert xlsx** các tệp chứa nhiều biểu đồ, hãy lặp lại quá trình xuất cho mỗi worksheet hoặc sử dụng `Workbook.save` với `SaveFormat.PPTX` sau khi điều chỉnh sheet hoạt động.

---

## Cách chuyển đổi XLSX bằng lập trình (bonus)

Ngoài PPTX, bạn cũng có thể muốn chuyển đổi workbook sang định dạng khác như PDF hoặc PNG. Lớp `ImageOrPrintOptions` tương tự hoạt động cho các mục tiêu đó:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

Điều này minh họa khả năng **how to convert xlsx** rộng hơn của Aspose.Cells.

---

## Các lỗi thường gặp và mẹo thực hành tốt

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| Hình dạng trở thành hình ảnh | `setEditable(false)` (mặc định) | Gọi `exportOptions.setEditable(true)` |
| Slide xuất ra trống | Vùng in không bao gồm dữ liệu nào | Xác minh chuỗi phạm vi được truyền vào `setPrintArea` |
| Biểu đồ mất định dạng | Sử dụng phiên bản Aspose.Cells lỗi thời | Nâng cấp lên thư viện mới nhất (≥ 23.9) |
| Kích thước tệp lớn | Xuất toàn bộ worksheet | Giới hạn vùng in hoặc ẩn các hàng/cột không dùng |

---

## Kết luận

Bạn giờ đã biết **how to export Excel** workbook sang PPTX với các hình dạng và biểu đồ hoàn toàn có thể chỉnh sửa, cách **set print area** để tập trung đầu ra, và cách **convert Excel chart** các đối tượng để chỉnh sửa bản trình chiếu liền mạch. Ví dụ Java đầy đủ, có thể chạy ở trên có thể được chèn vào bất kỳ dự án nào đã sử dụng Aspose.Cells.

**Các bước tiếp theo**

* Khám phá các tùy chọn **convert excel chart** trong PowerPoint (ví dụ: thay đổi loại biểu đồ).  
* Kết hợp việc xuất này với tự động hoá **set print area excel** để tạo nhiều slide từ một workbook duy nhất.  
* Thử xuất sang các định dạng khác (PDF, PNG) bằng cùng mẫu `ImageOrPrintOptions`.

Hãy tự do thử nghiệm với các phạm vi khác nhau, nhiều worksheet, hoặc bố cục slide tùy chỉnh. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách đặt vùng in excel và xuất sang PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Chuyển đổi Excel sang PowerPoint và đặt vùng in](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Đặt vùng in trong Excel và xuất sang PowerPoint – Hướng dẫn từng bước](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}