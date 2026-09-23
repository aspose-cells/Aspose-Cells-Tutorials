---
category: general
date: 2026-03-22
description: Cách xuất Excel với định dạng và giữ nguyên định dạng số. Tìm hiểu cách
  chuyển đổi phạm vi Excel, lấy kết quả công thức và xuất Excel với định dạng bằng
  Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: vi
og_description: Cách xuất Excel với định dạng và giữ nguyên định dạng số. Hướng dẫn
  chi tiết từng bước để chuyển đổi vùng Excel, lấy kết quả công thức và xuất Excel
  với định dạng trong C#.
og_title: Cách xuất Excel có định dạng – Bảo tồn định dạng số
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cách xuất Excel có định dạng – Giữ nguyên định dạng số
url: /vi/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất Excel với định dạng – Bảo toàn định dạng số

Bạn đã bao giờ tự hỏi **cách xuất Excel** dữ liệu trong khi giữ nguyên giao diện của từng ô như bạn thấy trong workbook chưa? Có thể bạn cần gửi báo cáo cho khách hàng, cung cấp dữ liệu cho một điều khiển lưới, hoặc chỉ đơn giản lưu các giá trị vào cơ sở dữ liệu. Vấn đề thường gặp là mất định dạng số hoặc công thức biến thành chuỗi thô.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ C# hoàn chỉnh, sẵn sàng chạy, **bảo toàn định dạng số**, **chuyển đổi một phạm vi Excel** thành `DataTable`, **lấy kết quả công thức**, và cuối cùng **xuất Excel với định dạng** bằng Aspose.Cells. Khi kết thúc, bạn sẽ có một phương thức duy nhất có thể chèn vào bất kỳ dự án nào và gọi với một tham chiếu worksheet.

> **Xem nhanh:** mã tạo một workbook, ghi một giá trị và một công thức, yêu cầu Aspose.Cells xuất các ô dưới dạng chuỗi đã định dạng, và in ra `123.456 | 246.912` – chính xác những gì bạn mong đợi khi xem trong Excel.

---

## Những gì bạn cần

- **Aspose.Cells for .NET** (bản dùng thử miễn phí vẫn đủ cho việc học)
- .NET 6.0 trở lên (API giống nhau trên .NET Framework)
- Môi trường phát triển C# cơ bản (Visual Studio, VS Code, Rider… tùy bạn)

Không cần bất kỳ gói NuGet nào khác ngoài Aspose.Cells. Nếu bạn chưa cài đặt, chạy:

```bash
dotnet add package Aspose.Cells
```

---

## Bước 1 – Tạo Workbook và Ghi Giá trị (bao gồm công thức)

Đầu tiên chúng ta tạo một workbook mới và đặt một giá trị số vào **A1**. Sau đó thêm một công thức đơn giản trong **B1** nhân ô đầu tiên với hai. Điều này tạo nền tảng để minh họa **lấy kết quả công thức** sau này.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Tại sao điều này quan trọng:**  
- `PutValue` lưu số thô, trong khi `PutFormula` lưu công thức tính toán.  
- Aspose.Cells giữ công thức **sống**, vì vậy khi chúng ta sau này yêu cầu giá trị của ô, chúng ta sẽ thực sự nhận được `246.912`, không phải chuỗi `"=A1*2"`.

---

## Bước 2 – Yêu cầu Aspose.Cells xuất giá trị dưới dạng chuỗi đã định dạng

Nếu bạn chỉ gọi `ExportDataTable` với cài đặt mặc định, các ô số sẽ được trả về dưới dạng giá trị `double` gốc của chúng. Điều này sẽ loại bỏ mọi dấu phân cách hàng nghìn, ký hiệu tiền tệ, hoặc số chữ số thập phân tùy chỉnh mà bạn đã thiết lập. Lớp `ExportTableOptions` cho phép chúng ta **bảo toàn định dạng số** và **xuất dưới dạng chuỗi**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Điểm quan trọng:** `ExportNumberFormat = true` là cờ cho phép **bảo toàn định dạng số** hoạt động. Nếu không, bạn sẽ thấy `"123.456"` và `"246.912"` dưới dạng số thô, có thể trông ổn trong code nhưng không khi dán dữ liệu vào UI mong đợi cùng định dạng như Excel.

---

## Bước 3 – In dữ liệu đã xuất (Xác minh)

