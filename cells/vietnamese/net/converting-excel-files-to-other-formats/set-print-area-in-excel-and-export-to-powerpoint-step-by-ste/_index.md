---
category: general
date: 2026-03-22
description: Đặt vùng in trong Excel và chuyển đổi Excel sang PowerPoint với các hình
  dạng có thể chỉnh sửa. Tìm hiểu cách lặp lại hàng tiêu đề, tạo PowerPoint từ Excel
  và xuất Excel sang file pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: vi
og_description: Đặt vùng in trong Excel và chuyển nó thành một slide PowerPoint với
  các hình dạng có thể chỉnh sửa. Hãy làm theo hướng dẫn đầy đủ này để lặp lại hàng
  tiêu đề và xuất Excel sang PPTX.
og_title: Đặt khu vực in trong Excel – Hướng dẫn xuất sang PowerPoint
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Đặt vùng in trong Excel và xuất sang PowerPoint – Hướng dẫn từng bước
url: /vi/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Vùng In trong Excel và Xuất ra PowerPoint – Hướng Dẫn Lập Trình Đầy Đủ

Bạn đã bao giờ cần **đặt vùng in** trong một bảng tính Excel rồi chuyển phần đó thành một slide PowerPoint chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình báo cáo, cùng một dữ liệu được in đẹp mắt cũng cần xuất hiện trong bản trình bày, thường với hàng đầu tiên được lặp lại làm tiêu đề. Tin tốt? Chỉ với vài dòng C# bạn có thể **convert excel to powerpoint**, giữ mọi textbox có thể chỉnh sửa, và thậm chí **repeat title row** một cách tự động.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết: từ cấu hình vùng in đến tạo file PPTX mà bạn có thể chỉnh sửa ngay trong PowerPoint. Khi hoàn thành, bạn sẽ có thể **create powerpoint from excel**, xuất kết quả dưới dạng **export excel to pptx**, và tái sử dụng cùng một đoạn mã trong bất kỳ dự án .NET nào. Không có phép màu, chỉ có các bước rõ ràng và một ví dụ đầy đủ, có thể chạy được.

## Những Điều Bạn Cần Chuẩn Bị

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **.NET 6.0** hoặc mới hơn (API cũng hoạt động với .NET Framework)
- **Aspose.Cells for .NET** (thư viện cung cấp `Workbook`, `ImageOrPrintOptions`, v.v.)
- Một IDE C# cơ bản (Visual Studio, Rider, hoặc VS Code với extension C#)
- Một file Excel (`input.xlsx`) chứa dữ liệu bạn muốn xuất

Đó là tất cả—không cần thêm bất kỳ gói NuGet nào ngoài Aspose.Cells. Nếu bạn chưa thêm thư viện, chạy:

```bash
dotnet add package Aspose.Cells
```

Bây giờ chúng ta đã sẵn sàng.

## Bước 1: Tải Workbook – Điểm Khởi Đầu cho Việc Xuất

Điều đầu tiên bạn phải làm là tải workbook chứa sheet mà bạn muốn biến thành slide. Hãy nghĩ workbook như tài liệu nguồn; nếu không có nó, mọi thứ khác đều vô nghĩa.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Tại sao lại quan trọng:** Việc tải workbook cho phép bạn truy cập vào bộ sưu tập worksheet, các tùy chọn page‑setup, và engine xuất. Nếu bỏ qua bước này, bạn sẽ không thể đặt **print area** hay lặp lại bất kỳ hàng nào.

> **Pro tip:** Dùng đường dẫn tuyệt đối khi thử nghiệm, sau đó chuyển sang đường dẫn tương đối hoặc dựa trên cấu hình cho môi trường production.

## Bước 2: Cấu Hình Các Tùy Chọn Xuất – Giữ Text Boxes và Shapes Có Thể Chỉnh Sửa

Khi xuất sang PowerPoint, bạn có thể muốn slide kết quả vẫn có thể chỉnh sửa. Aspose.Cells cho phép bạn kiểm soát điều này bằng `ImageOrPrintOptions`. Đặt `ExportTextBoxes` và `ExportShapeObjects` thành `true` sẽ khiến thư viện giữ các đối tượng này dưới dạng phần tử PowerPoint gốc thay vì chuyển chúng thành hình ảnh.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Tại sao lại quan trọng:** Nếu bạn từng cần **convert excel to powerpoint** rồi chỉnh sửa slide thủ công, cài đặt này sẽ giúp bạn tránh việc phải tạo lại các textbox từ đầu. Nó cũng đảm bảo mọi shape (như mũi tên hay biểu đồ) vẫn ở dạng vector có thể thay đổi kích thước.

## Bước 3: Đặt Vùng In và Lặp Lại Hàng Tiêu Đề

