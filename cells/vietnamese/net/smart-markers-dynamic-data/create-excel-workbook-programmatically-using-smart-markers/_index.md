---
category: general
date: 2026-09-24
description: Tạo sổ làm việc Excel một cách lập trình và học cách tạo nhiều sheet
  chi tiết, sau đó lưu sổ làm việc dưới dạng tệp xlsx với ví dụ C# rõ ràng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: vi
lastmod: 2026-09-24
og_description: Tạo workbook Excel bằng lập trình, xem cách tạo nhiều sheet chi tiết
  và lưu workbook dưới dạng tệp xlsx trong một ví dụ duy nhất, có thể chạy được.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Tạo workbook Excel bằng lập trình – hướng dẫn C# đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Tạo workbook Excel bằng cách lập trình sử dụng Smart Markers
url: /vi/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo workbook Excel bằng chương trình sử dụng Smart Markers

Nếu bạn cần **tạo workbook Excel bằng chương trình**, hướng dẫn này sẽ chỉ cho bạn cách thực hiện với Aspose.Cells .NET. Bạn cũng sẽ khám phá **cách tạo nhiều sheet chi tiết** từ một nguồn dữ liệu duy nhất và cuối cùng **lưu workbook dưới dạng tệp xlsx** mà không cần bất kỳ bước thủ công nào.  

Giải pháp là tự chứa: chúng tôi sẽ đi qua từng dòng mã, giải thích tại sao mỗi thiết lập quan trọng, và đề cập đến các lỗi thường gặp như tên sheet trùng lặp. Khi hoàn thành, bạn sẽ có một ứng dụng console sẵn sàng chạy, tạo ra một workbook có sheet tổng quan và một tập hợp các sheet chi tiết.

## Những gì bạn sẽ cần

| Điều kiện tiên quyết | Lý do |
|----------------------|-------|
| .NET 6.0 SDK hoặc mới hơn | Cung cấp môi trường chạy cho ứng dụng console C# |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Cung cấp các lớp `Workbook`, `SmartMarkerProcessor` và `SmartMarkerOptions` |
| Nguồn dữ liệu đơn giản (ví dụ: `DataTable` hoặc danh sách các đối tượng) | Cung cấp các giá trị mà Smart Markers sẽ mở rộng |
| Visual Studio 2022 hoặc bất kỳ trình soạn thảo nào hỗ trợ .NET | Giúp dễ dàng biên dịch và chạy mã |

> **Mẹo chuyên nghiệp:** Cài đặt gói Aspose.Cells qua CLI trước khi bắt đầu:  
> `dotnet add package Aspose.Cells`

## Bước 1: Thiết lập dự án và nhập các namespace

Tạo một dự án console mới và đưa các namespace cần thiết vào phạm vi.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Tại sao điều này quan trọng*: `Aspose.Cells` xử lý vòng đời workbook, trong khi `Aspose.Cells.SmartMarkers` cung cấp engine Smart Marker mạnh mẽ có thể tạo nhiều sheet từ một mẫu duy nhất.

## Bước 2: Tạo workbook Excel bằng chương trình

Hành động cụ thể đầu tiên là khởi tạo một `Workbook`. Đối tượng này đại diện cho toàn bộ tệp Excel trong bộ nhớ.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Nếu bạn muốn bắt đầu từ một mẫu đã có sẵn các hàng tiêu đề hoặc định dạng, thay thế `new Workbook()` bằng `new Workbook("Template.xlsx")`. Phần còn lại của quy trình hoạt động tương tự.

## Bước 3: Chuẩn bị mẫu Smart Marker

Smart Markers hoạt động trên nội dung ô chứa các placeholder như `&=Employees.Name`. Trong tutorial này chúng ta sẽ thêm một mẫu đơn giản trực tiếp qua mã, nhưng bạn cũng có thể chỉnh sửa sheet thủ công trong Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Tại sao điều này quan trọng*: Placeholder `&=Employees.Name` cho biết bộ xử lý Smart Marker sẽ lặp lại trên tập hợp `Employees`. Mỗi lần lặp sẽ tạo ra một worksheet mới vì chúng ta sẽ cấu hình bộ xử lý để tạo **sheet chi tiết** cho mỗi hàng.

## Bước 4: Xây dựng nguồn dữ liệu chứa nhiều hàng

Chúng ta sẽ sử dụng một `DataTable` như một cách nhanh để mô phỏng tập hợp các bản ghi nhân viên.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Bạn có thể thay thế bằng bất kỳ `IEnumerable` nào (ví dụ: `List<Employee>`) – Smart Markers chấp nhận bất kỳ nguồn dữ liệu nào triển khai `IEnumerable`.

## Bước 5: Cấu hình tùy chọn Smart Marker – cách tạo nhiều sheet chi tiết

