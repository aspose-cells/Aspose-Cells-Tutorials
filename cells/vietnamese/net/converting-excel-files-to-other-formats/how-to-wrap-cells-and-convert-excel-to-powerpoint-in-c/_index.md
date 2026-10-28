---
category: general
date: 2026-09-18
description: Cách gói các ô trong một workbook Excel và lưu dưới dạng tệp PowerPoint.
  Tìm hiểu cách sử dụng WRAPCOLS, tạo worksheet trong workbook và xuất ra PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: vi
lastmod: 2026-09-18
og_description: Cách gói ô trong Excel và xuất workbook thành tệp PowerPoint có thể
  chỉnh sửa bằng C#. Hãy theo dõi hướng dẫn từng bước để thành thạo WRAPCOLS và việc
  tạo worksheet trong workbook.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: Cách bọc ô và chuyển đổi Excel sang PowerPoint bằng C#
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Cách bọc ô và chuyển đổi Excel sang PowerPoint trong C#
url: /vi/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách gói ô và chuyển đổi Excel sang PowerPoint bằng C#

Nếu bạn cần **cách gói ô** trong một bảng Excel và sau đó chuyển bảng đó thành bản trình chiếu PowerPoint, hướng dẫn này sẽ cung cấp cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy. Sau hai câu đầu tiên, bạn sẽ biết chính xác API nào thực hiện việc gói và phương thức nào lưu tệp dưới dạng PPTX.

Chúng ta sẽ sử dụng Aspose.Cells for .NET, một thư viện cho phép bạn thao tác với các workbook Excel mà không cần cài đặt Microsoft Office. Bài học bao gồm **chuyển đổi Excel sang PowerPoint**, trình bày **cách sử dụng WRAPCOLS**, và giải thích các thực hành tốt nhất khi **tạo worksheet workbook**. Không cần công cụ bên ngoài—chỉ cần môi trường phát triển .NET.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+)
- Gói NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Kiến thức cơ bản về C# và khái niệm worksheet
- Một IDE như Visual Studio hoặc VS Code

> **Mẹo chuyên nghiệp:** Sử dụng giấy phép dùng thử miễn phí của Aspose.Cells khi thử nghiệm; thay thế bằng giấy phép đầy đủ trước khi đưa vào sản xuất.

## Bước 1: Tạo workbook và thêm worksheet

Điều đầu tiên bạn phải **tạo worksheet workbook** là khởi tạo một đối tượng `Workbook`. Mặc định Aspose.Cells tạo một worksheet (chỉ mục 0), chúng ta sẽ dùng nó cho bản demo.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**Tại sao điều này quan trọng:** Khởi tạo workbook cung cấp cho bạn một canvas sạch sẽ. Worksheet mặc định đã nằm trong bộ sưu tập `Worksheets`, vì vậy bạn không cần gọi `Add()` trừ khi muốn thêm các sheet khác.

## Bước 2: Điền dữ liệu vào phạm vi nguồn (A2:A10)

Trước khi chúng ta có thể **cách gói ô**, cần có dữ liệu để gói. Bước này sẽ điền các ô A2 tới A10 bằng văn bản mẫu.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**Trường hợp biên:** Nếu phạm vi nguồn rỗng, `WRAPCOLS` sẽ trả về `#VALUE!`. Luôn đảm bảo phạm vi chứa ít nhất một ô không trống.

## Bước 3: Áp dụng công thức WRAPCOLS

Bây giờ chúng ta trả lời câu hỏi cốt lõi **cách sử dụng WRAPCOLS**. Công thức này nhận một phạm vi dọc và bố trí nó thành một số cột xác định. Chúng ta ghi công thức vào ô `A1`; mảng kết quả sẽ tự động tràn sang các ô lân cận.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**Bên trong thực tế:** `WRAPCOLS` đánh giá phạm vi nguồn, chia các mục đều nhau (hoặc gần nhất) vào các cột đích, và ghi các giá trị vào một khối hình chữ nhật. Kích thước khối là động, vì vậy bạn không cần định nghĩa trước phạm vi đích.

