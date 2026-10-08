---
category: general
date: 2026-06-21
description: Nhập JSON vào Excel nhanh chóng và tìm hiểu cách chuyển đổi JSON sang
  XLSX, tạo Excel từ JSON, và xuất JSON ra bảng tính trong vài bước đơn giản.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: vi
og_description: Nhập JSON vào Excel một cách dễ dàng. Hướng dẫn này chỉ cho bạn cách
  chuyển đổi JSON sang XLSX, tạo Excel từ JSON và xuất JSON ra bảng tính bằng C#.
og_title: Nhập JSON vào Excel với Aspose.Cells – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Nhập JSON vào Excel với Aspose.Cells – Hướng dẫn lập trình toàn diện
url: /vi/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhập JSON vào Excel – Hướng Dẫn Lập Trình Đầy Đủ

Bạn đã bao giờ tự hỏi **cách nhập JSON vào Excel** mà không cần viết trình phân tích tùy chỉnh chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần chuyển một payload JSON thành một bảng tính gọn gàng để báo cáo hoặc phân tích dữ liệu. Tin tốt là gì? Với Aspose.Cells, bạn có thể **chuyển đổi JSON sang XLSX** chỉ trong vài dòng code, và toàn bộ quá trình đều nhanh và an toàn về kiểu dữ liệu.

Trong tutorial này, chúng tôi sẽ hướng dẫn từng bước cần thiết để **tạo Excel từ JSON**, lưu kết quả dưới dạng tệp `.xlsx`, và thậm chí khám phá một vài biến thể hữu ích—như xuất JSON ra bảng tính tự động cập nhật khi bạn thay đổi dữ liệu nguồn. Khi hoàn thành, bạn sẽ có một đoạn mã có thể tái sử dụng trong bất kỳ dự án .NET nào.

## Yêu cầu trước

