---
category: general
date: 2026-09-27
description: Học cách xóa các hàng trong bảng Excel bằng C# với hướng dẫn chi tiết
  từng bước, đồng thời biết cách tải nhanh workbook Excel trong C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: vi
lastmod: 2026-09-27
og_description: Xóa các hàng khỏi bảng Excel trong C# với một ví dụ rõ ràng. Hướng
  dẫn này cũng bao gồm cách tải workbook Excel bằng C# và xử lý các trường hợp ngoại
  lệ phổ biến.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Xóa các dòng trong bảng Excel bằng C# – hướng dẫn mã hoàn chỉnh
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Cách xóa các hàng trong bảng Excel bằng C#
url: /vi/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xóa các hàng khỏi bảng Excel trong C# – hướng dẫn lập trình đầy đủ

Nếu bạn cần **xóa các hàng khỏi bảng Excel** trong một tệp .xlsx, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng C#. Bạn sẽ thấy một ví dụ ngắn gọn, có thể chạy được, tải một workbook Excel, loại bỏ các hàng cụ thể khỏi bảng đầu tiên, và lưu kết quả. Cách tiếp cận này hoạt động với thư viện Aspose.Cells phổ biến và có thể được điều chỉnh cho các API Excel .NET khác.

Xóa các hàng khỏi một bảng là một nhiệm vụ phổ biến khi làm sạch dữ liệu nhập khẩu, cắt giảm các phần báo cáo, hoặc tự động cập nhật bảng tính. Khi kết thúc hướng dẫn này, bạn sẽ có thể **load Excel workbook C#**, xác định một bảng (ListObject), xóa bất kỳ hàng nào bạn muốn, và ghi lại tệp đã sửa đổi trở lại đĩa.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn đã được cài đặt (mã cũng hoạt động với .NET Framework 4.7+).
* Tham chiếu tới gói NuGet **Aspose.Cells** (hoặc bất kỳ thư viện tương thích nào cung cấp các kiểu `Workbook`, `Worksheet`, và `ListObject`).
* Một tệp đầu vào có tên `input.xlsx` được đặt trong thư mục bạn có thể tham chiếu từ dự án của mình.
* Kiến thức cơ bản về cú pháp C# và Visual Studio (hoặc IDE bạn ưa thích).

> **Mẹo:** Nếu bạn thích một giải pháp mã nguồn mở, cùng một logic có thể áp dụng với **ClosedXML** – chỉ cần thay thế các lớp đặc thù của Aspose bằng `XLWorkbook`, `IXLWorksheet`, và `IXLTable`.

## Bước 1: Tải workbook Excel trong C#

Hoạt động đầu tiên là đọc tệp nguồn vào bộ nhớ. Việc tải workbook là nhanh chóng đối với các kích thước bảng tính thông thường và cho phép bạn truy cập đầy đủ vào các worksheet, bảng và giá trị ô.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Tại sao điều này quan trọng:* `Workbook` phân tích cấu trúc Open XML của tệp .xlsx, cung cấp một tập hợp các đối tượng `Worksheet`. Nếu không tìm thấy tệp, Aspose sẽ ném ra `FileNotFoundException`, vì vậy hãy chắc chắn rằng đường dẫn là đúng.

## Bước 2: Truy cập worksheet mục tiêu

Hầu hết các bảng tính chứa nhiều sheet; bạn cần chọn sheet chứa bảng bạn muốn chỉnh sửa. Ở đây chúng ta sử dụng sheet đầu tiên (`Worksheets[0]`), đây là mặc định an toàn cho các tệp đơn giản.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Tại sao điều này quan trọng:* `Worksheet` là container cho các bảng (`ListObjects`). Truy cập đúng sheet ngăn ngừa việc thay đổi nhầm dữ liệu không liên quan.

## Bước 3: Xóa các hàng khỏi bảng Excel

Các bảng Excel được biểu diễn bằng các đối tượng `ListObject`. Bảng đầu tiên trên sheet là `ListObjects[0]`. Phương thức `DeleteRows(startIndex, rowCount)` loại bỏ các hàng **liên quan tới vùng dữ liệu của bảng**, không phải số hàng tuyệt đối của worksheet.  

