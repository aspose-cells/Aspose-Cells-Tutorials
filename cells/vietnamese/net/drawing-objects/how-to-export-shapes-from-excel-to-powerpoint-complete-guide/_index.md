---
category: general
date: 2026-07-26
description: Cách xuất các hình dạng từ bảng tính Excel sang PowerPoint chỉ trong
  vài bước – hướng dẫn nhanh xuất Excel sang PPTX cho nhà phát triển.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: vi
lastmod: 2026-07-26
og_description: Cách xuất các hình dạng từ Excel sang PowerPoint từng bước một. Hãy
  làm theo hướng dẫn xuất Excel sang PPTX này và xem các bảng tính của bạn biến thành
  các slide có thể chỉnh sửa.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Cách xuất các hình dạng từ Excel sang PowerPoint – Nhanh và Dễ dàng
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Cách xuất các hình dạng từ Excel sang PowerPoint – Hướng dẫn toàn diện
url: /vi/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất các hình dạng từ Excel sang PowerPoint – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách xuất các hình dạng** từ một tệp Excel và giữ chúng có thể chỉnh sửa trong một bản trình chiếu PowerPoint chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một pipeline báo cáo hay chỉ cần một cách nhanh chóng để chuyển một bảng tính thành bản trình bày, khả năng **chuyển đổi worksheet sang PowerPoint** mà không mất khả năng chỉnh sửa hình dạng có thể tiết kiệm cho bạn hàng giờ công việc thủ công.

Trong **excel to powerpoint tutorial** này, chúng tôi sẽ hướng dẫn qua một ví dụ C# hoàn chỉnh, tải một workbook, cấu hình các tùy chọn xuất phù hợp, và ghi một tệp PPTX trong đó các hộp văn bản và các đối tượng vẽ khác vẫn có thể chỉnh sửa. Không có tham chiếu mơ hồ—chỉ có mã bạn có thể sao chép, dán và chạy ngay hôm nay.

## Những gì bạn sẽ học

- Các bước chính xác để **export excel to pptx** trong khi giữ nguyên khả năng chỉnh sửa hình dạng.  
- Cách thư viện `Aspose.Cells` với `PptxSaveOptions` kiểm soát hành vi xuất.  
- Mẹo xử lý nhiều worksheet, tệp bị thiếu, và cài đặt hình dạng tùy chỉnh.  
- Một chương trình hoàn chỉnh, có thể chạy được mà bạn có thể đưa vào bất kỳ dự án .NET nào.

### Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động trên .NET Framework 4.7+).  
- Giấy phép hợp lệ cho **Aspose.Cells for .NET** (bản dùng thử miễn phí hoạt động cho việc thử nghiệm).  
- Một workbook Excel (ví dụ, `ShapesDemo.xlsx`) chứa ít nhất một hộp văn bản hoặc hình dạng.  
- Môi trường phát triển—Visual Studio, Rider, hoặc VS Code đều được.

Nếu bạn đã có những thứ này, hãy bắt đầu.

## Bước 1: Tải Workbook – Điểm khởi đầu cho Cách xuất các hình dạng  

Đầu tiên chúng ta cần mở tệp Excel chứa các hình dạng mà chúng ta muốn giữ có thể chỉnh sửa.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Tại sao điều này quan trọng:**  
`Đối tượng` `Workbook` là cổng vào mọi ô, biểu đồ và đối tượng vẽ trong tệp. Bằng cách lấy worksheet đầu tiên (`Worksheets[0]`) chúng ta đảm bảo làm việc với một sheet đã biết, nhưng bạn có thể thay thế chỉ mục bằng tên (`workbook.Worksheets["Sheet2"]`) nếu cần một tab cụ thể.

> **Mẹo chuyên nghiệp:** Đặt lệnh tải trong một khối `try / catch` để cung cấp lỗi thân thiện nếu đường dẫn tệp sai.

## Bước 2: Cấu hình tùy chọn xuất PPTX – Cốt lõi của Cách xuất các hình dạng  

Bây giờ chúng ta chỉ định cho Aspose.Cells giữ các hình dạng có thể chỉnh sửa trong PPTX kết quả.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Tại sao lại dùng các cờ này?**  
- `ExportEditableTextBoxes` chuyển các hộp văn bản Excel thành các placeholder văn bản PowerPoint mà bạn có thể nhấp đúp và chỉnh sửa.  
- `ExportEditableShapes` làm tương tự cho các hình dạng như mũi tên, hình chữ nhật và SmartArt. Nếu không có chúng, các đối tượng sẽ trở thành hình ảnh tĩnh, làm mất mục đích của quy trình **convert worksheet to powerpoint**.

Bạn cũng có thể tinh chỉnh `PptxSaveOptions` để kiểm soát kích thước slide, giao diện, hoặc việc nhúng phông chữ—hữu ích khi bản trình bày của bạn phải phù hợp với thương hiệu công ty.

