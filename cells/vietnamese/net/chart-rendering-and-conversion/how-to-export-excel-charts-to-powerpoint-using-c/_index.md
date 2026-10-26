---
category: general
date: 2026-10-26
description: Học cách xuất biểu đồ Excel sang PowerPoint bằng C#. Giữ khả năng chỉnh
  sửa hình dạng và lưu dưới dạng PPTX chỉ trong vài dòng mã.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: vi
lastmod: 2026-10-26
og_description: Xuất biểu đồ Excel sang PowerPoint bằng C#. Hướng dẫn này chỉ cho
  bạn cách giữ các hình dạng có thể chỉnh sửa và lưu dưới dạng PPTX bằng Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Xuất biểu đồ Excel sang PowerPoint bằng C# – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Cách xuất biểu đồ Excel sang PowerPoint bằng C#
url: /vi/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất biểu đồ Excel sang PowerPoint bằng C#

Nếu bạn cần **export Excel charts to PowerPoint**, hướng dẫn này sẽ đưa bạn qua một giải pháp hoàn chỉnh, sẵn sàng chạy. Dù bạn đang xây dựng bảng điều khiển báo cáo hay tự động tạo các bộ slide, bạn sẽ thấy cách chỉ vài dòng mã C# giữ cho các hình dạng biểu đồ của bạn vẫn có thể chỉnh sửa hoàn toàn sau khi chuyển đổi.

Trong tutorial này bạn sẽ học cách:

* Tải một workbook Excel hiện có có chứa biểu đồ.  
* (Tùy chọn) tinh chỉnh các cài đặt workbook trước khi chuyển đổi.  
* Lưu workbook dưới dạng file PowerPoint đồng thời giữ được khả năng chỉnh sửa hình dạng.  

Tất cả đều được thực hiện bằng **Aspose.Cells for .NET**, một thư viện xử lý chuyển đổi Excel‑to‑PowerPoint mà không cần cài đặt Microsoft Office trên server.

## Những gì bạn cần

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 hoặc mới hơn | Môi trường chạy hiện đại với đầy đủ tính năng ngôn ngữ |
| Visual Studio 2022 (hoặc bất kỳ IDE nào) | Trình soạn thảo và trình gỡ lỗi tiện lợi |
| **Aspose.Cells for .NET** NuGet package | Cung cấp lớp `Workbook` và hỗ trợ `SaveFormat.Pptx` |
| Một file Excel (`ChartAndShapes.xlsx`) chứa ít nhất một biểu đồ | Nguồn của các biểu đồ bạn muốn xuất |

> **Mẹo chuyên nghiệp:** Sử dụng phiên bản **Aspose.Cells Evaluation** miễn phí để thử nghiệm mã; một key license sẽ loại bỏ watermark đánh giá.

```bash
dotnet add package Aspose.Cells
```

## Xuất biểu đồ Excel sang PowerPoint – quy trình đầy đủ

Dưới đây là đoạn mã end‑to‑end thực hiện việc xuất đồng thời **giữ khả năng chỉnh sửa hình dạng**. Mỗi bước được giải thích chi tiết.

### Bước 1: Tải workbook Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*Lớp `Workbook` đại diện cho toàn bộ file Excel. Khi tải file, tất cả các worksheet, chart và shape sẽ được đọc vào bộ nhớ, cần thiết cho bất kỳ thao tác tiếp theo nào.*

### Bước 2: (Tùy chọn) Điều chỉnh cài đặt workbook

Trong hầu hết các trường hợp, các cài đặt mặc định đã đủ cho một xuất sạch. Tuy nhiên, nếu bạn cần thay đổi chế độ tính toán, thiết lập trang, hoặc ẩn một số sheet, bạn có thể thực hiện ở đây.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Tại sao điều này quan trọng:** Điều chỉnh cài đặt trước khi chuyển đổi đảm bảo các slide được tạo phản ánh chính xác trạng thái bạn mong muốn, đặc biệt khi công thức hoặc sheet ẩn có thể ảnh hưởng đến dữ liệu biểu đồ.

