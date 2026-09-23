---
category: general
date: 2026-03-21
description: Cách xuất dữ liệu Excel kèm tên cột, giữ nguyên định dạng số và đọc các
  hàng cụ thể bằng Aspose.Cells trong C#. Học cách đọc bảng tính Excel và xuất các
  hàng cụ thể một cách hiệu quả.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: vi
og_description: Cách xuất dữ liệu Excel kèm tên cột, giữ định dạng số và đọc các hàng
  cụ thể bằng Aspose.Cells. Một ví dụ đầy đủ, có thể chạy được cho các nhà phát triển
  C#.
og_title: Cách xuất dữ liệu Excel trong C# – Hướng dẫn lập trình toàn diện
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Cách xuất dữ liệu Excel trong C# – Hướng dẫn từng bước
url: /vi/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Xuất Dữ Liệu Excel trong C# – Hướng Dẫn Lập Trình Toàn Diện

Bạn đã bao giờ tự hỏi **cách xuất excel** dữ liệu mà không mất định dạng gốc chưa? Có thể bạn đã thử sao chép‑dán nhanh và kết quả là ngày tháng hiển thị dưới dạng “44728” hoặc thiếu tiêu đề cột. Thật là bực bội, đúng không? Trong tutorial này, bạn sẽ thấy một cách tiếp cận sạch sẽ, từ đầu tới cuối để đọc một worksheet Excel, bảo tồn định dạng số, xuất kèm tên cột, và thậm chí chỉ lấy những hàng bạn cần.

Chúng ta sẽ sử dụng thư viện Aspose.Cells vì nó cho phép kiểm soát chi tiết các tùy chọn xuất. Khi kết thúc hướng dẫn, bạn sẽ có một đoạn mã có thể tái sử dụng, có thể chèn vào bất kỳ dự án .NET nào, và bạn sẽ hiểu tại sao mỗi tùy chọn lại quan trọng. Không cần tài liệu bên ngoài—mọi thứ bạn cần đều có ở đây.

---

## Những Điều Bạn Sẽ Học

- **Read Excel worksheet** vào bộ nhớ với Aspose.Cells.  
- **Export specific rows** (ví dụ: hàng 0‑49) trong khi giữ lại tên cột.  
- **Preserve number format** để tiền tệ, ngày tháng và phần trăm vẫn giữ nguyên.  
- Cách **export with column names** và bao gồm bình luận ô nếu cần.  
- Một ví dụ C# hoàn chỉnh, sẵn sàng chạy, cùng các mẹo cho những lỗi thường gặp.

### Yêu Cầu Trước

- .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+).  
- Aspose.Cells for .NET được cài đặt qua NuGet (`Install-Package Aspose.Cells`).  
- Một file Excel (`input.xlsx`) được đặt trong thư mục bạn có thể tham chiếu.

> **Pro tip:** Nếu bạn đang chạy trên pipeline CI, hãy cân nhắc kéo gói NuGet từ feed riêng để tránh bất ngờ về giấy phép.

---

## Bước 1 – Cài Đặt Aspose.Cells và Thêm Namespaces

Đầu tiên, hãy chắc chắn rằng gói Aspose.Cells đã có trong dự án của bạn. Mở Package Manager Console và chạy:

```powershell
Install-Package Aspose.Cells
```

Sau đó thêm các `using` cần thiết ở đầu file C# của bạn:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Các import này cho phép bạn truy cập `Workbook`, `Worksheet`, `ExportTableOptions`, và `DataTable`—những thành phần cốt lõi để **đọc worksheet Excel** và xuất dữ liệu.

---

## Bước 2 – Tải Workbook (Đọc File Excel)

Bây giờ chúng ta thực sự **đọc worksheet Excel**. Hàm khởi tạo `Workbook` nhận đường dẫn tới file, và Aspose.Cells sẽ xử lý cả định dạng `.xlsx` và `.xls` cũ.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Tại sao điều này quan trọng:** Tải workbook một lần và tái sử dụng cùng một đối tượng `Worksheet` hiệu quả hơn rất nhiều so với việc mở file liên tục, đặc biệt với các bảng tính lớn.

---

## Bước 3 – Cấu Hình Các Tùy Chọn Xuất (Bảo Tồn Định Dạng Số & Tên Cột)

Ở đây chúng ta chỉ định cho Aspose.Cells *cách* xuất. Lớp `ExportTableOptions` cho phép tinh chỉnh đầu ra. Chúng ta sẽ bật ba cờ:

