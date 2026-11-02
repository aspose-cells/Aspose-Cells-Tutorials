---
category: general
date: 2026-08-04
description: Xuất biểu đồ Excel sang PowerPoint bằng Aspose.Cells trong C#. Thực hiện
  theo hướng dẫn chuyển đổi Excel sang PowerPoint từng bước và giữ cho các hình dạng
  có thể chỉnh sửa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: vi
lastmod: 2026-08-04
og_description: Xuất biểu đồ Excel sang PowerPoint bằng Aspose.Cells trong C#. Tìm
  hiểu cách tạo tệp PPTX có thể chỉnh sửa, bảo tồn dữ liệu biểu đồ và tự động chuyển
  đổi từ Excel sang PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Xuất biểu đồ Excel sang PowerPoint bằng C# – hướng dẫn đầy đủ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Xuất biểu đồ Excel sang PowerPoint bằng C# – hướng dẫn đầy đủ Aspose.Cells
url: /vi/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất biểu đồ Excel sang PowerPoint bằng C# – hướng dẫn đầy đủ Aspose.Cells

Nếu bạn cần **export Excel chart to PowerPoint**, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng Aspose.Cells và Aspose.Slides trong C#. Bạn sẽ nhận được một tệp PPTX có thể chỉnh sửa hoàn toàn, giữ nguyên dữ liệu và hình dạng của biểu đồ, giúp việc chuyển đổi sẵn sàng cho các công việc thiết kế tiếp theo.

Việc xuất biểu đồ từ Excel sang PowerPoint là một yêu cầu phổ biến khi xây dựng các quy trình báo cáo tự động, bộ trình bày bán hàng, hoặc tài liệu đào tạo. Trong hướng dẫn này, bạn sẽ học các bước chính xác để thực hiện một **Excel to PowerPoint conversion** giữ nguyên mọi thành phần của biểu đồ có thể chỉnh sửa. Không cần sao chép‑dán thủ công, và mã hoạt động với .NET 6+ cũng như .NET Framework truyền thống.

## Yêu cầu trước

- Một giấy phép Aspose.Cells hợp lệ (hoặc khóa đánh giá miễn phí)  
- Aspose.Slides for .NET đã được thêm vào dự án (thư viện này xử lý đầu ra PPTX)  
- .NET 6 SDK hoặc phiên bản mới hơn đã được cài đặt  
- Một workbook Excel chứa ít nhất một biểu đồ (trong ví dụ này chúng tôi sử dụng `Shapes.xlsx`)  

Bạn có thể cài đặt các gói NuGet bằng các lệnh sau:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Bước 1: Tải workbook Excel

Hoạt động đầu tiên là mở workbook chứa biểu đồ bạn muốn xuất. `Lớp Workbook` đại diện cho toàn bộ tệp Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Tại sao điều này quan trọng:** Việc tải workbook cho phép bạn truy cập vào các worksheet, biểu đồ và định dạng của nó. Aspose.Cells đọc tệp mà không cần cài đặt Microsoft Office, giúp giải pháp nhẹ và thân thiện với máy chủ.

## Bước 2: Chọn worksheet và xác định vùng in

Một worksheet có thể chứa nhiều biểu đồ, nhưng bạn thường xuất một vùng cụ thể. Thiết lập `PrintArea` cho Aspose.Cells biết những ô (bao gồm cả biểu đồ) cần được render.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Tại sao điều này quan trọng:** Bằng cách giới hạn việc xuất vào một vùng in đã định, bạn tránh được các slide trống không cần thiết và giữ kích thước tệp PPTX nhỏ. Vùng này có thể điều chỉnh để khớp chính xác với phạm vi biểu đồ của bạn.

## Bước 3: Cấu hình tùy chọn xuất cho PPTX có thể chỉnh sửa

Aspose.Cells sử dụng lớp `ImageOrPrintOptions` để kiểm soát định dạng đầu ra và khả năng chỉnh sửa. Đặt `ImageFormat` thành `ImageFormat.Pptx` tạo ra tệp PowerPoint, trong khi `ExportEditableShapes = true` giữ lại các đối tượng biểu đồ dưới dạng shape có thể chỉnh sửa.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Tại sao điều này quan trọng:** Cờ `ExportEditableShapes` là chìa khóa để có kết quả **editable shapes in PowerPoint**. Nếu không có nó, biểu đồ sẽ được raster hoá thành hình ảnh, mất khả năng chỉnh sửa các điểm dữ liệu hoặc kiểu dáng sau này.

## Bước 4: Lưu worksheet dưới dạng bản trình bày PowerPoint

Cuối cùng, gọi phương thức `Save` trên đối tượng `Workbook`. Enum `SaveFormat.Pptx` cho Aspose.Cells biết tạo ra tệp PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Khi mã hoàn thành, mở `ShapesExport.pptx` trong PowerPoint. Bạn sẽ thấy một slide chứa biểu đồ Excel gốc dưới dạng đối tượng biểu đồ PowerPoint gốc. Nhấp đúp vào biểu đồ để chỉnh sửa dữ liệu, thay đổi màu sắc, hoặc thêm hoạt ảnh—giống như khi bạn tạo biểu đồ trực tiếp trong PowerPoint.

