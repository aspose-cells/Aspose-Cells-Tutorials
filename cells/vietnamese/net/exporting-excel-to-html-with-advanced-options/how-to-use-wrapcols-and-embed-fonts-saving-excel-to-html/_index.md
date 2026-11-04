---
category: general
date: 2026-10-20
description: Tìm hiểu cách sử dụng wrapcols trong Aspose.Cells, nhúng phông chữ vào
  HTML và lưu Excel dưới dạng HTML với ví dụ C# đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: vi
lastmod: 2026-10-20
og_description: Cách sử dụng wrapcols trong Aspose.Cells, nhúng phông chữ vào HTML
  và chuyển đổi workbook sang HTML với hướng dẫn C# rõ ràng cho các nhà phát triển.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Cách sử dụng wrapcols và nhúng phông chữ khi xuất Excel sang HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Cách sử dụng wrapcols và nhúng phông chữ khi lưu Excel sang HTML
url: /vi/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng wrapcols và nhúng phông chữ khi lưu Excel thành HTML

Nếu bạn cần **cách sử dụng wrapcols** trong một công thức Aspose.Cells, hướng dẫn này sẽ chỉ cho bạn các bước chính xác. Bạn cũng sẽ học cách **nhúng phông chữ trong HTML** và **lưu Excel dưới dạng HTML** để kết quả hiển thị giống hệt trên mọi trình duyệt.  

Bài hướng dẫn bao gồm ba kịch bản thực tế: sử dụng hàm `WRAPCOLS`, xuất workbook với phông chữ được nhúng, và tạo báo cáo master‑detail với Smart Markers. Khi kết thúc, bạn sẽ có một chương trình C# duy nhất, có thể chạy được, minh họa tất cả các tính năng này.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 (hoặc mới hơn) đã được cài đặt.
* Aspose.Cells for .NET đã được thêm vào dự án của bạn (`dotnet add package Aspose.Cells`).
* Kiến thức cơ bản về C# và công thức Excel.

Không cần thư viện bên thứ ba nào khác; Aspose.Cells xử lý việc chuyển đổi HTML và nhúng phông chữ nội bộ.

## Bước 1: Trình diễn hàm **cách sử dụng wrapcols** trong công thức

Hàm `WRAPCOLS` chia một phạm vi một chiều thành một mảng hai chiều, điền dữ liệu theo cột trước. Điều này hữu ích khi bạn cần tái cấu trúc dữ liệu cho báo cáo hoặc biểu đồ.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Tại sao điều này hoạt động:**  
`WRAPCOLS` nhận hai đối số – phạm vi nguồn và số cột. Hàm này điền mảng theo chiều cột, loại bỏ bất kỳ giá trị thừa nào (số `3` trong ví dụ). Kết quả xuất hiện ở ô trên‑trái của phạm vi đích (`B1`), và bạn có thể mở rộng phạm vi thủ công nếu cần toàn bộ mảng.

> **Mẹo:** Sau khi đặt công thức, gọi `workbook.CalculateFormula()` để đảm bảo kết quả được cập nhật trước khi đọc giá trị ô.

## Bước 2: **Chuyển workbook sang HTML** và **nhúng phông chữ trong html**

Khi bạn xuất tệp Excel sang HTML, phông chữ thường bị thay thế bằng phông mặc định của trình duyệt, gây mất bố cục hình ảnh. Aspose.Cells cho phép bạn nhúng trực tiếp các phông chữ chính xác được sử dụng trong workbook vào tệp HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Tại sao việc nhúng phông chữ quan trọng:**  
Khi `EmbedFonts` được đặt là `true`, Aspose.Cells chuyển đổi mỗi phông TrueType/OpenType được sử dụng thành một quy tắc `@font-face` được mã hoá Base64 trong HTML được tạo. Điều này loại bỏ nhu cầu máy khách phải cài đặt cùng các phông chữ, đảm bảo việc hiển thị pixel‑perfect.

> **Trường hợp đặc biệt:** Nếu workbook nguồn tham chiếu một phông chữ không được cài đặt trên máy chủ, Aspose.Cells sẽ chuyển sang phông mặc định và đưa ra cảnh báo. Đảm bảo các phông chữ cần thiết có sẵn


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh kèm giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách sử dụng WRAPCOLS trong C# – Tạo Excel Workbook với các hàm Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Cách nhúng phông chữ trong HTML – Chuyển Excel sang HTML với C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Cách chuyển đổi tệp Excel sang HTML bằng Aspose.Cells cho .NET: Ẩn nội dung chồng lên](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}