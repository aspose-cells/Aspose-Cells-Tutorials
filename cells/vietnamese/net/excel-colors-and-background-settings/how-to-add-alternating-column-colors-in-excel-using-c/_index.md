---
category: general
date: 2026-10-01
description: Màu cột xen kẽ trong Excel bằng C# – học cách tạo file Excel từ DataTable,
  đặt màu nền cho ô bằng C#, và nhập DataTable vào Excel với các cột được định dạng.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: vi
lastmod: 2026-10-01
og_description: Màu cột xen kẽ trong Excel dễ dàng. Hãy làm theo hướng dẫn này để
  tạo tệp Excel từ DataTable, đặt màu nền cho ô bằng C#, và nhập DataTable vào Excel
  với các cột được định dạng.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Thêm màu cột xen kẽ trong Excel bằng C# – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Cách thêm màu cột xen kẽ trong Excel bằng C#
url: /vi/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm màu nền cột xen kẽ trong Excel bằng C#

Nếu bạn cần **alternating column colors excel** trong một báo cáo được tạo từ ứng dụng của mình, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh. Bạn sẽ thấy cách tạo tệp Excel từ một `DataTable`, đặt màu nền ô theo kiểu C#, và nhập datatable vào excel trong khi áp dụng một kiểu riêng cho mỗi cột.

Bài hướng dẫn bao gồm mọi thứ bạn cần: các gói NuGet bắt buộc, một mẫu mã đầy đủ, có thể chạy được, và giải thích lý do mỗi bước quan trọng. Khi hoàn thành, bạn sẽ có một workbook đã được định dạng có thể mở trực tiếp trong Microsoft Excel.

## Yêu cầu trước

