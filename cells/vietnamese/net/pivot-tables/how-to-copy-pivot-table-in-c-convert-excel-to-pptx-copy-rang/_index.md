---
category: general
date: 2026-01-14
description: Cách sao chép bảng pivot bằng Aspose.Cells và đồng thời học cách chuyển
  đổi Excel sang PPTX, sao chép vùng dữ liệu sang sổ làm việc khác, và làm cho textbox
  có thể chỉnh sửa trong PPTX trong một hướng dẫn duy nhất.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: vi
og_description: Cách sao chép bảng pivot, sau đó chuyển đổi Excel sang PPTX, sao chép
  phạm vi sang sổ làm việc khác và làm cho textbox có thể chỉnh sửa trong PPTX—tất
  cả đều bằng Aspose.Cells.
og_title: Cách sao chép Pivot Table trong C# – Hướng dẫn đầy đủ chuyển Excel sang
  PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Cách sao chép Pivot Table trong C# – Chuyển đổi Excel sang PPTX, sao chép vùng
  dữ liệu và làm hộp văn bản có thể chỉnh sửa
url: /vi/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sao Chép Pivot Table trong C# – Hướng Dẫn Đầy Đủ Từ Excel tới PPTX

Cách sao chép pivot table từ một workbook sang workbook khác là một câu hỏi thường gặp khi bạn tự động hoá các báo cáo dựa trên Excel. Trong tutorial này chúng ta sẽ đi qua ba kịch bản thực tế sử dụng **Aspose.Cells for .NET**: sao chép một vùng pivot‑table, xuất một worksheet ra file PPTX với textbox có thể chỉnh sửa, và đưa một mảng JSON vào một ô duy nhất bằng Smart Markers.  

Bạn cũng sẽ thấy cách **chuyển đổi Excel sang PPTX**, **sao chép vùng sang workbook khác**, và **tạo textbox có thể chỉnh sửa trong PPTX** mà không làm mất định dạng. Khi kết thúc, bạn sẽ có một bộ mã sẵn sàng chạy mà có thể chèn vào bất kỳ dự án .NET nào.

> **Mẹo chuyên nghiệp:** Tất cả các ví dụ nhắm tới Aspose.Cells 23.12, nhưng các khái niệm tương tự áp dụng cho các phiên bản trước với một vài thay đổi nhỏ trong API.

