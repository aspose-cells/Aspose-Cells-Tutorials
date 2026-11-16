---
category: general
date: 2026-11-16
description: Tạo Excel từ JSON bằng SmartMarker. Tìm hiểu cách chuyển đổi JSON sang
  Excel, nhúng JSON vào Excel và lưu workbook xlsx trong vài phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: vi
lastmod: 2026-11-16
og_description: Tạo file Excel từ JSON nhanh chóng. Hướng dẫn này chỉ cách chuyển
  đổi JSON sang Excel, nhúng JSON vào Excel và lưu workbook dưới dạng xlsx bằng Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Tạo Excel từ JSON bằng SmartMarker – hướng dẫn C# chi tiết
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Tạo Excel từ JSON bằng SmartMarker trong C#
url: /vi/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel từ JSON với SmartMarker trong C#

Nếu bạn cần **tạo Excel từ JSON** trong một dự án .NET, hướng dẫn này cung cấp một giải pháp hoàn chỉnh, có thể chạy được. Sử dụng bộ xử lý Smart Marker của Aspose.Cells, bạn có thể **chuyển đổi JSON sang Excel**, nhúng chuỗi JSON trực tiếp vào một ô, và **lưu workbook xlsx** mà không cần viết bất kỳ mã phân tích thủ công nào.

Bạn sẽ thấy cách đăng ký nguồn dữ liệu JSON, chèn một Smart Marker xuất toàn bộ mảng dưới dạng một chuỗi JSON duy nhất, xử lý worksheet, và cuối cùng ghi file ra đĩa. Khi kết thúc tutorial, bạn có thể tạo một file Excel chứa payload JSON gốc trong ô A1, sẵn sàng cho các quy trình xử lý hoặc báo cáo tiếp theo.

## Prerequisites

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
- Aspose.Cells for .NET (gói NuGet `Aspose.Cells`)
- Kiến thức cơ bản về C# và định dạng JSON
- Một IDE như Visual Studio hoặc VS Code

## Step 1: Set up the project and import namespaces

Tạo một ứng dụng console mới và thêm gói Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Sau đó, bao gồm các namespace cần thiết ở đầu file `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Why?**  
`Aspose.Cells` cung cấp mô hình workbook, trong khi `Aspose.Cells.SmartMarkers` chứa lớp `SmartMarkerProcessor` chịu trách nhiệm giải thích các marker `&=` trong worksheet.

## Step 2: Define the JSON data source

Đặt chuỗi JSON vào một biến. Trong ví dụ này chúng ta có một mảng các đơn hàng:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Why?**  
Smart Marker hoạt động với bất kỳ JSON hợp lệ nào. Giữ JSON dưới dạng chuỗi cho phép bạn đăng ký trực tiếp mà không cần một file trên đĩa.

## Step 3: Register the JSON data with SmartMarkerProcessor

Tạo một thể hiện `SmartMarkerProcessor` và liên kết chuỗi JSON với một tên mà bạn sẽ tham chiếu sau này trong worksheet:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Why?**  
`RegisterJsonDataSource` phân tích JSON và đưa cấu trúc phân cấp của nó vào Smart Markers. Tên `"OrdersJson"` trở thành đối tượng gốc trong các biểu thức marker.

## Step 4: Create a workbook and insert the Smart Marker

Khởi tạo một workbook mới, lấy worksheet đầu tiên, và viết một Smart Marker vào ô A1 để xuất toàn bộ mảng `Orders` dưới dạng một chuỗi JSON duy nhất:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Why?**  
Biểu thức `OrdersJson.Orders.ArrayAsSingle` chỉ cho Smart Marker lấy mảng `Orders` và tuần tự hoá lại thành JSON, đặt kết quả vào ô đích. Đây là cách đơn giản nhất để **nhúng JSON vào Excel**.

## Step 5: Process the worksheet

Chạy processor để nó thay thế marker bằng chuỗi JSON thực tế:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Why?**  
Quá trình xử lý sẽ kiểm tra mỗi ô có marker `&=` không, đánh giá chúng dựa trên các nguồn dữ liệu đã đăng ký, và ghi giá trị đã đánh giá trở lại worksheet.

## Step 6: Save the workbook as an .xlsx file

Cuối cùng, ghi workbook ra đĩa. Điều chỉnh đường dẫn tới thư mục mà bạn có quyền ghi:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Why?**  
`SaveFormat.Xlsx` đảm bảo file được lưu ở định dạng Office Open XML hiện đại, đáp ứng yêu cầu **save workbook xlsx**.

## Full source code

Kết hợp tất cả các phần lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Expected output in Excel

Mở `JsonArraySingleCell.xlsx`. Ô A1 sẽ chứa:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

Chuỗi JSON là một biểu diễn gọn gàng của mảng `Orders` gốc, giúp dễ dàng truyền tải hoặc tiêu thụ trong các quy trình làm việc dựa trên Excel.

## Common variations and edge cases

| Situation | Adjustment |
|-----------|------------|
| **Multiple JSON objects** | Đăng ký mỗi đối tượng với một tên riêng (ví dụ: `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) và tham chiếu chúng bằng các marker riêng biệt. |
| **Pretty‑printed JSON in a cell** | Sử dụng tùy chọn `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Large JSON payloads** | Xem xét ghi JSON vào một sheet ẩn hoặc sử dụng chuyển đổi `DataTable` để cải thiện hiệu năng. |
| **Embedding JSON in multiple cells** | Đặt các marker khác nhau vào các ô khác, ví dụ: `&=OrdersJson.Orders[0].Id` để lấy các trường riêng lẻ. |

**Pro tip:** Khi làm việc với JSON rất lớn, tăng bộ nhớ đệm của workbook (`WorkbookSettings.MemorySetting`) để tránh `OutOfMemoryException`.

## Testing the solution

1. Xây dựng và chạy ứng dụng console (`dotnet run`).  
2. Xác nhận console in ra đường dẫn đầy đủ tới file đã tạo.  
3. Mở file trong Excel hoặc bất kỳ trình xem bảng tính nào.  
4. Kiểm tra ô A1 chứa chuỗi JSON mảng đúng như trên.

Nếu ô chứa văn bản marker (`&=OrdersJson...`) thay vì JSON, hãy kiểm tra lại rằng processor đã được gọi **sau** khi marker được đặt và chuỗi JSON là hợp lệ.

## Conclusion

Bạn đã biết cách **tạo Excel từ JSON** bằng Smart Markers của Aspose.Cells, cách **chuyển đổi JSON sang Excel**, nhúng payload JSON trực tiếp vào một ô, và **lưu workbook xlsx** chỉ với một dòng lệnh. Cách tiếp cận này loại bỏ việc phân tích thủ công, hoạt động với bất kỳ cấu trúc JSON nào, và tạo ra một file Excel sạch, tuân thủ tiêu chuẩn.

### Next steps

- Khám phá **vòng lặp Smart Marker** (`&=OrdersJson.Orders`) để tạo một hàng cho mỗi đơn hàng thay vì một chuỗi JSON duy nhất.  
- Kết hợp kỹ thuật này với **công thức Excel** để tính tổng từ dữ liệu nhúng.  
- Tìm hiểu cách **đọc JSON lại từ Excel** bằng `Workbook.Load` và `SmartMarkerProcessor` theo hướng ngược lại.

Hãy tự do thử nghiệm với các dạng JSON khác nhau, nhiều worksheet, hoặc xuất ra các định dạng khác như CSV hoặc PDF. Chúc lập trình vui vẻ!

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}