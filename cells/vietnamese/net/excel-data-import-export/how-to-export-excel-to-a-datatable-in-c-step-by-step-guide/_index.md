---
category: general
date: 2026-03-18
description: Cách xuất dữ liệu Excel sang DataTable trong C# với mã xử lý các ô cụ
  thể, chuyển đổi Excel sang DataTable và định dạng số. Tìm hiểu cách xuất các ô cụ
  thể và nhiều hơn nữa.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: vi
og_description: Cách xuất dữ liệu Excel sang DataTable trong C#. Hướng dẫn này chỉ
  ra cách xuất các ô cụ thể, chuyển đổi Excel sang DataTable và định dạng số một cách
  dễ dàng.
og_title: Cách xuất Excel sang DataTable trong C# – Hướng dẫn đầy đủ
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Cách xuất Excel sang DataTable trong C# – Hướng dẫn từng bước
url: /vi/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất Excel sang DataTable trong C# – Hướng dẫn từng bước

Bạn đã bao giờ tự hỏi **cách xuất Excel** dữ liệu vào một `DataTable` mà không mất định dạng chưa? Bạn không phải là người duy nhất—các nhà phát triển thường xuyên cần lấy một phần của bảng tính vào bộ nhớ để báo cáo, kiểm tra, hoặc thực hiện các thao tác chèn hàng loạt. Tin tốt là gì? Chỉ với vài dòng C# bạn có thể xuất một phạm vi chính xác (ví dụ *A1:F11*), buộc mọi ô được xử lý như chuỗi, và thậm chí áp dụng định dạng số tùy chỉnh.

Trong tutorial này, chúng ta sẽ bao quát mọi thứ bạn cần biết: từ việc tải workbook, cấu hình **export specific cells**, chuyển đổi phạm vi thành `DataTable`, và xử lý các trường hợp đặc biệt như hàng trống hoặc số phụ thuộc vào ngôn ngữ. Khi kết thúc, bạn sẽ có một phương thức tái sử dụng cho các kịch bản **excel to datatable c#** trong mã sản xuất.

> **Prerequisites** – Bạn sẽ cần thư viện Aspose.Cells for .NET (hoặc bất kỳ API tương tự nào cung cấp `ExportDataTable`). Ví dụ giả định .NET 6+, nhưng các khái niệm cũng áp dụng cho các phiên bản trước.

---

## Bạn sẽ học được gì

- Cách **convert Excel to DataTable** bằng Aspose.Cells.  
- Xuất một phạm vi tùy chỉnh (`excel range to datatable`) trong khi xử lý tất cả giá trị dưới dạng chuỗi.  
- Áp dụng định dạng số hai chữ số thập phân (`#,#00.00`) trong quá trình xuất.  
- Các lỗi thường gặp (hàng null, cột ẩn) và cách tránh chúng.  
- Một mẫu mã sẵn sàng sao chép, chạy được hoàn chỉnh.

---

## Prerequisites and Setup

Trước khi chúng ta đi vào mã, hãy chắc chắn rằng bạn đã có:

1. **Aspose.Cells for .NET** được cài đặt qua NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Một file Excel (`input.xlsx`) được đặt trong thư mục bạn có thể tham chiếu, ví dụ `YOUR_DIRECTORY/input.xlsx`.  
3. Một dự án nhắm tới .NET 6 hoặc mới hơn (các câu lệnh `using` dưới đây sẽ hoạt động ngay).

> **Pro tip:** Nếu bạn đang dùng thư viện khác (ví dụ EPPlus hoặc ClosedXML), khái niệm vẫn giống nhau—tải workbook, chọn phạm vi, và gọi phương thức trả về một `DataTable`.

---

## Bước 1: Load the Workbook and Grab the First Worksheet

Điều đầu tiên bạn cần là một đối tượng `Workbook` đại diện cho file Excel của bạn. Khi đã có, bạn có thể truy cập bất kỳ worksheet nào bằng chỉ số hoặc tên.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Tại sao lại quan trọng:** Việc tải workbook sớm cho phép bạn kiểm tra cấu trúc (sheet ẩn, bảo vệ) trước khi quyết định xuất những ô nào. Nếu file lớn, hãy cân nhắc dùng `LoadOptions` để chỉ stream những phần cần thiết.

---

## Bước 2: Configure Export Options – Treat All Values as Strings

Khi xuất dữ liệu để xử lý tiếp (ví dụ chèn hàng loạt vào SQL), bạn thường muốn **đại diện chuỗi nhất quán**. Điều này tránh lỗi không khớp kiểu sau này.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Giải thích:**  
- `ExportAsString = true` yêu cầu Aspose.Cells bỏ qua kiểu dữ liệu gốc của ô và trả về văn bản đã định dạng.  
- `NumberFormat = "#,##0.00"` đảm bảo các số như `1234.5` trở thành `"1,234.50"`—rất hữu ích cho báo cáo tài chính.

Nếu bạn cần giữ nguyên kiểu dữ liệu gốc, chỉ cần đặt `ExportAsString` thành `false` và tự xử lý việc chuyển đổi.