Bây giờ chúng ta đến phần cốt lõi của tutorial: **set print area** và làm cho hàng đầu tiên lặp lại trên mỗi trang in (hoặc trong trường hợp của chúng ta, trên slide đã xuất). Vùng in cho Excel biết những ô nào sẽ được in—hoặc trong kịch bản này, sẽ được xuất.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Tại sao lại quan trọng:** Bằng cách giới hạn xuất trong `A1:G20` bạn tránh việc kéo toàn bộ các vùng trống lớn, giúp quá trình chuyển đổi nhanh hơn và slide gọn gàng hơn. Dòng `PrintTitleRows` khiến hàng đầu tiên hoạt động như tiêu đề—đúng như bạn muốn khi **repeat title row** trong bản trình bày.

> **Edge case:** Nếu dữ liệu của bạn bắt đầu từ hàng 2, hãy điều chỉnh phạm vi cho phù hợp (ví dụ, `PrintTitleRows = "$2:$2"`).

## Bước 4: Lưu Worksheet dưới Dạng File PowerPoint

Cuối cùng, chúng ta ghi slide ra đĩa. Phương thức `Save` nhận tên file đích và các tùy chọn đã cấu hình ở trên. Kết quả là một file PPTX với các textbox và shape có thể chỉnh sửa, sẵn sàng mở trong PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Bạn sẽ thấy gì:** Mở `SheetWithEditableShapes.pptx` trong PowerPoint. Hàng đầu tiên xuất hiện như tiêu đề, tất cả các ô từ `A1:G20` được render, và bất kỳ shape nào bạn đã thêm trong Excel vẫn có thể di chuyển và chỉnh sửa. Không có hình ảnh raster—chỉ các đối tượng PowerPoint gốc.

## Ví Dụ Hoàn Chỉnh – Tất Cả Các Bước Kết Hợp

Dưới đây là chương trình đầy đủ, sẵn sàng copy‑paste. Chạy nó như một console app hoặc nhúng vào bất kỳ giải pháp nào lớn hơn.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Kết quả mong đợi:** Sau khi chạy chương trình, console sẽ in thông báo thành công, và file PPTX sẽ xuất hiện ở vị trí đã chỉ định. Mở file sẽ thấy một slide duy nhất với phạm vi đã chọn, các textbox có thể chỉnh sửa, và mọi shape gốc.

## Câu Hỏi Thường Gặp & Những Cạm Bẫy

| Question | Answer |
|----------|--------|
| **Does this work with multiple worksheets?** | Yes. Loop through `workbook.Worksheets` and repeat the same steps for each sheet, changing the output filename each time. |
| **What if I need to export more than one slide?** | Call `workbook.Save` multiple times with different `ImageOrPrintOptions` objects, each configured with a different `PageSetup` if needed. |
| **Can I change the slide size?** | Use `exportOptions.ImageFormat` to set DPI, or adjust `sheet.PageSetup.PaperSize` before saving. |
| **Is Aspose.Cells free?** | It offers a free evaluation with watermarks. For production, a license is required. |
| **What about Excel formulas?** | The exported values are the **calculated results** at the time of export. If you need live formulas in PowerPoint, you’ll need a different approach. |

## Mẹo Để Quy Trình Trơn Tru

- **Pro tip:** Set `Workbook.Settings.CalcMode = CalculationModeType.Automatic` before export to guarantee all formulas are up‑to‑date.
- **Watch out for:** Very large ranges can cause memory pressure. Trim the print area to the smallest necessary range.
- **Performance tip:** Reuse a single `ImageOrPrintOptions` instance if you’re exporting many sheets; creating a new one each time adds overhead.
- **Version note:** The code above targets Aspose.Cells 23.10 (released November 2023). Later versions keep the same API, but always double‑check the release notes for breaking changes.

## Kết Luận

Chúng ta đã tìm hiểu cách **set print area** trong một worksheet Excel, lặp lại hàng đầu tiên làm tiêu đề, và sau đó **export excel to pptx** trong khi giữ các textbox và shape có thể chỉnh sửa. Nói tóm lại, bạn đã biết một cách đáng tin cậy để **convert excel to powerpoint**, **repeat title row**, và **create powerpoint from excel** chỉ với vài dòng C#.

Sẵn sàng cho bước tiếp theo? Hãy thử tự động hoá việc chuyển đổi hàng loạt cho hàng chục báo cáo, hoặc thêm layout slide tùy chỉnh bằng PowerPoint SDK sau khi xuất. Không giới hạn—hãy thử nghiệm, phá vỡ, và tận hưởng sức mạnh của việc tạo tài liệu lập trình.

Nếu bạn thấy tutorial này hữu ích, hãy chia sẻ, để lại bình luận với những tùy chỉnh của bạn, hoặc khám phá các hướng dẫn khác của chúng tôi về **export excel to pptx** và các chủ đề tự động hoá liên quan. Chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}