Trong ví dụ này chúng ta xóa hàng thứ hai và thứ ba của bảng (header là hàng 0, vì vậy chúng ta bắt đầu từ chỉ số 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Nếu bảng có tên hoặc vị trí khác thì sao?

* **Bảng có tên:** Sử dụng `ws.ListObjects["MyTableName"]` thay vì chỉ mục.
* **Nhiều bảng:** Duyệt qua `ws.ListObjects` và chọn bảng phù hợp với một điều kiện (ví dụ, tên tiêu đề cột).
* **Số hàng động:** Bạn có thể tính `rowCount` tại thời gian chạy bằng cách kiểm tra `ws.ListObjects[0].DataRange.RowCount`.

### Xử lý các trường hợp biên

| Tình huống                              | Thay đổi mã đề xuất                                      |
|----------------------------------------|----------------------------------------------------------|
| Bảng trống hoặc có ít hàng hơn          | Kiểm tra `ws.ListObjects[0].DataRange.RowCount` trước khi xóa. |
| Số hàng cần xóa vượt quá kích thước bảng| Giới hạn `rowCount` thành `DataRange.RowCount - startIndex`. |
| Cần xóa hàng dựa trên một điều kiện (ví dụ, giá trị ở cột C) | Duyệt `DataRange.Rows` và thu thập các chỉ số khớp, sau đó xóa theo thứ tự ngược lại để giữ chỉ số ổn định. |

## Bước 4: Lưu workbook đã chỉnh sửa

Sau khi xóa, ghi workbook trở lại một tệp mới (hoặc ghi đè lên tệp gốc nếu bạn muốn). Việc lưu tạo ra một tệp .xlsx mới phản ánh bảng đã được cập nhật.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Tại sao điều này quan trọng:* `Save` tuần tự hoá đại diện trong bộ nhớ ra đĩa. Nếu bạn cần giữ nguyên tệp gốc, luôn ghi vào một đường dẫn khác.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các bước lại với nhau sẽ cho bạn một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Kết quả mong đợi** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Mở `output.xlsx` – bảng đầu tiên hiện không còn các hàng bạn đã xóa, trong khi hàng tiêu đề vẫn còn nguyên vẹn.

## Câu hỏi thường gặp và các biến thể

### Làm sao để xóa các hàng khỏi **tất cả** các bảng trong một workbook?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Tôi có thể xóa các hàng dựa trên **giá trị ô** không?

Có. Quét `DataRange` để tìm các ô khớp, thu thập chỉ số bắt đầu từ 0 của chúng, sau đó xóa theo thứ tự giảm dần:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Nếu tôi cần **giữ định dạng** thì sao?

`DeleteRows` loại bỏ toàn bộ hàng khỏi bảng nhưng vẫn giữ kiểu của bảng cho các hàng còn lại. Nếu bạn cần giữ định dạng cụ thể trên một hàng đang xóa, hãy sao chép kiểu sang một hàng khác trước khi xóa.

### Điều này có hoạt động với các tệp **.xls** (Excel 97‑2003) không?

Có. Aspose.Cells tự động phát hiện định dạng tệp, vì vậy cùng một mã hoạt động với `.xls`. Chỉ cần thay đổi phần mở rộng tệp trong hàm khởi tạo `Workbook`.

## Mẹo hiệu năng

* **Xóa hàng hàng loạt:** Xóa nhiều hàng từng cái một có thể chậm hơn. Sử dụng một lời gọi `DeleteRows(start, count)` duy nhất khi có thể.
* **Tránh chặn luồng UI:** Nếu bạn tích hợp vào ứng dụng desktop, chạy việc thao tác workbook trên một luồng nền để giữ UI phản hồi.
* **Giải phóng đúng cách:** Mặc dù Aspose.Cells sử dụng bộ nhớ quản lý, hãy bọc `Workbook` trong khối `using` nếu bạn làm việc với tệp lớn để giải phóng tài nguyên kịp thời.

## Kết luận

Bây giờ bạn đã có một ví dụ hoàn chỉnh, sẵn sàng cho môi trường production để **xóa các hàng khỏi bảng Excel** bằng C#. Hướng dẫn đã đề cập cách **load Excel workbook C#**, xác định `ListObject` mong muốn, an toàn loại bỏ các hàng, và lưu tệp đã cập nhật. Với các xử lý trường hợp biên và lời khuyên về hiệu năng được đưa vào, bạn có thể áp dụng mẫu này cho các kịch bản phức tạp hơn như xóa có điều kiện, nhiều bảng, hoặc các thư viện Excel .NET thay thế.

### Các bước tiếp theo

* Khám phá **ClosedXML** hoặc **EPPlus** nếu bạn muốn một stack hoàn toàn mã nguồn mở.
* Kết hợp việc xóa hàng với **validation dữ liệu** để làm sạch bảng tính trước khi nhập vào cơ sở dữ liệu.
* Tự động hoá quy trình cho một thư mục các workbook bằng cách sử dụng `Directory.GetFiles` và một vòng lặp.

Bạn có thể tự do thử nghiệm với các phạm vi hàng khác nhau, tên bảng và logic có điều kiện. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tải tệp Excel C# – Cách xóa hàng và loại bỏ các hàng cụ thể](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Cách chèn và xóa hàng trong Excel với Aspose.Cells cho .NET: Hướng dẫn toàn diện](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Cách xóa các hàng trống trong Excel bằng Aspose.Cells .NET để làm sạch dữ liệu](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}