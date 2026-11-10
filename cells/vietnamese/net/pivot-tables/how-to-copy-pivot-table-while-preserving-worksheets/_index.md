---
category: general
date: 2026-09-15
description: Tìm hiểu cách sao chép bảng pivot, sao chép worksheet có pivot và lưu
  workbook dưới dạng pptx bằng Aspose.Cells trong C#. Hướng dẫn chi tiết từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: vi
lastmod: 2026-09-15
og_description: Cách sao chép bảng pivot, sao chép worksheet có pivot và lưu workbook
  dưới dạng pptx bằng Aspose.Cells. Tham khảo các ví dụ C# đầy đủ, có thể chạy được.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Cách sao chép bảng pivot và xuất các trang tính – hướng dẫn đầy đủ C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách sao chép bảng tổng hợp mà vẫn giữ nguyên các bảng tính
url: /vi/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sao chép pivot table trong khi giữ nguyên các worksheet

Nếu bạn cần **how to copy pivot table** từ một workbook sang workbook khác mà không mất pivot cache nền, hướng dẫn này cung cấp một giải pháp sẵn sàng chạy. Bạn cũng sẽ thấy cách **copy worksheet with pivot** và cách **save workbook as pptx** trong khi giữ nguyên các textbox có thể chỉnh sửa. Tất cả các ví dụ sử dụng Aspose.Cells for .NET mới nhất, vì vậy bạn có thể chèn mã vào bất kỳ dự án C# nào và thấy kết quả ngay lập tức.

Làm việc với các tệp Excel một cách lập trình thường liên quan đến việc di chuyển dữ liệu giữa các workbook, xuất ra bản trình chiếu, hoặc chèn Smart Markers phức tạp. Ba đoạn mã dưới đây bao phủ các kịch bản phổ biến này và giải thích lý do mỗi bước quan trọng.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn đã được cài đặt  
* Aspose.Cells for .NET (phiên bản 25.11 hoặc mới hơn) được tham chiếu trong dự án của bạn  
* Một thư mục có tên `YOUR_DIRECTORY` nơi các tệp mẫu sẽ được đọc và ghi  

Không cần thêm bất kỳ gói NuGet nào.

---

## Cách sao chép pivot table với Aspose.Cells

Sao chép một vùng chứa pivot table trong khi giữ nguyên pivot cache là một yêu cầu thường gặp. Các bước sau đây minh họa chuỗi thao tác chính xác mà bạn cần.

### Bước 1 – Tải workbook nguồn chứa pivot table

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Why*: Aspose.Cells đọc workbook vào bộ nhớ, cho phép bạn truy cập vào worksheets, cells và pivot tables.

### Bước 2 – Tạo một workbook đích rỗng

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Why*: Bắt đầu với một workbook trống đảm bảo không có style ẩn hoặc named ranges can thiệp vào quá trình sao chép.

### Bước 3 – Sao chép các hàng chứa pivot table

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Why*: `CopyRows` sao chép giá trị thô của các ô, định dạng và các tham chiếu pivot cache nền. Vùng cần bao gồm toàn bộ khu vực của pivot table.

### Bước 4 – Sao chép các cột chứa pivot table

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Why*: Pivot table trải rộng cả hàng và cột; sao chép các cột đảm bảo bố cục toàn bộ bảng được giữ nguyên.

### Bước 5 – Chuyển sheet đã chuẩn bị vào workbook đích

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Why*: Phương thức `Copy` sao chép worksheet, bao gồm cả pivot cache, vì vậy workbook đích hiển thị một pivot table giống hệt.

### Bước 6 – Lưu kết quả – pivot table vẫn nguyên vẹn

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Why*: Lưu workbook sẽ ghi tất cả các cấu trúc nội bộ, đảm bảo pivot có thể được làm mới sau này.

**Mẹo**: Sau khi sao chép, bạn có thể gọi `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` để cập nhật dữ liệu nếu dữ liệu nguồn đã thay đổi.

---

## Sao chép worksheet với pivot – một cách thay thế ngắn gọn

Nếu bạn chỉ cần sao chép toàn bộ worksheet đã chứa pivot table, bạn có thể bỏ qua các bước sao chép hàng/cột và sử dụng trực tiếp phương thức `Copy` ở mức worksheet.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Cách tiếp cận này hữu ích khi worksheet không chứa dữ liệu bổ sung ngoài khu vực pivot. Thao tác **copy worksheet with pivot** tự động giữ nguyên mọi định dạng, named ranges và pivot caches.