---

## Bước 3: Export a Specific Range (A1:F11) to a DataTable

Bây giờ là phần cốt lõi của **export specific cells**. Phương thức `ExportDataTable` nhận chỉ số hàng/cột bắt đầu và kết thúc (đánh số từ 0) cùng một cờ cho việc bao gồm tiêu đề.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Kết quả bạn nhận được:** Một `DataTable` với 11 hàng (bao gồm tiêu đề) và 6 cột (`A`‑`F`). Tất cả giá trị đều là chuỗi được định dạng theo `exportOptions`.

---

## Bước 4: Verify the Result – Print to Console

Luôn luôn kiểm tra kết quả trước khi chuyển `DataTable` cho thành phần khác.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Bạn sẽ thấy một đầu ra giống như:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Lưu ý các cột số hiển thị hai chữ số thập phân, đúng như chúng ta đã chỉ định.

---

## Full Working Example (Copy‑Paste Ready)

Dưới đây là chương trình hoàn chỉnh liên kết mọi phần lại với nhau. Đặt nó vào một dự án console mới, chỉnh đường dẫn file, và chạy—không cần cấu hình thêm.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Những điểm chính từ mã:**  

- Đối tượng `ExportTableOptions` có thể tái sử dụng; bạn có thể truyền nó vào nhiều lời gọi `ExportDataTable` nếu cần xuất nhiều phạm vi.  
- Chỉ số bắt đầu từ **0**, vì vậy `A1` tương ứng với `(0,0)`.  
- Đặt `includeColumnNames` thành `true` sẽ tự động dùng hàng đầu làm tiêu đề cột—rất tiện cho các thao tác `DataTable` tiếp theo.

---

## Handling Edge Cases & Common Questions

### Worksheet có hàng hoặc cột ẩn thì sao?

Aspose.Cells mặc định tôn trọng tính hiển thị. Nếu bạn muốn xuất dữ liệu ẩn, đặt `exportOptions.ExportHiddenRows = true` và `ExportHiddenColumns = true`.

### File Excel của tôi chứa công thức—tôi có nhận được giá trị đã tính không?

Có. Mặc định `ExportDataTable` trả về **giá trị hiển thị** (kết quả của công thức). Nếu bạn muốn lấy nguyên văn công thức, đặt `exportOptions.ExportFormulas = true`.

### Làm sao để bỏ qua các hàng hoàn toàn trống?

Sau khi xuất, bạn có thể loại bỏ các hàng rỗng trong `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Có thể xuất một phạm vi không liên tiếp (ví dụ A1:B5 và D1:E5) không?

Aspose.Cells không hỗ trợ các phạm vi rời rạc trong một lời gọi duy nhất. Thay vào đó, hãy xuất từng khối riêng biệt rồi gộp các `DataTable` lại thủ công.

---

## Performance Tips

- **Reuse `ExportTableOptions`** cho nhiều lần xuất; tạo một instance mới mỗi lần sẽ tạo ra chi phí không đáng kể nhưng làm code rối.  
- **Stream các file lớn** bằng `LoadOptions` để tránh tải toàn bộ workbook vào bộ nhớ.  
- **Tránh dùng `DataTable`** nếu bạn chỉ cần xuất nhanh sang CSV—`ExportDataTable` tiện lợi nhưng không phải là cách tiết kiệm bộ nhớ nhất cho các sheet rất lớn.

---

## Conclusion

Chúng ta đã đi qua **cách xuất Excel** dữ liệu vào một `DataTable` đồng thời kiểm soát định dạng, xử lý các phạm vi ô cụ thể, và đảm bảo mọi giá trị đều được trả về dưới dạng chuỗi. Ví dụ đầy đủ minh họa một cách tiếp cận sạch sẽ, sẵn sàng cho môi trường sản xuất mà bạn có thể điều chỉnh cho **convert excel to datatable**, **export specific cells**, hoặc bất kỳ **excel range to datatable** nào bạn gặp.

Hãy thử nghiệm: thay đổi phạm vi, bật/tắt `ExportAsString`, hoặc truyền `DataTable` thẳng vào Entity Framework để chèn hàng loạt. Khi đã có nền tảng vững chắc này, khả năng của bạn sẽ mở rộng vô hạn.

---

### Next Steps & Related Topics

- **Importing DataTable back into Excel** – học cách thực hiện ngược lại với `ImportDataTable`.  
- **Bulk inserting a DataTable into SQL Server** – dùng `SqlBulkCopy` để tải nhanh dữ liệu.  
- **Working with EPPlus or ClosedXML** – xem cách thực hiện cùng nhiệm vụ với các thư viện thay thế.  
- **Formatting cells on export** – khám phá thêm `ExportTableOptions` cho định dạng ngày, thiết lập văn hoá tùy chỉnh, và nhiều hơn nữa.

Có câu hỏi hoặc trường hợp sử dụng khác? Hãy để lại bình luận, và chúng ta sẽ tiếp tục trao đổi. Chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}