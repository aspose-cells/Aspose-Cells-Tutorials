---
category: general
date: 2026-05-23
description: Chuyển đổi Excel sang PowerPoint trong C# bằng Aspose.Cells. Tìm hiểu
  cách tạo PowerPoint từ tệp Excel, lưu workbook dưới dạng PowerPoint và xuất bảng
  tính sang PowerPoint.
draft: false
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- save workbook as powerpoint
- export spreadsheet to powerpoint
- convert workbook to pptx
language: vi
og_description: Chuyển đổi Excel sang PowerPoint trong C#. Hướng dẫn này chỉ cho bạn
  cách tạo PowerPoint từ tệp Excel, lưu sổ làm việc dưới dạng PowerPoint và xuất bảng
  tính sang PowerPoint.
og_title: Chuyển đổi Excel sang PowerPoint bằng C# – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Convert Excel to PowerPoint in C# using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, save workbook as PowerPoint, and export spreadsheet
    to PowerPoint.
  headline: Convert Excel to PowerPoint with C# – Complete Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
- Automation
title: Chuyển đổi Excel sang PowerPoint bằng C# – Hướng dẫn toàn diện
url: /vi/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Excel to PowerPoint with C# – Complete Guide

Bạn đã bao giờ cần **convert Excel to PowerPoint** nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp cùng một khó khăn khi muốn chuyển một bảng tính thành bộ slide mà không phải sao chép dữ liệu thủ công.  

Trong tutorial này, chúng tôi sẽ hướng dẫn qua một **complete, end‑to‑end solution** cho phép bạn **create PowerPoint from Excel file** bằng C#. Bạn sẽ thấy chính xác cách **save workbook as PowerPoint**, xử lý các tùy chọn, và thậm chí kiểm tra đầu ra—tất cả chỉ trong vài dòng code.

> **What you’ll get:** một ứng dụng console C# sẵn sàng chạy, nhận `input.xlsx` và tạo ra `output.pptx` trong cùng thư mục, cùng với các mẹo xử lý hình ảnh, biểu đồ và các vấn đề thường gặp.

---

## Prerequisites

- **.NET 6.0** (hoặc bất kỳ phiên bản .NET mới nào) đã được cài đặt.
- Một **valid license** cho **Aspose.Cells for .NET** (phiên bản dùng thử miễn phí hoạt động cho việc thử nghiệm).
- Một workbook Excel (`input.xlsx`) mà bạn muốn chuyển thành bản trình chiếu.
- Một IDE yêu thích—Visual Studio, VS Code, Rider—bất cứ gì bạn thích.

Không cần thư viện bên thứ ba nào khác.

---

## Step 1: Convert Excel to PowerPoint – Load the Workbook

Đầu tiên, chúng ta cần mở file Excel để Aspose.Cells có thể làm việc với nó. Hãy nghĩ lớp `Workbook` như cổng vào mọi sheet, ô và biểu đồ trong bảng tính của bạn.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the Excel workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Optional: Verify that the workbook loaded correctly
Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");
```

> **Why this matters:** Việc tải workbook cung cấp cho chúng ta một biểu diễn trong bộ nhớ mà sau này có thể render thành các slide PowerPoint. Nếu đường dẫn file sai, hàm khởi tạo `Workbook` sẽ ném lỗi, cho phép bạn bắt lỗi sớm.

---

## Step 2: Configure PowerPoint Export Options

Aspose.Cells sử dụng lớp `ImageOrPrintOptions` để kiểm soát cách workbook được chuyển thành bản trình chiếu. Thuộc tính quan trọng là `SaveFormat`, chúng ta sẽ đặt nó thành `SaveFormat.Pptx`.

```csharp
// Set up options for exporting to PowerPoint
ImageOrPrintOptions saveOptions = new ImageOrPrintOptions
{
    // This tells Aspose.Cells we want a PPTX file, not an image or PDF
    SaveFormat = SaveFormat.Pptx,

    // Optional: Adjust slide size or image quality if needed
    // ImageResolution = 300,
    // SlideSize = SlideSizeType.Widescreen
};
```

> **Pro tip:** Nếu bạn cần kích thước slide cụ thể (ví dụ, 16:9 widescreen), hãy điều chỉnh thuộc tính `SlideSize`. Nếu không, mặc định sẽ hoạt động cho hầu hết các trường hợp.

---

## Step 3: Save the Workbook as PowerPoint

Bây giờ chúng ta thực hiện chuyển đổi. Phương thức `Save` nhận đường dẫn đầu ra và các tùy chọn chúng ta vừa định nghĩa.

```csharp
// Save the workbook as a PPTX file
string outputPath = @"YOUR_DIRECTORY\output.pptx";
workbook.Save(outputPath, saveOptions);

