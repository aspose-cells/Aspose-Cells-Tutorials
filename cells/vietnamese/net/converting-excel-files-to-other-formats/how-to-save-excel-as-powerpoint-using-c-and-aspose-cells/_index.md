---
category: general
date: 2026-08-17
description: Lưu Excel thành PowerPoint bằng C# – hướng dẫn từng bước chuyển đổi tệp
  XLSX, làm cho các hộp văn bản có thể chỉnh sửa và tạo ra tệp PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: vi
lastmod: 2026-08-17
og_description: Lưu Excel thành PowerPoint trong C# với ví dụ mã đầy đủ. Tìm hiểu
  cách chuyển đổi XLSX, làm cho các hộp văn bản có thể chỉnh sửa và xuất ra PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Lưu Excel thành PowerPoint trong C# – hướng dẫn chuyển đổi đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Cách lưu Excel dưới dạng PowerPoint bằng C# và Aspose.Cells
url: /vi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách lưu Excel dưới dạng PowerPoint bằng C# và Aspose.Cells

Nếu bạn cần **save Excel as PowerPoint** trong một dự án .NET, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Bạn sẽ thấy cách tải một workbook XLSX, làm cho mọi textbox trên sheet có thể chỉnh sửa, và xuất kết quả ra file PPTX — chỉ với vài dòng C#.

Chuyển đổi Excel sang PowerPoint là một yêu cầu phổ biến cho các bảng điều khiển báo cáo, bộ slide, hoặc việc tạo bài thuyết trình tự động. Bài hướng dẫn này cũng đề cập đến **how to edit textboxes** một cách lập trình, để bạn có thể tùy chỉnh nội dung slide trước khi lưu.

## Yêu cầu trước

