---
category: general
date: 2026-04-07
description: Thêm màu nền cho các hàng trong Excel bằng C#. Tìm hiểu cách áp dụng
  màu nền xen kẽ cho các hàng, thiết lập kiểu nền đặc, và nhập DataTable vào Excel
  trong một quy trình duy nhất.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: vi
og_description: Thêm màu nền cho các hàng Excel bằng C#. Hướng dẫn này chỉ cách áp
  dụng màu nền xen kẽ cho các hàng, đặt nền màu đồng nhất và nhập DataTable vào Excel
  một cách hiệu quả.
og_title: Thêm màu nền vào Excel – Kiểu dòng xen kẽ trong C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Thêm màu nền Excel – Kiểu dòng xen kẽ trong C#
url: /vi/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm màu nền excel – Kiểu hàng xen kẽ trong C#

Bạn đã bao giờ cần **thêm màu nền excel** cho các hàng nhưng không chắc làm thế nào mà không phải viết hàng ngàn dòng code rắc rối? Bạn không đơn độc—hầu hết các nhà phát triển đều gặp khó khăn này khi lần đầu cố gắng làm cho bảng tính của mình trông hơn chỉ là một đống dữ liệu thô.  

Tin tốt là gì? Chỉ trong vài phút, bạn có thể **áp dụng màu nền xen kẽ cho các hàng**, thiết lập **nền đặc**, và thậm chí **nhập datatable vào excel** bằng một mẫu sạch, có thể tái sử dụng trong C#.  

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình, từ việc lấy dữ liệu vào một `DataTable` đến việc tạo kiểu cho mỗi hàng với mẫu sọc màu vàng‑nhẹ‑trắng. Không cần thư viện bên ngoài nào ngoài một gói xử lý Excel vững chắc (như **ClosedXML** hoặc **GemBox.Spreadsheet**), và bạn sẽ thấy tại sao cách tiếp cận này vừa hiệu năng cao vừa dễ bảo trì.

## Những gì bạn sẽ học

- Cách lấy dữ liệu và đưa nó vào một worksheet Excel.  
- Cách **định dạng các hàng excel** với màu nền xen kẽ.  
- Cơ chế phía sau **đặt nền đặc** bằng cách sử dụng đối tượng `Style`.  
- Cách **nhập datatable vào excel** trong khi giữ nguyên kiểu cho các hàng.  
- Mẹo xử lý các trường hợp đặc biệt như bảng trống hoặc bảng màu tùy chỉnh.  

> **Mẹo chuyên nghiệp:** Nếu bạn đã đang sử dụng một đối tượng workbook (`wb`) từ một thư viện hỗ trợ tạo style, bạn có thể tái sử dụng cùng một instance `Style` trên nhiều worksheet—giảm bộ nhớ và giữ cho mã của bạn gọn gàng.

---

## Bước 1: Lấy dữ liệu – Chuẩn bị DataTable

Trước khi có thể áp dụng bất kỳ kiểu nào, chúng ta cần một nguồn dữ liệu cho các hàng. Trong hầu hết các trường hợp thực tế, dữ liệu này đến từ cơ sở dữ liệu, API, hoặc tệp CSV. Để minh họa, chúng ta sẽ chỉ tạo một `DataTable` đơn giản trong bộ nhớ.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Tại sao điều này quan trọng:** Sử dụng `DataTable` cung cấp cho bạn một container dạng bảng, có nhận thức về schema, mà thư viện Excel có thể nhập trực tiếp, loại bỏ nhu cầu viết vòng lặp từng ô.

---

## Bước 2: Tạo kiểu cho hàng – **Áp dụng màu nền xen kẽ cho các hàng**

