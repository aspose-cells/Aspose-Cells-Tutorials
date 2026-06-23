---
category: general
date: 2026-06-05
description: Cách xuất biểu đồ từ PowerPoint bằng C#. Bao gồm xuất các đối tượng OLE
  và làm cho biểu đồ có thể chỉnh sửa trong tệp PPTX kết quả – từng bước.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: vi
og_description: Cách xuất biểu đồ từ PowerPoint bằng C#. Tìm hiểu cách xuất đối tượng
  OLE và làm cho biểu đồ có thể chỉnh sửa trong file PPTX đã lưu – từng bước.
og_title: Cách xuất biểu đồ – Hướng dẫn đầy đủ PowerPoint C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Cách xuất biểu đồ – Hướng dẫn đầy đủ PowerPoint C#
url: /vi/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Xuất Biểu Đồ – Hướng Dẫn PowerPoint C# Hoàn Chỉnh

Bạn đã bao giờ tự hỏi **cách xuất biểu đồ** từ một bộ PowerPoint mà không mất khả năng chỉnh sửa chúng sau này chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình báo cáo, dữ liệu biểu đồ nằm trong file PPTX, và khi bạn chuyển file cho người nhận, họ thường cần chỉnh sửa một giá trị hoặc thay đổi nhãn. Tin tốt là với vài dòng C# bạn có thể giữ được khả năng chỉnh sửa, và thậm chí có thể xuất các đối tượng OLE được nhúng cùng lúc.

Trong tutorial này chúng ta sẽ đi qua một ví dụ thực tế, sẵn sàng chạy, cho thấy **cách xuất biểu đồ**, **cách xuất đối tượng OLE**, và **cách làm cho biểu đồ có thể chỉnh sửa** trong file đầu ra. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng, chèn vào bất kỳ dự án .NET nào sử dụng thư viện Aspose.Slides.

> **Mẹo chuyên nghiệp:** Nếu bạn mới bắt đầu với Aspose.Slides, hãy chắc chắn đã thêm gói NuGet `Aspose.Slides.NET` vào dự án của mình — nếu không code sẽ không biên dịch.

## Những Gì Bạn Cần Chuẩn Bị

| Yêu cầu | Tại sao quan trọng |
|---------|--------------------|
| .NET 6+ (hoặc .NET Framework 4.7+) | Các runtime hiện đại mang lại hiệu năng tốt hơn và quản lý gói dễ dàng hơn. |
| Aspose.Slides for .NET (phiên bản mới nhất) | Thư viện này cung cấp các lớp `Presentation` và `PptxSaveOptions` mà chúng ta sẽ dùng. |
| Một file PowerPoint mẫu có ít nhất một biểu đồ | Bản demo hoạt động trên bất kỳ file `.pptx` nào chứa biểu đồ; bạn sẽ thấy khả năng chỉnh sửa sau khi xuất. |
| Một IDE (Visual Studio, Rider, hoặc VS Code) | Tiện lợi cho việc gỡ lỗi nhanh và xem file đã tạo. |

Không cần công cụ bên thứ ba nào khác — mọi thứ đều được xử lý bởi API của Aspose.

## Bước 1 – Tải Bản Trình Chiếu Nguồn

Đầu tiên chúng ta cần đưa file PPTX gốc vào bộ nhớ. Hãy nghĩ đây như việc mở một tài liệu Word trước khi bắt đầu chỉnh sửa.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Tại sao điều này quan trọng:** Đối tượng `Presentation` là điểm vào cho mọi thao tác tiếp theo. Nó phân tích file, xây dựng mô hình đối tượng của các slide, shape, chart và OLE, và giữ mọi thứ ở trạng thái có thể thay đổi.

## Bước 2 – Tạo Các Tùy Chọn Lưu Và Bật Biểu Đồ Có Thể Chỉnh Sửa

Mặc định, khi bạn gọi `Save` thư viện sẽ làm phẳng biểu đồ thành hình ảnh tĩnh. Để giữ chúng có thể chỉnh sửa, bạn phải bật cờ `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Cách hoạt động:** Khi `ExportEditableCharts` được đặt là `true`, thư viện sẽ ghi định nghĩa XML của biểu đồ (`chart.xml`) vào PPTX thay vì raster hoá nó. PowerPoint sau đó đọc XML này và cho phép người dùng mở trình chỉnh sửa biểu đồ.

## Bước 3 – Bật Xuất Các Đối Tượng OLE Được Nhúng

Nhiều bản trình chiếu nhúng bảng Excel, sơ đồ Visio, hoặc thậm chí file PDF dưới dạng OLE. Nếu bạn muốn chúng tồn tại qua quá trình xuất‑nhập, hãy bật `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Ý nghĩa thực sự của “xuất OLE objects”:** Gói OLE được lưu dưới dạng khối nhị phân trong PPTX. Khi bật cờ này, nhị phân gốc được giữ nguyên, cho phép người nhận nhấp đúp vào đối tượng và mở nó trong ứng dụng gốc (ví dụ: Excel). Nếu không bật, đối tượng OLE sẽ bị loại bỏ, làm mất liên kết và dữ liệu.

## Bước 4 – Lưu Bản Trình Chiếu Với Các Tùy Chọn Đã Cấu Hình

Sau khi đã chuẩn bị các tùy chọn, chúng ta chỉ cần yêu cầu Aspose ghi file ra.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Kết quả:** `editable.pptx` chứa các slide giống như `input.pptx`, nhưng bất kỳ biểu đồ nào đều có thể chỉnh sửa trực tiếp trong PowerPoint, và mọi đối tượng OLE được nhúng vẫn nguyên vẹn.