* .NET 6.0 (hoặc mới hơn) SDK đã được cài đặt  
* Môi trường phát triển như Visual Studio 2022 hoặc VS Code  
* Giấy phép Aspose.Cells cho .NET (hoặc khóa dùng thử miễn phí) – tải về từ [Aspose website](https://products.aspose.com/cells/net/)  
* File `input.xlsx` mà bạn muốn chuyển đổi  

> **Mẹo chuyên nghiệp:** Nếu bạn sử dụng phiên bản dùng thử miễn phí, file PPTX đầu ra sẽ chứa watermark. Phiên bản có giấy phép sẽ loại bỏ nó.

## Bước 1: Cài đặt gói NuGet Aspose.Cells

Mở terminal trong thư mục dự án của bạn và chạy:

```bash
dotnet add package Aspose.Cells
```

Lệnh này sẽ thêm assembly `Aspose.Cells`, cung cấp các lớp `Workbook`, `Worksheet` và `Shape` cần thiết cho việc chuyển đổi.

## Bước 2: Tạo khung ứng dụng console

Tạo một dự án console mới (nếu bạn chưa có):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Thay thế file `Program.cs` được tạo tự động bằng mã được hiển thị trong các bước tiếp theo.

## Bước 3: Tải workbook và chọn worksheet đầu tiên

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Tại sao điều này quan trọng:**  
`Workbook` đọc file Excel vào bộ nhớ, trong khi `Worksheet` cho phép bạn truy cập vào các ô, biểu đồ và hình dạng của sheet. Worksheet đầu tiên thường là báo cáo mặc định mà bạn muốn trình bày.

## Bước 4: Đặt mọi textbox trên sheet thành có thể chỉnh sửa

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Tại sao bạn cần điều này:**  
Mặc định, các textbox được nhập từ Excel sẽ ở chế độ chỉ đọc khi hiển thị trong PowerPoint. Đặt `IsEditable = true` cho phép bạn (hoặc người dùng PowerPoint sau này) chỉnh sửa văn bản trực tiếp trên slide.

## Bước 5: Lưu workbook dưới dạng bản trình chiếu PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Quá trình bên trong:**  
`Workbook.Save` phát hiện giá trị enum `SaveFormat.Pptx` và chuyển đổi bố cục sheet Excel — bao gồm các hàng, cột, biểu đồ và các textbox hiện có thể chỉnh sửa — thành các đối tượng slide PowerPoint.

## Mã nguồn đầy đủ (có thể chạy được)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Kết quả mong đợi

Khi bạn chạy chương trình (`dotnet run`), bạn sẽ thấy:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Mở `output.pptx` trong Microsoft PowerPoint sẽ hiển thị một slide phản ánh chính xác sheet Excel gốc. Tất cả các textbox có thể được chỉnh sửa trực tiếp bằng cách nhấp đúp vào chúng.

## Các câu hỏi thường gặp và trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Tôi có thể chuyển đổi một worksheet cụ thể thay vì worksheet đầu tiên không?** | Có. Thay `workbook.Worksheets[0]` bằng `workbook.Worksheets["SheetName"]` hoặc bất kỳ chỉ mục nào bạn cần. |
| **Nếu workbook chứa nhiều sheet thì sao?** | Gọi `workbook.Save` cho mỗi worksheet, cung cấp một tên file PPTX riêng cho mỗi sheet, hoặc kết hợp chúng thành một bản trình chiếu duy nhất bằng cách sử dụng các đối tượng `Presentation` từ Aspose.Slides. |
| **Biểu đồ có được giữ lại không?** | Aspose.Cells tự động chuyển đổi các biểu đồ Excel thành đối tượng biểu đồ PowerPoint. Không cần thêm mã nào. |
| **Làm sao để thay đổi kích thước slide?** | Sau khi `workbook.Save`, bạn có thể tải file PPTX đã tạo bằng Aspose.Slides và điều chỉnh `Presentation.SlideSize`. |
| **Nếu tôi cần chỉnh sửa văn bản textbox trước khi lưu thì sao?** | Truy cập `shapeItem.TextBox.Text` trong vòng lặp, sửa đổi nó, sau đó đặt `IsEditable = true`. Ví dụ: `shapeItem.TextBox.Text = "New title";` |

## Mẹo khắc phục sự cố

* **“ShapeType.TextBox” không tìm thấy** – Đảm bảo bạn đang sử dụng Aspose.Cells phiên bản 25.11 hoặc mới hơn; các phiên bản cũ hơn không có thuộc tính `IsEditable`.  
* **Lỗi không tìm thấy file** – Kiểm tra xem `YOUR_DIRECTORY` có phải là đường dẫn tuyệt đối hay không hoặc đường dẫn tương đối có trỏ đúng vị trí.  
* **Giấy phép chưa được áp dụng** – Gọi `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` trước khi tải workbook để loại bỏ watermark dùng thử.

## Kết luận

Bây giờ bạn đã biết cách **save Excel as PowerPoint** bằng C# bằng cách tải workbook XLSX, làm cho mọi textbox có thể chỉnh sửa, và xuất ra PPTX. Phương pháp này tự động xử lý biểu đồ, hình ảnh và định dạng ô, cung cấp cho bạn một bộ slide sẵn sàng trình bày.

Tiếp theo, khám phá các chủ đề liên quan như **convert Excel to PowerPoint with Aspose.Slides**, **how to edit textboxes programmatically after conversion**, hoặc **batch‑process multiple workbooks**. Mỗi chủ đề này dựa trên các bước cốt lõi đã trình bày và có thể tự động hoá quy trình báo cáo của bạn hơn nữa.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã đầy đủ, hoạt động, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách chuyển đổi Excel sang PowerPoint bằng Aspose.Cells cho .NET: Hướng dẫn đầy đủ](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cách sao chép Pivot Table trong C# – Chuyển đổi Excel sang PPTX, sao chép vùng và tạo Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Cách lưu file Excel ở nhiều định dạng bằng Aspose.Cells .NET (Hướng dẫn 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}