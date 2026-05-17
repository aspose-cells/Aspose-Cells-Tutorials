---
category: general
date: 2026-02-21
description: Học cách định dạng các cột khi nhập DataTable vào Excel bằng C#. Bao
  gồm các mẹo để tô màu cột thứ hai trong Excel và nhập DataTable vào Excel bằng C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: vi
og_description: Cách định dạng cột khi nhập DataTable vào Excel bằng C#. Mã từng bước,
  tô màu cột thứ hai trong Excel và các thực tiễn tốt nhất.
og_title: Cách Định Dạng Cột trong Excel bằng C# – Hướng Dẫn Toàn Diện
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Cách định dạng các cột trong Excel bằng C# – Nhập DataTable
url: /vi/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Dạng Các Cột trong Excel bằng C# – Nhập DataTable

Bạn đã bao giờ tự hỏi **cách định dạng các cột** trong một worksheet Excel khi lấy dữ liệu trực tiếp từ `DataTable` chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần một chút màu nhanh—có thể là màu đỏ cho cột đầu tiên, màu xanh cho cột thứ hai—mà không phải chỉnh sửa từng ô một sau khi nhập.  

Tin tốt? Câu trả lời chỉ cần vài dòng mã C#, và bạn sẽ có một bảng tính được định dạng đầy đủ ngay khi dữ liệu được nhập. Trong hướng dẫn này, chúng tôi cũng sẽ đề cập đến **import datatable to excel**, cho bạn thấy **color second column excel**, và giải thích tại sao cách tiếp cận này hoạt động cho cả dự án .NET Framework và .NET 6+.

---

## Những Điều Bạn Sẽ Học

- Lấy một `DataTable` đã được điền dữ liệu (hoặc tạo mới ngay tại chỗ).  
- Định nghĩa các đối tượng `Style` cho từng cột để đặt màu chữ.  
- Tạo một workbook, lấy worksheet đầu tiên, và nhập bảng với các style đã áp dụng.  
- Xử lý các trường hợp đặc biệt như bảng trống, dòng bắt đầu tùy chỉnh, và số cột động.  

Khi kết thúc, bạn sẽ có thể đưa một file Excel đã được định dạng vào bất kỳ quy trình báo cáo nào—không cần xử lý sau.

> **Điều kiện tiên quyết:** Hiểu biết cơ bản về C# và một thư viện bảng tính hỗ trợ `ImportDataTable` (ví dụ: Aspose.Cells, GemBox.Spreadsheet, hoặc EPPlus với một helper). Đoạn mã dưới đây sử dụng **Aspose.Cells** vì overload `ImportDataTable` của nó chấp nhận trực tiếp một `Style[]`.

## Bước 1: Thiết Lập Dự Án và Thêm Thư Viện Excel

Trước khi chúng ta có thể định dạng bất kỳ thứ gì, chúng ta cần một dự án tham chiếu tới một thư viện thao tác Excel.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Mẹo:* Nếu bạn đang dùng .NET 6, thêm gói bằng lệnh `dotnet add package Aspose.Cells`. Thư viện hoạt động trên Windows, Linux và macOS, vì vậy bạn sẽ an toàn cho tương lai.

## Bước 2: Lấy Hoặc Tạo DataTable Nguồn

Mục tiêu chính của hướng dẫn là định dạng, nhưng bạn vẫn cần một `DataTable`. Dưới đây là một hàm trợ giúp nhanh tạo dữ liệu mẫu; hãy thay thế nó bằng lời gọi `GetTable()` của bạn trong môi trường thực tế.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Tại sao điều này quan trọng:** Sử dụng `DataTable` giúp nguồn dữ liệu của bạn không phụ thuộc—dù đến từ SQL, CSV, hay một bộ sưu tập trong bộ nhớ, logic nhập vẫn giống nhau. Đây là nền tảng của **how to import datatable** một cách hiệu quả.

## Bước 3: Định Nghĩa Style Cho Các Cột (Trọng Tâm của “Cách Định Dạng Các Cột”)

Bây giờ chúng ta chỉ cho worksheet biết mỗi cột sẽ trông như thế nào. Lớp `Style` cho phép bạn đặt phông chữ, màu sắc, viền, và hơn thế nữa. Trong ví dụ này, chúng ta chỉ thay đổi màu chữ.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*Nếu bạn có nhiều cột hơn?* Chỉ cần tăng kích thước mảng và điền các style bạn muốn. Các cột không được định dạng sẽ tự động kế thừa style mặc định của worksheet.

## Bước 4: Tạo Workbook và Nhập DataTable Với Các Style

