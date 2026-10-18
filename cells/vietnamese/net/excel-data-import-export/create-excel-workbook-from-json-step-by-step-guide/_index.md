---
category: general
date: 2026-03-25
description: Tạo workbook Excel từ JSON và lưu workbook dưới dạng xlsx. Học cách xuất
  JSON sang xlsx, tạo Excel từ JSON và điền dữ liệu vào Excel từ JSON trong vài phút.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: vi
og_description: Tạo sổ làm việc Excel từ JSON ngay lập tức. Hướng dẫn này chỉ cách
  xuất JSON sang XLSX, tạo Excel từ JSON và điền dữ liệu vào Excel từ JSON bằng Aspose.Cells.
og_title: Tạo Workbook Excel từ JSON – Hướng dẫn C# toàn diện
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Tạo Sổ làm việc Excel từ JSON – Hướng dẫn từng bước
url: /vi/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel từ JSON – Hướng Dẫn C# Đầy Đủ

Bạn đã bao giờ cần **tạo excel workbook** từ một payload JSON nhưng không biết bắt đầu từ đâu chưa? Bạn không đơn độc; nhiều nhà phát triển gặp khó khăn khi họ cố gắng chuyển dữ liệu API thành một bảng tính gọn gàng. Tin tốt? Chỉ với vài dòng C# và Aspose.Cells, bạn có thể **export json to xlsx**, **generate excel from json**, và **populate excel from json** mà không cần dùng các bộ chuyển đổi bên thứ ba.

Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình — bắt đầu từ một chuỗi JSON thô, đưa nó vào SmartMarker, và cuối cùng **save workbook as xlsx** trên đĩa. Khi kết thúc, bạn sẽ có một tệp Excel sẵn sàng sử dụng trông như sau:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Nếu bạn đã sử dụng Aspose.Cells ở nơi khác trong dự án, bạn có thể tái sử dụng cùng một thể hiện `Workbook` cho nhiều lần nhập JSON — rất hữu ích cho xử lý hàng loạt.

## Những gì bạn cần