Console.WriteLine($"Successfully converted Excel to PowerPoint: {outputPath}");
```

> **What’s happening under the hood?** Aspose.Cells render mỗi worksheet thành một slide riêng, giữ nguyên định dạng ô, màu sắc, và thậm chí các biểu đồ đơn giản. Kết quả là một file PowerPoint sạch sẽ, có thể chỉnh sửa, bạn có thể mở trong Microsoft PowerPoint hoặc bất kỳ trình xem tương thích nào.

---

## Step 4: Verify the Generated PPTX

Một kiểm tra nhanh giúp bạn phát hiện sớm các vấn đề chuyển đổi. Mở file bằng cách lập trình (sử dụng Aspose.Slides) hoặc thủ công trong PowerPoint.

```csharp
using Aspose.Slides;

// Load the generated PPTX just to confirm it’s readable
Presentation ppt = new Presentation(outputPath);
Console.WriteLine($"PPTX contains {ppt.Slides.Count} slide(s).");

// Optionally, export the first slide as an image for visual verification
ppt.Slides[0].GetThumbnail(1f, 1f).Save(@"YOUR_DIRECTORY\first_slide.png");
```

Nếu số slide khớp với số worksheet, bạn đã hoàn thành.

---

## Step 5: Common Pitfalls & How to Avoid Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **Blank slides** | Worksheet chỉ chứa công thức chưa được tính toán. | Gọi `workbook.CalculateFormula();` trước khi lưu. |
| **Distorted charts** | Việc render biểu đồ bị tắt trong giấy phép. | Đảm bảo giấy phép Aspose.Cells của bạn bao gồm hỗ trợ biểu đồ. |
| **File not found** | Đường dẫn `YOUR_DIRECTORY` sai hoặc thiếu `input.xlsx`. | Sử dụng `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` cho các đường dẫn tương đối. |
| **Large PPTX size** | Hình ảnh độ phân giải cao hoặc nhiều hàng/cột ẩn. | Đặt `ImageResolution` thấp hơn hoặc ẩn các hàng/cột không cần thiết trước khi chuyển đổi. |

---

## Step 6: Extending the Conversion – Adding Images & Custom Slides

Đôi khi bạn cần nhiều hơn một ánh xạ trực tiếp từ sheet sang slide. Bạn có thể chèn các slide tùy chỉnh bằng **Aspose.Slides** sau khi chuyển đổi.

```csharp
using Aspose.Slides.Export;

// Load the PPTX we just created
Presentation presentation = new Presentation(outputPath);

// Add a title slide at the beginning
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
    .TextFrame.Text = "Quarterly Sales Overview";

