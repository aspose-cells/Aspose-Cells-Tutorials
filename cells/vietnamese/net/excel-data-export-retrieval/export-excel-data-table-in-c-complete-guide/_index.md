---
category: general
date: 2026-03-21
description: Xuất bảng dữ liệu Excel sang DataTable có tiêu đề, giới hạn số chữ số
  thập phân và xuất 100 dòng đầu tiên bằng Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: vi
og_description: Tìm hiểu cách xuất bảng dữ liệu Excel sang DataTable, giữ lại tiêu
  đề, giới hạn số chữ số thập phân và lấy 100 dòng đầu tiên trong C#.
og_title: Xuất Bảng Dữ liệu Excel trong C# – Hướng dẫn từng bước
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Xuất bảng dữ liệu Excel trong C# – Hướng dẫn toàn diện
url: /vi/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xuất Bảng Dữ Liệu Excel – Hướng Dẫn C# Đầy Đủ

Cần **xuất bảng dữ liệu excel** từ một workbook thành `DataTable` .NET? Bạn đã đến đúng nơi—hướng dẫn này sẽ chỉ cho bạn cách thực hiện, giữ lại tiêu đề cột, giới hạn số chữ số thập phân, và chỉ lấy 100 hàng đầu tiên.  

Nếu bạn từng nhìn vào một bảng tính và tự hỏi, “Làm sao đưa nó vào ứng dụng mà không mất định dạng?” bạn không đơn độc. Trong vài phút tới, chúng ta sẽ biến “nếu‑thế” đó thành một giải pháp sao chép‑dán cụ thể, hoạt động với Aspose.Cells, một thư viện phổ biến để thao tác Excel.

## Những Điều Bạn Sẽ Học

- Cách **export excel to datatable** bằng phương thức `ExportDataTable`.  
- Cách giữ lại tên cột gốc (`export excel with headers`).  
- Cách **limit decimal places excel** giá trị bằng cách cấu hình `ExportTableOptions`.  
- Cách an toàn chỉ lấy 100 hàng đầu tiên (`export first 100 rows`).  

Không có script bên ngoài, không có chuỗi ma thuật—chỉ là C# thuần mà bạn có thể chèn vào bất kỳ dự án .NET nào.

## Yêu Cầu Trước

| Yêu cầu | Tại sao quan trọng |
|-------------|----------------|
| .NET 6 hoặc mới hơn (hoặc .NET Framework 4.7+) | Aspose.Cells hỗ trợ cả hai, nhưng runtime mới hơn cung cấp API sẵn sàng async. |
| Gói NuGet Aspose.Cells cho .NET | Cung cấp `Workbook`, `ExportTableOptions`, và helper `ExportDataTable`. |
| Một file Excel mẫu (ví dụ: `Numbers.xlsx`) | Nguồn dữ liệu bạn sẽ xuất. |
| Kiến thức cơ bản về C# | Bạn sẽ theo dõi các đoạn mã, nhưng không cần gì phức tạp. |

Nếu bất kỳ mục nào trên còn lạ, hãy lấy gói NuGet bằng `dotnet add package Aspose.Cells` và tạo một file Excel nhỏ với vài số—dữ liệu thử nghiệm của bạn.

![ví dụ xuất bảng dữ liệu excel](excel-data-table.png "Ảnh chụp màn hình một sheet Excel sẽ được xuất thành DataTable")

## Bước 1: Tải Workbook (export excel data table)

Điều đầu tiên bạn cần là một thể hiện `Workbook` trỏ tới file Excel của bạn. Hãy tưởng tượng nó như mở một cuốn sách trước khi đọc bất kỳ chương nào.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Tại sao điều này quan trọng:** Việc tải workbook cho phép bạn truy cập các worksheet, ô và kiểu dáng của nó. Nếu đường dẫn file sai, Aspose sẽ ném `FileNotFoundException`, vì vậy hãy kiểm tra lại vị trí.

## Bước 2: Cấu Hình Tùy Chọn Xuất – limit decimal places excel

Mặc định Aspose xuất mọi giá trị số với độ chính xác đầy đủ. Thông thường bạn chỉ cần một vài chữ số có ý nghĩa, đặc biệt khi đưa dữ liệu vào lưới UI hoặc API yêu cầu số đã được làm tròn.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần chiến lược làm tròn khác (ví dụ: luôn làm tròn lên), bạn có thể xử lý sau khi xuất `DataTable`. Cài đặt `SignificantDigits` là cách nhanh nhất để **limit decimal places excel** mà không cần viết vòng lặp bổ sung.

## Bước 3: Xuất Phạm Vi Mong Muốn (export first 100 rows)

Bây giờ chúng ta chỉ định cho Aspose khối ô nào muốn kéo vào `DataTable`. Trong tutorial này chúng ta lấy 100 hàng đầu tiên và 10 cột đầu tiên, nhưng bạn có thể điều chỉnh các số này cho phù hợp với trường hợp của mình.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Trường hợp đặc biệt:** Nếu sheet có ít hơn 100 hàng, Aspose sẽ chỉ xuất những gì có mà không ném lỗi. Tuy nhiên, bạn có thể muốn bảo vệ trước một phạm vi bất ngờ quá nhỏ:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Bước 4: Kiểm Tra Kết Quả – In Nhanh lên Console

Xem dữ liệu trong debugger là tốt, nhưng in vài hàng ra console xác nhận rằng **export excel to datatable** thực sự hoạt động và các chữ số thập phân đã được cắt bớt.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Kết Quả Dự Kiến

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Chú ý cách các cột số giờ chỉ hiển thị bốn chữ số có ý nghĩa, phù hợp với cài đặt `SignificantDigits = 4` mà chúng ta đã áp dụng trước đó.

## Bước 5: Gói Gọn Tất Cả – Ví Dụ Hoàn Chỉnh, Có Thể Chạy

Dưới đây là chương trình đầy đủ bạn có thể sao chép‑dán vào một console app. Nó bao gồm xử lý lỗi, guard tùy chọn cho số hàng, và phương thức trợ giúp để in.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Chạy chương trình, và bạn sẽ thấy 100 hàng đầu tiên của sheet, đã được làm tròn gọn gàng, với tên cột vẫn nguyên vẹn.

## Câu Hỏi Thường Gặp & Những Lưu Ý

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu sheet của tôi có các ô hợp nhất thì sao?** | `ExportDataTable` sẽ làm phẳng các ô hợp nhất bằng cách lấy giá trị của ô trên‑trái. Nếu bạn cần xử lý tùy chỉnh, hãy hủy hợp nhất trước hoặc đọc các đối tượng `Cell` thô. |
| **Tôi có thể xuất sang `DataSet` thay vì không?** | Có—sử dụng `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}