- .NET 6.0 hoặc mới hơn (code cũng hoạt động trên .NET Framework)
- Giấy phép Aspose.Cells for .NET hợp lệ hoặc khóa đánh giá tạm thời
- Visual Studio 2022 (hoặc bất kỳ IDE C# nào bạn thích)
- Kiến thức cơ bản về cấu trúc JSON và cú pháp C#

Không cần thêm bất kỳ gói NuGet nào ngoài **Aspose.Cells**, giúp việc thiết lập nhẹ nhàng.

## Bước 1: Cài đặt Aspose.Cells và Thiết lập Dự án

Đầu tiên, thêm thư viện Aspose.Cells vào dự án của bạn. Mở Package Manager Console và chạy:

```powershell
Install-Package Aspose.Cells
```

Nếu bạn đang sử dụng .NET CLI, lệnh tương đương là:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Sau khi cài đặt, thêm tệp giấy phép (`Aspose.Cells.lic`) vào thư mục gốc của dự án và tải nó khi khởi động:

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Bây giờ bạn đã sẵn sàng để bắt đầu **nhập JSON vào Excel**.

## Bước 2: Chuẩn bị Payload JSON

Để minh họa, chúng ta sẽ sử dụng một mảng đơn giản các đối tượng người. Trong thực tế, bạn có thể đọc chuỗi này từ tệp, phản hồi API, hoặc cơ sở dữ liệu.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

Lưu ý cách JSON là một mảng phẳng—đúng là dạng dữ liệu phù hợp nhất với smart markers của Aspose.Cells.

## Bước 3: Cấu hình tùy chọn tải JSON

Aspose.Cells cho phép bạn xử lý toàn bộ mảng JSON như một *nguồn dữ liệu duy nhất*. Điều này rất quan trọng khi bạn muốn các hàng tự động mở rộng trong worksheet.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

Cài đặt `ArrayAsSingle = true` báo cho thư viện **tạo một smart marker lặp lại cho mỗi phần tử** trong mảng, đây là trọng tâm của quy trình **chuyển đổi JSON sang XLSX**.

## Bước 4: Tạo Workbook và Nhập JSON

Bây giờ chúng ta tạo một instance `Workbook` mới và nhập JSON bằng smart marker có tên `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

Ở phía sau, Aspose.Cells sẽ phân tích JSON, ánh xạ mỗi thuộc tính (`Name`, `Age`) vào một cột, và chuẩn bị một placeholder sẽ được mở rộng thành các hàng sau này.

## Bước 5: Đặt Smart Marker vào Worksheet

Một smart marker trông giống `{{People}}`. Khi workbook được lưu, Aspose.Cells sẽ thay thế marker này bằng một bảng chứa toàn bộ dữ liệu từ mảng JSON.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

Bạn có thể di chuyển marker tới bất kỳ vị trí nào—góc trên‑trái thường được chọn vì nó cho phép bảng mở rộng xuống dưới và sang phải.

## Bước 6: Lưu Workbook dưới dạng tệp XLSX

Cuối cùng, ghi workbook ra đĩa. Đây là bước **lưu JSON dưới dạng Excel** và nhận được một tệp `.xlsx` thực sự mà bạn có thể mở trong Excel, Google Sheets, hoặc bất kỳ ứng dụng bảng tính nào khác.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Khi bạn mở `JsonSingleCell.xlsx`, bạn sẽ thấy một bảng như sau:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

Đó là kết quả **tạo Excel từ JSON** đang hoạt động.

## Ví dụ Hoạt Động Đầy Đủ

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### Kết quả Dự Kiến

Chạy chương trình sẽ in ra:

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

Mở tệp sẽ hiển thị một bảng hai hàng với tiêu đề **Name** và **Age**, hoàn toàn khớp với mảng JSON gốc.

## Các Biến Thể Nâng Cao

### 1. Nhập Nhiều Mảng JSON vào Các Sheet Khác Nhau

Nếu bạn có nhiều mảng—ví dụ `"Employees"` và `"Departments"`—bạn có thể nhập mỗi mảng vào một worksheet riêng:

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

Bây giờ bạn đã **xuất JSON ra bảng tính** với nhiều tab, mỗi tab phản ánh một bộ dữ liệu riêng biệt.

### 2. Định dạng Bảng Được Tạo

Bạn có thể áp dụng kiểu sau khi dữ liệu được mở rộng:

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

Cải tiến nhỏ này làm cho hàng tiêu đề nổi bật hơn, rất hữu ích cho các bảng điều khiển báo cáo.

### 3. Sử dụng Tệp JSON Thay vì Chuỗi

Nếu JSON của bạn nằm trên đĩa, chỉ cần đọc nó trước:

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

Các bước còn lại vẫn giữ nguyên, vì vậy bạn có thể **lưu JSON dưới dạng Excel** từ bất kỳ nguồn nào.

## Những Cạm Bẫy Thường Gặp & Cách Tránh

- **Missing `ArrayAsSingle`** – Quên cờ này sẽ khiến mỗi đối tượng được xử lý như một nguồn dữ liệu riêng, dẫn đến các ô trống. Luôn đặt cờ này khi JSON của bạn là một mảng cấp cao nhất.
- **Incorrect Smart Marker Name** – Marker (`{{People}}`) phải khớp với `DataSourceName` bạn đã truyền (`"People"`). Sai chính tả sẽ khiến placeholder không được thay thế.
- **License Not Loaded** – Ở chế độ đánh giá, tệp xuất ra sẽ có watermark. Tải giấy phép sớm để workbook sạch sẽ.
- **File Path Permissions** – Cố lưu vào thư mục được bảo vệ sẽ gây ngoại lệ. Sử dụng `Environment.CurrentDirectory` hoặc đường dẫn mà người dùng có quyền ghi.

## Kiểm Tra Kết Quả Theo Chương Trình

Nếu bạn muốn xác minh việc xuất thành công mà không mở Excel, có thể đọc lại ô đầu tiên:

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

Kiểm tra nhanh trên console như vậy xác nhận rằng **chuyển đổi JSON sang XLSX** đã hoạt động như mong đợi.

## Kết Luận

Chúng ta vừa bao quát mọi thứ bạn cần để **nhập JSON vào Excel** bằng Aspose.Cells: từ cài đặt thư viện, chuẩn bị JSON, cấu hình smart markers, đến cuối cùng là **lưu JSON dưới dạng Excel**. Dù bạn cần **chuyển đổi JSON sang XLSX**, **tạo Excel từ JSON**, hay **xuất JSON ra bảng tính** cho phân tích, mẫu này vẫn giống nhau—smart markers thực hiện phần việc nặng.

Hãy tự do thử nghiệm với định dạng, nhiều sheet, hoặc thậm chí cập nhật động bằng cách nhập lại JSON tại thời gian chạy. Bước tiếp theo hợp lý là tích hợp đoạn code này vào một Web API cung cấp báo cáo Excel theo yêu cầu—chỉ cần thay thế dòng lưu tệp bằng một stream trả về cho client.

Có câu hỏi về các trường hợp đặc biệt, như JSON lồng nhau hoặc bộ dữ liệu lớn? Hãy để lại bình luận bên dưới, và chúc bạn coding vui!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Nhập JSON vào Excel một cách Hiệu Quả bằng Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Nhập Dữ Liệu JSON vào Excel bằng Aspose.Cells Java: Hướng Dẫn Toàn Diện](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Nhập JSON vào Excel một cách Dễ Dàng bằng Aspose.Cells cho .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}