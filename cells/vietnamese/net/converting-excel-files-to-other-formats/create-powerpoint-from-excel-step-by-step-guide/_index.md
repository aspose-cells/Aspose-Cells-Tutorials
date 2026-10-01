---
category: general
date: 2026-02-09
description: Tạo PowerPoint từ Excel trong vài phút – tìm hiểu cách chuyển đổi Excel
  sang PowerPoint và xuất Excel sang PPT với ví dụ mã C# đơn giản.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: vi
og_description: Tạo PowerPoint từ Excel nhanh chóng. Hướng dẫn này chỉ cách chuyển
  đổi Excel sang PowerPoint, xuất Excel sang PPT và tạo PPT từ Excel bằng C#.
og_title: Tạo PowerPoint từ Excel – Hướng dẫn lập trình toàn diện
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Tạo PowerPoint từ Excel – Hướng dẫn từng bước
url: /vi/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PowerPoint từ Excel – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **tạo PowerPoint từ Excel** nhưng không chắc nên gọi API nào? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi muốn chuyển bảng tính thành bộ slide mà không phải sao chép‑dán thủ công.  

Tin tốt: chỉ với vài dòng C# bạn có thể **chuyển đổi Excel sang PowerPoint**, xuất các hình dạng trong sheet, và có được một tệp PPTX sẵn sàng để trình chiếu. Trong tutorial này chúng tôi sẽ hướng dẫn toàn bộ quy trình, giải thích lý do mỗi bước quan trọng, và chỉ cho bạn cách xử lý các vấn đề thường gặp nhất.

## Những gì bạn sẽ học

- Cách tải một workbook Excel chứa biểu đồ, hình ảnh, hoặc SmartArt.  
- Lệnh gọi chính xác để **export Excel to PPT** bằng thư viện Aspose.Cells.  
- Cách lưu bản trình chiếu đã tạo và kiểm tra kết quả.  
- Mẹo xử lý workbook không có hình dạng, điều chỉnh kích thước slide, và khắc phục lỗi không tương thích phiên bản.

Không cần công cụ bên ngoài, không cần COM interop, chỉ là mã .NET thuần túy chạy ở bất kỳ môi trường nào hỗ trợ .NET Core hoặc .NET 5+.

---

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

1. **Aspose.Cells for .NET** (thư viện cung cấp `SaveToPresentation`). Bạn có thể tải từ NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. Một SDK .NET mới (khuyến nghị 6.0 trở lên).  
3. Một tệp Excel (`shapes.xlsx`) chứa ít nhất một shape, chart, hoặc image mà bạn muốn hiển thị trên slide.

Đó là tất cả—không cần cài đặt Office, không cần lo lắng về giấy phép cho mục đích demo này (phiên bản đánh giá miễn phí hoạt động tốt).

---

## Bước 1: Tải Workbook Excel (Create PowerPoint from Excel)

Điều đầu tiên chúng ta cần là một đối tượng `Workbook` trỏ tới tệp nguồn. Đối tượng này đại diện cho toàn bộ tài liệu Excel, bao gồm tất cả các worksheet, chart và các đối tượng nhúng.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Mẹo chuyên nghiệp:** Nếu bạn không chắc tệp có tồn tại hay không, hãy bao bọc constructor trong một `try/catch` và cung cấp thông báo lỗi chi tiết. Điều này sẽ tránh cho bạn gặp phải `FileNotFoundException` khó hiểu sau này.

---

## Bước 2: Chuyển Workbook thành PowerPoint Presentation (Export Excel to PPT)

Aspose.Cells đi kèm với một exporter tích hợp sẵn, cho phép chuyển toàn bộ workbook—hoặc chỉ một số sheet đã chọn—thành bản trình chiếu PowerPoint. Phương thức `SaveToPresentation` thực hiện phần công việc nặng.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

