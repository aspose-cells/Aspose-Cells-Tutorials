---
category: general
date: 2026-09-18
description: Tìm hiểu cách mở rộng mảng trong Excel bằng hàm EXPAND, điền dữ liệu
  vào mẫu Excel và tạo một bảng tính Excel với phạm vi động bằng C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: vi
lastmod: 2026-09-18
og_description: Cách mở rộng mảng trong Excel bằng hàm EXPAND, điền dữ liệu vào mẫu
  Excel và xây dựng giải pháp phạm vi động trong Excel bằng mã C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Cách mở rộng mảng trong Excel và điền vào mẫu
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Cách mở rộng mảng trong Excel và điền vào mẫu
url: /vi/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách mở rộng mảng trong Excel và điền vào mẫu

Nếu bạn cần **how to expand array** trong Excel khi điền một mẫu đã được thiết kế trước, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, từ đầu đến cuối. Sử dụng hàm `EXPAND` cùng với Smart Markers của Aspose.Cells, bạn có thể chuyển một tham chiếu ô duy nhất thành một phạm vi 5 × 5 và tự động thay thế các marker như `{IsActive}` bằng dữ liệu thực.

Bạn sẽ thấy cách **populate excel template**, tạo một **dynamic range excel**, và đúng cách **use expand function** trong một dự án C#. Khi kết thúc tutorial, bạn sẽ có một chương trình có thể chạy được, tải một tệp `.xlsx`, mở rộng công thức mảng, áp dụng Smart Markers và lưu kết quả.

## Yêu cầu trước

* .NET 6.0 hoặc phiên bản sau (code cũng hoạt động với .NET Core 3.1+)
* Aspose.Cells cho .NET (gói NuGet `Aspose.Cells`)
* Một workbook Excel chứa ô công thức placeholder (ví dụ, `B2`) và một Smart Marker như `{IsActive}`
* Kiến thức cơ bản về C# và công thức Excel

> **Mẹo chuyên nghiệp:** Hàm `EXPAND` chỉ có sẵn trong Excel cho Microsoft 365 và Excel 2021+. Các phiên bản cũ hơn sẽ trả về lỗi `#NAME?`.

## Bước 1: Cách mở rộng mảng với hàm EXPAND

Bước đầu tiên là tải workbook và viết công thức `EXPAND` chuyển một ô nguồn duy nhất thành một ma trận lớn hơn.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Tại sao điều này quan trọng: `EXPAND` loại bỏ nhu cầu sao chép công thức thủ công qua các hàng và cột. Khi ô nguồn (`A2`) thay đổi, toàn bộ khối 5 × 5 sẽ tự động cập nhật, cung cấp cho bạn một **dynamic range excel** phản ứng với các thay đổi dữ liệu.

## Bước 2: Điền mẫu Excel bằng Smart Markers

Smart Markers cho phép bạn nhúng các placeholder vào trong mẫu, sau đó được thay thế bằng giá trị từ một đối tượng C#. Đây là cách thuận tiện nhất để **populate excel template** mà không cần viết mã cho từng ô.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

Lệnh `SmartMarkersProcessor().Apply` sẽ quét toàn bộ sheet, tìm `{IsActive}` và chèn giá trị boolean. Công thức sau đó sẽ tự động đánh giá thành `"Active"` hoặc `"Inactive"`.

## Bước 3: Xác minh phạm vi đã mở rộng và kết quả đã điền

Sau khi áp dụng cả công thức `EXPAND` và Smart Markers, bạn có thể đọc một vài ô bằng chương trình để đảm bảo mọi thứ hoạt động như mong đợi.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Chạy chương trình sẽ in ra giá trị gốc từ `A2` (hoặc kết quả mảng) và either **Active** hoặc **Inactive** tùy thuộc vào cờ `IsActive`.

## Bước 4: Lưu workbook – kết quả cuối cùng

Cuối cùng, ghi workbook đã chỉnh sửa ra đĩa. Bước này minh họa quy trình đầy đủ từ tải, mở rộng, điền dữ liệu, đến lưu file.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

File `output.xlsx` đã lưu hiện chứa ma trận 5 × 5 được tạo bởi công thức `EXPAND` và một ô phản ánh giá trị của `{IsActive}`. Mở file trong Excel để xem phạm vi động đang hoạt động.

## Các trường hợp đặc biệt và thực hành tốt nhất

| Tình huống                              | Khuyến nghị                                                                 |
|----------------------------------------|------------------------------------------------------------------------------|
| Excel version does not support `EXPAND`| Quay lại các công thức cổ điển `=OFFSET` hoặc `=INDEX`, hoặc nâng cấp lên Office 365. |
| Need to expand to a variable size      | Sử dụng `ROWS(source)` và `COLUMNS(source)` trong `EXPAND` để đạt tính động thực sự.   |
| Multiple Smart Markers in the same sheet| Gọi `SmartMarkersProcessor().Apply` một lần với một đối tượng dữ liệu tổng hợp.      |
| Large workbooks ( > 10 000 rows)       | Vô hiệu hoá tính toán khi ghi công thức (`workbook.Settings.CheckFormula = false`). |

## Ví dụ làm việc đầy đủ

Dưới đây là chương trình hoàn chỉnh, tự chứa mà bạn có thể sao chép‑dán vào một dự án console mới.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Kết quả mong đợi khi bạn chạy chương trình** (giả sử `A2` chứa số `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Mở `output.xlsx` sẽ hiển thị khối 5 × 5 được lấp đầy bằng các giá trị lấy từ `A2` và một ô hiển thị **Active**.

## Kết luận

Bạn giờ đã biết **how to expand array** trong Excel bằng hàm `EXPAND`, cách **populate excel template** với Smart Markers, và cách xây dựng một **dynamic range excel** tự động thích nghi với dữ liệu nguồn. Ví dụ cũng minh họa cách đúng để **use expand function** và **expand array formula** trong một kịch bản tự động hoá C# thực tế.

Tiếp theo, hãy cân nhắc mở rộng giải pháp:

* Thay thế kích thước cố định `5,5` bằng `ROWS(A2:A10), COLUMNS(A2:E2)` để có phạm vi thực sự biến đổi.
* Kết hợp nhiều Smart Markers để tạo báo cáo đầy đủ (ví dụ: danh sách nhân viên, bảng doanh thu).
* Khám phá API styling của Aspose.Cells để định dạng khối đã mở rộng tự động.

Bạn có thể thoải mái thử nghiệm với các mảng nguồn khác nhau, tên marker và bố cục workbook. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Xuất dữ liệu ra Excel: Điền mẫu từ một mảng trong C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [Cách tạo mảng trong Excel với C# – Hướng dẫn từng bước](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Xử lý dữ liệu bằng hàm mảng trong Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}