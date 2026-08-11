---
category: general
date: 2026-08-11
description: Tạo sheet Excel từ DataTable trong C# và xuất DataTable ra Excel với
  việc đặt tên sheet tự động. Tìm hiểu cách thêm hàng vào DataTable và lưu workbook
  dưới dạng xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: vi
lastmod: 2026-08-11
og_description: Tạo bảng tính Excel từ DataTable trong C#. Hướng dẫn này cho thấy
  cách xuất DataTable ra Excel, thêm dòng vào DataTable, tạo nhiều bảng tính Excel
  và lưu workbook dưới dạng xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Tạo bảng tính Excel từ DataTable trong C# – hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Tạo bảng tính Excel từ DataTable trong C# – hướng dẫn từng bước
url: /vi/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo sheet Excel từ DataTable trong C# – hướng dẫn từng bước

Nếu bạn cần **tạo sheet excel** từ một `DataTable` trong C#, hướng dẫn này sẽ cho bạn thấy cách thực hiện chính xác. Bạn sẽ thấy cách **xuất datatable ra excel**, thêm các hàng, xử lý các tên sheet trùng lặp, và cuối cùng **lưu workbook dưới dạng xlsx**.

Ví dụ sử dụng Aspose.Cells, một thư viện .NET được sử dụng rộng rãi cho tự động hoá Excel. Các khái niệm tương tự áp dụng cho các thư viện khác hỗ trợ xử lý kiểu SmartMarker, nhưng đoạn mã dưới đây hoạt động ngay lập tức với Aspose.Cells 22.12 hoặc mới hơn.

## Yêu cầu trước

* .NET 6.0 SDK hoặc phiên bản mới hơn đã được cài đặt  
* Tham chiếu tới gói NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Kiến thức cơ bản về `DataTable` và các ứng dụng console C#  

Những yêu cầu này giúp hướng dẫn tự chứa và tránh việc sử dụng công cụ bên ngoài.

## Bước 1: Tạo một DataTable sẽ được xuất ra Excel

Bước đầu tiên là xây dựng một `DataTable` phản ánh dữ liệu bạn muốn trong bảng tính. Ở đây chúng ta tạo một bảng có tên **Sheet1**, thêm cột `Id`, và chèn hai hàng.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Tại sao điều này quan trọng:**  
`DataTable` là một biểu diễn dữ liệu dạng bảng trong bộ nhớ tiện lợi. Đặt tên bảng là `"Sheet1"` cho Aspose.Cells biết sheet nào sẽ được mục tiêu khi xử lý SmartMarkers.

## Bước 2: Thêm các hàng vào DataTable (mở rộng tùy chọn)

Nếu dữ liệu nguồn của bạn là động, bạn thường cần thêm các hàng trong một vòng lặp. Đoạn mã dưới đây minh họa một mẫu điển hình:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Mẹo:** Khi thêm nhiều hàng, hãy cân nhắc tắt các ràng buộc (`dataTable.Constraints.Clear()`) để cải thiện hiệu suất.

## Bước 3: Cấu hình tùy chọn SmartMarker để tự động tạo nhiều sheet excel

Các tùy chọn SmartMarker cho phép bạn kiểm soát cách xử lý các tên sheet trùng lặp. Đặt `DetailSheetNewName` thành `"Sheet1_{0}"` sẽ khiến Aspose.Cells đổi tên các sheet tiếp theo thành `Sheet1_1`, `Sheet1_2`, v.v.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Tại sao điều này quan trọng:**  
Khi bạn xử lý nhiều đối tượng `DataTable` có cùng tên, Excel thường sẽ báo lỗi vì tên sheet phải là duy nhất. Mẫu `DetailSheetNewName` loại bỏ xung đột này một cách tự động.

## Bước 4: Xử lý SmartMarkers và xuất datatable ra excel

