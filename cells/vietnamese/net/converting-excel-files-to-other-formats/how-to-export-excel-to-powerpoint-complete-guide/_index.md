---
category: general
date: 2026-07-03
description: Cách xuất tệp Excel sang PowerPoint với các hộp văn bản có thể chỉnh
  sửa bằng Aspose.Cells – hướng dẫn từng bước chuyển đổi XLSX sang PPTX.
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: vi
og_description: Cách xuất Excel sang PowerPoint với các hộp văn bản có thể chỉnh sửa.
  Tìm hiểu cách chuyển đổi XLSX sang PPTX bằng PresentationExportOptions trong C#.
og_title: Cách xuất Excel sang PowerPoint – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: Cách xuất Excel sang PowerPoint – Hướng dẫn đầy đủ
url: /vi/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng Dẫn Đầy Đủ Cách Xuất Excel Sang PowerPoint

Bạn đã bao giờ tự hỏi **cách xuất excel** dữ liệu trực tiếp vào một bản trình chiếu PowerPoint mà không mất khả năng chỉnh sửa chưa? Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn một cách thực tế để **tạo PowerPoint từ Excel** đồng thời giữ cho các hộp văn bản và hình dạng vẫn có thể chỉnh sửa được.

Chúng tôi sẽ đi qua từng dòng mã, giải thích lý do mỗi thiết lập quan trọng, và kết thúc bằng một tệp PowerPoint mà bạn có thể mở và tùy chỉnh ngay lập tức. Khi hoàn thành, bạn sẽ có thể **chuyển đổi XLSX sang PPTX** chỉ bằng một lời gọi phương thức, và bạn sẽ hiểu cách **các tùy chọn xuất bản trình chiếu** kiểm soát kết quả.

## Những Gì Bạn Cần Chuẩn Bị

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **.NET 6.0** (hoặc bất kỳ phiên bản .NET mới nào) đã được cài đặt trên máy của bạn.  
- Một **giấy phép** cho **Aspose.Cells for .NET** (bản dùng thử miễn phí đủ cho việc thử nghiệm).  
- Kiến thức cơ bản về C#—không cần quá phức tạp, chỉ cần có khả năng tạo một ứng dụng console hoặc một thư viện nhỏ.  
- Một workbook Excel (`input.xlsx`) mà bạn muốn chuyển thành bộ slide.

Đó là tất cả. Không cần công cụ bổ sung, không cần COM interop, chỉ cần mã quản lý thuần túy.

