---
category: general
date: 2026-07-03
description: Áp dụng màu nền xen kẽ cho các hàng khi bạn nhập DataTable vào Excel
  bằng C#. Tìm hiểu cách xuất DataTable C# sang Excel, lưu bảng Excel đã định dạng
  và giữ nguyên định dạng của workbook.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: vi
og_description: Áp dụng màu nền xen kẽ cho các hàng trong Excel bằng C#. Hướng dẫn
  này chỉ cách nhập DataTable vào Excel, xuất DataTable C# sang Excel và lưu workbook
  với định dạng.
og_title: Áp dụng màu nền xen kẽ cho các hàng trong Excel bằng C# – Hướng dẫn đầy
  đủ
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Áp dụng màu nền xen kẽ cho các hàng trong Excel bằng C# – Hướng dẫn chi tiết
url: /vi/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Áp Dụng Màu Nền Xen Kẽ Cho Các Hàng Trong Excel Bằng C# – Hướng Dẫn Đầy Đủ

Bạn đã bao giờ cần **áp dụng màu nền xen kẽ cho các hàng** khi xuất một `DataTable` C# ra Excel chưa? Bạn không phải là người duy nhất—các nhà phát triển luôn hỏi làm sao để các bảng tính trông chuyên nghiệp mà không phải chỉnh sửa thủ công trong Excel sau này. Tin tốt là gì? Bạn có thể làm điều này một cách lập trình chỉ với vài dòng code.

Trong tutorial này chúng ta sẽ đi qua **import datatable to excel**, cho bạn thấy cách **export c# datatable to excel** với một bảng được định dạng, và cuối cùng **save styled table excel** trong khi giữ nguyên định dạng. Khi kết thúc, bạn sẽ có thể **save workbook with formatting** trông sẵn sàng cho buổi họp khách hàng.

## Prerequisites

- .NET 6.0 hoặc mới hơn (ví dụ mẫu dùng .NET 6, nhưng bất kỳ phiên bản gần đây nào cũng được)
- Aspose.Cells for .NET (bản dùng thử miễn phí hoặc bản có giấy phép) – thư viện này giúp việc định dạng trở nên dễ dàng
- Một nguồn `DataTable` (có thể từ cơ sở dữ liệu, CSV, hoặc bộ sưu tập trong bộ nhớ)

> **Pro tip:** Nếu bạn chưa có Aspose.Cells, bạn có thể tải nó từ NuGet bằng lệnh `dotnet add package Aspose.Cells`.

## Step 1: Set Up the Project and Load Your Data

