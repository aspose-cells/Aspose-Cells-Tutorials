---
category: general
date: 2026-09-21
description: Xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa bằng Aspose.Cells.
  Thực hiện theo hướng dẫn từng bước này để chuyển đổi một bảng tính sang PPTX trong
  khi vẫn giữ cho biểu đồ có thể chỉnh sửa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: vi
lastmod: 2026-09-21
og_description: Xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa bằng Aspose.Cells.
  Tìm hiểu cách chuyển đổi một bảng tính sang PPTX trong khi vẫn giữ nguyên khả năng
  chỉnh sửa đầy đủ của biểu đồ.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa – Hướng dẫn C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa trong C#
url: /vi/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa trong C#

Xuất Excel sang PowerPoint với biểu đồ có thể chỉnh sửa là một yêu cầu phổ biến khi bạn cần tái sử dụng các hình ảnh bảng tính trong bài thuyết trình. Hướng dẫn này chỉ cho bạn cách **export Excel to PowerPoint** trong khi giữ khả năng chỉnh sửa biểu đồ, sử dụng Aspose.Cells cho .NET.

Bạn sẽ học cách:

* Tải một workbook hiện có chứa biểu đồ và hộp văn bản.  
* Cấu hình các tùy chọn xuất PPTX để biểu đồ và hình dạng vẫn có thể chỉnh sửa.  
* Chuyển đổi một worksheet cụ thể thành tệp PowerPoint có thể mở và chỉnh sửa trong Microsoft PowerPoint.

Bài hướng dẫn giả định bạn có kiến thức cơ bản về C# và một phiên bản .NET mới (≥ .NET 6). Không yêu cầu kinh nghiệm trước với Aspose.Cells.

---

## Xuất Excel sang PowerPoint – tổng quan

Ý tưởng cốt lõi đằng sau **export Excel to PowerPoint** là xem mỗi worksheet như một nguồn hình ảnh có thể được render thành một slide PPTX. Bằng cách bật/tắt các cờ `ExportChartAsEditableText` và `ExportShapeAsEditableText`, Aspose.Cells ghi dữ liệu biểu đồ gốc dưới dạng các đối tượng vẽ của PowerPoint thay vì một bitmap phẳng. Điều này làm cho slide kết quả có thể chỉnh sửa hoàn toàn — giống như một biểu đồ được tạo trực tiếp trong PowerPoint.

> **Tại sao nên sử dụng biểu đồ có thể chỉnh sửa?**  
> Biểu đồ có thể chỉnh sửa cho phép người thuyết trình điều chỉnh dữ liệu, màu sắc hoặc nhãn mà không cần quay lại tệp Excel gốc, giúp tăng tốc các thay đổi vào phút chót và duy trì quy trình làm việc của bài thuyết trình một cách suôn sẻ.

## Chuyển đổi một worksheet sang PowerPoint (worksheet to PowerPoint)

Dưới đây là một ví dụ đầy đủ, có thể chạy được minh họa việc chuyển đổi **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Giải thích từng bước

| Bước | Mã thực hiện gì | Tại sao lại quan trọng đối với **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Tải `input.xlsx` vào một đối tượng `Aspose.Cells.Workbook`. | Workbook cung cấp quyền truy cập vào các biểu đồ bạn muốn xuất. |
| 2️⃣   | Đặt `ExportType` thành `Pptx` và bật `ExportChartAsEditableText` & `ExportShapeAsEditableText`. | Các cờ này là chìa khóa cho **editable charts pptx** – chúng chỉ cho thư viện ghi hình học biểu đồ dưới dạng các đối tượng vẽ của PowerPoint thay vì hình ảnh raster. |
| 3️⃣   | Gọi `ConvertToImage` trên worksheet đầu tiên, tạo ra `Worksheet.pptx`. | Phương thức thực hiện thao tác **export excel to powerpoint** và ghi một tệp PPTX có thể mở trực tiếp trong PowerPoint. |

> **Mẹo chuyên nghiệp:** Nếu bạn cần xuất *nhiều* worksheet, lặp qua `workbook.Worksheets` và gọi `ConvertToImage` cho mỗi worksheet, tùy chọn đặt tên các tệp đầu ra như `Sheet1.pptx`, `Sheet2.pptx`, v.v.

## Bật biểu đồ có thể chỉnh sửa trong PPTX (export excel chart pptx)

Khi `ExportChartAsEditableText` được đặt thành `true`, Aspose.Cells ghi mỗi biểu đồ dưới dạng một tập hợp các phần tử `<a:graphic>` trong XML của PPTX. PowerPoint sau đó coi các phần tử này là các đối tượng biểu đồ gốc, cho phép bạn nhấp đúp để mở trình chỉnh sửa biểu đồ.

