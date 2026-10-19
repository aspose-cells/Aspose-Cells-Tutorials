---
category: general
date: 2026-05-04
description: Xuất phạm vi bảng tính bằng C# với định dạng tùy chỉnh. Tìm hiểu cách
  xuất phạm vi Excel và cách tùy chỉnh việc xuất ô trong vài bước đơn giản.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: vi
og_description: Xuất phạm vi bảng tính bằng C#. Hướng dẫn này cho thấy cách xuất phạm
  vi Excel và tùy chỉnh việc xuất ô một cách nhanh chóng và đáng tin cậy.
og_title: Xuất phạm vi bảng tính trong C# – Hướng dẫn lập trình toàn diện
tags:
- C#
- Excel
- Data Export
title: Xuất phạm vi worksheet trong C# – Hướng dẫn lập trình chi tiết
url: /vi/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất phạm vi worksheet trong C# – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **xuất phạm vi worksheet** nhưng kết quả mặc định không phải là những gì bạn muốn? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn khi cố gắng lấy một khối ô vào tệp CSV hoặc JSON. Tin tốt là gì? Chỉ với vài dòng C# bạn không chỉ **xuất phạm vi excel** mà còn **tùy chỉnh việc xuất ô** để phù hợp với bất kỳ định dạng nào phía sau.

Trong hướng dẫn này, chúng ta sẽ đi qua một kịch bản thực tế: lấy các ô *A1:D10* từ một workbook Excel, chuyển mỗi giá trị thành một chuỗi có dấu ngoặc, và ghi kết quả vào tệp. Khi hoàn thành, bạn sẽ biết chính xác **cách xuất phạm vi worksheet** với kiểm soát toàn diện đối với cách hiển thị của từng ô, cùng một vài mẹo cho các trường hợp biên bạn có thể gặp sau này.

## Những gì bạn cần

- .NET 6 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)  
- Gói NuGet **GemBox.Spreadsheet** (hoặc bất kỳ thư viện nào cung cấp `ExportTableOptions`; API được minh họa ở đây là của GemBox)  
- Kiến thức cơ bản về cú pháp C# – không cần gì phức tạp, chỉ cần các câu lệnh `using` và tạo đối tượng thông thường  

Nếu bạn đã có những thứ trên, bạn đã sẵn sàng để bắt đầu.

## Bước 1: Thiết lập tùy chọn xuất – Điểm kiểm soát chính  

Điều đầu tiên bạn làm là tạo một thể hiện `ExportTableOptions` và chỉ định nó xử lý mọi ô dưới dạng chuỗi. Đây là nền tảng cho **cách xuất phạm vi excel** trong khi giữ kiểu dữ liệu nhất quán.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Tại sao phải ép buộc xuất dưới dạng chuỗi?*  
Khi bạn tùy chỉnh từng ô sau này, bạn sẽ chèn dấu ngoặc và có thể các ký hiệu khác. Giữ mọi thứ dưới dạng chuỗi sẽ ngăn ngừa những bất ngờ khi chuyển đổi kiểu (ví dụ, ngày tháng biến thành số serial).

## Bước 2: Gắn vào sự kiện CellExport – Tùy chỉnh từng ô  

Bây giờ là phần thú vị: **cách tùy chỉnh việc xuất ô**. GemBox kích hoạt sự kiện `CellExport` cho mỗi ô sắp được ghi. Bằng cách xử lý sự kiện này, bạn có thể bao bọc giá trị trong dấu ngoặc, thêm tiền tố, hoặc thậm chí bỏ qua một ô hoàn toàn.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Mẹo chuyên nghiệp:* Nếu bạn chỉ muốn sửa đổi các ô số, hãy kiểm tra `e.Value.GetType()` trước khi áp dụng dấu ngoặc. Điều kiểm tra nhỏ này có thể giúp bạn tránh việc vô tình làm hỏng văn bản tiêu đề.

## Bước 3: Xuất phạm vi mong muốn – Hành động cốt lõi  

Với các tùy chọn đã sẵn sàng, bạn gọi `ExportTable`. Phương thức này nhận workbook bạn đã tải, địa chỉ của phạm vi bạn muốn, và các tùy chọn bạn vừa cấu hình.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Phiên bản overload chúng ta dùng ghi trực tiếp vào tệp (mặc định là CSV). Nếu bạn muốn một chuỗi trong bộ nhớ, hãy thay đối số cuối cùng bằng một `StringWriter` và đọc kết quả sau đó.

### Ví dụ hoàn chỉnh hoạt động

Dưới đây là một ứng dụng console tự chứa mà bạn có thể dán vào một dự án mới và chạy ngay (chỉ cần thay đổi đường dẫn tệp).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Kết quả mong đợi (đoạn CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Mỗi ô từ *A1* đến *D10* giờ đã được bao bọc trong dấu ngoặc vuông, chính xác như chúng ta đã định nghĩa trong trình xử lý `CellExport`.

## Xử lý các trường hợp biên thường gặp  

### 1. Ô trống  
Nếu một ô trống, `e.Value` sẽ là `null`. Cố gắng định dạng nó bằng string interpolation sẽ gây ra ngoại lệ. Hãy bảo vệ bằng cách:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Phạm vi lớn  
Xuất hàng triệu dòng có thể vượt quá giới hạn bộ nhớ. Trong trường hợp này, hãy stream đầu ra thay vì tải toàn bộ workbook vào bộ nhớ:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Dấu phân cách khác nhau  
CSV không phải là định dạng duy nhất bạn có thể cần. Thay đổi dấu phân cách bằng cách điều chỉnh `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Câu hỏi thường gặp  

**H: Điều này có hoạt động với các tệp .xlsx được tạo bởi Excel 365 không?**  
Đúng vậy. GemBox đọc định dạng OpenXML hiện đại mà không cần cấu hình bổ sung.

**H: Tôi có thể xuất nhiều phạm vi không liên tiếp cùng một lúc không?**  
Không trực tiếp bằng một lời gọi `ExportTable` duy nhất. Hãy lặp qua từng chuỗi phạm vi (`"A1:D10"`, `"F1:H5"` …) và tự mình nối các kết quả lại.

**H: Nếu tôi cần áp dụng định dạng khác nhau cho từng cột thì sao?**  
Trong trình xử lý `CellExport` bạn có quyền truy cập `e.ColumnIndex`. Sử dụng câu lệnh `switch` để áp dụng logic riêng cho mỗi cột.

## Kết luận  

Chúng ta đã khám phá **cách xuất phạm vi worksheet** với kiểm soát toàn diện đối với cách hiển thị của từng ô, trình bày **cách xuất phạm vi excel** bằng `ExportTableOptions`, và chỉ ra **cách tùy chỉnh việc xuất ô** qua sự kiện `CellExport`. Giải pháp hoàn chỉnh chỉ mất vài chục dòng C#, nhưng đủ linh hoạt cho các kịch bản sản xuất.

Bước tiếp theo? Thử thay đổi vòng bao dấu ngoặc thành định dạng thân thiện JSON, hoặc thử nghiệm logic điều kiện để bỏ qua các hàng ẩn. Bạn cũng có thể khám phá việc xuất trực tiếp tới một `MemoryStream` cho các phản hồi API web—không cần tệp tạm thời.

Nếu bạn đã theo dõi đến đây, bạn đã có một mẫu mẫu vững chắc để xuất bất kỳ phạm vi worksheet nào đúng cách bạn cần. Chúc lập trình vui vẻ, và đừng ngại để lại bình luận nếu gặp khó khăn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}