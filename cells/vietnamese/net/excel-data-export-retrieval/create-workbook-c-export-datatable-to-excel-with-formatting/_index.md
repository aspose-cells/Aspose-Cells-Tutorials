---
category: general
date: 2026-02-15
description: Tạo workbook C# và xuất DataTable sang Excel với định dạng hàng, đặt
  nền cho hàng, và tự động hoá các tác vụ Excel trong vài phút.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: vi
og_description: Tạo workbook C# nhanh chóng, áp dụng kiểu dòng, và tự động xuất Excel
  với các ví dụ mã đầy đủ và mẹo thực hành tốt nhất.
og_title: Tạo Workbook C# – Xuất DataTable sang Excel với Định dạng
tags:
- C#
- Excel
- DataExport
title: Tạo Workbook C# – Xuất DataTable ra Excel với Định dạng
url: /vi/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook C# – Xuất DataTable ra Excel với Định dạng

Bạn đã bao giờ cần **create workbook C#** và xuất một `DataTable` ra Excel với định dạng tùy chỉnh chưa? Bạn không phải là người duy nhất. Trong nhiều ứng dụng doanh nghiệp, yêu cầu là tạo ra một bảng tính được định dạng đẹp mắt mà người dùng không chuyên có thể mở và hiểu ngay lập tức.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy, cho bạn thấy **how to create workbook C#**, áp dụng **excel export formatting**, đặt **row background**, và tận dụng **excel automation c#** để tạo ra một tệp hoàn thiện. Không có các phím tắt mơ hồ “xem tài liệu”—chỉ có mã đầy đủ, giải thích lý do mỗi dòng quan trọng, và các mẹo bạn sẽ thực sự dùng ngay ngày mai.

---

## Yêu cầu trước

- .NET 6 (hoặc .NET Framework 4.6+).  
- Visual Studio 2022 hoặc bất kỳ IDE nào hỗ trợ C#.  
- Gói NuGet **Aspose.Cells for .NET** (hoặc bất kỳ thư viện nào cung cấp `Workbook`, `Worksheet`, `Style`).  
- Kiến thức cơ bản về `DataTable`.  

Nếu bạn chưa có Aspose.Cells, chạy:

```bash
dotnet add package Aspose.Cells
```

> **Mẹo chuyên nghiệp:** Bản dùng thử miễn phí hoạt động cho hầu hết các kịch bản phát triển; chỉ cần nhớ thay thế khóa giấy phép trước khi phát hành.

![Ví dụ tạo workbook C# hiển thị các hàng được định dạng trong Excel]( "Ví dụ tạo workbook C# với màu nền cho các hàng")

---

## Bước 1: Khởi tạo Workbook và Worksheet (Create Workbook C#)

Điều đầu tiên bạn phải làm là tạo một đối tượng `Workbook`. Hãy nghĩ nó như việc mở một tệp Excel mới hoàn toàn trong bộ nhớ.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Tại sao?**  
`Workbook` chứa toàn bộ tài liệu Excel, trong khi `Worksheet` đại diện cho một tab duy nhất. Bắt đầu với một workbook sạch sẽ giúp bạn kiểm soát mọi khía cạnh của đầu ra—không có kiểu mặc định ẩn nào lén lút.

---

## Bước 2: Chuẩn bị một DataTable mẫu (Export DataTable Excel)

Trong một dự án thực tế, bạn sẽ lấy dữ liệu từ cơ sở dữ liệu, nhưng để minh họa chúng ta sẽ tạo một `DataTable` nhỏ ngay trong mã.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Tại sao điều này quan trọng:**  
Xuất một `DataTable` là cách phổ biến nhất để chuyển dữ liệu dạng bảng từ ứng dụng sang Excel. Phương thức trên hoàn toàn độc lập, vì vậy bạn có thể sao chép‑dán nó vào bất kỳ dự án nào và nó sẽ hoạt động.

---

## Bước 3: Tạo Style cho mỗi hàng (Excel Export Formatting)

Để mỗi hàng có màu nền riêng, chúng ta tạo một đối tượng `Style` cho mỗi hàng trong `DataTable`. Đây là nơi **excel export formatting** tỏa sáng.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Tại sao lại định dạng theo hàng?**  
Nếu bạn cần làm nổi bật các bản ghi cụ thể (ví dụ: hoá đơn quá hạn) bạn có thể thay thế vòng màu đơn giản bằng logic điều kiện—chỉ cần đặt `style.ForegroundColor` dựa trên dữ liệu của hàng.

---

## Bước 4: Nhập DataTable với Style cho hàng (Set Row Background)

Bây giờ chúng ta kết hợp mọi thứ lại: dữ liệu, workbook và các style.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Bạn sẽ thấy:**  
Mở `EmployeesReport.xlsx` sẽ hiển thị một hàng tiêu đề với định dạng mặc định, tiếp theo là bốn hàng dữ liệu mỗi hàng được tô màu nền nhẹ. Kết quả trông như một báo cáo được tạo thủ công, không phải một bản xuất thô.

---

## Bước 5: Mẹo Nâng cao về Excel Automation C# (Excel Automation C#)

Dưới đây là một vài mẹo nhanh bạn có thể áp dụng lên ví dụ cơ bản:

| Mẹo | Đoạn mã | Khi nào sử dụng |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Sau khi nhập dữ liệu để tránh văn bản bị cắt ngắn. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Khi bảng có thể cuộn vượt quá màn hình. |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Làm nổi bật mức lương trên một ngưỡng. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Khi bạn cần báo cáo chỉ đọc. |

Các đoạn mã này thể hiện phạm vi của **excel automation c#**—bạn có thể tiếp tục mở rộng workbook mà không cần viết lại logic nhập dữ liệu cốt lõi.

---

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

**Nếu DataTable có hàng nghìn?**  
Aspose.Cells truyền dữ liệu một cách hiệu quả, nhưng bạn có thể muốn tắt việc tạo style cho mỗi hàng để tiết kiệm bộ nhớ. Thay vào đó, áp dụng một style duy nhất cho một phạm vi:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Tôi có thể xuất ra .csv thay vì .xlsx không?**  
Chắc chắn—chỉ cần thay đổi định dạng lưu:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Định dạng sẽ bị mất (CSV không hỗ trợ style), nhưng việc xuất dữ liệu vẫn giữ nguyên.

**Điều này có hoạt động trên .NET Core không?**  
Có. Aspose.Cells hỗ trợ .NET Standard 2.0 và các phiên bản sau, vì vậy cùng một đoạn mã có thể chạy trên .NET 6, .NET 7, hoặc .NET Framework.

---

## Ví dụ Hoàn chỉnh (Sẵn sàng Sao chép‑Dán)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Tạo một workbook mới – cốt lõi của create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Xuất DataTable với định dạng
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Nhập dữ liệu với style cho hàng – đặt nền cho hàng (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Tinh chỉnh tùy chọn
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}