---
category: general
date: 2026-11-16
description: Học cách lưu Excel dưới dạng PowerPoint và chuyển đổi Excel sang PowerPoint
  một cách lập trình. Hướng dẫn chi tiết này cũng bao gồm việc xuất Excel sang PPTX
  và lưu một workbook dưới dạng PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: vi
lastmod: 2026-11-16
og_description: Lưu Excel dưới dạng PowerPoint bằng Aspose.Cells. Tham khảo hướng
  dẫn này để chuyển đổi Excel sang PowerPoint, xuất Excel sang PPTX và lưu workbook
  dưới dạng PPTX trong vài phút.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Lưu Excel dưới dạng PowerPoint – Hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Cách lưu Excel thành PowerPoint bằng Aspose.Cells trong C#
url: /vi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu Excel thành PowerPoint với Aspose.Cells trong C#

Nếu bạn cần **lưu Excel thành PowerPoint** một cách lập trình, hướng dẫn này cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Dù bạn đang xây dựng một công cụ báo cáo hay một trình tạo slide tự động, các bước dưới đây cho phép bạn chuyển đổi một worksheet Excel thành một slide PPTX có thể chỉnh sửa chỉ trong vài dòng mã.

Bạn sẽ học cách **chuyển đổi Excel sang PowerPoint**, xuất sheet ra file PPTX, và giữ các hộp văn bản cũng như hình dạng có thể chỉnh sửa – tất cả mà không rời khỏi môi trường .NET.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7.2+)
* Giấy phép Aspose.Cells hợp lệ (bản dùng thử miễn phí hoạt động cho việc đánh giá)
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào)
* Một workbook Excel chứa dữ liệu và các hình dạng bạn muốn xuất

## Bước 1: Cài đặt Aspose.Cells

Thêm gói NuGet Aspose.Cells vào dự án của bạn:

```bash
dotnet add package Aspose.Cells
```

> **Mẹo chuyên nghiệp:** Sử dụng cờ `-v` để chỉ định một phiên bản cụ thể, ví dụ, `Aspose.Cells.24.5`.

## Bước 2: Tải workbook mà bạn muốn xuất

Hoạt động đầu tiên trong quy trình **lưu Excel thành PowerPoint** là tải workbook nguồn.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Tại sao điều này quan trọng:* Việc tải workbook cho phép bạn truy cập vào các worksheet, cài đặt trang và các đối tượng vẽ sẽ trở thành các hình dạng PowerPoint có thể chỉnh sửa.

## Bước 3: Cấu hình tùy chọn xuất cho một slide PPTX có thể chỉnh sửa

