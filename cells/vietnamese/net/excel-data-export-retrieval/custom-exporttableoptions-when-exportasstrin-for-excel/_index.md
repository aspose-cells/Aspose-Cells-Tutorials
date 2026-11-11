---
category: general
date: 2026-10-26
description: Tùy chỉnh ExportTableOptions khi ExportAsStrin cho phép bạn xuất dữ liệu
  Excel dưới dạng chuỗi trong C#. Hãy làm theo hướng dẫn từng bước để cấu hình và
  chạy quá trình xuất.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: vi
lastmod: 2026-10-26
og_description: Tùy chỉnh ExportTableOptions khi ExportAsStrin cho phép xuất Excel
  chỉ dưới dạng chuỗi. Tìm hiểu các bước chính xác để cấu hình và chạy việc xuất trong
  C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Tùy chỉnh ExportTableOptions khi ExportAsString – xuất Excel dưới dạng chuỗi
  trong C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Tùy chỉnh ExportTableOptions khi ExportAsString cho Excel
url: /vi/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – xuất Excel dưới dạng chuỗi trong C#

Nếu bạn cần **Custom ExportTableOptions when ExportAsStrin** để lấy giá trị của mỗi ô dưới dạng chuỗi thuần, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác. Dù bạn đang xây dựng một pipeline nhập dữ liệu hay cần một bản xuất CSV sạch sẽ, bạn sẽ thấy tại sao việc cấu hình các tùy chọn như vậy tránh được những bất ngờ khi chuyển đổi kiểu dữ liệu.

Trong tutorial này bạn sẽ học **cách xuất excel dưới dạng chuỗi** bằng thư viện Aspose.Cells, xem mã hoàn chỉnh, có thể chạy được, và hiểu lý do đằng sau mỗi cài đặt. Không cần tài liệu bên ngoài – mọi thứ bạn cần đều có ở đây.

## Yêu cầu trước

* .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ .NET)  
* Gói Aspose.Cells cho .NET (cài đặt qua NuGet: `Install-Package Aspose.Cells`)  
* Một workbook Excel (`sample.xlsx`) đặt trong thư mục gốc của dự án  

Các mục này là những phụ thuộc duy nhất; mã chạy trên Windows, Linux hoặc macOS mà không cần thư viện bổ sung.

## Bước 1: Tải workbook bạn muốn xuất

Điều đầu tiên bạn làm khi sử dụng **Custom ExportTableOptions when ExportAsStrin** là lấy một đối tượng `Worksheet` từ một workbook đã tải. Đối tượng này cho phép bạn truy cập vào các hàng, cột và API xuất.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*​Tại sao điều này quan trọng:*  
`Workbook` đọc tệp một lần và giữ tất cả thông tin định dạng trong bộ nhớ. Bằng cách chọn một `Worksheet` cụ thể, bạn giới hạn phạm vi xuất và tránh xử lý không cần thiết các sheet ẩn.

## Bước 2: Cấu hình ExportTableOptions với ExportAsString = true

Cốt lõi của **Custom ExportTableOptions when ExportAsStrin** là đối tượng `ExportTableOptions`. Đặt `ExportAsString` buộc trình xuất xử lý mọi ô như một chuỗi, bất kể kiểu dữ liệu gốc (ngày, số, boolean, v.v.). Bật `PreserveFormatting` giữ lại kiểu dáng trực quan (ví dụ, ký hiệu tiền tệ) trong chuỗi kết quả.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*​Tại sao điều này quan trọng:*  
Khi bạn sau này gọi `ExportDataTable`, thư viện thường cố gắng suy đoán kiểu .NET của mỗi cột. Với `ExportAsString = true`, bước suy đoán này bị bỏ qua, ngăn ngừa các chuyển đổi `DateTime` hoặc `double` không mong muốn có thể làm hỏng các bộ phân tích CSV phía sau.

## Bước 3: Xuất một phạm vi ra DataTable bằng các tùy chọn tùy chỉnh

Bây giờ bạn có thể xuất một phạm vi hình chữ nhật (hàng 0‑9, cột 0‑4) từ worksheet. Phương thức trả về một `DataTable` trong đó mọi trường đều là `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*​Tại sao điều này quan trọng:*  
`ExportDataTable` là cách thuận tiện nhất để chuyển dữ liệu Excel vào một cấu trúc quan hệ mà nhiều API .NET đã hiểu (ví dụ, Entity Framework, Dapper). Bằng cách truyền **Custom ExportTableOptions when ExportAsStrin**, bạn đảm bảo mỗi `DataColumn.DataType` sẽ là `typeof(string)`.

## Bước 4: Xác minh kết quả – tất cả giá trị đều là chuỗi

Thực hành tốt là xác nhận rằng quá trình xuất hoạt động như mong đợi. Vòng lặp sau in ra mỗi ô và kiểu thời gian chạy của nó.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Kết quả mong đợi**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Mỗi ô hiển thị `String` là kiểu của nó, xác nhận rằng **Custom ExportTableOptions when ExportAsStrin** đã hoạt động đúng.

## Bước 5: Tùy chọn – ghi DataTable ra CSV

Nếu mục tiêu cuối cùng của bạn là một tệp văn bản thuần, bạn có thể dễ dàng tuần tự hoá `DataTable` sang CSV:



## Bạn nên học gì tiếp theo?

Những tutorial sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, có thể chạy được cùng với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Xuất chuỗi HTML từ Excel sang DataTable bằng Aspose.Cells cho .NET: Hướng dẫn từng bước](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Xuất thuộc tính tùy chỉnh Excel PDF bằng Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java: Tùy chỉnh bộ lọc tải Excel xuất khẩu](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}