![Diagram showing how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## Những Gì Bạn Cần Chuẩn Bị

- Visual Studio 2022 (hoặc bất kỳ IDE C# nào)
- .NET 6.0 hoặc runtime mới hơn
- Gói NuGet Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Hai file Excel mẫu (`source.xlsx`, `chartWithTextbox.xlsx`) đặt trong một thư mục bạn quản lý (thay `YOUR_DIRECTORY` bằng đường dẫn thực tế của bạn).

Không cần thư viện bổ sung nào; cùng một assembly `Aspose.Cells` sẽ xử lý Excel, PPTX và Smart Markers.

---

## Cách Sao Chép Pivot Table và Giữ Nguyên Dữ Liệu

Khi bạn sao chép một vùng chứa pivot table, hành vi mặc định là chỉ dán **giá trị**. Để giữ nguyên định nghĩa pivot, bạn phải bật cờ `CopyPivotTable`.

### Các Bước Thực Hiện

1. **Tải workbook nguồn** chứa pivot table.  
2. **Tạo một workbook đích trống** – sẽ nhận vùng đã sao chép.  
3. **Sử dụng `CopyRange` với `CopyPivotTable = true`** để định nghĩa pivot đi cùng dữ liệu.  
4. **Lưu file đích** ở vị trí bạn muốn.

#### Ví Dụ Mã Đầy Đủ

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Tại sao cách này hoạt động:**  
`CopyOptions.CopyPivotTable` báo cho Aspose.Cells sao chép đối tượng `PivotTable` bên dưới thay vì chỉ các giá trị đã render. Workbook đích giờ đã chứa một pivot hoàn chỉnh, bạn có thể refresh hoặc chỉnh sửa nó bằng mã.

**Trường hợp đặc biệt:** Nếu workbook nguồn dùng nguồn dữ liệu bên ngoài, bạn có thể cần nhúng dữ liệu hoặc điều chỉnh chuỗi kết nối sau khi sao chép, nếu không pivot sẽ hiển thị “#REF!”.

---

## Chuyển Đổi Excel sang PPTX và Tạo Textbox Có Thể Chỉnh Sửa

Xuất một worksheet ra PowerPoint rất tiện cho việc tạo slide deck trực tiếp từ dữ liệu. Mặc định textbox được xuất sẽ là một shape tĩnh, nhưng thiết lập `IsTextBoxEditable` sẽ thay đổi hành vi này.

### Các Bước Thực Hiện

1. **Mở workbook** chứa biểu đồ và textbox bạn muốn xuất.  
2. **Cấu hình `ImageOrPrintOptions`** với `SaveFormat = SaveFormat.Pptx`.  
3. **Xác định khu vực in** bao gồm textbox.  
4. **Bật `IsTextBoxEditable`** để văn bản có thể chỉnh sửa sau khi mở PPTX.  
5. **Lưu file PPTX**.

#### Ví Dụ Mã Đầy Đủ

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Kết quả:** Mở `result.pptx` trong PowerPoint – textbox bạn đặt trong Excel sẽ trở thành một textbox thông thường mà bạn có thể gõ chữ vào. Không cần tạo lại thủ công.

**Những lỗi thường gặp:** Nếu worksheet có các ô đã gộp cắt ngang khu vực in, slide kết quả có thể bị lệch. Hãy điều chỉnh khu vực in hoặc tách các ô đã gộp trước khi xuất.

---

## Sao Chép Vùng Sang Workbook Khác với Smart Markers (JSON → Ô Đơn)

Đôi khi bạn cần nhúng một mảng JSON vào một ô Excel duy nhất, ví dụ khi truyền dữ liệu tới hệ thống downstream yêu cầu chuỗi JSON. Smart Markers của Aspose.Cells có thể tuần tự hoá mảng thành một ô duy nhất khi bạn đặt `ArrayAsSingle = true`.

### Các Bước Thực Hiện

1. **Tải một workbook mẫu** chứa placeholder Smart Marker (ví dụ `&=Items.Name`).  
2. **Chuẩn bị đối tượng dữ liệu** – một kiểu ẩn danh có mảng `Items`.  
3. **Tạo một `SmartMarkerProcessor`** và áp dụng dữ liệu với `ArrayAsSingle`.  
4. **Lưu workbook đã được điền dữ liệu**.

#### Ví Dụ Mã Đầy Đủ

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Giải thích:**  
Khi `ArrayAsSingle` được bật, Aspose.Cells nối từng phần tử của `Items.Name` thành một chuỗi dạng JSON (`["A","B"]`) và ghi vào ô chứa smart marker. Điều này tránh việc tạo một hàng riêng cho mỗi phần tử của mảng.

**Khi nào nên dùng:** Thích hợp cho việc xuất bảng cấu hình, payload API, hoặc bất kỳ trường hợp nào mà người tiêu thụ mong muốn một chuỗi JSON gọn gàng thay vì bố cục dạng bảng.

---

## Mẹo Bổ Sung & Xử Lý Các Trường Hợp Đặc Biệt

| Kịch bản | Điều Cần Lưu Ý | Giải Pháp Đề Xuất |
|----------|-------------------|---------------|
| **Pivot Table lớn** | Tiêu thụ bộ nhớ tăng mạnh khi sao chép cache pivot khổng lồ. | Sử dụng `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` trước khi tải. |
| **Xuất sang PPTX có ảnh** | Ảnh có thể bị raster hoá ở DPI thấp. | Đặt `pptxOptions.ImageResolution = 300` để có slide sắc nét hơn. |
| **Định dạng JSON Smart Marker** | Các ký tự đặc biệt (`"` , `\`) làm hỏng JSON. | Escape chúng thủ công hoặc dùng `JsonSerializer` để serialize trước khi đưa vào Smart Markers. |
| **Sao chép vùng giữa các phiên bản Excel khác nhau** | Các file `.xls` cũ có thể mất định dạng. | Lưu file đích dưới dạng `.xlsx` để bảo toàn các tính năng hiện đại. |

---

## Tóm Tắt – Cách Sao Chép Pivot Table và Nhiều Hơn Thế Nữa

Chúng ta đã bắt đầu bằng việc trả lời **cách sao chép pivot table** trong khi giữ nguyên chức năng, sau đó giới thiệu **cách chuyển đổi Excel sang PPTX**, **tạo textbox có thể chỉnh sửa trong PPTX**, và cuối cùng là **cách sao chép vùng sang workbook khác** bằng Smart Markers để nhúng một mảng JSON vào một ô duy nhất.  

Ba đoạn mã đều độc lập; bạn có thể dán chúng vào một ứng dụng console mới, chỉnh sửa đường dẫn file, và chạy ngay hôm nay.

---

## Tiếp Theo Bạn Nên Làm Gì?

- **Khám phá các định dạng xuất khác** – Aspose.Cells còn hỗ trợ PDF, XPS và HTML.  
- **Refresh pivot table bằng mã** sử dụng `PivotTable.RefreshData()` sau khi sao chép.  
- **Kết hợp Smart Markers với biểu đồ** để tạo dashboard động tự động cập nhật.  

Nếu bạn quan tâm tới **lưu workbook dưới dạng PPTX** với bố cục slide tùy chỉnh, hãy xem tài liệu Aspose.Cells về `SlideOptions`.  

Hãy thoải mái thử nghiệm—đổi khu vực in, thay đổi các tùy chọn `CopyOptions`, hoặc đưa vào payload JSON phức tạp hơn. API đủ linh hoạt cho hầu hết các pipeline báo cáo.

---

### Câu Hỏi Thường Gặp

**Hỏi: `CopyPivotTable` có sao chép slicer không?**  
Đáp: Không trực tiếp. Slicer là các đối tượng riêng; sau khi sao chép bạn cần tạo lại chúng hoặc sao chép qua bộ sưu tập `Worksheet.Shapes`.

**Hỏi: Tôi có thể xuất nhiều worksheet vào một PPTX duy nhất không?**  
Đáp: Có. Lặp qua từng worksheet, gọi `Save` với cùng một `ImageOrPrintOptions` và đặt `pptxOptions.StartSlideNumber` để tiếp tục đánh số slide.

**Hỏi: Nếu mảng JSON của tôi chứa các đối tượng lồng nhau thì sao?**  
Đáp: Đặt `ArrayAsSingle = false` và sử dụng template tùy chỉnh để lặp qua cấu trúc lồng nhau.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}