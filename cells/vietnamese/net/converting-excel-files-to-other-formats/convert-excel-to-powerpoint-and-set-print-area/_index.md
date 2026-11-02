---
category: general
date: 2026-10-10
description: Chuyển đổi Excel sang PowerPoint và thiết lập khu vực in trong C# với
  Aspose.Cells – tìm hiểu cách xuất Excel, thiết lập khu vực in và tạo tệp PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: vi
lastmod: 2026-10-10
og_description: Chuyển đổi Excel sang PowerPoint với Aspose.Cells. Hướng dẫn này cho
  thấy cách thiết lập vùng in, xuất Excel và tạo tệp PPTX bằng C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Chuyển đổi Excel sang PowerPoint – hướng dẫn đầy đủ cho lập trình viên C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Chuyển đổi Excel sang PowerPoint và thiết lập vùng in
url: /vi/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi Excel sang PowerPoint và đặt vùng in

Nếu bạn cần **convert Excel to PowerPoint**, hướng dẫn này cho bạn thấy chính xác cách thực hiện trong C#. Bằng cách xác định vùng in trước, bạn kiểm soát những ô nào sẽ xuất hiện trên mỗi slide, và tệp PPTX cuối cùng sẽ phù hợp với mong đợi bố cục của bạn. Giải pháp cũng trả lời “how to export Excel” và “how to set print area” bằng cùng một mã nguồn.

Trong tutorial này bạn sẽ:

* Tải một workbook hiện có.
* Đặt vùng in cho một worksheet (bước **set print area excel**).
* Cấu hình các tùy chọn chuyển đổi cho đầu ra PowerPoint.
* Tạo một tệp **convert excel to pptx** trong một lần gọi phương thức.

Tất cả mã cần thiết đã được bao gồm, vì vậy bạn có thể sao chép, dán và chạy ngay lập tức.

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| **.NET 6.0 hoặc sau này** | Mẫu này nhắm tới .NET 6+, nhưng bất kỳ phiên bản .NET nào hỗ trợ C# 10 đều hoạt động. |
| **Aspose.Cells for .NET** | Thư viện này cung cấp `Workbook`, `ImageOrPrintOptions`, và phương thức `ConvertToPdf` (được dùng cho PPTX). Cài đặt qua NuGet: `dotnet add package Aspose.Cells` |
| **Một tệp Excel đầu vào** | Hướng dẫn này sử dụng `input.xlsx`. Đặt nó trong một thư mục bạn có thể tham chiếu từ mã. |
| **Quyền ghi vào thư mục đầu ra** | Chương trình sẽ ghi `output.pptx`. Đảm bảo thư mục tồn tại và có thể ghi được. |

> **Mẹo:** Nếu bạn làm việc với nhiều worksheet, hãy lặp lại bước thiết lập vùng in cho mỗi sheet trước khi chuyển đổi.

## Bước 1: Tạo một dự án console C# mới

Mở terminal hoặc cửa sổ PowerShell và chạy:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Lệnh này tạo một dự án mới tên **ExcelToPowerPointDemo** và thêm gói Aspose.Cells, là phụ thuộc chính cho **how to export Excel** sang các định dạng khác.

## Bước 2: Viết mã chuyển đổi

Thay thế nội dung của `Program.cs` bằng ví dụ hoàn chỉnh dưới đây. Mã này minh họa **convert excel to powerpoint**, cho thấy **how to set print area**, và tạo ra một tệp **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Tại sao mỗi phần quan trọng

* **Loading the workbook** – Đây là bước đầu tiên trong bất kỳ kịch bản **how to export Excel** nào. `Workbook` đọc tệp vào bộ nhớ, cho phép bạn truy cập đầy đủ vào các sheet, ô và định dạng.
* **Setting the print area** – Bằng cách gán `PageSetup.PrintArea`, bạn chỉ định cho Aspose.Cells những ô nào sẽ được render. Đây là cốt lõi của **set print area excel**; nếu không, toàn bộ sheet sẽ được xuất, có thể tạo ra các slide khổng lồ, không đọc được.
* **Choosing `SaveFormat.Pptx`** – Đối tượng `ImageOrPrintOptions` cho phép bạn chuyển đổi định dạng đầu ra. Đặt `SaveFormat` thành `Pptx` sẽ kích hoạt quy trình **convert excel to pptx**.
* **Calling `ConvertToPdf`** – Mặc dù tên phương thức là `ConvertToPdf`, khi `SaveFormat` là `Pptx` thư viện sẽ xuất ra tệp PowerPoint. Đây là cách được khuyến nghị để **convert excel to powerpoint** trong một lần gọi.

## Bước 3: Chạy chương trình

Từ thư mục dự án, thực thi:

```bash
dotnet run
```

Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy đầu ra console tương tự như:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Mở `output.pptx` trong Microsoft PowerPoint hoặc bất kỳ trình xem nào tương thích. Mỗi slide tương ứng với trang đã in của worksheet, giới hạn trong phạm vi bạn đã định nghĩa.

## Xử lý nhiều worksheet

Nếu workbook của bạn chứa hơn một sheet và bạn muốn mỗi sheet có một bộ slide riêng, hãy lặp qua collection:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Mẫu này cho thấy **how to export Excel** dữ liệu sheet‑by‑sheet trong khi vẫn **setting print area** riêng lẻ.

## Các trường hợp đặc biệt và mẹo thực hành tốt

| Tình huống | Cách tiếp cận đề xuất |
|-----------|----------------------|
| **Very large worksheets** | Giảm vùng in hoặc tăng `HorizontalResolution`/`VerticalResolution` để giữ kích thước PPTX trong mức quản lý. |
| **Different page orientations** | Đặt `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` trước khi chuyển đổi. |
| **Custom slide size** | Sử dụng `conversionOptions.OnePagePerSheet = false;` và điều chỉnh `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Bao quanh mã tải trong khối `try { … } catch (FileNotFoundException)` để cung cấp thông báo lỗi rõ ràng. |
| **Non‑ASCII characters** | Đảm bảo workbook được lưu với mã hoá UTF‑8; Aspose.Cells tự động xử lý Unicode. |

## Mã nguồn đầy đủ để tham khảo

Dưới đây là toàn bộ chương trình, bao gồm các chỉ thị `using` và chú thích. Lưu nó dưới tên `Program.cs` trong dự án được tạo ở **Bước 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Kết quả mong đợi

Chạy chương trình sẽ tạo ra một tệp PowerPoint (`output.pptx`) chứa:

* Một slide cho mỗi trang đã in của worksheet.
* Chỉ các ô trong phạm vi **A1:G30** hiển thị trên mỗi slide.
* Định dạng được giữ nguyên (phông chữ, màu sắc, viền) như trong Excel.

Mở tệp trong PowerPoint để xác nhận bố cục khớp với vùng in đã định nghĩa.

## Kết luận

Bây giờ bạn đã biết cách **convert Excel to PowerPoint** đồng thời chính xác **set print area excel** bằng Aspose.Cells trong C#. Hướng dẫn đã bao gồm **how to export Excel**, trình bày **how to set print area**, và cho thấy toàn bộ **convert excel to pptx**.

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}