Bây giờ chúng ta có một `DataTable` đầy các chuỗi đã định dạng, hãy in nội dung ra console. Điều này cũng chứng minh rằng chúng ta đã **lấy kết quả công thức** thành công mà không cần tự mình tính toán công thức.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Chạy chương trình sẽ in:

```
123.456 | 246.912
```

Lưu ý cột thứ hai hiển thị **kết quả công thức**, không phải văn bản công thức. Đó chính là những gì bạn cần khi **xuất Excel với định dạng** cho quá trình xử lý tiếp theo.

---

## Bước 4 – Chuyển đổi phạm vi Excel lớn hơn (Tùy chọn)

Ví dụ trên chỉ xử lý một đoạn nhỏ `A1:B1`, nhưng trong thực tế thường cần xuất toàn bộ bảng. Phương thức này hoạt động cho bất kỳ khối hình chữ nhật nào – chỉ cần điều chỉnh các đối số `firstRow`, `firstColumn`, `totalRows`, và `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Mẹo chuyên nghiệp:** Nếu sheet của bạn đã có hàng tiêu đề, đặt `includeColumnNames` thành `true`. Aspose.Cells sẽ dùng hàng đầu tiên của phạm vi làm tên cột, rất hữu ích khi bạn sau này gắn `DataTable` vào lưới UI.

---

## Bước 5 – Những lỗi thường gặp & Cách tránh

| Vấn đề | Nguyên nhân | Cách khắc phục |
|-------|-------------|----------------|
| **Số mất dấu phẩy hoặc ký hiệu tiền tệ** | `ExportAsString` là `false` hoặc `ExportNumberFormat` bị bỏ qua | Đặt cả `ExportAsString = true` **và** `ExportNumberFormat = true`. |
| **Các ô công thức trả về văn bản công thức** | Bạn chưa gọi `CalculateFormula` trước khi xuất (chỉ cần nếu workbook không được đặt tự động tính toán) | Hoặc bật tự động tính toán (`workbook.CalculateFormula()`) hoặc dựa vào `ExportAsString` để buộc đánh giá. |
| **Tiêu đề xuất hiện như các dòng dữ liệu** | `includeColumnNames` được đặt là `false` trong khi phạm vi của bạn có hàng tiêu đề | Đặt `includeColumnNames = true` để coi hàng đầu tiên là tên cột. |
| **Phạm vi lớn gây áp lực bộ nhớ** | Xuất toàn bộ sheet một lần sẽ tải mọi thứ vào bộ nhớ | Xuất theo từng khối (ví dụ 500 dòng mỗi lần) và hợp nhất các `DataTable` nếu cần. |

---

## Bước 6 – Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

Dưới đây là toàn bộ chương trình, từ các câu lệnh `using` đến `Main`. Dán vào một ứng dụng console và nhấn **F5** – bạn sẽ ngay lập tức thấy đầu ra đã định dạng.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Kết quả mong đợi**

```
123.456 | 246.912

Press any key to exit...
```

Đó là toàn bộ quy trình **cách xuất excel**, với định dạng được giữ nguyên, kết quả công thức đã được tính, và một `DataTable` sạch sàng, sẵn sàng cho bất kỳ người tiêu dùng .NET nào.

---

## Kết luận

Chúng tôi đã đề cập mọi thứ bạn cần biết về **cách xuất dữ liệu Excel** trong khi **bảo toàn định dạng số**, **chuyển đổi một phạm vi Excel** thành `DataTable`, và **lấy kết quả công thức** mà không cần phân tích thêm. Điều quan trọng là cấu hình `ExportTableOptions` – một khi bạn đặt `ExportAsString` và `ExportNumberFormat` thành `true`, Aspose.Cells sẽ thực hiện phần công việc nặng cho bạn.

Từ đây bạn có thể:

- Gắn `DataTable` vào `DataGrid` WPF hoặc view ASP.NET MVC.
- Ghi bảng ra file CSV trong khi giữ nguyên biểu diễn trực quan.
- Mở rộng cách tiếp cận cho nhiều sheet hoặc phạm vi động.

Bạn có thể tự do thử nghiệm các định dạng khác nhau (tiền tệ, phần trăm) và các khối dữ liệu lớn hơn. Nếu gặp bất kỳ vấn đề nào, hãy quay lại bảng **những lỗi thường gặp** – nó bao gồm những trục trặc phổ biến nhất khi bạn **xuất excel với định dạng**.

Chúc lập trình vui vẻ, và hy vọng các bảng tính đã xuất luôn trông hoàn hảo như bản gốc!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}