Khi dữ liệu và style đã sẵn sàng, đã đến lúc kết hợp mọi thứ lại.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**Chuyện gì vừa xảy ra?**  
- `ImportDataTable` sao chép các hàng, cột, và *tùy chọn* hàng tiêu đề.  
- Bằng cách truyền `columnStyles`, mỗi cột sẽ nhận được `Style` mà chúng ta đã định nghĩa trước đó.  
- Lệnh này chỉ một dòng, có nghĩa là **import datatable excel c#** đơn giản như vậy.

## Bước 5: Kiểm Tra Kết Quả – Kết Quả Mong Đợi

Mở `StyledDataTable.xlsx` trong Excel (hoặc LibreOffice). Bạn sẽ thấy:

| **ID** (red) | **Name** (blue) | **Score** (default) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- Văn bản của cột đầu tiên hiển thị màu **đỏ**, đáp ứng yêu cầu “cách định dạng các cột”.  
- Văn bản của cột thứ hai là màu **xanh**, cũng đáp ứng truy vấn **color second column excel**.

Nếu file mở mà không có lỗi, bạn đã thành công trong việc **how to import datatable** đồng thời định dạng các cột.

## Câu Hỏi Thường Gặp & Các Trường Hợp Đặc Biệt

### Nếu DataTable trống thì sao?

`ImportDataTable` vẫn sẽ tạo hàng tiêu đề (nếu bạn truyền `true`). Không có hàng dữ liệu nào được thêm, nhưng các style vẫn áp dụng cho các ô tiêu đề.

### Cần bắt đầu nhập ở ô khác?

Thay đổi các tham số `rowIndex` và `columnIndex` trong `ImportDataTable`. Ví dụ, để bắt đầu tại `B2` dùng `1, 1` thay vì `0, 0`.

### Muốn định dạng hàng thay vì cột?

Bạn có thể lặp qua `worksheet.Cells.Rows` sau khi nhập và gán một `Style` cho mỗi hàng. Tuy nhiên, việc định dạng ở mức cột hiệu suất cao hơn nhiều vì thư viện áp dụng style một lần cho mỗi cột.

### Sử dụng EPPlus hoặc ClosedXML?

Các thư viện đó không cung cấp overload `ImportDataTable` trực tiếp với một mảng style. Giải pháp là nhập bảng trước, sau đó duyệt qua phạm vi cột và đặt `Style.Font.Color.SetColor(...)`. Logic vẫn giống, chỉ có thêm vài dòng mã.

## Mẹo Chuyên Nghiệp cho Mã Sẵn Sàng Sản Xuất

- **Tái sử dụng Styles:** Tạo một `Style` mới cho mỗi cột có thể lãng phí. Lưu các style có thể tái sử dụng trong một dictionary theo màu hoặc độ đậm phông.  
- **Tránh Đếm Cột Cố Định:** Phát hiện `dataTable.Columns.Count` và xây dựng mảng `columnStyles` một cách động.  
- **An Toàn Khi Đa Luồng:** Nếu bạn tạo nhiều workbook đồng thời, khởi tạo một `Workbook` riêng cho mỗi luồng; các đối tượng Aspose.Cells không an toàn với đa luồng.  
- **Hiệu Suất:** Đối với bảng lớn hơn 10 k hàng, cân nhắc tắt `AutoFitColumns` (nó quét mọi ô) và đặt độ rộng cột thủ công.

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Chạy chương trình, mở file `StyledDataTable.xlsx` đã tạo, và bạn sẽ ngay lập tức thấy các cột được tô màu. Đó là toàn bộ quy trình **import datatable excel c#** trong một cái nhìn tổng quan.

## Kết Luận

Chúng tôi vừa trình bày **cách định dạng các cột** khi bạn **import datatable to excel** bằng C#. Bằng cách định nghĩa một mảng `Style[]` và truyền nó vào `ImportDataTable`, bạn có thể tô màu cột đầu tiên đỏ, cột thứ hai xanh, và để các cột còn lại không thay đổi—tất cả chỉ trong một dòng mã.

Cách tiếp cận này có thể mở rộng: thêm nhiều đối tượng `Style` cho các cột bổ sung, điều chỉnh dòng bắt đầu, hoặc thay thế Aspose.Cells bằng thư viện khác có API tương tự. Giờ đây bạn có thể tạo các báo cáo Excel chuyên nghiệp mà không cần chỉnh sửa file thủ công.

**Các bước tiếp theo** bạn có thể khám phá:

- Sử dụng **conditional formatting** để làm nổi bật giá trị một cách động (liên quan tới “color second column excel”).  
- Xuất nhiều worksheet từ một tập hợp `DataTable` duy nhất (tuyệt vời cho bảng điều khiển hàng tháng).  
- Kết hợp điều này với việc chuyển **CSV → DataTable** để xây dựng một quy trình đầu‑cuối‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}