---

## Lưu workbook dưới dạng PPTX với các textbox có thể chỉnh sửa

Xuất một sheet Excel chứa textbox có thể chỉnh sửa sang PowerPoint có thể cần cho các bảng điều khiển báo cáo. Đoạn mã dưới đây hiển thị **save workbook as pptx** trong khi giữ textbox có thể chỉnh sửa.

### Bước 1 – Tải workbook có chứa textbox

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Bước 2 – Cấu hình tùy chọn lưu PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Why*: Thiết lập `ExportEditableTextBox` cho Aspose.Cells biết chuyển đổi textbox Excel thành một shape PowerPoint vẫn có thể chỉnh sửa sau khi xuất.

### Bước 3 – Lưu workbook dưới dạng PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Kết quả mong đợi**: Mở `Result.pptx` trong PowerPoint, chọn textbox và chỉnh sửa nội dung như bất kỳ shape gốc nào.

**Câu hỏi thường gặp**: *Nếu tôi muốn giữ textbox bị khóa thì sao?*  
Đặt `pptxOptions.ExportEditableTextBox = false`; shape sẽ được chuyển thành hình ảnh tĩnh.

---

## Xuất Smart Marker chứa mảng JSON dưới dạng giá trị một ô duy nhất

Smart Markers cho phép bạn điền dữ liệu vào các mẫu Excel với cấu trúc dữ liệu phức tạp. Dưới đây là một ví dụ đầy đủ minh họa cách xử lý dữ liệu kiểu **how to copy pivot table** khi chèn một mảng JSON vào một ô duy nhất.

### Bước 1 – Chuẩn bị SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Bước 2 – Chèn Smart Marker vào ô A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Bước 3 – Định nghĩa nguồn dữ liệu với mảng kiểu JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Bước 4 – Xử lý workbook

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Bước 5 – Lưu workbook kết quả

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Xác nhận kết quả**: Mở `JsonSingleCell.xlsx` và xác nhận ô A1 hiển thị `A,B,C`. Điều này minh họa cách xử lý một collection thành giá trị một ô duy nhất, một mẫu thường cần khi xuất dữ liệu cho các hệ thống downstream.

---

## Ví dụ hoạt động đầy đủ

Dưới đây là một chương trình duy nhất kết hợp ba kịch bản. Bạn có thể sao chép mã vào một ứng dụng console, điều chỉnh các đường dẫn tệp và chạy nó để xem cả ba kết quả.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Chạy chương trình này sẽ tạo ra:

* `CopyWithPivot.xlsx` – một bản sao hoàn hảo của pivot table gốc.  
* `Result.pptx` – một slide PowerPoint với textbox có thể chỉnh sửa.  
* `JsonSingleCell.xlsx` – một sheet nơi mảng JSON xuất hiện trong một ô duy nhất.

---

## Kết luận

Bây giờ bạn đã biết cách **how to copy pivot table** một cách an toàn, cách **copy worksheet with pivot** trong một lần gọi, và cách **save workbook as pptx** trong khi giữ nguyên các textbox có thể chỉnh sửa. Những mẫu này bao phủ các quy trình làm việc Excel‑to‑PowerPoint và Excel‑to‑JSON phổ biến nhất mà bạn sẽ gặp trong các dự án tự động hoá doanh nghiệp.

Tiếp theo, hãy xem xét khám phá:

* Làm mới các pivot table đã sao chép bằng lập trình (`PivotTable.Refresh()`)  
* Xuất ra các định dạng khác như PDF hoặc HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Sử dụng các tùy chọn Smart Marker nâng cao như hàm tùy chỉnh hoặc định dạng có điều kiện  

Bạn có thể tự do thử nghiệm với các vùng khác nhau, nhiều worksheet, hoặc cấu trúc JSON lớn hơn. Aspose.Cells API cung cấp kiểm soát chi tiết, vì vậy bạn có thể điều chỉnh các ví dụ này cho bất kỳ kịch bản thực tế nào. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Workbook Mới – Cách Sao chép Worksheet có Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Cách Sao chép Pivot Table trong C# – Chuyển Excel sang PPTX, Sao chép Range & Tạo Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Sao chép Sheets trong Workbook bằng Aspose.Cells cho .NET - Hướng dẫn Từng Bước](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}