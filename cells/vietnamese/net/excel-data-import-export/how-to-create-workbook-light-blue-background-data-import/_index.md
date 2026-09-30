---
category: general
date: 2026-02-09
description: Cách tạo workbook trong C# với nền màu xanh nhạt và nhập dữ liệu có tiêu
  đề. Tìm hiểu cách thêm nền màu xanh nhạt, sử dụng kiểu mặc định của Excel và nhập
  DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: vi
og_description: Cách tạo workbook trong C# với nền màu xanh nhạt, nhập dữ liệu có
  tiêu đề và áp dụng kiểu mặc định của Excel—tất cả trong một hướng dẫn ngắn gọn.
og_title: Cách tạo sổ làm việc – Nền xanh nhạt, Nhập dữ liệu
tags:
- C#
- Excel
- Aspose.Cells
title: Cách tạo Workbook – Nền xanh nhạt, Nhập dữ liệu
url: /vi/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo Workbook – Nền Xanh Nhạt, Nhập Dữ Liệu

Bạn đã bao giờ tự hỏi **how to create workbook** trong C# sao cho trông đẹp hơn một chút ngay từ đầu chưa? Có thể bạn đã lấy một `DataTable` từ cơ sở dữ liệu và đã chán ngấy những ô trắng mặc định. Trong hướng dẫn này, chúng ta sẽ đi qua việc tạo một workbook mới, thêm nền xanh nhạt cho một cột, và nhập dữ liệu kèm tiêu đề — tất cả đều sử dụng kiểu mặc định mà Excel cung cấp.

Chúng tôi cũng sẽ đưa vào một vài kịch bản “what‑if”, như xử lý giá trị null hoặc tùy chỉnh hơn một cột. Khi kết thúc, bạn sẽ có một tệp Excel đã được định dạng hoàn chỉnh mà bạn có thể gửi cho các bên liên quan mà không cần xử lý thêm.

## Yêu Cầu Trước

* **.NET 6+** (mã chạy trên .NET Framework 4.6+ cũng được)  
* **Aspose.Cells for .NET** – thư viện cung cấp các cuộc gọi `Workbook`, `Style`, và `ImportDataTable`. Cài đặt qua NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Một nguồn `DataTable` – chúng tôi sẽ tạo một mẫu trong ví dụ, nhưng bạn có thể thay thế bằng bất kỳ truy vấn ADO.NET nào.

Có đủ chưa? Tuyệt, hãy bắt đầu.

## Bước 1: Khởi Tạo Workbook Mới (Primary Keyword)

Điều đầu tiên bạn cần làm là **how to create workbook** – đúng nghĩa. Lớp `Workbook` đại diện cho toàn bộ tệp Excel, và hàm khởi tạo của nó cung cấp cho bạn một trang trắng.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Why this matters:** Bắt đầu với một `Workbook` mới đảm bảo bạn kiểm soát mọi kiểu ngay từ đầu. Nếu bạn mở một tệp hiện có, bạn sẽ kế thừa các kiểu mà người tạo ban đầu để lại, điều này có thể dẫn đến định dạng không nhất quán.

## Bước 2: Chuẩn Bị DataTable Sẽ Nhập

Để minh họa, chúng ta sẽ tạo một `DataTable` đơn giản. Trong các tình huống thực tế, bạn có thể sẽ gọi một stored procedure hoặc một phương thức ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tip:** Nếu bạn cần giữ nguyên thứ tự cột chính xác như trong cơ sở dữ liệu, hãy đặt tham số `importColumnNames` của `ImportDataTable` thành `true`. Điều này sẽ khiến Aspose.Cells tự viết tiêu đề cột cho bạn.

## Bước 3: Định Nghĩa Kiểu Cột – Mặc Định + Nền Xanh Nhạt

Bây giờ chúng ta trả lời phần **add light blue background** của câu đố. Aspose.Cells cho phép bạn truyền một mảng các đối tượng `Style` tương ứng với mỗi cột bạn nhập. Mục đầu tiên là kiểu cho cột 0, mục thứ hai cho cột 1, và cứ tiếp tục như vậy. Nếu bạn có ít kiểu hơn số cột, các cột còn lại sẽ sử dụng kiểu mặc định.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Why only two styles?** Trong ví dụ của chúng tôi có bốn cột, nhưng chúng tôi chỉ muốn cột thứ hai (Name) nổi bật. Độ dài mảng không cần phải khớp với số cột; bất kỳ mục nào thiếu sẽ tự động kế thừa kiểu mặc định của workbook.

## Bước 4: Nhập DataTable Kèm Tiêu Đề và Kiểu

Đây là nơi chúng ta kết hợp **excel import datatable c#** và **import data with headers**. Phương thức `ImportDataTable` thực hiện phần công việc nặng: nó ghi tên cột, các hàng, và áp dụng mảng kiểu mà chúng ta vừa tạo.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Kết Quả Mong Đợi

Sau khi chạy chương trình, `workbook` sẽ chứa một worksheet duy nhất trông như sau:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

- Cột **Name** có nền xanh nhạt, chứng minh mảng kiểu hoạt động.  
- Tiêu đề cột được tạo tự động vì chúng tôi đã truyền `true` cho `importColumnNames`.  
- Các giá trị null hiển thị dưới dạng ô trống, đây là hành vi mặc định của Aspose.Cells.

## Bước 5: Lưu Workbook (Tùy Chọn nhưng Hữu Ích)

Bạn có thể muốn ghi tệp ra đĩa hoặc truyền nó trở lại cho client web. Việc lưu rất đơn giản:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Nếu bạn đang nhắm tới các phiên bản Excel cũ hơn, hãy đổi `SaveFormat.Xlsx` thành `SaveFormat.Xls`. API sẽ tự thực hiện chuyển đổi cho bạn.

## Các Trường Hợp Cạnh & Biến Thể

### Nhiều Cột Được Định Dạng

Nếu bạn cần hơn một cột được định dạng, chỉ cần mở rộng mảng `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Bây giờ cả **Name** và **Salary** sẽ có nền xanh nhạt.

### Định Dạng Có Điều Kiện Thay Thế Kiểu Cố Định

Đôi khi bạn muốn một cột chuyển sang màu đỏ khi giá trị vượt quá ngưỡng. Đó là lúc **use default style excel** kết hợp với định dạng có điều kiện:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Nhập Không Có Tiêu Đề

Nếu hệ thống downstream của bạn đã cung cấp tiêu đề riêng, chỉ cần truyền `false` cho đối số `importColumnNames`. Dữ liệu sẽ bắt đầu tại `A1` và bạn có thể viết tiêu đề tùy chỉnh sau đó.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Ví Dụ Hoàn Chỉnh (Tất Cả

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}