---
category: general
date: 2026-10-26
description: Tìm hiểu cách nhập DataTable vào bảng tính Excel bằng C# và Aspose.Cells,
  giữ nguyên kiểu dáng và tiêu đề chỉ trong vài dòng mã.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: vi
lastmod: 2026-10-26
og_description: Cách nhập DataTable vào một worksheet Excel bằng C# và Aspose.Cells.
  Theo dõi hướng dẫn đầy đủ này để giữ nguyên kiểu dáng, tiêu đề và định dạng.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Cách nhập DataTable vào bảng tính Excel – Hướng dẫn từng bước C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Cách nhập DataTable vào bảng tính Excel bằng C#
url: /vi/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách nhập DataTable vào một worksheet Excel bằng C#

Nếu bạn cần **cách nhập datatable** vào một worksheet Excel, hướng dẫn này sẽ chỉ ra các bước chính xác trong C#. Dù bạn đang xây dựng một engine báo cáo hay xuất dữ liệu lưới, bạn sẽ thấy cách giữ nguyên tiêu đề cột và kiểu ô với Aspose.Cells. Giải pháp hoạt động với .NET 6+ và chỉ yêu cầu vài dòng code.

Nhập một DataTable là một nhiệm vụ phổ biến khi làm việc với bảng tính, nhưng các nhà phát triển thường quên bật chuyển đổi kiểu hoặc truyền đúng cờ tiêu đề. Trong tutorial này bạn sẽ học cách cấu hình **ImportTableOptions**, bật **ImportDataTableStyle**, và gọi `ImportDataTable` một cách an toàn. Khi kết thúc, bạn sẽ có một phương thức sẵn sàng chạy mà có thể đưa vào bất kỳ dự án C# nào.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6 SDK hoặc phiên bản mới hơn đã được cài đặt.
* Bản có giấy phép của **Aspose.Cells for .NET** (bản dùng thử miễn phí đủ cho việc thử nghiệm).
* Kiến thức cơ bản về `DataTable` và các khái niệm Excel.
* Một IDE như Visual Studio 2022 (bất kỳ trình soạn thảo nào hỗ trợ C# đều được).

Không cần thêm bất kỳ gói NuGet nào ngoài `Aspose.Cells`.

## Bước 1: Lấy dữ liệu nguồn vào một DataTable

Điều đầu tiên bạn làm khi trả lời **cách nhập datatable** là chuẩn bị dữ liệu. Trong hầu hết các trường hợp thực tế, `DataTable` đến từ truy vấn cơ sở dữ liệu, bộ phân tích CSV, hoặc một bộ sưu tập trong bộ nhớ. Dưới đây là một ví dụ tối thiểu tạo bảng với một vài dòng:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Lý do quan trọng*: Bằng cách xây dựng `DataTable` trước, bạn kiểm soát thứ tự cột, kiểu dữ liệu và tên tiêu đề — tất cả đều được bảo toàn khi bạn nhập bảng này vào một worksheet Excel sau này.

## Bước 2: Tạo `ImportTableOptions` và bật nhập kiểu

Khi trả lời **cách nhập datatable**, quyết định tiếp theo là bạn có muốn giữ lại kiểu hiển thị (phông chữ, màu sắc, viền) đã được định nghĩa trên `DataTable` nguồn hay không. Aspose.Cells cung cấp lớp `ImportTableOptions` để kiểm soát chi tiết. Đặt `ImportDataTableStyle = true` sẽ sao chép thông tin kiểu sang worksheet đích.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Lý do quan trọng*: Nếu không bật `ImportDataTableStyle`, các ô được nhập sẽ sử dụng kiểu mặc định của worksheet, làm mất mọi định dạng tùy chỉnh bạn đã áp dụng cho `DataTable`. Cờ này là thiết yếu cho một xuất khẩu chuyên nghiệp.

## Bước 3: Nhập DataTable vào worksheet, bao gồm tiêu đề

Bây giờ bạn đã có mọi thứ cần thiết để trả lời **cách nhập datatable** vào một tệp Excel. Bạn tạo một workbook, chọn một worksheet, và gọi `ImportDataTable`. Tham số thứ hai của phương thức (`true`) báo cho Aspose.Cells ghi tiêu đề cột ở hàng đầu tiên.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Chạy `ExportDataTableToExcel("Employees.xlsx")` sẽ tạo ra tệp `Employees.xlsx` trong đó hàng đầu tiên chứa **Id**, **Name**, và **Department**, và mỗi ô giữ nguyên kiểu đã định nghĩa trong `DataTable` gốc.

### Ví dụ đầy đủ có thể chạy

Dưới đây là một chương trình console tự chứa đầy đủ, minh họa **cách nhập datatable** và lưu kết quả vào thư mục hiện tại. Sao chép‑dán vào một dự án console mới và chạy nó.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Kết quả mong đợi**  
Khi mở `Employees.xlsx`, bạn sẽ thấy:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Tất cả các ô giữ nguyên kiểu mặc định của DataTable (phông chữ, căn chỉnh). Nếu bạn đã áp dụng kiểu tùy chỉnh cho `DataTable` trước khi nhập, các kiểu đó sẽ xuất hiện giống hệt trong worksheet vì `ImportDataTableStyle` được đặt thành `true`.

## Những lỗi thường gặp và mẹo thực tiễn

| Vấn đề | Nguyên nhân | Cách tránh |
|-------|-------------|------------|
| **Thiếu tiêu đề** | Truyền `false` làm tham số thứ hai của `ImportDataTable` khiến bỏ qua tên cột. | Luôn dùng `true` khi cần tiêu đề, hoặc tự viết tiêu đề trước khi nhập. |
| **Kiểu không được chuyển** | Quên bật `ImportDataTableStyle`. | Đặt `ImportDataTableStyle = true` trong `ImportTableOptions`. |
| **Bảng lớn gây chậm** | Nhập hàng triệu dòng mà không phân trang. | Nhập theo lô hoặc dùng overload `ImportDataTable` với tham số `startRow` để truyền dữ liệu từng phần. |
| **Tham chiếu worksheet sai** | Sử dụng `workbook.Worksheets[1]` khi chỉ có một sheet. | Dùng `workbook.Worksheets[0]` hoặc tạo sheet mới bằng `workbook.Worksheets.Add()`. |
| **Hết hạn giấy phép** | Bản dùng thử Aspose.Cells hiển thị watermark sau 30 ngày. | Áp dụng giấy phép hợp lệ với `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Mẹo chuyên nghiệp**: Nếu cần áp dụng một chủ đề tùy chỉnh sau khi nhập, gọi `ws.Cells.ApplyStyle(style)` trong đó `style` là một đối tượng `Style` bạn cấu hình một lần và tái sử dụng cho các hàng.

## Mở rộng giải pháp

Khi đã biết **cách nhập datatable**, bạn có thể khám phá các kịch bản liên quan:

* **Nhập nhiều bảng** – lặp lại quá trình nhập trên các worksheet khác nhau.
* **Định dạng có điều kiện** – sau khi nhập, thêm quy tắc bằng `ws.Cells.ApplyConditionalFormatting`.
* **Xuất sang CSV** – dùng `workbook.Save("file.csv", SaveFormat.Csv)` nếu cần định dạng văn bản thuần.
* **Đọc lại vào DataTable** – dùng `ws.Cells.ExportDataTable` để kiểm tra tính toàn vẹn vòng tròn.

Tất cả các mở rộng này dựa trên mẫu cốt lõi đã trình bày: lấy dữ liệu, cấu hình tùy chọn nhập, và gọi một phương thức Aspose.Cells duy nhất.

## Kết luận

Bạn đã có một câu trả lời hoàn chỉnh, sẵn sàng cho môi trường production về **cách nhập datatable** vào một worksheet Excel bằng C#. Tutorial đã bao gồm việc lấy dữ liệu nguồn, cấu hình `ImportTableOptions` với `ImportDataTableStyle`, và thực hiện nhập bằng `ImportDataTable`. Khi theo dõi mẫu code, bạn sẽ tự động giữ lại tiêu đề và kiểu, đồng thời có thể điều chỉnh mẫu cho tập dữ liệu lớn hơn, nhiều sheet, hoặc nhu cầu định dạng bổ sung.

Sẵn sàng tự động hoá quy trình báo cáo? Hãy thay thế `DataTable` mẫu bằng truy vấn cơ sở dữ liệu thực, thử nghiệm với các kiểu ô tùy chỉnh, và tích hợp phương thức vào lớp dịch vụ hiện có. Chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoạt động đầy đủ cùng giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}