// Save the extended deck
presentation.Save(@"YOUR_DIRECTORY\final_output.pptx", SaveFormat.Pptx);
Console.WriteLine("Added custom title slide.");
```

> **Why mix libraries?** Aspose.Cells thực hiện công việc nặng nhọc chuyển các worksheet thành slide, trong khi Aspose.Slides cho phép bạn tinh chỉnh bộ slide—thêm logo, chuyển động, hoặc ghi chú người thuyết trình.

---

## Complete Working Example

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép‑dán vào một dự án console mới. Nó bao gồm tất cả các chỉ thị `using`, xử lý lỗi và chú thích.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using Aspose.Slides;
using Aspose.Slides.Export;

class ExcelToPowerPoint
{
    static void Main()
    {
        // Define paths – adjust as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pptx");

        // -------------------------------------------------
        // Step 1: Load the Excel workbook
        // -------------------------------------------------
        Workbook workbook;
        try
        {
            workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} sheet(s).");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading workbook: {ex.Message}");
            return;
        }

        // -------------------------------------------------
        // Step 2: Set up PowerPoint export options
        // -------------------------------------------------
        ImageOrPrintOptions saveOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx,
            // Uncomment to tweak resolution or slide size
            // ImageResolution = 200,
            // SlideSize = SlideSizeType.Widescreen
        };

        // -------------------------------------------------
        // Step 3: Save the workbook as PowerPoint
        // -------------------------------------------------
        try
        {
            workbook.Save(outputPath, saveOptions);
            Console.WriteLine($"Successfully converted Excel to PowerPoint: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error during conversion: {ex.Message}");
            return;
        }

        // -------------------------------------------------
        // Step 4: Verify the PPTX (optional but recommended)
        // -------------------------------------------------
        try
        {
            using (Presentation ppt = new Presentation(outputPath))
            {
                Console.WriteLine($"PPTX contains {ppt.Slides.Count} slide(s).");
                // Export first slide as PNG for quick visual check
                ppt.Slides[0].GetThumbnail(1f, 1f).Save("first_slide.png");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error verifying PPTX: {ex.Message}");
        }

        // -------------------------------------------------
        // Step 5: (Optional) Add a custom title slide
        // -------------------------------------------------
        try
        {
            using (Presentation pres = new Presentation(outputPath))
            {
                ISlide titleSlide = pres.Slides.InsertEmptySlide(0, pres.LayoutSlides[0]);
                titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                    .TextFrame.Text = "Quarterly Sales Overview";

                pres.Save("final_output.pptx", SaveFormat.Pptx);
                Console.WriteLine("Added custom title slide and saved final_output.pptx");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error adding custom slide: {ex.Message}");
        }
    }
}
```

**Expected output when you run the program** (giả sử một `input.xlsx` đơn giản với hai worksheet):

```
Loaded workbook with 2 sheet(s).
Successfully converted Excel to PowerPoint: C:\Path\output.pptx
PPTX contains 2 slide(s).
Added custom title slide and saved final_output.pptx
```

Mở `final_output.pptx` trong PowerPoint—bạn sẽ thấy một slide tiêu đề rồi tiếp theo là hai slide phản ánh các worksheet của Excel.

---

## Conclusion

Bạn giờ đã có một **complete, production‑ready recipe to convert Excel to PowerPoint** bằng C#. Từ việc tải workbook, cấu hình tùy chọn xuất, lưu file, cho đến việc thêm slide tùy chỉnh, tutorial đã bao phủ mọi bước bạn có thể cần.  

Tiếp theo, hãy thử **export spreadsheet to PowerPoint** với nội dung phong phú hơn—nhúng biểu đồ, áp dụng theme slide, hoặc tự động chuyển đổi hàng loạt cho hàng chục workbook. Cùng mẫu này cũng hoạt động cho **save workbook as PowerPoint** trong các pipeline báo cáo tự động, làm cho quy trình trình bày dữ liệu của bạn mượt mà hơn bao giờ hết.

Có câu hỏi nào về **create powerpoint from excel

## Related Tutorials

- [Cách chuyển đổi Excel sang PowerPoint bằng Aspose.Cells cho .NET: Hướng dẫn đầy đủ](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Chuyển đổi Excel sang Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Chuyển đổi Excel sang Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}