Bây giờ chúng ta sẽ tạo một mảng các đối tượng `Style`—một cho mỗi hàng—để mỗi hàng có thể nhận nền riêng. Mẫu chúng ta sẽ dùng là màu vàng‑nhẹ cho các hàng chẵn và màu trắng cho các hàng lẻ.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Giải thích:**  
- `wb.CreateStyle()` cung cấp cho bạn một đối tượng style sạch mà bạn có thể chỉnh sửa mà không ảnh hưởng đến các đối tượng khác.  
- Toán tử ba ngôi `(i % 2 == 0)` quyết định hàng là chẵn (vàng nhạt) hay lẻ (trắng).  
- Thiết lập `Pattern = BackgroundType.Solid` là bước quan trọng để **đặt nền đặc**; nếu không, màu sẽ bị bỏ qua.

---

## Bước 3: Lấy Worksheet mục tiêu

Hầu hết các thư viện cung cấp một bộ sưu tập worksheet. Chúng ta sẽ làm việc với worksheet đầu tiên, nhưng bạn có thể chọn bất kỳ chỉ mục hoặc tên nào bạn muốn.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Nếu workbook mới hoàn toàn, thư viện thường tạo một sheet mặc định cho bạn. Nếu không, bạn có thể thêm một sheet một cách rõ ràng:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Bước 4: Nhập DataTable với kiểu hàng – **Nhập datatable vào excel**

Với các kiểu đã sẵn sàng, bước cuối cùng là đưa `DataTable` vào sheet đồng thời áp dụng kiểu tương ứng cho mỗi hàng.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Điều gì đang diễn ra bên trong?**  
- `true` cho phương thức biết viết tiêu đề cột ở hàng đầu tiên.  
- `0, 0` đánh dấu góc trên‑trái (A1) là điểm chèn.  
- `rowStyles` gắn mỗi `Style` với hàng dữ liệu tương ứng, cung cấp cho chúng ta các màu xen kẽ mà chúng ta đã chuẩn bị trước.

---

## Bước 5: Lưu Workbook

Bước cuối cùng của quá trình là lưu workbook vào tệp để bạn có thể mở nó trong Excel và xem kết quả.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Mở tệp và bạn sẽ thấy một sheet được định dạng gọn gàng:

- Hàng tiêu đề in đậm (định dạng mặc định của thư viện).  
- Hàng 1, 3, 5… với nền trắng sạch.  
- Hàng 2, 4, 6… với nền vàng nhạt nhẹ, giúp dễ dàng quét.

### Ảnh chụp đầu ra dự kiến

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Các hàng 2, 4, 6, … sẽ xuất hiện với nền vàng nhạt—đúng là hiệu ứng **áp dụng màu nền xen kẽ cho các hàng** mà chúng ta mong muốn.

![Ví dụ thêm màu nền excel](https://example.com/excel-background.png "Ví dụ thêm màu nền excel")

*(Văn bản thay thế bao gồm từ khóa chính cho SEO.)*

---

## Xử lý các trường hợp đặc biệt & Biến thể

### DataTable rỗng

Nếu `dataTable.Rows.Count` bằng không, mảng `rowStyles` sẽ rỗng và `ImportDataTable` vẫn sẽ ghi hàng tiêu đề (nếu `includeHeaders` là `true`). Không có ngoại lệ nào được ném, nhưng bạn có thể muốn bảo vệ khỏi việc tạo một tệp gần như trống:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Bảng màu tùy chỉnh

Bạn muốn sọc xanh/đậm thay vì vàng/trắng? Chỉ cần thay thế các giá trị `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Cứ tự do lấy màu từ tệp cấu hình để những người không phải lập trình viên có thể điều chỉnh bảng màu mà không cần chạm vào mã.

### Tái sử dụng Styles trên nhiều Worksheet

Nếu bạn xuất nhiều bảng vào cùng một workbook, bạn có thể tạo mảng style một lần và tái sử dụng nó:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Chỉ cần chú ý rằng cả hai bảng đều có cùng số hàng, hoặc tạo một mảng mới cho mỗi sheet.

---

## Ví dụ làm việc đầy đủ

Kết hợp mọi thứ lại, đây là một chương trình tự chứa mà bạn có thể sao chép‑dán vào một ứng dụng console.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Chạy chương trình, mở `Report.xlsx`, và bạn sẽ thấy nền xen kẽ chính xác như mô tả.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}