* .NET 6.0 (hoặc mới hơn) SDK đã được cài đặt  
* Visual Studio 2022 (hoặc bất kỳ IDE nào hỗ trợ C#)  
* Thư viện **Aspose.Cells for .NET** – cài đặt bằng  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells cung cấp các lớp `Workbook`, `Worksheet`, `Style`, và `BackgroundType` được sử dụng trong ví dụ.

## Bước 1: Lấy dữ liệu nguồn dưới dạng `DataTable`

Nhiệm vụ đầu tiên là lấy dữ liệu bạn muốn xuất. Trong các dự án thực tế, bạn có thể điền `DataTable` từ một truy vấn cơ sở dữ liệu, một lời gọi API, hoặc bất kỳ bộ sưu tập nào trong bộ nhớ.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Tại sao điều này quan trọng:**  
Một `DataTable` là một container chung có thể ánh xạ sạch sẽ sang một worksheet của Excel. Sử dụng `DataTable` cho phép bạn **create excel file from datatable c#** mà không cần viết vòng lặp tùy chỉnh cho từng cột.

## Bước 2: Tạo một workbook mới và lấy worksheet đầu tiên của nó

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Giải thích:**  
`Workbook` là đối tượng gốc; `Worksheets[0]` cung cấp cho bạn sheet mặc định nơi dữ liệu sẽ được đặt.

## Bước 3: Chuẩn bị một kiểu riêng cho mỗi cột (màu nền xen kẽ)

Để đạt được **alternating column colors excel**, chúng ta tạo một `Style` cho mỗi cột và gán một màu nền nhẹ thay đổi giữa hai sắc độ.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Tại sao chúng ta dùng vòng lặp:**  
Vòng lặp đảm bảo rằng **set cell background color c#** được áp dụng một cách nhất quán, ngay cả khi số cột thay đổi trong thời gian chạy. Điều này làm cho giải pháp trở nên vững chắc cho các báo cáo động.

## Bước 4: Nhập `DataTable` vào worksheet, áp dụng các kiểu cho cột

Aspose.Cells có thể nhập trực tiếp một `DataTable`, và chúng ta có thể truyền mảng các kiểu để tô màu cho mỗi cột.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Điều gì xảy ra phía sau:**  
`ImportDataTable` ghi hàng tiêu đề, sau đó là mỗi hàng dữ liệu. Vì chúng ta đã cung cấp `columnStyles`, mọi ô trong một cột nhất định sẽ nhận được kiểu tương ứng, mang lại màu nền xen kẽ mong muốn.

## Bước 5: Lưu workbook đã định dạng vào tệp

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Khi bạn mở *StyledTable.xlsx* trong Excel, bạn sẽ thấy mỗi cột được tô màu xen kẽ, giúp bảng dễ đọc hơn.

## Ví dụ đầy đủ, có thể chạy

Kết hợp tất cả các phần lại, dưới đây là một chương trình tự chứa mà bạn có thể sao chép, dán và chạy.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Kết quả mong đợi

* Một tệp có tên **StyledTable.xlsx** nằm tại `C:\Temp\`.
* Worksheet hiển thị ba cột (`Id`, `Name`, `Score`) với màu nền xen kẽ: cột 1 và 3 màu *LightYellow*, cột 2 màu *LightCyan*.
* Tất cả các hàng từ `DataTable` xuất hiện dưới hàng tiêu đề.

## Các câu hỏi thường gặp và trường hợp đặc biệt

| Question | Answer |
|----------|--------|
| *Tôi có thể dùng màu khác không?* | Có. Thay `System.Drawing.Color.LightYellow` và `LightCyan` bằng bất kỳ giá trị `System.Drawing.Color` nào. |
| *Nếu DataTable có nhiều cột thì sao?* | Vòng lặp tự động tạo một style cho mỗi cột, vì vậy mẫu có thể mở rộng mà không cần thay đổi mã. |
| *Tôi có cần giải phóng workbook không?* | Aspose.Cells triển khai `IDisposable`. Nếu bạn bao bọc `Workbook` trong một khối `using`, tài nguyên sẽ được giải phóng kịp thời. |
| *Làm sao áp dụng màu xen kẽ tương tự cho các hàng thay vì cột?* | Tạo một `Style[]` cho các hàng và gọi `worksheet.Cells.ImportDataTable(..., rowStyles)` – các overload của Aspose.Cells hỗ trợ cả hai. |
| *Tôi có thể ghi tệp trực tiếp vào stream (ví dụ, cho một web API) không?* | Có. Sử dụng `workbook.Save(stream, SaveFormat.Xlsx);` thay vì đường dẫn tệp. |

## Mẹo thực tiễn

* **Mẹo chuyên nghiệp:** Lưu cache các đối tượng style nếu bạn tạo nhiều worksheet trong một lần chạy – việc tạo một style tương đối rẻ, nhưng tái sử dụng chúng giảm thiểu việc tiêu tốn bộ nhớ.  
* **Cảnh báo:** Khi sử dụng `System.Drawing.Color` trên các nền tảng không phải Windows, thêm gói NuGet `System.Drawing.Common` và đảm bảo runtime hỗ trợ GDI+.

## Kết luận

Bạn đã biết cách **alternating column colors excel** bằng cách tạo tệp Excel từ một `DataTable` trong C#, đặt màu nền ô với Aspose.Cells, và **import datatable to excel** với một mảng cột đã định dạng. Cách tiếp cận này nhanh, dễ bảo trì, và hoạt động với bất kỳ kích thước dữ liệu nào.

### Các bước tiếp theo

* Khám phá **set cell background color c#** cho định dạng có điều kiện (ví dụ, làm nổi bật điểm thấp).  
* Kết hợp kỹ thuật này với **create excel file from datatable c#** để tạo báo cáo đa sheet.  
* Tìm hiểu API vẽ biểu đồ của Aspose.Cells để thêm tóm tắt trực quan vào cùng một workbook.

Bạn có thể tự do điều chỉnh màu sắc, định dạng tệp hoặc nguồn dữ liệu để phù hợp với nhu cầu dự án của mình. Chúc lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã làm việc đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Đặt Nền Cột trong Excel bằng C# – Hướng Dẫn Đầy Đủ](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Thêm màu nền excel – Kiểu Hàng Xen Kẽ trong C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Tạo Workbook C# – Nhập DataTable vào Excel với Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}