Nếu bạn chỉ cần **generate ppt from excel** cho một tập hợp con các sheet, có thể sử dụng overload nhận một collection `SheetOptions`. Đối với hầu hết các trường hợp, chuyển đổi mặc định là đủ.

---

## Bước 3: Lưu Presentation đã tạo (How to Convert Excel to PPTX)

Bây giờ chúng ta đã có một thể hiện `Presentation`, việc ghi nó ra đĩa rất đơn giản. Kết quả sẽ là một tệp `.pptx` tiêu chuẩn mà bất kỳ phiên bản PowerPoint hiện đại nào cũng mở được.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **Nếu workbook không có shape thì sao?**  
> Exporter vẫn sẽ tạo các slide, nhưng chúng sẽ trống. Bạn có thể kiểm tra `workbook.Worksheets[i].Shapes.Count` trước khi chuyển đổi và quyết định có bỏ qua sheet đó hay không.

---

## Tùy chọn: Tinh chỉnh đầu ra (Advanced Export Excel to PPT)

Đôi khi kích thước slide mặc định (standard 4:3) không phù hợp với các bài thuyết trình dạng widescreen. Bạn có thể điều chỉnh kích thước slide trước khi lưu:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

Những điều chỉnh này minh họa **cách chuyển đổi Excel sang PowerPoint** với giao diện chuyên nghiệp, không chỉ là một đống dữ liệu thô.

---

## Ví dụ hoàn chỉnh (All Steps Combined)

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Sao chép‑dán vào một console app, chỉnh sửa đường dẫn tệp, và nhấn **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Kết quả mong đợi:** Mở `shapes.pptx` trong PowerPoint. Bạn sẽ thấy một slide cho mỗi worksheet, mỗi slide giữ nguyên các chart, image và các shape gốc. Slide tiêu đề tùy chọn xuất hiện ở đầu, tạo nên một bộ deck chuyên nghiệp.

---

## Các câu hỏi thường gặp & Trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu tôi chỉ cần một sheet duy nhất thì sao?* | Dùng `Workbook.Worksheets[0]` và gọi `SaveToPresentation` cho sheet đó qua `SheetOptions`. |
| *Có thể giữ lại công thức Excel không?* | Không—công thức sẽ được render dưới dạng giá trị tĩnh trên slide. Nếu cần dữ liệu động, hãy cân nhắc liên kết PPTX với file Excel sau này. |
| *Có hoạt động trên Linux/macOS không?* | Có. Aspose.Cells không phụ thuộc vào nền tảng; chỉ cần cài .NET runtime là được. |
| *Còn workbook được bảo vệ bằng mật khẩu thì sao?* | Tải bằng `LoadOptions` có chứa mật khẩu trước khi gọi `SaveToPresentation`. |
| *Tại sao tôi lại nhận được các slide trắng?* | Kiểm tra workbook có thực sự chứa shape (`Shapes.Count > 0`). Các slide trắng được tạo cho các sheet rỗng. |

---

## Kết luận

Bây giờ bạn đã có một giải pháp toàn diện, đầu‑từ‑đầu, để **tạo PowerPoint từ Excel** bằng C#. Bằng cách tải workbook, gọi `SaveToPresentation`, và lưu kết quả, bạn có thể **chuyển đổi Excel sang PowerPoint**, **export Excel to PPT**, và **generate PPT from Excel** chỉ với vài dòng mã.  

Từ đây bạn có thể khám phá:

- Thêm animation cho các slide được tạo bằng Aspose.Slides.  
- Tự động hoá toàn bộ quy trình (ví dụ: đọc file từ thư mục, chuyển đổi hàng loạt).  
- Tích hợp mã vào một API ASP.NET Core để người dùng tải lên file Excel và nhận ngay PPTX.

Hãy thử nghiệm, điều chỉnh kích thước slide, thêm tiêu đề tùy chỉnh—có rất nhiều không gian để làm cho đầu ra thực sự là của bạn. Có câu hỏi hoặc gặp khó khăn? Để lại bình luận bên dưới, chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}