**Những khó khăn thường gặp**

* **Missing Aspose.Cells license** – Nếu không có giấy phép, thư viện sẽ thêm watermark vào kết quả. Đăng ký giấy phép sớm trong chương trình của bạn (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Unsupported chart types** – Mặc dù hầu hết các biểu đồ 2‑D (cột, đường, bánh) đều có thể chỉnh sửa hoàn toàn, một số biểu đồ 3‑D phức tạp hoặc biểu đồ kết hợp có thể chuyển sang dạng hình ảnh. Hãy kiểm tra các loại biểu đồ cụ thể của bạn nếu bạn dựa vào khả năng chỉnh sửa đầy đủ.  
* **Large worksheets** – Xuất các worksheet rất lớn có thể tiêu tốn đáng kể bộ nhớ. Xem xét sử dụng `ExportMaxRows` hoặc `ExportMaxColumns` trong `ImageOrPrintOptions` để giới hạn khu vực sẽ được chuyển đổi.

## Mẹo để giữ biểu đồ có thể chỉnh sửa (editable charts pptx)

1. **Preserve chart data ranges** – Đảm bảo nguồn dữ liệu biểu đồ nằm trong cùng worksheet mà bạn đang xuất. Các tham chiếu chéo sheet sẽ được chuyển thành giá trị tĩnh trong PPTX.  
2. **Use the latest Aspose.Cells version** – Các bản phát hành mới cải thiện hỗ trợ cho các tính năng biểu đồ bổ sung và sửa các lỗi đặc biệt liên quan đến xuất PPTX.  
3. **Validate the output** – Sau khi chuyển đổi, mở PPTX đã tạo trong PowerPoint và xác nhận rằng bạn có thể chỉnh sửa tiêu đề biểu đồ, các series và nhãn trục. Nếu bất kỳ thành phần nào xuất hiện dưới dạng hình ảnh, hãy kiểm tra lại rằng `ExportChartAsEditableText` đã được bật và loại biểu đồ được hỗ trợ.  
4. **Batch processing** – Đối với các kịch bản tự động (ví dụ: tạo bộ slide từ nhiều báo cáo Excel), gói logic chuyển đổi trong một phương thức nhận `Workbook`, `int worksheetIndex`, và `string outputPath`. Điều này tách riêng quy trình **export excel to powerpoint** và làm cho nó có thể tái sử dụng.

## Tóm tắt ví dụ làm việc đầy đủ

Kết hợp tất cả lại, đây là chương trình tối thiểu bạn có thể sao chép‑dán vào một dự án console .NET mới:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Kết quả mong đợi**

* Một tệp có tên `Worksheet.pptx` xuất hiện trong `YOUR_DIRECTORY`.  
* Mở tệp trong Microsoft PowerPoint sẽ hiển thị một slide chứa biểu đồ gốc và bất kỳ hộp văn bản nào.  
* Nhấp đúp vào biểu đồ sẽ mở trình chỉnh sửa biểu đồ của PowerPoint, cho phép bạn thay đổi giá trị series, màu sắc hoặc tiêu đề trục — xác nhận tính năng **editable charts pptx** hoạt động như mong đợi.

## Kết luận

Bây giờ bạn đã có một giải pháp hoàn chỉnh cho **export Excel to PowerPoint** giữ cho biểu đồ có thể chỉnh sửa. Bằng cách cấu hình `ImageOrPrintOptions` với `ExportChartAsEditableText` và `ExportShapeAsEditableText`, quá trình chuyển đổi tạo ra một tệp PPTX gốc, trong đó các biểu đồ hoạt động giống như những biểu đồ được tạo trực tiếp trong PowerPoint.

Từ đây bạn có thể:

* Mở rộng mã để xử lý nhiều worksheet (**worksheet to PowerPoint** cho mỗi worksheet).  
* Kết hợp việc xuất với các tính năng khác của Aspose.Cells, chẳng hạn thêm tiêu đề slide hoặc chèn hình ảnh.  
* Khám phá các chủ đề liên quan như **export Excel chart PPTX** với giao diện tùy chỉnh hoặc tự động hoá toàn bộ quy trình tạo bộ slide.

Hãy tự do thử nghiệm với các loại biểu đồ khác nhau, thêm nhãn dữ liệu, hoặc tích hợp quy trình này vào một hệ thống báo cáo lớn hơn. Chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}