### Bước 3: Lưu workbook dưới dạng file PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*Hằng số `SaveFormat.Pptx` chỉ cho Aspose.Cells ghi ra một bản trình chiếu PowerPoint. Nội bộ, thư viện sẽ chuyển đổi mỗi chart Excel thành một shape PowerPoint vẫn có thể chỉnh sửa đầy đủ trong Microsoft PowerPoint.*

### Bước 4: Xác minh kết quả

Mở `Shapes.pptx` trong PowerPoint và:

1. Chọn một chart trên bất kỳ slide nào.  
2. Nhấp chuột phải → **Edit Data**.  
3. Xác nhận bảng dữ liệu của chart xuất hiện và bạn có thể sửa các giá trị.

Nếu chart mở **Edit Data** pane, việc chuyển đổi đã thành công và **khả năng chỉnh sửa hình dạng** được giữ lại.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Ví dụ xuất biểu đồ Excel sang PowerPoint"}

## Các lỗi thường gặp và cách tránh chúng

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|------------|----------------|
| Biểu đồ xuất hiện dưới dạng hình ảnh tĩnh | Sử dụng phiên bản Aspose.Cells cũ không hỗ trợ xuất PPTX | Nâng cấp lên Aspose.Cells 23.x mới nhất hoặc mới hơn |
| Dữ liệu thiếu trong biểu đồ PowerPoint | Workbook chưa được tính toán đầy đủ trước khi xuất | Gọi `workbook.CalculateFormula()` trước `Save` |
| Các hình dạng không thể chỉnh sửa | Lưu bằng `SaveFormat.Xlsx` thay vì `SaveFormat.Pptx` | Đảm bảo truyền `SaveFormat.Pptx` vào `Workbook.Save` |
| Ngoại lệ giấy phép tại thời gian chạy | Phiên bản đánh giá không có giấy phép đã đăng ký | Đăng ký giấy phép của bạn bằng `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Trường hợp đặc biệt: Xuất nhiều worksheet có chart riêng biệt

Nếu file Excel của bạn chứa nhiều worksheet, mỗi worksheet có chart riêng, Aspose.Cells sẽ tự động tạo một slide riêng cho mỗi chart. Bạn có thể kiểm soát thứ tự slide bằng cách sắp xếp lại các worksheet trước khi thực hiện lưu.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Mẹo hiệu năng: Stream đầu ra thay vì ghi ra đĩa

Khi tạo file PowerPoint trong một web API, tránh tạo file tạm bằng cách ghi vào một `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Ví dụ đầy đủ, có thể chạy

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Kết quả mong đợi:** Console in ra thông báo xác nhận, và `Shapes.pptx` mở trong PowerPoint với mỗi chart Excel xuất hiện trên một slide riêng. Khi chọn một chart, bạn có thể chỉnh sửa dữ liệu, xác nhận rằng **khả năng chỉnh sửa hình dạng** được giữ lại.

## Tóm tắt và các bước tiếp theo

Bạn đã biết cách **export Excel charts to PowerPoint** bằng C# đồng thời giữ cho các chart vẫn có thể chỉnh sửa. Cốt lõi của giải pháp là phương thức `Workbook.Save` với `SaveFormat.Pptx`, một tính năng của **Aspose.Cells export** giúp trừu tượng hoá việc xử lý Open XML phức tạp.

Từ đây bạn có thể khám phá:

* Thêm tiêu đề slide hoặc ghi chú tùy chỉnh bằng API **Aspose.Slides**.  
* Chuyển đổi các đối tượng Excel khác (bảng, hình ảnh) cùng với chart.  
* Tự động xử lý hàng loạt nhiều workbook trong một service nền.

Hãy thử nghiệm các cài đặt tùy chọn ở trên, và tích hợp mẫu này vào quy trình báo cáo của bạn để tạo PowerPoint nhanh chóng và đáng tin cậy.

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Xuất biểu đồ Excel sang PowerPoint với C# – hướng dẫn đầy đủ Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Cách xuất Excel sang PowerPoint với C# – Hướng dẫn đầy đủ](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Cách xuất các hình dạng từ Excel sang PowerPoint – Hướng dẫn đầy đủ](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}