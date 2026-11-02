---
category: general
date: 2026-09-11
description: Sao chép bảng pivot và xuất Excel sang PPTX bằng Aspose.Cells. Tìm hiểu
  cách tạo PPTX có thể chỉnh sửa và lưu workbook dưới dạng PPTX trong C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: vi
lastmod: 2026-09-11
og_description: Sao chép bảng pivot và xuất Excel sang PPTX trong C# bằng Aspose.Cells.
  Tạo PPTX có thể chỉnh sửa và lưu workbook dưới dạng PPTX chỉ với vài dòng mã.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Sao chép bảng pivot và xuất Excel sang PPTX – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Sao chép bảng pivot và xuất Excel sang PPTX với Aspose.Cells
url: /vi/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sao chép bảng tổng hợp và xuất Excel sang PPTX với Aspose.Cells

Nếu bạn cần sao chép một bảng tổng hợp từ một bảng tính này sang bảng tính khác và sau đó xuất tệp Excel sang bản trình bày PowerPoint, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Sử dụng Aspose.Cells, bạn có thể tạo một tệp PPTX có thể chỉnh sửa và lưu workbook dưới dạng PPTX chỉ với vài dòng mã C#.

Hướng dẫn bao gồm mọi bước cần thiết để di chuyển bảng tổng hợp, giữ nguyên chức năng của nó, và tạo một tệp PPTX trong đó biểu đồ và các hình dạng vẫn có thể chỉnh sửa. Không cần công cụ bên ngoài—chỉ cần thư viện Aspose.Cells và môi trường phát triển .NET.

## Những gì bạn sẽ đạt được

* **Sao chép bảng tổng hợp** từ sheet nguồn sang sheet đích trong khi giữ nguyên tất cả các kết nối dữ liệu.  
* **Xuất Excel sang PPTX** để slide tạo ra có thể được chỉnh sửa trong PowerPoint.  
* **Tạo PPTX có thể chỉnh sửa** trong đó biểu đồ, bảng và hình dạng không bị chuyển thành hình ảnh.  
* **Lưu workbook dưới dạng PPTX** bằng cùng một lời gọi API của Aspose.Cells.  

### Yêu cầu trước

* .NET 6.0 trở lên (mã cũng hoạt động với .NET Framework 4.6+).  
* Aspose.Cells cho .NET (gói NuGet `Aspose.Cells`).  
* Kiến thức cơ bản về ứng dụng console C#.  

> **Mẹo chuyên nghiệp:** Cài đặt gói NuGet qua CLI để đảm bảo bạn có phiên bản mới nhất:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Cách sao chép bảng tổng hợp giữa các worksheet

Hoạt động đầu tiên là di chuyển bảng tổng hợp trong khi giữ nguyên định nghĩa của nó. Aspose.Cells cung cấp phương thức `CopyRange` với đối tượng `CopyOptions` bao gồm cờ `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Tại sao cách này hoạt động:**  
`CopyRange` sao chép dữ liệu ô, định dạng, và khi `CopyPivotTable` là true, bộ nhớ đệm và siêu dữ liệu của bảng tổng hợp. Phạm vi đích bắt đầu tại ô `A1` (hàng 0, cột 0) nhưng bạn có thể thay đổi offset để đặt bảng tổng hợp ở vị trí khác.

**Trường hợp đặc biệt thường gặp:** Nếu sheet đích đã chứa một bảng tổng hợp có cùng tên, Aspose.Cells sẽ tự động đổi tên bảng mới, tránh xung đột tên.

## Xuất Excel sang PPTX và tạo PPTX có thể chỉnh sửa

Sau khi bảng tổng hợp đã ở vị trí, bạn có thể xuất toàn bộ workbook thành tệp PPTX. Lớp `ImageOrPrintOptions` cho phép bạn chỉ định `ExportImageFormat = ImageFormat.Pptx`, điều này nói với Aspose.Cells rằng đầu ra sẽ là một bản trình bày PowerPoint thay vì ảnh raster.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Tại sao cách này hoạt động:**  
Khi `ExportImageFormat` được đặt thành `Pptx`, Aspose.Cells chuyển đổi mỗi worksheet thành một slide. Các hình dạng, biểu đồ và bảng tổng hợp được ghi dưới dạng đối tượng PowerPoint gốc, vì vậy bạn có thể nhấp đúp chúng trong PowerPoint và chỉnh sửa dữ liệu nền.

**Mẹo cho workbook lớn:** Nếu bạn chỉ cần một phần các sheet, hãy gọi `workbook.Worksheets.RemoveAt(index)` cho các sheet không muốn xuất trước khi gọi `Save`. Điều này giảm kích thước tệp PPTX.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh kết hợp các bước trên. Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế trên máy của bạn.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in ra:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Khi bạn mở `output.pptx` trong Microsoft PowerPoint, bạn sẽ thấy một slide chứa bảng tổng hợp đã sao chép dưới dạng biểu đồ có thể chỉnh sửa. Nhấp đúp vào biểu đồ sẽ mở trình chỉnh sửa biểu đồ của PowerPoint, cho phép bạn sửa đổi series, trục và nhãn dữ liệu mà không cần quay lại Excel.

## Xử lý các vấn đề thường gặp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| Bảng tổng hợp hiển thị dưới dạng hình ảnh tĩnh | Cờ `CopyPivotTable` bị bỏ qua hoặc `ExportImageFormat` được đặt thành `Png` | Đảm bảo `CopyPivotTable = true` và `ExportImageFormat = ImageFormat.Pptx`. |
| Sheet đích hiển thị các ô trống | Phạm vi nguồn không bao phủ toàn bộ vùng bảng tổng hợp | Mở rộng phạm vi (ví dụ, `"A1:H30"`) để bao gồm tất cả các trường pivot. |
| PPTX xuất ra quá lớn | Bao gồm các worksheet không cần thiết | Xóa các sheet không muốn trước khi gọi `Save`. |
| PowerPoint không thể chỉnh sửa biểu đồ | Sử dụng phiên bản cũ của Aspose.Cells không hỗ trợ PPTX | Nâng cấp lên phiên bản Aspose.Cells mới nhất (kiểm tra ghi chú phát hành). |

## Các bước tiếp theo và chủ đề liên quan

* **Xuất sheet Excel sang PPTX với bố cục slide tùy chỉnh** – khám phá `WorksheetToPdfConverter` để kiểm soát chi tiết hơn về giao diện slide.  
* **Xuất Excel sang PDF** – thay `ImageFormat.Pptx` bằng `ImageFormat.Pdf` để tạo PDF.  
* **Chỉnh sửa PPTX một cách lập trình sau khi xuất** – sử dụng thư viện `Aspose.Slides` để thêm hoạt ảnh hoặc ghi chú người thuyết trình.  

Bằng cách nắm vững **copy pivot table**, **export excel to pptx**, và **generate editable pptx**, bạn có thể xây dựng quy trình báo cáo đầu‑tới‑đầu di chuyển dữ liệu từ bảng tính trực tiếp vào bộ slide trình chiếu mà không mất khả năng chỉnh sửa.

---

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề có liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách sao chép Pivot Table trong C# – Chuyển Excel sang PPTX, Sao chép Range & Tạo Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Tạo Workbook Excel mới – Sao chép & Nhân bản Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Tạo Pivot Table trong Excel bằng Aspose.Cells cho .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}