1. `ExportAsString = true` – buộc mọi ô trở thành chuỗi, đảm bảo các số giữ nguyên dạng hiển thị.  
2. `IncludeCellComments = true` – sao chép bất kỳ bình luận nào gắn vào ô (hữu ích cho tài liệu).  
3. `PreserveNumberFormat = true` – giữ lại định dạng số gốc (ký hiệu tiền tệ, mẫu ngày, v.v.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Trường hợp đặc biệt:** Nếu bạn đặt `ExportAsString` thành `false` nhưng vẫn muốn giữ định dạng số, bạn có thể nhận được giá trị số thô (ví dụ, 44728 cho một ngày). Giữ cả ba cờ bật sẽ tránh được bất ngờ này.

---

## Bước 4 – Lấy Worksheet Đầu Tiên (Đọc Worksheet Excel)

Hầu hết các file đơn giản có dữ liệu cần thiết ở sheet đầu tiên, vì vậy chúng ta sẽ lấy nó theo chỉ số. Nếu bạn cần sheet khác, chỉ cần thay `0` bằng chỉ số zero‑based thích hợp hoặc dùng `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Lý do hữu ích:** Truy cập trực tiếp đối tượng worksheet cho phép bạn kiểm soát toàn bộ collection `Cells`, điều này thiết yếu để **xuất các hàng cụ thể** sau này.

---

## Bước 5 – Xuất Một Phạm Vi Ô (Xuất Các Hàng Cụ Thể)

Bây giờ là phần cốt lõi của tutorial: xuất các hàng 0‑49 và cột 0‑4 (tức là 50 hàng đầu và 5 cột đầu) vào một `DataTable`. Chúng ta cũng sẽ yêu cầu Aspose.Cells bao gồm tên cột làm hàng đầu tiên của `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Điều Gì Được Thực Hiện

- **`startRow: 0`** – bắt đầu từ đầu trang tính.  
- **`totalRows: 50`** – lấy 50 hàng đầu (tức là **xuất các hàng cụ thể**).  
- **`totalColumns: 5`** – giới hạn xuất chỉ trong 5 cột đầu.  
- **`includeColumnNames: true`** – đảm bảo tiêu đề cột của `DataTable` khớp với hàng tiêu đề trong Excel, đáp ứng yêu cầu **xuất kèm tên cột**.  
- **`exportOptions`** – áp dụng các cài đặt từ Bước 3, vì vậy các giá trị số của bạn vẫn hiển thị như “$1,234.56” thay vì “1234.56”.

---

## Bước 6 – Kiểm Tra Kết Quả Xuất (Kết Quả Trông Như Thế Nào)

Hãy in một vài hàng đầu ra console để bạn có thể thấy định dạng vẫn được bảo tồn.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Kết quả mong đợi (ví dụ):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Chú ý cách các ngày xuất hiện ở định dạng `MM/dd/yyyy` và tiền tệ vẫn giữ ký hiệu `$`—nhờ **bảo tồn định dạng số**.

---

## Các Vấn Đề Thường Gặp & Cách Khắc Phục

| Vấn đề | Nguyên nhân | Cách khắc phục |
|--------|-------------|----------------|
| Ngày chuyển thành số lớn | `ExportAsString` để `false` | Giữ `ExportAsString = true` hoặc chuyển đổi ô thủ công |
| Thiếu tiêu đề cột | `includeColumnNames` đặt `false` | Đặt nó thành `true` khi cần **xuất kèm tên cột** |
| Bình luận biến mất | `IncludeCellComments` không được bật | Bật `IncludeCellComments` trong `ExportTableOptions` |
| Xuất sheet sai | Dùng `Worksheets[0]` trên file đa sheet | Chỉ định tên sheet: `workbook.Worksheets["Data"]` |
| Ngoại lệ vượt phạm vi | `totalRows` lớn hơn số hàng thực tế | Dùng `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Xuất Toàn Bộ Sheet Trong Khi Vẫn Bảo Tồn Định Dạng

Nếu sau này bạn muốn xuất toàn bộ sheet, chỉ cần thay `totalRows` và `totalColumns` bằng kích thước tối đa của sheet:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Bây giờ bạn có một quy trình **đọc worksheet Excel** hoạt động cho bất kỳ kích thước nào, đồng thời vẫn **bảo tồn định dạng số** và **xuất kèm tên cột**.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là chương trình đầy đủ mà bạn có thể đặt vào một ứng dụng console. Nó bao gồm tất cả các bước, import, và một đoạn in kiểm tra đơn giản.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Lưu file này dưới tên `Program.cs`, chạy `dotnet run`, và bạn sẽ thấy bản xem trước đã được định dạng trong terminal.

---

## Kết Luận

Chúng ta vừa đi qua **cách xuất excel** dữ liệu bằng Aspose.Cells, bao gồm mọi thứ từ tải workbook, bảo tồn định dạng số, xuất kèm tên cột, và giới hạn xuất chỉ các hàng cần thiết. Mã nguồn độc lập, có thể chạy ngay, và bao gồm các biện pháp bảo vệ thực tế cho những trường hợp lỗi phổ biến nhất.

Sẵn sàng cho thử thách tiếp theo? Hãy thử xuất trực tiếp sang CSV vẫn giữ định dạng số gốc, hoặc đưa `DataTable` vào ngữ cảnh Entity Framework Core để chèn hàng loạt vào cơ sở dữ liệu. Cả hai kịch bản đều dựa trên những nền tảng chúng ta đã học ở đây.

If you found this guide helpful

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}