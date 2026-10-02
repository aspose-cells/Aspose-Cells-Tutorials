---
category: general
date: 2026-02-28
description: Xóa các hàng trong bảng Excel bằng C# nhanh chóng. Tìm hiểu cách thêm
  phạm vi có tên trong Excel, truy cập worksheet theo tên và tránh lỗi trùng tên.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: vi
og_description: Xóa các hàng trong bảng Excel bằng C#. Hướng dẫn này cũng chỉ cách
  thêm phạm vi có tên trong Excel và truy cập worksheet theo tên.
og_title: Xóa các hàng trong bảng Excel bằng C# – Hướng dẫn đầy đủ
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Xóa các hàng trong bảng Excel bằng C# – Hướng dẫn từng bước
url: /vi/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xóa Các Hàng Trong Bảng Excel bằng C# – Hướng Dẫn Lập Trình Toàn Diện

Bạn đã bao giờ cần **delete rows excel table** từ một workbook nhưng không chắc nên gọi API nào không? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp khó khăn tương tự khi lần đầu cố gắng giảm kích thước một bảng bằng cách lập trình.  

Trong hướng dẫn này chúng ta sẽ đi qua một ví dụ đầy đủ, có thể chạy được, không chỉ xóa các hàng khỏi một bảng Excel, mà còn cho thấy **how to add defined name** (hay còn gọi là *named range*), cách **access worksheet by name**, và lý do tại sao việc thêm một tên trùng lặp trên một sheet khác sẽ ném ra `InvalidOperationException`.  

Khi đọc xong bài viết, bạn sẽ có thể:

* Lấy một worksheet bằng tên tab của nó.  
* An toàn xóa các hàng dữ liệu khỏi bảng đầu tiên trên sheet đó.  
* Tạo một named range trỏ tới một địa chỉ cụ thể.  
* Hiểu các rủi ro khi có tên trùng lặp giữa các sheet.

Không cần tài liệu bên ngoài—mọi thứ bạn cần đều có ở đây.

---

## Những Điều Cần Chuẩn Bị

* **DevExpress Spreadsheet** (hoặc bất kỳ thư viện nào cung cấp các đối tượng `Workbook`, `Worksheet`, `ListObject` và `Names`).  
* Một dự án .NET nhắm tới **.NET 6** hoặc mới hơn (mã cũng biên dịch được với .NET Framework 4.8).  
* Kiến thức cơ bản về C#—nếu bạn có thể viết một vòng lặp `foreach`, bạn đã sẵn sàng.

> **Pro tip:** Nếu bạn đang dùng phiên bản Community Edition miễn phí của DevExpress, các API được sử dụng dưới đây hoàn toàn giống với phiên bản thương mại.

---

## Bước 1 – Truy Cập Worksheet Theo Tên

Điều đầu tiên bạn cần làm là xác định sheet chứa bảng bạn muốn chỉnh sửa.  
Nhiều nhà phát triển thường dùng `Worksheets[0]` vì thói quen, nhưng cách này khiến mã của bạn phụ thuộc vào thứ tự sheet và sẽ bị lỗi ngay khi ai đó đổi tên tab.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Why this matters:* Bằng cách sử dụng **name** của sheet thay vì chỉ số, bạn tránh được việc vô tình chỉnh sửa nhầm sheet khi workbook thay đổi.  

Nếu tên bạn cung cấp không tồn tại, thư viện sẽ ném ra `KeyNotFoundException`, bạn có thể bắt lỗi này để hiển thị thông báo thân thiện.

---

## Bước 2 – Xóa Các Hàng Trong Bảng Excel (Cách An Toàn)

Bây giờ bạn đã có worksheet đúng, hãy loại bỏ các hàng dữ liệu khỏi bảng đầu tiên.  
Một lỗi thường gặp là gọi `DeleteRows(1, rowCount‑1)`. Từ **DevExpress 22.2** overload này đã **bị cấm** và sẽ ném `InvalidOperationException`. Thư viện yêu cầu bạn xóa các hàng **trong phạm vi dữ liệu của bảng**, không phải hàng tiêu đề.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **What if the table is empty?** Điều kiện `if` ngăn việc gọi hàm khi `rowCount = 0`, tránh gây ra ngoại lệ.