- **.NET 6+** (hoặc bất kỳ .NET Framework gần đây nào hỗ trợ C# 10)
- **Aspose.Cells for .NET** – cài đặt qua NuGet: `dotnet add package Aspose.Cells`
- Kiến thức cơ bản về cú pháp C# (không cần hiểu sâu về Excel)

Đó là tất cả. Không có dịch vụ bên ngoài, không có COM interop, chỉ là mã quản lý thuần túy.

## Bước 1: Khởi tạo một Workbook Excel mới

Điều đầu tiên chúng ta làm là tạo một đối tượng workbook mới. Hãy nghĩ nó như việc mở một tệp Excel trống, nơi chúng ta sẽ đưa dữ liệu vào sau.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Tại sao bắt đầu với một workbook mới? Nó đảm bảo một khởi đầu sạch sẽ, ngăn ngừa các kiểu còn lại từ các lần chạy trước, và giữ kích thước tệp tối thiểu — hoàn hảo cho các pipeline tự động.

## Bước 2: Chuẩn bị dữ liệu JSON bạn muốn nhập

Để minh họa, chúng ta sẽ sử dụng một mảng JSON nhỏ, nhưng bạn có thể thay thế bằng bất kỳ JSON hợp lệ nào nhận được từ dịch vụ web, tệp, hoặc truy vấn cơ sở dữ liệu.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Lưu ý dấu ngoặc kép được escape đôi (`\"`) — đó chỉ là cú pháp chuỗi literal trong C#. Trong thực tế, bạn có thể đọc chuỗi này từ một tệp:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## Bước 3: Yêu cầu SmartMarker xử lý toàn bộ mảng như một bản ghi duy nhất

Engine SmartMarker của Aspose.Cells có thể lặp qua các collection một cách tự động. Bằng cách bật **ArrayAsSingle**, chúng ta xử lý toàn bộ mảng JSON như một bản ghi duy nhất, đúng như những gì chúng ta cần cho một bảng phẳng.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Nếu bạn quên bật cờ này, SmartMarker sẽ cố tạo một sheet riêng cho mỗi phần tử — chắc chắn không phải điều bạn muốn khi tạo một bảng đơn giản.

## Bước 4: Đặt token SmartMarker vào Worksheet

Token SmartMarker trông như `${jsonArray}`. Khi bộ xử lý chạy, nó sẽ thay thế token bằng dữ liệu từ nguồn JSON. Chúng ta sẽ đặt token vào ô **A1** để đầu ra bắt đầu ở góc trên‑trái.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Bạn cũng có thể định dạng trước hàng tiêu đề trước khi xử lý. Ví dụ, đặt phông chữ đậm cho hàng đầu tiên:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## Bước 5: Chạy bộ xử lý SmartMarker

Bây giờ phép màu xảy ra. Bộ xử lý đọc JSON, ánh xạ mỗi thuộc tính vào một cột, và ghi các hàng dưới token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Behind the scenes, Aspose.Cells:

1. Phân tích JSON thành đối tượng .NET.
2. Ghép tên thuộc tính (`Name`, `Score`) với tiêu đề cột.
3. Ghi mỗi phần tử mảng thành một hàng mới.

Nếu JSON của bạn chứa các đối tượng lồng nhau, bạn có thể tham chiếu chúng bằng ký hiệu chấm (`${parent.child}`) — một tính năng hữu ích cho các báo cáo phức tạp hơn.

## Bước 6: Lưu Workbook dưới dạng tệp XLSX

Cuối cùng, lưu workbook vào đĩa. Phần mở rộng tệp `.xlsx` cho Excel (và hầu hết các ứng dụng bảng tính khác) biết đây là một workbook OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Bạn cũng có thể truyền workbook trực tiếp tới phản hồi HTTP nếu bạn đang xây dựng một web API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## Ví dụ Hoạt động Đầy Đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy, bao gồm mọi bước ở trên. Sao chép‑dán vào một dự án console mới và nhấn **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Kết quả mong đợi:** Mở `json-single.xlsx` sẽ hiển thị hai hàng dưới tiêu đề đậm — `John` với điểm `90` và `Anna` với `85`. Tên cột được suy ra tự động từ tên thuộc tính JSON.

## Câu hỏi Thường gặp & Trường hợp Cạnh

### Nếu các khóa JSON của tôi chứa dấu cách hoặc ký tự đặc biệt thì sao?

SmartMarker yêu cầu tên định danh hợp lệ. Thay dấu cách bằng dấu gạch dưới hoặc sử dụng ánh xạ tùy chỉnh:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Làm sao để xuất một mảng JSON lớn (hàng ngàn dòng)?

The processor streams data internally, so memory usage stays modest. However, you might want to:

- Tăng giới hạn `MaxRows` của worksheet (`worksheet.Cells.MaxRow = 1_048_576;` – giới hạn tối đa của Excel).
- Tắt lưới để tăng hiệu năng (`worksheet.IsGridlinesVisible = false;`).

### Tôi có thể thêm nhiều bảng JSON vào cùng một workbook không?

Chắc chắn. Chỉ cần đặt các token SmartMarker khác nhau vào các vùng riêng biệt (ví dụ, `${orders}` ở `A10`, `${customers}` ở `D1`) và gọi `Process` một lần cho mỗi token hoặc một lần với một đối tượng JSON tổng hợp chứa cả hai mảng.

## Bonus: Thêm Biểu Đồ Đơn Giản (Tùy chọn)

Nếu bạn muốn trực quan hoá các điểm, thêm một biểu đồ cột nhanh sau khi dữ liệu đã được điền:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

Biểu đồ sẽ tự động tham chiếu các hàng mới thêm, cung cấp cho bạn một báo cáo hoàn chỉnh trong một lần.

## Kết luận

Bây giờ bạn đã biết **cách tạo excel workbook** từ một chuỗi JSON, **export json to xlsx**, **generate excel from json**, và **populate excel from json** bằng tính năng SmartMarker của Aspose.Cells. Giải pháp hoàn chỉnh — khởi tạo workbook, cấu hình SmartMarker, xử lý JSON, và lưu tệp — chỉ cần vài dòng code, nhưng vẫn mở rộng được cho các bộ dữ liệu khổng lồ.

Bước tiếp theo? Hãy thử thay thế JSON tĩnh bằng một cuộc gọi API, thêm định dạng có điều kiện dựa trên điểm, hoặc tạo nhiều sheet cho các miền dữ liệu khác nhau. Mẫu tương tự cũng hoạt động cho CSV, XML, hoặc thậm chí các tập kết quả từ cơ sở dữ liệu — chỉ cần thay đổi chuỗi nguồn và điều chỉnh token SmartMarker.

Chúc lập trình vui vẻ, và hy vọng các bảng tính của bạn luôn gọn gàng!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}