Để **chuyển đổi Excel sang PowerPoint** đồng thời giữ khả năng chỉnh sửa, bạn phải đặt một vài thuộc tính trên `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Giải thích:*  
* `SaveFormat = SaveFormat.Pptx` cho Aspose.Cells biết tạo file PowerPoint.  
* `ExportEditableText` và `ExportEditableShapes` đảm bảo slide kết quả hoạt động như một slide PowerPoint gốc — bạn có thể nhấp vào hộp văn bản hoặc hình dạng và chỉnh sửa trực tiếp trong PowerPoint.

## Bước 4: Xác định khu vực xuất và điều chỉnh nó thành một slide duy nhất

Khi bạn **xuất Excel sang PPTX**, thường bạn muốn một phạm vi cụ thể xuất hiện trên slide. Đặt khu vực in và các tùy chọn điều chỉnh đảm bảo đầu ra sạch sẽ, chỉ một slide.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Tại sao điều này quan trọng:* `PrintArea` giới hạn việc xuất chỉ các ô từ A1 đến G30, trong khi `FitToPagesTall` và `FitToPagesWide` nén mọi thứ vào một slide, ngăn ngừa các trang phụ không mong muốn.

## Bước 5: Lưu worksheet thành file PPTX có thể chỉnh sửa

Bây giờ bạn có thể cuối cùng **lưu workbook dưới dạng PPTX** và hoàn thành quy trình **lưu Excel thành PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Sau khi chạy chương trình, mở `EditableShapes.pptx` trong Microsoft PowerPoint. Bạn sẽ thấy một slide phản ánh phạm vi Excel đã chọn, và tất cả các hộp văn bản và hình dạng đều có thể chỉnh sửa hoàn toàn.

### Kết quả mong đợi

* Một file có tên `EditableShapes.pptx` nằm trong `C:\Output\`.
* Một slide PowerPoint chứa phạm vi A1:G30.
* Các hộp văn bản, biểu đồ và hình dạng mà bạn có thể nhấp đúp và chỉnh sửa trực tiếp trong PowerPoint.

## Mã nguồn đầy đủ (sẵn sàng sao chép)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Các câu hỏi thường gặp và xử lý trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| **Nếu tôi có nhiều worksheet?** | Lặp qua `workbook.Worksheets` và lặp lại các bước 3‑5 cho mỗi sheet, thay đổi tên file đầu ra (ví dụ, `Sheet1.pptx`, `Sheet2.pptx`). |
| **Tôi có thể xuất toàn bộ workbook thành một bộ PowerPoint duy nhất không?** | Có. Đặt `ExportAllSheets = true` trên `ImageOrPrintOptions`. Mỗi worksheet sẽ trở thành một slide riêng. |
| **Các hình dạng của tôi xuất hiện dưới dạng hình ảnh, không phải đối tượng có thể chỉnh sửa.** | Đảm bảo `ExportEditableShapes = true` và bạn đang sử dụng Aspose.Cells 24.5+ (các phiên bản trước không có tính năng này). |
| **PPTX được tạo ra quá lớn.** | Giảm khu vực in, hoặc hạ độ phân giải hình ảnh qua `exportOptions.ImageResolution`. |
| **Tôi có cần giấy phép cho việc sử dụng trong môi trường production không?** | Giấy phép trả phí sẽ loại bỏ watermark đánh giá và mở khóa hiệu năng đầy đủ. Bản dùng thử miễn phí hoạt động cho việc thử nghiệm. |

## Mẹo cho mã production ổn định

* **Xác thực đường dẫn file** trước khi gọi `Workbook` hoặc `Save` để tránh `FileNotFoundException`.  
* **Bao quanh quá trình xuất trong khối try/catch** để xử lý lỗi giấy phép (`Aspose.Cells.LicenseException`).  
* **Giải phóng workbook** (`workbook.Dispose()`) khi hoàn thành để giải phóng tài nguyên không quản lý.  
* **Sử dụng I/O bất đồng bộ** (`FileStream` với `await`) nếu bạn đang xuất nhiều sheet lớn trong một dịch vụ web.

## Các bước tiếp theo

Bây giờ bạn đã biết cách **lưu Excel thành PowerPoint**, bạn có thể khám phá các chủ đề liên quan:

* **Xuất Excel sang PPTX với bố cục slide tùy chỉnh** – điều chỉnh `SlideSize` và thêm một master slide.  
* **Chuyển đổi slide Excel sang PDF** – sử dụng `SaveFormat.Pdf` cho phiên bản có thể in.  
* **Chuyển đổi hàng loạt một thư mục các workbook** – kết hợp vòng lặp đã trình bày ở trên với `Directory.GetFiles`.  

Thử nghiệm với các khu vực in khác nhau, tùy chọn tỷ lệ và chủ đề PowerPoint để tùy chỉnh đầu ra phù hợp với thương hiệu của tổ chức bạn.

---

*Chúc lập trình vui vẻ! Nếu hướng dẫn này giúp bạn **chuyển đổi Excel sang PowerPoint**, hãy chia sẻ với đồng nghiệp hoặc mở một issue trên repository GitHub của Aspose.Cells để được hỗ trợ thêm.*

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách lưu Excel thành PowerPoint bằng C# và Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Cách lưu PPTX từ Excel – Hướng dẫn đầy đủ để xuất Sheet Excel sang PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Chuyển đổi Excel sang PowerPoint – Hướng dẫn chi tiết từng bước](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}