## Bước 4: Lưu workbook dưới dạng tệp PowerPoint có thể chỉnh sửa

Cuối cùng, chúng ta giải quyết **chuyển đổi Excel sang PowerPoint** và **lưu Excel dưới dạng PowerPoint**. Aspose.Cells có thể xuất trực tiếp một worksheet ra PPTX, giữ nguyên bố cục dưới dạng một shape có thể chỉnh sửa.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**Tại sao lại là PPTX?** PowerPoint được tạo chứa một slide duy nhất với các ô đã gói hiển thị dưới dạng bảng. Bạn có thể mở tệp trong Microsoft PowerPoint, chỉnh sửa văn bản, thay đổi kiểu, hoặc thêm slide bổ sung—mọi thứ vẫn hoàn toàn có thể chỉnh sửa.

### Kết quả mong đợi

- **Mặt Excel:** Ô `A1` hiển thị một mảng 3 cột của các chuỗi dài gốc, mỗi cột chứa gần như số hàng bằng nhau.
- **Mặt PowerPoint:** Khi mở `ChartEditable.pptx` sẽ hiển thị một slide với bảng phản ánh bố cục đã gói. Bảng có thể được chọn, thay đổi kích thước hoặc chỉnh sửa giống như bất kỳ đối tượng PowerPoint gốc nào.

## Các biến thể phổ biến và lưu ý

| Kịch bản | Điều chỉnh |
|----------|------------|
| **Gói vào nhiều cột hơn** | Thay đổi đối số thứ hai của `WRAPCOLS`, ví dụ: `=WRAPCOLS(A2:A10,5)`. |
| **Gói một phạm vi khác** | Cập nhật tham chiếu công thức, ví dụ: `=WRAPCOLS(B2:B15,2)`. |
| **Xuất chỉ một phần của sheet** | Sử dụng `Worksheet.ExportDataTable` để trích xuất một `DataTable` rồi dùng API `Presentation` để tạo PPTX tùy chỉnh. |
| **Worksheet lớn ( > 10 000 dòng )** | Xem xét chia xuất thành nhiều slide để tránh tắc nghẽn hiệu năng. |

> **Cảnh báo:** Xuất PPTX mặc định sẽ render worksheet dưới dạng một hình ảnh duy nhất khi workbook chứa biểu đồ. Sử dụng `WRAPCOLS` giúp dữ liệu vẫn ở dạng bảng, giữ được khả năng chỉnh sửa.

## Mã nguồn đầy đủ để sao chép nhanh

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

Lưu tệp dưới tên `Program.cs`, khôi phục gói NuGet, và chạy:

```bash
dotnet run
```

Bạn sẽ thấy thông báo trên console xác nhận việc xuất, và tệp PPTX sẽ xuất hiện trong thư mục đã chỉ định.

## Kết luận

Bây giờ bạn đã biết **cách gói ô** trong một worksheet Excel, **cách sử dụng WRAPCOLS**, và các bước chính để **chuyển đổi Excel sang PowerPoint** bằng **lưu excel dưới dạng powerpoint** với Aspose.Cells. Giải pháp hoàn chỉnh này minh họa **tạo worksheet workbook**, áp dụng công thức gói, và tạo ra một tệp PPTX có thể chỉnh sửa, sẵn sàng cho các chỉnh sửa trình chiếu.

### Các bước tiếp theo

- Khám phá các hàm Excel khác (ví dụ: `TRANSPOSE`, `FILTER`) trước khi xuất.
- Kết hợp nhiều worksheet thành một bộ PowerPoint đa slide bằng vòng lặp.
- Thêm tiêu đề slide hoặc thương hiệu tùy chỉnh bằng cách tích hợp Aspose.Slides sau khi xuất.

Hãy tự do thử nghiệm với số cột khác nhau, phạm vi nguồn khác, hoặc thậm chí kết hợp biểu đồ và bảng trong cùng một PPTX. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong bài này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Wrap Text in Excel Using Aspose.Cells for .NET | Formatting Tutorial](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Export Excel Workbook and Worksheet Properties to HTML Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}