Bây giờ chúng ta tạo một `Workbook` mới, chạy `ProcessSmartMarkers`, và để Aspose.Cells điền dữ liệu vào (các) worksheet dựa trên `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Giải thích:**  
`ProcessSmartMarkers` quét workbook để tìm các marker như `&=Sheet1!A1` (không hiển thị ở đây) và thay thế chúng bằng dữ liệu từ `dataTable`. Vì chúng ta bắt đầu với một workbook trống, Aspose.Cells tạo một sheet mới có tên trùng với tên bảng và điền các hàng mà chúng ta đã thêm.

## Bước 5: Lưu workbook dưới dạng xlsx

Cuối cùng, ghi workbook ra đĩa với định dạng OpenXML hiện đại (`.xlsx`). Bạn có thể thay đổi đường dẫn cho phù hợp với môi trường của mình.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Kết quả:**  
Chạy chương trình sẽ tạo ra một tệp Excel chứa:

| Tên sheet | Các hàng |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (nếu một DataTable khác có cùng tên được xử lý) |

Logic đổi tên sheet đảm bảo **tạo nhiều sheet excel** mà không cần quản lý tên thủ công.

## Các biến thể phổ biến và trường hợp đặc biệt

| Situation | How to handle it |
|-----------|------------------|
| **Bảng rất lớn** (≥ 100 000 hàng) | Sử dụng `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` trước khi xử lý để giảm mức sử dụng bộ nhớ. |
| **Thứ tự cột tùy chỉnh** | Sắp xếp lại các đối tượng `DataColumn` trong `DataTable` trước khi gọi `ProcessSmartMarkers`. |
| **Nhiều DataTable với các tên khác nhau** | Gọi `ProcessSmartMarkers` cho mỗi bảng; Aspose.Cells sẽ tự động tạo một sheet riêng cho mỗi tên. |
| **Cần một hàng tiêu đề có định dạng** | Sau khi xử lý, truy cập `Worksheet.Cells["A1"]` và áp dụng các thuộc tính `Style` (phông chữ, nền). |
| **Lưu vào stream thay vì file** | Thay thế `workbook.Save(outputPath, SaveFormat.Xlsx)` bằng `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Mẹo chuyên nghiệp:** Luôn bao bọc các thao tác hệ thống tệp trong khối `try…catch` để phát hiện sớm các vấn đề về quyền truy cập.

## Toàn bộ mã nguồn (sẵn sàng sao chép)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in ra:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Mở `DuplicateSheets.xlsx` sẽ hiển thị một sheet có tên **Sheet1** với cột `Id` chứa các giá trị `1, 2, 3, 4, 5`. Nếu sau này bạn xử lý một `DataTable` khác có tên `"Sheet1"` trong cùng một workbook, Aspose.Cells sẽ tự động tạo **Sheet1_1**, **Sheet1_2**, v.v.

## Kết luận

Bây giờ bạn đã biết cách **tạo sheet excel** từ một `DataTable` trong C#, **xuất datatable ra excel**, **thêm các hàng vào datatable**, tạo **nhiều sheet excel** với việc đặt tên tự động, và **lưu workbook dưới dạng xlsx**. Ví dụ đầy đủ, có thể chạy được này minh họa quy trình từ đầu đến cuối và cung cấp các mẹo thực tế cho các bộ dữ liệu lớn và định dạng tùy chỉnh.

### Tiếp theo là gì?

* Khám phá **định dạng ô** (phông chữ, màu sắc, viền) bằng cách truy cập `Worksheet.Cells` sau `ProcessSmartMarkers`.  
* Sử dụng **vòng lặp SmartMarker** để tạo báo cáo master‑detail trong một workbook duy nhất.  
* Chuyển sang **xuất CSV** bằng cách thay đổi `SaveFormat.Csv` nếu bạn cần một biểu diễn dạng văn bản thuần.  

Bạn có thể tự do điều chỉnh mã cho các nguồn dữ liệu của mình—cho dù đó là truy vấn cơ sở dữ liệu, phản hồi API, hoặc một collection trong bộ nhớ. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo và lưu Workbook Excel dưới dạng ODS bằng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cách tạo và lưu Workbook Excel dưới dạng SVG bằng Aspose.Cells cho Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Cách tạo và xuất Excel sang HTML bằng Aspose.Cells Java | Hướng dẫn thao tác Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}