![Cách xuất excel sang PowerPoint diagram](https://example.com/placeholder.png "Sơ đồ mô tả quy trình xuất dữ liệu excel sang PowerPoint")

## Bước 1: Cài Đặt Aspose.Cells và Thiết Lập Dự Án

Để **cách xuất excel** bạn trước tiên cần thư viện cho phép thực hiện điều này. Mở terminal trong thư mục dự án và chạy:

```bash
dotnet add package Aspose.Cells
```

Lệnh này sẽ tải gói Aspose.Cells mới nhất từ NuGet. Thư viện bao gồm mọi thứ bạn cần cho **các tùy chọn xuất bản trình chiếu**, vì vậy bạn sẽ không phải tham chiếu các assembly Office Interop.

> **Mẹo chuyên nghiệp:** Nếu bạn đang nhắm tới .NET Framework, hãy sử dụng phiên bản NuGet phù hợp (ví dụ, `Aspose.Cells.NET`) để tránh các bất ngờ về tương thích.

## Bước 2: Tải Workbook Excel

Bây giờ thư viện đã sẵn sàng, hãy tải tệp nguồn. Lớp `Workbook` đại diện cho toàn bộ tài liệu Excel.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Lý do quan trọng:* Việc tải workbook là bước đầu tiên trong bất kỳ quy trình **chuyển đổi XLSX sang PPTX** nào. Đối tượng `Workbook` chứa các sheet, biểu đồ và định dạng ô, tất cả đều có thể được ánh xạ sang các đối tượng PowerPoint sau này.

## Bước 3: Cấu Hình Các Tùy Chọn Xuất Bản Trình Chiếu (Hộp Văn Bản Có Thể Chỉnh Sửa)

Đây là nơi phép thuật xảy ra. Mặc định, Aspose.Cells xuất các hình dạng dưới dạng hình ảnh tĩnh. Để giữ chúng là **hộp văn bản có thể chỉnh sửa**, bạn phải bật cờ thích hợp.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **Tại sao cần bật `ExportEditableObjects`?**  
> Khi thuộc tính này được đặt là `true`, Aspose.Cells sẽ chuyển mỗi hình dạng Excel thành một hình dạng PowerPoint gốc. Điều đó có nghĩa là bạn có thể mở file `.pptx` tạo ra trong PowerPoint và chỉnh sửa văn bản, thay đổi kích thước hộp, hoặc thay đổi màu sắc—đúng như mong đợi khi **tạo PowerPoint từ Excel**.

## Bước 4: Xuất Workbook Sang PowerPoint

Với workbook đã được tải và các tùy chọn đã cấu hình, dòng lệnh cuối cùng sẽ lưu tệp dưới dạng bản trình chiếu PowerPoint.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*Bạn sẽ thấy gì:* Tệp `output.pptx` sẽ chứa một slide cho mỗi worksheet (theo mặc định). Mỗi slide sao chép bố cục của sheet gốc, và mọi hộp văn bản bạn đặt trong Excel sẽ trở thành **hộp văn bản có thể chỉnh sửa** trong PowerPoint.

## Bước 5: Kiểm Tra Kết Quả và Điều Chỉnh Nếu Cần

Mở `output.pptx` trong Microsoft PowerPoint:

1. Điều hướng đến một slide được tạo từ một worksheet.  
2. Nhấp vào một hộp văn bản—bạn sẽ thấy có thể chỉnh sửa văn bản trực tiếp.  
3. Điều chỉnh kích thước hoặc màu sắc của hình dạng; các thay đổi sẽ được lưu lại.

Nếu có gì không ổn, hãy cân nhắc các điều chỉnh sau:

- **Xuất chỉ các sheet cụ thể:** Sử dụng `workbook.Worksheets.RemoveAt(index)` trước khi lưu.  
- **Kiểm soát bố cục slide:** Đặt `exportOptions.ExportAllSheetsAsSlide = false` và tự thêm slide thủ công.  
- **Bảo tồn định dạng biểu đồ:** Đảm bảo biểu đồ đã được đặt trên sheet trước khi xuất; chúng sẽ tự động trở thành biểu đồ PowerPoint.

## Những Sai Lầm Thường Gặp và Cách Tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|------------|----------------|
| Hình dạng trở thành ảnh | `ExportEditableObjects` để mặc định (`false`) | Đặt `ExportEditableObjects = true` như trong Bước 3. |
| Thiếu worksheet | Gọi `Save` trước khi loại bỏ các sheet không cần | Loại bỏ hoặc ẩn các sheet không cần trước khi xuất. |
| Kích thước tệp lớn | Hình ảnh độ phân giải cao được nhúng cùng với các hình dạng | Dùng `exportOptions.ImageResolution = 150` để giảm DPI nếu cần. |
| Cảnh báo tương thích trong PowerPoint | Sử dụng phiên bản Aspose.Cells cũ | Nâng cấp lên gói NuGet mới nhất (hỗ trợ PPTX 2016+). |

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép‑dán vào một ứng dụng console. Nó bao gồm tất cả các bước, xử lý lỗi và chú thích.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**Kết quả mong đợi trong console:**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

Mở `output.pptx` đã tạo—bạn sẽ thấy mỗi worksheet đã chuyển thành một slide, và mọi hình dạng bạn thêm trong Excel bây giờ là **hộp văn bản có thể chỉnh sửa** mà bạn có thể tinh chỉnh ngay lập tức.

## Tóm Tắt: Cách Xuất Excel Nhanh Gọn

Chúng ta đã đi qua toàn bộ quy trình **cách xuất excel**—từ cài đặt Aspose.Cells, cấu hình **các tùy chọn xuất bản trình chiếu**, đến cuối cùng **chuyển đổi XLSX sang PPTX** với nội dung hoàn toàn có thể chỉnh sửa. Những điểm quan trọng cần nhớ:

- Sử dụng `PresentationExportOptions.ExportEditableObjects = true` để giữ các hình dạng có thể chỉnh sửa.  
- Phương thức `Workbook.Save` thực hiện phần lớn công việc; bạn không cần bất kỳ COM interop nào.  
- Điều chỉnh các thiết lập tùy chọn (độ phân giải ảnh, lựa chọn sheet) để tinh chỉnh kết quả.

## Tiếp Theo Bạn Nên Làm Gì?

Nếu bạn thích việc biến bảng tính thành slide, bạn cũng có thể khám phá:

- **Nhúng biểu đồ** dưới dạng biểu đồ PowerPoint gốc (`exportOptions.ExportChartAsShape = false`).  
- **Áp dụng master slide tùy chỉnh** sau khi xuất để phù hợp với bộ nhận diện công ty.  
- **Tự động chuyển đổi hàng loạt** cho hàng chục tệp bằng một vòng lặp `foreach` đơn giản.  

Tất cả các chủ đề này dựa trên những nền tảng chúng ta vừa học, vì vậy bạn đã có nền tảng vững chắc.

---

Nếu gặp khó khăn, hãy để lại bình luận, hoặc chia sẻ cách bạn đã mở rộng mẫu này trong dự án của mình. Chúc bạn lập trình vui vẻ và tận hưởng cầu nối liền mạch giữa Excel và PowerPoint!

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây liên quan chặt chẽ đến các kỹ thuật đã được trình bày trong bài viết này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Add and Access Text Boxes in Excel using Aspose.Cells .NET | Step-by-Step Guide](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}