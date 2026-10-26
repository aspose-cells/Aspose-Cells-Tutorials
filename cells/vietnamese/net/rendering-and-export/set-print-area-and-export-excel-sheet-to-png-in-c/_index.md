---
category: general
date: 2026-10-26
description: Đặt vùng in và xuất một sheet Excel sang PNG trong C#. Tìm hiểu các tùy
  chọn xuất hình ảnh, cách xuất PNG và nhận được hình ảnh có thể in từ một workbook.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: vi
lastmod: 2026-10-26
og_description: Đặt vùng in và xuất một sheet Excel sang PNG trong C#. Hướng dẫn chi
  tiết này bao gồm các tùy chọn xuất hình ảnh và cách xuất PNG từ một workbook.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Đặt vùng in và xuất sheet Excel sang PNG – Hướng dẫn C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Đặt vùng in và xuất bảng Excel sang PNG trong C#
url: /vi/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt vùng in và xuất sheet Excel ra PNG trong C#

Nếu bạn cần **đặt vùng in** trước khi xuất một sheet Excel ra PNG, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy một ví dụ hoàn chỉnh bằng C# cấu hình các tùy chọn xuất ảnh, điều chỉnh vùng in của worksheet và lưu kết quả dưới dạng hình ảnh.

Xuất một sheet Excel ra PNG là yêu cầu phổ biến khi bạn muốn nhúng ảnh chụp nhanh của worksheet vào báo cáo, email hoặc trang web. Đoạn mã dưới đây hoạt động với bất kỳ workbook nào chứa pivot table, nhưng kỹ thuật này cũng áp dụng cho các vùng dữ liệu thông thường. Không cần công cụ bên ngoài—chỉ cần thư viện Aspose.Cells cho .NET.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mẫu này nhắm tới .NET 6, nhưng bất kỳ phiên bản .NET gần đây nào cũng hoạt động)
- Aspose.Cells cho .NET (cài đặt qua NuGet: `Install-Package Aspose.Cells`)
- Kiến thức cơ bản về C# và các khái niệm Excel như worksheet và vùng in

## Bước 1: Cấu hình tùy chọn xuất ảnh

Điều đầu tiên bạn làm là tạo một thể hiện `ImageOrPrintOptions`. Đối tượng này cho Aspose.Cells biết cách render sheet dưới dạng ảnh.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Tại sao lại quan trọng:** `ImageOrPrintOptions` kiểm soát định dạng đầu ra, độ phân giải và các chi tiết render khác. Sử dụng PNG đảm bảo chất lượng không mất dữ liệu, lý tưởng cho các báo cáo yêu cầu văn bản và đồ họa sắc nét.

## Bước 2: Tải workbook và truy cập worksheet mục tiêu

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Tại sao lại quan trọng:** Bạn phải làm việc với một đối tượng `Worksheet` cụ thể vì vùng in là thiết lập ở mức worksheet.

## Bước 3: Xác định phạm vi bạn muốn in

Trong nhiều trường hợp, dữ liệu bạn quan tâm nằm trong một pivot table. Đoạn mã sau trích xuất phạm vi dữ liệu của pivot table đầu tiên trên sheet.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Nếu worksheet của bạn không chứa pivot table, bạn có thể thay `pivotDataRange` bằng bất kỳ `CellArea` nào bạn tạo thủ công, ví dụ:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Bước 4: **Đặt vùng in** để khớp với phạm vi đã chọn

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Tại sao lại quan trọng:** Vùng in cho Excel (và Aspose.Cells) biết những ô nào sẽ được bao gồm khi render sheet thành ảnh. Bằng cách căn chỉnh vùng in với phạm vi dữ liệu pivot, bạn tránh các lề trống và đảm bảo PNG xuất ra chỉ chứa dữ liệu liên quan.

## Bước 5: Xuất worksheet ra ảnh PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Tại sao lại quan trọng:** `worksheet.ToImage` tôn trọng vùng in đã được đặt trước, vì vậy file PNG chứa đúng các ô bạn đã định nghĩa. Gán ảnh vào một picture shape cho phép bạn nhúng lại vào workbook nếu cần, trong khi lưu ra đĩa cung cấp một file độc lập.

## Ví dụ hoàn chỉnh

Kết hợp tất cả các bước lại sẽ tạo ra một chương trình tự chứa bạn có thể chạy ngay lập tức.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ tạo ra `C:\Temp\WorksheetExport.png`. Mở file này sẽ hiển thị một ảnh PNG sắc nét chỉ chứa các ô được **đặt vùng in** (dữ liệu pivot table trong ví dụ này). Ảnh có thể được chèn vào tài liệu Word, slide PowerPoint hoặc trang web mà không cần bước chuyển đổi thêm.

## Xử lý nhiều worksheet hoặc pivot table

- **Nhiều worksheet:** Lặp qua `wb.Worksheets` và lặp lại các bước 3‑5 cho mỗi sheet bạn cần xuất.
- **Nhiều pivot table:** Chọn `PivotTables[index]` phù hợp hoặc duyệt `worksheet.PivotTables` để xuất từng bảng riêng biệt.
- **Không có pivot table:** Tạo một `CellArea` thủ công (xem chú thích trong Bước 3) và gán nó cho `PrintArea`.

## Mẹo thực tiễn (E‑E‑A‑T)

- **Mẹo chuyên nghiệp:** Đặt `HorizontalResolution` và `VerticalResolution` thành 300 DPI cho PNG chuẩn in; giá trị thấp hơn sẽ giảm kích thước file cho sử dụng trên web.
- **Cẩn thận với picture shape rỗng:** Nếu worksheet không có picture shape, hãy thêm một shape trước khi gán ảnh:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Hiệu năng:** Tái sử dụng một thể hiện `ImageOrPrintOptions` duy nhất cho nhiều worksheet sẽ tránh việc cấp phát không cần thiết.
- **Tương thích:** Aspose.Cells 23.9+ hoàn toàn hỗ trợ .NET 6 và các phiên bản sau; các phiên bản cũ hơn có thể cần điều chỉnh tên API.

## Kết luận

Bây giờ bạn đã biết cách **đặt vùng in** và xuất một sheet Excel ra PNG.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}