---
category: general
date: 2026-08-20
description: Tìm hiểu cách đặt vùng in trong Excel, sau đó xuất Excel sang PPTX bằng
  Aspose.Cells. Hướng dẫn này sẽ chỉ cho bạn cách chuyển đổi một worksheet sang PowerPoint
  và lưu dưới dạng PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: vi
lastmod: 2026-08-20
og_description: Đặt khu vực in trong Excel và sau đó xuất Excel sang PPTX bằng Aspose.Cells.
  Hãy làm theo hướng dẫn từng bước này để chuyển đổi một worksheet sang PowerPoint
  và lưu dưới dạng tệp PPTX.
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: Cài đặt vùng in trong Excel và xuất sang PowerPoint – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: Cách thiết lập vùng in trong Excel và xuất sang PowerPoint
url: /vi/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách đặt khu vực in trong Excel và xuất sang PowerPoint

Nếu bạn cần **set print area excel** trước khi chia sẻ dữ liệu trong một bộ slide, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy cách cấu hình khu vực in, sau đó **export excel to pptx** trong khi giữ các hộp văn bản có thể chỉnh sửa, vì vậy PowerPoint tạo ra sẵn sàng cho việc chỉnh sửa tiếp theo.

Chúng tôi sẽ sử dụng Aspose.Cells for Java để **convert worksheet to PowerPoint** và cuối cùng **save worksheet as PowerPoint** ở định dạng PPTX. Không cần thư viện bổ sung nào ngoài Aspose.Cells JAR. Khi kết thúc hướng dẫn này, bạn có thể chạy mã trên bất kỳ môi trường tương thích Java nào và tạo một bản trình bày phản ánh phạm vi Excel đã chọn.

## Yêu cầu trước

- Java Development Kit 17 hoặc mới hơn  
- Aspose.Cells for Java (tải xuống từ trang chính thức của Aspose)  
- Một workbook Excel chứa các shape mà bạn muốn giữ có thể chỉnh sửa (ví dụ, `BookWithShapes.xlsx`)  

Make sure the Aspose.Cells JAR is on your classpath:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## Bước 1: Đặt khu vực in trong Excel bằng Aspose.Cells

Bước đầu tiên là xác định phạm vi sẽ được xuất. Đặt khu vực in giới hạn việc chuyển đổi chỉ trong các ô bạn quan tâm và cải thiện hiệu suất.

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**Why this matters** – Phương thức `setPrintArea` cho Aspose.Cells biết ô nào thuộc trang có thể in. Khi bạn sau này **export excel to pptx**, chỉ khu vực này được render, vì vậy dữ liệu thừa sẽ không xuất hiện trên slide.

### Mẹo chuyên nghiệp
Nếu bạn cần một phạm vi động, bạn có thể tính địa chỉ một cách lập trình:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## Bước 2: Xuất Excel sang PPTX với các hộp văn bản có thể chỉnh sửa

Sau khi khu vực in đã được xác định, cấu hình các tùy chọn xuất. Bật `setExportEditableTextBoxes` giữ lại văn bản của shape dưới dạng các trường có thể chỉnh sửa trong PowerPoint.

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**Why this matters** – Mặc định Aspose.Cells rasterizes (chuyển đổi) các hộp văn bản thành hình ảnh. Đặt `ExportEditableTextBoxes` thành `true` giữ lại các đối tượng shape gốc, cho phép người dùng chỉnh sửa văn bản trực tiếp trong PowerPoint.

## Bước 3: Chuyển đổi worksheet sang PowerPoint và lưu tệp

Bây giờ thực hiện việc chuyển đổi thực tế. Phương thức `Workbook.save` nhận tên tệp đích và các tùy chọn đã chuẩn bị trước.

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

Khi mã hoàn thành, `SheetWithEditableShapes.pptx` chứa một slide duy nhất phản ánh khu vực in đã định nghĩa (`A1:G30`). Tất cả các shape, bao gồm cả hộp văn bản, vẫn có thể chỉnh sửa.

### Kết quả mong đợi
Open the generated PPTX in Microsoft PowerPoint:

- Slide hiển thị các ô từ **A1 đến G30** chính xác như trong Excel.  
- Bất kỳ shape nào có trong worksheet gốc sẽ xuất hiện dưới dạng shape PowerPoint.  
- Văn bản bên trong các shape đó có thể chỉnh sửa trực tiếp trong PowerPoint (không rasterization).

## Bước 4: Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh. Thay thế `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế trên máy của bạn.

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

Chạy chương trình như mô tả trong phần *Yêu cầu trước*. Tệp PowerPoint được tạo sẽ được đặt trong cùng thư mục bạn đã chỉ định.

## Câu hỏi thường gặp và các trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| **Tôi có thể xuất nhiều worksheet không?** | Có. Lặp qua `workbook.getWorksheets()` và gọi `save` cho mỗi sheet, tùy chọn thay đổi tên tệp đầu ra. |
| **Nếu workbook của tôi chứa biểu đồ thì sao?** | Biểu đồ được render dưới dạng hình ảnh theo mặc định. Để giữ chúng có thể chỉnh sửa, bạn cần chuyển chúng thành shape PowerPoint một cách thủ công, điều này nằm ngoài phạm vi của hướng dẫn này. |
| **Khu vực in có bắt buộc không?** | Không. Nếu bạn bỏ qua `setPrintArea`, Aspose.Cells sẽ xuất toàn bộ phạm vi đã sử dụng của worksheet. Đặt nó sẽ cho bạn kiểm soát chính xác. |
| **Điều này có hoạt động với các tệp .xlsx được tạo bởi công cụ khác không?** | Hoàn toàn có. Aspose.Cells hỗ trợ bất kỳ workbook Office Open XML hợp lệ nào, bất kể nguồn gốc. |

## Các bước tiếp theo

- **Save worksheet as PowerPoint** với bố cục slide tùy chỉnh: khám phá lớp `Presentation` từ Aspose.Slides để hợp nhất slide đã xuất vào một bộ slide lớn hơn.  
- **Export excel to pptx** với độ phân giải hình ảnh khác nhau: điều chỉnh `exportOptions.setResolution(300)` để có đầu ra DPI cao.  
- **Automate batch conversions**: kết hợp mã này với một file‑watcher để xử lý nhiều tệp Excel trong một thư mục.

Bằng cách thành thạo **set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint**, và **save worksheet as powerpoint**, bạn có thể tích hợp dữ liệu Excel vào các bộ slide một cách lập trình, tối ưu hoá quy trình báo cáo và giảm công việc sao chép‑dán thủ công.

---

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn thành thạo các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách đặt khu vực in trong Excel bằng Aspose.Cells cho .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Đặt khu vực in Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Đặt khu vực in Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}