Mặc định, Smart Markers ghi dữ liệu trở lại cùng một sheet. Để tạo **nhiều sheet chi tiết**, bạn phải đặt thuộc tính `DetailSheetNewName`. Điều này cũng minh họa **cách tạo nhiều sheet chi tiết** mà không gây xung đột tên.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Nếu nguồn dữ liệu chứa các tên trùng lặp, bộ xử lý sẽ tự động thêm hậu tố số (ví dụ: `Detail_1`, `Detail_2`). Điều này ngăn lỗi thời gian chạy và đảm bảo tất cả các sheet chi tiết được lưu.

## Bước 6: Xử lý Smart Markers

Bây giờ chúng ta gọi bộ xử lý, truyền nguồn dữ liệu và các tùy chọn vừa định nghĩa.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Tại sao điều này quan trọng*: Bộ xử lý đọc placeholder `&=Employees.Name`, lặp qua mỗi hàng của `employees`, tạo một sheet mới có tên “Detail”, và ghi dữ liệu hàng vào sheet đó. Sheet gốc vẫn giữ nguyên như một sheet tổng hợp hoặc master.

## Bước 7: Lưu workbook dưới dạng tệp xlsx

Cuối cùng, lưu workbook vào đĩa bằng mẫu **save workbook as xlsx file**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Enum `SaveFormat.Xlsx` đảm bảo tệp được lưu ở định dạng Office Open XML hiện đại, tương thích với Excel 2007+ và hầu hết các dịch vụ đám mây.

## Ví dụ đầy đủ, có thể chạy được

Sao chép đoạn mã sau vào `Program.cs` của một dự án console .NET và chạy nó. Chương trình sẽ tạo ra `detail.xlsx` trong thư mục `output`, chứa một sheet master và ba sheet chi tiết (mỗi nhân viên một sheet).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Kết quả mong đợi**

- `output/detail.xlsx` chứa:
  - **Sheet1** – mẫu gốc với tiêu đề “Employee Report”.
  - **Detail** – sheet chi tiết đầu tiên với bản ghi của Alice.
  - **Detail_1** – sheet chi tiết thứ hai với bản ghi của Bob.
  - **Detail_2** – sheet chi tiết thứ ba với bản ghi của Carol.

Mở tệp trong Excel và bạn sẽ thấy mỗi nhân viên trên một sheet riêng, chứng minh rằng chúng ta đã thành công **tạo nhiều sheet chi tiết** và **lưu workbook dưới dạng tệp xlsx**.

## Các câu hỏi thường gặp & xử lý trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu tôi cần một tên tùy chỉnh cho mỗi sheet chi tiết thì sao?* | Đặt `DetailSheetNewName = "Employee_"` và bao gồm một cột có tên `SheetName` trong nguồn dữ liệu. Bộ xử lý sẽ nối giá trị của `SheetName` vào tên cơ sở. |
| *Tôi có thể giữ sheet gốc làm bản tóm tắt của tất cả các chi tiết không?* | Có. Sheet master vẫn không bị thay đổi; bạn có thể thêm công thức tham chiếu đến các sheet chi tiết đã tạo. |
| *Điều gì xảy ra khi nguồn dữ liệu rỗng?* | Không có sheet chi tiết nào được tạo, nhưng workbook vẫn được lưu. Hãy cân nhắc kiểm tra `employees.Rows.Count` trước khi xử lý nếu cần xử lý đặc biệt. |
| *Có thể sử dụng tệp mẫu hiện có không?* | Thay thế `new Workbook()` bằng `new Workbook("Template.xlsx")`. Tất cả logic Smart Marker hoạt động như bình thường. |

## Kết luận

Bạn giờ đã biết **cách tạo workbook Excel bằng chương trình**, cách **tạo nhiều sheet chi tiết** bằng Smart Markers, và cách **lưu workbook dưới dạng tệp xlsx** với Aspose.Cells. Ví dụ hoàn chỉnh có thể được điều chỉnh cho hoá đơn, báo cáo, hoặc bất kỳ kịch bản nào yêu cầu đầu ra Excel master‑detail.

### Các bước tiếp theo

- Khám phá các tính năng Smart Marker khác như **group markers** và **conditional formatting**.  
- Thay thế `DataTable` bằng truy vấn cơ sở dữ liệu thực để tạo báo cáo quy mô lớn.  
- Sử dụng `Workbook.Save("output.pdf", SaveFormat.Pdf)` để xuất cùng dữ liệu sang PDF cho việc phân phối.

Hãy thoải mái thử nghiệm các cách đặt tên, kiểu dáng, hoặc thêm các worksheet khác—kỹ năng tạo Excel bằng chương trình của bạn đã sẵn sàng cho môi trường sản xuất. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Excel Workbook C# – Thêm Comment & Lưu dưới dạng XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Tạo Workbook mới trong C# – Thêm công thức và Lưu tệp Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Tạo Excel Workbook C# – Chèn JSON và Lưu dưới dạng XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}