Đầu tiên, tạo một console app (hoặc bất kỳ dự án C# nào) và thêm các câu lệnh `using` cần thiết. Sau đó kéo dữ liệu vào một `DataTable`. Để minh họa, chúng ta sẽ tạo một bảng đơn giản ngay trong code.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Tại sao điều này quan trọng:** Có một `DataTable` sẵn sàng có nghĩa là bạn có thể **import datatable to excel** chỉ bằng một lời gọi, loại bỏ nhu cầu chèn dữ liệu từng ô một một cách thủ công.

## Step 2: Create a Workbook and Define the Alternating Row Styles

Bây giờ chúng ta sẽ khởi tạo một `Workbook` mới. Bí quyết để **apply alternating row colors** nằm ở `ImportTableOptions.StyleArray`. Chúng ta sẽ dùng hai style có sẵn (thường là trắng và xám nhạt) nhưng bạn có thể tùy chỉnh sau.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Giải thích:** `ImportTableOptions` chỉ cho Aspose.Cells cách xử lý mỗi hàng trong quá trình nhập. Khi cung cấp một `StyleArray` gồm hai phần tử, thư viện sẽ tự động tô màu hàng lẻ bằng style đầu tiên và hàng chẵn bằng style thứ hai—đúng như bạn cần để **apply alternating row colors**.

## Step 3: Pull the DataTable Into the Worksheet (Including Headers)

Với workbook và các style đã sẵn sàng, chúng ta sẽ **import datatable to excel**. Phương thức `ImportDataTable` thực hiện phần lớn công việc: ghi tiêu đề cột, áp dụng mảng style, và đặt dữ liệu bắt đầu từ ô A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Tại sao chúng ta truyền `true` cho đối số thứ hai:** Nó báo cho phương thức ghi tên cột vào hàng đầu tiên, điều này rất cần thiết cho một báo cáo trông chuyên nghiệp.

## Step 4: Fine‑Tune the Table (Optional but Handy)

Nếu bạn muốn bảng tự động điều chỉnh độ rộng cột hoặc thêm một hàng lọc, một vài dòng bổ sung sẽ làm cho nó nổi bật hơn.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Những tinh chỉnh này không ảnh hưởng đến màu nền xen kẽ nhưng cải thiện trải nghiệm người dùng của file **save styled table excel**.

## Step 5: Save the Workbook While Keeping All Formatting

Cuối cùng, chúng ta ghi file ra đĩa. Phương thức `Save` giữ nguyên mọi style đã thiết lập, đảm bảo các hàng xen kẽ vẫn được duy trì.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Khi bạn mở `StyledEmployees.xlsx`, bạn sẽ thấy một bảng sạch sẽ với các hàng xen kẽ giữa trắng và xám nhạt—đúng như dấu hiệu trực quan mà nhiều người dùng dựa vào để tăng khả năng đọc.

### Expected Output

| ID | Tên    | Phòng ban | Ngày tuyển |
|----|--------|-----------|------------|
| 1  | Alice  | Finance   | 15‑01‑2020 |
| 2  | Bob    | HR        | 23‑06‑2019 |
| 3  | Charlie| IT        | 10‑03‑2021 |
| 4  | Diana  | Marketing | 05‑11‑2018 |

- Hàng 1, 3 … → nền trắng  
- Hàng 2, 4 … → nền xám nhạt  

Đó là toàn bộ quy trình **save workbook with formatting**.

## Common Questions & Edge Cases

### What if my DataTable has thousands of rows?

Phương thức `ImportDataTable` truyền dữ liệu một cách hiệu quả, nhưng bạn có thể gặp giới hạn bộ nhớ khi bảng quá lớn. Trong trường hợp đó, hãy cân nhắc chia xuất khẩu thành nhiều worksheet hoặc sử dụng overload của `ImportDataTable` cho phép chỉ định hàng và cột bắt đầu.

### Can I use custom colors instead of the built‑in ones?

Chắc chắn rồi. Chỉ cần thay thế các lệnh gán `ForegroundColor` trong `styleWhite` và `styleGray` bằng bất kỳ `System.Drawing.Color` nào bạn muốn—có thể là màu pastel xanh hoặc màu thương hiệu công ty.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### How do I ensure the alternating style works when the user adds rows later?

Nếu người dùng chỉnh sửa file thủ công, mảng style ban đầu sẽ không tự động mở rộng. Một cách khắc phục nhanh là chuyển phạm vi thành một Excel Table (`ListObject`) sau khi nhập; Excel sẽ tự lặp lại mẫu cho các hàng mới.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Bây giờ bất kỳ hàng mới nào cũng sẽ kế thừa màu nền xen kẽ.

## Full Working Example (All Steps in One Place)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Chạy chương trình, mở file đã tạo, và bạn sẽ ngay lập tức thấy các màu nền xen kẽ được áp dụng—không cần định dạng thủ công.

## Conclusion

Chúng ta vừa minh họa cách **apply alternating row colors** khi **import datatable to excel** bằng C#. Quy trình này bao gồm mọi thứ bạn cần để **export c# datatable to excel**, **save styled table excel**, và **save workbook with formatting** trông chuyên nghiệp ngay từ đầu.

Bước tiếp theo? Hãy thử hoán đổi hai style để tạo theme tùy chỉnh, hoặc biến phạm vi thành một Excel Table để người dùng có thể sắp xếp và lọc trong khi vẫn giữ nguyên mẫu màu. Bạn cũng có thể khám phá conditional formatting qua `ConditionalFormattingCollection` để có các dấu hiệu trực quan động hơn.

Got a twist


## What Should You Learn Next?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ và các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}