### Kết quả mong đợi

| Tên tệp                | Nội dung trên slide                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Biểu đồ từ `Shapes.xlsx` được hiển thị dưới dạng biểu đồ PowerPoint có thể chỉnh sửa, với nhãn trục, chú giải và chuỗi dữ liệu vẫn nguyên vẹn. |

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép, dán và chạy. Nó bao gồm tất cả các câu lệnh `using` cần thiết, xử lý lỗi và chú thích.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Giải thích từng khối**

| Block | Purpose |
|-------|---------|
| `using` directives | Kéo vào các namespace của Aspose.Cells và Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Tải tệp Excel mà không cần cài đặt Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Giới hạn việc xuất vào vùng chứa biểu đồ. |
| `ImageOrPrintOptions` | Cấu hình đầu ra PPTX và bật **Aspose.Cells PPTX export** với các shape có thể chỉnh sửa. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Ghi tệp PowerPoint ra đĩa. |
| `try / catch` | Cung cấp xử lý lỗi cơ bản cho các trường hợp thiếu tệp hoặc vấn đề giấy phép. |

Chạy chương trình này sẽ tạo ra một slide PowerPoint mà bạn có thể mở trong Microsoft PowerPoint, Google Slides (sau khi chuyển đổi), hoặc bất kỳ trình xem tương thích nào.

## Các biến thể thường gặp và trường hợp đặc biệt

### Xuất nhiều worksheet

Nếu bạn cần một slide cho mỗi worksheet, lặp qua `workbook.Worksheets` và gọi `Save` với tên tệp duy nhất cho mỗi lần lặp.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Kiểm soát bố cục slide

Aspose.Slides cho phép bạn thêm bố cục slide tùy chỉnh sau khi xuất. Tạo một bản trình bày mới, nhập slide đã tạo, và sau đó áp dụng chủ đề master.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Xử lý biểu đồ với nguồn dữ liệu bên ngoài

Nếu một biểu đồ tham chiếu tới phạm vi dữ liệu nằm ngoài vùng in đã định, mở rộng `PrintArea` để bao gồm các ô đó. Nếu không, biểu đồ có thể mất chuỗi dữ liệu khi xuất.

### Lưu ý về giấy phép

Thư viện Aspose hoạt động ở chế độ đánh giá với watermark. Để loại bỏ watermark, đặt giấy phép trước bất kỳ lời gọi API nào:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Thực hiện tương tự cho Aspose.Slides nếu bạn sử dụng các tính năng nâng cao của nó.

## Mẹo chuyên nghiệp

- **Tái sử dụng tùy chọn xuất:** Tạo một thể hiện `ImageOrPrintOptions` duy nhất và gán nó cho mỗi worksheet để giữ mã DRY.  
- **Xử lý hàng loạt:** Đối với báo cáo quy mô lớn, kết hợp logic xuất này với background worker hoặc Azure Function để tạo tệp PPTX theo yêu cầu.  
- **Hiệu năng:** Nếu bạn chỉ cần hình ảnh biểu đồ (không chỉnh sửa), đặt `ExportEditableShapes = false`. Điều này giảm sử dụng bộ nhớ và tăng tốc độ chuyển đổi.  
- **Kiểm thử:** Xác minh tệp PPTX được tạo trên cả PowerPoint Windows và macOS, vì một số vấn đề render có thể khác nhau giữa các nền tảng.

## Kết luận

Bây giờ bạn đã có một giải pháp hoàn chỉnh, từ đầu đến cuối cho **export Excel chart to PowerPoint** bằng C#. Hướng dẫn đã đề cập đến việc tải workbook, chọn vùng in, cấu hình **Aspose.Cells PPTX export** với **editable shapes in PowerPoint**, và lưu kết quả dưới dạng tệp PPTX có thể chỉnh sửa hoàn toàn.  

Từ đây bạn có thể khám phá các kịch bản **Excel to PowerPoint conversion** bổ sung như xuất hàng loạt, bố cục slide tùy chỉnh, hoặc tích hợp quy trình vào một Web API. Thử nghiệm với các loại biểu đồ khác nhau, thêm hình ảnh, hoặc kết hợp nhiều worksheet thành một bản trình bày duy nhất để điều chỉnh đầu ra phù hợp với nhu cầu kinh doanh của bạn.

Sẵn sàng tự động hoá quy trình báo cáo của bạn? Hãy thử thay đổi tệp nguồn, điều chỉnh vùng in, và tích hợp mã vào các dịch vụ .NET hiện có của bạn. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Chuyển Đổi Excel sang PowerPoint Sử Dụng Aspose.Cells cho .NET: Hướng Dẫn Đầy Đủ](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cách Xuất Biểu Đồ Excel sang PDF Sử Dụng Aspose.Cells cho .NET: Hướng Dẫn Từng Bước](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Xuất Ô Excel sang Hình Ảnh Sử Dụng Aspose.Cells .NET: Hướng Dẫn Từng Bước](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}