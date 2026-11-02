---
category: general
date: 2026-09-15
description: Tạo workbook Excel trong C# và học cách lưu workbook dưới dạng PDF trong
  khi trải rộng các mảng động bằng hàm EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: vi
lastmod: 2026-09-15
og_description: Tạo sổ làm việc Excel trong C# và nhanh chóng lưu sổ làm việc dưới
  dạng PDF trong khi sử dụng hàm EXPAND để mở rộng một mảng động.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Tạo sổ làm việc Excel và lưu dưới dạng PDF với mảng động
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Tạo sổ làm việc Excel và lưu dưới dạng PDF với mảng động
url: /vi/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook Excel và lưu dưới dạng PDF với mảng động

Nếu bạn cần **tạo workbook Excel** bằng mã và sau đó **lưu workbook dưới dạng PDF**, hướng dẫn này sẽ chỉ cho bạn một giải pháp hoàn chỉnh, từ đầu đến cuối bằng C#. Bạn cũng sẽ thấy cách **tràn mảng động** bằng cách sử dụng **hàm EXPAND**, đây là cách hiện đại để tạo mảng mà không cần VBA.  

Dù bạn đang xây dựng dịch vụ báo cáo, tính năng xuất dữ liệu cho hệ thống ERP, hay bảng điều khiển dựa trên dữ liệu, các bước dưới đây sẽ giúp bạn tạo workbook, điền dữ liệu Smart Marker, và tạo PDF giữ nguyên các tính năng phông chữ nâng cao.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng chạy được với .NET Framework 4.8)
* Phiên bản mới của **Aspose.Cells for .NET** (v25.8 trở lên) – cung cấp `Workbook`, `PdfSaveOptions`, và `SmartMarkerProcessor`.
* Một IDE như Visual Studio 2022 (bất kỳ trình soạn thảo nào có thể biên dịch C# đều được).

Thêm gói NuGet vào dự án của bạn:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Step 1: Create Excel workbook and set up the first worksheet

Nhiệm vụ đầu tiên là **tạo workbook Excel** và lấy tham chiếu tới worksheet mặc định. Worksheet này sẽ chứa mảng động và mẫu Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Why this matters*: Khi khởi tạo `Workbook` hệ thống workbook nội bộ được cấp phát, trong khi truy cập `Worksheets[0]` bạn sẽ có một sheet sẵn sàng sử dụng mà không cần phải tạo thủ công.

## Step 2: Spill dynamic array using the EXPAND function

**Hàm EXPAND** của Excel có thể biến một mảng tĩnh thành một vùng tràn (spill range) có kích thước bất kỳ. Ở đây chúng ta yêu cầu Excel mở rộng `{1,2,3}` thành một vùng 5 hàng × 1 cột bắt đầu tại `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Why this matters*: Sử dụng `EXPAND` giúp tránh các vòng lặp thủ công trong C#. Engine tính toán vùng tràn và lưu giá trị trực tiếp vào worksheet, sau này sẽ xuất hiện trong PDF.

## Step 3: Save workbook as PDF while preserving font variation selectors

Khi bạn cần **lưu workbook dưới dạng PDF**, bạn cũng có thể bật các tính năng kiểu chữ nâng cao như font variation selectors (có từ Aspose.Cells v25.8). Điều này đảm bảo PDF hiển thị đúng các script phức tạp.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Why this matters*: Đặt `FontVariationSelectors` thành `true` là cần thiết cho các ngôn ngữ dựa vào biến thể glyph (ví dụ: tiếng Trung, tiếng Nhật, emoji). PDF được tạo sẽ phản ánh chính xác giao diện Excel trên màn hình.

## Step 4: Insert a Smart Marker template that references a nested data source

Smart Marker cho phép bạn nhúng các placeholder trực tiếp vào worksheet. Mẫu dưới đây sẽ tạo danh sách đơn hàng và các mặt hàng của chúng.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Why this matters*: Khi đặt mẫu ở `A1`, bạn thông báo cho Aspose.Cells vị trí bắt đầu mở rộng dữ liệu. Cú pháp `:` (`Items:ItemName`) chỉ cho bộ xử lý lặp qua một collection lồng nhau.

## Step 5: Define the nested data source (orders containing items)

Chúng ta tạo một mảng ẩn danh các đơn hàng, mỗi đơn hàng chứa một collection các đối tượng mặt hàng. Điều này mô phỏng một kịch bản master‑detail điển hình.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Why this matters*: Cấu trúc lồng nhau này minh họa **cách tạo mảng động trong Excel** thông qua Smart Markers, mà không cần viết VBA hay vòng lặp ô thủ công.

## Step 6: Process the Smart Markers and save the final Excel file

Bây giờ chúng ta truyền workbook và nguồn dữ liệu cho `SmartMarkerProcessor`. Sau khi xử lý, các placeholder sẽ được thay thế bằng các hàng thực tế, và chúng ta lưu kết quả dưới dạng file `.xlsx` thông thường.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Why this matters*: `SmartMarkerProcessor` tự động mở rộng mẫu, tạo các hàng cần thiết và điền dữ liệu. Workbook cuối cùng có thể mở trong Excel để kiểm tra rằng mỗi đơn hàng và các mặt hàng của nó đã xuất hiện đúng.

## Expected output

* **VarSelector.pdf** – file PDF hiển thị các số 1‑3 tràn xuống năm hàng, được render với bất kỳ biến thể OpenType nào bạn đã bật.
* **NestedSmartMarker.xlsx** – file Excel có các dòng sau (bắt đầu tại `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

Phiên bản PDF giữ nguyên cùng một dải số tràn vì trạng thái worksheet đã được lưu trước khi xử lý Smart Marker; bạn có thể lặp lại việc lưu PDF sau khi xử lý nếu muốn dữ liệu cuối cùng cũng ở dạng PDF.

## Pro tips and common pitfalls

| Tip | Explanation |
|-----|-------------|
| **Reuse the same `PdfSaveOptions`** | Tạo đối tượng options một lần và tái sử dụng giúp tránh các khác biệt tinh tế trong việc render (ví dụ: thiếu variation selectors). |
| **Call `ws.Calculate()` after setting formulas** | Nếu không gọi tính toán rõ ràng, vùng tràn có thể vẫn để trống khi bạn kiểm tra workbook bằng mã. |
| **Place Smart Marker templates on a clean sheet** | Trộn mẫu với dữ liệu hiện có có thể gây chèn hàng không mong muốn. Nên dùng một sheet riêng nếu có thể. |
| **Mind the file paths** | Dùng `Path.Combine(Environment.CurrentDirectory, "output.pdf")` để tránh các thư mục được mã hóa cứng trên các máy khác nhau. |
| **Version check** | `FontVariationSelectors` chỉ có từ phiên bản 25.8; các phiên bản cũ hơn sẽ bỏ qua thuộc tính này mà không ném lỗi. |

## Next steps

Bây giờ bạn đã biết cách **tạo workbook Excel**, **tràn mảng động**, và **lưu workbook dưới dạng PDF**, bạn có thể khám phá:

* Thêm biểu đồ hoặc hình ảnh trước khi chuyển đổi sang PDF.
* Xuất cùng một workbook sang các định dạng khác (ví dụ: HTML, CSV) bằng các overload của `Save`.
* Sử dụng **biểu thức Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) để tính toán tổng hợp ngay tại chỗ.
* Tích hợp đoạn mã này vào một ASP.NET Core API để người dùng có thể tải PDF đã tạo trực tiếp từ endpoint web.

---

**Summary** – Bài hướng dẫn này đã chỉ cho bạn cách **tạo workbook Excel**, sử dụng **hàm EXPAND** để **tràn mảng động**, nhúng **Smart Marker** làm việc với nguồn dữ liệu lồng nhau, và cuối cùng **lưu workbook dưới dạng PDF** đồng thời giữ nguyên các tính năng phông chữ nâng cao. Ví dụ hoàn chỉnh, có thể chạy được có thể sao chép vào bất kỳ dự án C# nào và điều chỉnh cho cấu trúc dữ liệu của riêng bạn. Chúc lập trình vui!

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}