### Ví Dụ Hoàn Chỉnh Hoạt Động

Dưới đây là chương trình đầy đủ, tự chứa, bạn có thể biên dịch và chạy. Nó bao gồm các câu lệnh `using`, việc giải phóng tài nguyên đúng cách, và các chú thích giải thích từng dòng.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Kết quả mong đợi:** Sau khi chạy chương trình, mở `editable.pptx` trong PowerPoint. Nhấp chuột phải vào bất kỳ biểu đồ nào → *Edit Data* → trình chỉnh sửa biểu đồ sẽ mở, xác nhận rằng **việc làm cho biểu đồ có thể chỉnh sửa** đã thành công. Nhấp đúp vào một sheet Excel được nhúng, và nó sẽ mở trong Excel, chứng minh rằng **xuất OLE objects** đã hoạt động.

![cách xuất biểu đồ sơ đồ](https://example.com/images/export-charts.png "cách xuất biểu đồ – PowerPoint sau khi xuất")

*(Văn bản thay thế: cách xuất biểu đồ – ảnh chụp màn hình PowerPoint với biểu đồ có thể chỉnh sửa và đối tượng OLE)*

## Câu Hỏi Thường Gặp & Các Trường Hợp Cạnh

### Nếu file nguồn không có biểu đồ thì sao?

Code vẫn chạy; `ExportEditableCharts` chỉ không có tác dụng vì không có gì để chuyển đổi. Không có lỗi nào được ném ra.

### Tôi có thể xuất chỉ những biểu đồ cụ thể không?

Có. Thay vì dùng cờ toàn cục `ExportEditableCharts`, bạn có thể duyệt qua `presentation.Slides` và đặt `Chart.IsEditable = true` trên các đối tượng biểu đồ riêng lẻ trước khi lưu. Cách này cho phép kiểm soát chi tiết hơn.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Việc bật xuất OLE có làm tăng kích thước file không?

Một chút. Các luồng OLE nhị phân được lưu nguyên, vì vậy PPTX kết quả có thể lớn hơn vài kilobyte. Trong hầu hết các kịch bản doanh nghiệp, sự đánh đổi này đáng giá vì bạn giữ được khả năng chỉnh sửa đầy đủ.

### Các phiên bản PowerPoint nào có thể mở file kết quả?

Bất kỳ phiên bản nào hỗ trợ chuẩn OOXML (PowerPoint 2007 trở lên). Tính năng biểu đồ có thể chỉnh sửa dựa trên trình chỉnh sửa biểu đồ gốc được giới thiệu trong Office 2007, vì vậy các file nhị phân cũ như `.ppt` sẽ không hưởng lợi.

## Mẹo Cho Mã Sẵn Sàng Sản Xuất

| Mẹo | Lý do |
|-----|-------|
| Sử dụng khối `using` (như trong ví dụ) để giải phóng đối tượng `Presentation`. | Ngăn rò rỉ bộ nhớ, đặc biệt khi xử lý nhiều file trong một batch. |
| Kiểm tra hợp lệ các đường dẫn file trước khi tải. | Tránh `FileNotFoundException` làm dịch vụ nền bị sập. |
| Ghi log các thiết lập `ExportEditableCharts` và `ExportOLEObjects`. | Hữu ích khi người dùng báo cáo biểu đồ không thể chỉnh sửa. |
| Bắt `Aspose.Slides.Exception` riêng biệt. | Cung cấp thông báo lỗi rõ ràng hơn từ thư viện (ví dụ: loại biểu đồ không được hỗ trợ). |
| Xem xét `PptxCompressionLevel` nếu kích thước file quan trọng. | Bạn có thể nén file đầu ra mà vẫn giữ được khả năng chỉnh sửa. |

## Tóm Tắt – Những Gì Chúng Ta Đã Đạt Được

Chúng ta bắt đầu với một câu hỏi rõ ràng: **cách xuất biểu đồ** từ file PowerPoint mà vẫn giữ được khả năng chỉnh sửa và bảo tồn các đối tượng OLE được nhúng. Bằng cách tải bản trình chiếu, cấu hình `PptxSaveOptions` (`ExportEditableCharts = true` và `ExportOLEObjects = true`), và lưu file, chúng ta đã có một PPTX đáp ứng cả hai yêu cầu. Mẫu này có thể tái sử dụng cho chuyển đổi hàng loạt, pipeline CI, hoặc bất kỳ công cụ báo cáo tự động nào.

## Bạn Có Thể Khám Phá Gì Tiếp Theo?

- **Xuất biểu đồ dưới dạng hình ảnh** cho báo cáo tĩnh (`saveOptions.ExportEditableCharts = false`).  
- **Chuyển PPTX sang PDF** trong khi giữ vector graphics (`PdfSaveOptions`).  
- **Thao tác dữ liệu biểu đồ bằng mã** (ví dụ: cập nhật giá trị series trước khi xuất).  
- **Tích hợp với Azure Functions** để cung cấp API xuất biểu đồ theo yêu cầu.

Hãy thử nghiệm, và cho chúng tôi biết những trường hợp đặc biệt bạn gặp phải. Chúc bạn lập trình vui vẻ, và hy vọng mọi biểu đồ của bạn luôn có thể chỉnh sửa!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial dưới đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Apply Themes to Excel Charts Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}