## Bước 3: Lưu Worksheet dưới dạng PPTX – Phần cuối cùng của Export Excel Workbook PowerPoint  

Với các tùy chọn đã được đặt, việc lưu trở nên đơn giản.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Điều gì xảy ra bên trong?**  
Aspose.Cells duyệt qua mọi đối tượng vẽ trên sheet, ánh xạ chúng tới lớp shape tương ứng của PowerPoint, và ghi XML mà PowerPoint đọc. Vì chúng ta đã bật các cờ chỉnh sửa, XML đánh dấu mỗi shape là một `Shape` thay vì `Picture`, vì vậy PowerPoint coi nó là một đối tượng sống.

## Bước 4: Xác nhận xuất – Phản hồi nhanh cho người dùng  

Một thông báo console nhỏ cho bạn biết quá trình đã thành công.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Nếu bạn chạy chương trình và thấy thông báo, mở `ShapesEditable.pptx` trong PowerPoint. Nhấp vào bất kỳ hộp văn bản nào—bạn sẽ có thể chỉnh sửa văn bản trực tiếp, và kéo một shape sẽ di chuyển nó giống như một đối tượng PowerPoint gốc.

## Bước 5: Xử lý các kịch bản thực tế  

Dưới đây là các biến thể phổ biến mà bạn có thể gặp khi làm việc trên một **excel to powerpoint tutorial**.

### Nhiều Worksheet

Nếu bạn cần xuất nhiều sheet vào một PPTX duy nhất, lặp qua `workbook.Worksheets` và gọi `worksheet.Save` với cùng `pptxOptions`. Aspose.Cells sẽ tự động thêm một slide mới cho mỗi sheet.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Bố cục Slide tùy chỉnh

Bạn có thể chỉ định `pptxOptions.SlideSize` (ví dụ, `SlideSizeType.Widescreen`) để phù hợp với kích thước deck công ty của bạn.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### Tệp bị thiếu hoặc quyền truy cập

Đặt toàn bộ phương thức `Main` trong một khối `try`:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Điều này làm cho quy trình **export excel workbook powerpoint** trở nên vững chắc cho các pipeline sản xuất.

## Ví dụ hoàn chỉnh hoạt động

Đây là chương trình đầy đủ mà bạn có thể biên dịch ngay bây giờ. Lưu nó dưới tên `ExportEditableShapes.cs`, điều chỉnh đường dẫn tệp, và chạy `dotnet run`.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Kết quả mong đợi** khi bạn chạy chương trình:

```
Exported worksheet with editable shapes.
```

Mở `ShapesEditable.pptx` đã tạo và bạn sẽ thấy mỗi shape Excel là một đối tượng PowerPoint hoàn toàn có thể chỉnh sửa—đúng như bạn mong muốn khi tìm kiếm **how to export shapes**.

## Câu hỏi thường gặp

- **Điều này có hoạt động với các định dạng Excel cũ hơn (.xls) không?**  
  Có. `Workbook` có thể mở các tệp `.xls`, `.xlsx`, và thậm chí CSV. Việc xuất shape hoạt động tương tự.

- **Nếu tôi cần giữ biểu đồ có thể chỉnh sửa thì sao?**  
  Biểu đồ đã được xuất dưới dạng biểu đồ PowerPoint gốc; bạn không cần cờ bổ sung.

- **Tôi có thể xuất sang PDF thay vì PPTX không?**  
  Chắc chắn—chỉ cần thay `SaveFormat.Pptx` bằng `SaveFormat.Pdf` và bỏ qua `PptxSaveOptions`.

## Kết luận

Bạn hiện đã có một giải pháp toàn diện, đầu‑tới‑cuối cho **how to export shapes** từ Excel sang một deck PowerPoint có thể chỉnh sửa. Bằng cách tận dụng `PptxSaveOptions` của `Aspose.Cells`, bạn giữ lại mọi hộp văn bản và đối tượng vẽ, biến một bảng tính tĩnh thành một bản trình bày động với ít nỗ lực.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thêm slide master tùy chỉnh, chèn hình ảnh bằng mã, hoặc kết hợp việc xuất này vào pipeline CI/CD để tự động tạo các deck bán hàng hàng tuần. Thế giới **export excel workbook powerpoint** rộng mở—hãy khám phá!

--- 

*Nếu bạn thấy **excel to powerpoint tutorial** này hữu ích, hãy đánh dấu sao trên GitHub hoặc chia sẻ với đồng nghiệp vẫn sao chép‑dán bảng tính vào slide. Chúc lập trình vui vẻ!*

## Bạn nên học gì tiếp theo?

Những hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh cùng giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách xuất một Worksheet Excel sang PNG bằng Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Cách xuất các ô Excel dưới dạng hình ảnh bằng Aspose.Cells cho Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [Cách xuất biểu đồ Excel dưới dạng SVG bằng Aspose.Cells Java cho Đồ họa Vector có thể mở rộng](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}