### Tổng Quan Trực Quan  

![delete rows excel table example](image.png "Screenshot showing rows being removed from an Excel table")  

*Alt text: ví dụ xóa các hàng trong bảng Excel bằng mã C#*

---

## Bước 3 – Cách Thêm Defined Name (Tạo Named Range)

Sau khi dọn dẹp bảng, bạn có thể muốn tham chiếu tới một phạm vi cụ thể sau này—ví dụ cho biểu đồ hoặc danh sách kiểm tra dữ liệu. Đó là lúc **add named range excel** xuất hiện.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Phương thức `Names.Add` nhận hai tham số: định danh và địa chỉ theo kiểu A1.  
Vì chúng ta đã **access worksheet by name** ở bước trước, chuỗi địa chỉ có thể an toàn tham chiếu bất kỳ sheet nào mà không lo thay đổi chỉ số.

---

## Bước 4 – Named Range Trên Sheet Khác – Tránh Lỗi Tên Trùng Lặp

Bạn có thể nghĩ rằng có thể tái sử dụng cùng một định danh trên một sheet khác, như sau:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Thật không may, phạm vi đặt tên của Excel là **toàn workbook**, không phải riêng từng sheet. Lệnh trên sẽ gây ra `InvalidOperationException` với thông báo *“A name with the same identifier already exists.”*  

### Cách Khắc Phục

1. **Pick a unique name** (`MyTable_Sheet2`).  
2. **Delete the existing name** before re‑adding it (only if you truly want to replace it).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Ví Dụ Đầy Đủ, Có Thể Chạy

Kết hợp tất cả lại, dưới đây là một ứng dụng console tự chứa mà bạn có thể thả vào Visual Studio và chạy với file mẫu `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Kết quả mong đợi**

* Tất cả các hàng dữ liệu từ bảng đầu tiên trên **Sheet1** biến mất, chỉ còn lại hàng tiêu đề.  
* Tên **MyTable** giờ trỏ tới `Sheet1!$A$1:$C$5`.  
* Tên thứ hai **MyTable_Sheet2** an toàn tham chiếu một phạm vi trên **Sheet2** mà không ném ngoại lệ.

---

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | Grab the correct `ListObject` by index (`worksheet.ListObjects[1]`) or by name (`worksheet.ListObjects["MyTable"]`). |
| *Can I delete rows from a table that spans multiple worksheets?* | No—tables are confined to a single sheet. You must repeat the delete logic for each sheet. |
| *Is there a way to delete only a subset of rows?* | Yes—use `table.DeleteRows(startRow, count)` where `startRow` is zero‑based within the table’s data area. |
| *Do named ranges survive after saving?* | Absolutely. Once you call `SaveDocument`, the names become part of the workbook’s XML. |
| *How do I list all defined names in the workbook?* | Iterate `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Kết Luận

Chúng ta đã đề cập tới **delete rows excel table** bằng C#, trình bày **add named range excel**, và chỉ ra cách đúng để **access worksheet by name** đồng thời tránh được lỗi `InvalidOperationException` do tên trùng lặp.  

Giải pháp hoàn chỉnh nằm trong đoạn mã ở trên—sao chép, dán và chạy nó trên các file của bạn. Từ đây bạn có thể mở rộng logic để xử lý nhiều bảng, tính toán phạm vi động, hoặc thậm chí tích hợp vào giao diện người dùng.

**Next steps** bạn có thể khám phá:

* Sử dụng **named range on another sheet** để điều khiển series cho biểu đồ.  
* Kết hợp logic xóa với **ExcelDataReader** để nhập dữ liệu trước khi làm sạch.  
* Tự động cập nhật hàng loạt trên hàng chục workbook bằng một vòng lặp đơn giản `foreach (var file in Directory.GetFiles(...))`.

Có thêm câu hỏi nào về tự động hoá Excel trong C#? Hãy để lại bình luận, và chúng ta sẽ tiếp tục thảo luận. Chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}